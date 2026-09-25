---
title: AesirGetStartedService
description: "Runestone.AesirArchitecture.Editor.AesirGetStartedService 的 API 文档"
---

# `AesirGetStartedService`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor`

**继承链:** `System.Object` → `AesirGetStartedService`

## 声明

``` csharp
public static class AesirGetStartedService
```

Aesir Getting Started 服务 — 两版 Getting Started 窗口（IMGUI 兜底 / Odin 版）共用的无状态数据层： 扫描本机安装的 Aesir 包、解析示例清单与场景资产、按教学分组归置示例，并提供跳转动作。
包发现覆盖三种安装形态（同名包按此优先级取一）：① 代码导入 InstallRootRelativePath（复制 / unitypackage，示例位于包内 Samples/）；② 嵌入式包（Packages/ 目录下的包源码）；③ UPM Git URL 安装 （包源在 PackageCacheRootPath）。后两种 UPM 形态的示例须经 Package Manager → Samples 导入到 Assets/Samples/<包显示名>/<版本>/<示例显示名>/， 未导入的条目仍保留在清单中（IsImported 为 false）， 由窗口引导用户去 Package Manager 导入。

示例元数据（显示名 / 描述 / 顺序 / 档位）以各包 package.json 的 samples 清单为唯一真源， 本类不做逐示例硬编码登记——新增示例只需更新 package.json，窗口自动跟进。

## 字段

