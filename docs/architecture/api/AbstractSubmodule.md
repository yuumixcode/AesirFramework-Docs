---
title: AbstractSubmodule
description: "Runestone.AesirArchitecture.AbstractSubmodule 的 API 文档"
---

# `AbstractSubmodule`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AbstractSubmodule`

**实现接口:** `Runestone.AesirArchitecture.IContextHolder`，`Runestone.AesirArchitecture.ICanSetContext`，`Runestone.AesirArchitecture.ICanInitialize`，`System.IDisposable`

## 声明

``` csharp
[Serializable]
public abstract class AbstractSubmodule : Runestone.AesirArchitecture.IContextHolder, 
Runestone.AesirArchitecture.ICanSetContext, 
Runestone.AesirArchitecture.ICanInitialize, 
System.IDisposable
```

子模块基类。持有上下文引用，通过 OnInitialize 和 OnDispose 管理生命周期。
Model 和 Service 的公共逻辑统一在此实现。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Initialized`](#property-initialized) | 是否已初始化（只读） |

</div>

### Initialized {#property-initialized}

是否已初始化（只读）

``` csharp
public bool Initialized { get; private set; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Dispose()`](#method-dispose) | 释放资源，触发 OnDispose |
| [`OnDispose()`](#method-ondispose) | 释放时的清理逻辑，子类可覆写 |
| [`OnInitialize()`](#method-oninitialize) | 初始化逻辑，子类可选覆写（默认空实现）。 |

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

### Dispose() {#method-dispose}

释放资源，触发 OnDispose

``` csharp
public void Dispose()
```
### OnDispose() {#method-ondispose}

释放时的清理逻辑，子类可覆写

``` csharp
protected virtual void OnDispose()
```
### OnInitialize() {#method-oninitialize}

初始化逻辑，子类可选覆写（默认空实现）。

``` csharp
protected virtual void OnInitialize()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
