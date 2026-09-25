---
title: AesirUpdateWindow
description: "Runestone.AesirArchitecture.Editor.AesirUpdateWindow 的 API 文档"
---

# `AesirUpdateWindow`

!!! note ""

    - **种类:** `class`
    - **命名空间:** `Runestone.AesirArchitecture.Editor`
    - **程序集:** `Runestone.AesirArchitecture.Editor`

**继承链:** `System.Object` → `UnityEngine.Object` → `UnityEngine.ScriptableObject` → `UnityEditor.EditorWindow` → `AesirUpdateWindow`

## 声明

``` csharp
public class AesirUpdateWindow : UnityEditor.EditorWindow
```

Aesir 包更新窗口（IMGUI 兜底版）— 面向"代码导入 Assets/Runestone（非 UPM）"的用户， 检查远程最新版本并一键更新本地安装的 Aesir 包。
安装了 Odin Inspector 时，菜单入口经 OdinWindowOpener 路由到 Odin 版窗口 （AesirUpdateWindowOdin，界面与交互更丰富）；未安装时本窗口为菜单落点。 全部编排逻辑（检测 / 更新日志 / 更新执行 / 忙碌门禁）在共享控制器 AesirUpdateController 中与 Odin 版窗口共用，本类只做状态序列化与 IMGUI 展示。

流程：检测远程版本 → 拉取并展示「本地 → 远程」更新日志 → 确认框二次确认 → 备份 Assets/Runestone → 按清单差集清理残留 → 静默导入 → 逐包登记安装清单。 远程版本 / 检测结果 / 更新日志均为序列化字段，更新导入触发域重载后窗口内容不丢失； 过期包列表为缓存值，OnGUI 期间零 LINQ、零磁盘 IO。

## 构造方法

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`AesirUpdateWindow()`](#constructor-aesirupdatewindow) | — |

</div>

### AesirUpdateWindow() {#constructor-aesirupdatewindow}

``` csharp
public AesirUpdateWindow()
```

## 属性

**声明的属性**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`OdinWindowOpener`](#property-odinwindowopener) | Odin 版窗口的打开委托（由 Odin 程序集经 [InitializeOnLoadMethod] 注册； 未安装 Odin Inspector 时为 null，菜单打开本 IMGUI 兜底窗口）。 |

</div>

**继承的属性**

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
| `rootVisualElement` | — | `EditorWindow` |
| `autoRepaintOnSceneChange` | — | `EditorWindow` |
| `docked` | — | `EditorWindow` |
| `hasFocus` | — | `EditorWindow` |
| `hasUnsavedChanges` | — | `EditorWindow` |
| `maximized` | — | `EditorWindow` |
| `wantsLessLayoutEvents` | — | `EditorWindow` |
| `wantsMouseEnterLeaveWindow` | — | `EditorWindow` |
| `wantsMouseMove` | — | `EditorWindow` |
| `depthBufferBits` | — | `EditorWindow` |
| `name` | — | `Object` |
| `saveChangesMessage` | — | `EditorWindow` |
| `antiAlias` | — | `EditorWindow` |
| `title` | — | `EditorWindow` |

</div>

### OdinWindowOpener {#property-odinwindowopener}

Odin 版窗口的打开委托（由 Odin 程序集经 [InitializeOnLoadMethod] 注册； 未安装 Odin Inspector 时为 null，菜单打开本 IMGUI 兜底窗口）。

``` csharp
public static Action OdinWindowOpener { get; private set; }
```

## 方法

**声明的方法**

<div class="api-summary-table" markdown="1">

| 名称 | 描述 |
| :--- | :--- |
| [`RegisterOdinWindowOpener(Action)`](#method-registerodinwindowopener-action) | 注册 Odin 版窗口的打开方式（域重载清空静态委托后由 Odin 程序集重新注册）。 |

</div>

**继承的方法**

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
| `ShowUtility()` | — | `EditorWindow` |
| `MemberwiseClone()` | — | `object` |
| `Finalize()` | — | `object` |
| `OnBackingScaleFactorChanged()` | — | `EditorWindow` |
| `SetDirty()` | — | `ScriptableObject` |

</div>

### RegisterOdinWindowOpener(Action) {#method-registerodinwindowopener-action}

注册 Odin 版窗口的打开方式（域重载清空静态委托后由 Odin 程序集重新注册）。

``` csharp
public static void RegisterOdinWindowOpener(Action opener)
```

**参数**

<div class="api-params-table" markdown="1">

| 名称 | 类型 | 说明 |
| :--- | :--- | :--- |
| `opener` | `Action` | — |

</div>

## Additional Notes

> 首个 `## Additional Notes` 是增量生成文档标识符，请勿修改标题级别和内容！本文档由 [`Script Doc Generator`](https://github.com/yuumixcode/AesirFramework) 辅助生成。
