# Aesir Architecture 特性一览

## ObservableValue\<T\> — 响应式属性

Model 持有可写实例,View 经 `IReadOnlyObservableValue<T>` 只读订阅,读写分离由类型系统闭环:

```csharp
// Model 内部持有与写入
[SerializeField] ObservableValue<int> count = new ObservableValue<int>(0);
public IReadOnlyObservableValue<int> Count => count;
count.Value++;            // 写入并通知

// View 订阅(推荐 AddListenerAndInvoke:订阅即同步初始值)
model.Count.AddListenerAndInvoke(OnCountChanged)
    .RemoveListenerWhenGameObjectOnDestroyed(gameObject);

// 静默设置(不触发通知)
count.SetValueSilently(5);
```

**可观察集合家族**:`ObservableList<T>` / `ObservableDictionary<TKey, TValue>` / `ObservableHashSet<T>` 提供单轨变更通知 `AddListener`——无变更不通知、批量操作逐项通知、Sort / Reverse / Clear 走 Reset、监听句柄可绑定 Unity 生命周期自动移除,与 ObservableValue 同一套读写分离与句柄模式。队列等其他集合形态与同步视图 / R3 集成等高级能力不做,需要时推荐 [Cysharp/ObservableCollections](https://github.com/Cysharp/ObservableCollections)——两者可共存(程序集与命名空间完全隔离,同一项目可同时安装)。

## MiniEvent — 零分配轻量事件

直接多播调用、Invoke 路径零分配,异常语义 = 原生 C# 事件(fail-fast)。`AddListener` 返回 `AutoRemoveListenerHandle`,泄漏防护是 API 形态:

```csharp
MiniEvent doorOpened = new MiniEvent();
doorOpened.AddListener(OnDoorOpened)
    .RemoveListenerWhenGameObjectOnDestroyed(gameObject);   // 或 RemoveListenerWhenGameObjectOnDisable(UI 面板)
doorOpened.Invoke();
```

多参数载荷用 struct 包裹成单参事件。**监听回调不应抛异常**(框架约定):一个监听者抛异常会中断同事件后续监听者,业务异常在回调内部自行处理。

## 通知机制选型

每个场景有且只有一个默认答案 —— 不要在选择中瘫痪:

| 场景 | 推荐 | 理由 |
|------|------|------|
| Model 状态变了要通知外界(血量、分数) | `ObservableValue<T>` | 状态即数据;`AddListenerAndInvoke` 保证新订阅者拿到当前值 |
| 一次性 / 瞬时通知,无状态("门开了") | `MiniEvent` / `MiniEvent<T>` | 零分配直调,句柄即泄漏防护 |
| View 把输入暴露给 Presenter(MVP 内部) | 原生 C# `event` | 编译期限制外部只能 `+=` / `-=` |
| Inspector 拖拽连线的 UI 交互 | `UnityEvent` | 可视化配置,美术 / 策划可调 |

反模式:用 `public Action Xxx { get; set; }` 代替 `event`(外部可整体替换 / 置空 / 触发);用 MiniEvent 承载持续变化的状态(新订阅者拿不到当前值)。

## PlayerLoop 原生生命周期 {#playerloop-hooks}

`AesirPlayerLoop` 将自定义子系统注入 Unity PlayerLoop,无需 MonoBehaviour:

```csharp
AesirPlayerLoop.Register(
    AesirLifecyclePhase.BeforeUpdate, MyFrameCallback);

// 第三方 SDK 修改 PlayerLoop 后调用一次即可自愈(Register 期也会自动检测)
AesirPlayerLoop.EnsureInjected();
```

可用阶段:`BeforeUpdate`(Update 前)、`AfterUpdate`(PostLateUpdate 后)。

## 延时与下一帧

框架不内置时间调度原语(0.30.0 起连帧粒度调度器也已整体移除,原 `AesirScheduler` 全仓零使用)。需要"延时执行"时有两条现成路径:

```csharp
// ① 纯 C# 对象:用生命周期代理拿到帧回调,配合计时字段自行判定(无场景物体)
MonoLifecycleProxy.Instance.AddListener(MonoLifecycleEvent.Update, OnTick);

// ② 需要协程语义时,把驱动方挂在 GameObject 上,用 Unity 原生协程
yield return new WaitForSeconds(3f);
```

帧驱动本身由 [PlayerLoop 帧钩子](#playerloop-hooks) 提供(每帧持续调用直到注销);"到点调一次"属于业务层的计时字段,不再由框架代管。
## MonoLifecycleProxy — 生命周期代理

将 Unity 原生回调统一为可订阅的 MiniEvent;调用期增删监听为**快照语义**(挂起队列趟末应用,对齐原生多播委托),稳态零分配。PlaneWar 示例中与 MiniEvent、ObservableValue 组合运用。

## DDOL 显式决策

根单例(AesirArchitecture 等)的 `dontDestroyOnLoad` 序列化字段统一控制预放置 / 运行时两种来源:默认跨场景持久;关闭时随场景卸载销毁(Inspector 警告 + 运行时提醒),多场景叠加加载自行处理。

## Domain Reload 安全(铁律)

静态变量全部显式重置:非泛型类内 `[RuntimeInitializeOnLoadMethod]` 自重置;泛型类经 `ResetStaticsAssistant.Register()` 注册(泛型类 RIOLM 被 Unity 静默跳过,助手补位)。反复进出 Play Mode 无残留。

## 纯 C# 核心 + MonoBehaviour 适配层

Engine 层零 MonoBehaviour 依赖,适配层按需选用:

| 基类 | 能力 | 用途 |
|------|------|------|
| `MonoView<T>` | GetModel, GetService(只读) | MVC Standard / Strict 的 View |
| `MonoViewController<T>` | + ExecuteCommand, ExecuteQuery | MVC Quick 的 View 兼 Controller |
| `AesirView<T>` / `AesirViewController<T>` | 同上 + Odin 增强 | 需要 Odin 时(功能相同,体验更好) |

## GenericLocator\<T\> — 类型键控定位器

按类型注册 / 查询的通用定位器,按注册顺序保序,Context 内部与独立场景均可使用。

## 包内更新器

`Tools → Aesir → Check for Updates`:多源版本检测(直连 GitHub 三层 → 镜像站 → CDN 中转,大陆友好)、按"上次安装清单 − 新版清单"精确差集清理残留(导入成功之后执行)、不误伤用户新增文件、域重载中断安全。

## Odin Inspector 可选集成

经 `ODIN_INSPECTOR` 条件编译,独立 asmdef 隔离。**三条铁律**:核心架构流程闭环(Context 注册 → 初始化 → Command/Query → ObservableValue 通知)无 Odin 可完整运行;调试体验优化品可用 Odin;样式优化与代码逻辑分离(AttributeProcessor 动态注入,运行时程序集零样式特性)。