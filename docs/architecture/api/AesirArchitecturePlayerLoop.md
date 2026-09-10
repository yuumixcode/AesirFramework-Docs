---
title: AesirArchitecturePlayerLoop
description: "Runestone.AesirArchitecture.AesirArchitecturePlayerLoop 的 API 文档"
---

# `AesirArchitecturePlayerLoop`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AesirArchitecturePlayerLoop`

## 声明

``` csharp
public static class AesirArchitecturePlayerLoop
```

基于 PlayerLoop 的生命周期钩子系统，无需 MonoBehaviour 即可接入游戏级帧回调。
通过 Register 注册回调，order 越小越先执行；系统自动在域加载时注入 PlayerLoop。

注入自愈：PlayerLoop 注入可能被第三方 SDK 用其缓存的副本调用 PlayerLoop.SetPlayerLoop 覆盖， 导致钩子静默失效。框架通过 EnsureInjected 自愈：域加载时、每次 Register 时、 以及 MonoLifecycleProxy 运行期间周期性检测并补插缺失的注入点；用户也可手动调用。

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GetHookCount(AesirArchitectureLifecyclePhase)`](#method-gethookcount-aesirarchitecturelifecyclephase) | 获取指定阶段的已注册回调数量 |
| [`EnsureInjected()`](#method-ensureinjected) | 确保两个注入点存在于当前 PlayerLoop。已存在时为空操作，缺失时重新注入。 |
| [`Register(AesirArchitectureLifecyclePhase, Action, int)`](#method-register-aesirarchitecturelifecyclephase-action-int) | 注册回调，order 越小越先执行，默认 0。 回调持有者销毁前必须调用 Unregister 注销；若未注销，回调将永久残留并阻止目标对象被回收。 |
| [`Reset()`](#method-reset) | 清空所有回调 |
| [`Unregister(AesirArchitectureLifecyclePhase, Action)`](#method-unregister-aesirarchitecturelifecyclephase-action) | 注销回调。 必须传入注册时的同一委托实例，匿名函数无法通过此方法注销。 |

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

### GetHookCount(AesirArchitectureLifecyclePhase) {#method-gethookcount-aesirarchitecturelifecyclephase}

获取指定阶段的已注册回调数量

``` csharp
public static int GetHookCount(AesirArchitectureLifecyclePhase phase)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 |
| :--- |
| `int` |

</div>

### EnsureInjected() {#method-ensureinjected}

确保两个注入点存在于当前 PlayerLoop。已存在时为空操作，缺失时重新注入。

``` csharp
public static void EnsureInjected()
```
### Register(AesirArchitectureLifecyclePhase, Action, int) {#method-register-aesirarchitecturelifecyclephase-action-int}

注册回调，order 越小越先执行，默认 0。
回调持有者销毁前必须调用 Unregister 注销；若未注销，回调将永久残留并阻止目标对象被回收。

``` csharp
public static void Register(AesirArchitectureLifecyclePhase phase, Action callback, int order = 0)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` |
| `callback` | `Action` |
| `order` | `int` |

</div>

### Reset() {#method-reset}

清空所有回调

``` csharp
public static void Reset()
```
### Unregister(AesirArchitectureLifecyclePhase, Action) {#method-unregister-aesirarchitecturelifecyclephase-action}

注销回调。
必须传入注册时的同一委托实例，匿名函数无法通过此方法注销。

``` csharp
public static void Unregister(AesirArchitectureLifecyclePhase phase, Action callback)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `phase` | `AesirArchitectureLifecyclePhase` |
| `callback` | `Action` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
