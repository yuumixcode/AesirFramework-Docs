# Aesir Architecture 示例总览

包内含 **9 个可导入示例**(Package Manager → Aesir Architecture → Samples 标签页按需导入),外加 1 个仓库内编辑器示例。所有示例:

- 位于包内 `Samples/` 目录(仓库浏览时直接可见、场景可直接打开运行)
- 程序集为**运行时程序集 + 整文件 `#if UNITY_EDITOR`**:编辑器内可编译、可挂载、可 Play;玩家构建整体剔除,示例类型 0 入包
- 命名空间 `Runestone.AesirArchitecture.Samples.<示例名>`

## 计数器六档(MVC / MVP 各三课)

同一个"计数器界面"用六种写法实现,逐课同构对照 —— 这是学习框架的主线教程。每档只有一个核心增量:

| 档位 | 示例 | Model 暴露面 | 读写路径 | View 边界 |
|------|------|-------------|---------|-----------|
| MVC 第一课 | `Counter-Mvc-Quick` | 具体类,可写 `ObservableValue` | View 兼 Controller 直写直读 | `MonoViewController<T>` 单类 |
| MVC 第二课 | `Counter-Mvc-Standard` | 具体类,只读暴露 + 写方法 | Controller 直调写方法 | View 与 Controller 分离,共享 Model |
| MVC 第三课 | `Counter-Mvc-Strict` | 接口注册,只读暴露 + 写方法 | Command 写 + Query 加工读 | View 按业务窄接口持有 Controller |
| MVP 第一课 | `Counter-Mvp-Quick` | 具体类,可写 `ObservableValue` | Presenter 直改值并推送 | 纯 MonoBehaviour,零接口抽象 |
| MVP 第二课 | `Counter-Mvp-Standard` | 具体类,只读暴露 + 写方法 | Presenter 直调写方法 | View 契约 `IXxxView` |
| MVP 第三课 | `Counter-Mvp-Strict` | 接口注册,只读暴露 + 写方法 | Command 写 + Query 读 | View 按窄接口持有 Presenter |

各档要点:

=== "快捷档(Quick)"

    最少概念跑通数据驱动 UI 闭环。MVC 用 `MonoViewController<T>` 一个类兼 View 与 Controller;MVP 零接口抽象,Presenter 直改可写 `ObservableValue` 并推送被动 View。适合原型与教学起步。

=== "标准档(Standard)"

    **推荐起步档位**。Model 只读暴露 + 写方法封装修改入口;MVC 中 View 与 Controller 分离共享 Model;MVP 中 View 实现 `IXxxView` 契约,Presenter 直调写方法 + 读 Model 推送。

=== "严格档(Strict)"

    读写全解耦:Model 接口注册 + Command 写 + Query 读;View 按**业务窄接口**持有 Controller / Presenter —— 类型层面拿不到 `ExecuteCommand` / `GetModel` 等框架能力,读写分离由类型系统闭环。MVC 与 MVP 严格档结构完全对称。

!!! tip "学习路径建议"
    按 Quick → Standard → Strict 顺序对照源码阅读(MVC 与 MVP 各一遍),重点看每档"多出来的那一个概念"。六份示例的场景、UI、表现完全一致,差异只在架构分层。

## 工具类示例

### MiniEvent

`MiniEvent` 与 `MiniEvent<T>` 用法演示:无参 / 单参事件的订阅、触发与自动退订(多参数载荷建议用 struct 包裹成单参事件)。

### ObservableValue(需 Odin Inspector)

`ObservableValue<T>` 自定义 Drawer 演示:int / float / string / bool / Vector2 基础类型与 struct / class 复合类型在 Inspector 中的编辑与通知。

## PlaneWar 实战(Mono 版)

纵版射击飞机大战完整小游戏 —— 框架机制的组合实战:

- 得分 HUD(`ObservableValue` 驱动)、三型敌机、子弹命中计分(A=10 / B=20 / C=30)、坠毁重开流程
- 组合运用 `MiniEvent` + `ObservableValue` + `MonoLifecycleProxy`
- 素材自包含;菜单 `Tools → Aesir → PlaneWar → Fix Scene References` 一键修复场景引用

## RuntimeInitializeLoadType(仓库内示例)

编辑器窗口演示 `RuntimeInitializeLoadType` 五个初始化时机的执行顺序与静态重置最佳实践。菜单 `Tools → Aesir → Architecture → Samples → RuntimeInitializeLoadType`。

!!! note
    此示例是编辑器工具(Editor-only 程序集),未注册进 package.json Samples,仅在本仓库 `Samples/RuntimeInitializeLoadType/` 目录直接可用。

## 继续阅读

- [快速开始](getting-started.md) —— 手写第一个 MVC 计数器
- [架构概念](concepts.md) —— 示例背后的能力接口与 Context 机制
