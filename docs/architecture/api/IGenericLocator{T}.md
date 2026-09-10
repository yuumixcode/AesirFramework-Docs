---
title: IGenericLocator<T>
description: "Runestone.AesirArchitecture.IGenericLocator<T> 的 API 文档"
---

# `IGenericLocator<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

## 声明

``` csharp
public interface IGenericLocator<T> where T : class
```

泛型定位器接口。提供按类型注册、查询与获取对象实例的契约。

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetAllEntries()`](#method-getallentries) | 获取所有已注册键值对（仅供异常路径的近失识别使用）。 |
| [`GetAll()`](#method-getall) | 按注册顺序获取所有已注册的实例。 |
| [`GetByType(Type)`](#method-getbytype-type) | 按 Type 获取已注册的实例，不存在则返回 null。 用于依赖项校验等需要运行时 Type 查询的场景。 |
| [`Get()`](#method-get) | 获取已注册的实例，不存在则返回 null。 |
| [`IsRegistered()`](#method-isregistered) | 判断指定类型是否已注册。 |
| [`TryGet(ref TItem)`](#method-tryget-ref-titem) | 尝试获取已注册的实例。返回是否成功找到对应类型的注册。 |
| [`Clear()`](#method-clear) | 清空所有已注册的实例。 |
| [`Register(Type, T)`](#method-register-type-t) | 注册实例，以 Type 作为键。重复注册将覆盖已有实例。 |
| [`Register(TItem)`](#method-register-titem) | 注册实例，以 typeof(TItem) 作为键。重复注册将覆盖已有实例。 |
| [`Unregister()`](#method-unregister) | 注销指定类型的注册。 |

</div>

### GetAllEntries() {#method-getallentries}

获取所有已注册键值对（仅供异常路径的近失识别使用）。

``` csharp
public abstract IEnumerable<KeyValuePair<Type, T>> GetAllEntries()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<KeyValuePair<Type, T>>` |

</div>

### GetAll() {#method-getall}

按注册顺序获取所有已注册的实例。

``` csharp
public abstract IEnumerable<T> GetAll()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<T>` |

</div>

### GetByType(Type) {#method-getbytype-type}

按 Type 获取已注册的实例，不存在则返回 null。
用于依赖项校验等需要运行时 Type 查询的场景。

``` csharp
public abstract T GetByType(Type type)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `type` | `Type` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `T` |

</div>

### Get() {#method-get}

获取已注册的实例，不存在则返回 null。

``` csharp
public abstract TItem Get<TItem>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TItem` |

</div>

### IsRegistered() {#method-isregistered}

判断指定类型是否已注册。

``` csharp
public abstract bool IsRegistered<TItem>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### TryGet(ref TItem) {#method-tryget-ref-titem}

尝试获取已注册的实例。返回是否成功找到对应类型的注册。

``` csharp
public abstract bool TryGet<TItem>(out ref TItem instance)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `instance` | `ref TItem` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Clear() {#method-clear}

清空所有已注册的实例。

``` csharp
public abstract void Clear()
```
### Register(Type, T) {#method-register-type-t}

注册实例，以 Type 作为键。重复注册将覆盖已有实例。

``` csharp
public abstract void Register(Type type, T instance)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `type` | `Type` |
| `instance` | `T` |

</div>

### Register(TItem) {#method-register-titem}

注册实例，以 typeof(TItem) 作为键。重复注册将覆盖已有实例。

``` csharp
public abstract void Register<TItem>(TItem instance)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `instance` | `TItem` |

</div>

### Unregister() {#method-unregister}

注销指定类型的注册。

``` csharp
public abstract void Unregister<TItem>()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
