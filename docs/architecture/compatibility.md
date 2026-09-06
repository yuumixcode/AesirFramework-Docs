# Aesir Architecture 兼容性

## 引擎版本

| 项 | 支持 |
|----|------|
| Unity / 团结引擎 | **2022.3+**(开发与验证环境:2022.3.62f3c1) |
| 团结引擎 | 一等公民支持(与 Unity 同版本号等效验证) |
| .NET | Unity 2022.3 默认 profile(.NET Standard 2.1 / 4.x API 兼容级) |

## 渲染管线

架构框架为**纯 C# 层 + MonoBehaviour 适配层**,不涉及渲染,与管线无关 —— 内置管线 / URP / HDRP 均可使用。开发仓库基于 URP 14.0.12 验证。

## Odin Inspector(可选)

- **不装 Odin**:核心架构流程闭环完整可用(Context 注册 → Model/Service 初始化 → Command/Query 执行 → ObservableValue 通知),`AesirView<T>` 等 Odin 增强基类自动排除,使用 `MonoView<T>` / `MonoViewController<T>` 系列
- **安装 Odin 3.3.x+**:自动启用 `ODIN_INSPECTOR` 集成 —— DDOL 开关 InfoBox、ObservableValue Drawer、AttributeProcessor 样式注入等 Inspector 增强
- 集成代码隔离在独立 `OdinInspector/` asmdef + 条件编译,不影响核心程序集

## 包依赖

- **不依赖任何 Aesir 子包**,可独立安装
- `com.unity.test-framework` 1.1.33(仅测试程序集引用)
- 可选集成:Odin Inspector(见上)

## 线程与运行时约定

- 所有框架类型仅保证**主线程**使用;`Task.Run` 等异步回调请先调度回主线程再访问框架
- Domain Reload 安全:静态变量显式重置,`Enter Play Mode Options`(禁用 Domain Reload)可安全启用

## 示例与构建

- 示例为**运行时程序集 + 整文件 `#if UNITY_EDITOR`**:编辑器内可编译、可挂载、可 Play;玩家构建时整体剔除(示例类型 0 入包)
- 包内 `Documentation/` 为 Unity TextAsset 格式但无引用,构建自动排除
- `Samples~` / `Documentation~` 隐藏目录对 AssetDatabase 不可见