---
title: AesirScheduler.ScheduledTask
description: "Runestone.AesirArchitecture.AesirScheduler.ScheduledTask 的 API 文档"
---

# `AesirScheduler.ScheduledTask`

!!! note ""

    - **种类:** `struct`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `AesirScheduler.ScheduledTask`

## 声明

``` csharp
private struct AesirScheduler.ScheduledTask : System.ValueType
```

待结算任务

**备注**

结构体存储：列表本身零分配承载任务（无每任务堆分配），DueTime 为 time 域上的绝对到期时刻。

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Callback`](#field-callback) | — |
| [`DueTime`](#field-duetime) | — |
| [`BornFrame`](#field-bornframe) | — |

</div>

### Callback {#field-callback}

``` csharp
public Action Callback;
```

### DueTime {#field-duetime}

``` csharp
public float DueTime;
```

### BornFrame {#field-bornframe}

``` csharp
public int BornFrame;
```

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
