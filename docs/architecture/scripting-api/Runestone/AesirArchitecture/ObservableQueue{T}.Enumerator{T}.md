---
title: ObservableQueue<T>.Enumerator<T>
description: "Runestone.AesirArchitecture.ObservableQueue<T>.Enumerator<T> 的 API 文档"
---

# `ObservableQueue<T>.Enumerator<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `ObservableQueue<T>.Enumerator<T>`

**实现接口:** `System.Collections.Generic.IEnumerator<T>`，`System.Collections.IEnumerator`，`System.IDisposable`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
public struct ObservableQueue<T>.Enumerator<T> : System.ValueType, 
System.Collections.Generic.IEnumerator<T>, 
System.Collections.IEnumerator, 
System.IDisposable 
```

可观察队列实现。

**备注**

内部组合 Queue{T} 存储元素，变更通知经 MiniEvent{T} 分发——Invoke 路径零分配。 变更通知为单一事件（AddListener）：入队 → Add（索引为队尾位置）、出队 → Remove（索引固定 0）、 Clear → Reset（非空才通知）；批量入队 / 出队逐项通知；无变更的操作（TryDequeue 空队列）不通知。
[Serializable] 标记与类型上的 [SerializeField] 供 Odin 序列化等第三方集成使用—— Unity 原生不序列化 Queue{T}，初始元素请经构造函数或 EnqueueRange 填充。

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

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 存在下一个元素返回 true，遍历结束返回 false。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
