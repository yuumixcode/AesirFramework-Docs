---
title: ObservableHashSet<T>.Enumerator<T>
description: "Runestone.AesirArchitecture.ObservableHashSet<T>.Enumerator<T> 的 API 文档"
---

# `ObservableHashSet<T>.Enumerator<T>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `ObservableHashSet<T>.Enumerator<T>`

**实现接口:** `System.Collections.Generic.IEnumerator<T>`，`System.Collections.IEnumerator`，`System.IDisposable`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
public struct ObservableHashSet<T>.Enumerator<T> : System.ValueType, 
System.Collections.Generic.IEnumerator<T>, 
System.Collections.IEnumerator, 
System.IDisposable 
```

可观察集合实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。

**备注**

内部组合 HashSet{T} 存储元素，使用 MiniEvent 管理监听者——Invoke 路径零分配（直接多播调用）。
[SerializeField] 标记 set 字段——Unity 原生不序列化 HashSet{T}， 安装 Odin Inspector 后该字段可被 Odin 序列化，便于在 Inspector 中编辑初始元素（与 ObservableDictionary{TKey, TValue} 行为一致）。

写操作完成后才触发事件，监听者回调中读取到的集合已是变更后的状态。 无变更的操作不触发事件：Add 重复元素、Remove 不存在的元素、Clear 空集合。

集合代数操作逐项触发事件：UnionWith / ExceptWith 逐项复用 Add / Remove，天然去重； IntersectWith / SymmetricExceptWith 需物化参数集合与自身快照（各两次临时分配，低频批量操作可接受）， SymmetricExceptWith 先触发全部 Removed、再触发全部 Added。

遍历性能：foreach 具体类型走结构体枚举器，零分配；通过 IReadOnlyObservableHashSet{T} / IEnumerable{T} 接口遍历会装箱一次枚举器（与 BCL HashSet{T} 行为一致）。

需要同步视图、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

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
