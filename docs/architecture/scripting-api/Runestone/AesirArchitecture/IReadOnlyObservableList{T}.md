---
title: IReadOnlyObservableList<T>
description: "Runestone.AesirArchitecture.IReadOnlyObservableList<T> 的 API 文档"
---

# `IReadOnlyObservableList<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.Collections.Generic.IReadOnlyList<T>`，`System.Collections.Generic.IEnumerable<T>`，`System.Collections.IEnumerable`，`System.Collections.Generic.IReadOnlyCollection<T>`

**类型参数**

- `T` — 元素类型

## 声明

``` csharp
public interface IReadOnlyObservableList<T> : System.Collections.Generic.IReadOnlyList<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

只读可观察列表接口。
View 层通过此接口枚举元素并订阅变更，不能修改集合。

**备注**

事件语义与 MiniEvent{T} 一致：回调触发时集合已处于变更后的状态； 监听者抛异常按原生 C# 事件 fail-fast 向上传播，监听回调不应抛异常属框架约定。
变更通知仅覆盖游戏 UI 绑定最常用的四种：Added / Removed / Replaced / Cleared。 需要 Move、Sort、SynchronizedView、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddAddedListener(Action<CollectionAddEventArgs<T>>)`](#method-addaddedlistener-action-collectionaddeventargs-t) | 添加元素监听者。回调参数包含新元素及其索引。 |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | 添加清空监听者。集合被清空且清空前非空时触发。 |
| [`AddRemovedListener(Action<CollectionRemoveEventArgs<T>>)`](#method-addremovedlistener-action-collectionremoveeventargs-t) | 添加元素移除监听者。回调参数包含被移除元素及其移除前所在索引。 |
| [`AddReplacedListener(Action<CollectionReplaceEventArgs<T>>)`](#method-addreplacedlistener-action-collectionreplaceeventargs-t) | 添加元素替换监听者。索引器赋值且新旧值不同时触发，回调参数包含索引、旧项与新项。 |
| [`RemoveAddedListener(Action<CollectionAddEventArgs<T>>)`](#method-removeaddedlistener-action-collectionaddeventargs-t) | 移除元素添加监听者。 |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | 移除清空监听者。 |
| [`RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>)`](#method-removeremovedlistener-action-collectionremoveeventargs-t) | 移除元素移除监听者。 |
| [`RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>)`](#method-removereplacedlistener-action-collectionreplaceeventargs-t) | 移除元素替换监听者。 |

</div>

### AddAddedListener(Action<CollectionAddEventArgs<T>>) {#method-addaddedlistener-action-collectionaddeventargs-t}

添加元素监听者。回调参数包含新元素及其索引。

``` csharp
public abstract AutoRemoveListenerHandle AddAddedListener(Action<CollectionAddEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` | 元素添加时调用的回调函数。 |

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

### AddRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-addremovedlistener-action-collectionremoveeventargs-t}

添加元素移除监听者。回调参数包含被移除元素及其移除前所在索引。

``` csharp
public abstract AutoRemoveListenerHandle AddRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` | 元素移除时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### AddReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-addreplacedlistener-action-collectionreplaceeventargs-t}

添加元素替换监听者。索引器赋值且新旧值不同时触发，回调参数包含索引、旧项与新项。

``` csharp
public abstract AutoRemoveListenerHandle AddReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` | 元素替换时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### RemoveAddedListener(Action<CollectionAddEventArgs<T>>) {#method-removeaddedlistener-action-collectionaddeventargs-t}

移除元素添加监听者。

``` csharp
public abstract void RemoveAddedListener(Action<CollectionAddEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` | 先前通过 AddAddedListener 注册的回调函数。 |

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

### RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-removeremovedlistener-action-collectionremoveeventargs-t}

移除元素移除监听者。

``` csharp
public abstract void RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` | 先前通过 AddRemovedListener 注册的回调函数。 |

</div>

### RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-removereplacedlistener-action-collectionreplaceeventargs-t}

移除元素替换监听者。

``` csharp
public abstract void RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` | 先前通过 AddReplacedListener 注册的回调函数。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
