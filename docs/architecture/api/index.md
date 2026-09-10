---
title: Scripting API
description: "Runestone.AesirArchitecture 命名空间的 Scripting API 参考"
---

# Scripting API

命名空间 `Runestone.AesirArchitecture` · 程序集 `Runestone.AesirArchitecture` · 共 83 个类型。

本参考由 Script Doc Generator 基于 C# 反射离线生成，重新生成时自动保留各页面 `## Additional Notes` 之后的手写补充。页面按字母序排列；使用左侧目录或站内搜索定位类型。

## 类

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AbstractCommand`](<AbstractCommand.md>) | 命令基类。持有上下文引用，通过 OnExecute 执行命令逻辑。 |
| [`AbstractContext<T>`](<AbstractContext{T}.md>) | 上下文基类。纯 C# 实现，不依赖 MonoBehaviour。 子类在 Configure 中注册 Model 和 Service，通过 Instance 获取全局单例。 |
| [`AbstractModel`](<AbstractModel.md>) | Model 基类。继承 AbstractSubmodule 获得生命周期管理，实现 IModel 标记数据层角色。 |
| [`AbstractQuery<TResult>`](<AbstractQuery{TResult}.md>) | 查询基类。持有上下文引用，通过 OnExecute 执行查询逻辑并返回结果。 |
| [`AbstractService`](<AbstractService.md>) | Service 基类。继承 AbstractSubmodule 获得生命周期管理，实现 IService 标记服务层角色。 |
| [`AbstractSubmodule`](<AbstractSubmodule.md>) | 子模块基类。持有上下文引用，通过 OnInitialize 和 OnDispose 管理生命周期。 Model 和 Service 的公共逻辑统一在此实现。 |
| [`AesirArchitecture`](<AesirArchitecture.md>) | Aesir Architecture 接入 MonoBehaviour 生命周期的持久化物体对象。 |
| [`AesirArchitectureDebug`](<AesirArchitectureDebug.md>) | AesirArchitecture 内部日志工具。 所有架构模块的日志输出应走此工具，以醒目的颜色和 [AesirArchitecture] 标识区分来源。 Log/Warni… |
| [`AesirArchitecturePlayerLoop`](<AesirArchitecturePlayerLoop.md>) | 基于 PlayerLoop 的生命周期钩子系统，无需 MonoBehaviour 即可接入游戏级帧回调。 通过 Register 注册回调，order 越小越先执行；系统自动在… |
| [`AesirMonoBehaviour`](<AesirMonoBehaviour.md>) | RAA 架构标准 MonoBehaviour 基类，根据运行环境自动选择序列化方式。 |
| [`AesirScriptableObject`](<AesirScriptableObject.md>) | RAA 架构标准 ScriptableObject 基类，根据运行环境自动选择序列化方式。 |
| [`AesirView<T>`](<AesirView{T}.md>) | View 基类。通过泛型上下文获取模块访问能力，仅具备只读权限，AesirView 自动支持 Odin Inspector 序列化。 |
| [`AesirViewController<T>`](<AesirViewController{T}.md>) | View + Controller 双角色基类。通过泛型上下文获取模块访问能力，自动支持 Odin Inspector 序列化。 |
| [`CapabilityExtensions`](<CapabilityExtensions.md>) | 能力扩展方法集合 |
| [`GenericLocator<T>`](<GenericLocator{T}.md>) | 泛型对象定位器。按类型注册、查询与获取以 T 为基类的对象实例。 |
| [`InternalContextAttribute`](<InternalContextAttribute.md>) | 标记一个 AbstractContext{T} 派生类为框架内部 Context（示例 / 测试等非用户工作流用途）。 被标记的 Context 不会出现在用户工作流的 Con… |
| [`MiniEvent`](<MiniEvent.md>) | 单参事件 |
| [`MiniEvent<T>`](<MiniEvent{T}.md>) | 单参事件 |
| [`MonoLifecycleProxy`](<MonoLifecycleProxy.md>) | Mono 生命周期事件代理。作为全局单例挂载在 [Aesir Architecture] GameObject 上， 将 Unity 原生生命周期回调和自定义 PlayerLo… |
| [`MonoLifecycleProxyExtensions`](<MonoLifecycleProxyExtensions.md>) | Mono 生命周期事件扩展方法集合。 |
| [`MonoView<T>`](<MonoView{T}.md>) | View 基类。通过泛型上下文获取模块访问能力，仅具备只读权限。 |
| [`MonoViewController<T>`](<MonoViewController{T}.md>) | View + Controller 双角色基类。通过泛型上下文获取模块访问能力，无 Odin 依赖。 |
| [`ObservableDictionary<TKey, TValue>`](<ObservableDictionary{TKey, TValue}.md>) | 可观察字典实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`ObservableHashSet<T>`](<ObservableHashSet{T}.md>) | 可观察集合实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`ObservableList<T>`](<ObservableList{T}.md>) | 可观察列表实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。 |
| [`ObservableValue<T>`](<ObservableValue{T}.md>) | 可观察属性实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableValue{T} 只读订阅。 |
| [`PlayerLoopUtility`](<PlayerLoopUtility.md>) | PlayerLoop 操作的静态工具类，提供子系统的插入、查询与描述功能。 供框架内部和外部用户扩展 PlayerLoop，不局限于 AesirArchitectureLife… |
| [`RemoveListenerExtensions`](<RemoveListenerExtensions.md>) | 事件监听器自动移除扩展方法类，用于绑定移除操作到 Unity 生命周期 |
| [`RemoveListenerHandleCollection`](<RemoveListenerHandleCollection.md>) | 监听句柄集合。管理 AutoRemoveListenerHandle 句柄的添加与批量移除， 供 RemoveListenerTrigger 和 RemoveListenerO… |
| [`RemoveListenerOnDestroyTrigger`](<RemoveListenerOnDestroyTrigger.md>) | 在所属 GameObject 销毁时自动移除所有监听。 |
| [`RemoveListenerOnDisableTrigger`](<RemoveListenerOnDisableTrigger.md>) | GameObject 禁用时自动移除所有监听。挂载此组件后，当 GameObject 被禁用时将执行批量移除操作。 |
| [`RemoveListenerOnSceneUnloadedTrigger`](<RemoveListenerOnSceneUnloadedTrigger.md>) | 任意场景卸载时自动移除该场景注册的监听。按场景句柄（handle）分桶， 场景 A 卸载不会误杀场景 B 的监听。 挂载在 [Aesir Architecture] GameO… |
| [`RemoveListenerTrigger`](<RemoveListenerTrigger.md>) | 自动移除监听调用器基类。维护监听句柄列表，子类在特定生命周期事件中调用 RemoveAllListeners 批量移除。 |
| [`ResetStaticsAssistant`](<ResetStaticsAssistant.md>) | 静态变量重置助手（仅泛型类使用）。用于运行时阶段自动重置泛型类中的静态变量，兼容 Disable Domain Reload。 关闭 Domain Reload 时静态回调列表… |

</div>

## 结构体

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirArchitecturePlayerLoop.AesirArchitectureScriptRunAfterUpdate`](<AesirArchitecturePlayerLoop.AesirArchitectureScriptRunAfterUpdate.md>) | PlayerLoop 子系统 type 标识，在 PostLateUpdate 之后执行 |
| [`AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate`](<AesirArchitecturePlayerLoop.AesirArchitectureScriptRunBeforeUpdate.md>) | PlayerLoop 子系统 type 标识，在 Update 之前执行 |
| [`AesirArchitecturePlayerLoop.HookEntry`](<AesirArchitecturePlayerLoop.HookEntry.md>) | 回调条目，记录单个生命周期回调及其排序信息 |
| [`AutoRemoveListenerHandle`](<AutoRemoveListenerHandle.md>) | 自动移除监听句柄。包装注销回调。 |
| [`CollectionAddEventArgs<T>`](<CollectionAddEventArgs{T}.md>) | 集合添加事件参数。包含被添加项及其索引。 |
| [`CollectionRemoveEventArgs<T>`](<CollectionRemoveEventArgs{T}.md>) | 集合移除事件参数。包含被移除项及其移除前所在索引。 |
| [`CollectionReplaceEventArgs<T>`](<CollectionReplaceEventArgs{T}.md>) | 集合替换事件参数。包含替换位置索引、旧项与新项。 |
| [`DictionaryUpdateEventArgs<TKey, TValue>`](<DictionaryUpdateEventArgs{TKey, TValue}.md>) | 字典更新事件参数。包含键、旧值与新值。 |
| [`MonoLifecycleProxy.ListenerEntry`](<MonoLifecycleProxy.ListenerEntry.md>) | 监听条目，记录单个回调及其排序信息 |
| [`MonoLifecycleProxy.PendingChange`](<MonoLifecycleProxy.PendingChange.md>) | 挂起变更条目，记录调用期间累积的一次监听增删操作 |
| [`ObservableDictionary<TKey, TValue>.Enumerator<TKey, TValue>`](<ObservableDictionary{TKey, TValue}.Enumerator{TKey, TValue}.md>) | 可观察字典实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`ObservableHashSet<T>.Enumerator<T>`](<ObservableHashSet{T}.Enumerator{T}.md>) | 可观察集合实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`ObservableList<T>.Enumerator<T>`](<ObservableList{T}.Enumerator{T}.md>) | 可观察列表实现。 Model 层持有可写实例，View 层通过 IReadOnlyObservableList{T} 只读订阅。 |

