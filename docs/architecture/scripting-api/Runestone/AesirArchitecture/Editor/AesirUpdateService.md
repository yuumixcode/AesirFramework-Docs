---
title: AesirUpdateService
description: "Runestone.AesirArchitecture.Editor.AesirUpdateService 的 API 文档"
---

# `AesirUpdateService`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor`

**继承链:** `System.Object` → `AesirUpdateService`

## 声明

``` csharp
public static class AesirUpdateService
```

Aesir 包自动更新服务 — 供 AesirUpdateWindow 调用的无状态工具集。
适用场景：用户通过复制 / unitypackage 导入方式将包装在 InstallRootRelativePath （Assets/Runestone）下、代码可被修改的非 UPM 安装。经 Package Manager（Git URL）安装的副本 不位于 Assets 下，本工具扫描不到，应改用 Package Manager 更新。

版本检测面向大陆用户做了多源兜底（unitypackage 下载始终走 GitHub Release 直链）： ① jsDelivr 多域名拉取仓库内 UpdateInfoRelativePath（CDN 直达、无限流， 分支引用有最长约 12 小时的缓存延迟）；② GitHub Releases API（未认证 60 次/时/IP）；③ GitHub releases/latest 的 302 重定向探测（完全绕开 API 限流）。见 FetchLatestReleaseSnapshotAsync。

更新流程：检测远程版本 → 对比本地版本（直接读取包内 package.json）→ 更新前自动备份 （用户可能修改过代码）→ 按"上次安装清单 − 新版清单"精确差集清理残留（不误伤用户新增文件）→ 下载 .unitypackage → 静默导入 → 逐包登记安装清单。

## 字段

