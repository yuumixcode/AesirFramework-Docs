# 事件模块(实验性)

!!! warning "实验性模块"
    双轨订阅、优先级与表达式树优化已实现并有测试覆盖,但**尚未在实际项目中验证,API 可能调整**。简单场景建议优先用 [MiniEvent / ObservableValue](../architecture/observable.md)。

事件模块提供基于**双轨订阅**的发布-订阅系统,用于业务模块间解耦:

- **Attribute 订阅** —— `[AesirListener]` 特性标记方法,`AddListener(obj)` 反射扫描注册
- **Script 订阅** —— `AddListener<T>(obj, callback)` 动态注册委托,返回 `AutoRemoveListenerHandle`
- 两种订阅共存于独立注册表,分发时合并并按 **4 档优先级**排序执行

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

## SubscriberPriority —— 4 档优先级

| 档位 | 执行时机 | 默认归属 |
|------|---------|---------|
| `First` | 比所有默认档位更早,常规处理前运行 | — |
| `High` | 高优先级 | **Attribute 订阅默认值** |
| `Medium` | 中优先级 | **Script 订阅默认值** |
| `Last` | 所有订阅者之后,收尾 / 清理 | — |

## 架构设计

### 双注册表

```
AttributeBindings (Dictionary<string, List<BindingInfo>>)
  └─ StaticBindingInfo   — MethodInfo + 表达式树编译委托

DynamicBindings (Dictionary<string, List<BindingInfo>>)
  └─ DynamicBindingInfo<T> — Action<T> 直接委托

分发流程:
  1. 从两个注册表取订阅者列表
  2. 合并(仅在两个注册表都有数据时才创建新 List)
  3. 按优先级升序排序(订阅者数 > 1 才排序)
  4. 依次调用(复用 object[] 参数数组;逐个 try-catch 并解包内部异常)
```

### 表达式树优化

`StaticBindingInfo` 在注册时(`OnEnable` 等冷路径)通过 `Expression.Lambda.Compile()` 将 `MethodInfo` 编译为 `Action<object, object[]>` 委托;之后每次分发(热路径)直接委托调用,比 `MethodInfo.Invoke` 快约 20-40 倍。代价是首次编译约 1-3ms,且不支持 ref/out 参数。

### 健壮性细节

- 分发时跳过 Unity 假 null(已销毁但引用非空)的订阅者
- 按引用 + Method 去重,同一方法不会重复绑定
- 键为事件类型的 `AssemblyQualifiedName`,跨程序集同名事件不串扰

## 示例

Package Manager → Aesir Modules → Samples 导入 `Event Module - Key Press`:按键发布事件、`[AesirListener]` 静态订阅的完整演示(事件参数 `KeyPressedEvent`、发布者 `EventSender`、订阅者 `KeyPressSubscriber`)。

## 继续阅读

- [特性一览](features.md) —— 三模块速览
- [响应式与事件](../architecture/observable.md) —— MiniEvent / ObservableValue 决策表
