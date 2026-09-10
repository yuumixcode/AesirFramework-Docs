---
title: AesirArchitectureDebug
description: "Runestone.AesirArchitecture.AesirArchitectureDebug 的 API 文档"
---

# `AesirArchitectureDebug`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `AesirArchitectureDebug`

## 声明

``` csharp
public static class AesirArchitectureDebug
```

AesirArchitecture 内部日志工具。
所有架构模块的日志输出应走此工具，以醒目的颜色和 [AesirArchitecture] 标识区分来源。 Log/Warning 通过 [Conditional] 在打包时自动剔除；Error 始终保留。

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ErrorTag`](#field-errortag) | Error 级别的富文本标签，供异常消息复用以保持控制台输出风格一致。 |

</div>

### ErrorTag {#field-errortag}

Error 级别的富文本标签，供异常消息复用以保持控制台输出风格一致。

``` csharp
public const string ErrorTag = "<color=#FF4444><b>[AesirArchitecture]</b></color>";
```
## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`Log(object, string)`](#method-log-object-string) | 输出 Log 级别消息，附带来源标识 |
| [`Log(string)`](#method-log-string) | 输出 Log 级别消息 |
| [`LogError(object, string)`](#method-logerror-object-string) | 输出 Error 级别消息，附带来源标识 |
| [`LogError(string)`](#method-logerror-string) | 输出 Error 级别消息 |
| [`LogTestInfo(object, string)`](#method-logtestinfo-object-string) | 输出单元测试日志消息，附带来源标识 |
| [`LogTestInfo(string)`](#method-logtestinfo-string) | 输出单元测试日志消息。 仅在定义了 UNITY_INCLUDE_TESTS 的程序集中生效，非测试构建自动剔除调用。 |
| [`LogWarning(object, string)`](#method-logwarning-object-string) | 输出 Warning 级别消息，附带来源标识 |
| [`LogWarning(string)`](#method-logwarning-string) | 输出 Warning 级别消息 |

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

### Log(object, string) {#method-log-object-string}

输出 Log 级别消息，附带来源标识

``` csharp
[Conditional]
public static void Log(object source, string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `source` | `object` |
| `message` | `string` |

</div>

### Log(string) {#method-log-string}

输出 Log 级别消息

``` csharp
[Conditional]
public static void Log(string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `message` | `string` |

</div>

### LogError(object, string) {#method-logerror-object-string}

输出 Error 级别消息，附带来源标识

``` csharp
public static void LogError(object source, string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `source` | `object` |
| `message` | `string` |

</div>

### LogError(string) {#method-logerror-string}

输出 Error 级别消息

``` csharp
public static void LogError(string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `message` | `string` |

</div>

### LogTestInfo(object, string) {#method-logtestinfo-object-string}

输出单元测试日志消息，附带来源标识

``` csharp
[Conditional]
public static void LogTestInfo(object source, string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `source` | `object` |
| `message` | `string` |

</div>

### LogTestInfo(string) {#method-logtestinfo-string}

输出单元测试日志消息。
仅在定义了 UNITY_INCLUDE_TESTS 的程序集中生效，非测试构建自动剔除调用。

``` csharp
[Conditional]
public static void LogTestInfo(string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `message` | `string` |

</div>

### LogWarning(object, string) {#method-logwarning-object-string}

输出 Warning 级别消息，附带来源标识

``` csharp
[Conditional]
public static void LogWarning(object source, string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `source` | `object` |
| `message` | `string` |

</div>

### LogWarning(string) {#method-logwarning-string}

输出 Warning 级别消息

``` csharp
[Conditional]
public static void LogWarning(string message)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `message` | `string` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
