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

**类型参数**

- `T` — 元素类型

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

**备注**

内部组合 List{T} 存储元素，使用 MiniEvent 管理监听者——Invoke 路径零分配（直接多播调用）。 注意：订阅路径（AddListener / 句柄创建）有与监听者数量成正比的委托分配，勿在每帧订阅场景使用。
[SerializeField] 标记 items 字段使其可在 Inspector 中编辑初始元素； 反序列化填充不触发任何事件（与 ObservableValue{T} 行为一致）。

写操作完成后才触发事件，监听者回调中读取到的集合已是变更后的状态。 无变更的操作不触发事件：Remove 不存在的元素、Clear 空列表、索引器赋相同值。

遍历性能：foreach 具体类型走结构体枚举器，零分配；通过 IReadOnlyObservableList{T} / IEnumerable{T} 接口遍历会装箱一次枚举器（与 BCL List{T} 行为一致）。

需要 Move、Sort、SynchronizedView、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

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

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `initialItems` | `IEnumerable<T>` | 初始元素序列。 |

</div>

### ObservableList(int) {#constructor-observablelist-int}

指定初始元素构造。初始元素不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableList<T>(int capacity)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `capacity` | `int` | — |

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

**备注**

使用 EqualityComparer{T}.Default 判断值是否变化，仅在变化时触发事件。

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

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddClearedListener(Action) {#method-addclearedlistener-action}

``` csharp
public AutoRemoveListenerHandle AddClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-addremovedlistener-action-collectionremoveeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### AddReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-addreplacedlistener-action-collectionreplaceeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | — |

</div>

### GetEnumerator() {#method-getenumerator}

返回遍历元素的结构体枚举器，foreach 具体类型时零分配。

``` csharp
public ObservableList<T>.Enumerator<T> GetEnumerator()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `ObservableList<T>.Enumerator<T>` | 元素枚举器。 |

</div>

### Contains(T) {#method-contains-t}

判断是否包含指定元素。

``` csharp
public bool Contains(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | 要查找的元素。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 包含返回 true，否则返回 false。 |

</div>

### Remove(T) {#method-remove-t}

移除第一个匹配元素，成功时触发 Removed 事件。

``` csharp
public bool Remove(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | 要移除的元素。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 找到并移除返回 true；元素不存在时不触发事件，返回 false。 |

</div>

### IndexOf(T) {#method-indexof-t}

返回指定元素的索引；不存在时返回 -1。

``` csharp
public int IndexOf(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | 要查找的元素。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `int` | 元素索引或 -1。 |

</div>

### Add(T) {#method-add-t}

在末尾添加元素，触发 Added 事件（索引为 Count - 1）。

``` csharp
public void Add(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | 要添加的元素。 |

</div>

### AddRange(IEnumerable<T>) {#method-addrange-ienumerable-t}

批量添加元素。逐项添加并逐项触发 Added 事件。

``` csharp
public void AddRange(IEnumerable<T> itemsToAdd)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `itemsToAdd` | `IEnumerable<T>` | 要添加的元素序列。 |

</div>

### Clear() {#method-clear}

清空列表。列表非空时触发 Cleared 事件；已为空时不触发。

``` csharp
public void Clear()
```

### ClearListeners() {#method-clearlisteners}

清空所有事件监听。

**备注**

清除全部监听引用，防止因监听者未释放导致的内存泄漏。 与 Clear 不同——后者清空的是列表元素。

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

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `array` | `T[]` | 目标数组。 |
| `arrayIndex` | `int` | 目标数组起始索引。 |

</div>

### Insert(int, T) {#method-insert-int-t}

在指定索引插入元素，触发 Added 事件（索引为插入位置）。

``` csharp
public void Insert(int index, T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `index` | `int` | 插入位置索引。 |
| `item` | `T` | 要插入的元素。 |

</div>

### RemoveAddedListener(Action<CollectionAddEventArgs<T>>) {#method-removeaddedlistener-action-collectionaddeventargs-t}

``` csharp
public void RemoveAddedListener(Action<CollectionAddEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` | — |

</div>

### RemoveAt(int) {#method-removeat-int}

移除指定索引的元素，触发 Removed 事件（参数含移除前索引与被移除元素）。

``` csharp
public void RemoveAt(int index)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `index` | `int` | 要移除元素的索引。 |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

``` csharp
public void RemoveClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | — |

</div>

### RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-removeremovedlistener-action-collectionremoveeventargs-t}

``` csharp
public void RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` | — |

</div>

### RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-removereplacedlistener-action-collectionreplaceeventargs-t}

``` csharp
public void RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
