# AesirFramework

> 面向团结引擎 / Unity 的渐进式 MVC 架构框架与功能模块集合。**极简、可渐进、Unity 原生优先。**

## 核心包

### Aesir Architecture

渐进式 MVC 架构框架 —— 能力接口组合、命令/查询模式(CQRS)、轻量事件(MiniEvent)与响应式属性(ObservableValue)、PlayerLoop 原生生命周期。

- MVC / MVP 双模式,三档渐进路径(快捷 → 标准 → 严格)
- 纯 C# 架构根 + MonoBehaviour 适配层,Domain Reload 安全
- 9 个可导入示例:6 个计数器示例逐课对照 + PlaneWar 实战小游戏

[开始使用](architecture/getting-started.md){ .md-button .md-button--primary } [特性一览](architecture/features.md){ .md-button }

### Aesir Modules

Aesir Architecture 之上的功能模块集 —— UI 框架(Manager-of-Managers 单例、四层 Canvas 层级、面板生命周期)+ 场景管理工具 + 实验性事件模块。

[开始使用](modules/getting-started.md){ .md-button .md-button--primary } [特性一览](modules/features.md){ .md-button }

## 快速链接

- [Aesir Architecture 概览](architecture/index.md) / [Aesir Modules 概览](modules/index.md)
- [示例总览](architecture/samples.md) — 计数器六档对照 + PlaneWar 实战小游戏
- [更新日志](changelog.md) / [常见问题 FAQ](faq.md) / [支持](support.md)
- 源码仓库:[yuumixcode/AesirFramework](https://github.com/yuumixcode/AesirFramework)(MIT)

## 版本信息

| 项 | 值 |
|----|----|
| 当前版本 | 0.17.0(Architecture / Modules 同号发版) |
| Unity / 团结引擎 | 2022.3+(开发环境 2022.3.62f3c1) |
| 渲染管线 | 架构层与管线无关;开发验证于 URP 14.0.12 |
| 许可证 | MIT |