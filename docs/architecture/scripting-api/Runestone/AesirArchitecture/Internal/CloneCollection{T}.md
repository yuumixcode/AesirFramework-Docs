---
title: CloneCollection<T>
description: "Runestone.AesirArchitecture.Internal.CloneCollection<T> 的 API 文档"
---

# `CloneCollection<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture.Internal`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `CloneCollection<T>`

**实现接口:** `System.IDisposable`

## 声明

``` csharp
[NullableContext]
[Nullable]
internal struct CloneCollection<T> : System.ValueType, 
System.IDisposable 
```

ReadOnly cloned collection.

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CloneCollection(IEnumerable<T>)`](#constructor-clonecollection-ienumerable-t) | — |
| [`CloneCollection(List<T>, int, int)`](#constructor-clonecollection-list-t-int-int) | — |
| [`CloneCollection(ReadOnlySpan<T>)`](#constructor-clonecollection-readonlyspan-t) | — |
| [`CloneCollection(T)`](#constructor-clonecollection-t) | — |

</div>

### CloneCollection(IEnumerable<T>) {#constructor-clonecollection-ienumerable-t}

``` csharp
public CloneCollection<T>(IEnumerable<T> source)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `source` | `IEnumerable<T>` | — |

</div>

### CloneCollection(List<T>, int, int) {#constructor-clonecollection-list-t-int-int}

``` csharp
public CloneCollection<T>(List<T> source, int index, int count)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `source` | `List<T>` | — |
| `index` | `int` | — |
| `count` | `int` | — |

</div>

### CloneCollection(ReadOnlySpan<T>) {#constructor-clonecollection-readonlyspan-t}

``` csharp
public CloneCollection<T>(ReadOnlySpan<T> source)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `source` | `ReadOnlySpan<T>` | — |

</div>

### CloneCollection(T) {#constructor-clonecollection-t}

``` csharp
public CloneCollection<T>(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | — |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Span`](#property-span) | — |

</div>

### Span {#property-span}

``` csharp
[Nullable]
public ReadOnlySpan<T> Span { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AsEnumerable()`](#method-asenumerable) | — |
| [`Dispose()`](#method-dispose) | — |

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

### AsEnumerable() {#method-asenumerable}

``` csharp
public IEnumerable<T> AsEnumerable()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `IEnumerable<T>` | — |

</div>

### Dispose() {#method-dispose}

``` csharp
public void Dispose()
```

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
