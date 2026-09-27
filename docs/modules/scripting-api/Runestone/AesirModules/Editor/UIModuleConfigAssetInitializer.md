---
title: UIModuleConfigAssetInitializer
description: "Runestone.AesirModules.Editor.UIModuleConfigAssetInitializer 的 API 文档"
---

# `UIModuleConfigAssetInitializer`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirModules.Editor`
    - **程序集:** `Runestone.AesirModules.Editor`

**继承链:** `System.Object` → `UIModuleConfigAssetInitializer`

## 声明

``` csharp
internal static class UIModuleConfigAssetInitializer
```

确保 UI 模块配置资产存在：编辑模式域加载后，Resources 兜底路径缺失且项目中无同类型资产时， 自动创建 UIModuleConfigSO 至 Assets/Resources/UIModuleConfig/， 免去用户手动创建资产的前置步骤（配置调整不依赖预放置 [UIModule]）。

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
