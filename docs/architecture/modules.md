# 内置功能模块

Aesir Architecture 的运行时代码由三层组成:**架构核心**(Core —— Context 与 MVC / MVP 角色)、**内置功能模块**(Modules —— 本页主角)、**基础设施**(Common)。五个内置功能模块与架构角色解耦 —— [MiniEvent](#module-event)、Observable 家族、[GenericLocator](#module-locator)、[AesirScheduler](#module-aesir-scheduler) 均为纯 C# 类型,不依赖 Context 或场景物体即可独立使用;同时又深度服务于核心架构(Context 用 GenericLocator 托管注册表,Model 用 ObservableValue 承载数据)。

## 组成地图

| 层 | 源码目录 | 内容 |
|----|---------|------|
| 架构核心 | `Runtime/Core` | 能力接口、Context 上下文、MVC / MVP 角色与 MonoBehaviour 适配基类,详见[架构概念](concepts.md) |
| 内置功能模块 | `Runtime/Modules` | Event / Observable / CustomLifecycle / Locator / Utilities,本页逐模块详解 |
| 基础设施 | `Runtime/Common` | 单例宿主、架构基类、日志工具、静态重置助手,见[本页末节](#module-common) |

五个内置功能模块一览:

| 模块 | 源码目录 | 核心类型 | 作用 |
|------|---------|---------|------|
| **Event 事件** | `Modules/Event` | [MiniEvent](scripting-api/Runestone/AesirArchitecture/MiniEvent.md) / [MiniEvent\<T\>](scripting-api/Runestone/AesirArchitecture/MiniEvent{T}.md) | 零分配轻量事件 + 自动移除监听体系 |
| **Observable 可观察** | `Modules/Observable` | [ObservableValue\<T\>](scripting-api/Runestone/AesirArchitecture/ObservableValue{T}.md) + List / Dictionary / HashSet 三件套 | 响应式属性与可观察集合,读写分离由类型系统闭环 |
| **CustomLifecycle 自定义生命周期** | `Modules/CustomLifecycle` | [MonoLifecycleProxy](scripting-api/Runestone/AesirArchitecture/MonoLifecycleProxy.md) + ICustom* 接口家族 | 把 Unity 原生回调统一为可订阅事件,任意对象可接入 |
| **Locator 定位器** | `Modules/Locator` | [GenericLocator\<T\>](scripting-api/Runestone/AesirArchitecture/GenericLocator{T}.md) | 按类型注册 / 查询 / 获取实例,注册顺序保序 |
| **Utilities 工具** | `Modules/Utilities` | [AesirArchitecturePlayerLoop](scripting-api/Runestone/AesirArchitecture/AesirArchitecturePlayerLoop.md) / AesirScheduler / [PlayerLoopUtility](scripting-api/Runestone/AesirArchitecture/PlayerLoopUtility.md) | 游戏级帧钩子、帧粒度时间调度、PlayerLoop 自由扩展 |

---

## Event — 零分配事件模块 {#module-event}

**作用**:提供一套零分配的轻量事件原语,并用"句柄 + 触发器"的 API 形态把监听泄漏防护做进类型系统 —— 忘记移除监听不再靠自觉,而是靠生命周期绑定。

### MiniEvent 与 MiniEvent\<T\>

直接多播调用,Invoke 路径稳态零分配;异常语义 = 原生 C# 事件(fail-fast):一个监听者抛异常会中断同事件后续监听者,因此**监听回调不应抛异常**(框架约定),业务异常在回调内部自行处理:

```csharp
MiniEvent doorOpened = new MiniEvent();
MiniEvent<int> scoreChanged = new MiniEvent<int>();

doorOpened.AddListener(OnDoorOpened);          // 返回 AutoRemoveListenerHandle
scoreChanged.Invoke(10);
```

`AddListener` 返回 [`AutoRemoveListenerHandle`](scripting-api/Runestone/AesirArchitecture/AutoRemoveListenerHandle.md) —— 实现 `IDisposable` 的 struct,配合 `using` 语句可在作用域结束时自动移除监听,重复 Dispose 安全。多参数载荷用 struct 包裹成单参事件。

### 自动移除监听体系

句柄有三条自动清理路径,按"谁销毁谁负责"各取所需:

| 扩展方法([RemoveListenerExtensions](scripting-api/Runestone/AesirArchitecture/RemoveListenerExtensions.md)) | 触发时机 | 典型场景 |
|----------|---------|---------|
| `RemoveListenerWhenGameObjectOnDestroyed` | GameObject 销毁时 | 场景物体上的订阅 |
| `RemoveListenerWhenGameObjectOnDisable` | GameObject 禁用时 | UI 面板(缓存复用,不销毁) |
| `RemoveListenerWhenOnSceneUnloaded` | 场景卸载时 | 场景级订阅 |

```csharp
model.Count.AddListenerAndInvoke(OnCountChanged)
    .RemoveListenerWhenGameObjectOnDestroyed(gameObject);
```

底层由三个 MonoBehaviour 触发器组件支撑:`RemoveListenerOnDestroyTrigger` / `RemoveListenerOnDisableTrigger`(挂在订阅者物体上,按需懒挂载)、`RemoveListenerOnSceneUnloadedTrigger`(挂在 [Aesir Architecture] 宿主上,按 `Scene.handle` 分桶 —— 场景 A 卸载不误杀场景 B 的监听,同名场景各持唯一句柄互不共享桶);`RemoveListenerHandleCollection` 负责句柄的批量收集与一次性清理。

### 能力边界

不做事件总线 / EventChannel —— 跨模块通信用互相 GetModel + ObservableValue 订阅,或直接引用 MiniEvent(设计边界详见[架构概念](concepts.md));不做异常吞噬(保持零分配与原生语义)。

---

## Observable — 可观察模块 {#module-observable}

**作用**:把"状态 + 变更通知"做成类型 —— 持有方拿到可写实例,外界经只读接口订阅变化,读写分离不靠约定而靠类型系统闭环。这是 Model 数据层的标准载体,也可脱离架构单独使用。

### ObservableValue\<T\> 响应式属性

```csharp
// Model 内部:持有可写实例,只读暴露
[SerializeField] ObservableValue<int> count = new ObservableValue<int>(0);
public IReadOnlyObservableValue<int> Count => count;

count.Value++;                 // 值变化才通知
count.SetValueSilently(5);     // 静默设置,适合初始化 / 存档回填

// View 订阅:AddListenerAndInvoke 订阅即同步当前值
model.Count.AddListenerAndInvoke(OnCountChanged)
    .RemoveListenerWhenGameObjectOnDestroyed(gameObject);
```

只读接口 `IReadOnlyObservableValue<out T>` 为协变设计(泛型参数仅出现在逆变位,双重逆变抵消)。安装 Odin Inspector 时有自定义 Drawer,可在 Inspector 直接编辑与预览值变更。

### 可观察集合家族

[ObservableList\<T\>](scripting-api/Runestone/AesirArchitecture/ObservableList{T}.md) / [ObservableDictionary\<TKey, TValue\>](scripting-api/Runestone/AesirArchitecture/ObservableDictionary{TKey, TValue}.md) / [ObservableHashSet\<T\>](scripting-api/Runestone/AesirArchitecture/ObservableHashSet{T}.md) —— 组合 BCL 集合存储 + MiniEvent 事件,与 ObservableValue 同一套读写分离与句柄模式:

| 集合 | 变更事件 | 事件参数 |
|------|---------|---------|
| `ObservableList<T>` | Added / Removed / Replaced / Cleared | `CollectionAddEventArgs<T>` 等 readonly struct(含 Index / Item / OldItem / NewItem) |
| `ObservableDictionary<TKey, TValue>` | Added / Removed / Updated / Cleared | Added / Removed 直传 `KeyValuePair`,Updated 用 `DictionaryUpdateEventArgs`(含 Key / OldValue / NewValue) |
| `ObservableHashSet<T>` | Added / Removed / Cleared | 单值直传 `Action<T>` |

事件参数约定:**单值载荷直传,多字段才造结构体 EventArgs** —— 不为单值引入 EventArgs 类型。

### 不变型只读接口(有意设计)

只读接口(`IReadOnlyObservableList<T>` 等)无 `out`、为不变型:结构体事件参数与协变冲突(CS1961),这是有意取舍而非疏漏。Move / Sort / 同步视图等高级能力不做,需要时推荐 [Cysharp/ObservableCollections](https://github.com/Cysharp/ObservableCollections)(MIT)。

深入用法见[响应式与事件](observable.md)。

---

## CustomLifecycle — 自定义生命周期模块 {#module-customlifecycle}

**作用**:把 Unity 原生 MonoBehaviour 回调"翻译"成可订阅的 MiniEvent —— 任意对象(不必是 MonoBehaviour、不必挂在场景里)都能接收生命周期驱动,普通 C# 类由此获得逐帧驱动能力。

### MonoLifecycleProxy 生命周期代理

单例组件,提供两种接入方式:

```csharp
// 方式 1:按事件订阅(order 越小越先执行,同 order 按注册顺序 —— 稳定排序)
MonoLifecycleProxy.Instance.AddListener(MonoLifecycleEvent.Update, MyTick, order: 0);

// 方式 2:实现 ICustom* 接口后自动注册(扫描接口,免手工对表)
MonoLifecycleProxy.Register(this as MonoBehaviour);      // MonoBehaviour:GameObject 销毁时自动取消订阅
this.RegisterCustomLifecycle();                          // 扩展方法形式
```

可订阅 [`MonoLifecycleEvent`](scripting-api/Runestone/AesirArchitecture/MonoLifecycleEvent.md) 共 8 个事件:

| 事件 | 驱动来源 |
|------|---------|
| `FixedUpdate` / `Update` / `LateUpdate` | Unity 原生回调(经宿主 MonoBehaviour) |
| `BeforeUpdate` / `AfterUpdate` | PlayerLoop 钩子(早于当帧全部 Update / 晚于 PostLateUpdate) |
| `OnApplicationFocus` / `OnApplicationPause` / `OnApplicationQuit` | Unity 原生回调 |

### ICustom* 接口家族

每个事件对应一个接口(`ICustomFixedUpdate` / `ICustomBeforeUpdate` / `ICustomUpdate` / `ICustomLateUpdate` / `ICustomAfterUpdate` / `ICustomOnApplicationFocus` / `ICustomOnApplicationPause` / `ICustomOnApplicationQuit`),方法名以 `OnCustom` 前缀区分 Unity 原生回调。实现任意接口的对象经 `RegisterAuto` 自动注册到匹配事件;MonoBehaviour 经 `Register(MonoBehaviour)` 注册还会在 GameObject 销毁时自动取消订阅。

### 快照语义

调用期增删监听为**快照语义**:遍历期间的增删先挂进待处理队列,趟末按发生顺序统一应用 —— 对齐原生多播委托语义,监听者在回调中安全地增删监听,不会跳帧或抛集合修改异常;复用挂起队列,稳态零分配。

---

## Locator — 类型键控定位器模块 {#module-locator}

**作用**:按类型注册 / 查询 / 获取对象实例的通用定位器,是 Context 注册表的底层实现,也可独立用作轻量服务定位。

```csharp
var locator = new GenericLocator<IWeapon>();
locator.Register(new Sword());        // 以 typeof(Sword) 为键
locator.Get<Sword>().Attack();        // 注册与查询必须使用相同的类型参数
locator.GetAll();                     // 按注册顺序枚举
locator.Unregister<Sword>();          // 注销后再注册,追加到顺序末尾
```

### 保序与键匹配规则

- **注册顺序保序** —— `GetAll` 按插入顺序枚举,由显式顺序列表提供结构保证(不依赖 Dictionary 枚举顺序这一无契约保证的实现细节);Context 的"按注册顺序初始化 Model → Service、逆序 Dispose"即建立在此之上
- **键精确匹配** —— 以 `typeof(TItem)` 为键,注册与查询必须使用相同类型参数(按实现类注册、按接口获取会 miss)
- **覆盖不移位** —— 重复注册覆盖实例但不改变原位置;`Unregister` 后再注册按新插入语义追加到末尾
- `[Serializable]` + `IDisposable`,`Dispose` 清空全部注册

架构内用法:`AbstractContext<T>` 内部持有两个 `GenericLocator<T>` 实例分别管理 IModel 与 IService;独立用法:任何需要"类型 → 实例"注册表的场景(如局部对象池登记、编辑器工具)。

---

## Utilities — 工具模块 {#module-utilities}

**作用**:封装 Unity PlayerLoop 这一引擎底层能力,为纯 C# 代码(无 MonoBehaviour)提供游戏级帧驱动与延时手段 —— 架构里的 Model / Service / Command 不持有协程,延时需求在这里闭环。

### AesirArchitecturePlayerLoop — 游戏级帧钩子

无需 MonoBehaviour,把回调注入 PlayerLoop 的两个阶段:

| 阶段 | 插入点 | 典型用途 |
|------|--------|---------|
| `BeforeUpdate` | `PlayerLoop.Update` 之前 | 架构逻辑优先运算(早于当帧全部 Update) |
| `AfterUpdate` | `PlayerLoop.PostLateUpdate` 之后 | 读取当前帧最终状态 |

```csharp
AesirArchitecturePlayerLoop.Register(
    AesirArchitectureLifecyclePhase.BeforeUpdate, MyFrameCallback, order: 0);  // 返回句柄
```

- **注入自愈** —— 第三方 SDK 用缓存副本 `SetPlayerLoop` 会抹掉注入点;`EnsureInjected()` 在域加载时与每次 Register 时自动补插,也可手动调用
- **稳定排序** —— `order` 越小越先执行,同 order 按注册顺序
- **趟末生效** —— 遍历期间 Register / Unregister 缓存到趟末统一执行

### AesirScheduler — 帧粒度时间调度(0.21.0 新增) {#module-aesir-scheduler}

纯 C# 静态 API,为无协程能力的 Model / Service / Command 提供合法的延时执行手段;任务经 BeforeUpdate 钩子结算,无需任何场景物体,首次使用自动注册钩子:

```csharp
AesirScheduler.Delay(3f, () => Debug.Log("3 秒后(帧粒度)"));
AesirScheduler.NextFrame(() => RefreshView());   // 下一帧执行,等价于 Delay(0f)
int pending = AesirScheduler.PendingCount;        // 待结算任务数
```

有意收窄的能力边界:

| 边界 | 含义 |
|------|------|
| 帧粒度 | 计时按帧结算,`Delay(0.05f)` 在 60fps 下约 3-4 帧后触发;所有任务最早下一帧执行(含 `Delay(0)`,不做同帧投递) |
| 游戏时间 | 计时基于 `Time.time`,受 `timeScale` 影响(`timeScale = 0` 期间暂停计时) |
| 一次性任务 | 无句柄、无取消、无暂停、不池化;高频反复调度请评估直接持有句柄型事件 |
| 仅主线程 | 框架铁律;从异步回调访问请先调度回主线程 |

语义要点:回调内再调度的新任务从下一帧开始参与结算;回调不应抛异常(fail-fast —— 抛出时异常向上传播由 PlayerLoop 捕获记日志,本趟后续任务跳过且不补投递);`seconds` 为 NaN 时不设防(任务永不触发,极简原则);任务列表与结算缓冲复用,稳态零分配,空队列时钩子零成本直接返回。

### PlayerLoopUtility — PlayerLoop 自由扩展

PlayerLoop 操作的静态工具类,供框架内外扩展使用,不局限于上面的预定义阶段:

- `InsertSystemBefore<TTarget>(system)` / `InsertSystemAfter<TTarget>(system)` —— 在指定子系统(如 `typeof(UnityEngine.PlayerLoop.Update)`)前后插入自定义系统
- `ContainsSystem<T>()` —— 查询子系统是否已存在

---

## Common — 基础设施 {#module-common}

不属于功能模块,但是模块运转的地基:

| 类型 | 作用 |
|------|------|
| [AesirArchitecture](scripting-api/Runestone/AesirArchitecture/AesirArchitecture.md) | MonoBehaviour 单例宿主,承载框架挂载型组件(MonoLifecycleProxy、场景卸载触发器等),`[DefaultExecutionOrder(-999)]` 确保宿主尽早完成去重与 DDOL 决策;`dontDestroyOnLoad` 序列化字段统一控制预放置 / 运行时两种来源的跨场景持久;**不初始化任何架构数据**(Context 是纯 C# 懒加载单例) |
| [AesirMonoBehaviour](scripting-api/Runestone/AesirArchitecture/AesirMonoBehaviour.md) / [AesirScriptableObject](scripting-api/Runestone/AesirArchitecture/AesirScriptableObject.md) | 架构标准基类,条件编译自动选择序列化方式:装 Odin 时继承 `SerializedMonoBehaviour` / `SerializedScriptableObject`,否则继承 Unity 原生基类,业务代码一处继承全程兼容 |
| [AesirArchitectureDebug](scripting-api/Runestone/AesirArchitecture/AesirArchitectureDebug.md) | 内部日志工具,`[AesirArchitecture]` 前缀 + 醒目配色;Log / LogWarning 标注 `[Conditional("UNITY_EDITOR")]`,打包自动剔除调用点,LogError 始终保留 |
| [ResetStaticsAssistant](scripting-api/Runestone/AesirArchitecture/ResetStaticsAssistant.md) | 静态变量重置助手(仅泛型类)—— 泛型类中的 `[RuntimeInitializeOnLoadMethod]` 会被 Unity 静默跳过(2022.3 实测),助手在非泛型中心位置注册回调补位,兼容关闭 Domain Reload 的工作流 |

---

## 模块与架构核心的关系

各模块在 MVC / MVP 数据流中的位置:

| 环节 | 用到的模块 |
|------|-----------|
| Context 注册与获取 Model / Service | Locator(GenericLocator 保序托管注册表) |
| Model 承载数据与外界订阅 | Observable(ObservableValue / 可观察集合) |
| 跨模块通信 | 互相 GetModel + ObservableValue 订阅,或直接引用 MiniEvent(不做事件总线) |
| 纯 C# 对象的帧驱动 | CustomLifecycle(接口自动注册)或 Utilities(PlayerLoop 帧钩子) |
| Model / Service / Command 的延时执行 | Utilities(AesirScheduler —— 无协程能力者的合法延时手段) |
| 监听泄漏防护 | Event(句柄 + 触发器家族),所有订阅 API 统一返回 AutoRemoveListenerHandle |

模块间唯一的方向性依赖:Observable 与 CustomLifecycle 构建在 Event 的 MiniEvent 之上(变更通知、生命周期事件都是 MiniEvent);AesirScheduler 构建在 AesirArchitecturePlayerLoop 之上(BeforeUpdate 钩子结算)。其余模块彼此独立,可按需取用。

## 继续阅读

- [响应式与事件](observable.md) —— Observable 与 Event 的深入用法、事件机制决策表
- [架构概念](concepts.md) —— Core 层的能力接口组合与 Context 生命周期
- [特性一览](features.md) —— 按卖点视角速览同一批能力
- [Scripting API](scripting-api/index.md) —— 全部类型的参考文档
- [示例总览](samples.md) —— MiniEvent / ObservableCollections 独立示例与 PlaneWar 实战
