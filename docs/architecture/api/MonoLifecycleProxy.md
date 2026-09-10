---
title: MonoLifecycleProxy
description: "Runestone.AesirArchitecture.MonoLifecycleProxy 的 API 文档"
---

# `MonoLifecycleProxy`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.Component` → `UnityEngine.Behaviour` → `UnityEngine.MonoBehaviour` → `Sirenix.OdinInspector.SerializedMonoBehaviour` → `Runestone.AesirArchitecture.AesirMonoBehaviour` → `MonoLifecycleProxy`

**实现接口:** `Sirenix.Serialization.ISupportsPrefabSerialization`，`UnityEngine.ISerializationCallbackReceiver`

## 声明

``` csharp
[DisallowMultipleComponent]
[DefaultExecutionOrder]
public sealed class MonoLifecycleProxy : Runestone.AesirArchitecture.AesirMonoBehaviour, 
Sirenix.Serialization.ISupportsPrefabSerialization, 
UnityEngine.ISerializationCallbackReceiver
```

Mono 生命周期事件代理。作为全局单例挂载在 [Aesir Architecture] GameObject 上， 将 Unity 原生生命周期回调和自定义 PlayerLoop 阶段统一为可订阅的有序事件。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`MonoLifecycleProxy()`](#constructor-monolifecycleproxy) | — |

</div>

### MonoLifecycleProxy() {#constructor-monolifecycleproxy}

``` csharp
public MonoLifecycleProxy()
```

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Instance`](#property-instance) | 获取全局唯一的 MonoLifecycleProxy 实例。 |

</div>

**继承的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `destroyCancellationToken` | — | `MonoBehaviour` |
| `gameObject` | — | `Component` |
| `hideFlags` | — | `Object` |
| `transform` | — | `Component` |
| `enabled` | — | `Behaviour` |
| `isActiveAndEnabled` | — | `Behaviour` |
| `runInEditMode` | — | `MonoBehaviour` |
| `useGUILayout` | — | `MonoBehaviour` |
| `name` | — | `Object` |
| `tag` | — | `Component` |
| `animation` | — | `Component` |
| `audio` | — | `Component` |
| `camera` | — | `Component` |
| `collider` | — | `Component` |
| `collider2D` | — | `Component` |
| `constantForce` | — | `Component` |
| `hingeJoint` | — | `Component` |
| `light` | — | `Component` |
| `networkView` | — | `Component` |
| `particleSystem` | — | `Component` |
| `renderer` | — | `Component` |
| `rigidbody` | — | `Component` |
| `rigidbody2D` | — | `Component` |

</div>

### Instance {#property-instance}

获取全局唯一的 MonoLifecycleProxy 实例。

``` csharp
public static MonoLifecycleProxy Instance { get; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddListener(MonoLifecycleEvent, Action, int)`](#method-addlistener-monolifecycleevent-action-int) | 添加生命周期事件监听，返回可自动移除的监听句柄。 |
| [`RegisterAuto(object)`](#method-registerauto-object) | 快捷注册。扫描对象实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，返回组合句柄。 |
| [`GetListenerCount(MonoLifecycleEvent)`](#method-getlistenercount-monolifecycleevent) | 获取指定事件当前的监听者数量 |
| [`ClearAllListeners()`](#method-clearalllisteners) | 清空所有事件的监听者 |
| [`RemoveListener(MonoLifecycleEvent, Action)`](#method-removelistener-monolifecycleevent-action) | 移除指定事件的监听者 |
| [`Register(object)`](#method-register-object) | 快捷注册（任意对象）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中。 |
| [`Register(MonoBehaviour)`](#method-register-monobehaviour) | 快捷注册（MonoBehaviour 专用）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，并绑定到目标 GameObject 的 OnDestroy 自动取消订阅。 |

</div>

**继承的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetComponent(Type)` | — | `Component` |
| `GetComponent(string)` | — | `Component` |
| `GetComponentInChildren(Type)` | — | `Component` |
| `GetComponentInChildren(Type, bool)` | — | `Component` |
| `GetComponentInParent(Type)` | — | `Component` |
| `GetComponentInParent(Type, bool)` | — | `Component` |
| `GetComponents(Type)` | — | `Component` |
| `GetComponentsInChildren(Type)` | — | `Component` |
| `GetComponentsInChildren(Type, bool)` | — | `Component` |
| `GetComponentsInParent(Type)` | — | `Component` |
| `GetComponentsInParent(Type, bool)` | — | `Component` |
| `StartCoroutine(IEnumerator)` | — | `MonoBehaviour` |
| `StartCoroutine(string)` | — | `MonoBehaviour` |
| `StartCoroutine(string, object)` | — | `MonoBehaviour` |
| `GetComponent()` | — | `Component` |
| `GetComponentInChildren()` | — | `Component` |
| `GetComponentInChildren(bool)` | — | `Component` |
| `GetComponentInParent()` | — | `Component` |
| `GetComponentInParent(bool)` | — | `Component` |
| `GetComponents()` | — | `Component` |
| `GetComponentsInChildren()` | — | `Component` |
| `GetComponentsInChildren(bool)` | — | `Component` |
| `GetComponentsInParent()` | — | `Component` |
| `GetComponentsInParent(bool)` | — | `Component` |
| `GetType()` | — | `object` |
| `CompareTag(string)` | — | `Component` |
| `IsInvoking()` | — | `MonoBehaviour` |
| `IsInvoking(string)` | — | `MonoBehaviour` |
| `TryGetComponent(Type, ref Component)` | — | `Component` |
| `TryGetComponent(ref T)` | — | `Component` |
| `GetComponentIndex()` | — | `Component` |
| `GetInstanceID()` | — | `Object` |
| `Equals(object)` | — | `Object` |
| `GetHashCode()` | — | `Object` |
| `ToString()` | — | `Object` |
| `BroadcastMessage(string)` | — | `Component` |
| `BroadcastMessage(string, SendMessageOptions)` | — | `Component` |
| `BroadcastMessage(string, object)` | — | `Component` |
| `BroadcastMessage(string, object, SendMessageOptions)` | — | `Component` |
| `CancelInvoke()` | — | `MonoBehaviour` |
| `CancelInvoke(string)` | — | `MonoBehaviour` |
| `GetComponents(Type, List<Component>)` | — | `Component` |
| `GetComponents(List<T>)` | — | `Component` |
| `GetComponentsInChildren(List<T>)` | — | `Component` |
| `GetComponentsInChildren(bool, List<T>)` | — | `Component` |
| `GetComponentsInParent(bool, List<T>)` | — | `Component` |
| `Invoke(string, float)` | — | `MonoBehaviour` |
| `InvokeRepeating(string, float, float)` | — | `MonoBehaviour` |
| `SendMessage(string)` | — | `Component` |
| `SendMessage(string, SendMessageOptions)` | — | `Component` |
| `SendMessage(string, object)` | — | `Component` |
| `SendMessage(string, object, SendMessageOptions)` | — | `Component` |
| `SendMessageUpwards(string)` | — | `Component` |
| `SendMessageUpwards(string, SendMessageOptions)` | — | `Component` |
| `SendMessageUpwards(string, object)` | — | `Component` |
| `SendMessageUpwards(string, object, SendMessageOptions)` | — | `Component` |
| `StopAllCoroutines()` | — | `MonoBehaviour` |
| `StopCoroutine(Coroutine)` | — | `MonoBehaviour` |
| `StopCoroutine(IEnumerator)` | — | `MonoBehaviour` |
| `StopCoroutine(string)` | — | `MonoBehaviour` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |
| `OnAfterDeserialize()` | — | `SerializedMonoBehaviour` |
| `OnBeforeSerialize()` | — | `SerializedMonoBehaviour` |
| `StartCoroutine_Auto(IEnumerator)` | — | `MonoBehaviour` |

</div>

### AddListener(MonoLifecycleEvent, Action, int) {#method-addlistener-monolifecycleevent-action-int}

添加生命周期事件监听，返回可自动移除的监听句柄。

``` csharp
public AutoRemoveListenerHandle AddListener(MonoLifecycleEvent evt, Action callback, int order = 0)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
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

### RegisterAuto(object) {#method-registerauto-object}

快捷注册。扫描对象实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，返回组合句柄。

``` csharp
public AutoRemoveListenerHandle RegisterAuto(object obj)
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

### GetListenerCount(MonoLifecycleEvent) {#method-getlistenercount-monolifecycleevent}

获取指定事件当前的监听者数量

``` csharp
public int GetListenerCount(MonoLifecycleEvent evt)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `evt` | `MonoLifecycleEvent` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `int` |

</div>

### ClearAllListeners() {#method-clearalllisteners}

清空所有事件的监听者

``` csharp
public void ClearAllListeners()
```
### RemoveListener(MonoLifecycleEvent, Action) {#method-removelistener-monolifecycleevent-action}

移除指定事件的监听者

``` csharp
public void RemoveListener(MonoLifecycleEvent evt, Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `evt` | `MonoLifecycleEvent` |
| `callback` | `Action` |

</div>

### Register(object) {#method-register-object}

快捷注册（任意对象）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中。

``` csharp
public static AutoRemoveListenerHandle Register(object obj)
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

### Register(MonoBehaviour) {#method-register-monobehaviour}

快捷注册（MonoBehaviour 专用）。扫描实现的所有 ICustomXXX 接口， 将对应方法自动注册到匹配的生命周期事件中，并绑定到目标 GameObject 的 OnDestroy 自动取消订阅。

``` csharp
public static void Register(MonoBehaviour mono)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `mono` | `MonoBehaviour` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
