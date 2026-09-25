---
title: AesirScheduler
description: "Runestone.AesirArchitecture.AesirScheduler 的 API 文档"
---

# `AesirScheduler`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AesirScheduler`

## 声明

``` csharp
public static class AesirScheduler
```

帧粒度时间调度器 —— 纯 C# 静态 API，为无协程能力的 Model / Service / Command 提供合法的延时执行手段。

**备注**

任务经 AesirArchitecturePlayerLoop 的 BeforeUpdate 钩子结算（早于当帧全部 MonoBehaviour.Update），无需任何场景物体存在。首次使用时自动注册钩子（注册即自愈）。

有意收窄的能力边界： 帧粒度——计时按帧结算，Delay(0.05f) 在 60fps 下约 3-4 帧后触发； 所有任务最早下一帧执行（含 Delay(0)，不做同帧投递）。 游戏时间——计时基于 time，受 timeScale 影响 （timeScale = 0 期间暂停计时，随游戏时间推进）。 一次性任务——无句柄、无取消、无暂停、不池化；高频反复调度请评估直接持有句柄型事件。 仅主线程——框架铁律；从异步回调访问请先调度回主线程。

语义要点：回调内再调度的新任务从下一帧开始参与结算（不参与当趟）； 回调不应抛异常（框架约定 fail-fast）——抛出时异常向上传播由 PlayerLoop 捕获记日志， 本趟后续任务跳过且不补投递（已出队任务不会重试）； seconds 为 NaN 时不设防（任务永不触发，极简原则，误用自行排查）。

稳态零分配：任务列表与结算缓冲复用（仅列表扩容时分配）；空队列时钩子零成本直接返回。

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`PendingCount`](#property-pendingcount) | 当前待结算任务数量（含未到期），供调试与测试观察队列状态。 |

</div>

### PendingCount {#property-pendingcount}

当前待结算任务数量（含未到期），供调试与测试观察队列状态。

``` csharp
public static int PendingCount { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Delay(float, Action)`](#method-delay-float-action) | 延时执行一次指定回调（帧粒度，最早下一帧）。 |
| [`NextFrame(Action)`](#method-nextframe-action) | 下一帧执行一次指定回调。 |

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

### Delay(float, Action) {#method-delay-float-action}

延时执行一次指定回调（帧粒度，最早下一帧）。

**备注**

任务一次性且不可取消；重复调用各自独立入队。首次调用自动注册 PlayerLoop 钩子。

``` csharp
public static void Delay(float seconds, Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `seconds` | `float` | 延时秒数（time 域）；负值按 0 处理（下一帧触发） |
| `callback` | `Action` | 到期时执行的回调 |

</div>

### NextFrame(Action) {#method-nextframe-action}

下一帧执行一次指定回调。

**备注**

语义等价 Delay(float, Action) 传 0——帧粒度下"最早下一帧"即最短延时。

``` csharp
public static void NextFrame(Action callback)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `callback` | `Action` | 下一帧 BeforeUpdate 阶段执行的回调 |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
