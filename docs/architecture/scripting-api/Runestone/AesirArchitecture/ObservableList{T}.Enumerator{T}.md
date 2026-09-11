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

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
public struct ObservableList<T>.Enumerator<T> : System.ValueType, 
System.Collections.Generic.IEnumerator<T>, 
System.Collections.IEnumerator, 
System.IDisposable 
```

可观察列表实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。

**备注**

内部组合 List{T} 存储元素，使用 MiniEvent 管理监听者——Invoke 路径零分配（直接多播调用）。 注意：订阅路径（AddListener / 句柄创建）有与监听者数量成正比的委托分配，勿在每帧订阅场景使用。
[SerializeField] 标记 items 字段使其可在 Inspector 中编辑初始元素； 反序列化填充不触发任何事件（与 ObservableValue{T} 行为一致）。

写操作完成后才触发事件，监听者回调中读取到的集合已是变更后的状态。 无变更的操作不触发事件：Remove 不存在的元素、Clear 空列表、索引器赋相同值。

遍历性能：foreach 具体类型走结构体枚举器，零分配；通过 IReadOnlyObservableList{T} / IEnumerable{T} 接口遍历会装箱一次枚举器（与 BCL List{T} 行为一致）。

需要 Move、Sort、SynchronizedView、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

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
