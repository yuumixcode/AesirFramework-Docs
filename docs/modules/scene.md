# 场景模块

场景模块提供启动场景(Bootstrap)管理、叠加场景追踪与强类型场景引用,并配套编辑器工具。

## SceneModule —— 场景管理单例

作为 `[Aesir Modules]` 宿主的子物体懒加载创建,无需手动放置。

### 启动场景(Bootstrap)

按预设名称自动发现启动场景:`Bootstrap` / `BootstrapScene` / `Bootstrapper` / `BootstrapperScene` / `bootstrap_scene` / `bootstrap` / `bootstrapper_scene` / `bootstrapper`(与编辑器工具共用同一名单),也可在 Inspector 指定自定义 `SceneAssetWrapper`。

### 场景加载与卸载

```csharp
// 单模式加载(先清空叠加追踪,完成后设为激活场景)
SceneModule.Instance.LoadSceneSingle("Game", onCompleted: () => { }, onFailed: () => { });

// 纯叠加加载(不改变激活场景,按路径粒度去重追踪)
SceneModule.Instance.LoadSceneAdditive("UI", onCompleted: () => { });

// 卸载 / 全部卸载 / 异步重载当前场景
SceneModule.Instance.UnloadScene("UI", onUnloaded: () => { });
SceneModule.Instance.UnloadAllAddedScenes(onAllUnloaded: () => { });
SceneModule.Instance.ReloadScene(onCompleted: () => { }, onFailed: () => { });

// 进度与状态
float progress = SceneModule.Instance.GetTotalLoadingProgress();   // 0-1 平均进度
IReadOnlyList<string> added = SceneModule.Instance.AddedScenePaths;
Scene last = SceneModule.Instance.LastLoadedScene;
```

所有加载方法均支持路径字符串或 `SceneAssetWrapper` 重载,并带完成 / 失败回调。Addressable 状态的场景会被拒绝加载(走 `onFailed`),请改用 Addressables API。

## SceneAssetWrapper —— 可序列化场景引用

`[Serializable]` 强类型场景引用(功能设计参考 Eflatun.SceneReference),解决"场景引用无法序列化进预制体 / SO"的痛点:

- **GUID 锚点自愈** —— `SceneAsset` 引用丢失但 GUID 在时,自动经 `AssetDatabase.GUIDToAssetPath` 找回场景路径
- **状态机校验** —— `State`(Unsafe / Regular / Addressable)+ `UnsafeReason`(Empty / NotInBuild),Build Settings 途径优先于 Addressables
- **TryGet 安全读取家族** —— `TryGetScenePath` / `TryGetBuildIndex` / `TryGetSceneName` / `TryGetLoadedScene` / `TryGetAddress`,空引用返回 false 不抛异常
- **工厂方法** —— `FromScenePath(string)`(编辑器校验资产存在)/ `FromAsset(SceneAsset)`(仅编辑器)

数据访问属性(`ScenePath` / `Guid` / `SceneName` / `BuildIndex` / `LoadedScene` / `Address`)在空引用时抛带修复指引的异常:

| 异常 | 触发场景 |
|------|---------|
| `EmptySceneAssetWrapperException` | 空引用访问(修复:拖入 SceneAsset 或 FromScenePath) |
| `SceneNotAddressableException` | 非 Addressable 场景访问 `Address` |
| `SceneAssetWrapperCreationException` | 工厂方法入参无效 |
| `AddressablesSupportDisabledException` | 未安装 Addressables 包时访问 Address 功能 |

编辑器增强(安装 Odin Inspector 时):内联展示 + 状态着色(Addressable 青 / 悬空红 / 禁用黄 / 正常白)+ 一键修复按钮(添加到 Build Settings / 启用 / 加入 Addressables 默认组 / Reset)。

## Addressables 集成(可选)

条件编译架构:核心 asmdef 经 `versionDefines` 定义 `AESIR_MODULES_ADDRESSABLES`,独立胶水程序集在**未安装 Addressables 时整体不编译**(零报错):

- 装包即启用:`SceneAssetWrapper.Address` 地址查询与「加入 Addressables 默认组」能力
- 卸包自动隐藏:相关 API 运行期访问才抛 `AddressablesSupportDisabledException`(API 始终可见可编译,最小惊讶)
- 核心程序集零 Addressables 依赖,经 `SceneAssetWrapperAddressablesBridge` 静态委托桥接

## 编辑器工具

| 工具 | 入口 | 说明 |
|------|------|------|
| `SceneManagerWindow` | 菜单 `Tools → 场景管理方案设置窗口` | 场景管理设置窗口(内嵌 SceneEditorSettings) |
| `SceneEditorSettings` | ScriptableSingleton | 自动搜集 Bootstrapper 并注册、强制优先加载 Bootstrapper 等开关 |
| `BootstrapSceneHelper` | 自动(`InitializeOnLoad`) | 将 Bootstrapper 场景注册进 Build Settings 首位;Play 时自动切换到启动场景并往返恢复 |

## 继续阅读

- [快速开始](getting-started.md) —— 安装与 UI 上手
- [兼容性](compatibility.md) —— Addressables / Odin 可选集成矩阵
