---
title: IPresenter<T>
description: "Runestone.AesirArchitecture.IPresenter<T> 的 API 文档"
---

# `IPresenter<T>`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `Runestone.AesirArchitecture.IContextHolder`，`Runestone.AesirArchitecture.ICanGetModel`，`Runestone.AesirArchitecture.ICanGetService`，`Runestone.AesirArchitecture.ICanExecuteCommand`，`Runestone.AesirArchitecture.ICanExecuteQuery`，`Runestone.AesirArchitecture.IPresenter`，`System.IDisposable`

## 声明

``` csharp
public interface IPresenter<T> : Runestone.AesirArchitecture.IContextHolder, 
Runestone.AesirArchitecture.ICanGetModel, 
Runestone.AesirArchitecture.ICanGetService, 
Runestone.AesirArchitecture.ICanExecuteCommand, 
Runestone.AesirArchitecture.ICanExecuteQuery, 
Runestone.AesirArchitecture.IPresenter, 
System.IDisposable where T : new(), Runestone.AesirArchitecture.AbstractContext<T>
```

泛型 MVP 中介接口。绑定指定上下文类型，实现者自动获得 Context 绑定。

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