**常量字段**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`BackupKeepCount`](#field-backupkeepcount) | 本地备份保留份数（超出后按时间从旧到新删除）。 |
| [`DownloadTimeoutSeconds`](#field-downloadtimeoutseconds) | unitypackage 下载超时（秒）——大文件慢速连接，给足余量。 |
| [`GitHubCheckTimeoutSeconds`](#field-githubchecktimeoutseconds) | GitHub API / 重定向探测超时（秒）。 |
| [`JsDelivrCheckTimeoutSeconds`](#field-jsdelivrchecktimeoutseconds) | jsDelivr 检测超时（秒）——不可达时通常立刻失败，超时不宜过长。 |
| [`BackupDirName`](#field-backupdirname) | 项目根目录下的备份目录名（点前缀，Unity 不导入）。 |
| [`InstallRootRelativePath`](#field-installrootrelativepath) | 包安装根目录（项目相对路径）。 |
| [`ManifestFileName`](#field-manifestfilename) | 本地安装清单文件名（记录每次更新成功后各包的完整文件列表）。 |
| [`RepoPath`](#field-repopath) | GitHub 仓库路径（owner/repo）。 |
| [`StateDirName`](#field-statedirname) | 项目根目录下的更新状态目录名（点前缀，Unity 不导入）。 |
| [`UpdateInfoRelativePath`](#field-updateinforelativepath) | update-info.json 在仓库内的路径（CI 发版后以 [skip ci] 提交回 main）。 |

</div>

**声明的字段**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`GitHubDownloadUrlBase`](#field-githubdownloadurlbase) | GitHub Release 资产下载地址前缀（资产命名约定见 ReleaseSnapshot.GetUnityPackageUrl）。 |
| [`LatestReleaseApiUrl`](#field-latestreleaseapiurl) | GitHub Releases 最新版 API（降级源之二，未认证限流 60 次/时/IP）。 |
| [`LatestReleasePageUrl`](#field-latestreleasepageurl) | GitHub releases/latest 页面地址（302 到最新 tag，可完全绕开 API 限流）。 |
| [`ReleasesPageUrl`](#field-releasespageurl) | Releases 网页地址（供用户手动下载 / 查看更新日志）。 |
| [`JsDelivrDomains`](#field-jsdelivrdomains) | jsDelivr CDN 域名（按大陆可达性经验排序；fastly 会 301 跳转到主域名，自动跟随）。 |

</div>

### BackupKeepCount {#field-backupkeepcount}

本地备份保留份数（超出后按时间从旧到新删除）。

``` csharp
public const int BackupKeepCount = 3;
```

### DownloadTimeoutSeconds {#field-downloadtimeoutseconds}

unitypackage 下载超时（秒）——大文件慢速连接，给足余量。

``` csharp
public const int DownloadTimeoutSeconds = 120;
```

### GitHubCheckTimeoutSeconds {#field-githubchecktimeoutseconds}

GitHub API / 重定向探测超时（秒）。

``` csharp
public const int GitHubCheckTimeoutSeconds = 12;
```

### JsDelivrCheckTimeoutSeconds {#field-jsdelivrchecktimeoutseconds}

jsDelivr 检测超时（秒）——不可达时通常立刻失败，超时不宜过长。

``` csharp
public const int JsDelivrCheckTimeoutSeconds = 5;
```

### BackupDirName {#field-backupdirname}

项目根目录下的备份目录名（点前缀，Unity 不导入）。

``` csharp
public const string BackupDirName = ".aesir-backup";
```

### InstallRootRelativePath {#field-installrootrelativepath}

包安装根目录（项目相对路径）。

``` csharp
public const string InstallRootRelativePath = "Assets/Runestone";
```

### ManifestFileName {#field-manifestfilename}

本地安装清单文件名（记录每次更新成功后各包的完整文件列表）。

``` csharp
public const string ManifestFileName = "installed-manifest.json";
```

### RepoPath {#field-repopath}

GitHub 仓库路径（owner/repo）。

``` csharp
public const string RepoPath = "yuumixcode/AesirFramework";
```

### StateDirName {#field-statedirname}

项目根目录下的更新状态目录名（点前缀，Unity 不导入）。

``` csharp
public const string StateDirName = ".aesir";
```

### UpdateInfoRelativePath {#field-updateinforelativepath}

update-info.json 在仓库内的路径（CI 发版后以 [skip ci] 提交回 main）。

``` csharp
public const string UpdateInfoRelativePath = ".github/update-info.json";
```

### GitHubDownloadUrlBase {#field-githubdownloadurlbase}

GitHub Release 资产下载地址前缀（资产命名约定见 ReleaseSnapshot.GetUnityPackageUrl）。

``` csharp
public static readonly string GitHubDownloadUrlBase = "https://github.com/yuumixcode/AesirFramework/releases/download";
```

### LatestReleaseApiUrl {#field-latestreleaseapiurl}

GitHub Releases 最新版 API（降级源之二，未认证限流 60 次/时/IP）。

``` csharp
public static readonly string LatestReleaseApiUrl = "https://api.github.com/repos/yuumixcode/AesirFramework/releases/latest";
```

### LatestReleasePageUrl {#field-latestreleasepageurl}

GitHub releases/latest 页面地址（302 到最新 tag，可完全绕开 API 限流）。

``` csharp
public static readonly string LatestReleasePageUrl = "https://github.com/yuumixcode/AesirFramework/releases/latest";
```

### ReleasesPageUrl {#field-releasespageurl}

Releases 网页地址（供用户手动下载 / 查看更新日志）。

``` csharp
public static readonly string ReleasesPageUrl = "https://github.com/yuumixcode/AesirFramework/releases";
```

### JsDelivrDomains {#field-jsdelivrdomains}

jsDelivr CDN 域名（按大陆可达性经验排序；fastly 会 301 跳转到主域名，自动跟随）。

``` csharp
public static readonly string[] JsDelivrDomains;
```

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ProjectRootPath`](#property-projectrootpath) | Unity 项目根目录（Application.dataPath 的上一级）。 |
| [`StateFilePath`](#property-statefilepath) | 本地安装清单的项目相对路径。 |

</div>

### ProjectRootPath {#property-projectrootpath}

Unity 项目根目录（Application.dataPath 的上一级）。

``` csharp
public static string ProjectRootPath { get; } = "/Users/yuumix/Projects/Unity/AesirFramework";
```

### StateFilePath {#property-statefilepath}

本地安装清单的项目相对路径。

``` csharp
public static string StateFilePath { get; } = ".aesir/installed-manifest.json";
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`LoadLocalManifest()`](#method-loadlocalmanifest) | 读取本地安装清单；文件不存在或损坏返回 null。 |
| [`MergePackageEntry(AesirUpdateService.FilesManifest, AesirUpdateService.FilesManifest.PackageEntry)`](#method-mergepackageentry-aesirupdateservice-filesmanifest-aesirupdateservice-filesmanifest-packageentry) | 将远程清单中的一个包条目合并进本地清单（按 name 替换或追加）。 返回合并后的新清单实例（输入参数不被修改）。 |
| [`ParseFilesManifest(string)`](#method-parsefilesmanifest-string) | 解析本地清单 JSON；内容为空或格式异常时返回 null（调用方按"无记录"处理）。 |
| [`ParseUpdateInfo(string)`](#method-parseupdateinfo-string) | 解析 update-info.json；内容为空或格式异常时返回 null（调用方按"源不可用"处理）。 |
| [`ScanInstalledPackages(string)`](#method-scaninstalledpackages-string) | 扫描 installRootRelativePath 下的 Aesir 包安装。 识别依据：子目录中存在 package.json 且包 id 以 cn.runestone.aesir. 开头。 |
| [`ComputeStaleFiles(string[], string[], string)`](#method-computestalefiles-string-string-string) | 计算需要删除的残留条目：上次安装清单中存在、新版清单中不存在、且位于指定包目录内。 上次清单为空（首次安装 / 无历史记录）时返回空列表 — 没有历史就无法界定"该删什么"， 宁可残留也不误删。用户在包内新增的文件不在任何清单中，天然不会被删除。 |
| [`ParsePackageJson(string)`](#method-parsepackagejson-string) | 解析 package.json 的 name 与 version 字段。 轻量字段提取（要求自包含，不引入 JSON 库）。 |
| [`FetchLatestReleaseSnapshotAsync()`](#method-fetchlatestreleasesnapshotasync) | 获取最新 Release 快照（tag + 可能的清单）。按以下顺序兜底，首个成功即返回： ① jsDelivr 多域名拉取仓库内 update-info.json（大陆友好、无限流，CDN 缓存延迟最长约 12 小时）； ② GitHub Releases API（未认证 60 次/时/IP）；③ GitHub releases/latest 的 302 重定向探测。 全部失败时抛出含各源错误明细的异常。 |
| [`DownloadBytesAsync(string, Action<float>, int)`](#method-downloadbytesasync-string-action-float-int) | GET 二进制内容（用于下载 unitypackage），通过回调上报 0~1 下载进度。 |
| [`GetTextAsync(string, int)`](#method-gettextasync-string-int) | GET 文本内容（UnityWebRequest，编辑器主线程异步等待）。 |
| [`ProbeLatestTagFromRedirect()`](#method-probelatesttagfromredirect) | 向 GitHub releases/latest 发起禁止重定向的 HEAD 请求，从 302 Location 中提取最新 tag。 完全绕开 API 限流（该路径不走 api.github.com）。 |
| [`CompareVersion(string, string)`](#method-compareversion-string-string) | 比较两个语义化版本号（允许 v/V 前缀，缺省段按 0 处理）。 返回值：a < b 为负，相等为 0，a > b 为正。 |
| [`DeleteStaleEntries(IEnumerable<string>)`](#method-deletestaleentries-ienumerable-string) | 删除残留条目：文件直接删除（连带同名 .meta）；目录仅在其为空时删除。 返回实际删除的条目数。传入的路径必须是项目相对路径。 |
| [`PruneEmptyDirectories(string)`](#method-pruneemptydirectories-string) | 自底向上删除指定包目录下的空目录（连带 .meta，不删除包根目录本身）。 返回删除的目录数。用于残留文件删除后收尾清理空目录。 |
| [`BackupRunestone(string, string, string, int)`](#method-backuprunestone-string-string-string-int) | 将安装根目录整体复制到备份目录（<backupRoot>/<label>），并裁剪至保留最近 keepCount 份。源目录不存在时返回 null（无安装即无备份）。 |
| [`ExtractJsonField(string, string)`](#method-extractjsonfield-string-string) | 从 JSON 文本中按字段名提取第一个双引号字符串值（不依赖第三方 JSON 库）。 |
| [`ExtractTagFromLocation(string)`](#method-extracttagfromlocation-string) | 从 releases/latest 重定向地址中提取 tag（如 .../releases/tag/v0.15.0 → v0.15.0）； 不匹配返回 null。 |
| [`ToAbsolutePath(string)`](#method-toabsolutepath-string) | 将项目相对路径转为绝对路径。 |
| [`PruneBackups(string, int)`](#method-prunebackups-string-int) | 按目录名的 Ordinal 排序裁剪旧备份（label 以时间戳开头时排序即时间序）。 |
| [`SaveLocalManifest(AesirUpdateService.FilesManifest)`](#method-savelocalmanifest-aesirupdateservice-filesmanifest) | 写入本地安装清单（自动创建 .aesir 状态目录）。 |

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

### LoadLocalManifest() {#method-loadlocalmanifest}

读取本地安装清单；文件不存在或损坏返回 null。

``` csharp
public static AesirUpdateService.FilesManifest LoadLocalManifest()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirUpdateService.FilesManifest` | — |

</div>

### MergePackageEntry(AesirUpdateService.FilesManifest, AesirUpdateService.FilesManifest.PackageEntry) {#method-mergepackageentry-aesirupdateservice-filesmanifest-aesirupdateservice-filesmanifest-packageentry}

将远程清单中的一个包条目合并进本地清单（按 name 替换或追加）。 返回合并后的新清单实例（输入参数不被修改）。

``` csharp
public static AesirUpdateService.FilesManifest MergePackageEntry(AesirUpdateService.FilesManifest localManifest, AesirUpdateService.FilesManifest.PackageEntry entry)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `localManifest` | `AesirUpdateService.FilesManifest` | — |
| `entry` | `AesirUpdateService.FilesManifest.PackageEntry` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirUpdateService.FilesManifest` | — |

</div>

### ParseFilesManifest(string) {#method-parsefilesmanifest-string}

解析本地清单 JSON；内容为空或格式异常时返回 null（调用方按"无记录"处理）。

``` csharp
public static AesirUpdateService.FilesManifest ParseFilesManifest(string json)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `json` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirUpdateService.FilesManifest` | — |

</div>

### ParseUpdateInfo(string) {#method-parseupdateinfo-string}

解析 update-info.json；内容为空或格式异常时返回 null（调用方按"源不可用"处理）。

``` csharp
public static AesirUpdateService.UpdateInfo ParseUpdateInfo(string json)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `json` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `AesirUpdateService.UpdateInfo` | — |

</div>

### ScanInstalledPackages(string) {#method-scaninstalledpackages-string}

扫描 installRootRelativePath 下的 Aesir 包安装。 识别依据：子目录中存在 package.json 且包 id 以 cn.runestone.aesir. 开头。

``` csharp
public static List<AesirUpdateService.InstalledPackage> ScanInstalledPackages(string installRootRelativePath = "Assets/Runestone")
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `installRootRelativePath` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `List<AesirUpdateService.InstalledPackage>` | — |

</div>

### ComputeStaleFiles(string[], string[], string) {#method-computestalefiles-string-string-string}

计算需要删除的残留条目：上次安装清单中存在、新版清单中不存在、且位于指定包目录内。
上次清单为空（首次安装 / 无历史记录）时返回空列表 — 没有历史就无法界定"该删什么"， 宁可残留也不误删。用户在包内新增的文件不在任何清单中，天然不会被删除。

``` csharp
public static List<string> ComputeStaleFiles(string[] previousFiles, string[] newFiles, string packageAssetsPath)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `previousFiles` | `string[]` | — |
| `newFiles` | `string[]` | — |
| `packageAssetsPath` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `List<string>` | — |

</div>

### ParsePackageJson(string) {#method-parsepackagejson-string}

解析 package.json 的 name 与 version 字段。
轻量字段提取（要求自包含，不引入 JSON 库）。

``` csharp
public static ValueTuple<string, string> ParsePackageJson(string path)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `path` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `ValueTuple<string, string>` | — |

</div>

### FetchLatestReleaseSnapshotAsync() {#method-fetchlatestreleasesnapshotasync}

获取最新 Release 快照（tag + 可能的清单）。按以下顺序兜底，首个成功即返回： ① jsDelivr 多域名拉取仓库内 update-info.json（大陆友好、无限流，CDN 缓存延迟最长约 12 小时）； ② GitHub Releases API（未认证 60 次/时/IP）；③ GitHub releases/latest 的 302 重定向探测。 全部失败时抛出含各源错误明细的异常。

``` csharp
[AsyncStateMachine]
public static async Task<AesirUpdateService.ReleaseSnapshot> FetchLatestReleaseSnapshotAsync()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `Task<AesirUpdateService.ReleaseSnapshot>` | — |

</div>

### DownloadBytesAsync(string, Action<float>, int) {#method-downloadbytesasync-string-action-float-int}

GET 二进制内容（用于下载 unitypackage），通过回调上报 0~1 下载进度。

``` csharp
[AsyncStateMachine]
public static async Task<byte[]> DownloadBytesAsync(string url, Action<float> onProgress = null, int timeoutSeconds = 120)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `url` | `string` | — |
| `onProgress` | `Action<float>` | — |
| `timeoutSeconds` | `int` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `Task<byte[]>` | — |

</div>

### GetTextAsync(string, int) {#method-gettextasync-string-int}

GET 文本内容（UnityWebRequest，编辑器主线程异步等待）。

``` csharp
[AsyncStateMachine]
public static async Task<string> GetTextAsync(string url, int timeoutSeconds = 20)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `url` | `string` | — |
| `timeoutSeconds` | `int` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `Task<string>` | — |

</div>

### ProbeLatestTagFromRedirect() {#method-probelatesttagfromredirect}

向 GitHub releases/latest 发起禁止重定向的 HEAD 请求，从 302 Location 中提取最新 tag。 完全绕开 API 限流（该路径不走 api.github.com）。

``` csharp
[AsyncStateMachine]
public static async Task<string> ProbeLatestTagFromRedirect()
```

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `Task<string>` | — |

</div>

### CompareVersion(string, string) {#method-compareversion-string-string}

比较两个语义化版本号（允许 v/V 前缀，缺省段按 0 处理）。 返回值：a < b 为负，相等为 0，a > b 为正。

``` csharp
public static int CompareVersion(string a, string b)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `a` | `string` | — |
| `b` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `int` | — |

</div>

### DeleteStaleEntries(IEnumerable<string>) {#method-deletestaleentries-ienumerable-string}

删除残留条目：文件直接删除（连带同名 .meta）；目录仅在其为空时删除。 返回实际删除的条目数。传入的路径必须是项目相对路径。

``` csharp
public static int DeleteStaleEntries(IEnumerable<string> stalePaths)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `stalePaths` | `IEnumerable<string>` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `int` | — |

</div>

### PruneEmptyDirectories(string) {#method-pruneemptydirectories-string}

自底向上删除指定包目录下的空目录（连带 .meta，不删除包根目录本身）。 返回删除的目录数。用于残留文件删除后收尾清理空目录。

``` csharp
public static int PruneEmptyDirectories(string packageAssetsPath)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `packageAssetsPath` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `int` | — |

</div>

### BackupRunestone(string, string, string, int) {#method-backuprunestone-string-string-string-int}

将安装根目录整体复制到备份目录（<backupRoot>/<label>），并裁剪至保留最近 keepCount 份。源目录不存在时返回 null（无安装即无备份）。

``` csharp
public static string BackupRunestone(string label, string sourceRelativePath = "Assets/Runestone", string backupRootRelativePath = ".aesir-backup", int keepCount = 3)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `label` | `string` | 备份子目录名，须以时间戳开头（格式 yyyyMMdd-HHmmss_...）， 保证 Ordinal 排序即时间序（版本号前缀会打乱 0.9 与 0.14 的次序，故时间戳在前）。 |
| `sourceRelativePath` | `string` | — |
| `backupRootRelativePath` | `string` | — |
| `keepCount` | `int` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### ExtractJsonField(string, string) {#method-extractjsonfield-string-string}

从 JSON 文本中按字段名提取第一个双引号字符串值（不依赖第三方 JSON 库）。

``` csharp
public static string ExtractJsonField(string json, string fieldName)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `json` | `string` | — |
| `fieldName` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### ExtractTagFromLocation(string) {#method-extracttagfromlocation-string}

从 releases/latest 重定向地址中提取 tag（如 .../releases/tag/v0.15.0 → v0.15.0）； 不匹配返回 null。

``` csharp
public static string ExtractTagFromLocation(string location)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `location` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### ToAbsolutePath(string) {#method-toabsolutepath-string}

将项目相对路径转为绝对路径。

``` csharp
public static string ToAbsolutePath(string projectRelativePath)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `projectRelativePath` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `string` | — |

</div>

### PruneBackups(string, int) {#method-prunebackups-string-int}

按目录名的 Ordinal 排序裁剪旧备份（label 以时间戳开头时排序即时间序）。

``` csharp
public static void PruneBackups(string backupRootAbsolutePath, int keepCount)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `backupRootAbsolutePath` | `string` | — |
| `keepCount` | `int` | — |

</div>

### SaveLocalManifest(AesirUpdateService.FilesManifest) {#method-savelocalmanifest-aesirupdateservice-filesmanifest}

写入本地安装清单（自动创建 .aesir 状态目录）。

``` csharp
public static void SaveLocalManifest(AesirUpdateService.FilesManifest manifest)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `manifest` | `AesirUpdateService.FilesManifest` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
