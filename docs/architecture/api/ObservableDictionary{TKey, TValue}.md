---
title: ObservableDictionary<TKey, TValue>
description: "Runestone.AesirArchitecture.ObservableDictionary<TKey, TValue> 的 API 文档"
---

# `ObservableDictionary<TKey, TValue>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ObservableDictionary<TKey, TValue>`

**实现接口:** `System.Collections.Generic.IReadOnlyDictionary<TKey, TValue>`，`Runestone.AesirArchitecture.IReadOnlyObservableDictionary<TKey, TValue>`，`System.Collections.Generic.IDictionary<TKey, TValue>`，`System.Collections.Generic.IEnumerable<KeyValuePair<TKey, TValue>>`，`System.Collections.IEnumerable`，`Runestone.AesirArchitecture.IObservableDictionary<TKey, TValue>`，`System.Collections.Generic.ICollection<KeyValuePair<TKey, TValue>>`，`System.Collections.Generic.IReadOnlyCollection<KeyValuePair<TKey, TValue>>`

## 声明

``` csharp
[DefaultMember]
[Serializable]
public sealed class ObservableDictionary<TKey, TValue> : System.Collections.Generic.IReadOnlyDictionary<TKey, TValue>, 
Runestone.AesirArchitecture.IReadOnlyObservableDictionary<TKey, TValue>, 
System.Collections.Generic.IDictionary<TKey, TValue>, 
System.Collections.Generic.IEnumerable<KeyValuePair<TKey, TValue>>, 
System.Collections.IEnumerable, 
Runestone.AesirArchitecture.IObservableDictionary<TKey, TValue>, 
System.Collections.Generic.ICollection<KeyValuePair<TKey, TValue>>, 
System.Collections.Generic.IReadOnlyCollection<KeyValuePair<TKey, TValue>>  
```

