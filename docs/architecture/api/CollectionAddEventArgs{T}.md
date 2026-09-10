---
title: CollectionAddEventArgs<T>
description: "Runestone.AesirArchitecture.CollectionAddEventArgs<T> 的 API 文档"
---

# `CollectionAddEventArgs<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `CollectionAddEventArgs<T>`

## 声明

``` csharp
[IsReadOnly]
public struct CollectionAddEventArgs<T> : System.ValueType 
```

集合添加事件参数。包含被添加项及其索引。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CollectionAddEventArgs(int, T)`](#constructor-collectionaddeventargs-int-t) | 构造添加事件参数。 |

</div>

### CollectionAddEventArgs(int, T) {#constructor-collectionaddeventargs-int-t}

构造添加事件参数。

``` csharp
public CollectionAddEventArgs<T>(int index, T item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `index` | `int` |
| `item` | `T` |

</div>

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Item`](#field-item) | 被添加的项。 |
| [`Index`](#field-index) | 被添加项在列表中的索引。 |

</div>

### Item {#field-item}

被添加的项。

``` csharp
public readonly T Item;
```
### Index {#field-index}

被添加项在列表中的索引。

``` csharp
public readonly int Index;
```
## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Equals(object)` | — | `ValueType` |
| `GetHashCode()` | — | `ValueType` |
| `ToString()` | — | `ValueType` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
