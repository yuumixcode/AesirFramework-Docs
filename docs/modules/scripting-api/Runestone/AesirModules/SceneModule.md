---
title: SceneModule
description: "Runestone.AesirModules.SceneModule 的 API 文档"
---

# `SceneModule`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules`
    - **程序集:** `Runestone.AesirModules`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.Component` → `UnityEngine.Behaviour` → `UnityEngine.MonoBehaviour` → `Sirenix.OdinInspector.SerializedMonoBehaviour` → `Runestone.AesirArchitecture.AesirMonoBehaviour` → `SceneModule`

**实现接口:** `Sirenix.Serialization.ISupportsPrefabSerialization`，`UnityEngine.ISerializationCallbackReceiver`

## 声明

``` csharp
public class SceneModule : Runestone.AesirArchitecture.AesirMonoBehaviour, 
Sirenix.Serialization.ISupportsPrefabSerialization, 
UnityEngine.ISerializationCallbackReceiver
```

场景加载与叠加管理模块。
语义对齐 Unity 原生 LoadSceneMode：Single 卸载全部场景并重设激活场景； Additive 纯叠加、不改变激活场景，叠加场景统一记入追踪列表（UnloadScene 卸载时自动移出）。 Addressable 场景（Addressable）不归本模块加载， 请通过 Addressables API 加载。

加载/卸载完成会同步广播 SceneLoadedEvent / SceneUnloadedEvent （参数为场景路径），供多个系统订阅场景生命周期。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SceneModule()`](#constructor-scenemodule) | — |

</div>

### SceneModule() {#constructor-scenemodule}

``` csharp
public SceneModule()
```

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`PresetBootstrapSceneNames`](#field-presetbootstrapscenenames) | 预设的启动场景名称（运行时 BootstrapSceneHelper 共用的单一事实来源）。 仅供编辑器 BootstrapSceneHelper 按名称搜集启动场景使用，本模块运行时不做自动搜索。 |

</div>

### PresetBootstrapSceneNames {#field-presetbootstrapscenenames}

预设的启动场景名称（运行时 BootstrapSceneHelper 共用的单一事实来源）。 仅供编辑器 BootstrapSceneHelper 按名称搜集启动场景使用，本模块运行时不做自动搜索。

``` csharp
public static readonly IReadOnlyList<string> PresetBootstrapSceneNames;
```

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AddedScenePaths`](#property-addedscenepaths) | 叠加场景路径（只读）。含所有经本模块 Additive 加载、尚未卸载的场景。 |
| [`SceneLoadedEvent`](#property-sceneloadedevent) | — |
| [`SceneUnloadedEvent`](#property-sceneunloadedevent) | — |
| [`LastLoadedScene`](#property-lastloadedscene) | 最后一个已经加载的场景，Scene 结构体 |
| [`BootstrapSceneAssetWrapper`](#property-bootstrapsceneassetwrapper) | 启动场景引用（编辑器 BootstrapSceneHelper 的工作流之外，供用户代码读取路径/名称自行编排启动流程）。 |
| [`Instance`](#property-instance) | 全局单例入口。 优先在已加载场景中查找预放置的实例；未找到时在 AesirModules（DDOL）下创建子物体。 |

</div>

**继承的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `destroyCancellationToken` | — | `MonoBehaviour` |
| `gameObject` | — | `Component` |
| `hideFlags` | — | `Object` |
| `transform` | — | `Component` |
| `enabled` | — | `Behaviour` |
| `isActiveAndEnabled` | — | `Behaviour` |
| `runInEditMode` | — | `MonoBehaviour` |
| `useGUILayout` | — | `MonoBehaviour` |
| `name` | — | `Object` |
| `tag` | — | `Component` |
| `animation` | — | `Component` |
| `audio` | — | `Component` |
| `camera` | — | `Component` |
| `collider` | — | `Component` |
| `collider2D` | — | `Component` |
| `constantForce` | — | `Component` |
| `hingeJoint` | — | `Component` |
| `light` | — | `Component` |
| `networkView` | — | `Component` |
| `particleSystem` | — | `Component` |
| `renderer` | — | `Component` |
| `rigidbody` | — | `Component` |
| `rigidbody2D` | — | `Component` |

</div>

### AddedScenePaths {#property-addedscenepaths}

叠加场景路径（只读）。含所有经本模块 Additive 加载、尚未卸载的场景。

``` csharp
public IReadOnlyList<string> AddedScenePaths { get; }
```

### SceneLoadedEvent {#property-sceneloadedevent}

``` csharp
public MiniEvent<string> SceneLoadedEvent { get; }
```

### SceneUnloadedEvent {#property-sceneunloadedevent}

``` csharp
public MiniEvent<string> SceneUnloadedEvent { get; }
```

### LastLoadedScene {#property-lastloadedscene}

最后一个已经加载的场景，Scene 结构体

``` csharp
public Scene LastLoadedScene { get; private set; }
```

### BootstrapSceneAssetWrapper {#property-bootstrapsceneassetwrapper}

启动场景引用（编辑器 BootstrapSceneHelper 的工作流之外，供用户代码读取路径/名称自行编排启动流程）。

``` csharp
public SceneAssetWrapper BootstrapSceneAssetWrapper { get; }
```

### Instance {#property-instance}

全局单例入口。 优先在已加载场景中查找预放置的实例；未找到时在 AesirModules（DDOL）下创建子物体。

``` csharp
public static SceneModule Instance { get; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SetActiveScene(SceneAssetWrapper)`](#method-setactivescene-sceneassetwrapper) | 把已加载的指定场景设为激活场景。通过 SceneAssetWrapper 指定场景。 |
| [`SetActiveScene(string)`](#method-setactivescene-string) | 把已加载的指定场景设为激活场景（多场景叠加工作流的高频操作，决定光照设置来源与 Instantiate 默认落点）。对齐 Unity 原生 SetActiveScene 语义，返回是否成功； 场景未加载或引用无效时输出错误并返回 false。 |
| [`LoadSceneAdditive(SceneAssetWrapper, Action, Action, Action<float>)`](#method-loadsceneadditive-sceneassetwrapper-action-action-action-float) | 加载场景。Additive 模式。通过 SceneAssetWrapper 指定场景。 引用无效（空/不在 BuildSettings）或为 Addressable 场景时走失败回调。 |
| [`LoadSceneAdditive(string, Action, Action, Action<float>)`](#method-loadsceneadditive-string-action-action-action-float) | 加载场景。Additive 模式：纯叠加、不改变激活场景（对齐 Unity 原生语义），并记入叠加追踪。 可传入完成/失败回调与逐帧进度回调（0-1，已按 0.9 激活上限归一化）。 约定：请勿对同一路径重复叠加加载——Unity 会加载两个场景实例，而追踪列表按路径粒度只记录一次， UnloadScene(string, Action, Action) 按路径卸载时只卸载其中一个实例，剩余实例将脱离追踪。 |
| [`LoadSceneSingle(SceneAssetWrapper, Action, Action, Action<float>)`](#method-loadscenesingle-sceneassetwrapper-action-action-action-float) | 加载场景。Single 模式。通过 SceneAssetWrapper 指定场景。 引用无效（空/不在 BuildSettings）或为 Addressable 场景时走失败回调。 |
| [`LoadSceneSingle(string, Action, Action, Action<float>)`](#method-loadscenesingle-string-action-action-action-float) | 加载场景。Single 模式：卸载全部场景、重设激活场景、加载成功后清空叠加追踪（失败时保留）。 可传入完成/失败回调与逐帧进度回调（0-1，已按 0.9 激活上限归一化）。 |
| [`ReloadScene(Action, Action)`](#method-reloadscene-action-action) | 重新加载当前激活场景。异步 Single 模式，加载成功后清空叠加场景追踪。 编辑器中激活场景尚未保存（无有效路径）时走失败回调。 |
| [`UnloadAllAddedScenes(Action)`](#method-unloadalladdedscenes-action) | 卸载所有经本模块叠加加载的场景。单个场景卸载失败（场景已被外部卸载）时跳过并告警，不影响其余场景。 可传入全部卸载完成回调。 |
| [`UnloadScene(SceneAssetWrapper, Action, Action)`](#method-unloadscene-sceneassetwrapper-action-action) | 卸载场景。通过 SceneAssetWrapper 指定场景。 |
| [`UnloadScene(string, Action, Action)`](#method-unloadscene-string-action-action) | 卸载场景。若该场景在叠加追踪列表中则自动移出。可传入卸载完成/失败回调。 |

</div>

**继承的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetComponent(Type)` | — | `Component` |
| `GetComponent(string)` | — | `Component` |
| `GetComponentInChildren(Type)` | — | `Component` |
| `GetComponentInChildren(Type, bool)` | — | `Component` |
| `GetComponentInParent(Type)` | — | `Component` |
| `GetComponentInParent(Type, bool)` | — | `Component` |
| `GetComponents(Type)` | — | `Component` |
| `GetComponentsInChildren(Type)` | — | `Component` |
| `GetComponentsInChildren(Type, bool)` | — | `Component` |
| `GetComponentsInParent(Type)` | — | `Component` |
| `GetComponentsInParent(Type, bool)` | — | `Component` |
| `StartCoroutine(IEnumerator)` | — | `MonoBehaviour` |
| `StartCoroutine(string)` | — | `MonoBehaviour` |
| `StartCoroutine(string, object)` | — | `MonoBehaviour` |
| `GetComponent()` | — | `Component` |
| `GetComponentInChildren()` | — | `Component` |
| `GetComponentInChildren(bool)` | — | `Component` |
| `GetComponentInParent()` | — | `Component` |
| `GetComponentInParent(bool)` | — | `Component` |
| `GetComponents()` | — | `Component` |
| `GetComponentsInChildren()` | — | `Component` |
| `GetComponentsInChildren(bool)` | — | `Component` |
| `GetComponentsInParent()` | — | `Component` |
| `GetComponentsInParent(bool)` | — | `Component` |
| `GetType()` | — | `object` |
| `CompareTag(string)` | — | `Component` |
| `IsInvoking()` | — | `MonoBehaviour` |
| `IsInvoking(string)` | — | `MonoBehaviour` |
| `TryGetComponent(Type, ref Component)` | — | `Component` |
| `TryGetComponent(ref T)` | — | `Component` |
| `GetComponentIndex()` | — | `Component` |
| `GetInstanceID()` | — | `Object` |
| `Equals(object)` | — | `Object` |
| `GetHashCode()` | — | `Object` |
| `ToString()` | — | `Object` |
| `BroadcastMessage(string)` | — | `Component` |
| `BroadcastMessage(string, SendMessageOptions)` | — | `Component` |
| `BroadcastMessage(string, object)` | — | `Component` |
| `BroadcastMessage(string, object, SendMessageOptions)` | — | `Component` |
| `CancelInvoke()` | — | `MonoBehaviour` |
| `CancelInvoke(string)` | — | `MonoBehaviour` |
| `GetComponents(Type, List<Component>)` | — | `Component` |
| `GetComponents(List<T>)` | — | `Component` |
| `GetComponentsInChildren(List<T>)` | — | `Component` |
| `GetComponentsInChildren(bool, List<T>)` | — | `Component` |
| `GetComponentsInParent(bool, List<T>)` | — | `Component` |
| `Invoke(string, float)` | — | `MonoBehaviour` |
| `InvokeRepeating(string, float, float)` | — | `MonoBehaviour` |
| `SendMessage(string)` | — | `Component` |
| `SendMessage(string, SendMessageOptions)` | — | `Component` |
| `SendMessage(string, object)` | — | `Component` |
| `SendMessage(string, object, SendMessageOptions)` | — | `Component` |
| `SendMessageUpwards(string)` | — | `Component` |
| `SendMessageUpwards(string, SendMessageOptions)` | — | `Component` |
| `SendMessageUpwards(string, object)` | — | `Component` |
| `SendMessageUpwards(string, object, SendMessageOptions)` | — | `Component` |
| `StopAllCoroutines()` | — | `MonoBehaviour` |
| `StopCoroutine(Coroutine)` | — | `MonoBehaviour` |
| `StopCoroutine(IEnumerator)` | — | `MonoBehaviour` |
| `StopCoroutine(string)` | — | `MonoBehaviour` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |
| `OnAfterDeserialize()` | — | `SerializedMonoBehaviour` |
| `OnBeforeSerialize()` | — | `SerializedMonoBehaviour` |
| `StartCoroutine_Auto(IEnumerator)` | — | `MonoBehaviour` |

</div>

### SetActiveScene(SceneAssetWrapper) {#method-setactivescene-sceneassetwrapper}

把已加载的指定场景设为激活场景。通过 SceneAssetWrapper 指定场景。

``` csharp
public bool SetActiveScene(SceneAssetWrapper sceneRef)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sceneRef` | `SceneAssetWrapper` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | — |

</div>

### SetActiveScene(string) {#method-setactivescene-string}

把已加载的指定场景设为激活场景（多场景叠加工作流的高频操作，决定光照设置来源与 Instantiate 默认落点）。对齐 Unity 原生 SetActiveScene 语义，返回是否成功； 场景未加载或引用无效时输出错误并返回 false。

``` csharp
public bool SetActiveScene(string scenePath)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `scenePath` | `string` | — |

</div>

**返回值**

<div class="api-returns-table" markdown="1">

| 类型 | 说明 |
| :--- | :--- |
| `bool` | — |

</div>

### LoadSceneAdditive(SceneAssetWrapper, Action, Action, Action<float>) {#method-loadsceneadditive-sceneassetwrapper-action-action-action-float}

加载场景。Additive 模式。通过 SceneAssetWrapper 指定场景。 引用无效（空/不在 BuildSettings）或为 Addressable 场景时走失败回调。

``` csharp
public void LoadSceneAdditive(SceneAssetWrapper sceneRef, Action onCompleted = null, Action onFailed = null, Action<float> onProgress = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sceneRef` | `SceneAssetWrapper` | — |
| `onCompleted` | `Action` | — |
| `onFailed` | `Action` | — |
| `onProgress` | `Action<float>` | — |

</div>

### LoadSceneAdditive(string, Action, Action, Action<float>) {#method-loadsceneadditive-string-action-action-action-float}

加载场景。Additive 模式：纯叠加、不改变激活场景（对齐 Unity 原生语义），并记入叠加追踪。 可传入完成/失败回调与逐帧进度回调（0-1，已按 0.9 激活上限归一化）。
约定：请勿对同一路径重复叠加加载——Unity 会加载两个场景实例，而追踪列表按路径粒度只记录一次， UnloadScene(string, Action, Action) 按路径卸载时只卸载其中一个实例，剩余实例将脱离追踪。

``` csharp
public void LoadSceneAdditive(string scenePath, Action onCompleted = null, Action onFailed = null, Action<float> onProgress = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `scenePath` | `string` | — |
| `onCompleted` | `Action` | — |
| `onFailed` | `Action` | — |
| `onProgress` | `Action<float>` | — |

</div>

### LoadSceneSingle(SceneAssetWrapper, Action, Action, Action<float>) {#method-loadscenesingle-sceneassetwrapper-action-action-action-float}

加载场景。Single 模式。通过 SceneAssetWrapper 指定场景。 引用无效（空/不在 BuildSettings）或为 Addressable 场景时走失败回调。

``` csharp
public void LoadSceneSingle(SceneAssetWrapper sceneRef, Action onCompleted = null, Action onFailed = null, Action<float> onProgress = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sceneRef` | `SceneAssetWrapper` | — |
| `onCompleted` | `Action` | — |
| `onFailed` | `Action` | — |
| `onProgress` | `Action<float>` | — |

</div>

### LoadSceneSingle(string, Action, Action, Action<float>) {#method-loadscenesingle-string-action-action-action-float}

加载场景。Single 模式：卸载全部场景、重设激活场景、加载成功后清空叠加追踪（失败时保留）。 可传入完成/失败回调与逐帧进度回调（0-1，已按 0.9 激活上限归一化）。

``` csharp
public void LoadSceneSingle(string scenePath, Action onCompleted = null, Action onFailed = null, Action<float> onProgress = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `scenePath` | `string` | — |
| `onCompleted` | `Action` | — |
| `onFailed` | `Action` | — |
| `onProgress` | `Action<float>` | — |

</div>

### ReloadScene(Action, Action) {#method-reloadscene-action-action}

重新加载当前激活场景。异步 Single 模式，加载成功后清空叠加场景追踪。 编辑器中激活场景尚未保存（无有效路径）时走失败回调。

``` csharp
public void ReloadScene(Action onCompleted = null, Action onFailed = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `onCompleted` | `Action` | — |
| `onFailed` | `Action` | — |

</div>

### UnloadAllAddedScenes(Action) {#method-unloadalladdedscenes-action}

卸载所有经本模块叠加加载的场景。单个场景卸载失败（场景已被外部卸载）时跳过并告警，不影响其余场景。 可传入全部卸载完成回调。

``` csharp
public void UnloadAllAddedScenes(Action onAllUnloaded = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `onAllUnloaded` | `Action` | — |

</div>

### UnloadScene(SceneAssetWrapper, Action, Action) {#method-unloadscene-sceneassetwrapper-action-action}

卸载场景。通过 SceneAssetWrapper 指定场景。

``` csharp
public void UnloadScene(SceneAssetWrapper sceneRef, Action onUnloaded = null, Action onFailed = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `sceneRef` | `SceneAssetWrapper` | — |
| `onUnloaded` | `Action` | — |
| `onFailed` | `Action` | — |

</div>

### UnloadScene(string, Action, Action) {#method-unloadscene-string-action-action}

卸载场景。若该场景在叠加追踪列表中则自动移出。可传入卸载完成/失败回调。

``` csharp
public void UnloadScene(string scenePath, Action onUnloaded = null, Action onFailed = null)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `scenePath` | `string` | — |
| `onUnloaded` | `Action` | — |
| `onFailed` | `Action` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
