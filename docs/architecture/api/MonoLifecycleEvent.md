---
title: MonoLifecycleEvent
description: "Runestone.AesirArchitecture.MonoLifecycleEvent 的 API 文档"
---

# `MonoLifecycleEvent`

!!! note ""

    - **种类:** `enum`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `System.ValueType` → `System.Enum` → `MonoLifecycleEvent`

**实现接口:** `System.IFormattable`，`System.IComparable`，`System.IConvertible`

## 声明

``` csharp
public enum MonoLifecycleEvent : System.Enum, 
System.IFormattable, 
System.IComparable, 
System.IConvertible
```

Mono 生命周期事件类型，涵盖 Unity 原生生命周期回调和自定义 PlayerLoop 阶段。

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AfterUpdate`](#field-afterupdate) | 自定义 PlayerLoop 阶段：在 PostLateUpdate 之后执行 |
| [`BeforeUpdate`](#field-beforeupdate) | 自定义 PlayerLoop 阶段：在 Update 之前执行 |
| [`FixedUpdate`](#field-fixedupdate) | MonoBehaviour.FixedUpdate — 物理帧 |
| [`LateUpdate`](#field-lateupdate) | MonoBehaviour.LateUpdate — 每帧后处理 |
| [`OnApplicationFocus`](#field-onapplicationfocus) | MonoBehaviour.OnApplicationFocus — 应用获得或失去焦点 |
| [`OnApplicationPause`](#field-onapplicationpause) | MonoBehaviour.OnApplicationPause — 应用被系统暂停或恢复 |
| [`OnApplicationQuit`](#field-onapplicationquit) | MonoBehaviour.OnApplicationQuit — 应用退出 |
| [`Update`](#field-update) | MonoBehaviour.Update — 每帧逻辑更新 |

</div>

### AfterUpdate {#field-afterupdate}

自定义 PlayerLoop 阶段：在 PostLateUpdate 之后执行

``` csharp
public const MonoLifecycleEvent AfterUpdate;
```
### BeforeUpdate {#field-beforeupdate}

自定义 PlayerLoop 阶段：在 Update 之前执行

``` csharp
public const MonoLifecycleEvent BeforeUpdate;
```
### FixedUpdate {#field-fixedupdate}

MonoBehaviour.FixedUpdate — 物理帧

``` csharp
public const MonoLifecycleEvent FixedUpdate;
```
### LateUpdate {#field-lateupdate}

MonoBehaviour.LateUpdate — 每帧后处理

``` csharp
public const MonoLifecycleEvent LateUpdate;
```
### OnApplicationFocus {#field-onapplicationfocus}

MonoBehaviour.OnApplicationFocus — 应用获得或失去焦点

``` csharp
public const MonoLifecycleEvent OnApplicationFocus;
```
### OnApplicationPause {#field-onapplicationpause}

MonoBehaviour.OnApplicationPause — 应用被系统暂停或恢复

``` csharp
public const MonoLifecycleEvent OnApplicationPause;
```
### OnApplicationQuit {#field-onapplicationquit}

MonoBehaviour.OnApplicationQuit — 应用退出

``` csharp
public const MonoLifecycleEvent OnApplicationQuit;
```
### Update {#field-update}

MonoBehaviour.Update — 每帧逻辑更新

``` csharp
public const MonoLifecycleEvent Update;
```
## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `HasFlag(Enum)` | — | `Enum` |
| `Equals(object)` | — | `Enum` |
| `GetHashCode()` | — | `Enum` |
| `ToString()` | — | `Enum` |
| `ToString(string)` | — | `Enum` |
| `GetTypeCode()` | — | `Enum` |
| `CompareTo(object)` | — | `Enum` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |
| `ToString(IFormatProvider)` | — | `Enum` |
| `ToString(string, IFormatProvider)` | — | `Enum` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
