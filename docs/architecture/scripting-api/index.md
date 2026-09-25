---
title: Scripting API
description: "Runestone.AesirArchitecture 系列命名空间的 Scripting API 参考"
---

# Scripting API

本参考由 Script Doc Generator 基于 C# 反射离线生成，重新生成时自动保留各页面 `## Additional Notes` 之后的手写补充。页面按字母序排列；使用左侧目录或站内搜索定位类型。

## Runestone.AesirArchitecture

命名空间 `Runestone.AesirArchitecture` · 程序集 `Runestone.AesirArchitecture` · 共 85 个类型。

### 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AbstractCommand`](<Runestone/AesirArchitecture/AbstractCommand.md>) | 命令基类。持有上下文引用，通过 OnExecute 执行命令逻辑。 |
| [`AbstractContext<T>`](<Runestone/AesirArchitecture/AbstractContext{T}.md>) | 上下文基类。纯 C# 实现，不依赖 MonoBehaviour。 子类在 Configure 中注册 Model 和 Service，通过 Instance 获取全局单例。 |
| [`AbstractModel`](<Runestone/AesirArchitecture/AbstractModel.md>) | Model 基类。继承 AbstractSubmodule 获得生命周期管理，实现 IModel 标记数据层角色。 |
| [`AbstractQuery<TResult>`](<Runestone/AesirArchitecture/AbstractQuery{TResult}.md>) | 查询基类。持有上下文引用，通过 OnExecute 执行查询逻辑并返回结果。 |
| [`AbstractService`](<Runestone/AesirArchitecture/AbstractService.md>) | Service 基类。继承 AbstractSubmodule 获得生命周期管理，实现 IService 标记服务层角色。 |
| [`AbstractSubmodule`](<Runestone/AesirArchitecture/AbstractSubmodule.md>) | 子模块基类。持有上下文引用，通过 OnInitialize 和 OnDispose 管理生命周期。 Model 和 Service 的公共逻辑统一在此实现。 |
| [`AesirArchitecture`](<Runestone/AesirArchitecture/AesirArchitecture.md>) | Aesir Architecture 接入 MonoBehaviour 生命周期的持久化物体对象。 |
| [`AesirArchitectureDebug`](<Runestone/AesirArchitecture/AesirArchitectureDebug.md>) | AesirArchitecture 内部日志工具。 所有架构模块的日志输出应走此工具，以醒目的颜色和 [AesirArchitecture] 标识区分来源。 Log/Warni… |
| [`AesirArchitecturePlayerLoop`](<Runestone/AesirArchitecture/AesirArchitecturePlayerLoop.md>) | 基于 PlayerLoop 的生命周期钩子系统，无需 MonoBehaviour 即可接入游戏级帧回调。 通过 Register 注册回调，order 越小越先执行；系统自动在… |
| [`AesirMonoBehaviour`](<Runestone/AesirArchitecture/AesirMonoBehaviour.md>) | RAA 架构标准 MonoBehaviour 基类，根据运行环境自动选择序列化方式。 |
| [`AesirScheduler`](<Runestone/AesirArchitecture/AesirScheduler.md>) | 帧粒度时间调度器 —— 纯 C# 静态 API，为无协程能力的 Model / Service / Command 提供合法的延时执行手段。 |
| [`AesirScriptableObject`](<Runestone/AesirArchitecture/AesirScriptableObject.md>) | RAA 架构标准 ScriptableObject 基类，根据运行环境自动选择序列化方式。 |
| [`AesirView<T>`](<Runestone/AesirArchitecture/AesirView{T}.md>) | View 基类。通过泛型上下文获取模块访问能力，仅具备只读权限，AesirView 自动支持 Odin Inspector 序列化。 |
| [`AesirViewController<T>`](<Runestone/AesirArchitecture/AesirViewController{T}.md>) | View + Controller 双角色基类。通过泛型上下文获取模块访问能力，自动支持 Odin Inspector 序列化。 |
| [`CapabilityExtensions`](<Runestone/AesirArchitecture/CapabilityExtensions.md>) | 能力扩展方法集合 |
| [`GenericLocator<T>`](<Runestone/AesirArchitecture/GenericLocator{T}.md>) | 泛型对象定位器。按类型注册、查询与获取以 T 为基类的对象实例。 |
| [`InternalContextAttribute`](<Runestone/AesirArchitecture/InternalContextAttribute.md>) | 标记一个 AbstractContext{T} 派生类为框架内部 Context（示例 / 测试等非用户工作流用途）。 被标记的 Context 不会出现在用户工作流的 Con… |
| [`MiniEvent`](<Runestone/AesirArchitecture/MiniEvent.md>) | 单参事件 |
| [`MiniEvent<T>`](<Runestone/AesirArchitecture/MiniEvent{T}.md>) | 单参事件 |
| [`MonoLifecycleProxy`](<Runestone/AesirArchitecture/MonoLifecycleProxy.md>) | Mono 生命周期事件代理。作为全局单例挂载在 [Aesir Architecture] GameObject 上， 将 Unity 原生生命周期回调和自定义 PlayerLo… |
| [`MonoLifecycleProxyExtensions`](<Runestone/AesirArchitecture/MonoLifecycleProxyExtensions.md>) | Mono 生命周期事件扩展方法集合。 |
| [`MonoView<T>`](<Runestone/AesirArchitecture/MonoView{T}.md>) | View 基类。通过泛型上下文获取模块访问能力，仅具备只读权限。 |
| [`MonoViewController<T>`](<Runestone/AesirArchitecture/MonoViewController{T}.md>) | View + Controller 双角色基类。通过泛型上下文获取模块访问能力，无 Odin 依赖。 |
| [`ObservableDictionary<TKey, TValue>`](<Runestone/AesirArchitecture/ObservableDictionary{TKey, TValue}.md>) | 可观察字典实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`ObservableHashSet<T>`](<Runestone/AesirArchitecture/ObservableHashSet{T}.md>) | 可观察集合实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`ObservableList<T>`](<Runestone/AesirArchitecture/ObservableList{T}.md>) | 可观察列表实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。 |
| [`ObservableQueue<T>`](<Runestone/AesirArchitecture/ObservableQueue{T}.md>) | 可观察队列实现。 |
| [`ObservableValue<T>`](<Runestone/AesirArchitecture/ObservableValue{T}.md>) | 可观察属性实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableValue{T} 只读订阅。 |
| [`PlayerLoopUtility`](<Runestone/AesirArchitecture/PlayerLoopUtility.md>) | PlayerLoop 操作的静态工具类，提供子系统的插入、查询与描述功能。 供框架内部和外部用户扩展 PlayerLoop，不局限于 AesirArchitectureLife… |
| [`RemoveListenerExtensions`](<Runestone/AesirArchitecture/RemoveListenerExtensions.md>) | 事件监听器自动移除扩展方法类，用于绑定移除操作到 Unity 生命周期 |
| [`RemoveListenerHandleCollection`](<Runestone/AesirArchitecture/RemoveListenerHandleCollection.md>) | 监听句柄集合。管理 AutoRemoveListenerHandle 句柄的添加与批量移除， 供 RemoveListenerTrigger 和 RemoveListenerO… |
| [`RemoveListenerOnDestroyTrigger`](<Runestone/AesirArchitecture/RemoveListenerOnDestroyTrigger.md>) | 在所属 GameObject 销毁时自动移除所有监听。 |
| [`RemoveListenerOnDisableTrigger`](<Runestone/AesirArchitecture/RemoveListenerOnDisableTrigger.md>) | GameObject 禁用时自动移除所有监听。挂载此组件后，当 GameObject 被禁用时将执行批量移除操作。 |
| [`RemoveListenerOnSceneUnloadedTrigger`](<Runestone/AesirArchitecture/RemoveListenerOnSceneUnloadedTrigger.md>) | 任意场景卸载时自动移除该场景注册的监听。按场景句柄（handle）分桶， 场景 A 卸载不会误杀场景 B 的监听。 挂载在 [Aesir Architecture] GameO… |
| [`RemoveListenerTrigger`](<Runestone/AesirArchitecture/RemoveListenerTrigger.md>) | 自动移除监听调用器基类。维护监听句柄列表，子类在特定生命周期事件中调用 RemoveAllListeners 批量移除。 |
| [`ResetStaticsAssistant`](<Runestone/AesirArchitecture/ResetStaticsAssistant.md>) | 静态变量重置助手（仅泛型类使用）。用于运行时阶段自动重置泛型类中的静态变量，兼容 Disable Domain Reload。 关闭 Domain Reload 时静态回调列表… |

