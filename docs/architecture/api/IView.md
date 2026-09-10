---
title: IView
description: "Runestone.AesirArchitecture.IView 的 API 文档"
---

# `IView`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `Runestone.AesirArchitecture.IContextHolder`，`Runestone.AesirArchitecture.ICanGetModel`，`Runestone.AesirArchitecture.ICanGetService`

## 声明

``` csharp
public interface IView : Runestone.AesirArchitecture.IContextHolder, 
Runestone.AesirArchitecture.ICanGetModel, 
Runestone.AesirArchitecture.ICanGetService
```

表现层接口。View 层通过此接口与模块上下文交互。
能力：GetModel, GetService

View 可读取 Model 和 Service，但不能执行 Command 或修改 Model 状态。

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
