# 更新日志

本页为站点摘要视图。完整历史(含 0.14.0 之前版本与各子包独立变更)见主仓库:

- [根 CHANGELOG.md](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)(monorepo 聚合视图)
- [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases)(unitypackage 下载)

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/),版本号遵循[语义化版本](https://semver.org/lang/zh-CN/)。

## 当前版本

| 子包 | 包名 | 版本 |
|------|------|------|
| Aesir Architecture | `cn.runestone.aesir.architecture` | **0.20.0** |
| Aesir Modules | `cn.runestone.aesir.modules` | **0.20.0** |

!!! tip "版本策略"
    两包同号发版(CI 校验一致),推荐同版本安装。Aesir Modules 依赖 Aesir Architecture;Aesir Architecture 不依赖任何 Aesir 子包。

## [0.20.0] - 2026-09-11

### Aesir Architecture

- 新增《设计变更记录》文档——废弃机制(事件总线/ModelReplaced/120 帧轮询/初始化失败回滚/异常吞噬等十组)与设计来源统一收录,源码注释此后只描述当前行为
- 注释精简(12 文件):移除源码注释中的历史演进叙述(更名史/fake-null 演进史/复刻来源等),重复 remarks 去重
- 修复 `AesirArchitecture.DontDestroyOnLoad` 遗留 CS0108 编译警告(补 `new` 修饰符,行为不变)

### Aesir Modules

- **事件模块分发增强与 SO 资产化**——订阅者过滤器(`ISubscriberFilter` + `WithTag`/`WithPriority`/`SameSceneAsEmitter`/`OnlySelf`/`InsideCollider2D`,fail-closed);死引用清理(分发期自动移除已销毁订阅者);性能监控(`executionMsLimit`,默认关闭);`AesirEventArgsSO` 资产发布者 + `UnityEventOnAesirEvent` 桥接组件 + `SubclassSelector` 子类下拉;热路径绑定键缓存(分发热路径稳态零分配,编译委托加速 ~78 倍);新增 22 用例与 `02_Filters`/`03_SOAsset` 示例
- **新增音频模块(2D)**——`AudioModule` 全静态门面:SFX 独占音源轮询(每播音调/音量独立,无每播实例化开销)、BGM 淡入淡出与同曲幂等、Master/BGM/SFX 三通道音量与静音 PlayerPrefs 持久化;30 用例与 `01_BasicUsage` 示例
- **场景模块行为层补齐**——`SceneModule` 补 DDOL 字段(修复预放置实例被自己的 `LoadSceneSingle` 销毁)、新增 `SetActiveScene` 与场景事件广播、`onProgress` 进度回调、`SceneAssetWrapper` 悬空判定;20 用例与专属文档
- **UI 模块注册表重构(含破坏性变更)**——三字典合并单注册表(键=实际类型,基类类型调用 ShowPanel 报错拒绝/HidePanel/GetPanel 警告)、层 Canvas 缺失 fail-fast 中止、`HidePanel<T>` 约束收紧为 `MonoBehaviour, IUIPanel`;移除 `UIModule.RegisterUIRoot` 与 `IUIAssetLoader.Unload`(破坏性);13 用例与专属文档
- **ScriptDocGenerator 修复与增强**——生成器三处输出 bug 修复(单成员类丢章节/常量表过滤写反/空继承章节)、Zensical 生成器参数与备注全链路输出、面板配置域重载不再丢失、默认输出目录移出 Assets、UI Toolkit 窗口移除(Odin 窗口为唯一入口)、Summary 工具改为 `[Summary]` 特性优先语义
- 修复 `AesirListenerAttribute` 缺 `AllowMultiple`、`SubscriberPriority` 文档口径修正(实为 4 档 First/High/Medium/Last)

## [0.19.0] - 2026-09-11

### Aesir Architecture

- 新增 `IContext` / `AbstractContext<T>` 的 `UnregisterModel<TModel>` / `UnregisterService<TService>`——按类型键摘除注册并释放实例(幂等,注销后再注册追加到顺序末尾)
- 新增 `AesirArchitecture.DontDestroyOnLoad` 只读属性——暴露 DDOL 决策取值,供运行时查询与编辑器条件提示复用
- 修复 Odin AttributeProcessor 两处信息框宣称与实现不符(类级条件 Warning 补齐/DDOL 警告改条件显示);`AbstractSubmodule.Dispose` 重置 `Initialized`;快捷档示例 Model 改只读属性暴露、严格档示例缓存 Query 实例复用

### Aesir Modules

- 版本号与 Aesir Architecture 同步更新至 `0.19.0`,本包本版本无功能性变更

## [0.18.0] - 2026-09-10

### Aesir Architecture

- `AesirArchitecturePlayerLoop.Register` 现返回 `AutoRemoveListenerHandle`——Dispose 时自动注销本次注册,对齐全框架句柄风格;忽略返回值的既有调用不受影响
- 新增 `CapabilityExtensionsTests`(10 用例)——CQRS 执行链首次获得测试覆盖:带参/无参命令与查询、命令链、查询组合、`IController<T>` 默认接口实现绑定、两阶段初始化异常语义、Dispose 后单例重建
- 修复 **Model 初始化阶段获取 Service 的误导性报错**——明确「先全部 Model、后全部 Service」两阶段初始化下 Model 阶段无法获取 Service(与注册顺序无关),须延迟到运行期方法调用
- 修复 `AbstractContext<T>.Dispose` 后的**僵尸单例**——释放后解除 `Instance` 单例缓存,再次访问重建并重新初始化全新上下文,而非返回容器已清空的空壳
- 修正三处 XML 文档失实:`AesirArchitecture` 组件职责(实为 DDOL 宿主,不初始化架构数据)、`AesirArchitecturePlayerLoop` 已废弃的"周期性检测"宣称、`MiniEvent`"零分配"措辞(仅 Invoke 路径零分配)
- 解除 Editor 工具对测试框架的结构绑定:Editor 主程序集移除 `UNITY_INCLUDE_TESTS` defineConstraint、package.json 移除 test-framework 硬依赖;PlayMode 测试程序集以 `ODIN_INSPECTOR` 守卫(无 Odin 环境自动排除)
- `RegisterCustomLifecycle(mono / GameObject, evt, callback)` 现将监听绑定到所在物体销毁事件自动移除(行为变更,原先不自动移除)
- 重复实例去重改用 `Destroy(this)` 不再连带销毁业务物体;私有 `Reset` 更名 `ClearState` 避免撞名 Unity 魔法方法;`AbstractQuery` 补 `[Serializable]`

### Aesir Modules

- **ScriptDocGenerator 模块(需 Odin)**——原 `Assets/ScriptDocGenerator` 独立工具整合为包内功能模块:反射分析 C# 类型生成结构化 API 文档(增量保留手写内容),附 Summary 工具(XML `<summary>` ↔ `[Summary]` 双向同步);153 个单元测试汇入测试程序集;入口 `Tools → Aesir → Script Doc Generator`

## [0.17.0] - 2026-09-06

### Aesir Architecture

- 新增 `InternalContextAttribute` —— 标记框架内部 Context(示例 / 测试用途);Aesir Modules Binder 的「Context 类型」选择器自动跳过被标记的类型
- 修复**示例场景无法运行**(0.14.0 起回归):示例程序集改为运行时程序集 + 示例脚本整文件 `#if UNITY_EDITOR` 包裹 —— 编辑器内可编译、可挂载、可 Play,玩家构建整体剔除(示例类型 0 入包)

### Aesir Modules

- **Binder 组件绑定全面完善** —— 双生成模式(「同一脚本增量」默认 /「Partial 分部类」可选,默认 `.designer.cs` 后缀);基类下拉新增 `AesirBasePanelView<T>` / `AesirBasePanelViewController<T>` 预选;层级右键菜单快捷挂载 `BinderAssistant` / `BinderTag`;命名空间默认值与后缀候选持久化;新增 69 个 EditMode 测试
- 修复 Binder 生成脚本接口不匹配、Partial 模式覆盖手写文件、绑定校验空引用等问题
- 同步修复示例场景回归(同 Architecture 机制)

## [0.16.x] - 2026-09-06

- `LICENSE.md` 与 `Third Party Notices.md` 移至包根,对齐 UPM 包根约定
- Third Party Notices 收录设计参考条目:Cysharp/ObservableCollections(Architecture)、Eflatun.SceneReference(Modules)

## [0.16.0] - 2026-09-06(Modules 主要变更)

- `SceneAssetWrapper` 功能增强(吸收 Eflatun.SceneReference):GUID 锚点自愈、`State` / `UnsafeReason` 状态机、`TryGet` 安全读取家族、工厂方法
- Addressables 条件架构:未安装时相关代码整体不编译、零报错
- **破坏性变更**:删除 `AddScene` / `UnloadAddedScene` 统一为 `LoadSceneAdditive` 纯叠加追踪;`ReloadScene` 同步改异步;`SceneAssetWrapper` 空引用语义收紧(抛 `EmptySceneAssetWrapperException`);加载失败全系新增 `onFailed` 回调
- 目录调整为标准 Unity 自定义包根结构(`Runtime/` / `Editor/` 两级,模块以子目录存在,模块间零依赖)

## [0.15.0] - 2026-09-05

- 新增可观察集合 `ObservableHashSet<T>`;新增 RuntimeInitializeLoadType 示例
- 包内更新器大陆优化:jsDelivr 多域名 → GitHub API → 302 重定向探测三级兜底
- Modules 无功能性变更(版本同步)

## [0.14.0] - 2026-09-05

- **AesirFramework 转型**:AesirInspector 迁出为独立仓库;本仓库由 Aesir Architecture 与 Aesir Modules 组成
- Samples / Documentation 双目录结构(`Samples/` 编写主位 + `Samples~/` 发布镜像)
- 新增 PlaneWar 实战示例(Mono 版)

## 更早版本

0.13.0 及更早的完整变更(含 ObservableList / ObservableDictionary、DDOL 重设计、MVP 示例家族、Query 系统等里程碑)请查阅[根 CHANGELOG](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)与各子包内 `CHANGELOG.md`。
