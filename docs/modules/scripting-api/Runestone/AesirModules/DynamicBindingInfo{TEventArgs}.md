---
title: DynamicBindingInfo<TEventArgs>
description: "Runestone.AesirModules.DynamicBindingInfo<TEventArgs> 的 API 文档"
---

# `DynamicBindingInfo<TEventArgs>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `Runestone.AesirModules.BindingInfo` → `DynamicBindingInfo<TEventArgs>`

## 声明

``` csharp
public sealed class DynamicBindingInfo<TEventArgs> : Runestone.AesirModules.BindingInfo where TEventArgs : Runestone.AesirModules.AesirEventArgs
```

Script 订阅绑定信息。通过 Action{T} 委托直接调用，无需表达式树。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`DynamicBindingInfo(Action<TEventArgs>, SubscriberPriority, object)`](#constructor-dynamicbindinginfo-action-teventargs-subscriberpriority-object) | — |

</div>

### DynamicBindingInfo(Action<TEventArgs>, SubscriberPriority, object) {#constructor-dynamicbindinginfo-action-teventargs-subscriberpriority-object}

``` csharp
public DynamicBindingInfo<TEventArgs>(Action<TEventArgs> callback, SubscriberPriority priority, object subscriber)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<TEventArgs>` | — |
| `priority` | `SubscriberPriority` | — |
| `subscriber` | `object` | — |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `Priority` | — | `BindingInfo` |
| `InsertionIndex` | 注册顺序自增序号。由 EventModule 在注册时分配， 作为同优先级排序的次键（对齐 RAA HookEntry 范式）， 保证相同 Priority 的订阅者按注册顺序稳定执行。 | `BindingInfo` |
| `Subscriber` | — | `BindingInfo` |
| `BindingKey` | — | `BindingInfo` |

</div>

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Invoke(Object[])` | — | `DynamicBindingInfo<TEventArgs>` |
| `Equals(object)` | — | `object` |
| `GetHashCode()` | — | `object` |
| `ToString()` | — | `object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
