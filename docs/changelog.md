# 更新日志

本页为站点摘要视图。完整历史(含 0.14.0 之前版本与各子包独立变更)见主仓库:

- [根 CHANGELOG.md](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)(monorepo 聚合视图)
- [GitHub Releases](https://github.com/yuumixcode/AesirFramework/releases)(unitypackage 下载)

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/),版本号遵循[语义化版本](https://semver.org/lang/zh-CN/)。

## 当前版本

| 子包 | 包名 | 版本 |
|------|------|------|
| Aesir Architecture | `cn.runestone.aesir.architecture` | **0.27.1** |
| Aesir Modules | `cn.runestone.aesir.modules` | **0.27.1** |

!!! tip "版本策略"
    两包同号发版(CI 校验一致),推荐同版本安装。Aesir Modules 依赖 Aesir Architecture;Aesir Architecture 不依赖任何 Aesir 子包。

## [Unreleased]

### Aesir Modules

- **Removed**

    - `package.json` 依赖声明整段移除(破坏性)——UPM 不支持包内 Git URL 依赖(Unity 官方硬规定,保留会使单独安装直接失败),移除后单装可成功,缺 Aesir Architecture 时经 `Install Dependencies` 菜单一键补装;`com.unity.test-framework` 硬依赖一并移除(测试程序集已有 `UNITY_INCLUDE_TESTS` 守卫,非必需)。
    - 测试程序集收敛(破坏性)——每包只保留 `xxx.Tests.Editor`(EditMode)与 `xxx.Tests`(PlayMode)两个测试程序集:`Runestone.AesirModules.Scene.Tests` 并入包级 EditMode 程序集;包级 EditMode 改名 `Runestone.AesirModules.Tests.Editor`;PlayMode 程序集改名 `Runestone.AesirModules.Tests`。

- **Changed**

    - Scene 模块设置双窗口与无 Odin 编译修复——`SceneEditorSettings` 数据层 `#if ODIN_INSPECTOR` 包裹展示特性;Odin 版窗口迁入守卫程序集;新增原生 IMGUI 兜底窗口(OdinWindowOpener 路由,更新器双窗口同款);菜单更名 `Scene Module Settings`;无 Odin 环境 UPM E2E 0 编译错误(修复前 108 个 CS0246)。
    - `Install Dependencies` 补装菜单适用范围扩展——UPM 单独安装本包(缺 Aesir Architecture、核心程序集编译失败)同样触发一键补装;安装教程改为两包分别添加。

### Aesir Architecture

- **Changed**

    - `Tools → Aesir → Check for Updates` 菜单按安装形态显隐——扫描不到 Assets 形态的 Aesir 包安装时(纯 UPM 形态)菜单整体隐藏,Assets 形态安装(含与 UPM 混合并存)时照常显示。

## [0.27.1] - 2026-09-27

---

### Aesir Modules

**Fixed**

- **UniTask 集成的程序集名错误(asmdef 引用名与宏维护器检测名)** — UniTask 的命名空间名 `Cysharp.Threading.Tasks` 被误当作程序集名使用(com.cysharp.unitask 包内 asmdef 实际名为 `UniTask`):①核心与适配程序集的 asmdef `references` 解析不到任何程序集,含 UniTask 的消费工程刷新即报 `CS0246`(`'Cysharp'` / `'UniTaskVoid'` 找不到);②`AesirUniTaskDefineKeeper` 按该名检测域内程序集恒为 false,unitypackage / DLL 安装形态下已装 UniTask 的工程全局宏 `AESIR_MODULES_UNITASK` 反被误删、UniTask 分支与适配程序集静默失效零报错(UPM 安装形态宏由 versionDefines 管理,未受影响——多数工程未察觉的原因)。现 references 改按程序集名 `UniTask` 引用;检测改为白名单(`UniTask`——asmdef 源码 / unitypackage 形态;`Cysharp.Threading.Tasks`——NuGet 预编译 DLL);`AesirUniTaskDefineKeeperTests` 新增命名守卫 2 用例(白名单含真实程序集名 + 两处 asmdef 引用锁定),共 7 用例

Aesir Architecture 本版本无功能变更,随版本配套发布。

## [0.27.0] - 2026-09-27

---

### Aesir Architecture

**Added**

- **更新器单包更新入口** — 包列表每行新增「更新」按钮(IMGUI 与 Odin 窗口同步),另一已知包在场且落后时确认框前置「配套版本警告」,提示但不阻止
- **「全部更新」升级为"补全 + 更新"语义** — 目标扩展为"过期包 + 缺失的已知包补装",确认框逐包标注「更新 / 新安装」并前置缺包说明

**Fixed**

- **「全部更新」在 GitHub 直连不可用时卡死在下载进度条** — unitypackage 下载按「直连 → 镜像站代理(ghproxy.net / gh-proxy.com)」逐线路兜底,全部失败时异常附手动下载指引
- **更新进度条不可取消** — 下载阶段进度条可随时点「取消」中止,取消后温和收尾(区分已完成导入与未更新的包)
- **更新流程收尾异常导致程序集重载锁泄漏** — 收尾重构为配平守卫结构,任何异常路径恰好解锁一次;顺序改为「先解锁、再清忙碌标记」,不再存在死锁窗口
- **`AESIR_ARCHITECTURE` 宏确保器写入时机重入风险(预防性加固)** — 写宏推迟到 `EditorApplication.delayCall`,仅在符号缺失时写入
- **Tools/Aesir 组菜单排序随域重载抖动** — Getting Started 菜单优先级调整,稳定居 Tools/Odin 组之后并自动插独立分割线

**Changed**

- **移除 DDOL 关闭时的运行时 Warning 提醒日志** — 非 DDOL 提示完全由 Inspector 信息框承担
- **DDOL 开关字段前移至类声明首位** — 确立各单例类「DDOL 开关在最上」的统一排布
- **更新确认框文案重构** — 全部更新与单包更新分别构建确认文案;`UpdatePackagesAsync` 返回 `UpdateResult`(已完成包 / 是否取消 / 未更新包)

**Removed**

- **移除更新器更新前自动备份机制(`.aesir-backup/`)** — 全量复制数千文件对消费者 git 仓库构成无谓噪音;回滚走 GitHub Releases 旧版 unitypackage 重新导入(确认框已明示),`BackupRunestone` / `UpdateResult.BackupPath` 等 API 一并移除

---

### Aesir Modules

**Added**

- **Scene 模块 UniTask 适配(新程序集 `Runestone.AesirModules.UniTask`)** — 安装 UniTask 时内部流程自动改为 UniTask 驱动,新增可 await 的 `SceneModuleUniTask` API;宏 `AESIR_MODULES_UNITASK` 由 versionDefines + 编辑器宏维护器自动维护
- **UI 模块全局配置资产 `UIModuleConfigSO`(单例)** — 窗口蒙版模式等模块级配置迁出 `UIModule` 序列化字段,不再要求预放置;加载器注册 → Resources 兜底 → 内存默认实例三级解析,编辑器自动创建兜底资产
- **场景模块全局配置资产 `SceneModuleConfigSO`(单例)** — 承载全局启动场景兜底与加载进度归一化上限,设计对齐 `UIModuleConfigSO`
- **Script Doc Generator 静态 API(`ScriptDocGeneratorAPI`)** — 面板的无 UI 等价入口,供自动化脚本与 AI 直接调用(按类型/程序集/文件夹生成,返回 `ScriptDocGenerationResult`)

**Changed(含破坏性)**

- **`SceneModule` 公开 API 静态门面化(破坏性)** — 全部公开成员改为静态(直接 `SceneModule.LoadSceneSingle(...)`),实例侧全私有(守护用例锁定)
- **窗口蒙版模式配置迁移至 `UIModuleConfigSO`(破坏性)** — 移除 `UIModule` 的 `maskMode` 序列化字段,升级后以配置资产为准
- **加载进度上限配置迁移至 `SceneModuleConfigSO`** — 常量 0.9 改为配置资产字段,消费端钳制 (0, 1]
- **移除各模块 DDOL 关闭时的运行时 Warning 提醒日志;DDOL 开关字段统一前移至类声明首位**
- **Script Doc Generator「调试检查模式」重排至窗口最底部** — TypeData 中间结果列表位于开关下方,提示三态化

**Fixed**

- **Script Doc Generator 调试检查模式关闭时 TypeData 列表仍显示** — 根因是 Odin 对同一成员的多个 ShowIf 为 OR 语义,现合并为复合条件属性(AND)
- **Script Doc Generator 调试模式警告信息框表达式解析错误** — `$value` 误用,改为 `@成员名` 根实例上下文解析
- **Script Doc Generator 窗口 PropertyTree 未释放** — `OnDisable` 释放并置空,消除 GC 警告
- **Script Doc Generator 绘制回调内解析资产库单例导致卡顿与 "GUIStateObj is deleted" 报错** — 单例解析收敛到 `OnEnable` + 按域缓存

---

## [0.26.0] - 2026-09-25

---

### Aesir Architecture

**Added**

- **更新器检测线路可见化** — 检测结果新增线路模型(直连 GitHub / 镜像站 / CDN 中转):窗口显示「GitHub 直连是否可用(可用即版本信息 100% 实时)」与「最终获取线路」,新增「检测详情(各层尝试)」折叠区(含每层耗时与失败原因),结果来自 CDN 中转时额外给出延迟提示

**Changed**

- **更新器版本检测改为「直连 GitHub → 镜像站 → CDN 中转」三层兜底(修复新版本检测延迟)** — 此前 jsDelivr CDN 排在首位,其分支缓存最长约 12 小时,刚发布的版本在窗口里仍会显示为旧版本。现直连层依次尝试 Releases API、`releases/latest` 的 302 探测、仓库内 `update-info.json` 的直连 raw(单源超时 5 秒即落下一层),直连不可用才落镜像站(ghproxy.net / gh-proxy.com,代理 raw 内容、版本实时),最后才是 CDN 中转;只有 tag 的结果会按同 tag 校验补齐文件清单,拒绝陈旧清单避免错删文件

**Fixed**

- **更新/检测缺少超时,进度条可能长时间卡住** — 连接检测与 unitypackage 下载补齐硬性墙钟上限:单源检测 5 秒、整轮检测 30 秒(超时后不再发起新请求并留痕)、下载「总时长 120 秒 + 连续 30 秒无进展」双判据;任一超时都会中止请求并抛明确异常,上层必定收起进度条
- **两个包连续更新时流程可能中途断裂(进度条停留 + 按钮提前可点)** — 导入 unitypackage 带来的脚本变更会触发域重载,异步流程随旧域消失导致第二个包等不到、进度条停在上一包的导入文案上,而忙碌标志被重置又让按钮可点。现整段更新流程锁住程序集重载、只在全部收尾后解锁一次;导入期间先收起本工具进度条避免与 Unity 自带导入条互相覆盖;另加域重载兜底收尾
- **Odin 版更新器窗口正文被渲染成「禁用灰」** — Odin 对不可编辑属性会推入禁用绘制作用域,导致说明框、列表标签、行文本与状态行全部呈禁用态;现按 Odin 官方做法标注 `[EnableGUI]` 强制按可用状态绘制(不可编辑语义不变),实测文字亮度 128 → 196

---

### Aesir Modules

- 与 Aesir Architecture 同步发布 0.26.0(版本号对齐,本包无功能变更)

---

## [0.25.1] - 2026-09-25

---

### Aesir Modules

**Fixed**

- **场景测试套件把测试场景常驻 EditorBuildSettings(并被打进玩家构建)** — 原先经 `[InitializeOnLoadMethod]` 在编辑模式域加载期把两个测试场景登记为 enabled 条目且从不摘除,条目随 `ProjectSettings/EditorBuildSettings.asset` 落盘、进玩家构建;现改为 `IPrebuildSetup` 在进入 Play 前的编辑模式阶段登记、`IPostBuildCleanup` 退出 Play 后按名摘除,条目仅存在于本次运行期间,另有域加载兜底清扫回收被强杀遗留的条目。新增 EditMode 守护用例锁定「测试场景不得常驻 BuildSettings」
- **SceneModule 测试无法随包进入实际工程** — 测试原先硬依赖宿主工程存在 `Assets/Scenes/SampleScene.unity`(消费工程可能已删除它),缺失时 `FromScenePath` 直接抛异常;现由 SetUp 在缺失时从包内最小场景夹具临时复制、TearDown 按「谁创建谁删除」还原(含空目录)。测试资产路径不再写死 Assets 相对路径,改为按文件名经 AssetDatabase 定位(Assets 安装 / 嵌入式包 / UPM Git 安装自适应)

---

### Aesir Architecture

- 与 Aesir Modules 同步发布 0.25.1(版本号对齐,本包无功能变更)

---

## [0.25.0] - 2026-09-25

---

### Aesir Modules

**Fixed**

- **Script Doc Generator 增量重生成产出双 Front Matter** — Zensical 生成器自产 YAML 头后,增量合并逻辑会把旧文件的 Front Matter 再拼一份到新内容前,对已存在文档重生成必然产出双重头部;合并逻辑收敛为 `MergeFrontMatterWhenMissing`:新内容自带 Front Matter 时以新生成的为准,不自带(如中文 API 生成器)仍保留旧文件头部。新增 EditMode 回归测试 4 用例

---

### Aesir Architecture

- 与 Aesir Modules 同步发布 0.25.0(版本号对齐,本包无功能变更)

---

## [0.24.0] - 2026-09-25

---

### Aesir Architecture

**Added**

- **Aesir Getting Started 窗口** — 菜单 `Tools → Aesir → Getting Started`(priority -1000 居顶 + 独立分割线):概览页展示包卡片(含未安装包占位引导),包页按教学分组列出示例;整卡点击定位示例文件夹,带场景的示例经「打开场景」按钮直达(先保存当前场景一次再切换),结果经右下角 Toast 提示。数据层以各包 package.json samples 清单为唯一真源;IMGUI 兜底 + Odin 动效窗口经 `OdinWindowOpener` 委托路由
- **示例构建剔除钩子** — 构建时自动把 Build Settings 场景列表中的 Aesir 示例场景从本次构建剔除并输出 `[Aesir Build]` 日志(持久数据不动);「示例不进玩家构建」自此覆盖脚本与场景两条路径
- **安装位置锚点机制** — 包根 `AesirPathLookup.asset` 锚点(参照 Odin Inspector 同款资产),`AesirAssetPaths` 三级解析实际安装根——Runestone 可整体移动到项目任意文件夹,构建剔除 / 包更新器 / Getting Started 三个消费端全部跟随
- **示例脚本构建剔除守护测试** — 运行时示例程序集内每个 .cs 必须整文件 `#if UNITY_EDITOR` 包裹,漏包裹在 EditMode 测试失败

**Changed**

- 更新器 Odin 窗口标题区改手绘(移除灰暗 `[Title]`);Tools/Aesir 菜单按包分组(包专属项归入 `Architecture/`、`Modules/` 子菜单);Check for Updates 移至菜单最底部(1100 + 分割线);`QuickCreateSOMenuItem` 移入 `Editor/MenuItems/`;`AesirArchitecturePlayerLoop` / `AesirScheduler` 文件归位 `Runtime/Common/`

**Renamed(破坏性变更)**

- `ScriptingSymbolUtility` → `ScriptingSymbolEditorUtility`(Utilities 目录命名规范,外部脚本直接引用需同步更名)

---

### Aesir Modules

**Added**

- **UI 模块 Canvas 根窗口形态** — 与 Panel 并列的第二种 UI 形态:窗口预制体根节点自带 Canvas,挂 UIRoot 下(不经四层 Canvas),`sortingOrder` 默认 500 恒在面板四层之上;静态 API `UIModule.Open<T>()` / `Close<T>()` / `GetWindow<T>()` 等;预制体结构约定 `Mask`(蒙版) + `Content`(内容容器)
- **窗口蒙版遮罩机制** — `maskMode` 单遮(仅最高层可见窗口蒙版生效)/ 叠遮(各窗口独立),运行时可切换;蒙版点击经 `OnMaskClicked()` 虚方法默认按 `closeOnMaskClick` 关闭
- **Binder 窗口感知** — 基类下拉含 `AesirBaseWindow` 家族,根节点带 Canvas 时默认脚本名后缀 `Window`
- **示例 UI Basic Usage**(`Samples/UI/01_BasicUsage`,已登记 samples);窗口与蒙版 EditMode 测试 22 用例
- **缺依赖一键补装(`AesirDependencyInstaller`)** — unitypackage 形态下 Aesir Architecture 缺失时,菜单 `Tools → Aesir → Modules → Install Dependencies` 确认后经 UPM 自动补装;配套 package.json 依赖由不可解析的 semver 改为 Git URL 版本分支(UPM 安装时自动递归拉取);新增零引用 `Runestone.AesirModules.Editor.Bootstrap` 程序集

**Changed**

- Script Doc Generator / Scene Editor Settings 菜单归入 `Tools/Aesir/Modules/`;Odin / Addressables 细分程序集锚点由 `Common/` 迁至 `Integration/`(程序集名与引用零变化);示例 `KeyPressedEvent` 的 using 指令移入 `#if UNITY_EDITOR` 内

**Planned(下期候选)**

- SmartShowHide 伪隐藏(全屏窗口弹出时自动伪隐藏被遮挡面板、关闭后恢复)

---

## [0.23.0] - 2026-09-23

### Aesir Architecture

本批为全仓锐评修复与"保持极简"定位收敛,含破坏性变更(详见包内 CHANGELOG 的 [0.23.0] 段)。

- **Added**: `ObservableQueue<T>` 专属测试(8 用例,补齐四集合专属测试的最后缺口); AesirScheduler NaN 延时回归用例
- **Changed**: AesirScheduler NaN 延时语义与文档对齐(NaN 传播 = 永不触发); `ObservableList<T>.Move` 同索引零变化不通知; `MiniEvent` / `MiniEvent<T>` 的 AddListener 补 null 守卫; `ObservableQueue<T>` 结构补齐对齐其余三集合(sealed / `[Serializable]` / 结构体枚举器 / 构造 null 容忍); 根 README 失实宣称修正、测试数与示例计数更新、快速开始改版为最小五概念快车道
- **Removed(破坏性变更)**: `ObservableHashSet<T>` 集合代数全套 10 方法(`IObservableHashSet<T>` 不再继承 `ISet<T>`,需要时用内部 `HashSet<T>` 或上游 Cysharp.ObservableCollections); `ObservableList<T>` 区间 Sort / Reverse 重载; ReadOnlySpan 批量重载(保留 `T[]` 与 `IEnumerable<T>` 双轨); Dictionary / HashSet 构造器收敛至「默认 / 初始元素 / 比较器」三个; `ObservableValue<T>.SetValue` 别名; 调试 / 测试专用面收窄 internal(`IContext` 与 `IGenericLocator<T>` 各删 4 个接口成员、`MiniEvent.GetListeners`、`AesirArchitecturePlayerLoop.Reset` 等)
- **Renamed(破坏性变更)**: `ObservableValue<T>.Clear()` → `ClearListeners()`——命名对齐集合家族语义

### Aesir Modules

- **Added**: Binder 代码生成器同类型多组件测试 ×2(按出现序号取 `GetComponents<T>()[n]`); SceneModule 批量卸载重入 PlayMode 回归
- **Fixed**: Binder 三处 P1(Missing 脚本组件空引用 / 增量模式命名空间错位致自动挂载静默失效 / 同类型多组件错绑)+ partial 模式重生成幂等; SceneModule 批量卸载重入洞(嵌套 UnloadAllAddedScenes 截断外层快照); UIModule / AudioModule / EventModule 重复实例销毁粒度统一 `Destroy(this)`; `PrewarmPanel` 补键语义守卫; 三个测试 asmdef 补 `ODIN_INSPECTOR` 装配守卫; SDG 缩进正则修正与 SourceScanner 显式接口实现文档键错配修复(fail-closed 告警)
- **Changed**: 更新器双窗口编排上提共享控制器 `AesirUpdateController`(消除 ~200 行双真源); `ui-module.md` 补 Binder 两条边界声明(仅编辑期构建 / 生成产物使用 Odin 特性)

## [0.22.0] - 2026-09-22

### Aesir Architecture

- **可观察集合升级为 ObservableCollections 轻量内置子集** —— 新增 `ObservableQueue<T>`,四种集合统一单轨变更通知 `AddListener` / `RemoveListener`(`MiniEvent<T>` 承载,返回 `AutoRemoveListenerHandle`,可绑定 Unity 生命周期自动移除):无变更的写操作不通知、批量操作逐项通知、字典值更新以 Replace 表达(旧值在 OldItem)、Move 单事件、Sort / Reverse / Clear 统一 Reset;Odin Inspector 内联调试面板(可选);与上游 Cysharp 库可在同一项目共存(程序集/包名/命名空间三层隔离)
- **Removed(破坏性变更)** —— 轻量事件 API 全套(`AddXxxListener` 与四个事件参数类型)、原生 `CollectionChanged` 事件与 `SortOperation<T>` 移除,语义并入单轨事件(迁移:改订阅 `AddListener`,按 `e.Action` 分流);移除内部加锁与 `SyncRoot`(集合边界统一为仅主线程使用)
- 测试改写为单轨断言(含句柄绑定 GameObject OnDisable 集成用例),RAA Editor EditMode 186 用例全绿

### Aesir Modules

- 与 Aesir Architecture 0.22.0 版本同步发布,本包无功能变更

## [0.21.0] - 2026-09-14

### Aesir Architecture

- **包内更新器全面升级**——新增 Odin Inspector 界面(与 IMGUI 兜底共用逻辑)、更新日志面板(按远程 tag 拉取包内 CHANGELOG 展示本地→远程区间段落)与更新前确认框;修复预发布版本比较(rc 与正式版判等)、移除单包更新入口(防版本撕裂)、残留清理移到导入成功之后
- **新增 `AesirScheduler` 帧粒度时间调度原语**——`Delay(seconds, callback)` / `NextFrame(callback)` 纯 C# 静态 API,经 PlayerLoop BeforeUpdate 钩子结算,为无协程能力的 Model / Service / Command 提供合法延时手段;有意收窄(帧粒度/游戏时间/一次性任务/不池化)
- package.json samples 登记 `RuntimeInitializeLoadType` 示例(共 11 个可导入示例)
- 修复 DDOL 根物体保护(预放置为子物体时跟随宿主)、脏排序只重排脏列表、QuickCreateSO 空资源名
- 测试扩充:View/触发器族、工具类、更新器 19→32、MiniEvent RemoveListener;PlayMode 测试卫生(断言拆分/卸载等待/全量 Warning 捕获/真实时间窗)

### Aesir Modules

- **事件模块三缺陷修复(全仓最严重单点)**——重入分发(回调内再发布事件)不再覆写共享参数数组;分发改注册表快照迭代(回调内退订/注册不干扰本趟);优先级稳定排序(同档按注册顺序);摘除"实验性"标注,文档改写快照与重入安全语义、零分配口径收敛
- **音频模块修复**——补 `ResetStatics` 静态重置(RAM 唯一漏掉的单例铁律)、`PlayBgm` 淡出中重播同曲取消淡出续接(幂等误伤)、`PlaySfx` 音调钳制 [0.01, 3] 不再反播;示例音量滑条改"拖动结束落键"
- **UI 模块**——`ShowPanel`/`PrewarmPanel` 注册时序前移(OnShow 抛异常不泄漏、递归 Show 不重复实例化);re-show 强转改 `as` 判空、`InstantiateInactive` try/finally 恢复源预制体、`RegisterPrefab` 换路径诊断警告
- **场景模块**——`UnloadAllAddedScenes` 快照迭代(广播期间嵌套加载/卸载不干扰本趟)、Single 成功路径 `SetActiveScene` 前 `IsValid` 校验;**新增 RAM 首个 PlayMode 测试套件**(真实加载成功路径 4 用例,`Tests/Runtime/`)
- **ScriptDocGenerator**——XML 实体解码(泛型实体不再双重转义)、多成员代码块归属分析(fail-closed 跳过告警)、Default 生成器与 Zensical 收敛共享 `MemberGrouper` 引擎(582→343 行)、杂项六项修复
- 测试扩充:EventModuleTests 22→32、AudioModuleTests 30→38、UIModuleTests 13→17、XmlSummaryToolTests 25→34、新增 Zensical 输出 7 用例

## [0.20.0] - 2026-09-11

### Aesir Architecture

- 新增《设计变更记录》文档——废弃机制(事件总线/ModelReplaced/120 帧轮询/初始化失败回滚/异常吞噬等十组)与设计来源统一收录,源码注释此后只描述当前行为
- 注释精简(12 文件):移除源码注释中的历史演进叙述(更名史/fake-null 演进史/复刻来源等),重复 remarks 去重
- 修复 `AesirArchitecture.DontDestroyOnLoad` 遗留 CS0108 编译警告(补 `new` 修饰符,行为不变)

### Aesir Modules

- **事件模块分发增强与 SO 资产化**——订阅者过滤器(`ISubscriberFilter` + `WithTag`/`WithPriority`/`SameSceneAsEmitter`/`OnlySelf`/`InsideCollider2D`,fail-closed);死引用清理(分发期自动移除已销毁订阅者);性能监控(`executionMsLimit`,默认关闭);`AesirEventArgsSO` 资产发布者 + `UnityEventOnAesirEvent` 桥接组件 + `SubclassSelector` 子类下拉;热路径绑定键缓存(分发热路径稳态零分配,编译委托加速 ~78 倍);新增 22 用例与 `02_Filters`/`03_SOAsset` 示例
- **新增音频模块(2D)**——`AudioModule` 全静态门面:SFX 独占音源轮询(每播音调/音量独立,无每播实例化开销)、BGM 淡入淡出与同曲幂等、Master/BGM/SFX 三通道音量与静音 PlayerPrefs 持久化;30 用例与 `01_BasicUsage` 示例
- **场景模块行为层补齐**——`SceneModule` 补 DDOL 字段(修复预放置实例被自己的 `LoadSceneSingle` 销毁)、新增 `SetActiveScene` 与场景事件广播、`onProgress` 进度回调、`SceneAssetWrapper` 悬空判定;20 用例与专属文档
- **UI 模块注册表重构(含破坏性变更)**——三字典合并单注册表(键=实际类型,基类类型调用 ShowPanel 报错拒绝/HidePanel/GetPanel 警告)、层 Canvas 缺失 fail-fast 中止、`HidePanel<T>` 约束收紧为 `MonoBehaviour, IUIPanel`;移除 `UIModule.RegisterUIRoot` 与 `IUIAssetLoader.Unload`(破坏性);13 用例与专属文档
- **ScriptDocGenerator 修复与增强**——生成器三处输出 bug 修复(单成员类丢章节/常量表过滤写反/空继承章节)、Zensical 生成器参数与备注全链路输出、面板配置域重载不再丢失、默认输出目录移出 Assets、UI Toolkit 窗口移除(Odin 窗口为唯一入口)、Summary 工具改为 `[Summary]` 特性优先语义
- 修复 `AesirListenerAttribute` 缺 `AllowMultiple`、`SubscriberPriority` 文档口径修正(实为 4 档 First/High/Medium/Last)

## [0.19.0] - 2026-09-11

### Aesir Architecture

- 新增 `IContext` / `AbstractContext<T>` 的 `UnregisterModel<TModel>` / `UnregisterService<TService>`——按类型键摘除注册并释放实例(幂等,注销后再注册追加到顺序末尾)
- 新增 `AesirArchitecture.DontDestroyOnLoad` 只读属性——暴露 DDOL 决策取值,供运行时查询与编辑器条件提示复用
- 修复 Odin AttributeProcessor 两处信息框宣称与实现不符(类级条件 Warning 补齐/DDOL 警告改条件显示);`AbstractSubmodule.Dispose` 重置 `Initialized`;快捷档示例 Model 改只读属性暴露、严格档示例缓存 Query 实例复用

### Aesir Modules

- 版本号与 Aesir Architecture 同步更新至 `0.19.0`,本包本版本无功能性变更

## [0.18.0] - 2026-09-10

### Aesir Architecture

- `AesirArchitecturePlayerLoop.Register` 现返回 `AutoRemoveListenerHandle`——Dispose 时自动注销本次注册,对齐全框架句柄风格;忽略返回值的既有调用不受影响
- 新增 `CapabilityExtensionsTests`(10 用例)——CQRS 执行链首次获得测试覆盖:带参/无参命令与查询、命令链、查询组合、`IController<T>` 默认接口实现绑定、两阶段初始化异常语义、Dispose 后单例重建
- 修复 **Model 初始化阶段获取 Service 的误导性报错**——明确「先全部 Model、后全部 Service」两阶段初始化下 Model 阶段无法获取 Service(与注册顺序无关),须延迟到运行期方法调用
- 修复 `AbstractContext<T>.Dispose` 后的**僵尸单例**——释放后解除 `Instance` 单例缓存,再次访问重建并重新初始化全新上下文,而非返回容器已清空的空壳
- 修正三处 XML 文档失实:`AesirArchitecture` 组件职责(实为 DDOL 宿主,不初始化架构数据)、`AesirArchitecturePlayerLoop` 已废弃的"周期性检测"宣称、`MiniEvent`"零分配"措辞(仅 Invoke 路径零分配)
- 解除 Editor 工具对测试框架的结构绑定:Editor 主程序集移除 `UNITY_INCLUDE_TESTS` defineConstraint、package.json 移除 test-framework 硬依赖;PlayMode 测试程序集以 `ODIN_INSPECTOR` 守卫(无 Odin 环境自动排除)
- `RegisterCustomLifecycle(mono / GameObject, evt, callback)` 现将监听绑定到所在物体销毁事件自动移除(行为变更,原先不自动移除)
- 重复实例去重改用 `Destroy(this)` 不再连带销毁业务物体;私有 `Reset` 更名 `ClearState` 避免撞名 Unity 魔法方法;`AbstractQuery` 补 `[Serializable]`

### Aesir Modules

- **ScriptDocGenerator 模块(需 Odin)**——原 `Assets/ScriptDocGenerator` 独立工具整合为包内功能模块:反射分析 C# 类型生成结构化 API 文档(增量保留手写内容),附 Summary 工具(XML `<summary>` ↔ `[Summary]` 双向同步);153 个单元测试汇入测试程序集;入口 `Tools → Aesir → Script Doc Generator`

## [0.17.0] - 2026-09-06

### Aesir Architecture

- 新增 `InternalContextAttribute` —— 标记框架内部 Context(示例 / 测试用途);Aesir Modules Binder 的「Context 类型」选择器自动跳过被标记的类型
- 修复**示例场景无法运行**(0.14.0 起回归):示例程序集改为运行时程序集 + 示例脚本整文件 `#if UNITY_EDITOR` 包裹 —— 编辑器内可编译、可挂载、可 Play,玩家构建整体剔除(示例类型 0 入包)

### Aesir Modules

- **Binder 组件绑定全面完善** —— 双生成模式(「同一脚本增量」默认 /「Partial 分部类」可选,默认 `.designer.cs` 后缀);基类下拉新增 `AesirBasePanelView<T>` / `AesirBasePanelViewController<T>` 预选;层级右键菜单快捷挂载 `BinderAssistant` / `BinderTag`;命名空间默认值与后缀候选持久化;新增 69 个 EditMode 测试
- 修复 Binder 生成脚本接口不匹配、Partial 模式覆盖手写文件、绑定校验空引用等问题
- 同步修复示例场景回归(同 Architecture 机制)

## [0.16.x] - 2026-09-06

- `LICENSE.md` 与 `Third Party Notices.md` 移至包根,对齐 UPM 包根约定
- Third Party Notices 收录设计参考条目:Cysharp/ObservableCollections(Architecture)、Eflatun.SceneReference(Modules)

## [0.16.0] - 2026-09-06(Modules 主要变更)

- `SceneAssetWrapper` 功能增强(吸收 Eflatun.SceneReference):GUID 锚点自愈、`State` / `UnsafeReason` 状态机、`TryGet` 安全读取家族、工厂方法
- Addressables 条件架构:未安装时相关代码整体不编译、零报错
- **破坏性变更**:删除 `AddScene` / `UnloadAddedScene` 统一为 `LoadSceneAdditive` 纯叠加追踪;`ReloadScene` 同步改异步;`SceneAssetWrapper` 空引用语义收紧(抛 `EmptySceneAssetWrapperException`);加载失败全系新增 `onFailed` 回调
- 目录调整为标准 Unity 自定义包根结构(`Runtime/` / `Editor/` 两级,模块以子目录存在,模块间零依赖)

## [0.15.0] - 2026-09-05

- 新增可观察集合 `ObservableHashSet<T>`;新增 RuntimeInitializeLoadType 示例
- 包内更新器大陆优化:jsDelivr 多域名 → GitHub API → 302 重定向探测三级兜底
- Modules 无功能性变更(版本同步)

## [0.14.0] - 2026-09-05

- **AesirFramework 转型**:AesirInspector 迁出为独立仓库;本仓库由 Aesir Architecture 与 Aesir Modules 组成
- Samples / Documentation 双目录结构(`Samples/` 编写主位 + `Samples~/` 发布镜像)
- 新增 PlaneWar 实战示例(Mono 版)

## 更早版本

0.13.0 及更早的完整变更(含 ObservableList / ObservableDictionary、DDOL 重设计、MVP 示例家族、Query 系统等里程碑)请查阅[根 CHANGELOG](https://github.com/yuumixcode/AesirFramework/blob/main/CHANGELOG.md)与各子包内 `CHANGELOG.md`。
