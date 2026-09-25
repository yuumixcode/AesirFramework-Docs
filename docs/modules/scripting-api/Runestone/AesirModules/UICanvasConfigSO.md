---
title: UICanvasConfigSO
description: "Runestone.AesirModules.UICanvasConfigSO 的 API 文档"
---

# `UICanvasConfigSO`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.ScriptableObject` → `Sirenix.OdinInspector.SerializedScriptableObject` → `Runestone.AesirArchitecture.AesirScriptableObject` → `UICanvasConfigSO`

**实现接口:** `UnityEngine.ISerializationCallbackReceiver`

## 声明

``` csharp
public class UICanvasConfigSO : Runestone.AesirArchitecture.AesirScriptableObject, 
UnityEngine.ISerializationCallbackReceiver
```

UI Canvas 配置资产。创建路径：Assets → Create → Aesir Modules → UI → Default UICanvasConfig。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`UICanvasConfigSO()`](#constructor-uicanvasconfigso) | — |

</div>

### UICanvasConfigSO() {#constructor-uicanvasconfigso}

``` csharp
public UICanvasConfigSO()
```

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `hideFlags` | — | `Object` |
| `name` | — | `Object` |

</div>

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ApplyToCanvas(Canvas)`](#method-applytocanvas-canvas) | 将本资产的所有配置统一应用到目标 Canvas 及其关联的 CanvasScaler 和 GraphicRaycaster。 |
| [`CreateDefault()`](#method-createdefault) | — |

</div>

**继承的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `GetInstanceID()` | — | `Object` |
| `Equals(object)` | — | `Object` |
| `GetHashCode()` | — | `Object` |
| `ToString()` | — | `Object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |
| `OnAfterDeserialize()` | — | `SerializedScriptableObject` |
| `OnBeforeSerialize()` | — | `SerializedScriptableObject` |
| `SetDirty()` | — | `ScriptableObject` |

</div>

### ApplyToCanvas(Canvas) {#method-applytocanvas-canvas}

将本资产的所有配置统一应用到目标 Canvas 及其关联的 CanvasScaler 和 GraphicRaycaster。

``` csharp
public void ApplyToCanvas(Canvas canvas)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `canvas` | `Canvas` | 目标 Canvas。 |

</div>

### CreateDefault() {#method-createdefault}

``` csharp
public static UICanvasConfigSO CreateDefault()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `UICanvasConfigSO` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
