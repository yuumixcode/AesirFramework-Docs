---
title: IObservableValue<T>
description: "Runestone.AesirArchitecture.IObservableValue<T> 的 API 文档"
---

# `IObservableValue<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `Runestone.AesirArchitecture.IReadOnlyObservableValue<T>`

## 声明

``` csharp
public interface IObservableValue<T> : Runestone.AesirArchitecture.IReadOnlyObservableValue<T> 
```

完整可观察属性接口。
Presenter 层通过此接口读写数据。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Value`](#property-value) | — |

</div>

### Value {#property-value}

``` csharp
public T Value { get; set; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SetValue(T)`](#method-setvalue-t) | 设置值。语义等价于 Value 的 setter，便于以方法形式调用。 |
| [`SetValueSilently(T)`](#method-setvaluesilently-t) | 静默设置值，不触发通知。用于反序列化或批量更新后统一触发。 |

</div>

### SetValue(T) {#method-setvalue-t}

设置值。语义等价于 Value 的 setter，便于以方法形式调用。

``` csharp
public abstract void SetValue(T value)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `value` | `T` |

</div>

### SetValueSilently(T) {#method-setvaluesilently-t}

静默设置值，不触发通知。用于反序列化或批量更新后统一触发。

``` csharp
public abstract void SetValueSilently(T value)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `value` | `T` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
