---
title: GenericLocator<T>
description: "Runestone.AesirArchitecture.GenericLocator<T> 的 API 文档"
---

# `GenericLocator<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `GenericLocator<T>`

**实现接口:** `Runestone.AesirArchitecture.IGenericLocator<T>`，`System.IDisposable`

## 声明

``` csharp
[Serializable]
public sealed class GenericLocator<T> : Runestone.AesirArchitecture.IGenericLocator<T>, 
System.IDisposable where T : class
```

泛型对象定位器。按类型注册、查询与获取以 T 为基类的对象实例。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GenericLocator()`](#constructor-genericlocator) | — |

</div>

### GenericLocator() {#constructor-genericlocator}

按注册顺序获取所有已注册的实例集合

``` csharp
public GenericLocator<T>()
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetAllEntries()`](#method-getallentries) | 获取所有已注册键值对（仅供异常路径的近失识别使用） |
| [`GetAll()`](#method-getall) | 按注册顺序获取所有已注册的实例集合 |
| [`GetByType(Type)`](#method-getbytype-type) | 按 Type 获取实例（非泛型版本） |
| [`Get()`](#method-get) | 获取指定类型的实例。如果不存在，返回 null。 |
| [`IsRegistered()`](#method-isregistered) | 检查是否已注册指定类型的实例 |
| [`TryGet(ref TItem)`](#method-tryget-ref-titem) | 尝试获取指定类型的实例 |
| [`Clear()`](#method-clear) | 清空所有已注册的实例 |
| [`Dispose()`](#method-dispose) | 释放资源，清空所有注册。 |
| [`Register(Type, T)`](#method-register-type-t) | 按显式指定的类型注册一个实例。如果类型已存在，则覆盖原有注册（不改变其插入顺序位置）。 |
| [`Register(TItem)`](#method-register-titem) | 注册一个实例。如果类型已存在，则覆盖原有注册（不改变其插入顺序位置）。 |
| [`Unregister()`](#method-unregister) | 注销指定类型的实例 |

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

### GetAllEntries() {#method-getallentries}

获取所有已注册键值对（仅供异常路径的近失识别使用）

``` csharp
public IEnumerable<KeyValuePair<Type, T>> GetAllEntries()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<KeyValuePair<Type, T>>` |

</div>

### GetAll() {#method-getall}

``` csharp
[IteratorStateMachine]
public IEnumerable<T> GetAll()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `IEnumerable<T>` |

</div>

### GetByType(Type) {#method-getbytype-type}

按 Type 获取实例（非泛型版本）

``` csharp
public T GetByType(Type type)
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

获取指定类型的实例。如果不存在，返回 null。

``` csharp
public TItem Get<TItem>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `TItem` |

</div>

### IsRegistered() {#method-isregistered}

检查是否已注册指定类型的实例

``` csharp
public bool IsRegistered<TItem>()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### TryGet(ref TItem) {#method-tryget-ref-titem}

尝试获取指定类型的实例

``` csharp
public bool TryGet<TItem>(out ref TItem instance)
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

清空所有已注册的实例

``` csharp
public void Clear()
```
### Dispose() {#method-dispose}

释放资源，清空所有注册。

``` csharp
public void Dispose()
```
### Register(Type, T) {#method-register-type-t}

按显式指定的类型注册一个实例。如果类型已存在，则覆盖原有注册（不改变其插入顺序位置）。

``` csharp
public void Register(Type type, T instance)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `type` | `Type` |
| `instance` | `T` |

</div>

### Register(TItem) {#method-register-titem}

注册一个实例。如果类型已存在，则覆盖原有注册（不改变其插入顺序位置）。

``` csharp
public void Register<TItem>(TItem instance)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `instance` | `TItem` |

</div>

### Unregister() {#method-unregister}

注销指定类型的实例

``` csharp
public void Unregister<TItem>()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
