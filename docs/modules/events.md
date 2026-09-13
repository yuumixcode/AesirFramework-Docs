# 事件模块

事件模块提供基于**双轨订阅**的发布-订阅系统,用于业务模块间解耦:

- **Attribute 订阅** —— `[AesirListener]` 特性标记方法,`AddListener(obj)` 反射扫描注册(AllowMultiple:一个方法可监听多种事件)
- **Script 订阅** —— `AddListener<T>(obj, callback)` 动态注册委托,返回 `AutoRemoveListenerHandle`
- 两种订阅共存于独立注册表,分发时合并进迭代快照,按 **4 档优先级**稳定排序执行(同档按注册顺序)
- **订阅者过滤器** —— `WithFilter` 链式声明"只让特定范围的订阅者收到"(精确投递)
- **分发期可靠性** —— 快照迭代(回调内退订/注册不影响本趟分发)、支持重入发布、已销毁订阅者自动清理(死引用)+ 可选分发耗时告警
- **SO 资产化** —— `AesirEventArgsSO` 让事件可保存为 .asset 资源,配合 `UnityEventOnAesirEvent` 桥接组件,非程序员可在 Inspector 配置事件

!!! note "与 MiniEvent 的定位差异"
    `AesirEventArgs` 只是**事件参数载体**(类似 `EventArgs`),本身不持有监听者;订阅管理由 `EventModule` 的双注册表负责。这与 `MiniEvent`(自身持有监听列表的自包含事件)在设计定位上不同 —— 事件参数载体命名 `XxxEventArgs`,自包含事件才命名 `XxxEvent`。

## 使用方式

### 1. 定义事件参数

```csharp
using Runestone.AesirModules;

public class OnPlayerScored : AesirEventArgs
{
    public int points;
    public string playerName;
}
```

### 2. Attribute 订阅

```csharp
public class ScoreUI : MonoBehaviour
{
    void OnEnable()  => EventModule.AddListener(this);    // 反射扫描 [AesirListener] 方法
    void OnDisable() => EventModule.RemoveListener(this); // 移除该对象全部绑定

    [AesirListener]   // 事件类型从方法第一个参数推断
    private void OnPlayerScored(OnPlayerScored e) { /* ... */ }
}
```

### 3. Script 订阅

```csharp
AutoRemoveListenerHandle _handle;

void OnEnable() =>
    _handle = EventModule.AddListener<OnPlayerScored>(this, e => Debug.Log(e.points));

void OnDisable() => _handle.Dispose();   // 重复调用安全
```

### 4. 发布事件

```csharp
// 链式(sender 即发布者)
new OnPlayerScored { points = 10, playerName = "Player1" }.Invoke(this);

// 或直接调用
EventModule.InvokeEvent(this, new OnPlayerScored { points = 10 });
```

### 5. 指定优先级

```csharp
[AesirListener(SubscriberPriority.First)]                    // Attribute 方式
private void OnPlayerScored(OnPlayerScored e) { ... }

EventModule.AddListener<OnPlayerScored>(this, e => { ... }, SubscriberPriority.Last);
```

### 6. 订阅者过滤器(精确投递)

发布时经 `WithFilter` 链式声明过滤器,分发时逐订阅者检查,**全部通过才投递**:

```csharp
// 只有 Tag 为 "Enemy" 的订阅者收到
new OnExplosion().WithFilter(new WithTag("Enemy")).Invoke(this);

// 组合过滤:爆炸半径内的敌人(两个过滤器都须通过)
new OnExplosion()
    .WithFilter(new InsideCollider2D())
    .WithFilter(new WithTag("Enemy"))
    .Invoke(this);

// 多场景叠加:只通知与发布者同场景的订阅者
new OnLevelLoaded().WithFilter(new SameSceneAsEmitter()).Invoke(this);

// 家族命令:只通知自身 / 子树 / 父级链上的订阅者
new OnChildActivated().WithFilter(new OnlySelf()).Invoke(this);
```

内建过滤器:

| 过滤器 | 语义 |
|--------|------|
| `WithTag(tag)` | 仅 Tag 匹配的订阅者收到(tag 须非 null 非空串,构造期 fail-fast 抛出) |
| `WithPriority(priority)` | 仅绑定在指定优先级档位的订阅者收到 |
| `SameSceneAsEmitter` | 仅与发布者同场景的订阅者收到(适配多场景叠加加载) |
| `OnlySelf` | 仅发布者自身 / 子树 / 父级链上的订阅者收到 |
| `InsideCollider2D` | 仅位于发布者 Collider2D 范围内的订阅者收到(空间局域广播) |

自定义过滤器实现 `ISubscriberFilter.ShouldReceive(args, subscriber, priority)` 即可。

!!! note "fail-closed 约定"
    过滤器无法解析对象(发布者 / 订阅者不是 GameObject 或 Component、已销毁)时按"不通过"处理,避免过滤条件失效导致事件意外扩散。

### 7. SO 资产化(Inspector 配置事件)

**`AesirEventArgsSO`** —— 事件参数的 ScriptableObject 包装:Project 右键 `Create → Aesir → Event Module → AesirEventArgsSO` 创建资产,Inspector 中经 `SubclassSelector` 下拉选择事件参数子类并配置载荷,运行时点击「触发事件(Raise)」按钮或代码调用 `Raise()`(发布者为资产本身)。

**`UnityEventOnAesirEvent`** —— UnityEvent 桥接组件:挂载后经下拉选择监听的事件类型,在 On Raised 中绑定任意 UnityEvent 回调(播放音效、激活物体等),非程序员零代码串联事件。

