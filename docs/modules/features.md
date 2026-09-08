# Aesir Modules 特性一览

## UI 框架

### 核心类型

| 类型 | 说明 |
|------|------|
| `UIModule` | UI 管理器单例(Manager of Managers):面板注册、显示、隐藏、预热与注册表维护;提供静态快捷 API 全局调用 |
| `UIRoot` | UI 根节点:构建四层 Canvas(Background / Normal / Popup / Top)+ UICamera + EventSystem,Canvas 统一配置经 `UICanvasConfigSO` |
| `IUIPanel` | 面板契约:生命周期 `Initialize → Show(payload) → Hide → DestroyPanel`;属性 `Layer` / `DestroyOnHide` / `IsOpen` |
| `AesirBasePanel` | 面板基类:虚方法 `OnInit` / `OnShow` / `OnHide` / `OnClose`,便捷方法 `HideSelf()` |
| `AesirBasePanelView<T>` | MVP 模式面板视图基类:继承 `AesirBasePanel` 并按 Context 类型绑定,经 Context 访问 Model / Service |
| `IUIAssetLoader` / `ResourcesUILoader` | 可插拔资源加载契约与默认实现 |
| `UILayer` | 层级枚举:Background / Normal / Popup / Top |

### 面板生命周期

```
激活 → 停用(缓存)→ 销毁
```

- 面板以停用状态实例化,按 挂层 → `Initialize` → `Show` 顺序驱动
- `DestroyOnHide = false` 时隐藏仅 SetActive(false) 缓存复用;`true` 时隐藏即销毁
- `Prewarm<T>()` 逐帧预实例化,`PrewarmAll()` 分摊首次打开的实例化卡顿
- `AesirBasePanel.OnDestroy` 静态反清理 `UIModule` 注册表,防止域内残留

### Binder 组件绑定(Odin 可选)

`BinderAssistant` / `BinderTag` 将 UI 元素自动绑定到面板脚本:

- `BinderTag` 挂在子物体上做标记;`BinderAssistant` 挂在面板根,「构建绑定单元」按标记增量维护绑定列表
- 两种生成模式:**同一脚本增量**(只替换 `*.cs` 内「绑定字段(自动生成)」region,region 外归开发者)与 **Partial 分部类**(手写 partial + 自动维护文件,Rider 用户推荐)
- 生成脚本基类可下拉选择:`MonoBehaviour`、Aesir 面板家族(`AesirBasePanel` / `AesirBasePanelView<T>` / `AesirBasePanelViewController<T>`)或用户以 `[BinderBaseType]` 标记的类
- 编译完成后自动挂载组件并执行一次绑定;配套 EditMode 测试

### Input System 适配(可选)

独立程序集;启用 Input System 包时自动以 `InputSystemUIInputModule` 替换 UIRoot 的默认输入模块。

## 事件模块(⚠️ 实验性)

> 尚未在实际项目中验证,API 可能调整。

双轨订阅事件系统:`[AesirListener]` 特性静态订阅 + `AddListener<T>` 动态 Lambda 订阅,共存于同一分发流程,按 4 档优先级(First / High / Medium / Last)排序执行;静态绑定经**表达式树编译委托**优化反射开销(仅首次编译有成本,调用零反射)。详见[事件模块](events.md)。

```csharp
// 1. 定义事件参数(数据载体)
public class OnPlayerScored : AesirEventArgs
{
    public int points;
    public string playerName;
}

// 2. Attribute 订阅
public class ScoreUI : MonoBehaviour
{
    void OnEnable()  => EventModule.AddListener(this);
    void OnDisable() => EventModule.RemoveListener(this);

    [AesirListener]
    private void OnPlayerScored(OnPlayerScored e) { /* ... */ }
}

// 3. Script 订阅(返回 AutoRemoveListenerHandle)
_handle = EventModule.AddListener<OnPlayerScored>(this, e => Debug.Log(e.points));
_handle.Dispose();

// 4. 发布
new OnPlayerScored { points = 10, playerName = "Player1" }.Invoke(this);
```

核心类型:`AesirEventArgs`(参数基类)、`AesirListenerAttribute`、`EventModule`(单例)、`BindingInfo` 家族、`SubscriberPriority`。

## 场景模块

`SceneModule`(MonoBehaviour 单例)负责启动场景与叠加场景管理:

- **启动场景(Bootstrap)** — 按预设名称(`Bootstrap` / `Bootstrapper` 等)或自定义 `SceneAssetWrapper` 引用自动发现启动场景,确保其在构建设置中序号为 0、优先加载
- **场景加载** — `LoadSceneSingle` 单模式、`LoadSceneAdditive` 纯叠加追踪(`AddedScenePaths` / `LastLoadedScene` / `GetTotalLoadingProgress`);路径或 `SceneAssetWrapper` 重载,均带完成 / 失败回调
- **场景卸载** — `UnloadScene` / `UnloadAllAddedScenes` / `ReloadScene`(异步重载当前场景)
- **`SceneAssetWrapper`** — 可序列化场景引用:GUID 锚点自愈、状态机校验(`State` / `UnsafeReason`)、`TryGet` 安全读取家族;安装 Addressables 时自动扩展地址查询能力
- **编辑器配套** — `SceneManagerWindow` 场景管理窗口;`BootstrapSceneHelper` 自动搜集 Bootstrapper 场景并注册进 Build Settings