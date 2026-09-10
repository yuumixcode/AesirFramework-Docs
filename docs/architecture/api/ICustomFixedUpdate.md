---
title: ICustomFixedUpdate
description: "Runestone.AesirArchitecture.ICustomFixedUpdate 的 API 文档"
---

# `ICustomFixedUpdate`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

## 声明

``` csharp
public interface ICustomFixedUpdate
```

自定义生命周期接口集合。实现这些接口的类可通过 Register(object) 自动注册到对应的生命周期事件。

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`OnCustomFixedUpdate()`](#method-oncustomfixedupdate) | 在 FixedUpdate 阶段执行的自定义逻辑 |

</div>

### OnCustomFixedUpdate() {#method-oncustomfixedupdate}

在 FixedUpdate 阶段执行的自定义逻辑

``` csharp
public abstract void OnCustomFixedUpdate()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
