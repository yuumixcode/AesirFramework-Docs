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

## 声明

``` csharp
public interface IReadOnlyObservableHashSet<T> : System.Collections.Generic.IEnumerable<T>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IReadOnlyCollection<T> 
```

只读可观察集合接口。
View 层通过此接口读取元素并订阅变更，不能修改集合。

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

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

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

### AddRemovedListener(Action<T>) {#method-addremovedlistener-action-t}

添加元素移除监听者。回调参数为被移除的元素。

``` csharp
public abstract AutoRemoveListenerHandle AddRemovedListener(Action<T> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### Contains(T) {#method-contains-t}

判断是否包含指定元素。

``` csharp
public abstract bool Contains(T item)
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

### RemoveAddedListener(Action<T>) {#method-removeaddedlistener-action-t}

移除元素添加监听者。

``` csharp
public abstract void RemoveAddedListener(Action<T> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

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

### RemoveRemovedListener(Action<T>) {#method-removeremovedlistener-action-t}

移除元素移除监听者。

``` csharp
public abstract void RemoveRemovedListener(Action<T> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
