---
title: ObservableList<T>
description: "Runestone.AesirArchitecture.ObservableList<T> 的 API 文档"
---

# `ObservableList<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ObservableList<T>`

**实现接口:** `System.Collections.Generic.IReadOnlyList<T>`，`Runestone.AesirArchitecture.IReadOnlyObservableList<T>`，`System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.IList<T>`，`Runestone.AesirArchitecture.IObservableList<T>`，`System.Collections.Generic.ICollection<T>`，`System.Collections.Generic.IReadOnlyCollection<T>`

## 声明

``` csharp
[DefaultMember]
[Serializable]
public sealed class ObservableList<T> : System.Collections.Generic.IReadOnlyList<T>, 
Runestone.AesirArchitecture.IReadOnlyObservableList<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IList<T>, 
Runestone.AesirArchitecture.IObservableList<T>, 
System.Collections.Generic.ICollection<T>, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

可观察列表实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ObservableList()`](#constructor-observablelist) | 默认构造，创建空列表。 |
| [`ObservableList(IEnumerable<T>)`](#constructor-observablelist-ienumerable-t) | 指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。 |
| [`ObservableList(int)`](#constructor-observablelist-int) | 指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。 |

</div>

### ObservableList() {#constructor-observablelist}

默认构造，创建空列表。

``` csharp
public ObservableList<T>()
```
### ObservableList(IEnumerable<T>) {#constructor-observablelist-ienumerable-t}

指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableList<T>(IEnumerable<T> initialItems)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `initialItems` | `IEnumerable<T>` |

</div>

### ObservableList(int) {#constructor-observablelist-int}

指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableList<T>(int capacity)
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
| [`Item`](#property-item) | 读写指定索引的元素。赋值与旧值不同时触发 Replaced 事件，相同则跳过。 |
| [`IsReadOnly`](#property-isreadonly) | 固定返回 false，该集合可写。 |
| [`Count`](#property-count) | 元素数量。 |

</div>

### Item {#property-item}

读写指定索引的元素。赋值与旧值不同时触发 Replaced 事件，相同则跳过。

``` csharp
public T Item { get; set; }
```
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
| [`AddAddedListener(Action<CollectionAddEventArgs<T>>)`](#method-addaddedlistener-action-collectionaddeventargs-t) | — |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | — |
| [`AddRemovedListener(Action<CollectionRemoveEventArgs<T>>)`](#method-addremovedlistener-action-collectionremoveeventargs-t) | — |
| [`AddReplacedListener(Action<CollectionReplaceEventArgs<T>>)`](#method-addreplacedlistener-action-collectionreplaceeventargs-t) | — |
| [`GetEnumerator()`](#method-getenumerator) | 返回遍历元素的结构体枚举器，foreach 具体类型时零分配。 |
| [`Contains(T)`](#method-contains-t) | 判断是否包含指定元素。 |
| [`Remove(T)`](#method-remove-t) | 移除第一个匹配元素，成功时触发 Removed 事件。 |
| [`IndexOf(T)`](#method-indexof-t) | 返回指定元素的索引；不存在时返回 -1。 |
| [`Add(T)`](#method-add-t) | 在末尾添加元素，触发 Added 事件（索引为 Count - 1）。 |
| [`AddRange(IEnumerable<T>)`](#method-addrange-ienumerable-t) | 批量添加元素。逐项添加并逐项触发 Added 事件。 |
| [`Clear()`](#method-clear) | 清空列表。列表非空时触发 Cleared 事件；已为空时不触发。 |
| [`ClearListeners()`](#method-clearlisteners) | 清空所有事件监听。 |
| [`CopyTo(T[], int)`](#method-copyto-t-int) | 从指定数组索引开始复制元素到目标数组。 |
| [`Insert(int, T)`](#method-insert-int-t) | 在指定索引插入元素，触发 Added 事件（索引为插入位置）。 |
| [`RemoveAddedListener(Action<CollectionAddEventArgs<T>>)`](#method-removeaddedlistener-action-collectionaddeventargs-t) | — |
| [`RemoveAt(int)`](#method-removeat-int) | 移除指定索引的元素，触发 Removed 事件（参数含移除前索引与被移除元素）。 |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | — |
| [`RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>)`](#method-removeremovedlistener-action-collectionremoveeventargs-t) | — |
| [`RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>)`](#method-removereplacedlistener-action-collectionreplaceeventargs-t) | — |

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

### AddAddedListener(Action<CollectionAddEventArgs<T>>) {#method-addaddedlistener-action-collectionaddeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddAddedListener(Action<CollectionAddEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` |

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

### AddRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-addremovedlistener-action-collectionremoveeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-addreplacedlistener-action-collectionreplaceeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` |

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
public ObservableList<T>.Enumerator<T> GetEnumerator()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `ObservableList<T>.Enumerator<T>` |

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

### Remove(T) {#method-remove-t}

移除第一个匹配元素，成功时触发 Removed 事件。

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

### IndexOf(T) {#method-indexof-t}

返回指定元素的索引；不存在时返回 -1。

``` csharp
public int IndexOf(T item)
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
| `int` |

</div>

### Add(T) {#method-add-t}

在末尾添加元素，触发 Added 事件（索引为 Count - 1）。

``` csharp
public void Add(T item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `item` | `T` |

</div>

### AddRange(IEnumerable<T>) {#method-addrange-ienumerable-t}

批量添加元素。逐项添加并逐项触发 Added 事件。

``` csharp
public void AddRange(IEnumerable<T> itemsToAdd)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `itemsToAdd` | `IEnumerable<T>` |

</div>

### Clear() {#method-clear}

清空列表。列表非空时触发 Cleared 事件；已为空时不触发。

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

### Insert(int, T) {#method-insert-int-t}

在指定索引插入元素，触发 Added 事件（索引为插入位置）。

``` csharp
public void Insert(int index, T item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `index` | `int` |
| `item` | `T` |

</div>

### RemoveAddedListener(Action<CollectionAddEventArgs<T>>) {#method-removeaddedlistener-action-collectionaddeventargs-t}

``` csharp
public void RemoveAddedListener(Action<CollectionAddEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` |

</div>

### RemoveAt(int) {#method-removeat-int}

移除指定索引的元素，触发 Removed 事件（参数含移除前索引与被移除元素）。

``` csharp
public void RemoveAt(int index)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `index` | `int` |

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

### RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-removeremovedlistener-action-collectionremoveeventargs-t}

``` csharp
public void RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` |

</div>

### RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-removereplacedlistener-action-collectionreplaceeventargs-t}

``` csharp
public void RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
