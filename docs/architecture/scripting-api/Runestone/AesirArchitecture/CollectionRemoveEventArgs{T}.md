---
title: CollectionRemoveEventArgs<T>
description: "Runestone.AesirArchitecture.CollectionRemoveEventArgs<T> 的 API 文档"
---

# `CollectionRemoveEventArgs<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `CollectionRemoveEventArgs<T>`

**类型参数**

- `T` — 集合元素类型

## 声明

``` csharp
[IsReadOnly]
public struct CollectionRemoveEventArgs<T> : System.ValueType 
```

集合移除事件参数。包含被移除项及其移除前所在索引。

**备注**

只读结构体，事件回调时零分配传递变更细节。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CollectionRemoveEventArgs(int, T)`](#constructor-collectionremoveeventargs-int-t) | 构造移除事件参数。 |

</div>

### CollectionRemoveEventArgs(int, T) {#constructor-collectionremoveeventargs-int-t}

构造移除事件参数。

``` csharp
public CollectionRemoveEventArgs<T>(int index, T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `index` | `int` | 被移除项移除前的索引 |
| `item` | `T` | 被移除的项 |

</div>

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Item`](#field-item) | 被移除的项。 |
| [`Index`](#field-index) | 被移除项移除前在列表中的索引。 |

</div>

### Item {#field-item}

被移除的项。

``` csharp
public readonly T Item;
```

### Index {#field-index}

被移除项移除前在列表中的索引。

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
