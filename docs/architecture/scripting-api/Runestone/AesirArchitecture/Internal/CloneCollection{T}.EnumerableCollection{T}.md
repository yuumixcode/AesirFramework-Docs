---
title: CloneCollection<T>.EnumerableCollection<T>
description: "Runestone.AesirArchitecture.Internal.CloneCollection<T>.EnumerableCollection<T> 的 API 文档"
---

# `CloneCollection<T>.EnumerableCollection<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture.Internal`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `CloneCollection<T>.EnumerableCollection<T>`

**实现接口:** `System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.ICollection<T>`

## 声明

``` csharp
[Nullable]
private class CloneCollection<T>.EnumerableCollection<T> : System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.ICollection<T> 
```

ReadOnly cloned collection.

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CloneCollection(T[], int)`](#constructor-clonecollection-t-int) | — |

</div>

### CloneCollection(T[], int) {#constructor-clonecollection-t-int}

``` csharp
public CloneCollection<T>.EnumerableCollection<T>(T[] array, int count)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `array` | `T[]` | — |
| `count` | `int` | — |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`IsReadOnly`](#property-isreadonly) | — |
| [`Count`](#property-count) | — |

</div>

### IsReadOnly {#property-isreadonly}

``` csharp
public bool IsReadOnly { get; }
```

### Count {#property-count}

``` csharp
public int Count { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetEnumerator()`](#method-getenumerator) | — |
| [`Contains(T)`](#method-contains-t) | — |
| [`Remove(T)`](#method-remove-t) | — |
| [`Add(T)`](#method-add-t) | — |
| [`Clear()`](#method-clear) | — |
| [`CopyTo(T[], int)`](#method-copyto-t-int) | — |

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

### GetEnumerator() {#method-getenumerator}

``` csharp
[IteratorStateMachine]
public IEnumerator<T> GetEnumerator()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `IEnumerator<T>` | — |

</div>

### Contains(T) {#method-contains-t}

``` csharp
public bool Contains(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | — |

</div>

### Remove(T) {#method-remove-t}

``` csharp
public bool Remove(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | — |

</div>

### Add(T) {#method-add-t}

``` csharp
public void Add(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | — |

</div>

### Clear() {#method-clear}

``` csharp
public void Clear()
```

### CopyTo(T[], int) {#method-copyto-t-int}

``` csharp
public void CopyTo(T[] dest, int destIndex)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `dest` | `T[]` | — |
| `destIndex` | `int` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
