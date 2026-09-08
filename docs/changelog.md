# 更新日志

本页为站点摘要视图。完整历史(含 0.14.0 之前版本与各子包独立变更)见主仓库:

- [根 CHANGELOG.md](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)(monorepo 聚合视图)
- [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases)(unitypackage 下载)

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/),版本号遵循[语义化版本](https://semver.org/lang/zh-CN/)。

## 当前版本

| 子包 | 包名 | 版本 |
|------|------|------|
| Aesir Architecture | `cn.runestone.aesir.architecture` | **0.17.0** |
| Aesir Modules | `cn.runestone.aesir.modules` | **0.17.0** |

!!! tip "版本策略"
    两包同号发版(CI 校验一致),推荐同版本安装。Aesir Modules 依赖 Aesir Architecture;Aesir Architecture 不依赖任何 Aesir 子包。

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
