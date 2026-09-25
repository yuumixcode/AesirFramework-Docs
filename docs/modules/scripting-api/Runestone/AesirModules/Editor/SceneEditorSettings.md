---
title: SceneEditorSettings
description: "Runestone.AesirModules.Editor.SceneEditorSettings 的 API 文档"
---

# `SceneEditorSettings`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules.Editor`
    - **程序集:** `Runestone.AesirModules.Editor`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.ScriptableObject` → `UnityEditor.ScriptableSingleton<SceneEditorSettings>` → `SceneEditorSettings`

## 声明

``` csharp
[FilePath]
public class SceneEditorSettings : UnityEditor.ScriptableSingleton<SceneEditorSettings>
```

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SceneEditorSettings()`](#constructor-sceneeditorsettings) | — |

</div>

### SceneEditorSettings() {#constructor-sceneeditorsettings}

``` csharp
public SceneEditorSettings()
```

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`FirstLoadBootstrapScene`](#property-firstloadbootstrapscene) | — |
| [`SetupBootstrapper`](#property-setupbootstrapper) | — |
| [`BootstrapperScenePath`](#property-bootstrapperscenepath) | — |
| [`PreviousScenePath`](#property-previousscenepath) | — |

</div>

**继承的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `hideFlags` | — | `Object` |
| `name` | — | `Object` |

</div>

### FirstLoadBootstrapScene {#property-firstloadbootstrapscene}

``` csharp
[LabelWidth]
[LabelText]
[ShowInInspector]
public bool FirstLoadBootstrapScene { get; set; }
```

### SetupBootstrapper {#property-setupbootstrapper}

``` csharp
[LabelWidth]
[LabelText]
[ShowInInspector]
public bool SetupBootstrapper { get; set; }
```

### BootstrapperScenePath {#property-bootstrapperscenepath}

``` csharp
[PropertyOrder]
[ReadOnly]
[ShowInInspector]
public string BootstrapperScenePath { get; set; }
```

### PreviousScenePath {#property-previousscenepath}

``` csharp
[PropertyOrder]
[ReadOnly]
[ShowInInspector]
public string PreviousScenePath { get; set; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ManualSetupBootstrapper()`](#method-manualsetupbootstrapper) | — |

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
| `Save(bool)` | — | `ScriptableSingleton<SceneEditorSettings>` |
| `SetDirty()` | — | `ScriptableObject` |

</div>

### ManualSetupBootstrapper() {#method-manualsetupbootstrapper}

``` csharp
[Button]
public void ManualSetupBootstrapper()
```

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
