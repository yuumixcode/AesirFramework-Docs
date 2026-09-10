# 更新日志

本页为站点摘要视图。完整历史(含 0.14.0 之前版本与各子包独立变更)见主仓库:

- [根 CHANGELOG.md](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)(monorepo 聚合视图)
- [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases)(unitypackage 下载)

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/),版本号遵循[语义化版本](https://semver.org/lang/zh-CN/)。

## 当前版本

| 子包 | 包名 | 版本 |
|------|------|------|
| Aesir Architecture | `cn.runestone.aesir.architecture` | **0.18.0** |
| Aesir Modules | `cn.runestone.aesir.modules` | **0.18.0** |

!!! tip "版本策略"
    两包同号发版(CI 校验一致),推荐同版本安装。Aesir Modules 依赖 Aesir Architecture;Aesir Architecture 不依赖任何 Aesir 子包。

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
