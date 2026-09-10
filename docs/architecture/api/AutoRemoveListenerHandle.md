---
title: AutoRemoveListenerHandle
description: "Runestone.AesirArchitecture.AutoRemoveListenerHandle 的 API 文档"
---

# `AutoRemoveListenerHandle`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `AutoRemoveListenerHandle`

**实现接口:** `System.IDisposable`

## 声明

``` csharp
public struct AutoRemoveListenerHandle : System.ValueType, 
System.IDisposable
```

自动移除监听句柄。包装注销回调。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AutoRemoveListenerHandle(Action)`](#constructor-autoremovelistenerhandle-action) | — |

</div>

### AutoRemoveListenerHandle(Action) {#constructor-autoremovelistenerhandle-action}

``` csharp
public AutoRemoveListenerHandle(Action removeListenerCallback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListenerCallback` | `Action` |

</div>

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Dispose()`](#method-dispose) | 执行移除监听，重复调用安全 |

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

### Dispose() {#method-dispose}

执行移除监听，重复调用安全

``` csharp
public void Dispose()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