</div>

## 接口

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`ICanExecuteCommand`](<ICanExecuteCommand.md>) | 执行命令的能力接口 |
| [`ICanExecuteQuery`](<ICanExecuteQuery.md>) | 执行查询的能力接口 |
| [`ICanGetModel`](<ICanGetModel.md>) | 获取 Model 的能力接口 |
| [`ICanGetService`](<ICanGetService.md>) | 获取 Service 的能力接口 |
| [`ICanInitialize`](<ICanInitialize.md>) | 可初始化接口。提供初始化与初始化状态标记。 被 IModel 和 IService 继承。 |
| [`ICanSetContext`](<ICanSetContext.md>) | 可设置上下文引用接口 |
| [`ICommand`](<ICommand.md>) | 同步命令接口。通过 Command 修改 Model 状态，只写无返回值。 能力：GetModel, GetService, ExecuteCommand |
| [`IContext`](<IContext.md>) | 模块上下文接口。提供模块注册与获取。 |
| [`IContextHolder`](<IContextHolder.md>) | 上下文持有者接口。 |
| [`IController`](<IController.md>) | 泛型控制器接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IController<T>`](<IController{T}.md>) | 泛型控制器接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`ICustomAfterUpdate`](<ICustomAfterUpdate.md>) | 自定义 AfterUpdate 生命周期。对应 AfterUpdate。 |
| [`ICustomBeforeUpdate`](<ICustomBeforeUpdate.md>) | 自定义 BeforeUpdate 生命周期。对应 BeforeUpdate。 |
| [`ICustomFixedUpdate`](<ICustomFixedUpdate.md>) | 自定义 FixedUpdate 生命周期。对应 MonoLifecycleEvent.FixedUpdate。 |
| [`ICustomLateUpdate`](<ICustomLateUpdate.md>) | 自定义 LateUpdate 生命周期。对应 LateUpdate。 |
| [`ICustomOnApplicationFocus`](<ICustomOnApplicationFocus.md>) | 自定义 OnApplicationFocus 生命周期。对应 OnApplicationFocus。 |
| [`ICustomOnApplicationPause`](<ICustomOnApplicationPause.md>) | 自定义 OnApplicationPause 生命周期。对应 OnApplicationPause。 |
| [`ICustomOnApplicationQuit`](<ICustomOnApplicationQuit.md>) | 自定义 OnApplicationQuit 生命周期。对应 OnApplicationQuit。 |
| [`ICustomUpdate`](<ICustomUpdate.md>) | 自定义 Update 生命周期。对应 Update。 |
| [`IGenericLocator<T>`](<IGenericLocator{T}.md>) | 泛型定位器接口。提供按类型注册、查询与获取对象实例的契约。 |
| [`IModel`](<IModel.md>) | 数据层接口。持有状态（通常使用 ObservableValue{T}）。 能力：GetModel, Initialize, Dispose |
| [`IObservableDictionary<TKey, TValue>`](<IObservableDictionary{TKey, TValue}.md>) | 完整可观察字典接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableDictionary{TKey, TValue} 只读订阅。 |
| [`IObservableHashSet<T>`](<IObservableHashSet{T}.md>) | 完整可观察集合接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableHashSet{T} 只读订阅。 |
| [`IObservableList<T>`](<IObservableList{T}.md>) | 完整可观察列表接口。 Model 层通过此接口读写集合；View 层使用 IReadOnlyObservableList{T} 只读订阅。 |
| [`IObservableValue<T>`](<IObservableValue{T}.md>) | 完整可观察属性接口。 Presenter 层通过此接口读写数据。 |
| [`IPresenter`](<IPresenter.md>) | 泛型 MVP 中介接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IPresenter<T>`](<IPresenter{T}.md>) | 泛型 MVP 中介接口。绑定指定上下文类型，实现者自动获得 Context 绑定。 |
| [`IQuery<TResult>`](<IQuery{TResult}.md>) | 查询接口。通过 Query 执行读操作并返回结果，无副作用。 与 ICommand 的区别：Command 负责写操作（无返回值），Query 负责读操作（返回 TResult）。 |
| [`IReadOnlyObservableDictionary<TKey, TValue>`](<IReadOnlyObservableDictionary{TKey, TValue}.md>) | 只读可观察字典接口。 View 层通过此接口读取键值并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableHashSet<T>`](<IReadOnlyObservableHashSet{T}.md>) | 只读可观察集合接口。 View 层通过此接口读取元素并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableList<T>`](<IReadOnlyObservableList{T}.md>) | 只读可观察列表接口。 View 层通过此接口枚举元素并订阅变更，不能修改集合。 |
| [`IReadOnlyObservableValue<T>`](<IReadOnlyObservableValue{T}.md>) | 只读可观察属性接口。 View 层通过此接口添加监听，不能修改值。 |
| [`IService`](<IService.md>) | 服务层接口。万能协调层，封装跨模块业务逻辑，协调模块间交互与通信。 Service 能读写 Model、调用其他 Service，完成跨模块协调。 不包含 ICanExecut… |
| [`IView`](<IView.md>) | 表现层接口。View 层通过此接口与模块上下文交互。 能力：GetModel, GetService |

</div>

## 枚举

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirArchitectureLifecyclePhase`](<AesirArchitectureLifecyclePhase.md>) | 游戏级生命周期阶段，对应 PlayerLoop 子系统插入点 |
| [`MonoLifecycleEvent`](<MonoLifecycleEvent.md>) | Mono 生命周期事件类型，涵盖 Unity 原生生命周期回调和自定义 PlayerLoop 阶段。 |

</div>
