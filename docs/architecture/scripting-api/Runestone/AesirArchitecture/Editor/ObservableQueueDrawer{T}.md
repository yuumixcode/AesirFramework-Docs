---
title: ObservableQueueDrawer<T>
description: "Runestone.AesirArchitecture.Editor.ObservableQueueDrawer<T> 的 API 文档"
---

# `ObservableQueueDrawer<T>`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor.OdinInspector`

**继承链:** `System.Object` → `Sirenix.OdinInspector.Editor.OdinDrawer` → `Sirenix.OdinInspector.Editor.OdinValueDrawer<ObservableQueue<T>>` → `ObservableQueueDrawer<T>`

## 声明

``` csharp
[DrawerPriority]
internal sealed class ObservableQueueDrawer<T> : Sirenix.OdinInspector.Editor.OdinValueDrawer<ObservableQueue<T>> 
```

可观察队列的内联调试面板。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ObservableQueueDrawer()`](#constructor-observablequeuedrawer) | — |

</div>

### ObservableQueueDrawer() {#constructor-observablequeuedrawer}

``` csharp
public ObservableQueueDrawer<T>()
```

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `ValueEntry` | — | `OdinValueDrawer<ObservableQueue<T>>` |
| `Property` | — | `OdinDrawer` |
| `Initialized` | — | `OdinDrawer` |
| `SkipWhenDrawing` | — | `OdinDrawer` |

</div>

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `CanDrawProperty(InspectorProperty)` | — | `OdinValueDrawer<ObservableQueue<T>>` |
| `CanDrawTypeFilter(Type)` | — | `OdinDrawer` |
| `Equals(object)` | — | `object` |
| `GetHashCode()` | — | `object` |
| `ToString()` | — | `object` |
| `DrawProperty(GUIContent)` | — | `OdinDrawer` |
| `Initialize(InspectorProperty)` | — | `OdinDrawer` |
| `CallNextDrawer(GUIContent)` | — | `OdinDrawer` |
| `MemberwiseClone()` | — | `object` |
| `DrawPropertyLayout(GUIContent)` | — | `ObservableQueueDrawer<T>` |
| `CanDrawValueProperty(InspectorProperty)` | — | `OdinValueDrawer<ObservableQueue<T>>` |
| `Finalize()` | — | `object` |
| `Initialize()` | — | `OdinDrawer` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
