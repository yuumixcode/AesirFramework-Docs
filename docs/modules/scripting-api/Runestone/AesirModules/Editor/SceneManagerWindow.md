---
title: SceneManagerWindow
description: "Runestone.AesirModules.Editor.SceneManagerWindow 的 API 文档"
---

# `SceneManagerWindow`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirModules.Editor`
    - **程序集:** `Runestone.AesirModules.Editor`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.ScriptableObject` → `UnityEditor.EditorWindow` → `Sirenix.OdinInspector.Editor.OdinEditorWindow` → `SceneManagerWindow`

**实现接口:** `UnityEngine.ISerializationCallbackReceiver`，`UnityEditor.IHasCustomMenu`

## 声明

``` csharp
public class SceneManagerWindow : Sirenix.OdinInspector.Editor.OdinEditorWindow, 
UnityEngine.ISerializationCallbackReceiver, 
UnityEditor.IHasCustomMenu
```

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`SceneManagerWindow()`](#constructor-scenemanagerwindow) | — |

</div>

### SceneManagerWindow() {#constructor-scenemanagerwindow}

``` csharp
public SceneManagerWindow()
```

## 字段

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `ToastPopupArea` | — | `OdinEditorWindow` |

</div>

## 属性

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `titleContent` | — | `EditorWindow` |
| `hideFlags` | — | `Object` |
| `dataModeController` | — | `EditorWindow` |
| `overlayCanvas` | — | `EditorWindow` |
| `position` | — | `EditorWindow` |
| `maxSize` | — | `EditorWindow` |
| `minSize` | — | `EditorWindow` |
| `WindowPadding` | — | `OdinEditorWindow` |
| `rootVisualElement` | — | `EditorWindow` |
| `DrawUnityEditorPreview` | — | `OdinEditorWindow` |
| `UseScrollView` | — | `OdinEditorWindow` |
| `autoRepaintOnSceneChange` | — | `EditorWindow` |
| `docked` | — | `EditorWindow` |
| `hasFocus` | — | `EditorWindow` |
| `hasUnsavedChanges` | — | `EditorWindow` |
| `maximized` | — | `EditorWindow` |
| `wantsLessLayoutEvents` | — | `EditorWindow` |
| `wantsMouseEnterLeaveWindow` | — | `EditorWindow` |
| `wantsMouseMove` | — | `EditorWindow` |
| `DefaultEditorPreviewHeight` | — | `OdinEditorWindow` |
| `DefaultLabelWidth` | — | `OdinEditorWindow` |
| `depthBufferBits` | — | `EditorWindow` |
| `name` | — | `Object` |
| `saveChangesMessage` | — | `EditorWindow` |
| `CurrentDrawingTargets` | — | `OdinEditorWindow` |
| `PropertyTree` | — | `OdinEditorWindow` |
| `antiAlias` | — | `EditorWindow` |
| `title` | — | `EditorWindow` |

</div>

## 事件

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `OnBeginGUI` | — | `OdinEditorWindow` |
| `OnClose` | — | `OdinEditorWindow` |
| `OnEndGUI` | — | `OdinEditorWindow` |

</div>

## 方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 | 声明类型 |
| :--- | :--- | :--- |
| `GetType()` | — | `object` |
| `SendEvent(Event)` | — | `EditorWindow` |
| `TryGetOverlay(string, ref Overlay)` | — | `EditorWindow` |
| `GetInstanceID()` | — | `Object` |
| `Equals(object)` | — | `Object` |
| `GetHashCode()` | — | `Object` |
| `ToString()` | — | `Object` |
| `GetExtraPaneTypes()` | — | `EditorWindow` |
| `AddItemsToMenu(GenericMenu)` | — | `OdinEditorWindow` |
| `DiscardChanges()` | — | `EditorWindow` |
| `Repaint()` | — | `EditorWindow` |
| `SaveChanges()` | — | `EditorWindow` |
| `BeginWindows()` | — | `EditorWindow` |
| `Close()` | — | `EditorWindow` |
| `EndWindows()` | — | `EditorWindow` |
| `Focus()` | — | `EditorWindow` |
| `RemoveNotification()` | — | `EditorWindow` |
| `Show()` | — | `EditorWindow` |
| `Show(bool)` | — | `EditorWindow` |
| `ShowAsDropDown(Rect, Vector2)` | — | `EditorWindow` |
| `ShowAuxWindow()` | — | `EditorWindow` |
| `ShowModal()` | — | `EditorWindow` |
| `ShowModalUtility()` | — | `EditorWindow` |
| `ShowNotification(GUIContent)` | — | `EditorWindow` |
| `ShowNotification(GUIContent, double)` | — | `EditorWindow` |
| `ShowPopup()` | — | `EditorWindow` |
| `ShowTab()` | — | `EditorWindow` |
| `ShowToast(ToastPosition, SdfIconType, string, string, Color, float)` | — | `OdinEditorWindow` |
| `ShowToast(ToastPosition, SdfIconType, string, string, Color, float, string, Action)` | — | `OdinEditorWindow` |
| `ShowToast(ToastPosition, SdfIconType, string, Color, float)` | — | `OdinEditorWindow` |
| `ShowToast(ToastPosition, SdfIconType, string, Color, float, string, Action)` | — | `OdinEditorWindow` |
| `ShowUtility()` | — | `EditorWindow` |
| `MemberwiseClone()` | — | `object` |
| `OnEnable()` | — | `SceneManagerWindow` |
| `GetTargets()` | — | `OdinEditorWindow` |
| `GetTarget()` | — | `OdinEditorWindow` |
| `DrawEditor(int)` | — | `OdinEditorWindow` |
| `DrawEditorPreview(int, float)` | — | `OdinEditorWindow` |
| `DrawEditors()` | — | `OdinEditorWindow` |
| `Finalize()` | — | `object` |
| `Initialize()` | — | `OdinEditorWindow` |
| `OnAfterDeserialize()` | — | `OdinEditorWindow` |
| `OnBackingScaleFactorChanged()` | — | `EditorWindow` |
| `OnBeforeSerialize()` | — | `OdinEditorWindow` |
| `OnBeginDrawEditors()` | — | `OdinEditorWindow` |
| `OnDestroy()` | — | `OdinEditorWindow` |
| `OnDisable()` | — | `OdinEditorWindow` |
| `OnEndDrawEditors()` | — | `OdinEditorWindow` |
| `OnImGUI()` | — | `OdinEditorWindow` |
| `EnableAutomaticHeightAdjustment(int, bool)` | — | `OdinEditorWindow` |
| `EnsureEditorsAreReady()` | — | `OdinEditorWindow` |
| `UpdateEditors()` | — | `OdinEditorWindow` |
| `SetDirty()` | — | `ScriptableObject` |
| `OnGUI()` | — | `OdinEditorWindow` |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
