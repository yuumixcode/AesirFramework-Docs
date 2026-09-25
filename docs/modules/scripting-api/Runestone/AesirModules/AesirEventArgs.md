---
title: AesirEventArgs
description: "Runestone.AesirModules.AesirEventArgs 的 API 文档"
---

# `AesirEventArgs`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `AesirEventArgs`

**实现接口:** `System.ICloneable`

## 声明

``` csharp
[Serializable]
public abstract class AesirEventArgs : System.ICloneable
```

事件参数基类。所有自定义事件参数继承此类，作为事件数据载体在 EventModule 中传递。
注意：AesirEventArgs 本身不持有监听者，仅作为参数实例。 订阅管理由 EventModule 的 BindingRegistry 负责。

通过 WithFilter / WithFilters 可链式声明订阅者过滤器， 实现"只让特定范围的订阅者收到"的精确投递。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Filters`](#property-filters) | 只读过滤器列表视图。未添加任何过滤器时为 null。 |
| [`Sender`](#property-sender) | 事件发布者。由 EventModule 在分发时写入。 |

</div>

### Filters {#property-filters}

只读过滤器列表视图。未添加任何过滤器时为 null。

``` csharp
public IReadOnlyList<ISubscriberFilter> Filters { get; }
```

### Sender {#property-sender}

事件发布者。由 EventModule 在分发时写入。

``` csharp
public object Sender { get; private set; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SetSender(object)`](#method-setsender-object) | 设置事件发布者。 |
| [`WithFilter(ISubscriberFilter)`](#method-withfilter-isubscriberfilter) | 链式添加一个订阅者过滤器。多次调用依次叠加，分发时全部过滤器通过才投递。 过滤器随事件参数实例存在：缓存复用的参数实例（如 AesirEventArgsSO）会保留已添加的过滤器。 |
| [`WithFilters(ISubscriberFilter[])`](#method-withfilters-isubscriberfilter) | 链式添加一组订阅者过滤器。 |
| [`Clone()`](#method-clone) | 创建事件参数的浅拷贝。供用户在需要隔离分发实例时手动调用。 基于 MemberwiseClone 实现：值类型字段会被独立复制， 但引用类型字段（如数组、List{T}、自定义类等） 仅复制引用，克隆体与原实例会共享同一个底层对象。 若事件参数子类包含可变的引用类型字段，且需要保证各订阅者互不影响， 应在该子类中重写本方法以实现深拷贝。 过滤器列表 Filters 同样仅复制引用，克隆体与原实例共享同一过滤器列表。 |
| [`Invoke()`](#method-invoke) | 使用已设置的发布者触发事件。需先通过 SetSender 设置发布者。 |
| [`Invoke(object)`](#method-invoke-object) | 使用指定发布者触发事件。 |

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

### SetSender(object) {#method-setsender-object}

设置事件发布者。

``` csharp
public AesirEventArgs SetSender(object sender)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sender` | `object` | 发布者对象。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirEventArgs` | 当前事件参数实例（支持链式调用）。 |

</div>

### WithFilter(ISubscriberFilter) {#method-withfilter-isubscriberfilter}

链式添加一个订阅者过滤器。多次调用依次叠加，分发时全部过滤器通过才投递。 过滤器随事件参数实例存在：缓存复用的参数实例（如 AesirEventArgsSO）会保留已添加的过滤器。

``` csharp
public AesirEventArgs WithFilter(ISubscriberFilter filter)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `filter` | `ISubscriberFilter` | 过滤器实例。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirEventArgs` | 当前事件参数实例（支持链式调用）。 |

</div>

### WithFilters(ISubscriberFilter[]) {#method-withfilters-isubscriberfilter}

链式添加一组订阅者过滤器。

``` csharp
public AesirEventArgs WithFilters(params ISubscriberFilter[] filters)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `filters` | `ISubscriberFilter[]` | 过滤器实例数组。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirEventArgs` | 当前事件参数实例（支持链式调用）。 |

</div>

### Clone() {#method-clone}

创建事件参数的浅拷贝。供用户在需要隔离分发实例时手动调用。 基于 MemberwiseClone 实现：值类型字段会被独立复制， 但引用类型字段（如数组、List{T}、自定义类等） 仅复制引用，克隆体与原实例会共享同一个底层对象。 若事件参数子类包含可变的引用类型字段，且需要保证各订阅者互不影响， 应在该子类中重写本方法以实现深拷贝。 过滤器列表 Filters 同样仅复制引用，克隆体与原实例共享同一过滤器列表。

``` csharp
public object Clone()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `object` | 事件参数的克隆实例。 |

</div>

### Invoke() {#method-invoke}

使用已设置的发布者触发事件。需先通过 SetSender 设置发布者。

``` csharp
public void Invoke()
```

### Invoke(object) {#method-invoke-object}

使用指定发布者触发事件。

``` csharp
public void Invoke(object sender)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sender` | `object` | 发布者对象。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
