---
title: EventModule
description: "Runestone.AesirModules.EventModule 的 API 文档"
---

# `EventModule`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.Component` → `UnityEngine.Behaviour` → `UnityEngine.MonoBehaviour` → `Sirenix.OdinInspector.SerializedMonoBehaviour` → `Runestone.AesirArchitecture.AesirMonoBehaviour` → `EventModule`

**实现接口:** `Sirenix.Serialization.ISupportsPrefabSerialization`，`UnityEngine.ISerializationCallbackReceiver`

## 声明

``` csharp
[DisallowMultipleComponent]
[AddComponentMenu]
public class EventModule : Runestone.AesirArchitecture.AesirMonoBehaviour, 
Sirenix.Serialization.ISupportsPrefabSerialization, 
UnityEngine.ISerializationCallbackReceiver
```

事件模块（MonoBehaviour 单例）。 通过 [AesirListener] 特性实现 Attribute 订阅，通过 AddListener{TEventArgs}(object, Action{TEventArgs}) 实现 Script 订阅， 通过 InvokeEvent{TEventArgs} 分发事件。
支持 4 档优先级排序分发与双轨订阅共存。两种订阅分别存储于独立注册表， 分发时合并并按优先级排序。

分发期可靠性：自动检测并清理已销毁的 Unity 对象订阅者（死引用）； 支持 WithFilter 声明的订阅者过滤器实现精确投递； 可通过 executionMsLimit 开启分发耗时告警。

快照语义与重入安全：每趟分发基于注册表快照迭代——回调内退订/注册只影响后续分发， 不干扰本趟；回调内同步发布事件（重入）使用独立的迭代缓冲区与参数数组， 外层分发不受覆写影响。性能计时（executionMsLimit）仅对顶层分发生效。 排序为 Priority 主键 + 注册序号次键的稳定排序，同优先级按注册顺序执行。

