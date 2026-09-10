---
title: ICanInitialize
description: "Runestone.AesirArchitecture.ICanInitialize 的 API 文档"
---

# `ICanInitialize`

!!! note ""

    - **种类:** `interface`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**实现接口:** `System.IDisposable`

## 声明

``` csharp
public interface ICanInitialize : System.IDisposable
```

可初始化接口。提供初始化与初始化状态标记。
被 IModel 和 IService 继承。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Initialized`](#property-initialized) | — |

</div>

### Initialized {#property-initialized}

``` csharp
public bool Initialized { get; }
```

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Initialize()`](#method-initialize) | 初始化 |

</div>

### Initialize() {#method-initialize}

初始化

``` csharp
public abstract void Initialize()
```
## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
