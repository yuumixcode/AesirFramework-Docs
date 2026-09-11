---
title: ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>
description: "Runestone.AesirArchitecture.ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue> 的 API 文档"
---

# `ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>`

**实现接口:** `System.Collections.Generic.IEnumerator<KeyValuePair<TKey, TValue>>`，`System.Collections.IEnumerator`，`System.IDisposable`

**类型参数**

- `TKey` — 键类型
- `TValue` — 值类型

## 声明

``` csharp
public struct ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue> : System.ValueType, 
System.Collections.Generic.IEnumerator<KeyValuePair<TKey, TValue>>, 
System.Collections.IEnumerator, 
System.IDisposable  
```

可观察字典实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。

**备注**

内部组合 Dictionary{TKey,TValue} 存储键值，使用 MiniEvent 管理监听者——Invoke 路径零分配（直接多播调用）。
[SerializeField] 标记 dictionary 字段——Unity 原生不序列化 Dictionary{TKey, TValue}， 安装 Odin Inspector 后该字段可被 Odin 序列化，便于在 Inspector 中编辑初始键值。

写操作完成后才触发事件，监听者回调中读取到的集合已是变更后的状态。 索引器为已存在的键赋相同值时跳过；为不存在的键赋值时触发 Added 而非 Updated。

遍历性能：foreach 具体类型走结构体枚举器，零分配；通过 IReadOnlyObservableDictionary{TKey, TValue} / IEnumerable{T} 接口遍历会装箱一次枚举器（与 BCL Dictionary{TKey, TValue} 行为一致）。

需要同步视图、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Current`](#property-current) | 获取当前位置的键值对。 |

</div>

### Current {#property-current}

获取当前位置的键值对。

``` csharp
public KeyValuePair<TKey, TValue> Current { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`MoveNext()`](#method-movenext) | 前进到下一个键值对。 |

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

前进到下一个键值对。

``` csharp
public bool MoveNext()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 存在下一个键值对返回 true，遍历结束返回 false。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
