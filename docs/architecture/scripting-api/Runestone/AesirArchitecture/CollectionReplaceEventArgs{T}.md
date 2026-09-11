---
title: CollectionReplaceEventArgs<T>
description: "Runestone.AesirArchitecture.CollectionReplaceEventArgs<T> 的 API 文档"
---

# `CollectionReplaceEventArgs<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `CollectionReplaceEventArgs<T>`

**类型参数**

- `T` — 集合元素类型

## 声明

``` csharp
[IsReadOnly]
public struct CollectionReplaceEventArgs<T> : System.ValueType 
```

集合替换事件参数。包含替换位置索引、旧项与新项。

**备注**

只读结构体，事件回调时零分配传递变更细节。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CollectionReplaceEventArgs(int, T, T)`](#constructor-collectionreplaceeventargs-int-t-t) | 构造替换事件参数。 |

</div>

### CollectionReplaceEventArgs(int, T, T) {#constructor-collectionreplaceeventargs-int-t-t}

构造替换事件参数。

``` csharp
public CollectionReplaceEventArgs<T>(int index, T oldItem, T newItem)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `index` | `int` | 发生替换的索引 |
| `oldItem` | `T` | 替换前的旧项 |
| `newItem` | `T` | 替换后的新项 |

</div>

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`NewItem`](#field-newitem) | 替换后的新项。 |
| [`OldItem`](#field-olditem) | 替换前的旧项。 |
| [`Index`](#field-index) | 发生替换的索引。 |

</div>

### NewItem {#field-newitem}

替换后的新项。

``` csharp
public readonly T NewItem;
```

### OldItem {#field-olditem}

替换前的旧项。

``` csharp
public readonly T OldItem;
```

### Index {#field-index}

发生替换的索引。

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
