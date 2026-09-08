# 常见问题(FAQ)

## 安装与更新

### Git URL 和 unitypackage 怎么选?

| 方式 | 适合谁 |
|------|--------|
| **Git URL(固定版本分支)** | 常规项目;包只读、经 Package Manager 更新,不碰用户代码区 |
| **unitypackage + 包内更新器** | 想**改包源码**、或大陆 / 离线环境 GitHub 直连不稳的项目;安装在 `Assets/Runestone/` 下,`Tools → Aesir → Check for Updates` 一键更新 |
| **跟踪 main(`?path=`)** | 想吃最新开发预览的用户 |

### 为什么更新器检测不到刚发布的版本?

版本检测面向大陆做了多源兜底(jsDelivr CDN → GitHub API → 重定向探测)。经 CDN 检测时,分支引用缓存最长约 12 小时 —— **最新发布最长约 12 小时后才被检测到**。

### 更新器能更新 Git URL(UPM)安装的包吗?

不能。更新器只管辖 `Assets/Runestone/` 下的代码导入副本;UPM 副本请直接用 Package Manager 更新。**开发仓库(存在 `.git`)切勿点更新** —— Release 内容会覆盖本地源码(窗口已内置警告)。

### 版本分支策略是什么?

版本分支(`AesirArchitecture-v<版本>` / `AesirModules-v<版本>`)由 CI 在每次推送 main 时自动按包目录 subtree split 生成,**仓库只保留最新版本分支**,旧版本分支随发版删除。想锁旧版本请用 Releases 页面的 unitypackage。

### 安装 Aesir Modules 时为什么还要添加 Architecture 的 URL?

Modules 依赖 Architecture(必需)。UPM 对 Git URL 安装的包不会自动解析包内 dependencies 为 Registry 引用,因此两个包的 Git URL 都要添加(推荐同版本)。

## 使用问题

### 没装 Odin Inspector 能用吗?

**能**。核心架构流程闭环(Context 注册 → Model/Service 初始化 → Command/Query 执行 → ObservableValue 通知)与 UI 框架核心功能无 Odin 完整可用;Odin 相关代码经 `#if ODIN_INSPECTOR` 条件编译自动排除,只影响 Inspector 增强体验(`AesirView<T>` 系列基类、Binder、Drawer 等)。

### 示例怎么导入?会进构建吗?

- **Git URL 安装**:Package Manager → 选中包 → `Samples` 标签页按需 Import
- **unitypackage 导入 / 本仓库浏览**:示例随包内含,位于各包 `Samples/` 目录
- 示例程序集为运行时程序集 + 整文件 `#if UNITY_EDITOR`:编辑器内可运行,**玩家构建整体剔除**(示例类型 0 入包)

### 示例场景打开后脚本 Missing / 无法挂载?

请确认使用 Unity / 团结引擎 2022.3+,并完整导入包(含 `Samples`)。本仓库直接浏览时示例就在 `Samples/` 目录下,场景可直接打开运行。

## 高频陷阱与修法

> 完整 10 条陷阱清单见包内 `Documentation/常见陷阱清单.md`。异常消息已含修复指引(fail-fast)。

### `GetModel<T>()` 抛"未注册"异常

按实现类注册、按接口获取(或反过来)—— **Register 与 Get 必须使用相同类型参数**(推荐都用接口)。异常消息含近失识别提示。

### 拿到了第二个 Context 实例 / 空引用

`Configure()` 与各模块 `OnInitialize()` 中**禁止访问 `Instance`** —— 会递归创建第二个上下文。模块间互相访问放到 `OnInitialize()`(此时全部已注册完毕)。

### 抛"该 Model 尚未初始化"

注册顺序错误或循环依赖 —— Configure 中**被依赖的模块先注册**(框架按注册顺序初始化 Model → Service)。

### 一个监听者抛异常后,后面的监听者不执行了

MiniEvent 是零分配直调,异常语义 = 原生 C# 事件(fail-fast)。**监听回调不应抛异常**(框架约定);业务异常在回调内部自行 try-catch。

### GameObject 销毁后仍收到事件 / 内存泄漏

`AddListener` 返回的 `AutoRemoveListenerHandle` 未绑定生命周期。一行修法:

```csharp
model.Count.AddListenerAndInvoke(OnCountChanged)
    .RemoveListenerWhenGameObjectOnDestroyed(gameObject);   // UI 面板用 RemoveListenerWhenGameObjectOnDisable
```

### 外部代码把我的事件链整体替换了(`view.Xxx = null`)

用 `public Action Xxx { get; set; }` 代替了 `event`。接口中声明 `event Action Xxx;` —— 编译期限制外部只能 `+=` / `-=`。

### 事件模块(EventModule)为什么标"实验性"?

双轨订阅(Attribute + Script)、4 档优先级与表达式树优化已实现并有测试覆盖,但**尚未在实际项目中验证,API 可能调整**;简单场景建议优先用 MiniEvent / ObservableValue。

## 未找到答案?

前往[支持](support.md)或在 [GitHub Issues](https://github.com/yuumixcode/AesirFramework/issues) 提问(附复现步骤与 Unity 版本)。