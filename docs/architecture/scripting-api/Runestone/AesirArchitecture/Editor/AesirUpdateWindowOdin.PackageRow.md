---
title: AesirUpdateWindowOdin.PackageRow
description: "Runestone.AesirArchitecture.Editor.AesirUpdateWindowOdin.PackageRow 的 API 文档"
---

# `AesirUpdateWindowOdin.PackageRow`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor.OdinInspector`

**继承链:** `System.Object` → `AesirUpdateWindowOdin.PackageRow`

## 声明

``` csharp
[Serializable]
public sealed class AesirUpdateWindowOdin.PackageRow
```

单个本地安装包的行视图模型。显示文本 / 颜色 / 可更新标记在 RebuildRows 时一次性算好，绘制期只读。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirUpdateWindowOdin.PackageRow()`](#constructor-aesirupdatewindowodin-packagerow) | — |

</div>

### AesirUpdateWindowOdin.PackageRow() {#constructor-aesirupdatewindowodin-packagerow}

``` csharp
public AesirUpdateWindowOdin.PackageRow()
```

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Model`](#field-model) | 对应的本地安装包数据。 |
| [`StatusColor`](#field-statuscolor) | 状态文本着色。 |
| [`Outdated`](#field-outdated) | 本地版本落后于远程版本。 |
| [`Local`](#field-local) | — |
| [`Name`](#field-name) | — |
| [`Remote`](#field-remote) | — |
| [`RemoteVersion`](#field-remoteversion) | 检测到的远程版本（仅待更新时有值）。 |
| [`UpdateHint`](#field-updatehint) | 待更新提示文本（不提供单包更新按钮——统一走「全部更新」，防版本撕裂）。 |

</div>

### Model {#field-model}

对应的本地安装包数据。

``` csharp
[HideInInspector]
public AesirUpdateService.InstalledPackage Model;
```

### StatusColor {#field-statuscolor}

状态文本着色。

``` csharp
[HideInInspector]
public Color StatusColor;
```

### Outdated {#field-outdated}

本地版本落后于远程版本。

``` csharp
[HideInInspector]
public bool Outdated;
```

### Local {#field-local}

``` csharp
[HorizontalGroup]
[DisplayAsString]
[HideLabel]
public string Local;
```

### Name {#field-name}

``` csharp
[HorizontalGroup]
[DisplayAsString]
[HideLabel]
public string Name;
```

### Remote {#field-remote}

``` csharp
[HorizontalGroup]
[DisplayAsString]
[HideLabel]
[GUIColor]
public string Remote;
```

### RemoteVersion {#field-remoteversion}

检测到的远程版本（仅待更新时有值）。

``` csharp
[HideInInspector]
public string RemoteVersion;
```

### UpdateHint {#field-updatehint}

待更新提示文本（不提供单包更新按钮——统一走「全部更新」，防版本撕裂）。

``` csharp
[HorizontalGroup]
[DisplayAsString]
[HideLabel]
[ShowIf]
public string UpdateHint;
```

## 方法

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

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
