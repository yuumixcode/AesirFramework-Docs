---
title: IReadOnlyObservableHashSet<T>
description: "Runestone.AesirArchitecture.IReadOnlyObservableHashSet<T> 的 API 文档"
---

# `IReadOnlyObservableHashSet<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.IReadOnlyCollection<T>`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
public interface IReadOnlyObservableHashSet<T> : System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

只读可观察集合接口。
View 层通过此接口读取元素并订阅变更，不能修改集合。

**备注**

事件语义与 MiniEvent{T} 一致：回调触发时集合已处于变更后的状态； 监听者抛异常按原生 C# 事件 fail-fast 向上传播，监听回调不应抛异常属框架约定。
变更通知仅覆盖最常用的三种：Added / Removed / Cleared。集合没有索引与键， 也就没有 Replaced / Updated 语义；需要同步视图、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

.NET Standard 2.1 无 IReadOnlySet<T>（.NET 5 才引入），只读侧无法继承只读集合契约， 因此本接口自行声明 Contains，其余读取能力继承自 IReadOnlyCollection{T}。

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddAddedListener(Action<T>)`](#method-addaddedlistener-action-t) | 添加元素监听者。回调参数为新增的元素。 |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | 添加清空监听者。集合被清空且清空前非空时触发。 |
| [`AddRemovedListener(Action<T>)`](#method-addremovedlistener-action-t) | 添加元素移除监听者。回调参数为被移除的元素。 |
| [`Contains(T)`](#method-contains-t) | 判断是否包含指定元素。 |
| [`RemoveAddedListener(Action<T>)`](#method-removeaddedlistener-action-t) | 移除元素添加监听者。 |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | 移除清空监听者。 |
| [`RemoveRemovedListener(Action<T>)`](#method-removeremovedlistener-action-t) | 移除元素移除监听者。 |

</div>

### AddAddedListener(Action<T>) {#method-addaddedlistener-action-t}

添加元素监听者。回调参数为新增的元素。

``` csharp
public abstract AutoRemoveListenerHandle AddAddedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<T>` | 元素添加时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听，避免手动管理生命周期。 |

</div>

### AddClearedListener(Action) {#method-addclearedlistener-action}

添加清空监听者。集合被清空且清空前非空时触发。

``` csharp
public abstract AutoRemoveListenerHandle AddClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | 集合清空时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### AddRemovedListener(Action<T>) {#method-addremovedlistener-action-t}

添加元素移除监听者。回调参数为被移除的元素。

``` csharp
public abstract AutoRemoveListenerHandle AddRemovedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<T>` | 元素移除时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### Contains(T) {#method-contains-t}

判断是否包含指定元素。

``` csharp
public abstract bool Contains(T item)
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

### RemoveAddedListener(Action<T>) {#method-removeaddedlistener-action-t}

移除元素添加监听者。

``` csharp
public abstract void RemoveAddedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<T>` | 先前通过 AddAddedListener 注册的回调函数。 |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

移除清空监听者。

``` csharp
public abstract void RemoveClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | 先前通过 AddClearedListener 注册的回调函数。 |

</div>

### RemoveRemovedListener(Action<T>) {#method-removeremovedlistener-action-t}

移除元素移除监听者。

``` csharp
public abstract void RemoveRemovedListener(Action<T> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<T>` | 先前通过 AddRemovedListener 注册的回调函数。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
