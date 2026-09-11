# 场景模块

场景模块负责场景加载、叠加追踪与卸载回收,语义对齐 Unity 原生 `LoadSceneMode`:Single 卸载全部场景并重设激活场景;Additive 纯叠加、不改变激活场景,叠加场景统一记入追踪列表。

## SceneModule —— 场景管理单例

预放置优先:把 `SceneModule` 挂到启动场景物体上(推荐);未预放置时运行时自动创建于 `[Aesir Modules]` 宿主下。

!!! warning "预放置请保持 DDOL 开启"
    预放置为根物体时受 `dontDestroyOnLoad` 字段(默认开)控制 —— **保持开启**:Single 加载会卸载所有旧场景,关闭 DDOL 的实例将随场景销毁并中断进行中的加载回调。重复实例只销毁自身组件,不连带销毁宿主物体。

### 场景加载与卸载

```csharp
// 单模式加载(onProgress 逐帧 0-1,已按 Unity 场景激活上限 0.9 归一化,进度条可平滑走满)
SceneModule.Instance.LoadSceneSingle(scenePath,
    onCompleted: () => { },
    onFailed:    () => { },
    onProgress:  p => { });

// 纯叠加加载(不改变激活场景,按路径粒度去重追踪)
SceneModule.Instance.LoadSceneAdditive(scenePath);

// 卸载(经本模块叠加加载的场景自动移出追踪;批量卸载单个失败跳过并告警)
SceneModule.Instance.UnloadScene(scenePath);
SceneModule.Instance.UnloadAllAddedScenes();

// 激活场景切换(多场景叠加工作流:决定光照设置来源与 Instantiate 默认落点)
SceneModule.Instance.SetActiveScene(scenePath);

// 重载当前激活场景(异步 Single 语义)
SceneModule.Instance.ReloadScene();

// 场景生命周期广播(MiniEvent,参数为场景路径;AddListener 返回自动清理句柄)
SceneModule.Instance.SceneLoadedEvent.AddListener(path => Debug.Log($"已加载 {path}"));
SceneModule.Instance.SceneUnloadedEvent.AddListener(path => Debug.Log($"已卸载 {path}"));

// 查询
IReadOnlyList<string> added = SceneModule.Instance.AddedScenePaths;   // 叠加追踪
Scene last = SceneModule.Instance.LastLoadedScene;
```

所有加载方法均支持路径字符串或 `SceneAssetWrapper` 重载。引用无效(空 / 不在 BuildSettings)或 Addressable 场景走 `onFailed`,不抛异常。

### 启动场景(Bootstrap)分工

- **运行时**:`SceneModule` 只持有 `bootstrapScene` 引用(`BootstrapSceneAssetWrapper`)供用户代码读取,不做自动流转
- **编辑器**:BuildSettings 序号 0 与进 Play 强制打开 Bootstrap 场景由 `BootstrapSceneHelper` 负责(`Tools → Aesir → Scene Editor Settings` 中开启,**默认关闭**)

## SceneAssetWrapper —— 可序列化场景引用

`[Serializable]` 强类型场景引用(功能设计参考 Eflatun.SceneReference),解决"场景引用无法序列化进预制体 / SO"的痛点:

- **GUID 锚点自愈** —— `SceneAsset` 引用丢失但 GUID 在时,自动经 `AssetDatabase.GUIDToAssetPath` 找回场景路径(移动 / 重命名免疫)
- **状态机校验** —— `State`(Regular / Addressable / Unsafe)+ `UnsafeReason`(Empty / NotInBuild),Build Settings 途径优先于 Addressables
- **TryGet 安全读取家族** —— `TryGetScenePath` / `TryGetBuildIndex` / `TryGetSceneName` / `TryGetLoadedScene` / `TryGetAddress`,空引用返回 false 不抛异常
- **工厂方法** —— `FromScenePath(string)`(编辑器校验资产存在)/ `FromAsset(SceneAsset)`(仅编辑器)
- **专用异常族** —— 数据访问属性(`ScenePath` / `SceneName` / `Address` 等)在空引用 / 未装包 / 不可寻址时抛四类专用异常,消息均带"修复 / 规避"双指引

编辑器增强(**需 Odin Inspector**):Inspector 拖拽赋值 + 三态着色(Addressable 青 / 悬空与缺 Build 红 / 禁用黄 / 正常白)+ 一键修复按钮(添加到 BuildSettings / 启用 / 加入 Addressables 默认组)。

!!! note "未安装 Odin 时"
    仅保证 API 可用:`FromScenePath` 构造、编辑器下 `SceneAsset` 属性代码赋值、TryGet 家族读取;Inspector 面板效果(拖拽 / 着色 / 一键修复)不支持。

## Addressables 集成(可选)

条件编译架构:核心 asmdef 经 `versionDefines` 定义 `AESIR_MODULES_ADDRESSABLES`,独立胶水程序集在**未安装 Addressables 时整体不编译**(零报错):

- 装包即启用:`SceneAssetWrapper.Address` / `TryGetAddress` 地址查询能力
- 卸包自动隐藏:相关 API 运行期访问才抛 `AddressablesSupportDisabledException`(API 始终可见可编译,最小惊讶)
- 核心程序集零 Addressables 依赖,经 `SceneAssetWrapperAddressablesBridge` 静态委托桥接

> **Addressable 场景不经 SceneModule 加载** —— wrapper 提供地址后,加载 / 卸载请直接调用 Addressables API(如 `Addressables.LoadSceneAsync(wrapper.Address)`)。

## 编辑器工具

| 工具 | 入口 | 说明 |
|------|------|------|
| `Scene Editor Settings` | 菜单 `Tools → Aesir → Scene Editor Settings` | 场景编辑器设置窗口(内嵌 SceneEditorSettings 与 bootstrap 辅助开关) |
| `SceneEditorSettings` | ScriptableSingleton | 编辑器阶段持久化设置 |
| `BootstrapSceneHelper` | 设置窗口开启(默认关闭) | 搜集 Bootstrapper 场景注册进 Build Settings 首位;进 Play 强制打开启动场景 |

## 设计边界

- **重复叠加同一路径后果自负** —— Unity 会加载两个场景实例而追踪列表按路径只记一条,`UnloadScene` 只卸载其一;请勿对同一路径重复 `LoadSceneAdditive`
- **不做场景间传参 / async 化** —— 跨场景传数据用框架 MiniEvent 或共享 Model

## 继续阅读

- [快速开始](getting-started.md) —— 安装与 UI 上手
- [兼容性](compatibility.md) —— Addressables / Odin 可选集成矩阵
