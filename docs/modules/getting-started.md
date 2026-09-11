# Aesir Modules 快速开始

## 前置要求

- Unity / 团结引擎 2022.3+
- **Aesir Architecture**(必需依赖,两包同号发版,推荐同版本安装)
- Odin Inspector 可选(仅影响 Binder 绑定等增强功能)

## 安装

Unity Package Manager → `+` → `Add package from git URL...`:

```
https://github.com/yuumixcode/AesirFramework.git#AesirModules-v0.20.0
```

只安装 Aesir Modules 时,请同时添加 Aesir Architecture 的 Git URL(UPM 对 Git URL 安装的包不会自动解析包内 dependencies 声明为 Registry 引用):

```
https://github.com/yuumixcode/AesirFramework.git#AesirArchitecture-v0.20.0
```

或编辑 `Packages/manifest.json`:

```json
{
  "dependencies": {
    "cn.runestone.aesir.architecture": "https://github.com/yuumixcode/AesirFramework.git#AesirArchitecture-v0.20.0",
    "cn.runestone.aesir.modules": "https://github.com/yuumixcode/AesirFramework.git#AesirModules-v0.20.0"
  }
}
```

**unitypackage 方式**:从 [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases) 下载 `AesirModules-v<版本>.unitypackage`(注意不含依赖,需自行导入 Architecture;或直接用两包合并的 `AesirFramework-v<版本>.unitypackage`)。导入后经 `Tools → Aesir → Check for Updates` 一键更新。

## 第一个面板

### 1. 创建 UIRoot

菜单 `GameObject → Aesir Modules → UI → Create UIRoot`,一键构建四层 Canvas(Background / Normal / Popup / Top)+ UICamera + EventSystem。层 Canvas / UICamera / EventSystem 为序列化引用持久化,构建后可自由调整。

### 2. 编写面板脚本

```csharp
using Runestone.AesirModules;

public class MainMenuPanel : AesirBasePanel
{
    protected override void OnInit() { }                 // 首次实例化后调用一次
    protected override void OnShow(object payload) { }   // 每次显示时调用(含首次)
    protected override void OnHide() { }                 // 隐藏时调用
    protected override void OnClose() { }                // 销毁前调用
}
```

制作面板预制体,根节点挂上面板脚本,在 Inspector 中设置 `layer`(层级)与 `destroyOnHide`(隐藏时销毁还是缓存复用)。

### 3. 注册并显示

```csharp
// 注册面板预制体
UIModule.RegisterPrefab<MainMenuPanel>(prefab);

// 显示面板
UIModule.Show<MainMenuPanel>();

// 带参数显示(强类型 payload)
UIModule.Show<ConfirmDialogPanel, ConfirmData>(new ConfirmData { message = "确定?" });

// 关闭(按面板的 DestroyOnHide 决定销毁或缓存复用)
UIModule.Hide<ConfirmDialogPanel>();

// 预热:预实例化并隐藏,首次 Show 直接复用,避免卡顿
UIModule.Prewarm<MainMenuPanel>();
```

> **生命周期细节**:面板以停用状态实例化(Awake / OnEnable 推迟到 Show 激活时才触发,保证 OnEnable 可安全访问 OnInit 之后才有值的引用),按 挂层 → `Initialize` → `Show` 顺序驱动;面板注册以实例的**实际类型**为键,以基类类型 Show 后需以实际类型(或面板内 `HideSelf()`)关闭。

### 4. 自定义资源加载(可选)

默认从 Resources 目录加载(`ResourcesUILoader`,预制体路径约定为面板类型名)。实现 `IUIAssetLoader` 即可替换为 Addressables 等:

```csharp
UIModule.Instance.RegisterAssetLoader(new MyAddressablesLoader());
```

## 导入示例

Package Manager → Aesir Modules → **Samples**:

| 示例 | 说明 |
|------|------|
| `Events/01_KeyPress` | 事件模块基本发布-订阅:按键发布事件、`[AesirListener]` 静态订阅 |

## 下一步

- [特性一览](features.md) — UI / Event / Scene 三模块与 Binder
- [概览](index.md) — 模块总览与包结构