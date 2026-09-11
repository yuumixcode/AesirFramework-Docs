---
title: EnsureAesirArchitectureDefine
description: "Runestone.AesirArchitecture.Editor.EnsureAesirArchitectureDefine 的 API 文档"
---

# `EnsureAesirArchitectureDefine`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor`

**继承链:** `System.Object` → `EnsureAesirArchitectureDefine`

## 声明

``` csharp
[InitializeOnLoad]
internal static class EnsureAesirArchitectureDefine
```

自动确保 AESIR_ARCHITECTURE 脚本宏定义符号存在。
通过 InitializeOnLoadAttribute 在编辑器加载时自动执行， 供 Aesir 系列其他插件通过 #if AESIR_ARCHITECTURE 检测本架构是否存在。

**备注**

[InitializeOnLoad] 特性使 Unity 在编辑器加载时自动调用此类的静态构造函数， 静态构造函数通过 EnsureScriptingDefineSymbol 方法 确保所有构建目标中都存在 AESIR_ARCHITECTURE 宏定义， 从而使依赖本架构的其他包可以通过条件编译指令在编译期检测架构是否可用。

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
