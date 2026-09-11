---
title: DictionaryUpdateEventArgs<TKey, TValue>
description: "Runestone.AesirArchitecture.DictionaryUpdateEventArgs<TKey, TValue> 的 API 文档"
---

# `DictionaryUpdateEventArgs<TKey, TValue>`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `DictionaryUpdateEventArgs<TKey, TValue>`

**类型参数**

- `TKey` — 键类型
- `TValue` — 值类型

## 声明

``` csharp
[IsReadOnly]
public struct DictionaryUpdateEventArgs<TKey, TValue> : System.ValueType  
```

字典更新事件参数。包含键、旧值与新值。

**备注**

仅在通过索引器为已存在的键赋新值时触发；新增键触发的是 Added 事件（参数为 KeyValuePair{TKey, TValue} ）。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`DictionaryUpdateEventArgs(TKey, TValue, TValue)`](#constructor-dictionaryupdateeventargs-tkey-tvalue-tvalue) | 构造更新事件参数。 |

</div>

### DictionaryUpdateEventArgs(TKey, TValue, TValue) {#constructor-dictionaryupdateeventargs-tkey-tvalue-tvalue}

构造更新事件参数。

``` csharp
public DictionaryUpdateEventArgs<TKey, TValue>(TKey key, TValue oldValue, TValue newValue)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `key` | `TKey` | 被更新的键 |
| `oldValue` | `TValue` | 更新前的旧值 |
| `newValue` | `TValue` | 更新后的新值 |

</div>

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Key`](#field-key) | 被更新的键。 |
| [`NewValue`](#field-newvalue) | 更新后的新值。 |
| [`OldValue`](#field-oldvalue) | 更新前的旧值。 |

</div>

### Key {#field-key}

被更新的键。

``` csharp
public readonly TKey Key;
```

### NewValue {#field-newvalue}

更新后的新值。

``` csharp
public readonly TValue NewValue;
```

### OldValue {#field-oldvalue}

更新前的旧值。

``` csharp
public readonly TValue OldValue;
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Equals(object)` | — | `ValueType` |
| `GetHashCode()` | — | `ValueType` |
| `ToString()` | — | `ValueType` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
