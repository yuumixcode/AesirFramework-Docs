# Aesir Modules 兼容性

## 引擎版本

- Unity / 团结引擎 **2022.3+**(开发与验证环境:2022.3.62f3c1)
- 与渲染管线无关(纯逻辑层 + uGUI)

## 包依赖

| 依赖 | 必需性 | 说明 |
|------|--------|------|
| `cn.runestone.aesir.architecture` | **必需** | 两包同号发版,推荐同版本安装(如 0.20.0);经 Git URL 安装时需同时添加两个包的 URL |
| `com.unity.test-framework` | 仅测试程序集 | 运行时无依赖 |

## 可选集成

三个可选能力均遵循"未安装时不报错、自动隐藏"原则:

### Odin Inspector(`ODIN_INSPECTOR`)

- Binder 组件绑定全家桶位于独立 Odin 程序集(`Runestone.AesirModules.OdinInspector`),未安装 Odin 时整体排除
- UI / Scene 模块的 AttributeProcessor 样式增强同理条件编译
- 核心功能(UIModule / UIRoot / SceneModule)无 Odin 完整可用

### Addressables(`AESIR_MODULES_ADDRESSABLES`)

- `SceneAssetWrapper` 的地址查询能力经**胶水程序集 + defineConstraints** 条件编译
- 装包即启用;卸包后相关 API 自动隐藏,不产生编译错误
- UI 资源加载默认走 Resources;需要 Addressables 时实现 `IUIAssetLoader` 替换

### Input System(`ENABLE_INPUT_SYSTEM`)

- 独立程序集,启用 Input System 包时自动以 `InputSystemUIInputModule` 替换 UIRoot 默认输入模块
- 未安装时使用 uGUI 默认输入(StandaloneInputModule)

## 模块隔离

- 模块间零依赖:**删除模块 = 删除 `Runtime/<模块>/` 与 `Editor/<模块>/`**,不影响其余模块编译
- 核心程序集锚点在层根,模块主代码自动汇入;细分程序集(Odin / Addressables)经 asmref 汇入