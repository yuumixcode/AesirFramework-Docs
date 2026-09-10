---
title: IContext
description: "Runestone.AesirArchitecture.IContext 的 API 文档"
---

# `IContext`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.IDisposable`

## 声明

``` csharp
public interface IContext : System.IDisposable
```

模块上下文接口。提供模块注册与获取。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Initialized`](#property-initialized) | — |

</div>

### Initialized {#property-initialized}

``` csharp
public bool Initialized { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetAllModels()`](#method-getallmodels) | 获取所有已注册的 Model 列表 |
| [`GetAllServices()`](#method-getallservices) | 获取所有已注册的 Service 列表 |
| [`GetModel()`](#method-getmodel) | 获取已注册的 Model |
| [`GetService()`](#method-getservice) | 获取已注册的 Service |
| [`RegisterModel(T)`](#method-registermodel-t) | 注册 Model |
| [`RegisterService(T)`](#method-registerservice-t) | 注册 Service |

</div>

### GetAllModels() {#method-getallmodels}

获取所有已注册的 Model 列表

``` csharp
public abstract IEnumerable<IModel> GetAllModels()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<IModel>` |

</div>

### GetAllServices() {#method-getallservices}

获取所有已注册的 Service 列表

``` csharp
public abstract IEnumerable<IService> GetAllServices()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<IService>` |

</div>

### GetModel() {#method-getmodel}

获取已注册的 Model

``` csharp
public abstract T GetModel<T>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `T` |

</div>

### GetService() {#method-getservice}

获取已注册的 Service

``` csharp
public abstract T GetService<T>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `T` |

</div>

### RegisterModel(T) {#method-registermodel-t}

注册 Model

``` csharp
public abstract void RegisterModel<T>(T model)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `model` | `T` |

</div>

### RegisterService(T) {#method-registerservice-t}

注册 Service

``` csharp
public abstract void RegisterService<T>(T service)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `service` | `T` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
