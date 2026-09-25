---
title: AesirDependencyInstaller
description: "Runestone.AesirModules.Editor.Bootstrap.AesirDependencyInstaller 的 API 文档"
---

# `AesirDependencyInstaller`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirModules.Editor.Bootstrap`
    - **程序集:** `Runestone.AesirModules.Editor.Bootstrap`

**继承链:** `System.Object` → `AesirDependencyInstaller`

## 声明

``` csharp
internal static class AesirDependencyInstaller
```

Aesir Modules 依赖补全器 —— 检测 Aesir Architecture (RAA) 缺失并经 Git URL 引导安装。

**备注**

本类所在程序集必须零引用（不引用 RAM 核心、RAA、Odin）：Assets 形态安装本包时若 RAA 缺失，RAM 核心 / Editor 程序集因解析不到 Runestone.AesirArchitecture 全部不编译， 此时本菜单是唯一可用的 Aesir 工具入口，其编译不得依赖任何会失败的程序集。
UPM 形态安装无需本菜单：本包 package.json 的 dependencies 已声明 RAA 的 Git URL， Package Manager 安装时自动递归拉取依赖。

安装走 Add（Git URL），RAA 落在 Packages/ 下以 UPM 形态存在； RAM 核心 asmdef 按程序集名引用（非 GUID），UPM 形态的 RAA 同名程序集同样能解析， Assets + UPM 混合形态可正常编译。

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`MenuPath`](#field-menupath) | 菜单路径：Aesir Modules 包专属工具，归 Tools/Aesir/Modules/ 组。 |

</div>

### MenuPath {#field-menupath}

菜单路径：Aesir Modules 包专属工具，归 Tools/Aesir/Modules/ 组。

``` csharp
public const string MenuPath = "Tools/Aesir/Modules/Install Dependencies";
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