```csharp
// 代码触发(发布者 = SO 资产本身)
scoredEventAsset.Raise();
```

> `SubclassSelector` 对任意 `[SerializeReference]` 字段生效;`ExcludeSubclassSelector` 可把不想出现在下拉中的类型排除。

## SubscriberPriority —— 4 档优先级

| 档位 | 执行时机 | 默认归属 |
|------|---------|---------|
| `First` | 比所有默认档位更早,常规处理前运行 | — |
| `High` | 高优先级 | **Attribute 订阅默认值** |
| `Medium` | 中优先级 | **Script 订阅默认值** |
| `Last` | 所有订阅者之后,收尾 / 清理 | — |

## 架构设计

### 双注册表与分发流程

```
AttributeBindings (Dictionary<string, List<BindingInfo>>)
  └─ StaticBindingInfo   — MethodInfo + 表达式树编译委托

DynamicBindings (Dictionary<string, List<BindingInfo>>)
  └─ DynamicBindingInfo<T> — Action<T> 直接委托

分发流程:
  1. 从两个注册表取订阅者列表
  2. 合并进迭代快照(顶层复用迭代缓冲区;重入层使用独立局部列表)
  3. 按优先级稳定排序(Priority 主键 + 注册序次键;订阅者数 > 1 才排序)
  4. 逐订阅者:死引用检查 → 过滤器检查 → 调用(顶层复用 object[] 参数数组)
  5. 循环外:移除本轮收集的死绑定;超过阈值输出耗时告警(仅顶层分发计时)
```

### 快照迭代与重入安全

分发循环基于注册表快照执行,两个语义由此保证:

- **回调内退订/注册不影响本趟分发** —— 订阅者回调内 `RemoveListener` / 句柄 `Dispose` / 新增订阅只修改注册表本身,本趟迭代仍按快照执行完毕(退订的订阅者本趟仍会收到,新增的从下趟开始收到),不会出现"退订后续订阅者导致跳过一个"的索引位移。
- **回调内可安全同步发布事件(重入)** —— 回调内再发布任何事件(同型或异型),重入层使用独立的局部迭代列表、局部参数数组与局部死绑定收集,外层循环继续时剩余订阅者仍收到正确的外层事件参数。重入层不复用顶层共享缓冲区,代价是每次重入分发一次小的局部分配。

### 死引用清理

订阅者 GameObject 被 Destroy 后绑定仍会残留在注册表。分发循环内把 Unity 假 null 的订阅者收集到复用列表,**循环结束后**从双注册表移除,并在编辑器输出 Warning 提示检查退订遗漏(玩家构建中静默清理)。遗漏退订由此自动兜底,无泄漏累积。

### 性能模型(冷 / 热路径)

反射只发生在**冷路径**(注册期,一次性成本),**热路径**(分发期)零反射、零字符串分配、零装箱、零闭包捕获;顶层分发零列表分配(迭代缓冲区 Clear 复用),重入层除外(见上文"快照迭代与重入安全"):

| 路径 | 操作 | 实测成本 |
|------|------|---------|
| 冷 | `Bind`(方法扫描 + 特性实例化 + 表达式树编译) | ~50µs/订阅者 |
| 冷 | 表达式树 `Expression.Lambda.Compile()` | ~1-3ms/唯一方法,仅首次 |
| 热 | 编译委托调用(vs `MethodInfo.Invoke` ~300ns) | ~4ns/次,加速 ~78 倍 |
| 热 | 绑定键查询(按事件类型缓存;原生拼接每次 ~1µs 且新分配字符串) | ~20ns 字典查询,零分配 |
| 热 | 1000 订阅者单次发布(含死引用 / 过滤器检查、排序、调用) | ~571µs |

顶层热路径复用迭代缓冲区、`object[]` 参数数组、死绑定收集列表与静态 `Stopwatch`(Clear 保留容量,稳态零分配);过滤器列表懒分配(未声明过滤器时为 null,零开销)。`List.Sort` 的比较器包装为每次排序一次小分配(订阅者 ≥ 2 才触发)。性能特征由 EditMode 回归测试锁定(绑定键缓存引用同一性 + 编译委托对比计时 + 千订阅者量级软门槛)。

### 性能监控

`executionMsLimit`(毫秒,默认 0 = 关闭)为单次分发耗时告警阈值,超过输出 Warning(含事件名、耗时与订阅者数量)。**仅顶层分发计时** —— 重入层不计时,避免嵌套分发的 Restart/Stop 互相破坏计时。分发支持重入,语义见上文"快照迭代与重入安全"。

## 示例

Package Manager → Aesir Modules → Samples 导入:

| 示例 | 说明 |
|------|------|
| `Events/01_KeyPress` | 基本发布-订阅:按键发布事件、`[AesirListener]` 静态订阅 |
| `Events/02_Filters` | 订阅者过滤器对照:Space 发布 `WithTag`+`InsideCollider2D` 双重过滤警报、R 发布 `OnlySelf` 家族命令,场景内置圈内 / 圈外 / 无标签多组对照 |
| `Events/03_SOAsset` | SO 资产化:`ScoreEventAsset.asset` 配置事件载荷,`UnityEventOnAesirEvent` 在 Inspector 零代码串联 UnityEvent 回调 |

## 继续阅读

- [特性一览](features.md) —— 五模块速览
- [响应式与事件](../architecture/observable.md) —— MiniEvent / ObservableValue 决策表
