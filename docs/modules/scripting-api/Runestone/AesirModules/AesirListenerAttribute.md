---
title: AesirListenerAttribute
description: "Runestone.AesirModules.AesirListenerAttribute 的 API 文档"
---

# `AesirListenerAttribute`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `System.Attribute` → `AesirListenerAttribute`

**实现接口:** `System.Runtime.InteropServices._Attribute`

## 声明

``` csharp
[AttributeUsage]
public class AesirListenerAttribute : System.Attribute, 
System.Runtime.InteropServices._Attribute
```

事件订阅者特性。标记在方法上，表示该方法监听指定类型的 AesirEventArgs。
用法示例： [AesirListener] private void OnKeyPressed(OnKeyPressed e) { ... } [AesirListener(typeof(OnKeyPressed))] private void OnKeyPressed() { ... } [AesirListener(SubscriberPriority.First)] private void OnKeyPressed(OnKeyPressed e) { ... } [AesirListener(typeof(OnKeyPressed), SubscriberPriority.Last)] private void OnKeyPressedLast() { ... }

AllowMultiple = true：同一方法可标注多个 [AesirListener] 监听多种事件类型。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirListenerAttribute()`](#constructor-aesirlistenerattribute) | 创建默认特性实例。事件类型从方法第一个参数推断，优先级默认 High。 |
| [`AesirListenerAttribute(SubscriberPriority)`](#constructor-aesirlistenerattribute-subscriberpriority) | 创建特性实例并显式指定监听的事件类型。 |
| [`AesirListenerAttribute(Type)`](#constructor-aesirlistenerattribute-type) | 创建特性实例并显式指定监听的事件类型。 |
| [`AesirListenerAttribute(Type, SubscriberPriority)`](#constructor-aesirlistenerattribute-type-subscriberpriority) | 创建特性实例并显式指定监听的事件类型和优先级。 |

</div>

### AesirListenerAttribute() {#constructor-aesirlistenerattribute}

创建默认特性实例。事件类型从方法第一个参数推断，优先级默认 High。

``` csharp
public AesirListenerAttribute()
```

### AesirListenerAttribute(SubscriberPriority) {#constructor-aesirlistenerattribute-subscriberpriority}

创建特性实例并显式指定监听的事件类型。

``` csharp
public AesirListenerAttribute(SubscriberPriority priority)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `priority` | `SubscriberPriority` | — |

</div>

### AesirListenerAttribute(Type) {#constructor-aesirlistenerattribute-type}

创建特性实例并显式指定监听的事件类型。

``` csharp
public AesirListenerAttribute(Type eventType)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `eventType` | `Type` | 事件类型，必须继承自 AesirEventArgs。 |

</div>

### AesirListenerAttribute(Type, SubscriberPriority) {#constructor-aesirlistenerattribute-type-subscriberpriority}

创建特性实例并显式指定监听的事件类型和优先级。

``` csharp
public AesirListenerAttribute(Type eventType, SubscriberPriority priority)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `eventType` | `Type` | 事件类型，必须继承自 AesirEventArgs。 |
| `priority` | `SubscriberPriority` | 订阅优先级。 |

</div>

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Priority`](#property-priority) | 订阅优先级。决定订阅者在分发中的执行顺序。 默认 High。 |
| [`EventType`](#property-eventtype) | 显式指定监听的事件类型。为 null 时从方法第一个参数推断。 |

</div>

**继承的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `TypeId` | — | `Attribute` |

</div>

### Priority {#property-priority}

订阅优先级。决定订阅者在分发中的执行顺序。 默认 High。

``` csharp
public SubscriberPriority Priority { get; set; }
```

### EventType {#property-eventtype}

显式指定监听的事件类型。为 null 时从方法第一个参数推断。

``` csharp
public Type EventType { get; set; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Equals(object)` | — | `Attribute` |
| `GetHashCode()` | — | `Attribute` |
| `IsDefaultAttribute()` | — | `Attribute` |
| `Match(object)` | — | `Attribute` |
| `ToString()` | — | `object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
