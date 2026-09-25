---
title: BindingInfo
description: "Runestone.AesirModules.BindingInfo 的 API 文档"
---

# `BindingInfo`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `BindingInfo`

## 声明

``` csharp
public abstract class BindingInfo
```

绑定信息基类。Attribute 订阅与 Script 订阅的共同部分。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Priority`](#property-priority) | — |
| [`InsertionIndex`](#property-insertionindex) | 注册顺序自增序号。由 EventModule 在注册时分配， 作为同优先级排序的次键（对齐 RAA HookEntry 范式）， 保证相同 Priority 的订阅者按注册顺序稳定执行。 |
| [`Subscriber`](#property-subscriber) | — |
| [`BindingKey`](#property-bindingkey) | — |

</div>

### Priority {#property-priority}

``` csharp
public SubscriberPriority Priority { get; protected set; }
```

### InsertionIndex {#property-insertionindex}

注册顺序自增序号。由 EventModule 在注册时分配， 作为同优先级排序的次键（对齐 RAA HookEntry 范式）， 保证相同 Priority 的订阅者按注册顺序稳定执行。

``` csharp
public long InsertionIndex { get; internal set; }
```

### Subscriber {#property-subscriber}

``` csharp
public object Subscriber { get; protected set; }
```

### BindingKey {#property-bindingkey}

``` csharp
public string BindingKey { get; protected set; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Invoke(Object[])`](#method-invoke-object) | — |

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

### Invoke(Object[]) {#method-invoke-object}

``` csharp
public abstract void Invoke(Object[] args = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `args` | `Object[]` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
