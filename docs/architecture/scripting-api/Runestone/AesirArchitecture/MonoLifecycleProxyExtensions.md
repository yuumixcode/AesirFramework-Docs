---
title: MonoLifecycleProxyExtensions
description: "Runestone.AesirArchitecture.MonoLifecycleProxyExtensions 的 API 文档"
---

# `MonoLifecycleProxyExtensions`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `MonoLifecycleProxyExtensions`

## 声明

``` csharp
[Extension]
public static class MonoLifecycleProxyExtensions
```

Mono 生命周期事件扩展方法集合。

**备注**

提供 MonoBehaviour 和 GameObject 的 AddListener 扩展方法， 内部委托给 Instance 单例。
返回的 AutoRemoveListenerHandle 可配合 RemoveListenerExtensions 使用， 也可手动调用 Dispose 移除监听。

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`RegisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action, int)`](#method-registercustomlifecycle-gameobject-monolifecycleevent-action-int) | 添加生命周期事件监听，并绑定到 go 的销毁事件自动移除。 |
| [`RegisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action, int)`](#method-registercustomlifecycle-monobehaviour-monolifecycleevent-action-int) | 添加生命周期事件监听，并绑定到 mono 所在 GameObject 的销毁事件自动移除。 |
| [`RegisterCustomLifecycle(object)`](#method-registercustomlifecycle-object) | 快捷注册（任意对象）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中。 |
| [`RegisterCustomLifecycle(MonoBehaviour)`](#method-registercustomlifecycle-monobehaviour) | 快捷注册（MonoBehaviour 专用）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，并在 GameObject 销毁时自动取消订阅。 |
| [`UnregisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action)`](#method-unregistercustomlifecycle-gameobject-monolifecycleevent-action) | 移除生命周期事件监听。 |
| [`UnregisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action)`](#method-unregistercustomlifecycle-monobehaviour-monolifecycleevent-action) | 移除生命周期事件监听。 |

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

### RegisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action, int) {#method-registercustomlifecycle-gameobject-monolifecycleevent-action-int}

添加生命周期事件监听，并绑定到 go 的销毁事件自动移除。

**备注**

适用于非 MonoBehaviour 的纯 C# 类。调用方负责在适当时机 Dispose 返回的句柄以取消订阅。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this GameObject go, MonoLifecycleEvent evt, Action callback, int order = 0)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `go` | `GameObject` | 监听所依附的 GameObject，销毁时自动移除监听 |
| `evt` | `MonoLifecycleEvent` | 要监听的生命周期事件类型 |
| `callback` | `Action` | 事件触发时执行的回调委托 |
| `order` | `int` | 执行优先级，值越小越先执行；同 order 时按注册顺序执行 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 用于后续手动移除该监听的句柄（Dispose 与销毁自动移除等效，重复调用安全） |

</div>

### RegisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action, int) {#method-registercustomlifecycle-monobehaviour-monolifecycleevent-action-int}

添加生命周期事件监听，并绑定到 mono 所在 GameObject 的销毁事件自动移除。

**备注**

适用于非 MonoBehaviour 的纯 C# 类。调用方负责在适当时机 Dispose 返回的句柄以取消订阅。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this MonoBehaviour mono, MonoLifecycleEvent evt, Action callback, int order = 0)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `mono` | `MonoBehaviour` | 监听所依附的 MonoBehaviour，其所在 GameObject 销毁时自动移除监听 |
| `evt` | `MonoLifecycleEvent` | 要监听的生命周期事件类型 |
| `callback` | `Action` | 事件触发时执行的回调委托 |
| `order` | `int` | 执行优先级，值越小越先执行；同 order 时按注册顺序执行 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 用于后续手动移除该监听的句柄（Dispose 与销毁自动移除等效，重复调用安全） |

</div>

### RegisterCustomLifecycle(object) {#method-registercustomlifecycle-object}

快捷注册（任意对象）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中。

**备注**

适用于非 MonoBehaviour 的纯 C# 类。调用方负责在适当时机 Dispose 返回的句柄以取消订阅。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this object obj)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `obj` | `object` | 实现了任意 ICustomXXX 接口的对象（MonoBehaviour 或纯 C# 类均可） |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 组合句柄，Dispose 时一次性移除本次注册的所有监听 |

</div>

### RegisterCustomLifecycle(MonoBehaviour) {#method-registercustomlifecycle-monobehaviour}

快捷注册（MonoBehaviour 专用）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，并在 GameObject 销毁时自动取消订阅。

**备注**

适用于非 MonoBehaviour 的纯 C# 类。调用方负责在适当时机 Dispose 返回的句柄以取消订阅。

``` csharp
[Extension]
[Ext] public static void RegisterCustomLifecycle(this MonoBehaviour mono)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `mono` | `MonoBehaviour` | 实现了任意 ICustomXXX 接口的 MonoBehaviour |

</div>

### UnregisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action) {#method-unregistercustomlifecycle-gameobject-monolifecycleevent-action}

移除生命周期事件监听。

``` csharp
[Extension]
[Ext] public static void UnregisterCustomLifecycle(this GameObject go, MonoLifecycleEvent evt, Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `go` | `GameObject` | 监听所依附的 GameObject |
| `evt` | `MonoLifecycleEvent` | 目标生命周期事件类型 |
| `callback` | `Action` | 要移除的回调委托，必须与注册时传入的实例相同 |

</div>

### UnregisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action) {#method-unregistercustomlifecycle-monobehaviour-monolifecycleevent-action}

移除生命周期事件监听。

``` csharp
[Extension]
[Ext] public static void UnregisterCustomLifecycle(this MonoBehaviour mono, MonoLifecycleEvent evt, Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `mono` | `MonoBehaviour` | 监听所依附的 MonoBehaviour |
| `evt` | `MonoLifecycleEvent` | 目标生命周期事件类型 |
| `callback` | `Action` | 要移除的回调委托，必须与注册时传入的实例相同 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
