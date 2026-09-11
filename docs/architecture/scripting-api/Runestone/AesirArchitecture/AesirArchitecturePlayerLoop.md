---
title: AesirArchitecturePlayerLoop
description: "Runestone.AesirArchitecture.AesirArchitecturePlayerLoop 的 API 文档"
---

# `AesirArchitecturePlayerLoop`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AesirArchitecturePlayerLoop`

## 声明

``` csharp
public static class AesirArchitecturePlayerLoop
```

基于 PlayerLoop 的生命周期钩子系统，无需 MonoBehaviour 即可接入游戏级帧回调。
通过 Register 注册回调，order 越小越先执行；系统自动在域加载时注入 PlayerLoop。

注入自愈：PlayerLoop 注入可能被第三方 SDK 用其缓存的副本调用 PlayerLoop.SetPlayerLoop 覆盖， 导致钩子静默失效。框架通过 EnsureInjected 自愈：域加载时与每次 Register 时 检测并补插缺失的注入点（注册即自愈）；用户也可手动调用。

**备注**

待处理命令机制：在遍历回调执行期间，如果有 Register 或 Unregister 调用， 不会直接修改回调集合（否则会抛出 InvalidOperationException）， 而是将操作缓存到 PendingCommands 列表中，待当前遍历结束后统一执行。

稳定排序机制：回调列表使用 Order 字段进行优先级排序，Order 越小越先执行。 当多个回调的 Order 相同时，使用 InsertionIndex（插入顺序自增序号）作为次级排序键， 确保相同优先级的回调按注册顺序执行，排序结果稳定可预期。

域加载安全：通过 [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.SubsystemRegistration)] 在 Unity 的子系统注册阶段自动注入 PlayerLoop，该阶段早于场景加载和脚本初始化， 确保在 Disable Domain Reload 模式下也能正确重建钩子系统。

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Register(AesirArchitectureLifecyclePhase, Action, int)`](#method-register-aesirarchitecturelifecyclephase-action-int) | 注册回调，order 越小越先执行，默认 0。 返回 AutoRemoveListenerHandle，Dispose 时自动注销本次注册，与全框架监听句柄风格一致。 忽略返回值的调用方须在持有者销毁前手动调用 Unregister 注销——匿名委托无法经 Unregister 定位注销，只能依赖返回的句柄；若均未注销，回调将永久残留并阻止目标对象被回收。 |
| [`GetHookCount(AesirArchitectureLifecyclePhase)`](#method-gethookcount-aesirarchitecturelifecyclephase) | 获取指定阶段的已注册回调数量 |
| [`EnsureInjected()`](#method-ensureinjected) | 确保两个注入点存在于当前 PlayerLoop。已存在时为空操作，缺失时重新注入。 |
| [`Reset()`](#method-reset) | 清空所有回调 |
| [`Unregister(AesirArchitectureLifecyclePhase, Action)`](#method-unregister-aesirarchitecturelifecyclephase-action) | 注销回调。 必须传入注册时的同一委托实例，匿名函数无法通过此方法注销。 |

</div>

**继承的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Equals(object)` | — | `object` |
| `GetHashCode()` | — | `object` |
| `ToString()` | — | `object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

### Register(AesirArchitectureLifecyclePhase, Action, int) {#method-register-aesirarchitecturelifecyclephase-action-int}

注册回调，order 越小越先执行，默认 0。
返回 AutoRemoveListenerHandle，Dispose 时自动注销本次注册，与全框架监听句柄风格一致。 忽略返回值的调用方须在持有者销毁前手动调用 Unregister 注销——匿名委托无法经 Unregister 定位注销，只能依赖返回的句柄；若均未注销，回调将永久残留并阻止目标对象被回收。

``` csharp
public static AutoRemoveListenerHandle Register(AesirArchitectureLifecyclePhase phase, Action callback, int order = 0)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` | 目标生命周期阶段，决定回调在哪一帧阶段执行 |
| `callback` | `Action` | 每帧执行的回调委托，必须为非空委托实例 |
| `order` | `int` | 执行优先级，值越小越先执行；同 order 时按注册顺序执行 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 自动注销句柄，Dispose 时注销本次注册（与手动 Unregister 等效，重复调用安全） |

</div>

### GetHookCount(AesirArchitectureLifecyclePhase) {#method-gethookcount-aesirarchitecturelifecyclephase}

获取指定阶段的已注册回调数量

``` csharp
public static int GetHookCount(AesirArchitectureLifecyclePhase phase)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `int` | — |

</div>

### EnsureInjected() {#method-ensureinjected}

确保两个注入点存在于当前 PlayerLoop。已存在时为空操作，缺失时重新注入。

**备注**

PlayerLoop 注入的自愈入口，幂等可重复调用。第三方 SDK 若使用其缓存的 PlayerLoop 副本调用 PlayerLoop.SetPlayerLoop，会连同框架注入的两个子系统一起抹掉， 导致 BeforeUpdate / AfterUpdate 钩子静默失效。 此方法通过 ContainsSystem{TTarget} 检测后仅补插缺失的子系统， 并保留当前 PlayerLoop 中第三方已有的其他修改。调用时机： Initialize 在域加载时调用； Register 每次注册回调时调用（注册即自愈）； 用户在已知第三方 SDK 修改 PlayerLoop 后也可手动调用。

``` csharp
public static void EnsureInjected()
```

### Reset() {#method-reset}

清空所有回调

**备注**

此方法在 Initialize 中调用，确保域重载后清空旧的回调数据和待处理命令， 防止 Disable Domain Reload 模式下残留的静态状态导致回调重复执行或引用已销毁的对象。

``` csharp
public static void Reset()
```

### Unregister(AesirArchitectureLifecyclePhase, Action) {#method-unregister-aesirarchitecturelifecyclephase-action}

注销回调。
必须传入注册时的同一委托实例，匿名函数无法通过此方法注销。

**备注**

若在回调遍历期间调用此方法，注销操作不会立即执行，而是被缓存到待处理命令列表中， 待当前阶段所有回调遍历结束后才统一执行，以避免遍历期间修改集合导致异常。

``` csharp
public static void Unregister(AesirArchitectureLifecyclePhase phase, Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` | 目标生命周期阶段 |
| `callback` | `Action` | 要注销的回调委托，必须与注册时传入的实例相同 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