可观察字典实现。
Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ObservableDictionary()`](#constructor-observabledictionary) | 默认构造，创建空字典。 |
| [`ObservableDictionary(IEnumerable<KeyValuePair<TKey, TValue>>)`](#constructor-observabledictionary-ienumerable-keyvaluepair-tkey-tvalue) | 指定初始键值构造。初始键值不触发 Added 事件（语义同反序列化填充）。 |
| [`ObservableDictionary(int)`](#constructor-observabledictionary-int) | 指定初始键值构造。初始键值不触发 Added 事件（语义同反序列化填充）。 |

</div>

### ObservableDictionary() {#constructor-observabledictionary}

默认构造，创建空字典。

``` csharp
public ObservableDictionary<TKey, TValue>()
```
### ObservableDictionary(IEnumerable<KeyValuePair<TKey, TValue>>) {#constructor-observabledictionary-ienumerable-keyvaluepair-tkey-tvalue}

指定初始键值构造。初始键值不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableDictionary<TKey, TValue>(IEnumerable<KeyValuePair<TKey, TValue>> initialItems)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `initialItems` | `IEnumerable<KeyValuePair<TKey, TValue>>` |

</div>

### ObservableDictionary(int) {#constructor-observabledictionary-int}

指定初始键值构造。初始键值不触发 Added 事件（语义同反序列化填充）。

``` csharp
public ObservableDictionary<TKey, TValue>(int capacity)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `capacity` | `int` |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Keys`](#property-keys) | 所有键的集合。 |
| [`Values`](#property-values) | 所有值的集合。 |
| [`Item`](#property-item) | 读写指定键的值。 读取：键不存在时抛 KeyNotFoundException（fail-fast）。  写入：键不存在时添加并触发 Added；键已存在且新值不同时更新并触发 Updated（参数含旧值）；值相同则跳过。 |
| [`IsReadOnly`](#property-isreadonly) | 固定返回 false，该集合可写。 |
| [`Count`](#property-count) | 键值对数量。 |

</div>

### Keys {#property-keys}

所有键的集合。

``` csharp
public IEnumerable<TKey> Keys { get; }
```
### Values {#property-values}

所有值的集合。

``` csharp
public IEnumerable<TValue> Values { get; }
```
### Item {#property-item}

读写指定键的值。
读取：键不存在时抛 KeyNotFoundException（fail-fast）。

``` csharp
public TValue Item { get; set; }
```
写入：键不存在时添加并触发 Added；键已存在且新值不同时更新并触发 Updated（参数含旧值）；值相同则跳过。

### IsReadOnly {#property-isreadonly}

固定返回 false，该集合可写。

``` csharp
public bool IsReadOnly { get; }
```
### Count {#property-count}

键值对数量。

``` csharp
public int Count { get; }
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddAddedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-addaddedlistener-action-keyvaluepair-tkey-tvalue) | — |
| [`AddClearedListener(Action)`](#method-addclearedlistener-action) | — |
| [`AddRemovedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-addremovedlistener-action-keyvaluepair-tkey-tvalue) | — |
| [`AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>)`](#method-addupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue) | — |
| [`GetEnumerator()`](#method-getenumerator) | 返回遍历键值对的结构体枚举器，foreach 具体类型时零分配。 |
| [`Contains(KeyValuePair<TKey, TValue>)`](#method-contains-keyvaluepair-tkey-tvalue) | 判断是否包含指定键值对（键存在且值相等）。 |
| [`ContainsKey(TKey)`](#method-containskey-tkey) | 判断是否包含指定键。 |
| [`Remove(KeyValuePair<TKey, TValue>)`](#method-remove-keyvaluepair-tkey-tvalue) | 移除与指定键值对匹配的项（键存在且值相等），成功时触发 Removed 事件。 |
| [`Remove(TKey)`](#method-remove-tkey) | 移除指定键的键值对，成功时触发 Removed 事件（参数含被移除的值）。 |
| [`TryGetValue(TKey, ref TValue)`](#method-trygetvalue-tkey-ref-tvalue) | 获取与指定键关联的值。 |
| [`Add(KeyValuePair<TKey, TValue>)`](#method-add-keyvaluepair-tkey-tvalue) | 添加键值对，触发 Added 事件。键已存在时抛 ArgumentException（fail-fast）。 |
| [`Add(TKey, TValue)`](#method-add-tkey-tvalue) | 添加键值对，触发 Added 事件。键已存在时抛 ArgumentException（fail-fast）。 |
| [`Clear()`](#method-clear) | 清空字典。字典非空时触发 Cleared 事件；已为空时不触发。 |
| [`ClearListeners()`](#method-clearlisteners) | 清空所有事件监听。 |
| [`CopyTo(KeyValuePair<TKey, TValue>[], int)`](#method-copyto-keyvaluepair-tkey-tvalue-int) | 从指定数组索引开始复制键值对到目标数组。 |
| [`RemoveAddedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-removeaddedlistener-action-keyvaluepair-tkey-tvalue) | — |
| [`RemoveClearedListener(Action)`](#method-removeclearedlistener-action) | — |
| [`RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>>)`](#method-removeremovedlistener-action-keyvaluepair-tkey-tvalue) | — |
| [`RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>)`](#method-removeupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue) | — |

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

### AddAddedListener(Action<KeyValuePair<TKey, TValue>>) {#method-addaddedlistener-action-keyvaluepair-tkey-tvalue}

``` csharp
public AutoRemoveListenerHandle AddAddedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddClearedListener(Action) {#method-addclearedlistener-action}

``` csharp
public AutoRemoveListenerHandle AddClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddRemovedListener(Action<KeyValuePair<TKey, TValue>>) {#method-addremovedlistener-action-keyvaluepair-tkey-tvalue}

``` csharp
public AutoRemoveListenerHandle AddRemovedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>) {#method-addupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue}

``` csharp
public AutoRemoveListenerHandle AddUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<DictionaryUpdateEventArgs<TKey, TValue>>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `AutoRemoveListenerHandle` |

</div>

### GetEnumerator() {#method-getenumerator}

返回遍历键值对的结构体枚举器，foreach 具体类型时零分配。

``` csharp
public ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue> GetEnumerator()
```
**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>` |

</div>

### Contains(KeyValuePair<TKey, TValue>) {#method-contains-keyvaluepair-tkey-tvalue}

判断是否包含指定键值对（键存在且值相等）。

``` csharp
public bool Contains(KeyValuePair<TKey, TValue> item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `item` | `KeyValuePair<TKey, TValue>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### ContainsKey(TKey) {#method-containskey-tkey}

判断是否包含指定键。

``` csharp
public bool ContainsKey(TKey key)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `key` | `TKey` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Remove(KeyValuePair<TKey, TValue>) {#method-remove-keyvaluepair-tkey-tvalue}

移除与指定键值对匹配的项（键存在且值相等），成功时触发 Removed 事件。

``` csharp
public bool Remove(KeyValuePair<TKey, TValue> item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `item` | `KeyValuePair<TKey, TValue>` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Remove(TKey) {#method-remove-tkey}

移除指定键的键值对，成功时触发 Removed 事件（参数含被移除的值）。

``` csharp
public bool Remove(TKey key)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `key` | `TKey` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### TryGetValue(TKey, ref TValue) {#method-trygetvalue-tkey-ref-tvalue}

获取与指定键关联的值。

``` csharp
public bool TryGetValue(TKey key, out ref TValue value)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `key` | `TKey` |
| `value` | `ref TValue` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `bool` |

</div>

### Add(KeyValuePair<TKey, TValue>) {#method-add-keyvaluepair-tkey-tvalue}

添加键值对，触发 Added 事件。键已存在时抛 ArgumentException（fail-fast）。

``` csharp
public void Add(KeyValuePair<TKey, TValue> item)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `item` | `KeyValuePair<TKey, TValue>` |

</div>

### Add(TKey, TValue) {#method-add-tkey-tvalue}

添加键值对，触发 Added 事件。键已存在时抛 ArgumentException（fail-fast）。

``` csharp
public void Add(TKey key, TValue value)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `key` | `TKey` |
| `value` | `TValue` |

</div>

### Clear() {#method-clear}

清空字典。字典非空时触发 Cleared 事件；已为空时不触发。

``` csharp
public void Clear()
```
### ClearListeners() {#method-clearlisteners}

清空所有事件监听。

``` csharp
public void ClearListeners()
```
### CopyTo(KeyValuePair<TKey, TValue>[], int) {#method-copyto-keyvaluepair-tkey-tvalue-int}

从指定数组索引开始复制键值对到目标数组。

``` csharp
public void CopyTo(KeyValuePair<TKey, TValue>[] array, int arrayIndex)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `array` | `KeyValuePair<TKey, TValue>[]` |
| `arrayIndex` | `int` |

</div>

### RemoveAddedListener(Action<KeyValuePair<TKey, TValue>>) {#method-removeaddedlistener-action-keyvaluepair-tkey-tvalue}

``` csharp
public void RemoveAddedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` |

</div>

### RemoveClearedListener(Action) {#method-removeclearedlistener-action}

``` csharp
public void RemoveClearedListener(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

### RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>>) {#method-removeremovedlistener-action-keyvaluepair-tkey-tvalue}

``` csharp
public void RemoveRemovedListener(Action<KeyValuePair<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<KeyValuePair<TKey, TValue>>` |

</div>

### RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>>) {#method-removeupdatedlistener-action-dictionaryupdateeventargs-tkey-tvalue}

``` csharp
public void RemoveUpdatedListener(Action<DictionaryUpdateEventArgs<TKey, TValue>> callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action<DictionaryUpdateEventArgs<TKey, TValue>>` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
