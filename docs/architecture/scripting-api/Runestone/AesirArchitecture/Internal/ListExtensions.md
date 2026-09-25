---
title: ListExtensions
description: "Runestone.AesirArchitecture.Internal.ListExtensions 的 API 文档"
---

# `ListExtensions`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture.Internal`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `ListExtensions`

## 声明

``` csharp
[Extension]
internal static class ListExtensions
```

List{T} 的只读跨度批量操作降级实现。

**备注**

上游 Cysharp.ObservableCollections 在 Shims/Collections.cs 中通过 Unsafe.As 直接改写 List{T} 内部数组实现零拷贝批量插入（仅 .NET 8 有原生 AddRange(ReadOnlySpan<T>)）。 本项目不引入 System.Runtime.CompilerServices.Unsafe（Unity netstandard2.1 参考程序集不含该程序集）， 因此改为语义等价的降级实现：插入走"先物化再插入"，添加走逐项追加。

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
