---
title: MiniEvent
description: "Runestone.AesirArchitecture.MiniEvent 的 API 文档"
---

# `MiniEvent`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `MiniEvent`

**实现接口:** `System.IDisposable`

## 声明

``` csharp
public sealed class MiniEvent : System.IDisposable
```

单参事件

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`MiniEvent()`](#constructor-minievent) | — |

</div>

### MiniEvent() {#constructor-minievent}

``` csharp
public MiniEvent()
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddListener(Action)`](#method-addlistener-action) | 添加监听者，并返回可自动移除的监听句柄 |
| [`GetListeners()`](#method-getlisteners) | 获取当前所有已注册的委托列表 |
| [`Dispose()`](#method-dispose) | 清空所有委托引用，释放内存 |
| [`Invoke()`](#method-invoke) | 调用事件，通知所有监听者 |
| [`RemoveListener(Action)`](#method-removelistener-action) | 移除监听者 |

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

### AddListener(Action) {#method-addlistener-action}

添加监听者，并返回可自动移除的监听句柄

``` csharp
public AutoRemoveListenerHandle AddListener(Action listener)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `listener` | `Action` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### GetListeners() {#method-getlisteners}

获取当前所有已注册的委托列表

``` csharp
public Delegate[] GetListeners()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `Delegate[]` |

</div>

### Dispose() {#method-dispose}

清空所有委托引用，释放内存

``` csharp
public void Dispose()
```
### Invoke() {#method-invoke}

调用事件，通知所有监听者

``` csharp
public void Invoke()
```
### RemoveListener(Action) {#method-removelistener-action}

移除监听者

``` csharp
public void RemoveListener(Action listener)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `listener` | `Action` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
