---
title: IReadOnlyObservableDictionary<TKey, TValue>
description: "Runestone.AesirArchitecture.IReadOnlyObservableDictionary<TKey, TValue> 的 API 文档"
---

# `IReadOnlyObservableDictionary<TKey, TValue>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.Collections.Generic.IReadOnlyDictionary<TKey, TValue>`，`System.Collections.Generic.IEnumerable<KeyValuePair<TKey, TValue>>`，`System.Collections.IEnumerable`，`System.Collections.Generic.IReadOnlyCollection<KeyValuePair<TKey, TValue>>`

**类型参数**

- `TKey` — 键类型
- `TValue` — 值类型

## 声明

``` csharp
public interface IReadOnlyObservableDictionary<TKey, TValue> : System.Collections.Generic.IReadOnlyDictionary<TKey, TValue>, 
System.Collections.Generic.IEnumerable<KeyValuePair<TKey, TValue>>, 
System.Collections.IEnumerable, 
System.Collections.Generic.IReadOnlyCollection<KeyValuePair<TKey, TValue>>  
```

只读可观察字典接口。
View 层通过此接口读取键值并订阅变更，不能修改集合。

**备注**

事件语义与 MiniEvent{T} 一致：回调触发时集合已处于变更后的状态； 监听者抛异常按原生 C# 事件 fail-fast 向上传播，监听回调不应抛异常属框架约定。
变更通知仅覆盖最常用的四种：Added / Removed / Updated / Cleared。 需要同步视图、R3 集成等高级能力时，建议使用完整方案 Cysharp.ObservableCollections。

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddAddedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-addaddedlistener-action-keyvaluepair-tkey-tvalue) | 添加键值监听者。回调参数为新增的键值对。 |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | 添加清空监听者。字典被清空且清空前非空时触发。 |
| [`AddRemovedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-addremovedlistener-action-keyvaluepair-tkey-tvalue) | 添加键值移除监听者。回调参数为被移除的键值对（含移除前的值）。 |
| [`AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>)`](#method-addupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue) | 添加值更新监听者。索引器为已存在的键赋新值且新旧值不同时触发，回调参数包含键、旧值与新值。 |
| [`RemoveAddedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-removeaddedlistener-action-keyvaluepair-tkey-tvalue) | 移除键值添加监听者。 |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | 移除清空监听者。 |
| [`RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-removeremovedlistener-action-keyvaluepair-tkey-tvalue) | 移除键值移除监听者。 |
| [`RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>)`](#method-removeupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue) | 移除值更新监听者。 |

</div>

### AddAddedListener(Action<KeyValuePair<TKey, TValue>>) {#method-addaddedlistener-action-keyvaluepair-tkey-tvalue}

添加键值监听者。回调参数为新增的键值对。

``` csharp
public abstract AutoRemoveListenerHandle AddAddedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` | 键值对添加时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听，避免手动管理生命周期。 |

</div>

### AddClearedListener(Action) {#method-addclearedlistener-action}

添加清空监听者。字典被清空且清空前非空时触发。

``` csharp
public abstract AutoRemoveListenerHandle AddClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | 字典清空时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### AddRemovedListener(Action<KeyValuePair<TKey, TValue>>) {#method-addremovedlistener-action-keyvaluepair-tkey-tvalue}

添加键值移除监听者。回调参数为被移除的键值对（含移除前的值）。

``` csharp
public abstract AutoRemoveListenerHandle AddRemovedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` | 键值对移除时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>) {#method-addupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue}

添加值更新监听者。索引器为已存在的键赋新值且新旧值不同时触发，回调参数包含键、旧值与新值。

``` csharp
public abstract AutoRemoveListenerHandle AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<DictionaryUpdateEventArgs<TKey, TValue>>` | 值更新时调用的回调函数。 |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AutoRemoveListenerHandle` | 返回一个 AutoRemoveListenerHandle，释放后自动移除监听。 |

</div>

### RemoveAddedListener(Action<KeyValuePair<TKey, TValue>>) {#method-removeaddedlistener-action-keyvaluepair-tkey-tvalue}

移除键值添加监听者。

``` csharp
public abstract void RemoveAddedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` | 先前通过 AddAddedListener 注册的回调函数。 |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

移除清空监听者。

``` csharp
public abstract void RemoveClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | 先前通过 AddClearedListener 注册的回调函数。 |

</div>

### RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>>) {#method-removeremovedlistener-action-keyvaluepair-tkey-tvalue}

移除键值移除监听者。

``` csharp
public abstract void RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` | 先前通过 AddRemovedListener 注册的回调函数。 |

</div>

### RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>) {#method-removeupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue}

移除值更新监听者。

``` csharp
public abstract void RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action<DictionaryUpdateEventArgs<TKey, TValue>>` | 先前通过 AddUpdatedListener 注册的回调函数。 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
