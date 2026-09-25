---
title: ObservableQueue<T>
description: "Runestone.AesirArchitecture.ObservableQueue<T> 的 API 文档"
---

# `ObservableQueue<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ObservableQueue<T>`

**实现接口:** `System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`Runestone.AesirArchitecture.IObservableCollection<T>`，`System.Collections.Generic.IReadOnlyCollection<T>`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
[Serializable]
public sealed class ObservableQueue<T> : System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
Runestone.AesirArchitecture.IObservableCollection<T>, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

可观察队列实现。

**备注**

内部组合 Queue{T} 存储元素，变更通知经 MiniEvent{T} 分发——Invoke 路径零分配。 变更通知为单一事件（AddListener）：入队 → Add（索引为队尾位置）、出队 → Remove（索引固定 0）、 Clear → Reset（非空才通知）；批量入队 / 出队逐项通知；无变更的操作（TryDequeue 空队列）不通知。
[Serializable] 标记与类型上的 [SerializeField] 供 Odin 序列化等第三方集成使用—— Unity 原生不序列化 Queue{T}，初始元素请经构造函数或 EnqueueRange 填充。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ObservableQueue()`](#constructor-observablequeue) | — |
| [`ObservableQueue(IEnumerable<T>)`](#constructor-observablequeue-ienumerable-t) | — |
| [`ObservableQueue(int)`](#constructor-observablequeue-int) | — |

</div>

### ObservableQueue() {#constructor-observablequeue}

``` csharp
public ObservableQueue<T>()
```

### ObservableQueue(IEnumerable<T>) {#constructor-observablequeue-ienumerable-t}

``` csharp
public ObservableQueue<T>(IEnumerable<T> collection)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `collection` | `IEnumerable<T>` | — |

</div>

### ObservableQueue(int) {#constructor-observablequeue-int}

``` csharp
public ObservableQueue<T>(int capacity)
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
| [`Count`](#property-count) | — |

</div>

### Count {#property-count}

``` csharp
public int Count { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddListener(Action<CollectionChangedEventArgs<T>>)`](#method-addlistener-action-collectionchangedeventargs-t) | — |
| [`GetEnumerator()`](#method-getenumerator) | 返回遍历元素的结构体枚举器，foreach 具体类型时零分配。 |
| [`Dequeue()`](#method-dequeue) | 队首元素出队并返回，触发 Remove 通知（索引固定 0）。 |
| [`Peek()`](#method-peek) | — |
| [`ToArray()`](#method-toarray) | — |
| [`TryDequeue(ref T)`](#method-trydequeue-ref-t) | 尝试让队首元素出队，成功时触发 Remove 通知（索引固定 0）；空队列不通知。 |
| [`TryPeek(ref T)`](#method-trypeek-ref-t) | — |
| [`Clear()`](#method-clear) | 清空队列。队列非空时以 Reset 通知；已为空时不通知。 |
| [`ClearListeners()`](#method-clearlisteners) | 清空所有变更监听。 |
| [`DequeueRange(Span<T>)`](#method-dequeuerange-span-t) | 让队首元素依次出队并写入 dest，逐项触发 Remove 通知（索引固定 0）。 |
| [`DequeueRange(int)`](#method-dequeuerange-int) | 让队首的 count 个元素依次出队，逐项触发 Remove 通知（索引固定 0）。 |
| [`Enqueue(T)`](#method-enqueue-t) | 元素入队，触发 Add 通知（索引为队尾位置）。 |
| [`EnqueueRange(IEnumerable<T>)`](#method-enqueuerange-ienumerable-t) | 批量入队元素序列，逐项触发 Add 通知。 |
| [`EnqueueRange(T[])`](#method-enqueuerange-t) | 批量入队元素数组，逐项触发 Add 通知。 |
| [`RemoveListener(Action<CollectionChangedEventArgs<T>>)`](#method-removelistener-action-collectionchangedeventargs-t) | — |
| [`TrimExcess()`](#method-trimexcess) | — |

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

### AddListener(Action<CollectionChangedEventArgs<T>>) {#method-addlistener-action-collectionchangedeventargs-t}

``` csharp
public AutoRemoveListenerHandle AddListener(Action<CollectionChangedEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionChangedEventArgs<T>>` | — |

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
public ObservableQueue<T>.Enumerator<T> GetEnumerator()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `ObservableQueue<T>.Enumerator<T>` | 元素枚举器。 |

</div>

### Dequeue() {#method-dequeue}

队首元素出队并返回，触发 Remove 通知（索引固定 0）。

``` csharp
public T Dequeue()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `T` | 出队的元素。 |

</div>

### Peek() {#method-peek}

``` csharp
public T Peek()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `T` | — |

</div>

### ToArray() {#method-toarray}

``` csharp
public T[] ToArray()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `T[]` | — |

</div>

### TryDequeue(ref T) {#method-trydequeue-ref-t}

尝试让队首元素出队，成功时触发 Remove 通知（索引固定 0）；空队列不通知。

``` csharp
public bool TryDequeue(out ref T result)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `result` | `ref T` | 出队的元素；队列为空时为类型默认值。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 出队成功返回 true，队列为空返回 false。 |

</div>

### TryPeek(ref T) {#method-trypeek-ref-t}

``` csharp
public bool TryPeek(out ref T result)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `result` | `ref T` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | — |

</div>

### Clear() {#method-clear}

清空队列。队列非空时以 Reset 通知；已为空时不通知。

``` csharp
public void Clear()
```

### ClearListeners() {#method-clearlisteners}

清空所有变更监听。

**备注**

清除全部监听引用，防止因监听者未释放导致的内存泄漏。 与 Clear 不同——后者清空的是队列元素。

``` csharp
public void ClearListeners()
```

### DequeueRange(Span<T>) {#method-dequeuerange-span-t}

让队首元素依次出队并写入 dest，逐项触发 Remove 通知（索引固定 0）。

``` csharp
public void DequeueRange(Span<T> dest)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `dest` | `Span<T>` | 接收出队元素的跨度，长度即出队数量。 |

</div>

### DequeueRange(int) {#method-dequeuerange-int}

让队首的 count 个元素依次出队，逐项触发 Remove 通知（索引固定 0）。

``` csharp
public void DequeueRange(int count)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `count` | `int` | 要出队的元素数量。 |

</div>

### Enqueue(T) {#method-enqueue-t}

元素入队，触发 Add 通知（索引为队尾位置）。

``` csharp
public void Enqueue(T item)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `item` | `T` | 要入队的元素。 |

</div>

### EnqueueRange(IEnumerable<T>) {#method-enqueuerange-ienumerable-t}

批量入队元素序列，逐项触发 Add 通知。

**备注**

先整体拷贝再入队，传入队列自身时也能正常终止。

``` csharp
public void EnqueueRange(IEnumerable<T> items)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `items` | `IEnumerable<T>` | 要入队的元素序列。 |

</div>

### EnqueueRange(T[]) {#method-enqueuerange-t}

批量入队元素数组，逐项触发 Add 通知。

**备注**

先整体拷贝再入队，传入队列自身时也能正常终止。

``` csharp
public void EnqueueRange(T[] items)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `items` | `T[]` | 要入队的元素数组。 |

</div>

### RemoveListener(Action<CollectionChangedEventArgs<T>>) {#method-removelistener-action-collectionchangedeventargs-t}

``` csharp
public void RemoveListener(Action<CollectionChangedEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionChangedEventArgs<T>>` | — |

</div>

### TrimExcess() {#method-trimexcess}

``` csharp
public void TrimExcess()
```

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
