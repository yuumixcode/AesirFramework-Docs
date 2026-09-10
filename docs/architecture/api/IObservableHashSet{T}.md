---
title: IObservableHashSet<T>
description: "Runestone.AesirArchitecture.IObservableHashSet<T> 的 API 文档"
---

# `IObservableHashSet<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `Runestone.AesirArchitecture.IReadOnlyObservableHashSet<T>`，`System.Collections.Generic.ISet<T>`，`System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.ICollection<T>`，`System.Collections.Generic.IReadOnlyCollection<T>`

## 声明

``` csharp
public interface IObservableHashSet<T> : Runestone.AesirArchitecture.IReadOnlyObservableHashSet<T>, 
System.Collections.Generic.ISet<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.ICollection<T>, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

完整可观察集合接口。
Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableHashSet{T} 只读订阅。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Count`](#property-count) | — |

</div>

### Count {#property-count}

``` csharp
public int Count { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Contains(T)`](#method-contains-t) | — |

</div>

### Contains(T) {#method-contains-t}

``` csharp
public abstract bool Contains(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `item` | `T` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
