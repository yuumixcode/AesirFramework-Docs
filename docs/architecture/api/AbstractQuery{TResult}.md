---
title: AbstractQuery<TResult>
description: "Runestone.AesirArchitecture.AbstractQuery<TResult> 的 API 文档"
---

# `AbstractQuery<TResult>`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AbstractQuery<TResult>`

**实现接口:** `Runestone.AesirArchitecture.IContextHolder`，`Runestone.AesirArchitecture.IQuery<TResult>`，`Runestone.AesirArchitecture.ICanSetContext`，`Runestone.AesirArchitecture.ICanGetModel`，`Runestone.AesirArchitecture.ICanGetService`，`Runestone.AesirArchitecture.ICanExecuteQuery`

## 声明

``` csharp
public abstract class AbstractQuery<TResult> : Runestone.AesirArchitecture.IContextHolder, 
Runestone.AesirArchitecture.IQuery<TResult>, 
Runestone.AesirArchitecture.ICanSetContext, 
Runestone.AesirArchitecture.ICanGetModel, 
Runestone.AesirArchitecture.ICanGetService, 
Runestone.AesirArchitecture.ICanExecuteQuery 
```

查询基类。持有上下文引用，通过 OnExecute 执行查询逻辑并返回结果。

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`OnExecute()`](#method-onexecute) | 查询执行逻辑，子类必须实现 |

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

### OnExecute() {#method-onexecute}

查询执行逻辑，子类必须实现

``` csharp
protected abstract TResult OnExecute()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TResult` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
