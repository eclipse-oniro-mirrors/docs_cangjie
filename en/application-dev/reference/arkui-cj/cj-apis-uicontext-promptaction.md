# PromptAction

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

## class ActionMenuOptions

```cangjie
public open class ActionMenuOptions {
    public var buttons: Array<ButtonInfo>
    public var isModal: Bool
    public var showInSubWindow: Bool
    public var title: ResourceStr
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
    public var alignment: DialogAlignment
    public var autoCancel: Bool
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public var isModal: Bool
    public var keyboardAvoidMode: KeyboardAvoidMode
    public var maskColor: ResourceColor
    public var maskRect: Rectangle
    public var offset: Offset
    public var onDidAppear: () -> Unit
    public var onDidDisappear: () -> Unit
    public var onWillAppear: () -> Unit
    public var onWillDisappear: () -> Unit
    public var showInSubWindow: Bool
    public var transition: TransitionEffect
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
    public var color: ResourceColor
    public var primary: Bool
    public var text: ResourceStr
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
    public var backgroundColor: ResourceColor
    public var borderColor: EdgeColors
    public var borderRadius: BorderRadiuses
    public var borderStyle: EdgeStyles
    public var borderWidth: EdgeWidths
    public var builder: () -> Unit
    public var backgroundBlurStyle: BlurStyle
    public var height: Length
    public var shadow: ?ShadowOptions
    public var width: Length
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
    public var bottom: ResourceColor
    public var left: ResourceColor
    public var right: ResourceColor
    public var top: ResourceColor
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
    public var alignment: DialogAlignment
    public var backgroundColor: ResourceColor
    public var backgroundBlurStyle: BlurStyle
    public var buttons: Array<ButtonInfo>
    public var buttonsSize: UInt32
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public var isModal: Bool
    public var maskRect: Rectangle
    public var message: ResourceStr
    public var offset: Offset
    public var shadow: ?ShadowOptions
    public var showInSubWindow: Bool
    public var title: ResourceStr
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
    public var alignment: Alignment
    public var backgroundColor: ResourceColor
    public var bottom: Length
    public var duration: UInt32
    public var enableHoverMode: Bool
    public var hoverModeArea: HoverModeAreaType
    public var message: ResourceStr
    public var offset: Offset
    public var backgroundBlurStyle: BlurStyle
    public var shadow: ?ShadowOptions = None
    public var showMode: ToastShowMode
    public var textColor: ResourceColor
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

## type ShowDialogCallBack

```cangjie
public type ShowDialogCallBack = AsyncCallback<Int32>
```

**Function:** ShowDialogCallBack callback function.

**Type:** [AsyncCallback\<Int32>](../arkinterop/cj-api-business_exception.md#type-asynccallback)

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## type ShowActionMenuCallBack

```cangjie
public type ShowActionMenuCallBack = AsyncCallback<Int32>
```

**Function:** ShowActionMenuCallBack callback function.

**Type:** [AsyncCallback\<Int32>](../arkinterop/cj-api-business_exception.md#type-asynccallback)

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22
