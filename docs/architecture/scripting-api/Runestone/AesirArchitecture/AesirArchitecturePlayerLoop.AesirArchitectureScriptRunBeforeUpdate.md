---
title: AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate
description: "Runestone.AesirArchitecture.AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate 的 API 文档"
---

# `AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate`

## 声明

``` csharp
private struct AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate : System.ValueType
```

PlayerLoop 子系统 type 标识，在 Update 之前执行

**备注**

此空结构体仅作为 PlayerLoopSystem.type 的类型标识使用， 让 PlayerLoopUtility.ContainsSystem<T> 能够检测自定义子系统是否已注入， 避免重复注入。不包含任何运行时逻辑。

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
