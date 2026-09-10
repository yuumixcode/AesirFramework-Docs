---
title: ObservableList<T>.Enumerator<T>
description: "Runestone.AesirArchitecture.ObservableList<T>.Enumerator<T> 的 API 文档"
---

# `ObservableList<T>.Enumerator<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `ObservableList<T>.Enumerator<T>`

**实现接口:** `System.Collections.Generic.IEnumerator<T>`，`System.Collections.IEnumerator`，`System.IDisposable`

## 声明

``` csharp
public struct ObservableList<T>.Enumerator<T> : System.ValueType, 
System.Collections.Generic.IEnumerator<T>, 
System.Collections.IEnumerator, 
System.IDisposable 
```

可观察列表实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Current`](#property-current) | 获取当前位置的元素。 |

</div>

### Current {#property-current}

获取当前位置的元素。

``` csharp
public T Current { get; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`MoveNext()`](#method-movenext) | 前进到下一个元素。 |

</div>

**继承的方法**

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

### MoveNext() {#method-movenext}

前进到下一个元素。

``` csharp
public bool MoveNext()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