</div>

### 结构体

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirArchitecturePlayerLoop.AesirArchitectureScriptRunAfterUpdate`](<Runestone/AesirArchitecture/AesirArchitecturePlayerLoop.AesirArchitectureScriptRunAfterUpdate.md>) | PlayerLoop 子系统 type 标识，在 PostLateUpdate 之后执行 |
| [`AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate`](<Runestone/AesirArchitecture/AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate.md>) | PlayerLoop 子系统 type 标识，在 Update 之前执行 |
| [`AesirArchitecturePlayerLoop.HookEntry`](<Runestone/AesirArchitecture/AesirArchitecturePlayerLoop.HookEntry.md>) | 回调条目，记录单个生命周期回调及其排序信息 |
| [`AesirScheduler.ScheduledTask`](<Runestone/AesirArchitecture/AesirScheduler.ScheduledTask.md>) | 待结算任务 |
| [`AutoRemoveListenerHandle`](<Runestone/AesirArchitecture/AutoRemoveListenerHandle.md>) | 自动移除监听句柄。包装注销回调。 |
| [`CollectionChangedEventArgs<T>`](<Runestone/AesirArchitecture/CollectionChangedEventArgs{T}.md>) | 集合变更事件参数。每次变更携带单个变更项；批量操作（AddRange / RemoveRange 等）由集合逐项触发事件。 |
| [`MonoLifecycleProxy.ListenerEntry`](<Runestone/AesirArchitecture/MonoLifecycleProxy.ListenerEntry.md>) | 监听条目，记录单个回调及其排序信息 |
| [`MonoLifecycleProxy.PendingChange`](<Runestone/AesirArchitecture/MonoLifecycleProxy.PendingChange.md>) | 挂起变更条目，记录调用期间累积的一次监听增删操作 |
| [`ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>`](<Runestone/AesirArchitecture/ObservableDictionary{TKey, TValue}.Enumerator{TKey, TValue}.md>) | 可观察字典实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`ObservableHashSet<T>.Enumerator<T>`](<Runestone/AesirArchitecture/ObservableHashSet{T}.Enumerator{T}.md>) | 可观察集合实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`ObservableList<T>.Enumerator<T>`](<Runestone/AesirArchitecture/ObservableList{T}.Enumerator{T}.md>) | 可观察列表实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。 |
| [`ObservableQueue<T>.Enumerator<T>`](<Runestone/AesirArchitecture/ObservableQueue{T}.Enumerator{T}.md>) | 可观察队列实现。 |

</div>

### 接口

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ICanExecuteCommand`](<Runestone/AesirArchitecture/ICanExecuteCommand.md>) | 执行命令的能力接口 |
| [`ICanExecuteQuery`](<Runestone/AesirArchitecture/ICanExecuteQuery.md>) | 执行查询的能力接口 |
| [`ICanGetModel`](<Runestone/AesirArchitecture/ICanGetModel.md>) | 获取 Model 的能力接口 |
| [`ICanGetService`](<Runestone/AesirArchitecture/ICanGetService.md>) | 获取 Service 的能力接口 |
| [`ICanInitialize`](<Runestone/AesirArchitecture/ICanInitialize.md>) | 可初始化接口。提供初始化与初始化状态标记。 被 IModel 和 IService 继承。 |
| [`ICanSetContext`](<Runestone/AesirArchitecture/ICanSetContext.md>) | 可设置上下文引用接口 |
| [`ICommand`](<Runestone/AesirArchitecture/ICommand.md>) | 同步命令接口。通过 Command 修改 Model 状态，只写无返回值。 能力：GetModel, GetService, ExecuteCommand |
| [`IContext`](<Runestone/AesirArchitecture/IContext.md>) | 模块上下文接口。提供模块注册与获取。 |
| [`IContextHolder`](<Runestone/AesirArchitecture/IContextHolder.md>) | 上下文持有者接口。 |
| [`IController`](<Runestone/AesirArchitecture/IController.md>) | 泛型控制器接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IController<T>`](<Runestone/AesirArchitecture/IController{T}.md>) | 泛型控制器接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`ICustomAfterUpdate`](<Runestone/AesirArchitecture/ICustomAfterUpdate.md>) | 自定义 AfterUpdate 生命周期。对应 AfterUpdate。 |
| [`ICustomBeforeUpdate`](<Runestone/AesirArchitecture/ICustomBeforeUpdate.md>) | 自定义 BeforeUpdate 生命周期。对应 BeforeUpdate。 |
| [`ICustomFixedUpdate`](<Runestone/AesirArchitecture/ICustomFixedUpdate.md>) | 自定义 FixedUpdate 生命周期。对应 FixedUpdate。 |
| [`ICustomLateUpdate`](<Runestone/AesirArchitecture/ICustomLateUpdate.md>) | 自定义 LateUpdate 生命周期。对应 LateUpdate。 |
| [`ICustomOnApplicationFocus`](<Runestone/AesirArchitecture/ICustomOnApplicationFocus.md>) | 自定义 OnApplicationFocus 生命周期。对应 OnApplicationFocus。 |
| [`ICustomOnApplicationPause`](<Runestone/AesirArchitecture/ICustomOnApplicationPause.md>) | 自定义 OnApplicationPause 生命周期。对应 OnApplicationPause。 |
| [`ICustomOnApplicationQuit`](<Runestone/AesirArchitecture/ICustomOnApplicationQuit.md>) | 自定义 OnApplicationQuit 生命周期。对应 OnApplicationQuit。 |
| [`ICustomUpdate`](<Runestone/AesirArchitecture/ICustomUpdate.md>) | 自定义 Update 生命周期。对应 Update。 |
| [`IGenericLocator<T>`](<Runestone/AesirArchitecture/IGenericLocator{T}.md>) | 泛型定位器接口。提供按类型注册、查询与获取对象实例的契约。 |
| [`IModel`](<Runestone/AesirArchitecture/IModel.md>) | 数据层接口。持有状态（通常使用 ObservableValue{T}）。 能力：GetModel, Initialize, Dispose |
| [`IObservableCollection<T>`](<Runestone/AesirArchitecture/IObservableCollection{T}.md>) | 可观察集合契约：单一变更事件的订阅与退订。 |
| [`IObservableDictionary<TKey, TValue>`](<Runestone/AesirArchitecture/IObservableDictionary{TKey, TValue}.md>) | 完整可观察字典接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`IObservableHashSet<T>`](<Runestone/AesirArchitecture/IObservableHashSet{T}.md>) | 完整可观察集合接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`IObservableList<T>`](<Runestone/AesirArchitecture/IObservableList{T}.md>) | 完整可观察列表接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableList{T} 只读订阅。 |
| [`IObservableValue<T>`](<Runestone/AesirArchitecture/IObservableValue{T}.md>) | 完整可观察属性接口。 Presenter 层通过此接口读写数据。 |
| [`IPresenter`](<Runestone/AesirArchitecture/IPresenter.md>) | 泛型 MVP 中介接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IPresenter<T>`](<Runestone/AesirArchitecture/IPresenter{T}.md>) | 泛型 MVP 中介接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IQuery<TResult>`](<Runestone/AesirArchitecture/IQuery{TResult}.md>) | 查询接口。通过 Query 执行读操作并返回结果，无副作用。 与 ICommand 的区别：Command 负责写操作（无返回值），Query 负责读操作（返回 TResult）。 |
| [`IReadOnlyObservableDictionary<TKey, TValue>`](<Runestone/AesirArchitecture/IReadOnlyObservableDictionary{TKey, TValue}.md>) | 只读可观察字典接口。 View 层通过此接口读取键值并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableHashSet<T>`](<Runestone/AesirArchitecture/IReadOnlyObservableHashSet{T}.md>) | 只读可观察集合接口。 View 层通过此接口读取元素并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableList<T>`](<Runestone/AesirArchitecture/IReadOnlyObservableList{T}.md>) | 只读可观察列表接口。 View 层通过此接口枚举元素并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableValue<T>`](<Runestone/AesirArchitecture/IReadOnlyObservableValue{T}.md>) | 只读可观察属性接口。 View 层通过此接口添加监听，不能修改值。 |
| [`IService`](<Runestone/AesirArchitecture/IService.md>) | 服务层接口。万能协调层，封装跨模块业务逻辑，协调模块间交互与通信。 Service 能读写 Model、调用其他 Service，完成跨模块协调。 不包含 ICanExecut… |
| [`IView`](<Runestone/AesirArchitecture/IView.md>) | 表现层接口。View 层通过此接口与模块上下文交互。 能力：GetModel, GetService |

