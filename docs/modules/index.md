# Aesir Modules 概览

**Aesir Modules(RAM)** 是 Aesir Architecture 之上的功能模块集合,采用标准 Unity 自定义包根结构(`Runtime/` / `Editor/` 两级,模块以子目录存在,模块间零依赖 —— 删除模块 = 删除对应目录)。

## 模块总览

| 模块 | 状态 | 说明 |
|------|------|------|
| **UI** | 已实现 | `UIModule` 单例(Manager of Managers)+ `UIRoot` 四层 Canvas + 面板生命周期 + 可插拔资源加载 |
| **Event** | ⚠️ 实验性 | `EventModule` 双轨订阅(Attribute + Script)+ 4 档优先级 + 表达式树优化;尚未在实际项目中验证 |
| **Scene** | 已实现 | `SceneModule` 启动 / 叠加场景管理 + 编辑器工具(SceneManagerWindow / BootstrapSceneHelper) |

另有两项**可选能力**:

- **Binder 组件绑定**(需 Odin Inspector)—— `BinderAssistant` / `BinderTag` 将 UI 元素自动绑定到面板脚本,支持代码生成
- **Input System 适配**(独立程序集)—— 启用 Input System 包时自动替换 UIRoot 的输入模块

## 依赖

- **Aesir Architecture** `cn.runestone.aesir.architecture`(必需;两包同号发版,推荐同版本安装)
- **Odin Inspector**(可选):仅经 `#if ODIN_INSPECTOR` 条件编译参与,未导入时自动排除

## 继续阅读

- [快速开始](getting-started.md) — 安装、UIRoot 与第一个面板
- [特性一览](features.md) — UI / Event / Scene 三模块速览
- [UI 框架](ui.md) — UIRoot / UIModule / 面板生命周期 / Binder
- [场景模块](scene.md) — SceneModule / SceneAssetWrapper / Addressables
- [事件模块](events.md) — 双轨订阅与优先级(实验性)
- [兼容性](compatibility.md) — 可选依赖(Odin / Addressables / Input System)