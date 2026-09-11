---
title: Scripting API
description: "Runestone.AesirArchitecture 系列命名空间的 Scripting API 参考"
---

# Scripting API

本参考由 Script Doc Generator 基于 C# 反射离线生成，重新生成时自动保留各页面 `## Additional Notes` 之后的手写补充。页面按字母序排列；使用左侧目录或站内搜索定位类型。

## Runestone.AesirArchitecture

命名空间 `Runestone.AesirArchitecture` · 程序集 `Runestone.AesirArchitecture` · 共 83 个类型。

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
| [`AutoRemoveListenerHandle`](<Runestone/AesirArchitecture/AutoRemoveListenerHandle.md>) | 自动移除监听句柄。包装注销回调。 |
| [`CollectionAddEventArgs<T>`](<Runestone/AesirArchitecture/CollectionAddEventArgs{T}.md>) | 集合添加事件参数。包含被添加项及其索引。 |
| [`CollectionRemoveEventArgs<T>`](<Runestone/AesirArchitecture/CollectionRemoveEventArgs{T}.md>) | 集合移除事件参数。包含被移除项及其移除前所在索引。 |
| [`CollectionReplaceEventArgs<T>`](<Runestone/AesirArchitecture/CollectionReplaceEventArgs{T}.md>) | 集合替换事件参数。包含替换位置索引、旧项与新项。 |
| [`DictionaryUpdateEventArgs<TKey, TValue>`](<Runestone/AesirArchitecture/DictionaryUpdateEventArgs{TKey, TValue}.md>) | 字典更新事件参数。包含键、旧值与新值。 |
| [`MonoLifecycleProxy.ListenerEntry`](<Runestone/AesirArchitecture/MonoLifecycleProxy.ListenerEntry.md>) | 监听条目，记录单个回调及其排序信息 |
| [`MonoLifecycleProxy.PendingChange`](<Runestone/AesirArchitecture/MonoLifecycleProxy.PendingChange.md>) | 挂起变更条目，记录调用期间累积的一次监听增删操作 |
| [`ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>`](<Runestone/AesirArchitecture/ObservableDictionary{TKey, TValue}.Enumerator{TKey, TValue}.md>) | 可观察字典实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`ObservableHashSet<T>.Enumerator<T>`](<Runestone/AesirArchitecture/ObservableHashSet{T}.Enumerator{T}.md>) | 可观察集合实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`ObservableList<T>.Enumerator<T>`](<Runestone/AesirArchitecture/ObservableList{T}.Enumerator{T}.md>) | 可观察列表实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。 |

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

命名空间 `Runestone.AesirArchitecture.Editor` · 程序集 `Runestone.AesirArchitecture.Editor` · 共 10 个类型。

### 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirUpdateService`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.md>) | Aesir 包自动更新服务 — 供 AesirUpdateWindow 调用的无状态工具集。 适用场景：用户通过复制 / unitypackage 导入方式将包装在 Insta… |
| [`AesirUpdateService.FilesManifest`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.FilesManifest.md>) | files-manifest 结构的本地安装清单（.aesir/installed-manifest.json）。 与 UpdateInfo 共用 PackageEntry。 |
| [`AesirUpdateService.FilesManifest.PackageEntry`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.FilesManifest.PackageEntry.md>) | 单个包的安装清单。 |
| [`AesirUpdateService.InstalledPackage`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.InstalledPackage.md>) | 扫描到的本地已安装包。 |
| [`AesirUpdateService.ReleaseSnapshot`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.ReleaseSnapshot.md>) | 一次成功检测的结果快照：来源 + tag +（可能缺失的）清单。 unitypackage 下载地址按命名约定从 tag 构造，不依赖 API 的资产列表。 |
| [`AesirUpdateService.UpdateInfo`](<Runestone/AesirArchitecture/Editor/AesirUpdateService.UpdateInfo.md>) | update-info.json 结构：版本信息 + 各包文件清单（仓库内文件，jsDelivr / GitHub 均可拉取）。 数组而非 Dictionary — JsonU… |
| [`AesirUpdateWindow`](<Runestone/AesirArchitecture/Editor/AesirUpdateWindow.md>) | Aesir 包更新窗口 — 面向"代码导入 Assets/Runestone（非 UPM）"的用户， 检查远程最新版本并一键更新本地安装的 Aesir 包。 版本检测面向大陆用… |
| [`EnsureAesirArchitectureDefine`](<Runestone/AesirArchitecture/Editor/EnsureAesirArchitectureDefine.md>) | 自动确保 AESIR_ARCHITECTURE 脚本宏定义符号存在。 通过 InitializeOnLoadAttribute 在编辑器加载时自动执行， 供 Aesir 系列其… |
| [`QuickCreateSOMenuItem`](<Runestone/AesirArchitecture/Editor/QuickCreateSOMenuItem.md>) | 右键快捷生成 ScriptableObject 资源文件。 项目同时安装 Aesir Inspector（独立包，写入 AESIR_INSPECTOR 宏）时本类整体不参与编译… |
| [`ScriptingSymbolUtility`](<Runestone/AesirArchitecture/Editor/ScriptingSymbolUtility.md>) | 脚本宏定义工具，用于管理 PlayerSettings 中的 Scripting Define Symbols。 遍历所有构建目标（排除 Unknown 和 Dedicated… |

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
