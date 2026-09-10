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

## 声明

``` csharp
public interface IReadOnlyObservableList<T> : System.Collections.Generic.IReadOnlyList<T>, 
System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

只读可观察列表接口。
View 层通过此接口枚举元素并订阅变更，不能修改集合。

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

添加清空监听者。集合被清空且清空前非空时触发。

``` csharp
public abstract AutoRemoveListenerHandle AddClearedListener(Action callback)
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

添加元素移除监听者。回调参数包含被移除元素及其移除前所在索引。

``` csharp
public abstract AutoRemoveListenerHandle AddRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
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

添加元素替换监听者。索引器赋值且新旧值不同时触发，回调参数包含索引、旧项与新项。

``` csharp
public abstract AutoRemoveListenerHandle AddReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
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

### RemoveAddedListener(Action<CollectionAddEventArgs<T>>) {#method-removeaddedlistener-action-collectionaddeventargs-t}

移除元素添加监听者。

``` csharp
public abstract void RemoveAddedListener(Action<CollectionAddEventArgs<T>> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionAddEventArgs<T>>` |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

移除清空监听者。

``` csharp
public abstract void RemoveClearedListener(Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

### RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>>) {#method-removeremovedlistener-action-collectionremoveeventargs-t}

移除元素移除监听者。

``` csharp
public abstract void RemoveRemovedListener(Action<CollectionRemoveEventArgs<T>> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionRemoveEventArgs<T>>` |

</div>

### RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>>) {#method-removereplacedlistener-action-collectionreplaceeventargs-t}

移除元素替换监听者。

``` csharp
public abstract void RemoveReplacedListener(Action<CollectionReplaceEventArgs<T>> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<CollectionReplaceEventArgs<T>>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
