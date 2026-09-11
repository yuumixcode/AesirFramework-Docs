---
title: IObservableList<T>
description: "Runestone.AesirArchitecture.IObservableList<T> 的 API 文档"
---

# `IObservableList<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.Collections.Generic.IReadOnlyList<T>`，`Runestone.AesirArchitecture.IReadOnlyObservableList<T>`，`System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.IList<T>`，`System.Collections.Generic.ICollection<T>`，`System.Collections.Generic.IReadOnlyCollection<T>`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
[DefaultMember]
public interface IObservableList<T> : System.Collections.Generic.IReadOnlyList<T>, 
Runestone.AesirArchitecture.IReadOnlyObservableList<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IList<T>, 
System.Collections.Generic.ICollection<T>, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

完整可观察列表接口。
Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableList{T} 只读订阅。

**备注**

在 IList{T} 基础上追加 AddRange 批量添加。 所有写操作完成后才触发对应事件，监听者回调中读取到的集合已是变更后的状态。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Item`](#property-item) | 读写指定索引的元素。重新声明以统一 IList{T} 与 IReadOnlyList{T} 的索引器。 |
| [`Count`](#property-count) | — |

</div>

### Item {#property-item}

读写指定索引的元素。重新声明以统一 IList{T} 与 IReadOnlyList{T} 的索引器。

``` csharp
public T Item { get; set; }
```

### Count {#property-count}

``` csharp
public int Count { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddRange(IEnumerable<T>)`](#method-addrange-ienumerable-t) | 批量添加元素。逐项添加并逐项触发 Added 事件。 |

</div>

### AddRange(IEnumerable<T>) {#method-addrange-ienumerable-t}

批量添加元素。逐项添加并逐项触发 Added 事件。

**备注**

每添加一项触发一次 Added；如需"整体刷新一次通知"的语义，可先 Clear 再逐项 Add。

``` csharp
public abstract void AddRange(IEnumerable<T> items)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `items` | `IEnumerable<T>` | 要添加的元素序列。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
