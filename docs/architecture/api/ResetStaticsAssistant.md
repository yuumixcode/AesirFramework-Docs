---
title: ResetStaticsAssistant
description: "Runestone.AesirArchitecture.ResetStaticsAssistant 的 API 文档"
---

# `ResetStaticsAssistant`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ResetStaticsAssistant`

## 声明

``` csharp
public static class ResetStaticsAssistant
```

静态变量重置助手（仅泛型类使用）。用于运行时阶段自动重置泛型类中的静态变量，兼容 Disable Domain Reload。 关闭 Domain Reload 时静态回调列表不会重置，所以每次启动时均可调用重置方法。

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Register(Action)`](#method-register-action) | 注册静态变量重置回调，在 Domain Reload 时自动调用 |
| [`ResetForTests()`](#method-resetfortests) | 手动执行所有已注册的静态变量重置回调。仅供单元测试隔离静态单例状态使用。 |

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

### Register(Action) {#method-register-action}

注册静态变量重置回调，在 Domain Reload 时自动调用

``` csharp
public static void Register(Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `callback` | `Action` |

</div>

### ResetForTests() {#method-resetfortests}

手动执行所有已注册的静态变量重置回调。仅供单元测试隔离静态单例状态使用。

``` csharp
[Conditional]
public static void ResetForTests()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
