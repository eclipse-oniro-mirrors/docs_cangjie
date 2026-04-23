# PromptAction

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Create and display instant feedback, dialogs, action menus, and custom popups.

> **Note:**
>
> The following APIs require first obtaining a PromptAction instance via the [getPromptAction()](./cj-apis-uicontext-uicontext.md#func-getpromptaction) method from [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext), then calling corresponding methods through this instance.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class PromptAction

```cangjie
public class PromptAction {}
```

**Description:** The PromptAction class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func closeCustomDialog(Int32)

```cangjie
public func closeCustomDialog(dialogId: Int32): Unit
```

**Description:** Closes a custom dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| dialogId | Int32 | Yes | - | The ID of the dialog to close, returned by openCustomDialog. |

### func openCustomDialog(CustomDialogOptions, (Int32) -> Unit)

```cangjie
public func openCustomDialog(options: CustomDialogOptions, callBack: (Int32) -> Unit): Unit
```

**Description:** Opens a custom dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| options | [CustomDialogOptions](#class-customdialogoptions) | Yes | - | Custom dialog options. |
| callBack | (Int32) -> Unit | Yes | - | Callback function. |

### func showActionMenu(ActionMenuOptions, ShowActionMenuCallBack)

```cangjie
public func showActionMenu(option: ActionMenuOptions, callback!: ShowActionMenuCallBack = defaultCallback)
```

**Description:** Displays an action menu with given settings. This API uses asynchronous callback to return results.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| option | [ActionMenuOptions](#class-actionmenuoptions) | Yes | - | Action menu options. |
| callback | [ShowActionMenuCallBack](#type-showactionmenucallback) | No | defaultCallback | **Named parameter.** Callback for returning action menu response results. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code | Description |
  |:----------|:------------|
  | 100001 | Internal error: failed to allocate memory. |

### func showDialog(ShowDialogOptions, ShowDialogCallBack)

```cangjie
public func showDialog(option: ShowDialogOptions, callback!: ShowDialogCallBack = defaultCallback)
```

**Description:** Displays a dialog with given settings. This API uses asynchronous callback to return results.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| option | [ShowDialogOptions](#class-showdialogoptions) | Yes | - | Dialog options. |
| callback | [ShowDialogCallBack](#type-showdialogcallback) | No | defaultCallback | **Named parameter.** Callback for returning dialog response results. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code | Description |
  |:----------|:------------|
  | 100001 | Internal error: failed to allocate memory. |

### func showToast(ShowToastOptions)

```cangjie
public func showToast(option: ShowToastOptions): Unit
```

**Description:** Displays a Toast with given settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| option | [ShowToastOptions](#class-showtoastoptions) | Yes | - | Toast options. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code | Description |
  |:----------|:------------|
  | 100001 | Internal error: failed to allocate memory. |

### func openCustomDialog(CustomDialogConfig, (Int32) -> Unit)

```cangjie
public func openCustomDialog(options: CustomDialogConfig, callBack: (Int32) -> Unit): Unit
```

**Function:** Opens a custom dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [CustomDialogConfig](#class-customdialogconfig) | Yes | - | Custom dialog configuration options. |
| callBack | (Int32) -> Unit | Yes | - | Callback function. |

### func showActionMenu(ActionMenuConfig, ShowActionMenuCallBack)

```cangjie
public func showActionMenu(option: ActionMenuConfig, callback!: ShowActionMenuCallBack = defaultCallback)
```

**Function:** Displays an action menu with given settings. This API uses asynchronous callback to return results.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| option | [ActionMenuConfig](#class-actionmenuconfig) | Yes | - | Action menu configuration options. |
| callback | [ShowActionMenuCallBack](#type-showactionmenucallback) | No | defaultCallback | **Named parameter.** Callback for returning action menu response results. defaultCallback indicates {_: Option\<BusinessException>, _: Option\<Int32> =>} |

### func showDialog(ShowDialogConfig, ShowDialogCallBack)

```cangjie
public func showDialog(option: ShowDialogConfig, callback!: ShowDialogCallBack = defaultCallback)
```

**Function:** Displays a dialog with given settings. This API uses asynchronous callback to return results.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| option | [ShowDialogConfig](#class-showdialogconfig) | Yes | - | Dialog configuration options. |
| callback | [ShowDialogCallBack](#type-showdialogcallback) | No | defaultCallback | **Named parameter.** Callback for returning dialog response results. defaultCallback indicates {_: Option\<BusinessException>, _: Option\<Int32> =>} |

## class ActionMenuOptions

```cangjie
public open class ActionMenuOptions {
    public var title: ResourceStr
    public var buttons: Array<ButtonInfo>
    public var showInSubWindow: Bool
    public var isModal: Bool
    public init(
        title!: ResourceStr = '',
        buttons!: Array<ButtonInfo>,
        showInSubWindow!: Bool = false,
        isModal!: Bool = true
    )
}
```

**Description:** Action menu options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var buttons

```cangjie
public var buttons: Array<ButtonInfo>
```

**Description:** Array of buttons in the dialog.

**Type:** Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isModal

```cangjie
public var isModal: Bool
```

**Description:** Whether it is a modal dialog.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Description:** Whether to display in a sub-window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var title

```cangjie
public var title: ResourceStr
```

**Description:** The text title to display.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(ResourceStr, Array\<ButtonInfo>, Bool, Bool)

```cangjie
public init(
    title!: ResourceStr = '',
    buttons!: Array<ButtonInfo>,
    showInSubWindow!: Bool = false,
    isModal!: Bool = true
)
```

**Description:** Constructor for ActionMenuOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| title | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | **Named parameter.** The text title to display. |
| buttons | Array\<[ButtonInfo](#class-buttoninfo)> | Yes | - | **Named parameter.** Array of buttons. |
| showInSubWindow | Bool | No | false | **Named parameter.** Whether to display in a sub-window. |
| isModal | Bool | No | true | **Named parameter.** Whether it is a modal dialog. |

## class BaseDialogOptions

```cangjie
public open class BaseDialogOptions {
    public var maskRect: Rectangle
    public var alignment: DialogAlignment
    public var offset: Offset
    public var isModal: Bool
    public var showInSubWindow: Bool
    public var autoCancel: Bool
    public var maskColor: ResourceColor
    public var transition: TransitionEffect
    public var onDidAppear: () -> Unit
    public var onDidDisappear: () -> Unit
    public var onWillAppear: () -> Unit
    public var onWillDisappear: () -> Unit
    public var keyboardAvoidMode: KeyboardAvoidMode
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public init(
        maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0.vp, 0.vp),
        isModal!: Bool = true,
        showInSubWindow!: Bool = false,
        autoCancel!: Bool = true,
        maskColor!: ResourceColor = Color(0x33000000),
        transition!: TransitionEffect = TransitionEffect.OPACITY,
        onDidAppear!: () -> Unit = {=>},
        onDidDisappear!: () -> Unit = {=>},
        onWillAppear!: () -> Unit = {=>},
        onWillDisappear!: () -> Unit = {=>},
        keyboardAvoidMode!: KeyboardAvoidMode = KeyboardAvoidMode.Default,
        enableHoverMode!: Bool = false,
        hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
    )
}
```

**Description:** Basic dialog options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Description:** The alignment of the dialog on the screen.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var autoCancel

```cangjie
public var autoCancel: Bool
```

**Description:** Whether to allow users to exit by clicking the mask layer.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Description:** Whether to respond to hover mode.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Description:** The display area of the dialog in hover mode.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isModal

```cangjie
public var isModal: Bool
```

**Description:** Whether it is a modal dialog.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var keyboardAvoidMode

```cangjie
public var keyboardAvoidMode: KeyboardAvoidMode
```

**Description:** The keyboard avoidance mode for custom dialogs.

**Type:** [KeyboardAvoidMode](#enum-keyboardavoidmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var maskColor

```cangjie
public var maskColor: ResourceColor
```

**Description:** The mask color of the custom dialog.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Description:** The mask area of the dialog. Size cannot exceed the main window.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: Offset
```

**Description:** The offset of the dialog.

**Type:** [Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onDidAppear

```cangjie
public var onDidAppear: () -> Unit
```

**Description:** Callback function when the dialog appears.

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onDidDisappear

```cangjie
public var onDidDisappear: () -> Unit
```

**Description:** Callback function when the dialog disappears.

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillAppear

```cangjie
public var onWillAppear: () -> Unit
```

**Description:** Callback function before the dialog opening animation starts.

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillDisappear

```cangjie
public var onWillDisappear: () -> Unit
```

**Description:** Callback function before the dialog closing animation starts.

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Description:** Whether to display in a sub-window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: TransitionEffect
```

**Description:** Transition parameters when opening/closing the custom dialog.

**Type:** [TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Rectangle, DialogAlignment, Offset, Bool, Bool, Bool, ResourceColor, TransitionEffect, () -> Unit, () -> Unit, () -> Unit, () -> Unit, KeyboardAvoidMode, Bool, HoverModeAreaType)

```cangjie
public init(
    maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0.vp, 0.vp),
    isModal!: Bool = true,
    showInSubWindow!: Bool = false,
    autoCancel!: Bool = true,
    maskColor!: ResourceColor = Color(0x33000000),
    transition!: TransitionEffect = TransitionEffect.OPACITY,
    onDidAppear!: () -> Unit = {=>},
    onDidDisappear!: () -> Unit = {=>},
    onWillAppear!: () -> Unit = {=>},
    onWillDisappear!: () -> Unit = {=>},
    keyboardAvoidMode!: KeyboardAvoidMode = KeyboardAvoidMode.Default,
    enableHoverMode!: Bool = false,
    hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
)
```

**Description:** Constructor for BaseDialogOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---------|:-----|:--------|:--------|:------------|
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | **Named parameter.** The mask area of the dialog. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | **Named parameter.** The alignment of the dialog on the screen. |
| offset | [Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** The offset of the dialog. |
| isModal | Bool | No | true | **Named parameter.** Whether it is a modal dialog. |
| showInSubWindow | Bool | No | false | **Named parameter.** Whether to display in a sub-window. |
| autoCancel | Bool | No | true | **Named parameter.** Whether to allow users to exit by clicking the mask layer. |
| maskColor | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color(0x33000000) | **Named parameter.** The mask color of the custom dialog. |
| transition | [TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | TransitionEffect.OPACITY | **Named parameter.** Transition parameters when opening/closing the custom dialog. |
| onDidAppear | () -> Unit | No | {=>} | **Named parameter.** Callback function when the dialog appears. |
| onDidDisappear | () -> Unit | No | {=>} | **Named parameter.** Callback function when the dialog disappears. |
| onWillAppear | () -> Unit | No | {=>} | **Named parameter.** Callback function before the dialog opening animation starts. |
| onWillDisappear | () -> Unit | No | {=>} | **Named parameter.** Callback function before the dialog closing animation starts. |
| keyboardAvoidMode | [KeyboardAvoidMode](#enum-keyboardavoidmode## class ButtonInfo

```cangjie
public class ButtonInfo {
    public var text: ResourceStr
    public var color: ResourceColor
    public var primary: Bool
    public init(text!: ResourceStr, color!: ResourceColor, primary!: Bool = false)
}
```

**Function:** Provides menu item button configuration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var color

```cangjie
public var color: ResourceColor
```

**Function:** Text color of the button.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var primary

```cangjie
public var primary: Bool
```

**Function:** Determines whether the button responds to Enter/Space keys by default.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var text

```cangjie
public var text: ResourceStr
```

**Function:** Display text on the button.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(ResourceStr, ResourceColor, Bool)

```cangjie
public init(text!: ResourceStr, color!: ResourceColor, primary!: Bool = false)
```

**Function:** Constructs a menu item button within a menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| text | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Button text content. |
| color | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | **Named parameter.** Button text color. |
| primary | Bool | No | false | **Named parameter.** Whether the button responds to Enter/Space keys by default. |

## class CustomDialogOptions

```cangjie
public class CustomDialogOptions <: BaseDialogOptions {
    public var builder: () -> Unit
    public var backgroundColor: ResourceColor
    public var cornerRadius: BorderRadiuses
    public var borderWidth: EdgeWidths
    public var borderColor: EdgeColors
    public var borderStyle: EdgeStyles
    public var width: Length
    public var height: Length
    public var shadow: ?ShadowOptions
    public var backgroundBlurStyle: BlurStyle
    public init(
        builder!: () -> Unit,
        maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0.vp, 0.vp),
        isModal!: Bool = true,
        showInSubWindow!: Bool = false,
        autoCancel!: Bool = true,
        maskColor!: ResourceColor = Color(0x33000000),
        transition!: TransitionEffect = TransitionEffect.OPACITY,
        onDidAppear!: () -> Unit = {=>},
        onDidDisappear!: () -> Unit = {=>},
        onWillAppear!: () -> Unit = {=>},
        onWillDisappear!: () -> Unit = {=>},
        keyboardAvoidMode!: KeyboardAvoidMode = KeyboardAvoidMode.Default,
        enableHoverMode!: Bool = false,
        hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen,
        backgroundColor!: ResourceColor = Color.Transparent,
        cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
            bottomRight: 32.vp),
        borderWidth!: EdgeWidths = EdgeWidths(top: 0.vp, right: 0.vp, bottom: 0.vp, left: 0.vp),
        borderColor!: EdgeColors = EdgeColors(top: Color.Black, right: Color.Black, bottom: Color.Black, left: Color.Black),
        borderStyle!: EdgeStyles = EdgeStyles(),
        width!: Length = 400.vp,
        height!: Length = 100.vp,
        shadow!: ?ShadowOptions = None,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick
    )
}
```

**Function:** Custom dialog content options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [BaseDialogOptions](#class-basedialogoptions)

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Background color of the custom dialog.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderColor

```cangjie
public var borderColor: EdgeColors
```

**Function:** Border color of the custom dialog.

**Type:** [EdgeColors](#class-edgecolors)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderRadius

```cangjie
public var borderRadius: BorderRadiuses
```

**Function:** Border radius of the custom dialog.

**Type:** [BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderStyle

```cangjie
public var borderStyle: EdgeStyles
```

**Function:** Border style of the custom dialog.

**Type:** [EdgeStyles](./cj-common-types.md#class-edgestyles)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderWidth

```cangjie
public var borderWidth: EdgeWidths
```

**Function:** Border width of the custom dialog.

**Type:** [EdgeWidths](./cj-common-types.md#class-edgewidths)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var builder

```cangjie
public var builder: () -> Unit
```

**Function:** Allows developers to customize dialog content.

**Type:** () -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Background blur style of the dialog.

**Type:** [BlurStyle](./cj-common-types.md#enum-blurstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: Length
```

**Function:** Height of the dialog.

**Type:** [Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Shadow effect of the dialog.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: Length
```

**Function:** Width of the dialog.

**Type:** [Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(() -> Unit, Rectangle, DialogAlignment, Offset, Bool, Bool, Bool, ResourceColor, TransitionEffect, () -> Unit, () -> Unit, () -> Unit, () -> Unit, KeyboardAvoidMode, Bool, HoverModeAreaType, ResourceColor, BorderRadiuses, EdgeWidths, EdgeColors, EdgeStyles, Length, Length, ?ShadowOptions, BlurStyle)

```cangjie
public init(
    builder!: () -> Unit,
    maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0.vp, 0.vp),
    isModal!: Bool = true,
    showInSubWindow!: Bool = false,
    autoCancel!: Bool = true,
    maskColor!: ResourceColor = Color(0x33000000),
    transition!: TransitionEffect = TransitionEffect.OPACITY,
    onDidAppear!: () -> Unit = {=>},
    onDidDisappear!: () -> Unit = {=>},
    onWillAppear!: () -> Unit = {=>},
    onWillDisappear!: () -> Unit = {=>},
    keyboardAvoidMode!: KeyboardAvoidMode = KeyboardAvoidMode.Default,
    enableHoverMode!: Bool = false,
    hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen,
    backgroundColor!: ResourceColor = Color.Transparent,
    cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
        bottomRight: 32.vp),
    borderWidth!: EdgeWidths = EdgeWidths(top: 0.vp, right: 0.vp, bottom: 0.vp, left: 0.vp),
    borderColor!: EdgeColors = EdgeColors(top: Color.Black, right: Color.Black, bottom: Color.Black, left: Color.Black),
    borderStyle!: EdgeStyles = EdgeStyles(),
    width!: Length = 400.vp,
    height!: Length = 100.vp,
    shadow!: ?ShadowOptions = None,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick
)
```

**Function:** Dialog constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| builder | () -> Unit | Yes | - | **Named parameter.** Custom dialog content builder. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | **Named parameter.** Dialog mask area. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | **Named parameter.** Dialog alignment on screen. |
| offset | [Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** Dialog offset. |
| isModal | Bool | No | true | **Named parameter.** Whether the dialog is modal. |
| showInSubWindow | Bool | No | false | **Named parameter.** Whether to show in sub-window. |
| autoCancel | Bool | No | true | **Named parameter.** Whether clicking mask layer can dismiss dialog. |
| maskColor | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color(0x33000000) | **Named parameter.** Custom dialog mask color. |
| transition | [TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | TransitionEffect.OPACITY | **Named parameter.** Transition effects when dialog opens/closes. |
| onDidAppear | () -> Unit | No | {=>} | **Named parameter.** Callback when dialog appears. |
| onDidDisappear | () -> Unit | No | {=>} | **Named parameter.** Callback when dialog disappears. |
| onWillAppear | () -> Unit | No | {=>} | **Named parameter.** Callback before dialog opening animation starts. |
| onWillDisappear | () -> Unit | No | {=>} | **Named parameter.** Callback before dialog closing animation starts. |
| keyboardAvoidMode | [KeyboardAvoidMode](#enum-keyboardavoidmode) | No | KeyboardAvoidMode.Default | **Named parameter.** Keyboard avoidance mode for custom dialog. |
| enableHoverMode | Bool | No | false | **Named parameter.** Whether to enable hover mode. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | **Named parameter.** Display area in hover mode. |
| backgroundColor | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color.Transparent | **Named parameter.** Custom dialog background color. |
| cornerRadius | [BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) | **Named parameter.** Custom dialog corner radius. |
| borderWidth | [EdgeWidths](./cj-common-types.md#class-edgewidths) | No | EdgeWidths(top: 0.vp, right: 0.vp, bottom: 0.vp, left: 0.vp) | **Named parameter.** Custom dialog border width. |
| borderColor | [EdgeColors](#class-edgecolors) | No | EdgeColors(top: Color.Black, right: Color.Black, bottom: Color.Black, left: Color.Black) | **Named parameter.** Custom dialog border color. |
| borderStyle | [EdgeStyles](./cj-common-types.md#class-edgestyles) | No | EdgeStyles() | **Named parameter.** Custom dialog border style. |
| width | [Length](./cj-common-types.md#interface-length) | No | 400.vp | **Named parameter.** Dialog width. |
| height | [Length](./cj-common-types.md#interface-length) | No | 100.vp | **Named parameter.** Dialog height. |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Dialog shadow effect. |
| backgroundBlurStyle | [BlurStyle](./cj-common-types.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Dialog background blur style. |

## class EdgeColors

```cangjie
public class EdgeColors {
    public var top: ResourceColor
    public var right: ResourceColor
    public var bottom: ResourceColor
    public var left: ResourceColor
    public init(
        top!: ResourceColor = Color.Black,
        right!: ResourceColor = Color.Black,
        bottom!: ResourceColor = Color.Black,
        left!: ResourceColor = Color.Black
    )
}
```

**Function:** Provides border color configuration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottom

```cangjie
public var bottom: ResourceColor
```

**Function:** Bottom border color.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var left

```cangjie
public var left: ResourceColor
```

**Function:** Left border color.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var right

```cangjie
public var right: ResourceColor
```

**Function:** Right border color.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var top

```cangjie
public var top: ResourceColor
```

**Function:** Top border color.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(ResourceColor, ResourceColor, ResourceColor, ResourceColor)

```cangjie
public init(
    top!: ResourceColor = Color.Black,
    right!: ResourceColor = Color.Black,
    bottom!: ResourceColor = Color.Black,
    left!: ResourceColor = Color.Black
)
```

**Function:** EdgeColors constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Top border color. |
| right | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Right border color. |
| bottom | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Bottom border color. |
| left | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Left border color. |## class ShowDialogOptions

```cangjie
public open class ShowDialogOptions {
    public var title: ResourceStr
    public var message: ResourceStr
    public var buttons: Array<ButtonInfo>
    public var alignment: DialogAlignment
    public var offset: Offset
    public var maskRect: Rectangle
    public var showInSubWindow: Bool
    public var isModal: Bool
    public var backgroundColor: ResourceColor
    public var backgroundBlurStyle: BlurStyle
    public var shadow: ?ShadowOptions
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public init(
        title!: ResourceStr = '',
        message!: ResourceStr = '',
        buttons!: Array<ButtonInfo> = [],
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0.vp, 0.vp),
        maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
        showInSubWindow!: Bool = false,
        isModal!: Bool = true,
        backgroundColor!: Color = Color.Transparent,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        shadow!: ?ShadowOptions = None,
        enableHoverMode!: Bool = false,
        hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
    )
}
```

**Function:** Dialog display options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Function:** Alignment of the dialog on the screen.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Background color of the dialog.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Background blur style of the dialog.

**Type:** [BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var buttons

```cangjie
public var buttons: Array<ButtonInfo>
```

**Function:** Array of buttons in the dialog. Supports multiple buttons.

**Type:** Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var buttonsSize

```cangjie
public var buttonsSize: UInt32
```

**Function:** Number of buttons.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Function:** Whether to enable hover mode.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Function:** Display area of the dialog in hover mode.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Whether the dialog is modal.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** Mask area of the dialog. Size cannot exceed the main window.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var message

```cangjie
public var message: ResourceStr
```

**Function:** Main text content.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: Offset
```

**Function:** Offset of the dialog.

**Type:** [Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Shadow options of the dialog.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Whether to display in a sub-window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var title

```cangjie
public var title: ResourceStr
```

**Function:** Title text to be displayed.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(ResourceStr, ResourceStr, Array\<ButtonInfo\>, DialogAlignment, Offset, Rectangle, Bool, Bool, Color, BlurStyle, ?ShadowOptions, Bool, HoverModeAreaType)

```cangjie
public init(
    title!: ResourceStr = '',
    message!: ResourceStr = '',
    buttons!: Array<ButtonInfo> = [],
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0.vp, 0.vp),
    maskRect!: Rectangle = Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent),
    showInSubWindow!: Bool = false,
    isModal!: Bool = true,
    backgroundColor!: Color = Color.Transparent,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    shadow!: ?ShadowOptions = None,
    enableHoverMode!: Bool = false,
    hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
)
```

**Function:** Constructor for dialog display options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | '' | **Named parameter.** Title text. |
| message | [ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | '' | **Named parameter.** Main text content. |
| buttons | Array\<[ButtonInfo](#class-buttoninfo)> | No | [] | **Named parameter.** Array of buttons in the dialog. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | **Named parameter.** Alignment of the dialog on the screen. |
| offset | [Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** Offset of the dialog. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | **Named parameter.** Mask area of the dialog. |
| showInSubWindow | Bool | No | false | **Named parameter.** Whether to display in a sub-window. |
| isModal | Bool | No | true | **Named parameter.** Whether the dialog is modal. |
| backgroundColor | [Color](./cj-common-types.md#class-color) | No | Color.Transparent | **Named parameter.** Background color of the dialog. |
| backgroundBlurStyle | [BlurStyle](./cj-common-types.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Background blur style of the dialog. |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Shadow options of the dialog. |
| enableHoverMode | Bool | No | false | **Named parameter.** Whether to enable hover mode. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | **Named parameter.** Display area of the dialog in hover mode. |

## class ShowToastOptions

```cangjie
public class ShowToastOptions {
    public var message: ResourceStr
    public var duration: UInt32
    public var bottom: Length
    public var showMode: ToastShowMode
    public var alignment: Alignment
    public var offset: Offset
    public var backgroundColor: ResourceColor
    public var textColor: ResourceColor
    public var backgroundBlurStyle: BlurStyle
    public var shadow: ?ShadowOptions = None
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public init(
        message!: ResourceStr,
        duration!: UInt32 = 1500,
        bottom!: Length = 80.vp,
        showMode!: ToastShowMode = ToastShowMode.Default,
        alignment!: Alignment = Alignment.Bottom,
        offset!: Offset = Offset(0.vp, 0.vp),
        backgroundColor!: Color = Color.Transparent,
        textColor!: Color = Color.Black,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        shadow!: ?ShadowOptions = None,
        enableHoverMode!: Bool = false,
        hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
    )
}
```

**Function:** Toast display options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var alignment

```cangjie
public var alignment: Alignment
```

**Function:** Alignment of the Toast on the screen.

**Type:** [Alignment](./cj-common-types.md#enum-alignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Background color of the Toast.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottom

```cangjie
public var bottom: Length
```

**Function:** Distance between the Toast dialog and the bottom of the screen.

**Type:** [Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var duration

```cangjie
public var duration: UInt32
```

**Function:** Duration of the Toast dialog.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Function:** Whether to enable hover mode.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Function:** Display area of the Toast in hover mode.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var message

```cangjie
public var message: ResourceStr
```

**Function:** Text to be displayed.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: Offset
```

**Function:** Offset of the Toast.

**Type:** [Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Background blur style of the Toast.

**Type:** [BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowOptions = None
```

**Function:** Shadow options of the Toast.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showMode

```cangjie
public var showMode: ToastShowMode
```

**Function:** Determines the display mode of the Toast.

**Type:** [ToastShowMode](#enum-toastshowmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var textColor

```cangjie
public var textColor: ResourceColor
```

**Function:** Text color of the Toast.

**Type:** [ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(ResourceStr, UInt32, Length, ToastShowMode, Alignment, Offset, Color, Color, BlurStyle, ?ShadowOptions, Bool, HoverModeAreaType)

```cangjie
public init(
    message!: ResourceStr,
    duration!: UInt32 = 1500,
    bottom!: Length = 80.vp,
    showMode!: ToastShowMode = ToastShowMode.Default,
    alignment!: Alignment = Alignment.Bottom,
    offset!: Offset = Offset(0.vp, 0.vp),
    backgroundColor!: Color = Color.Transparent,
    textColor!: Color = Color.Black,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    shadow!: ?ShadowOptions = None,
    enableHoverMode!: Bool = false,
    hoverModeArea!: HoverModeAreaType = HoverModeAreaType.BottomScreen
)
```

**Function:** Constructor for Toast display options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| message | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Text to be displayed. |
| duration | UInt32 | No | 1500 | **Named parameter.** Duration of the Toast dialog. |
| bottom | [Length](./cj-common-types.md#interface-length) | No | 80.vp | **Named parameter.** Distance between the Toast dialog and the bottom of the screen. |
| showMode | [ToastShowMode](#enum-toastshowmode) | No | ToastShowMode.Default | **Named parameter.** Display mode of the Toast. |
| alignment | [Alignment](./cj-common-types.md#enum-alignment) | No | Alignment.Bottom | **Named parameter.** Alignment of the Toast on the screen. |
| offset | [Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** Offset of the Toast. |
| backgroundColor | [Color](./cj-common-types.md#class-color) | No | Color.Transparent | **Named parameter.** Background color of the Toast. |
| textColor | [Color](./cj-common-types.md#class-color) | No | Color.Black | **Named parameter.** Text color of the Toast. |
| backgroundBlurStyle | [BlurStyle](./cj-common-types.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Background blur style of the Toast. |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Shadow options of the Toast. |
| enableHoverMode | Bool | No | false | **Named parameter.** Whether to enable hover mode. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | H## enum HoverModeAreaType

```cangjie
public enum HoverModeAreaType <: Equatable<HoverModeAreaType> {
    | TopScreen
    | BottomScreen
    | ...
}
```

**Function:** Provides hover mode area types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[HoverModeAreaType](#enum-hovermodeareatype)>

### TopScreen

```cangjie
TopScreen
```

**Function:** Top screen hover mode area type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomScreen

```cangjie
BottomScreen
```

**Function:** Bottom screen hover mode area type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(HoverModeAreaType)

```cangjie
public operator func !=(other: HoverModeAreaType): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HoverModeAreaType](#enum-hovermodeareatype) | Yes | - | Another HoverModeAreaType instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when not equal. |

### operator func ==(HoverModeAreaType)

```cangjie
public operator func ==(other: HoverModeAreaType): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HoverModeAreaType](#enum-hovermodeareatype) | Yes | - | Another HoverModeAreaType instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when equal. |

## class BaseDialogConfig

```cangjie
public open class BaseDialogConfig {
    public mut prop maskRect: ?Rectangle
    public mut prop alignment: ?DialogAlignment
    public mut prop offset: ?Offset
    public mut prop isModal: ?Bool
    public mut prop showInSubWindow: ?Bool
    public mut prop autoCancel: ?Bool
    public mut prop maskColor: ?ResourceColor
    public mut prop transition: ?TransitionEffect
    public mut prop onDidAppear: ?() -> Unit
    public mut prop onDidDisappear: ?() -> Unit
    public mut prop onWillAppear: ?() -> Unit
    public mut prop onWillDisappear: ?() -> Unit
    public mut prop keyboardAvoidMode: ?KeyboardAvoidMode
    public mut prop enableHoverMode: ?Bool
    public mut prop hoverModeArea: ?HoverModeAreaType
    public mut prop levelMode: ?LevelMode
    public init(
        maskRect!: ?Rectangle = Option.None,
        alignment!: ?DialogAlignment = Option.None,
        offset!: ?Offset = Option.None,
        isModal!: ?Bool = Option.None,
        showInSubWindow!: ?Bool = Option.None,
        autoCancel!: ?Bool = Option.None,
        maskColor!: ?ResourceColor = Option.None,
        transition!: ?TransitionEffect = Option.None,
        onDidAppear!: ?() -> Unit = Option.None,
        onDidDisappear!: ?() -> Unit = Option.None,
        onWillAppear!: ?() -> Unit = Option.None,
        onWillDisappear!: ?() -> Unit = Option.None,
        keyboardAvoidMode!: ?KeyboardAvoidMode = Option.None,
        enableHoverMode!: ?Bool = Option.None,
        hoverModeArea!: ?HoverModeAreaType = Option.None,
        levelMode!: ?LevelMode = Option.None
    )
}
```

**Function:** Base dialog configuration class, serving as the base class for dialog configurations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop maskRect

```cangjie
public mut prop maskRect: ?Rectangle
```

**Function:** Dialog mask area. Size cannot exceed the main window.

**Type:** ?[Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop alignment

```cangjie
public mut prop alignment: ?DialogAlignment
```

**Function:** Defines the alignment of the dialog on the screen.

**Type:** ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop offset

```cangjie
public mut prop offset: ?Offset
```

**Function:** Dialog offset.

**Type:** ?[Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop isModal

```cangjie
public mut prop isModal: ?Bool
```

**Function:** Whether it is a modal dialog.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop showInSubWindow

```cangjie
public mut prop showInSubWindow: ?Bool
```

**Function:** Whether to display in a sub-window.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop autoCancel

```cangjie
public mut prop autoCancel: ?Bool
```

**Function:** Whether to allow users to exit by clicking the mask layer.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop maskColor

```cangjie
public mut prop maskColor: ?ResourceColor
```

**Function:** Custom dialog mask color.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop transition

```cangjie
public mut prop transition: ?TransitionEffect
```

**Function:** Transition parameters when opening/closing the custom dialog.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop onDidAppear

```cangjie
public mut prop onDidAppear: ?() -> Unit
```

**Function:** Callback function when the dialog appears.

**Type:** ?() -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop onDidDisappear

```cangjie
public mut prop onDidDisappear: ?() -> Unit
```

**Function:** Callback function when the dialog disappears.

**Type:** ?() -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop onWillAppear

```cangjie
public mut prop onWillAppear: ?() -> Unit
```

**Function:** Callback function before the dialog opening animation starts.

**Type:** ?() -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop onWillDisappear

```cangjie
public mut prop onWillDisappear: ?() -> Unit
```

**Function:** Callback function before the dialog closing animation starts.

**Type:** ?() -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop keyboardAvoidMode

```cangjie
public mut prop keyboardAvoidMode: ?KeyboardAvoidMode
```

**Function:** Keyboard avoidance mode for custom dialogs.

**Type:** ?[KeyboardAvoidMode](#enum-keyboardavoidmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop enableHoverMode

```cangjie
public mut prop enableHoverMode: ?Bool
```

**Function:** Whether to respond to hover mode.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop hoverModeArea

```cangjie
public mut prop hoverModeArea: ?HoverModeAreaType
```

**Function:** Display area of the dialog in hover mode.

**Type:** ?[HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### prop levelMode

```cangjie
public mut prop levelMode: ?LevelMode
```

**Function:** Defines the display level mode of the dialog.

**Type:** ?[LevelMode](#enum-levelmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### init(?Rectangle, ?DialogAlignment, ?Offset, ?Bool, ?Bool, ?Bool, ?ResourceColor, ?TransitionEffect, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?KeyboardAvoidMode, ?Bool, ?HoverModeAreaType, ?LevelMode)

```cangjie
public init(
    maskRect!: ?Rectangle = Option.None,
    alignment!: ?DialogAlignment = Option.None,
    offset!: ?Offset = Option.None,
    isModal!: ?Bool = Option.None,
    showInSubWindow!: ?Bool = Option.None,
    autoCancel!: ?Bool = Option.None,
    maskColor!: ?ResourceColor = Option.None,
    transition!: ?TransitionEffect = Option.None,
    onDidAppear!: ?() -> Unit = Option.None,
    onDidDisappear!: ?() -> Unit = Option.None,
    onWillAppear!: ?() -> Unit = Option.None,
    onWillDisappear!: ?() -> Unit = Option.None,
    keyboardAvoidMode!: ?KeyboardAvoidMode = Option.None,
    enableHoverMode!: ?Bool = Option.None,
    hoverModeArea!: ?HoverModeAreaType = Option.None,
    levelMode!: ?LevelMode = Option.None
)
```

**Function:** Constructor for dialog options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | Option.None | **Named parameter.** Dialog mask area.<br>Default: Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent)<br>**Note:** maskRect does not take effect when showInSubWindow is true.<br>If some properties of Rectangle are set and others are not, the default value for the unset properties is 0.|
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | Option.None | **Named parameter.** Vertical alignment of the dialog. Default: DialogAlignment.Default|
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | Option.None | **Named parameter.** Offset of the dialog relative to the alignment position. Default: Offset(dx: 0.vp, dy: 0.vp)|
| isModal | ?Bool | No | Option.None | **Named parameter.** Whether the dialog is a modal window. When set to true, it is a modal window with a mask layer and cannot interact with other controls around the dialog, meaning events in the mask layer area cannot be passed through. When set to false, it is a non-modal window without a mask layer and can interact with other controls around the dialog. Default: true.|
| showInSubWindow | ?Bool | No | Option.None | **Named parameter.** When a dialog needs to be displayed outside the main window, whether to display this dialog in a sub-window. When set to true, the dialog is displayed in a sub-window. Default: false, the dialog is displayed within the application, not in an independent sub-window.|
| autoCancel | ?Bool | No | Option.None | **Named parameter.** Whether to close the dialog when clicking the mask layer. true means close the dialog, false means do not close the dialog. Default: true|
| maskColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Option.None | **Named parameter.** Custom mask layer color. Default: Color(0x33000000)|
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | Option.None | **Named parameter.** Sets the transition effect for dialog display and exit.<br>**Note:**<br>1. If not set, the default display/exit animation is used.<br>2. Pressing the back key during display animation interrupts the display animation and executes the exit animation, with the animation effect being the combined result of display and exit animation curves.<br>3. Pressing the back key during exit animation does not interrupt the exit animation, and continues pressing the back key to exit the application.|
| onDidAppear | ?() -> Unit | No | Option.None | **Named parameter.** Callback after the dialog appears.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onDidDisappear | ?() -> Unit | No | Option.None | **Named parameter.** Callback after the dialog disappears.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onWillAppear | ?() -> Unit | No | Option.None | **Named parameter.** Callback before the dialog display animation starts.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onWillDisappear | ?() -> Unit | No | Option.None | **Named parameter.** Callback before the dialog exit animation starts.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| keyboardAvoidMode | ?[KeyboardAvoidMode](#enum-keyboardavoidmode) | No | Option.None | **Named parameter.** Sets whether the dialog automatically avoids the soft keyboard when it appears. Default: KeyboardAvoidMode.Default|
| enableHoverMode | ?Bool | No | false | **Named parameter.** Whether to respond to hover state. When set to true, it responds to hover state.<br>Default: false, no response by default.|
| hoverModeArea | ?[HoverModeAreaType](#enum-hovermodeareatype) | No | Option.None | **Named parameter.** Default display area of the dialog in hover mode. Default: HoverModeAreaType.BottomScreen|
| levelMode | ?[LevelMode](#enum-levelmode) | No | Option.None | **Named parameter.** Sets the display level of the dialog.<br>**Note:**<br>Default: LevelMode.Overlay<br>Only takes effect when showInSubWindow property is set to false.|

## class CustomDialogConfig

```cangjie
public class CustomDialogConfig <: BaseDialogConfig {
    public var builder: () -> Unit
    public var backgroundColor: ?ResourceColor
    public var cornerRadius: ?BorderRadiuses
    public var borderWidth: ?EdgeWidths
    public var borderColor: ?EdgeColors
    public var borderStyle: ?EdgeStyles
    public var width: ?Length
    public var height: ?Length
    public var shadow: ?ShadowOptions
    public var backgroundBlurStyle: ?BlurStyle
    public init(
        builder!: () -> Unit,
        maskRect!: ?Rectangle = Option.None,
        alignment!: ?DialogAlignment = Option.None,
        offset!: ?Offset = Option.None,
        isModal!: ?Bool = Option.None,
        showInSubWindow!: ?Bool = Option.None,
        autoCancel!: ?Bool = Option.None,
        maskColor!: ?ResourceColor = Option.None,
        transition!: ?TransitionEffect = Option.None,
        onDidAppear!: ?() -> Unit = Option.None,
        onDidDisappear!: ?() -> Unit = Option.None,
        onWillAppear!: ?() -> Unit = Option.None,
        onWillDisappear!: ?() -> Unit = Option.None,
        keyboardAvoidMode!: ?KeyboardAvoidMode = Option.None,
        enableHoverMode!: ?Bool = Option.None,
        hoverModeArea!: ?HoverModeAreaType = Option.None,
        levelMode!: ?LevelMode = Option.None,
        backgroundColor!: ?ResourceColor = Option.None,
        cornerRadius!: ?BorderRadiuses = Option.None,
        borderWidth!: ?EdgeWidths = Option.None,
        borderColor!: ?EdgeColors = Option.None,
        borderStyle!: ?EdgeStyles = Option.None,
        width!: ?Length = Option.None,
        height!: ?Length = Option.None,
        shadow!: ?ShadowOptions = Option.None,
        backgroundBlurStyle!: ?BlurStyle = Option.None
    )
}
```

**Function:** Custom dialog configuration class, inherits from BaseDialogConfig, used to configure display options for custom dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parent Type:**

- [BaseDialogConfig](#class-basedialogconfig)

### var builder

```cangjie
public var builder: () -> Unit
```

**Function:** Sets the content of the custom popup.

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** Sets the background color of the popup.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var cornerRadius

```cangjie
public var cornerRadius: ?BorderRadiuses
```

**Function:** Sets the corner radius of the background. Can set the radius of 4 corners separately.

**Type:** ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var borderWidth

```cangjie
public var borderWidth: ?EdgeWidths
```

**Function:** Sets the border width of the popup background. Can set the width of 4 borders separately.

**Type:** ?[EdgeWidths](./cj-common-types.md#class-edgewidths)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var borderColor

```cangjie
public var borderColor: ?EdgeColors
```

**Function:** Sets the border color of the popup background.

**Type:** ?[EdgeColors](#class-edgecolors)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var borderStyle

```cangjie
public var borderStyle: ?EdgeStyles
```

**Function:** Sets the border style of the popup background.

**Type:** ?[EdgeStyles](./cj-common-types.md#class-edgestyles)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var width

```cangjie
public var width: ?Length
```

**Function:** Sets the width of the popup background.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var height

```cangjie
public var height: ?Length
```

**Function:** Sets the height of the popup background.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Sets the shadow of the popup background.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Background blur style of the popup.

**Type:** ?[BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### init(() -> Unit, ?Rectangle, ?DialogAlignment, ?Offset, ?Bool, ?Bool, ?Bool, ?ResourceColor, ?TransitionEffect, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?KeyboardAvoidMode, ?Bool, ?HoverModeAreaType, ?ResourceColor, ?BorderRadiuses, ?EdgeWidths, ?EdgeColors, ?EdgeStyles, ?Length, ?Length, ?ShadowOptions, ?BlurStyle, ?LevelMode)

```cangjie
public init(
    builder!: () -> Unit,
    maskRect!: ?Rectangle = Option.None,
    alignment!: ?DialogAlignment = Option.None,
    offset!: ?Offset = Option.None,
    isModal!: ?Bool = Option.None,
    showInSubWindow!: ?Bool = Option.None,
    autoCancel!: ?Bool = Option.None,
    maskColor!: ?ResourceColor = Option.None,
    transition!: ?TransitionEffect = Option.None,
    onDidAppear!: ?() -> Unit = Option.None,
    onDidDisappear!: ?() -> Unit = Option.None,
    onWillAppear!: ?() -> Unit = Option.None,
    onWillDisappear!: ?() -> Unit = Option.None,
    keyboardAvoidMode!: ?KeyboardAvoidMode = Option.None,
    enableHoverMode!: ?Bool = Option.None,
    hoverModeArea!: ?HoverModeAreaType = Option.None,
    backgroundColor!: ?ResourceColor = Option.None,
    cornerRadius!: ?BorderRadiuses = Option.None,
    borderWidth!: ?EdgeWidths = Option.None,
    borderColor!: ?EdgeColors = Option.None,
    borderStyle!: ?EdgeStyles = Option.None,
    width!: ?Length = Option.None,
    height!: ?Length = Option.None,
    shadow!: ?ShadowOptions = Option.None,
    backgroundBlurStyle!: ?BlurStyle = Option.None,
    levelMode!: ?LevelMode = Option.None
)
```

**Function:** Custom dialog configuration constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| builder | () -> Unit | Yes | - | **Named parameter.** Custom dialog content builder.|
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | Option.None | **Named parameter.** Dialog mask area.<br>Default: Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent)<br>**Note:** maskRect does not take effect when showInSubWindow is true.<br>If some properties of Rectangle are set and others are not, the default value for the unset properties is 0.|
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | Option.None | **Named parameter.** Vertical alignment of the dialog. Default: DialogAlignment.Default|
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | Option.None | **Named parameter.** Offset of the dialog relative to the alignment position. Default: Offset(dx: 0.vp, dy: 0.vp)|
| isModal | ?Bool | No | Option.None | **Named parameter.** Whether the dialog is a modal window. When set to true, it is a modal window with a mask layer and cannot interact with other controls around the dialog, meaning events in the mask layer area cannot be passed through. When set to false, it is a non-modal window without a mask layer and can interact with other controls around the dialog. Default: true.|
| showInSubWindow | ?Bool | No | Option.None | **Named parameter.** When a dialog needs to be displayed outside the main window, whether to display this dialog in a sub-window. When set to true, the dialog is displayed in a sub-window. Default: false, the dialog is displayed within the application, not in an independent sub-window.|
| autoCancel | ?Bool | No | Option.None | **Named parameter.** Whether to close the dialog when clicking the mask layer. true means close the dialog, false means do not close the dialog. Default: true|
| maskColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Option.None | **Named parameter.** Custom mask layer color. Default: Color(0x33000000)|
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | Option.None | **Named parameter.** Sets the transition effect for dialog display and exit.<br>**Note:**<br>1. If not set, the default display/exit animation is used.<br>2. Pressing the back key during display animation interrupts the display animation and executes the exit animation, with the animation effect being the combined result of display and exit animation curves.<br>3. Pressing the back key during exit animation does not interrupt the exit animation, and continues pressing the back key to exit the application.|
| onDidAppear | ?() -> Unit | No | Option.None | **Named parameter.** Callback after the dialog appears.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onDidDisappear | ?() -> Unit | No | Option.None | **Named parameter.** Callback after the dialog disappears.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onWillAppear | ?() -> Unit | No | Option.None | **Named parameter.** Callback before the dialog display animation starts.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| onWillDisappear | ?() -> Unit | No | Option.None | **Named parameter.** Callback before the dialog exit animation starts.**Note:**<br>1. Normal sequence: onWillAppear>>onDidAppear>>(onDateAccept/onCancel/onDateChange)>>onWillDisappear>>onDidDisappear.<br>2. Setting callback events to change dialog display effects inside onDidAppear takes effect on the second appearance.<br>3. When quickly clicking to show and dismiss the dialog, onWillDisappear may take effect before onDidAppear.<br>4. When the dialog is closed before the entry animation completes, this callback will not be triggered.|
| keyboardAvoidMode | ?[KeyboardAvoidMode](#enum-keyboardavoidmode) | No | Option.None | **Named parameter.** Sets whether the dialog automatically avoids the soft keyboard when it appears. Default: KeyboardAvoidMode.Default|
| enableHoverMode | Bool | No | false | **Named parameter.** Whether to respond to hover state. When set to true, it responds to hover state.<br>Default: false, no response by default.|
| hoverModeArea | ?[HoverModeAreaType](#enum-hovermodeareatype) | No | Option.None | **Named parameter.** Default display area of the dialog in hover mode. Default: HoverModeAreaType.BottomScreen|
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | Option.None | **Named parameter.** Sets the background color of the dialog. Default: Color.Transparent<br>**Note:**<br>When backgroundColor is set to a non-transparent color, backgroundBlurStyle needs to be set to BlurStyle.NONE, otherwise the color display will not meet expected effects.|
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | Option.None | **Named parameter.** Sets the corner radius of the background. Can set the radius of 4 corners separately.<br>Default: BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp)<br>Corner radius size is limited by component size, maximum value is half of the component width or height, if the value is negative, it is processed according to the default value.<br>Percentage parameter mode: Sets the corner radius of the dialog using percentages of the parent element dialog width and height.|
| borderWidth | ?[EdgeWidths](./cj-common-types.md#class-edgewidths) | No | Option.None | **Named parameter.** Sets the border width of the dialog background.<br>Can set the width of 4 borders separately. Default: EdgeWidths(top: 0.vp, right: 0.vp, bottom: 0.vp, left: 0.vp)<br>Percentage parameter mode: Sets the border width of the dialog using percentages of the parent element dialog width.<br>When the left and right borders are larger than the dialog width, and the top and bottom borders are larger than the dialog height, the display may not meet expectations.|
| borderColor | ?[EdgeColors](#class-edgecolors) | No | Option.None | **Named parameter.** Sets the border color of the dialog background.<br>Default: EdgeColors(top: Color.Black, right: Color.Black, bottom: Color.Black, left: Color.Black).<br>If using the borderColor property, it needs to be used together with the borderWidth property.|
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | Option.None | **Named parameter.** Sets the border style of the dialog background.<br>Default: EdgeStyles().<br>If using the borderStyle property, it needs to be used together with the borderWidth property.|
| width | ?[Length](./cj-common-types.md#interface-length) | No | Option.None | **Named parameter.** Sets the width of the dialog background.<br>**Note:**<br>Default maximum dialog width: 400.vp<br>Percentage parameter mode: Dialog reference width is adjusted based on the width of the window it is in.|
| height | ?[Length](./cj-common-types.md#interface-length) | No | Option.None | **Named parameter.** Sets the height of the dialog background.<br>**Note:**<br>Default maximum dialog height: 0.9 * (window height - safe area).<br>Percentage parameter mode: Dialog reference height is (window height - safe area), adjusted up or down based on this.|
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | Option.None | **Named parameter.** Sets the shadow of the dialog background.|
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | Option.None | **Named parameter.** Background blur style of the dialog. Default: BlurStyle.ComponentUltraThick|
| levelMode | ?[LevelMode](#enum-levelmode) | No | Option.None | **Named parameter.** Sets the display level of the dialog.<br>**Note:**<br>Default: LevelMode.Overlay<br>Only takes effect when showInSubWindow property is set to false.|

## class ShowDialogConfig

```cangjie
public class ShowDialogConfig {
    public var title: ?ResourceStr
    public var message: ?ResourceStr
    public var buttons: ?Array<ButtonInfo>
    public var alignment: ?DialogAlignment
    public var offset: ?Offset
    public var maskRect: ?Rectangle
    public var showInSubWindow: ?Bool
    public var isModal: ?Bool
    public var backgroundColor: ?ResourceColor
    public var backgroundBlurStyle: ?BlurStyle
    public var shadow: ?ShadowOptions
    public var enableHoverMode: ?Bool
    public var hoverModeArea: ?HoverModeAreaType
    public var levelMode: ?LevelMode
    public init(
        title!: ?ResourceStr = Option.None,
        message!: ?ResourceStr = Option.None,
        buttons!: ?Array<ButtonInfo> = Option.None,
        alignment!: ?DialogAlignment = Option.None,
        offset!: ?Offset = Option.None,
        maskRect!: ?Rectangle = Option.None,
        showInSubWindow!: ?Bool = Option.None,
        isModal!: ?Bool = Option.None,
        backgroundColor!: ?ResourceColor = Option.None,
        backgroundBlurStyle!: ?BlurStyle = Option.None,
        shadow!: ?ShadowOptions = Option.None,
        enableHoverMode!: ?Bool = Option.None,
        hoverModeArea!: ?HoverModeAreaType = Option.None,
        levelMode!: ?LevelMode = Option.None
    )
}
```

**Function:** Dialog display configuration class, used to configure display options for standard dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var title

```cangjie
public var title: ?ResourceStr
```

**Function:** Title text.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var message

```cangjie
public var message: ?ResourceStr
```

**Function:** Content text.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var buttons

```cangjie
public var buttons: ?Array<ButtonInfo>
```

**Function:** Array of buttons in the dialog, supports multiple buttons.

**Type:** ?Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var alignment

```cangjie
public var alignment: ?DialogAlignment
```

**Function:** Vertical alignment of the dialog.

**Type:** ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var offset

```cangjie
public var offset: ?Offset
```

**Function:** Offset of the dialog relative to the alignment position.

**Type:** ?[Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var maskRect

```cangjie
public var maskRect: ?Rectangle
```

**Function:** Dialog mask layer area, events within the mask layer area are not passed through, events outside the mask layer area are passed through.

**Type:** ?[Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** When a dialog needs to be displayed outside the main window, whether to display this dialog in a sub-window. A value of true means the dialog is displayed in a sub-window.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var isModal

```cangjie
public var isModal: ?Bool
```

**Function:** Whether the dialog is a modal window. A value of true means it is a modal window with a mask layer, and cannot interact with other controls around the dialog, that is, events in the mask layer area cannot be passed through. A value of false means it is a non-modal window without a mask layer, and can interact with other controls around the dialog.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** Dialog background color.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Dialog background blur style.

**Type:** ?[BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Sets the shadow of the dialog background.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var enableHoverMode

```cangjie
public var enableHoverMode: ?Bool
```

**Function:** Whether to respond to hover state, when the value is true, it responds to hover state.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var hoverModeArea

```cangjie
public var hoverModeArea: ?HoverModeAreaType
```

**Function:** Sets the default display area of the dialog in hover mode.

**Type:** ?[HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var levelMode

```cangjie
public var levelMode: ?LevelMode
```

**Function:** Sets the display level of the dialog.

**Type:** ?[LevelMode](#enum-levelmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### init(?ResourceStr, ?ResourceStr, ?Array\<ButtonInfo\>, ?DialogAlignment, ?Offset, ?Rectangle, ?Bool, ?Bool, ?Color, ?BlurStyle, ?ShadowOptions, ?Bool, ?HoverModeAreaType, ?LevelMode)

```cangjie
public init(
    title!: ?ResourceStr = Option.None,
    message!: ?ResourceStr = Option.None,
    buttons!: ?Array<ButtonInfo> = Option.None,
    alignment!: ?DialogAlignment = Option.None,
    offset!: ?Offset = Option.None,
    maskRect!: ?Rectangle = Option.None,
    showInSubWindow!: ?Bool = Option.None,
    isModal!: ?Bool = Option.None,
    backgroundColor!: ?ResourceColor = Option.None,
    backgroundBlurStyle!: ?BlurStyle = Option.None,
    shadow!: ?ShadowOptions = Option.None,
    enableHoverMode!: ?Bool = Option.None,
    hoverModeArea!: ?HoverModeAreaType = Option.None,
    levelMode!: ?LevelMode = Option.None
)
```

**Function:** Constructor for dialog display options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | **Named parameter.** Title text. Default: "", when set to "" the title is not displayed by default.|
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | **Named parameter.** Content text. Default: "", when set to "" the content is not displayed by default.|
| buttons | ?Array\<[ButtonInfo](#class-buttoninfo)> | No | [] | **Named parameter.** Array of buttons in the dialog, supports more than 1 button.|
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | **Named parameter.** Vertical alignment of the dialog. Default: DialogAlignment.Default<br>**Note:**<br>If showInSubWindow is set to true in UIExtension, the dialog will align based on the UIExtension host window.|
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** Offset of the dialog relative to the alignment position.<br>Default: Offset(dx: 0.vp, dy: 0.vp).|
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | **Named parameter.** Dialog mask area, events within the mask area are not passed through, events outside the mask area are passed through.<br>Default: Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent)<br>**Note:** maskRect does not take effect when showInSubWindow is true.<br>If some properties of Rectangle are set and others are not, the default value for the unset properties is 0.|
| showInSubWindow | ?Bool | No | false | **Named parameter.** When a dialog needs to be displayed outside the main window, whether to display this dialog in a sub-window. When set to true, the dialog is displayed in a sub-window.<br>Default: false, the dialog is displayed within the application, not in an independent sub-window.<br>**Note:**<br>A dialog with showInSubWindow set to true cannot trigger the display of another dialog with showInSubWindow set to true.|
| isModal | ?Bool | No | true | **Named parameter.** Whether the dialog is a modal window. When set to true, it is a modal window with a mask layer and cannot interact with other controls around the dialog, meaning events in the mask layer area cannot be passed through. When set to false, it is a non-modal window without a mask layer and can interact with other controls around the dialog. Default: true.|
| backgroundColor | ?[Color](./cj-common-types.md#class-color) | No | Color.Transparent | **Named parameter.** Dialog background color. Default: Color.Transparent.|
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Dialog background blur style. Default: BlurStyle.ComponentUltraThick.|
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the dialog background.|
| enableHoverMode | ?Bool | No | false | **Named parameter.** Whether to respond to hover state. When set to true, it responds to hover state. Default: false, no response by default.|
| hoverModeArea | ?[HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | **Named parameter.** Sets the default display area of the dialog in hover mode. Default: HoverModeAreaType.BottomScreen.|
| levelMode | ?[LevelMode](#enum-levelmode) | No | Option.None | **Named parameter.** Sets the display level of the dialog.<br>**Note:**<br>Default: LevelMode.Overlay<br>Only takes effect when showInSubWindow property is set to false.|

## class ActionMenuConfig

```cangjie
public class ActionMenuConfig {
    public var title: ?ResourceStr
    public var buttons: ?Array<ButtonInfo>
    public var showInSubWindow: ?Bool
    public var isModal: ?Bool
    public var levelMode: ?LevelMode
    public init(
        title!: ?ResourceStr = Option.None,
        buttons!: ?Array<ButtonInfo> = Option.None,
        showInSubWindow!: ?Bool = Option.None,
        isModal!: ?Bool = Option.None,
        levelMode!: ?LevelMode = Option.None
    )
}
```

**Function:** Action menu configuration class, used to configure display options for action menus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var title

```cangjie
public var title: ?ResourceStr
```

**Function:** Title text.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var buttons

```cangjie
public var buttons: ?Array<ButtonInfo>
```

**Function:** Array of menu item buttons in the menu. Supports 1-6 buttons. When the number of buttons exceeds 6, only the first 6 buttons are displayed, and subsequent buttons are not displayed.

**Type:** ?Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** When an action menu needs to be displayed outside the main window, whether to display this menu in a sub-window. A value of true means the menu is displayed in a sub-window.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var isModal

```cangjie
public var isModal: ?Bool
```

**Function:** Whether the menu is a modal window. A value of true means it is a modal window with a mask layer, and cannot interact with other controls around the menu, that is, events in the mask layer area cannot be passed through. A value of false means it is a non-modal window without a mask layer, and can interact with other controls around the menu.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### var levelMode

```cangjie
public var levelMode: ?LevelMode
```

**Function:** Sets the display level of the menu.

**Type:** ?[LevelMode](#enum-levelmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### init(?ResourceStr, ?Array\<ButtonInfo>, ?Bool, ?Bool, ?LevelMode)

```cangjie
public init(
    title!: ?ResourceStr = Option.None,
    buttons!: ?Array<ButtonInfo> = Option.None,
    showInSubWindow!: ?Bool = Option.None,
    isModal!: ?Bool = Option.None,
    levelMode!: ?LevelMode = Option.None
)
```

**Function:** Constructor for action menu options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | **Named parameter.** Text title to display.|
| buttons | ?Array\<[ButtonInfo](#class-buttoninfo)> | Yes | - | **Named parameter.** Button array.|
| showInSubWindow | ?Bool | No | false | **Named parameter.** When an action menu needs to be displayed outside the main window, whether to display this menu in a sub-window. When set to true, the menu is displayed in a sub-window.<br>Default: false, the menu is not displayed in a sub-window.<br>**Note:** A menu with showInSubWindow set to true cannot trigger the display of another menu with showInSubWindow set to true.<br>If showInSubWindow is set to true in UIExtension, the menu will align based on the UIExtension host window.|
| isModal | ?Bool | No | true | **Named parameter.** Whether the menu is a modal window. When set to true, it is a modal window with a mask layer and cannot interact with other controls around the menu, meaning events in the mask layer area cannot be passed through. When set to false, it is a non-modal window without a mask layer and can interact with other controls around the menu. Default: true.|
| levelMode | ?[LevelMode](#enum-levelmode) | No | Option.None | **Named parameter.** Sets the display level of the popup.<br>**Note:**<br>Default: LevelMode.Overlay<br>Only takes effect when showInSubWindow property is set to false.|

## enum KeyboardAvoidMode

```cangjie
public enum KeyboardAvoidMode <: Equatable<KeyboardAvoidMode> {
    | Default
    | None
    | ...
}
```

**Function:** Provides keyboard avoidance modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[KeyboardAvoidMode](#enum-keyboardavoidmode)>

### Default

```cangjie
Default
```

**Function:** Default keyboard avoidance mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** No keyboard avoidance mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(KeyboardAvoidMode)

```cangjie
public operator func !=(other: KeyboardAvoidMode): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [KeyboardAvoidMode](#enum-keyboardavoidmode) | Yes | - | Another KeyboardAvoidMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when not equal. |

### operator func ==(KeyboardAvoidMode)

```cangjie
public operator func ==(other: KeyboardAvoidMode): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [KeyboardAvoidMode](#enum-keyboardavoidmode) | Yes | - | Another KeyboardAvoidMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when equal. |

## enum ToastShowMode

```cangjie
public enum ToastShowMode <: Equatable<ToastShowMode> {
    | Default
    | TopMost
    | ...
}
```

**Function:** Toast display mode enumeration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ToastShowMode](#enum-toastshowmode)>

### Default

```cangjie
Default
```

**Function:** Toast displays within the application.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopMost

```cangjie
TopMost
```

**Function:** Toast displays at the top.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(ToastShowMode)

```cangjie
public operator func !=(other: ToastShowMode): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ToastShowMode](#enum-toastshowmode) | Yes | - | Another ToastShowMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when not equal. |

### operator func ==(ToastShowMode)

```cangjie
public operator func ==(other: ToastShowMode): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ToastShowMode](#enum-toastshowmode) | Yes | - | Another ToastShowMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when equal. |

## enum LevelMode

```cangjie
public enum LevelMode <: Equatable<LevelMode> {
    | Overlay
    | Embedded
    | ...
}
```

**Function:** Popup display level mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parent Type:**

- Equatable\<[LevelMode](#enum-levelmode)>

### Overlay

```cangjie
Overlay
```

**Function:** The popup level is at the application window root node, and the popup does not hide when navigating within the application.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### Embedded

```cangjie
Embedded
```

**Function:** The popup node is under the page routing/navigation node, and the popup hides with the page when navigation changes.

**Note:**

1. Currently only supports mounting on Page or NavDestination nodes, with priority mounting on Page nodes, only supports top-level display within these two types of pages.

2. In this mode, new pages can cover the popup, and when returning from the page, the popup still exists and its content is not lost.

3. In this mode, ensure that the target page node (such as Page node) is mounted before showing the popup, otherwise the popup cannot be mounted to the corresponding page node.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

### operator func !=(LevelMode)

```cangjie
public operator func !=(other: LevelMode): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LevelMode](#enum-levelmode) | Yes | - | Another LevelMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when not equal. |

### operator func ==(LevelMode)

```cangjie
public operator func ==(other: LevelMode): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.0.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LevelMode](#enum-levelmode) | Yes | - | Another LevelMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true when equal. |

## type ShowDialogCallBack

```cangjie
public type ShowDialogCallBack = AsyncCallback<Int32>
```

**Function:** ShowDialogCallBack callback function.

**Type:** [AsyncCallback\<Int32>](../arkinterop/cj-api-business_exception.md#type-asynccallback)

## type ShowActionMenuCallBack

```cangjie
public type ShowActionMenuCallBack = AsyncCallback<Int32>
```

**Function:** ShowActionMenuCallBack callback function.

**Type:** [AsyncCallback\<Int32>](../arkinterop/cj-api-business_exception.md#type-asynccallback)
