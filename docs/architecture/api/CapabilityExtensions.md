---
title: CapabilityExtensions
description: "Runestone.AesirArchitecture.CapabilityExtensions 的 API 文档"
---

# `CapabilityExtensions`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `CapabilityExtensions`

## 声明

``` csharp
[Extension]
public static class CapabilityExtensions
```

能力扩展方法集合

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetModel(ICanGetModel)`](#method-getmodel-icangetmodel) | 获取已注册的 Model。未注册时由 GetModel{T} 抛出异常； 已注册但尚未初始化时，抛出注册顺序错误或循环依赖异常。 |
| [`GetService(ICanGetService)`](#method-getservice-icangetservice) | 获取已注册的 Service。未注册时由 GetService{T} 抛出异常； 已注册但尚未初始化时抛出——Service 间依赖为注册顺序问题，Model 初始化阶段调用则属两阶段初始化的必然约束。 |
| [`ExecuteQuery(ICanExecuteQuery)`](#method-executequery-icanexecutequery) | 执行无参查询 |
| [`ExecuteQuery(ICanExecuteQuery, IQuery<TResult>)`](#method-executequery-icanexecutequery-iquery-tresult) | 执行带参查询 |
| [`ExecuteCommand(ICanExecuteCommand)`](#method-executecommand-icanexecutecommand) | 执行无参命令 |
| [`ExecuteCommand(ICanExecuteCommand, T)`](#method-executecommand-icanexecutecommand-t) | 执行带参命令 |

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

### GetModel(ICanGetModel) {#method-getmodel-icangetmodel}

获取已注册的 Model。未注册时由 GetModel{T} 抛出异常； 已注册但尚未初始化时，抛出注册顺序错误或循环依赖异常。

``` csharp
[Extension]
[Ext] public static T GetModel<T>(this ICanGetModel self)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanGetModel` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `T` |

</div>

### GetService(ICanGetService) {#method-getservice-icangetservice}

获取已注册的 Service。未注册时由 GetService{T} 抛出异常； 已注册但尚未初始化时抛出——Service 间依赖为注册顺序问题，Model 初始化阶段调用则属两阶段初始化的必然约束。

``` csharp
[Extension]
[Ext] public static T GetService<T>(this ICanGetService self)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanGetService` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `T` |

</div>

### ExecuteQuery(ICanExecuteQuery) {#method-executequery-icanexecutequery}

执行无参查询

``` csharp
[Extension]
[Ext] public static TResult ExecuteQuery<TQuery, TResult>(this ICanExecuteQuery self)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanExecuteQuery` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TResult` |

</div>

### ExecuteQuery(ICanExecuteQuery, IQuery<TResult>) {#method-executequery-icanexecutequery-iquery-tresult}

执行带参查询

``` csharp
[Extension]
[Ext] public static TResult ExecuteQuery<TResult>(this ICanExecuteQuery self, IQuery<TResult> query)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanExecuteQuery` |
| `query` | `IQuery<TResult>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TResult` |

</div>

### ExecuteCommand(ICanExecuteCommand) {#method-executecommand-icanexecutecommand}

执行无参命令

``` csharp
[Extension]
[Ext] public static void ExecuteCommand<T>(this ICanExecuteCommand self)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanExecuteCommand` |

</div>

### ExecuteCommand(ICanExecuteCommand, T) {#method-executecommand-icanexecutecommand-t}

执行带参命令

``` csharp
[Extension]
[Ext] public static void ExecuteCommand<T>(this ICanExecuteCommand self, T command)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `self` | `ICanExecuteCommand` |
| `command` | `T` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