</div>

### 枚举

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirArchitectureLifecyclePhase`](<Runestone/AesirArchitecture/AesirArchitectureLifecyclePhase.md>) | 游戏级生命周期阶段，对应 PlayerLoop 子系统插入点 |
| [`MonoLifecycleEvent`](<Runestone/AesirArchitecture/MonoLifecycleEvent.md>) | Mono 生命周期事件类型，涵盖 Unity 原生生命周期回调和自定义 PlayerLoop 阶段。 |

</div>

## Runestone.AesirArchitecture.Editor

命名空间 `Runestone.AesirArchitecture.Editor` · 程序集 `Runestone.AesirArchitecture.Editor`、`Runestone.AesirArchitecture.Editor.OdinInspector` · 共 38 个类型。

### 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirAssetPaths`](<Runestone/AesirArchitecture/Editor/AesirAssetPaths.md>) | Aesir 本地安装路径定位器 — 解析 Assets 形态安装（复制 / unitypackage 导入）的 Runestone 安装根目录，确保 Runestone 可移动… |
| [`AesirGetStartedService`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.md>) | Aesir Getting Started 服务 — 两版 Getting Started 窗口（IMGUI 兜底 / Odin 版）共用的无状态数据层： 扫描本机安装的 Ae… |
| [`AesirGetStartedService.AesirKnownPackage`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.AesirKnownPackage.md>) | 框架已知包（概览页按此补全「未安装」占位卡片；新增公开包时在此登记）。 |
| [`AesirGetStartedService.AesirPackageInfo`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.AesirPackageInfo.md>) | 已安装的 Aesir 包信息（扫描产物）。 |
| [`AesirGetStartedService.AesirSampleInfo`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.AesirSampleInfo.md>) | 单个示例信息（元数据来自 package.json samples 清单，路径经扫描解析）。 |
| [`AesirGetStartedService.PackageJsonMeta`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.PackageJsonMeta.md>) | package.json 反序列化载体（仅取 Getting Started 所需字段）。 |
| [`AesirGetStartedService.SampleGroup`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.SampleGroup.md>) | 教学分组（示例卡片页的分组小节，组内保持 package.json 声明顺序）。 |
| [`AesirGetStartedService.SampleJsonMeta`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.SampleJsonMeta.md>) | package.json samples 清单项。 |
| [`AesirGetStartedWindow`](<Runestone/AesirArchitecture/Editor/AesirGetStartedWindow.md>) | Aesir Getting Started 窗口（IMGUI 兜底版）— 框架示例导航：列出本机安装的 Aesir 包及其示例， 按教学分组展示，一键打开示例场景或定位示例目录… |
| [`AesirGetStartedWindowOdin`](<Runestone/AesirArchitecture/Editor/AesirGetStartedWindowOdin.md>) | Aesir Getting Started 窗口（Odin Inspector 版）— 框架示例导航主入口：概览页以包卡片展示本机安装的 Aesir 包（未安装的已知包显示占位… |
| [`AesirGetStartedWindowOdin.GetStartedPage`](<Runestone/AesirArchitecture/Editor/AesirGetStartedWindowOdin.GetStartedPage.md>) | Getting Started 页面基类（照 Odin GettingStartedPage：标题栏 / footer / 页面栈进出 / 滚动页包装）。 |
| [`AesirGetStartedWindowOdin.PackageCard`](<Runestone/AesirArchitecture/Editor/AesirGetStartedWindowOdin.PackageCard.md>) | 概览卡片视图模型（扫描时重建；显示文本预计算，OnGUI 零拼接）。 |
| [`AesirGetStartedWindowOdin.PackagePage`](<Runestone/AesirArchitecture/Editor/AesirGetStartedWindowOdin.PackagePage.md>) | 包示例页：按教学分组列出示例卡片，点击卡片打开示例场景。 |
| [`AesirPathLookup`](<Runestone/AesirArchitecture/Editor/AesirPathLookup.md>) | Aesir 安装位置锚点资产 — 空壳标记资产，每包包根各放一份（AesirPathLookup.asset）。 机制参照 Odin Inspector 的 SirenixPa… |
| [`AesirPathLookupAssetEditor`](<Runestone/AesirArchitecture/Editor/AesirPathLookupAssetEditor.md>) | AesirPathLookup 锚点资产的 Inspector — 说明资产用途并比对期望 / 实际 GUID （参照 Odin 的 SirenixPathLookupScri… |
| [`AesirSamplesBuildFilter`](<Runestone/AesirArchitecture/Editor/AesirSamplesBuildFilter.md>) | Aesir 示例构建剔除钩子 — 构建发起时自动把本次构建场景列表中的 Aesir 示例场景剔除，并输出明细日志。 示例面向编辑器内学习，不应进入玩家构建：示例脚本已由整文件 … |
| [`AesirUpdateController`](<Runestone/AesirArchitecture/Editor/AesirUpdateController.md>) | 包更新窗口的共享编排控制器——检测 / 更新日志 / 更新执行 / 忙碌门禁 / 进度的唯一真源。 IMGUI 兜底窗口与 Odin 版窗口经构造注入同一 UpdateStat… |
| [`AesirUpdateController.UpdateState`](<Runestone/AesirArchitecture/Editor/AesirUpdateController.UpdateState.md>) | 更新器状态。窗口以 [SerializeField] 持有以跨域重载保留远程检测结果与更新日志； AesirUpdateController 是唯一写入者，窗口层只读。 |
| [`AesirUpdateService`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.md>) | Aesir 包自动更新服务 — 供 AesirUpdateWindow 调用的无状态工具集。 适用场景：用户通过复制 / unitypackage 导入方式将包装在 Insta… |
| [`AesirUpdateService.ChangelogSection`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.ChangelogSection.md>) | CHANGELOG 中的一个版本段落（Keep a Changelog 格式的 ## [x.y.z] - 日期 小节）。 |
| [`AesirUpdateService.FilesManifest`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.FilesManifest.md>) | files-manifest 结构的本地安装清单（.aesir/installed-manifest.json）。 与 UpdateInfo 共用 PackageEntry。 |
| [`AesirUpdateService.FilesManifest.PackageEntry`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.FilesManifest.PackageEntry.md>) | 单个包的安装清单。 |
| [`AesirUpdateService.InstalledPackage`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.InstalledPackage.md>) | 扫描到的本地已安装包。 |
| [`AesirUpdateService.ReleaseSnapshot`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.ReleaseSnapshot.md>) | 一次成功检测的结果快照：来源 + tag +（可能缺失的）清单。 unitypackage 下载地址按命名约定从 tag 构造，不依赖 API 的资产列表。 标记 Serial… |
| [`AesirUpdateService.UpdateInfo`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.UpdateInfo.md>) | update-info.json 结构：版本信息 + 各包文件清单（仓库内文件，jsDelivr / GitHub 均可拉取）。 数组而非 Dictionary — JsonU… |
| [`AesirUpdateWindow`](<Runestone/AesirArchitecture/Editor/AesirUpdateWindow.md>) | Aesir 包更新窗口（IMGUI 兜底版）— 面向"代码导入 Assets/Runestone（非 UPM）"的用户， 检查远程最新版本并一键更新本地安装的 Aesir 包。… |
| [`AesirUpdateWindowOdin`](<Runestone/AesirArchitecture/Editor/AesirUpdateWindowOdin.md>) | Aesir 包更新窗口（Odin Inspector 版）— 检测远程最新版本、展示「本地 → 远程」更新日志、 确认后一键更新 InstallRootRelativePath… |
| [`AesirUpdateWindowOdin.PackageRow`](<Runestone/AesirArchitecture/Editor/AesirUpdateWindowOdin.PackageRow.md>) | 单个本地安装包的行视图模型。显示文本 / 颜色 / 可更新标记在 RebuildRows 时一次性算好，绘制期只读。 |
| [`EnsureAesirArchitectureDefine`](<Runestone/AesirArchitecture/Editor/EnsureAesirArchitectureDefine.md>) | 自动确保 AESIR_ARCHITECTURE 脚本宏定义符号存在。 通过 InitializeOnLoadAttribute 在编辑器加载时自动执行， 供 Aesir 系列其… |
| [`ObservableCollectionDrawerHelper`](<Runestone/AesirArchitecture/Editor/ObservableCollectionDrawerHelper.md>) | 可观察集合的 Odin 内联调试面板 —— 在 Inspector 中直接显示集合运行状态与元素预览， 其下仍保留默认绘制（元素可正常编辑）。 |
| [`ObservableCollectionInspectorUtility`](<Runestone/AesirArchitecture/Editor/ObservableCollectionInspectorUtility.md>) | 可观察集合调试面板的反射工具 —— 在编辑器侧读取集合的运行时状态。 |
| [`ObservableDictionaryDrawer<TKey, TValue>`](<Runestone/AesirArchitecture/Editor/ObservableDictionaryDrawer{TKey, TValue}.md>) | — |
| [`ObservableHashSetDrawer<T>`](<Runestone/AesirArchitecture/Editor/ObservableHashSetDrawer{T}.md>) | 可观察集合（HashSet）的内联调试面板。 |
| [`ObservableListDrawer<T>`](<Runestone/AesirArchitecture/Editor/ObservableListDrawer{T}.md>) | 可观察列表的内联调试面板。 |
| [`ObservableQueueDrawer<T>`](<Runestone/AesirArchitecture/Editor/ObservableQueueDrawer{T}.md>) | 可观察队列的内联调试面板。 |
| [`QuickCreateSOMenuItem`](<Runestone/AesirArchitecture/Editor/QuickCreateSOMenuItem.md>) | 右键快捷生成 ScriptableObject 资源文件。 项目同时安装 Aesir Inspector（独立包，写入 AESIR_INSPECTOR 宏）时本类整体不参与编译… |
| [`ScriptingSymbolEditorUtility`](<Runestone/AesirArchitecture/Editor/ScriptingSymbolEditorUtility.md>) | 脚本宏定义工具，用于管理 PlayerSettings 中的 Scripting Define Symbols。 遍历所有构建目标（排除 Unknown 和 Dedicated… |

