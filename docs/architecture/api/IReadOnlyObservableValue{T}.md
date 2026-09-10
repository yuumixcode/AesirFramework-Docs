---
title: IReadOnlyObservableValue<T>
description: "Runestone.AesirArchitecture.IReadOnlyObservableValue<T> 的 API 文档"
---

# `IReadOnlyObservableValue<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

## 声明

``` csharp
public interface IReadOnlyObservableValue<T> 
```

只读可观察属性接口。
View 层通过此接口添加监听，不能修改值。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Value`](#property-value) | — |

</div>

### Value {#property-value}

``` csharp
public T Value { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddListener(Action<T>)`](#method-addlistener-action-t) | 添加监听者。回调参数为新值。 |
| [`AddListenerAndInvoke(Action<T>)`](#method-addlistenerandinvoke-action-t) | 添加监听并立即触发一次当前值，用于初始化时同步监听方状态。 |
| [`InvokeEvent()`](#method-invokeevent) | 触发值变更通知，用于强制刷新监听方状态。 |
| [`RemoveListener(Action<T>)`](#method-removelistener-action-t) | 移除监听者。 |

</div>

### AddListener(Action<T>) {#method-addlistener-action-t}

添加监听者。回调参数为新值。

``` csharp
public abstract AutoRemoveListenerHandle AddListener(Action<T> callback)
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

### AddListenerAndInvoke(Action<T>) {#method-addlistenerandinvoke-action-t}

添加监听并立即触发一次当前值，用于初始化时同步监听方状态。

``` csharp
public abstract AutoRemoveListenerHandle AddListenerAndInvoke(Action<T> callback)
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

### InvokeEvent() {#method-invokeevent}

触发值变更通知，用于强制刷新监听方状态。

``` csharp
public abstract void InvokeEvent()
```
### RemoveListener(Action<T>) {#method-removelistener-action-t}

移除监听者。

``` csharp
public abstract void RemoveListener(Action<T> callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<T>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
