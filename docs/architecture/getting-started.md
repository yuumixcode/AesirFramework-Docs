# Aesir Architecture 快速开始

## 前置要求

- Unity 或团结引擎 **2022.3+**(开发环境:2022.3.62f3c1)
- Odin Inspector **可选**(3.3.x+):未安装时核心架构流程完整可用,仅排除 Inspector 增强功能

## 安装

### 方式 1:固定版本分支(推荐)

Unity Package Manager → 左上角 `+` → `Add package from git URL...`:

```
https://github.com/yuumixcode/AesirFramework.git#AesirArchitecture-v0.18.0
```

版本分支由 CI 自动按包目录 subtree split 生成,仓库只保留最新版本分支。

### 方式 2:unitypackage 导入 + 包内更新器(大陆 / 离线友好)

从 [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases) 下载 `AesirArchitecture-v<版本>.unitypackage`(或两包合并的 `AesirFramework-v<版本>.unitypackage`)导入。

以此方式安装的包位于 `Assets/Runestone/` 下(代码可改),**更新无需手动重新下载**:菜单 `Tools → Aesir → Check for Updates` 打开包内更新器,一键完成"检测新版本 → 自动备份 → 差集清理残留 → 静默导入"。版本检测面向大陆做了多源兜底(jsDelivr CDN → GitHub API → 重定向探测);经 CDN 检测,最新发布最长约 12 小时后才被检测到。

!!! warning "更新器管辖范围"

    经 Git URL(UPM)安装的副本**不在更新器管辖内**,请直接用 Package Manager 更新。开发仓库(存在 `.git`)切勿点更新。

### 方式 3:跟踪 main 最新(开发预览)

```
https://github.com/yuumixcode/AesirFramework.git?path=Assets/Runestone/AesirArchitecture
```

## 第一个 MVC 应用

### 1. 定义 Context

```csharp
using Runestone.AesirArchitecture;

public class CounterContext : AbstractContext<CounterContext>
{
    protected override void Configure()
    {
        RegisterModel<ICounterModel>(new CounterModel());
    }
}
```

### 2. 定义 Model

```csharp
public interface ICounterModel : IModel
{
    IReadOnlyObservableValue<int> Count { get; }
    void Increase();
    void Decrease();
}

public sealed class CounterModel : AbstractModel, ICounterModel
{
    [SerializeField] ObservableValue<int> count = new ObservableValue<int>(0);

    public IReadOnlyObservableValue<int> Count => count;
    public void Increase() => count.Value++;
    public void Decrease() => count.Value--;

    protected override void OnInitialize() { }
}
```

### 3. 定义 View

```csharp
public class UICounterPanel : MonoView<CounterContext>
{
    [SerializeField] Text countText;
    [SerializeField] Button increaseButton;

    ICounterModel _model;
    CounterController _ctrl;

    void Start()
    {
        _model = this.GetModel<ICounterModel>();
        _model.Count.AddListenerAndInvoke(UpdateCountText)
            .RemoveListenerWhenGameObjectOnDestroyed(gameObject);
        _ctrl = new CounterController();
    }

    void OnEnable() => increaseButton.onClick.AddListener(_ctrl.Increase);
    void OnDisable() => increaseButton.onClick.RemoveListener(_ctrl.Increase);

    public void UpdateCountText(int count) => countText.text = count.ToString();
}
```

### 4. 使用 Command / Query(严格档)

```csharp
// 定义命令(写操作)
public class AddScoreCommand : AbstractCommand
{
    protected override void OnExecute()
    {
        var model = this.GetModel<IScoreModel>();
        model.AddScore(10);
    }
}

// Controller 中执行
this.ExecuteCommand<AddScoreCommand>();
```

## 导入示例

Package Manager → Aesir Architecture → **Samples** 标签页,按需导入:

| 示例 | 档次 | 亮点 |
|------|------|------|
| `Counter-Mvc-Quick / Standard / Strict` | MVC 三课 | View 兼 Controller 直改 → 只读暴露 + 写方法 → Command 写 + Query 读 |
| `Counter-Mvp-Quick / Standard / Strict` | MVP 三课 | 与 MVC 逐课同构,View 被动、Presenter 推送 |
| `MiniEvent` / `ObservableValue` | 工具类 | MiniEvent 用法 / Odin Drawer 演示(后者需 Odin) |
| `PlaneWar` | 实战 | 纵版射击完整小游戏:MiniEvent + ObservableValue + MonoLifecycleProxy 组合运用 |

本仓库用户也可直接浏览包内 `Samples/` 目录;示例场景可运行,构建时自动剔除(整文件 `#if UNITY_EDITOR`)。

## 下一步

- [特性一览](features.md) — 核心机制速览与选型决策
- [概览](index.md) — 架构角色与三档渐进路径
- [FAQ](../faq.md) — 高频问题与陷阱修法