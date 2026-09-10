---
title: RemoveListenerHandleCollection
description: "Runestone.AesirArchitecture.RemoveListenerHandleCollection 的 API 文档"
---

# `RemoveListenerHandleCollection`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `RemoveListenerHandleCollection`

## 声明

``` csharp
public sealed class RemoveListenerHandleCollection
```

监听句柄集合。管理 AutoRemoveListenerHandle 句柄的添加与批量移除， 供 RemoveListenerTrigger 和 RemoveListenerOnSceneUnloadedTrigger 复用。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`RemoveListenerHandleCollection()`](#constructor-removelistenerhandlecollection) | — |

</div>

### RemoveListenerHandleCollection() {#constructor-removelistenerhandlecollection}

``` csharp
public RemoveListenerHandleCollection()
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Add(AutoRemoveListenerHandle)`](#method-add-autoremovelistenerhandle) | 添加监听句柄，使其在调用条件满足时自动移除 |
| [`RemoveAllListeners()`](#method-removealllisteners) | 移除所有已注册的监听并清空列表 |

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

### Add(AutoRemoveListenerHandle) {#method-add-autoremovelistenerhandle}

添加监听句柄，使其在调用条件满足时自动移除

``` csharp
public void Add(AutoRemoveListenerHandle handle)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `handle` | `AutoRemoveListenerHandle` |

</div>

### RemoveAllListeners() {#method-removealllisteners}

移除所有已注册的监听并清空列表

``` csharp
public void RemoveAllListeners()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
