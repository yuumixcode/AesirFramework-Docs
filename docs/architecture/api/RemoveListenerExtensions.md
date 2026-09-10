---
title: RemoveListenerExtensions
description: "Runestone.AesirArchitecture.RemoveListenerExtensions 的 API 文档"
---

# `RemoveListenerExtensions`

!!! note ""

    - **种类:** `static class`
    - **命名空间:** `Runestone.AesirArchitecture`
    - **程序集:** `Runestone.AesirArchitecture`

**继承链:** `System.Object` → `RemoveListenerExtensions`

## 声明

``` csharp
[Extension]
public static class RemoveListenerExtensions
```

事件监听器自动移除扩展方法类，用于绑定移除操作到 Unity 生命周期

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`RemoveListenerWhenGameObjectOnDestroyed(AutoRemoveListenerHandle, GameObject)`](#method-removelistenerwhengameobjectondestroyed-autoremovelistenerhandle-gameobject) | 当指定的 GameObject 被销毁时自动移除监听 |
| [`RemoveListenerWhenGameObjectOnDestroyed(AutoRemoveListenerHandle, MonoBehaviour)`](#method-removelistenerwhengameobjectondestroyed-autoremovelistenerhandle-monobehaviour) | 当指定的 MonoBehaviour 所属 GameObject 被销毁时自动移除监听 |
| [`RemoveListenerWhenGameObjectOnDisable(AutoRemoveListenerHandle, GameObject)`](#method-removelistenerwhengameobjectondisable-autoremovelistenerhandle-gameobject) | 当指定的 GameObject 被禁用（OnDisable）时自动移除监听 |
| [`RemoveListenerWhenGameObjectOnDisable(AutoRemoveListenerHandle, MonoBehaviour)`](#method-removelistenerwhengameobjectondisable-autoremovelistenerhandle-monobehaviour) | 当指定的 MonoBehaviour 所属 GameObject 被禁用（OnDisable）时自动移除监听 |
| [`RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle)`](#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle) | 当当前活动场景卸载时自动移除监听 |
| [`RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle, MonoBehaviour)`](#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle-monobehaviour) | 当监听者所在 GameObject 所属的场景卸载时自动移除监听 |
| [`RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle, Scene)`](#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle-scene) | 当指定场景卸载时自动移除监听 |

</div>

**继承的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `Equals(object)` | — | `object` |
| `GetHashCode()` | — | `object` |
| `ToString()` | — | `object` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |

</div>

### RemoveListenerWhenGameObjectOnDestroyed(AutoRemoveListenerHandle, GameObject) {#method-removelistenerwhengameobjectondestroyed-autoremovelistenerhandle-gameobject}

当指定的 GameObject 被销毁时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenGameObjectOnDestroyed(this AutoRemoveListenerHandle removeListener, GameObject gameObject)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `gameObject` | `GameObject` |

</div>

### RemoveListenerWhenGameObjectOnDestroyed(AutoRemoveListenerHandle, MonoBehaviour) {#method-removelistenerwhengameobjectondestroyed-autoremovelistenerhandle-monobehaviour}

当指定的 MonoBehaviour 所属 GameObject 被销毁时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenGameObjectOnDestroyed(this AutoRemoveListenerHandle removeListener, MonoBehaviour mono)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `mono` | `MonoBehaviour` |

</div>

### RemoveListenerWhenGameObjectOnDisable(AutoRemoveListenerHandle, GameObject) {#method-removelistenerwhengameobjectondisable-autoremovelistenerhandle-gameobject}

当指定的 GameObject 被禁用（OnDisable）时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenGameObjectOnDisable(this AutoRemoveListenerHandle removeListener, GameObject gameObject)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `gameObject` | `GameObject` |

</div>

### RemoveListenerWhenGameObjectOnDisable(AutoRemoveListenerHandle, MonoBehaviour) {#method-removelistenerwhengameobjectondisable-autoremovelistenerhandle-monobehaviour}

当指定的 MonoBehaviour 所属 GameObject 被禁用（OnDisable）时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenGameObjectOnDisable(this AutoRemoveListenerHandle removeListener, MonoBehaviour mono)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `mono` | `MonoBehaviour` |

</div>

### RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle) {#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle}

当当前活动场景卸载时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenOnSceneUnloaded(this AutoRemoveListenerHandle removeListener)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |

</div>

### RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle, MonoBehaviour) {#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle-monobehaviour}

当监听者所在 GameObject 所属的场景卸载时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenOnSceneUnloaded(this AutoRemoveListenerHandle removeListener, MonoBehaviour mono)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `mono` | `MonoBehaviour` |

</div>

### RemoveListenerWhenOnSceneUnloaded(AutoRemoveListenerHandle, Scene) {#method-removelistenerwhenonsceneunloaded-autoremovelistenerhandle-scene}

当指定场景卸载时自动移除监听

``` csharp
[Extension]
[Ext] public static void RemoveListenerWhenOnSceneUnloaded(this AutoRemoveListenerHandle removeListener, Scene scene)
```
**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 |
| :--- | :--- |
| `removeListener` | `AutoRemoveListenerHandle` |
| `scene` | `Scene` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
