---
title: StaticBindingInfo
description: "Runestone.AesirModules.StaticBindingInfo 的 API 文档"
---

# `StaticBindingInfo`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `Runestone.AesirModules.BindingInfo` → `StaticBindingInfo`

## 声明

``` csharp
public sealed class StaticBindingInfo : Runestone.AesirModules.BindingInfo
```

Attribute 订阅绑定信息。
在注册时（冷路径）通过表达式树将 MethodInfo 编译为 Action（object target, object[] args）委托， 分发时（热路径）直接委托调用，避免每次反射。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`StaticBindingInfo(string, MethodInfo, object, SubscriberPriority)`](#constructor-staticbindinginfo-string-methodinfo-object-subscriberpriority) | — |

</div>

### StaticBindingInfo(string, MethodInfo, object, SubscriberPriority) {#constructor-staticbindinginfo-string-methodinfo-object-subscriberpriority}

``` csharp
public StaticBindingInfo(string bindingKey, MethodInfo method, object subscriber, SubscriberPriority priority)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `bindingKey` | `string` | — |
| `method` | `MethodInfo` | — |
| `subscriber` | `object` | — |
| `priority` | `SubscriberPriority` | — |

</div>

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Method`](#property-method) | 原始方法信息。仅用于去重判断 IsAlreadyBound。 不参与分发调用。 |

</div>

**继承的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `Priority` | — | `BindingInfo` |
| `InsertionIndex` | 注册顺序自增序号。由 EventModule 在注册时分配， 作为同优先级排序的次键（对齐 RAA HookEntry 范式）， 保证相同 Priority 的订阅者按注册顺序稳定执行。 | `BindingInfo` |
| `Subscriber` | — | `BindingInfo` |
| `BindingKey` | — | `BindingInfo` |

</div>

### Method {#property-method}

原始方法信息。仅用于去重判断 IsAlreadyBound。 不参与分发调用。

``` csharp
public MethodInfo Method { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Invoke(Object[])` | — | `StaticBindingInfo` |
| `Equals(object)` | — | `object` |
| `GetHashCode()` | — | `object` |
| `ToString()` | — | `object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
