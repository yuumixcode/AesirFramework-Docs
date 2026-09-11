---
title: IGenericLocator<T>
description: "Runestone.AesirArchitecture.IGenericLocator<T> 的 API 文档"
---

# `IGenericLocator<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**类型参数**

- `T` — 定位器管理的基类型，所有注册的实例必须可赋值给该类型。

## 声明

``` csharp
public interface IGenericLocator<T> where T : class
```

泛型定位器接口。提供按类型注册、查询与获取对象实例的契约。

**备注**

定位器的抽象契约，定义了注册、查询、获取与注销实例的标准接口。 GenericLocator{T} 是其默认实现，内部以 Dictionary{TKey,TValue} 存储注册关系。

注册与查询须使用相同的类型参数。若以具体类型注册（如 Register<Sword>）， 再以接口类型查询（如 Get<IWeapon>），将返回 null。

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

| 类型 | 说明 |
| :--- | :--- |
| `IEnumerable<KeyValuePair<Type, T>>` | 已注册键与实例的 KeyValuePair{TKey,TValue} 集合。 |

</div>

### GetAll() {#method-getall}

按注册顺序获取所有已注册的实例。

``` csharp
public abstract IEnumerable<T> GetAll()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `IEnumerable<T>` | 所有已注册实例的 IEnumerable{T} 集合，不含类型键，按注册顺序排列。 |

</div>

### GetByType(Type) {#method-getbytype-type}

按 Type 获取已注册的实例，不存在则返回 null。
用于依赖项校验等需要运行时 Type 查询的场景。

``` csharp
public abstract T GetByType(Type type)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `type` | `Type` | 要查询的 Type，作为注册键。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `T` | 已注册的实例；若未注册则返回 null。 |

</div>

### Get() {#method-get}

获取已注册的实例，不存在则返回 null。

``` csharp
public abstract TItem Get<TItem>()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `TItem` | 已注册的实例；若未注册则返回 null。 |

</div>

### IsRegistered() {#method-isregistered}

判断指定类型是否已注册。

``` csharp
public abstract bool IsRegistered<TItem>()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 已注册则返回 true；否则返回 false。 |

</div>

### TryGet(ref TItem) {#method-tryget-ref-titem}

尝试获取已注册的实例。返回是否成功找到对应类型的注册。

``` csharp
public abstract bool TryGet<TItem>(out ref TItem instance)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `instance` | `ref TItem` | 找到时输出已注册的实例；未找到时输出 null。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 成功找到则返回 true；未注册则返回 false。 |

</div>

### Clear() {#method-clear}

清空所有已注册的实例。

``` csharp
public abstract void Clear()
```

### Register(Type, T) {#method-register-type-t}

注册实例，以 Type 作为键。重复注册将覆盖已有实例。

**备注**

注意：注册与查询必须使用相同的类型参数。若以具体类型注册（如 Register<Sword>）， 再以接口类型查询（如 Get<IWeapon>），将返回 null。

``` csharp
public abstract void Register(Type type, T instance)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `type` | `Type` | 注册时使用的键类型，实例必须可赋值给该类型。 |
| `instance` | `T` | 要注册的实例。 |

</div>

### Register(TItem) {#method-register-titem}

注册实例，以 typeof(TItem) 作为键。重复注册将覆盖已有实例。

**备注**

注意：注册与查询必须使用相同的类型参数。若以具体类型注册（如 Register<Sword>）， 再以接口类型查询（如 Get<IWeapon>），将返回 null。

``` csharp
public abstract void Register<TItem>(TItem instance)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `instance` | `TItem` | 要注册的实例。 |

</div>

### Unregister() {#method-unregister}

注销指定类型的注册。

``` csharp
public abstract void Unregister<TItem>()
```

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
