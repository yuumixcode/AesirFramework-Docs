---
title: ObservableHashSet<T>
description: "Runestone.AesirArchitecture.ObservableHashSet<T> 的 API 文档"
---

# `ObservableHashSet<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ObservableHashSet<T>`

**实现接口:** `Runestone.AesirArchitecture.IReadOnlyObservableHashSet<T>`，`System.Collections.Generic.ISet<T>`，`System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`Runestone.AesirArchitecture.IObservableHashSet<T>`，`System.Collections.Generic.ICollection<T>`，`System.Collections.Generic.IReadOnlyCollection<T>`

## 声明

``` csharp
[Serializable]
public sealed class ObservableHashSet<T> : Runestone.AesirArchitecture.IReadOnlyObservableHashSet<T>, 
System.Collections.Generic.ISet<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
Runestone.AesirArchitecture.IObservableHashSet<T>, 
System.Collections.Generic.ICollection<T>, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

可观察集合实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ObservableHashSet()`](#constructor-observablehashset) | 默认构造，创建空集合。 |
| [`ObservableHashSet(IEnumerable<T>)`](#constructor-observablehashset-ienumerable-t) | 指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。 |
| [`ObservableHashSet(int)`](#constructor-observablehashset-int) | 指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。 |

</div>

### ObservableHashSet() {#constructor-observablehashset}

默认构造，创建空集合。

``` csharp
public ObservableHashSet<T>()
```
### ObservableHashSet(IEnumerable<T>) {#constructor-observablehashset-ienumerable-t}

指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableHashSet<T>(IEnumerable<T> initialItems)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `initialItems` | `IEnumerable<T>` |

</div>

### ObservableHashSet(int) {#constructor-observablehashset-int}

指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableHashSet<T>(int capacity)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `capacity` | `int` |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`IsReadOnly`](#property-isreadonly) | 固定返回 false，该集合可写。 |
| [`Count`](#property-count) | 元素数量。 |

</div>

### IsReadOnly {#property-isreadonly}

固定返回 false，该集合可写。

``` csharp
public bool IsReadOnly { get; }
```
### Count {#property-count}

元素数量。

``` csharp
public int Count { get; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddAddedListener(Action<T>)`](#method-addaddedlistener-action-t) | — |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | — |
| [`AddRemovedListener(Action<T>)`](#method-addremovedlistener-action-t) | — |
| [`GetEnumerator()`](#method-getenumerator) | 返回遍历元素的结构体枚举器，foreach 具体类型时零分配。 |
| [`Add(T)`](#method-add-t) | 添加元素，实际添加时触发 Added 事件（参数为该元素）。 |
| [`Contains(T)`](#method-contains-t) | 判断是否包含指定元素。 |
| [`IsProperSubsetOf(IEnumerable<T>)`](#method-ispropersubsetof-ienumerable-t) | 判断当前集合是否为 other 的真子集。 |
| [`IsProperSupersetOf(IEnumerable<T>)`](#method-ispropersupersetof-ienumerable-t) | 判断当前集合是否为 other 的真超集。 |
| [`IsSubsetOf(IEnumerable<T>)`](#method-issubsetof-ienumerable-t) | 判断当前集合是否为 other 的子集。 |
| [`IsSupersetOf(IEnumerable<T>)`](#method-issupersetof-ienumerable-t) | 判断当前集合是否为 other 的超集。 |
| [`Overlaps(IEnumerable<T>)`](#method-overlaps-ienumerable-t) | 判断当前集合与 other 是否存在共同元素。 |
| [`Remove(T)`](#method-remove-t) | 移除指定元素，成功时触发 Removed 事件（参数为该元素）。 |
| [`SetEquals(IEnumerable<T>)`](#method-setequals-ienumerable-t) | 判断当前集合与 other 是否包含完全相同的元素。 |
| [`Clear()`](#method-clear) | 清空集合。集合非空时触发 Cleared 事件；已为空时不触发。 |
| [`ClearListeners()`](#method-clearlisteners) | 清空所有事件监听。 |
| [`CopyTo(T[], int)`](#method-copyto-t-int) | 从指定数组索引开始复制元素到目标数组。 |
| [`ExceptWith(IEnumerable<T>)`](#method-exceptwith-ienumerable-t) | 差集运算：逐项复用 Remove，仅对实际存在的元素触发 Removed 事件。 |
| [`IntersectWith(IEnumerable<T>)`](#method-intersectwith-ienumerable-t) | 交集运算：移除不在 other 中的元素，逐项触发 Removed 事件。 |
| [`RemoveAddedListener(Action<T>)`](#method-removeaddedlistener-action-t) | — |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | — |
| [`RemoveRemovedListener(Action<T>)`](#method-removeremovedlistener-action-t) | — |
| [`SymmetricExceptWith(IEnumerable<T>)`](#method-symmetricexceptwith-ienumerable-t) | 对称差集运算：移除双方共有的元素，添加仅 other 拥有的元素。 |
| [`UnionWith(IEnumerable<T>)`](#method-unionwith-ienumerable-t) | 并集运算：逐项复用 Add，仅对实际新增的元素触发 Added 事件。 |

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

### AddAddedListener(Action<T>) {#method-addaddedlistener-action-t}

``` csharp
public AutoRemoveListenerHandle AddAddedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddClearedListener(Action) {#method-addclearedlistener-action}

``` csharp
public AutoRemoveListenerHandle AddClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddRemovedListener(Action<T>) {#method-addremovedlistener-action-t}

``` csharp
public AutoRemoveListenerHandle AddRemovedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### GetEnumerator() {#method-getenumerator}

返回遍历元素的结构体枚举器，foreach 具体类型时零分配。

``` csharp
public ObservableHashSet<T>.Enumerator<T> GetEnumerator()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `ObservableHashSet<T>.Enumerator<T>` |

</div>

### Add(T) {#method-add-t}

添加元素，实际添加时触发 Added 事件（参数为该元素）。

``` csharp
public bool Add(T item)
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

### Contains(T) {#method-contains-t}

判断是否包含指定元素。

``` csharp
public bool Contains(T item)
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

### IsProperSubsetOf(IEnumerable<T>) {#method-ispropersubsetof-ienumerable-t}

判断当前集合是否为 other 的真子集。

``` csharp
public bool IsProperSubsetOf(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### IsProperSupersetOf(IEnumerable<T>) {#method-ispropersupersetof-ienumerable-t}

判断当前集合是否为 other 的真超集。

``` csharp
public bool IsProperSupersetOf(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### IsSubsetOf(IEnumerable<T>) {#method-issubsetof-ienumerable-t}

判断当前集合是否为 other 的子集。

``` csharp
public bool IsSubsetOf(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### IsSupersetOf(IEnumerable<T>) {#method-issupersetof-ienumerable-t}

判断当前集合是否为 other 的超集。

``` csharp
public bool IsSupersetOf(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Overlaps(IEnumerable<T>) {#method-overlaps-ienumerable-t}

判断当前集合与 other 是否存在共同元素。

``` csharp
public bool Overlaps(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Remove(T) {#method-remove-t}

移除指定元素，成功时触发 Removed 事件（参数为该元素）。

``` csharp
public bool Remove(T item)
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

### SetEquals(IEnumerable<T>) {#method-setequals-ienumerable-t}

判断当前集合与 other 是否包含完全相同的元素。

``` csharp
public bool SetEquals(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Clear() {#method-clear}

清空集合。集合非空时触发 Cleared 事件；已为空时不触发。

``` csharp
public void Clear()
```
### ClearListeners() {#method-clearlisteners}

清空所有事件监听。

``` csharp
public void ClearListeners()
```
### CopyTo(T[], int) {#method-copyto-t-int}

从指定数组索引开始复制元素到目标数组。

``` csharp
public void CopyTo(T[] array, int arrayIndex)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `array` | `T[]` |
| `arrayIndex` | `int` |

</div>

### ExceptWith(IEnumerable<T>) {#method-exceptwith-ienumerable-t}

差集运算：逐项复用 Remove，仅对实际存在的元素触发 Removed 事件。

``` csharp
public void ExceptWith(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

### IntersectWith(IEnumerable<T>) {#method-intersectwith-ienumerable-t}

交集运算：移除不在 other 中的元素，逐项触发 Removed 事件。

``` csharp
public void IntersectWith(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

### RemoveAddedListener(Action<T>) {#method-removeaddedlistener-action-t}

``` csharp
public void RemoveAddedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

``` csharp
public void RemoveClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

### RemoveRemovedListener(Action<T>) {#method-removeremovedlistener-action-t}

``` csharp
public void RemoveRemovedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

### SymmetricExceptWith(IEnumerable<T>) {#method-symmetricexceptwith-ienumerable-t}

对称差集运算：移除双方共有的元素，添加仅 other 拥有的元素。

``` csharp
public void SymmetricExceptWith(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

### UnionWith(IEnumerable<T>) {#method-unionwith-ienumerable-t}

并集运算：逐项复用 Add，仅对实际新增的元素触发 Added 事件。

``` csharp
public void UnionWith(IEnumerable<T> other)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `other` | `IEnumerable<T>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