**常量字段**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`PackageCacheRootPath`](#field-packagecacherootpath) | UPM Git URL 安装的包缓存根目录（项目相对路径，Unity 不导入）。 |
| [`PackageIdPrefix`](#field-packageidprefix) | Aesir 包的 package.json name 前缀（识别本框架包）。 |
| [`UpmSamplesRootPath`](#field-upmsamplesrootpath) | UPM 示例导入的落地根目录（Package Manager → Samples → Import 后的位置）。 |

</div>

**声明的字段**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`KnownPackages`](#field-knownpackages) | 已公开发布的 Aesir 包（顺序即概览卡片顺序）。 |

</div>

### PackageCacheRootPath {#field-packagecacherootpath}

UPM Git URL 安装的包缓存根目录（项目相对路径，Unity 不导入）。

``` csharp
public const string PackageCacheRootPath = "Library/PackageCache";
```

### PackageIdPrefix {#field-packageidprefix}

Aesir 包的 package.json name 前缀（识别本框架包）。

``` csharp
public const string PackageIdPrefix = "cn.runestone.aesir.";
```

### UpmSamplesRootPath {#field-upmsamplesrootpath}

UPM 示例导入的落地根目录（Package Manager → Samples → Import 后的位置）。

``` csharp
public const string UpmSamplesRootPath = "Assets/Samples";
```

### KnownPackages {#field-knownpackages}

已公开发布的 Aesir 包（顺序即概览卡片顺序）。

``` csharp
public static readonly AesirGetStartedService.AesirKnownPackage[] KnownPackages;
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ScanPackages()`](#method-scanpackages) | 扫描本机安装的 Aesir 包并解析示例。包按 Id 字母序返回 （cn.runestone.aesir.architecture → cn.runestone.aesir.modules，恰为教学顺序）； 同名包按「Assets 副本 → 嵌入式 → PackageCache」优先级取一。 |
| [`GroupSamples(AesirGetStartedService.AesirPackageInfo)`](#method-groupsamples-aesirgetstartedservice-aesirpackageinfo) | 按教学分组归置包内示例（组内保持 package.json 声明顺序；组间按 GetGroupOrder 排序，同序号保持首现顺序——插入排序保证稳定性）。 |
| [`OpenSampleScene(AesirGetStartedService.AesirSampleInfo)`](#method-opensamplescene-aesirgetstartedservice-aesirsampleinfo) | 打开示例场景：先保存当前打开的场景一次（无未保存修改时为空操作），再切换到示例场景。 当前场景从未保存过（无路径）时由 Unity Save 面板兜底，用户在面板中取消保存则中止切换 （避免丢失未保存的改动）；无场景 / 未导入示例退化为 PingSample 定位。 |
| [`PingSample(AesirGetStartedService.AesirSampleInfo)`](#method-pingsample-aesirgetstartedservice-aesirsampleinfo) | 在 Project 窗口选中并 Ping 示例根目录文件夹（未导入时打开 Package Manager）。 |
| [`BuildOpenSceneToastMessage(AesirGetStartedService.AesirSampleInfo)`](#method-buildopenscenetoastmessage-aesirgetstartedservice-aesirsampleinfo) | 打开场景动作的 Toast 提示文本（告知示例场景已打开、切换前的场景已保存）。 |
| [`BuildPingToastMessage(AesirGetStartedService.AesirSampleInfo)`](#method-buildpingtoastmessage-aesirgetstartedservice-aesirsampleinfo) | 定位动作的 Toast 提示文本（告知用户已在 Project 窗口选中示例文件夹）。 |
| [`GetSampleBadge(AesirGetStartedService.AesirSampleInfo)`](#method-getsamplebadge-aesirgetstartedservice-aesirsampleinfo) | 档位徽章文本（无档位返回 null）：名称中的 快捷 / 标准 / 严格，或目录序号（01 基础、其余进阶）。 |
| [`GetSampleGroup(AesirGetStartedService.AesirSampleInfo)`](#method-getsamplegroup-aesirgetstartedservice-aesirsampleinfo) | 示例分组标题（渐进式教学顺序：MVC → MVP → 功能演示 → 实战 → 各模块）。 |
| [`OpenPackageManager()`](#method-openpackagemanager) | 打开 Package Manager（UPM / 嵌入式安装的示例经其 Samples 标签页导入）。 |

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

### ScanPackages() {#method-scanpackages}

扫描本机安装的 Aesir 包并解析示例。包按 Id 字母序返回 （cn.runestone.aesir.architecture → cn.runestone.aesir.modules，恰为教学顺序）； 同名包按「Assets 副本 → 嵌入式 → PackageCache」优先级取一。

``` csharp
public static List<AesirGetStartedService.AesirPackageInfo> ScanPackages()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `List<AesirGetStartedService.AesirPackageInfo>` | — |

</div>

### GroupSamples(AesirGetStartedService.AesirPackageInfo) {#method-groupsamples-aesirgetstartedservice-aesirpackageinfo}

按教学分组归置包内示例（组内保持 package.json 声明顺序；组间按 GetGroupOrder 排序，同序号保持首现顺序——插入排序保证稳定性）。

``` csharp
public static List<AesirGetStartedService.SampleGroup> GroupSamples(AesirGetStartedService.AesirPackageInfo pkg)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `pkg` | `AesirGetStartedService.AesirPackageInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `List<AesirGetStartedService.SampleGroup>` | — |

</div>

### OpenSampleScene(AesirGetStartedService.AesirSampleInfo) {#method-opensamplescene-aesirgetstartedservice-aesirsampleinfo}

打开示例场景：先保存当前打开的场景一次（无未保存修改时为空操作），再切换到示例场景。
当前场景从未保存过（无路径）时由 Unity Save 面板兜底，用户在面板中取消保存则中止切换 （避免丢失未保存的改动）；无场景 / 未导入示例退化为 PingSample 定位。

``` csharp
public static bool OpenSampleScene(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 是否已实际打开示例场景（保存被取消或示例不可打开时为 false，不产生切换）。 |

</div>

### PingSample(AesirGetStartedService.AesirSampleInfo) {#method-pingsample-aesirgetstartedservice-aesirsampleinfo}

在 Project 窗口选中并 Ping 示例根目录文件夹（未导入时打开 Package Manager）。

``` csharp
public static bool PingSample(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | 是否定位成功（资产缺失或未导入时为 false）。 |

</div>

### BuildOpenSceneToastMessage(AesirGetStartedService.AesirSampleInfo) {#method-buildopenscenetoastmessage-aesirgetstartedservice-aesirsampleinfo}

打开场景动作的 Toast 提示文本（告知示例场景已打开、切换前的场景已保存）。

``` csharp
public static string BuildOpenSceneToastMessage(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### BuildPingToastMessage(AesirGetStartedService.AesirSampleInfo) {#method-buildpingtoastmessage-aesirgetstartedservice-aesirsampleinfo}

定位动作的 Toast 提示文本（告知用户已在 Project 窗口选中示例文件夹）。

``` csharp
public static string BuildPingToastMessage(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### GetSampleBadge(AesirGetStartedService.AesirSampleInfo) {#method-getsamplebadge-aesirgetstartedservice-aesirsampleinfo}

档位徽章文本（无档位返回 null）：名称中的 快捷 / 标准 / 严格，或目录序号（01 基础、其余进阶）。

``` csharp
public static string GetSampleBadge(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### GetSampleGroup(AesirGetStartedService.AesirSampleInfo) {#method-getsamplegroup-aesirgetstartedservice-aesirsampleinfo}

示例分组标题（渐进式教学顺序：MVC → MVP → 功能演示 → 实战 → 各模块）。

``` csharp
public static string GetSampleGroup(AesirGetStartedService.AesirSampleInfo sample)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sample` | `AesirGetStartedService.AesirSampleInfo` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### OpenPackageManager() {#method-openpackagemanager}

打开 Package Manager（UPM / 嵌入式安装的示例经其 Samples 标签页导入）。

``` csharp
public static void OpenPackageManager()
```

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
