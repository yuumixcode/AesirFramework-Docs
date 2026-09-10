---
title: AbstractContext<T>
description: "Runestone.AesirArchitecture.AbstractContext<T> 的 API 文档"
---

# `AbstractContext<T>`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AbstractContext<T>`

**实现接口:** `Runestone.AesirArchitecture.IContext`，`System.IDisposable`

## 声明

``` csharp
[Serializable]
public abstract class AbstractContext<T> : Runestone.AesirArchitecture.IContext, 
System.IDisposable where T : new(), Runestone.AesirArchitecture.AbstractContext<T>
```

上下文基类。纯 C# 实现，不依赖 MonoBehaviour。
子类在 Configure 中注册 Model 和 Service，通过 Instance 获取全局单例。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Initialized`](#property-initialized) | 是否已初始化（只读） |
| [`Instance`](#property-instance) | 获取当前上下文类型的单例接口实例。首次访问时自动创建并初始化。 |

</div>

### Initialized {#property-initialized}

是否已初始化（只读）

``` csharp
public bool Initialized { get; private set; }
```
### Instance {#property-instance}

获取当前上下文类型的单例接口实例。首次访问时自动创建并初始化。

``` csharp
public static T Instance { get; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetAllModels()`](#method-getallmodels) | 获取所有已注册的 Model 列表 |
| [`GetAllServices()`](#method-getallservices) | 获取所有已注册的 Service 列表 |
| [`GetModel()`](#method-getmodel) | 获取已注册的 Model。 |
| [`GetService()`](#method-getservice) | 获取已注册的 Service。 |
| [`Dispose()`](#method-dispose) | 释放资源。逆序销毁 Service 和 Model，清空容器。 |
| [`Initialize()`](#method-initialize) | 统一初始化。调用 Configure 注册模块后，按注册顺序依次初始化 Model 和 Service。 开发者需保证注册顺序满足依赖关系——被依赖的模块先注册。运行时通过 GetModel / GetService 获取未注册模块会抛出异常。 |
| [`RegisterModel(TModel)`](#method-registermodel-tmodel) | 注册 Model 并绑定上下文。 若该类型已注册，视为动态替换：输出一条 Warning 日志，旧实例会被 Dispose 后再覆盖。 |
| [`RegisterService(TService)`](#method-registerservice-tservice) | 注册 Service 并绑定上下文。 若上下文已完成统一初始化，则立即初始化该 Service。若该类型已注册，视为动态替换：输出一条 Warning 日志，旧实例会被 Dispose 后再覆盖。 |
| [`Configure()`](#method-configure) | 配置上下文模块，子类在此注册 Model 和 Service。 |
| [`OnDispose()`](#method-ondispose) | 子类可选覆写，在释放前执行自定义清理 |

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

### GetAllModels() {#method-getallmodels}

获取所有已注册的 Model 列表

``` csharp
public IEnumerable<IModel> GetAllModels()
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
public IEnumerable<IService> GetAllServices()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<IService>` |

</div>

### GetModel() {#method-getmodel}

获取已注册的 Model。

``` csharp
public TModel GetModel<TModel>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TModel` |

</div>

### GetService() {#method-getservice}

获取已注册的 Service。

``` csharp
public TService GetService<TService>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TService` |

</div>

### Dispose() {#method-dispose}

释放资源。逆序销毁 Service 和 Model，清空容器。

``` csharp
public void Dispose()
```
### Initialize() {#method-initialize}

统一初始化。调用 Configure 注册模块后，按注册顺序依次初始化 Model 和 Service。
开发者需保证注册顺序满足依赖关系——被依赖的模块先注册。运行时通过 GetModel / GetService 获取未注册模块会抛出异常。

``` csharp
public void Initialize()
```
### RegisterModel(TModel) {#method-registermodel-tmodel}

注册 Model 并绑定上下文。
若该类型已注册，视为动态替换：输出一条 Warning 日志，旧实例会被 Dispose 后再覆盖。

``` csharp
public void RegisterModel<TModel>(TModel model)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `model` | `TModel` |

</div>

### RegisterService(TService) {#method-registerservice-tservice}

注册 Service 并绑定上下文。
若上下文已完成统一初始化，则立即初始化该 Service。若该类型已注册，视为动态替换：输出一条 Warning 日志，旧实例会被 Dispose 后再覆盖。

``` csharp
public void RegisterService<TService>(TService service)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `service` | `TService` |

</div>

### Configure() {#method-configure}

配置上下文模块，子类在此注册 Model 和 Service。

``` csharp
protected abstract void Configure()
```
### OnDispose() {#method-ondispose}

子类可选覆写，在释放前执行自定义清理

``` csharp
protected virtual void OnDispose()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
