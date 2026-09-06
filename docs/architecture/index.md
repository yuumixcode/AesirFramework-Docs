# Aesir Architecture

**渐进式 MVC 架构框架**,以 MVC 为主要模式,`IController` 是推荐的快速开发入口;`IPresenter`(MVP)作为可选的分层模式。

!!! note "占位"

    本页为骨架占位,正式内容整理中。

## 待整理章节

- [快速开始](getting-started.md)
- [特性](features.md)
- [兼容性](compatibility.md)
- [变更日志](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)

## 核心设计

- **能力接口组合**:每个角色(View / Controller / Presenter / Command / Query / Service / Model)通过组合细粒度能力接口定义
- **极简原则**:不做事件总线、不做命令池化、不做线程安全,保持同步零缓存