作为 AesirModules 的子物体存在，由 GetOrAddChild{T} 懒加载创建。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`EventModule()`](#constructor-eventmodule) | — |

</div>

### EventModule() {#constructor-eventmodule}

``` csharp
public EventModule()
```

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AttributeBindings`](#field-attributebindings) | Attribute 订阅注册表。以事件类型 AssemblyQualifiedName 为键。 |
| [`DynamicBindings`](#field-dynamicbindings) | Script 订阅注册表。以事件类型 AssemblyQualifiedName 为键。 |

</div>

### AttributeBindings {#field-attributebindings}

Attribute 订阅注册表。以事件类型 AssemblyQualifiedName 为键。

``` csharp
public Dictionary<string, List<BindingInfo>> AttributeBindings;
```

### DynamicBindings {#field-dynamicbindings}

Script 订阅注册表。以事件类型 AssemblyQualifiedName 为键。

``` csharp
public Dictionary<string, List<BindingInfo>> DynamicBindings;
```

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Instance`](#property-instance) | 全局单例入口。 优先在已加载场景中查找预放置的实例；未找到时在 AesirModules（DDOL）下创建子物体。 |

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

全局单例入口。 优先在已加载场景中查找预放置的实例；未找到时在 AesirModules（DDOL）下创建子物体。

``` csharp
public static EventModule Instance { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddListener(object, AesirEventArgs, Action<AesirEventArgs>)`](#method-addlistener-object-aesireventargs-action-aesireventargs) | 添加 Script 订阅（非泛型版）。通过事件参数实例推断类型，反射适配。 默认优先级 Medium。 |
| [`AddListener(object, AesirEventArgs, SubscriberPriority, Action<AesirEventArgs>)`](#method-addlistener-object-aesireventargs-subscriberpriority-action-aesireventargs) | 添加 Script 订阅（非泛型版），指定优先级。 |
| [`AddListener(object, Action<TEventArgs>)`](#method-addlistener-object-action-teventargs) | 添加 Script 订阅。通过 Lambda 委托监听指定事件类型，无需 [AesirListener] 特性。 返回自动移除句柄，Dispose 或 using 块结束时自动注销。 默认优先级 Medium。 |
| [`AddListener(object, Action<TEventArgs>, SubscriberPriority)`](#method-addlistener-object-action-teventargs-subscriberpriority) | 添加 Script 订阅，指定优先级。返回自动移除句柄。 |
| [`AddListener(object)`](#method-addlistener-object) | 添加 Attribute 订阅者。反射扫描对象上标有 [AesirListener] 的方法并注册。 通常在 OnEnable 中调用。 |
| [`InvokeEvent(object, TEventArgs)`](#method-invokeevent-object-teventargs) | 触发事件。合并两个注册表的订阅者，按优先级排序后依次调用。 |
| [`RemoveListener(object)`](#method-removelistener-object) | 移除订阅者。从两个注册表中移除该对象的所有绑定（含 Attribute 和 Script）。 通常在 OnDisable 中调用。 |

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

### AddListener(object, AesirEventArgs, Action<AesirEventArgs>) {#method-addlistener-object-aesireventargs-action-aesireventargs}

添加 Script 订阅（非泛型版）。通过事件参数实例推断类型，反射适配。 默认优先级 Medium。

``` csharp
public static AutoRemoveListenerHandle AddListener(object subscriber, AesirEventArgs eventArgs, Action<AesirEventArgs> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |
| `eventArgs` | `AesirEventArgs` | — |
| `callback` | `Action<AesirEventArgs>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddListener(object, AesirEventArgs, SubscriberPriority, Action<AesirEventArgs>) {#method-addlistener-object-aesireventargs-subscriberpriority-action-aesireventargs}

添加 Script 订阅（非泛型版），指定优先级。

``` csharp
public static AutoRemoveListenerHandle AddListener(object subscriber, AesirEventArgs eventArgs, SubscriberPriority priority, Action<AesirEventArgs> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |
| `eventArgs` | `AesirEventArgs` | — |
| `priority` | `SubscriberPriority` | — |
| `callback` | `Action<AesirEventArgs>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddListener(object, Action<TEventArgs>) {#method-addlistener-object-action-teventargs}

添加 Script 订阅。通过 Lambda 委托监听指定事件类型，无需 [AesirListener] 特性。 返回自动移除句柄，Dispose 或 using 块结束时自动注销。 默认优先级 Medium。

``` csharp
public static AutoRemoveListenerHandle AddListener<TEventArgs>(object subscriber, Action<TEventArgs> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |
| `callback` | `Action<TEventArgs>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddListener(object, Action<TEventArgs>, SubscriberPriority) {#method-addlistener-object-action-teventargs-subscriberpriority}

添加 Script 订阅，指定优先级。返回自动移除句柄。

``` csharp
public static AutoRemoveListenerHandle AddListener<TEventArgs>(object subscriber, Action<TEventArgs> callback, SubscriberPriority priority)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |
| `callback` | `Action<TEventArgs>` | — |
| `priority` | `SubscriberPriority` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddListener(object) {#method-addlistener-object}

添加 Attribute 订阅者。反射扫描对象上标有 [AesirListener] 的方法并注册。 通常在 OnEnable 中调用。

``` csharp
public static void AddListener(object subscriber)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |

</div>

### InvokeEvent(object, TEventArgs) {#method-invokeevent-object-teventargs}

触发事件。合并两个注册表的订阅者，按优先级排序后依次调用。

``` csharp
public static void InvokeEvent<TEventArgs>(object sender, TEventArgs eventArgs)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sender` | `object` | — |
| `eventArgs` | `TEventArgs` | — |

</div>

### RemoveListener(object) {#method-removelistener-object}

移除订阅者。从两个注册表中移除该对象的所有绑定（含 Attribute 和 Script）。 通常在 OnDisable 中调用。

``` csharp
public static void RemoveListener(object subscriber)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `subscriber` | `object` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