</div>

### 枚举

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirGetStartedService.AesirInstallType`](<Runestone/AesirArchitecture/Editor/AesirGetStartedService.AesirInstallType.md>) | 包安装形态（决定示例根目录的解析方式）。 |

</div>

## Runestone.AesirArchitecture.Editor.OdinInspector

命名空间 `Runestone.AesirArchitecture.Editor.OdinInspector` · 程序集 `Runestone.AesirArchitecture.Editor.OdinInspector` · 共 3 个类型。

### 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirArchitectureAttributeProcessor`](<Runestone/AesirArchitecture/Editor/OdinInspector/AesirArchitectureAttributeProcessor.md>) | 为 AesirArchitecture 类动态添加特性。 |
| [`ObservableValueAttributeProcessor<T>`](<Runestone/AesirArchitecture/Editor/OdinInspector/ObservableValueAttributeProcessor{T}.md>) | 为泛型 ObservableValue 提供的 Odin Inspector 特性处理器，用于优化其在面板上的展示效果。 |
| [`RemoveListenerOnSceneUnloadedTriggerAttributeProcessor`](<Runestone/AesirArchitecture/Editor/OdinInspector/RemoveListenerOnSceneUnloadedTriggerAttributeProcessor.md>) | 为 RemoveListenerOnSceneUnloadedTrigger 类提供 Odin Inspector 属性处理器 |

</div>

## Runestone.AesirArchitecture.Internal

命名空间 `Runestone.AesirArchitecture.Internal` · 程序集 `Runestone.AesirArchitecture` · 共 4 个类型。

### 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CloneCollection<T>.EnumerableCollection<T>`](<Runestone/AesirArchitecture/Internal/CloneCollection{T}.EnumerableCollection{T}.md>) | ReadOnly cloned collection. |
| [`ListExtensions`](<Runestone/AesirArchitecture/Internal/ListExtensions.md>) | List{T} 的只读跨度批量操作降级实现。 |
| [`ObservableCollectionUtility`](<Runestone/AesirArchitecture/Internal/ObservableCollectionUtility.md>) | 可观察集合内部工具。 |

</div>

### 结构体

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`CloneCollection<T>`](<Runestone/AesirArchitecture/Internal/CloneCollection{T}.md>) | ReadOnly cloned collection. |

</div>
