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

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`RegisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action, int)`](#method-registercustomlifecycle-gameobject-monolifecycleevent-action-int) | 添加生命周期事件监听。 |
| [`RegisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action, int)`](#method-registercustomlifecycle-monobehaviour-monolifecycleevent-action-int) | 添加生命周期事件监听。 |
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

添加生命周期事件监听。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this GameObject go, MonoLifecycleEvent evt, Action callback, int order = 0)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `go` | `GameObject` |
| `evt` | `MonoLifecycleEvent` |
| `callback` | `Action` |
| `order` | `int` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### RegisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action, int) {#method-registercustomlifecycle-monobehaviour-monolifecycleevent-action-int}

添加生命周期事件监听。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this MonoBehaviour mono, MonoLifecycleEvent evt, Action callback, int order = 0)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `mono` | `MonoBehaviour` |
| `evt` | `MonoLifecycleEvent` |
| `callback` | `Action` |
| `order` | `int` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### RegisterCustomLifecycle(object) {#method-registercustomlifecycle-object}

快捷注册（任意对象）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中。

``` csharp
[Extension]
[Ext] public static AutoRemoveListenerHandle RegisterCustomLifecycle(this object obj)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `obj` | `object` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### RegisterCustomLifecycle(MonoBehaviour) {#method-registercustomlifecycle-monobehaviour}

快捷注册（MonoBehaviour 专用）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，并在 GameObject 销毁时自动取消订阅。

``` csharp
[Extension]
[Ext] public static void RegisterCustomLifecycle(this MonoBehaviour mono)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `mono` | `MonoBehaviour` |

</div>

### UnregisterCustomLifecycle(GameObject, MonoLifecycleEvent, Action) {#method-unregistercustomlifecycle-gameobject-monolifecycleevent-action}

移除生命周期事件监听。

``` csharp
[Extension]
[Ext] public static void UnregisterCustomLifecycle(this GameObject go, MonoLifecycleEvent evt, Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `go` | `GameObject` |
| `evt` | `MonoLifecycleEvent` |
| `callback` | `Action` |

</div>

### UnregisterCustomLifecycle(MonoBehaviour, MonoLifecycleEvent, Action) {#method-unregistercustomlifecycle-monobehaviour-monolifecycleevent-action}

移除生命周期事件监听。

``` csharp
[Extension]
[Ext] public static void UnregisterCustomLifecycle(this MonoBehaviour mono, MonoLifecycleEvent evt, Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `mono` | `MonoBehaviour` |
| `evt` | `MonoLifecycleEvent` |
| `callback` | `Action` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
