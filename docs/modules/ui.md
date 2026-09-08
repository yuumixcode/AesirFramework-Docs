# UI 框架

Aesir Modules 的 UI 框架采用 Manager-of-Managers 单例模式:`UIRoot` 负责层级与画布,`UIModule` 负责面板生命周期,面板经 `AesirBasePanel` 家族接入。

## UIRoot —— UI 根节点

菜单 `GameObject → Aesir Modules → UI → Create UIRoot` 一键构建:

- **四层 Canvas**:Background(sortingOrder 100)/ Normal(200)/ Popup(300)/ Top(400),每层为 ScreenSpaceCamera 画布 + CanvasScaler + GraphicRaycaster
- **UICamera**:正交、depth 1、cullingMask 为 UI 与 TransparentFX 层
- **EventSystem**:全场景去重检查;默认挂 `StandaloneInputModule`(安装 Input System 包时自动替换为 `InputSystemUIInputModule`)

层级 Canvas / UICamera / EventSystem 均为**序列化引用持久化** —— 存在性判定只看引用非空,子物体重命名不会破坏引用;构建后可自由调整结构。

画布参数(分辨率 1920×1080、ScaleWithScreenSize 等)由 `UICanvasConfigSO` 统一配置;菜单 `Assets → Create → Aesir Modules → UI → Default UICanvasConfig` 生成默认配置资产,未配置时使用内置默认值。

## UIModule —— 面板管理器

静态快捷 API(全部转发到单例):

| API | 说明 |
|-----|------|
| `UIModule.Show<T>(payload, path)` | 显示面板(可带强类型 payload 与 Resources 路径) |
| `UIModule.Hide<T>()` | 隐藏面板(按 `DestroyOnHide` 决定销毁或缓存) |
| `UIModule.Get<T>()` | 获取已注册面板实例 |
| `UIModule.RegisterPrefab<T>(prefab)` | 注册面板预制体 |
| `UIModule.ContainPrefab<T>()` | 查询预制体是否已注册 |
| `UIModule.Prewarm<T>(path)` | 预实例化并隐藏,首次 Show 直接复用 |

`PrewarmAll()` 通过协程**逐帧**预实例化,分摊首次打开的实例化卡顿。

!!! warning "注册键 = 面板实例的实际类型"
    以基类类型 `Show` 后,需以实际类型(或面板内 `HideSelf()`)关闭。推荐始终用面板具体类型调用泛型 API。

## 面板生命周期

```
实例化(停用状态,Awake/OnEnable 不触发)
  → 挂到对应层 Canvas → Initialize → Show(payload)
  → Hide ── DestroyOnHide=false → 停用缓存(SetActive(false),下次 Show 复用)
         └ DestroyOnHide=true  → DestroyPanel(OnHide → OnClose → Destroy)
```

- 面板以**停用状态**实例化:`Awake` / `OnEnable` 推迟到 Show 激活时才触发,保证 `OnEnable` 可安全访问 `OnInit` 之后才有值的引用
- 面板被外部销毁 / 场景卸载时,`AesirBasePanel.OnDestroy` 自动反向清理 UIModule 注册表,无残留

面板基类家族:

| 基类 | 角色 | 用途 |
|------|------|------|
| `AesirBasePanel` | `IUIPanel` | 通用面板基类,虚方法 `OnInit` / `OnShow(payload)` / `OnHide` / `OnClose`,便捷方法 `HideSelf()` |
| `AesirBasePanelView<T>` | + RAA `IView` | MVP 模式面板:按 Context 类型绑定,只读访问 Model / Service |
| `AesirBasePanelViewController<T>` | + RAA `IController` | MVC 模式面板:可执行 Command / Query |

## 可插拔资源加载

默认 `ResourcesUILoader`(预制体路径约定为**面板类型名**)。实现 `IUIAssetLoader` 可替换为 Addressables 等方案:

```csharp
public interface IUIAssetLoader
{
    GameObject Load(string path);
    void Unload(GameObject prefab);
}

// 注入自定义加载器
UIModule.Instance.RegisterAssetLoader(new MyAddressablesLoader());
```

## DDOL 机制

`AesirModules` / `UIRoot` / `UIModule` 均有 `[SerializeField] bool dontDestroyOnLoad = true`:

- `AesirModules` 宿主:运行时创建恒为 DDOL
- `UIRoot`:预放置与运行时创建统一由该字段控制
- `UIModule`:字段仅在**预放置为根物体**时生效;运行时自动创建时挂载于 `[Aesir Modules]` 宿主下,跟随宿主决策

## Binder 组件绑定(需 Odin Inspector)

将 UI 元素自动绑定到面板脚本,免去手写 `transform.Find` / `GetComponent`:

1. `BinderTag` 挂在待绑定子物体上做标记(右键菜单 `GameObject → Aesir → 添加 BinderTag 标记`)
2. `BinderAssistant` 挂在面板根(右键菜单 `GameObject → Aesir → 挂载 BinderAssistant`),「构建绑定单元」按标记增量维护绑定列表
3. 「生成脚本」产出绑定代码;编译完成后自动挂载组件并执行一次绑定

两种生成模式:

| 模式 | 行为 |
|------|------|
| **同一脚本增量**(默认) | 只替换 `*.cs` 内「绑定字段(自动生成)」region,region 外归开发者 |
| **Partial 分部类** | 自动维护文件(后缀默认 `.designer.cs`)+ 手写 partial 仅首次生成;Rider 用户推荐 |

生成脚本基类可下拉选择:`MonoBehaviour`、Aesir 面板家族(`AesirBasePanel` / `AesirBasePanelView<T>` / `AesirBasePanelViewController<T>`)或用户以 `[BinderBaseType]` 标记的自定义基类;选择 Aesir 泛型基类时,「Context 类型」下拉扫描项目内 `AbstractContext` 派生类(自动排除 `[InternalContext]` 标记的示例 / 测试 Context)。

!!! note "Odin 依赖"
    Binder 的类型选择器(组件 / 基类下拉)强依赖 Odin Inspector,整套功能收录于独立 Odin 程序集;未安装 Odin 时整体排除,不影响 UI 框架其余功能。

## 继续阅读

- [快速开始](getting-started.md) —— 第一个面板的最小流程
- [场景模块](scene.md) —— SceneModule 与 SceneAssetWrapper
