---
title: MemberData
description: "Runestone.AesirModules.ScriptDocGenerator.MemberData 的 API 文档"
---

# `MemberData`

!!! note ""

    - **种类:** `abstract class`
    - **命名空间:** `Runestone.AesirModules.ScriptDocGenerator`
    - **程序集:** `Runestone.AesirModules.OdinInspector`

**继承链:** `System.Object` → `MemberData`

**实现接口:** `Runestone.AesirModules.ScriptDocGenerator.IMemberData`

## 声明

``` csharp
[Serializable]
public abstract class MemberData : Runestone.AesirModules.ScriptDocGenerator.IMemberData
```

解析成员数据的基类

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`DefaultAttributeFilter`](#field-defaultattributefilter) | — |

</div>

### DefaultAttributeFilter {#field-defaultattributefilter}

``` csharp
public static readonly DefaultAttributeFilter DefaultAttributeFilter;
```

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`DeclaringType`](#property-declaringtype) | 声明此成员的类型 |
| [`ReflectedType`](#property-reflectedtype) | 通过反射获取该成员的类型 |
| [`IsFromInheritance`](#property-isfrominheritance) | 成员是否从继承中获取，这里的成员不包括 Type 类型 |
| [`IsObsolete`](#property-isobsolete) | 是否已过时 |
| [`AttributesDeclaration`](#property-attributesdeclaration) | 特性声明字符串 |
| [`DeclaringTypeFullName`](#property-declaringtypefullname) | 声明类型的完整名称，包括命名空间 |
| [`DeclaringTypeName`](#property-declaringtypename) | 声明类型的名称 |
| [`Name`](#property-name) | 成员名称 |
| [`ReflectedTypeFullName`](#property-reflectedtypefullname) | 通过反射获取该成员的类型的完整名称，包括命名空间 |
| [`ReflectedTypeName`](#property-reflectedtypename) | 通过反射获取该成员的类型名称 |
| [`RemarksSummary`](#property-remarkssummary) | 备注注释（XML <remarks> 标签）。无注释时为 null |
| [`SummaryAttributeValue`](#property-summaryattributevalue) | 注释 |
| [`RemarksResolver`](#property-remarksresolver) | 备注注释解析委托（XML <remarks> 标签）。 Editor 程序集在加载时注入源文件解析实现；默认无备注注释（返回 null）。 |
| [`SummaryResolver`](#property-summaryresolver) | Summary 解析委托。Editor 程序集在加载时注入源文件解析实现（基于 SourceScanner）， 从源代码的 XML /// <summary> 注释中读取成员摘要。 默认回退到 [Summary] 特性，保持向后兼容。 |
| [`ValueResolver`](#property-valueresolver) | 属性值注释解析委托（XML <value> 标签），由属性数据类消费。 Editor 程序集在加载时注入源文件解析实现；默认无注释（返回 null）。 |
| [`ParamSummariesResolver`](#property-paramsummariesresolver) | 参数级注释解析委托（XML <param> 标签），键为参数名，适用于方法与构造函数。 Editor 程序集在加载时注入源文件解析实现；默认无参数级注释（返回 null）。 |
| [`ReturnsSummaryResolver`](#property-returnssummaryresolver) | 返回值注释解析委托（XML <returns> 标签），适用于方法。 Editor 程序集在加载时注入源文件解析实现；默认无返回值注释（返回 null）。 |
| [`TypeParamsResolver`](#property-typeparamsresolver) | 泛型参数注释解析委托（XML <typeparam> 标签），键为参数名，由类型数据类消费。 Editor 程序集在加载时注入源文件解析实现；默认无注释（返回 null）。 |

</div>

### DeclaringType {#property-declaringtype}

声明此成员的类型

``` csharp
public Type DeclaringType { get; }
```

### ReflectedType {#property-reflectedtype}

通过反射获取该成员的类型

``` csharp
public Type ReflectedType { get; }
```

### IsFromInheritance {#property-isfrominheritance}

成员是否从继承中获取，这里的成员不包括 Type 类型

``` csharp
public bool IsFromInheritance { get; }
```

### IsObsolete {#property-isobsolete}

是否已过时

``` csharp
public bool IsObsolete { get; }
```

### AttributesDeclaration {#property-attributesdeclaration}

特性声明字符串

``` csharp
public string AttributesDeclaration { get; }
```

### DeclaringTypeFullName {#property-declaringtypefullname}

声明类型的完整名称，包括命名空间

``` csharp
public string DeclaringTypeFullName { get; }
```

### DeclaringTypeName {#property-declaringtypename}

声明类型的名称

``` csharp
public string DeclaringTypeName { get; }
```

### Name {#property-name}

成员名称

``` csharp
public string Name { get; }
```

### ReflectedTypeFullName {#property-reflectedtypefullname}

通过反射获取该成员的类型的完整名称，包括命名空间

``` csharp
public string ReflectedTypeFullName { get; }
```

### ReflectedTypeName {#property-reflectedtypename}

通过反射获取该成员的类型名称

``` csharp
public string ReflectedTypeName { get; }
```

### RemarksSummary {#property-remarkssummary}

备注注释（XML <remarks> 标签）。无注释时为 null

``` csharp
public string RemarksSummary { get; }
```

### SummaryAttributeValue {#property-summaryattributevalue}

注释

``` csharp
public string SummaryAttributeValue { get; }
```

### RemarksResolver {#property-remarksresolver}

备注注释解析委托（XML <remarks> 标签）。 Editor 程序集在加载时注入源文件解析实现；默认无备注注释（返回 null）。

``` csharp
public static Func<MemberInfo, string> RemarksResolver { get; set; }
```

### SummaryResolver {#property-summaryresolver}

Summary 解析委托。Editor 程序集在加载时注入源文件解析实现（基于 SourceScanner）， 从源代码的 XML /// <summary> 注释中读取成员摘要。 默认回退到 [Summary] 特性，保持向后兼容。

``` csharp
public static Func<MemberInfo, string> SummaryResolver { get; set; }
```

### ValueResolver {#property-valueresolver}

属性值注释解析委托（XML <value> 标签），由属性数据类消费。 Editor 程序集在加载时注入源文件解析实现；默认无注释（返回 null）。

``` csharp
public static Func<MemberInfo, string> ValueResolver { get; set; }
```

### ParamSummariesResolver {#property-paramsummariesresolver}

参数级注释解析委托（XML <param> 标签），键为参数名，适用于方法与构造函数。 Editor 程序集在加载时注入源文件解析实现；默认无参数级注释（返回 null）。

``` csharp
public static Func<MethodBase, IReadOnlyDictionary<string, string>> ParamSummariesResolver { get; set; }
```

### ReturnsSummaryResolver {#property-returnssummaryresolver}

返回值注释解析委托（XML <returns> 标签），适用于方法。 Editor 程序集在加载时注入源文件解析实现；默认无返回值注释（返回 null）。

``` csharp
public static Func<MethodInfo, string> ReturnsSummaryResolver { get; set; }
```

### TypeParamsResolver {#property-typeparamsresolver}

泛型参数注释解析委托（XML <typeparam> 标签），键为参数名，由类型数据类消费。 Editor 程序集在加载时注入源文件解析实现；默认无注释（返回 null）。

``` csharp
public static Func<Type, IReadOnlyDictionary<string, string>> TypeParamsResolver { get; set; }
```

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
