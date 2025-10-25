# Custom Dialog (CustomDialog)

Display custom dialogs using the CustomDialogController class. When using dialog components, custom dialogs should be prioritized for easier customization of dialog styles and content.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class CustomDialogController

```cangjie
public class CustomDialogController {
    public init(value: CustomDialogControllerOptions)
}
```

**Function:** Constructs an object of type CustomDialogController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(CustomDialogControllerOptions)

```cangjie
public init(value: CustomDialogControllerOptions)
```

**Function:** Creates a constructor for custom dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [CustomDialogControllerOptions](#class-customdialogcontrolleroptions) | Yes | - | Parameters for configuring the custom dialog. |

### func bindView(CustomView)

```cangjie
public func bindView(view: CustomView)
```

**Function:** Binds a CustomView to the custom dialog builder. Users do not need to call this explicitly; it is implicitly invoked after macro expansion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| view | [CustomView](./cj-ui-framework.md#class-customview) | Yes | - | The CustomView to be bound. |

### func closeDialog()

```cangjie
public func closeDialog()
```

**Function:** Closes the displayed custom dialog. If already closed, this has no effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func openDialog()

```cangjie
public func openDialog()
```

**Function:** Displays the custom dialog content. Can be called multiple times, but if the dialog is in SubWindow mode, it cannot spawn another SubWindow dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func releaseSelf()

```cangjie
public func releaseSelf(): Unit
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func setBuilder(() -> Unit)

```cangjie
public func setBuilder(builder: () -> Unit)
```

**Function:** Sets a builder function. Users do not need to call this explicitly; it is implicitly invoked after macro expansion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| builder | ()->Unit | Yes | - | The rendering function corresponding to the builder. |

## class CustomDialogControllerOptions

```cangjie
public class CustomDialogControllerOptions {
    public var cancel: VoidCallback
    public var autoCancel: Bool
    public var alignment: DialogAlignment
    public var offset: Offset
    public var customStyle: Bool
    public var gridCount:?UInt32
    public var maskColor: ResourceColor
    public var maskRect: Rectangle
    public var openAnimation:?AnimateParam
    public var closeAnimation:?AnimateParam
    public var showInSubWindow: Bool
    public var backgroundColor: ResourceColor
    public var cornerRadius: Length
    public var isModal: Bool
    public var onWillDismiss:?Callback<DismissDialogAction, Unit>
    public var borderWidth: Length
    public var borderColor: ResourceColor
    public var borderStyle: EdgeStyles
    public var width:?Length
    public var height:?Length
    public var shadow:?ShadowOptions
    public var backgroundBlurStyle: BlurStyle
    public init(
        cancel!: VoidCallback = {=>},
        autoCancel!: Bool = true,
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0.vp, 0.vp),
        customStyle!: Bool = false,
        gridCount!: ?UInt32 = None,
        maskColor!: ResourceColor = Color(0x33000000),
        maskRect!: Rectangle = Rectangle(),
        openAnimation!: ?AnimateParam = None,
        closeAnimation!: ?AnimateParam = None,
        showInSubWindow!: Bool = false,
        backgroundColor!: ResourceColor = Color.Transparent,
        cornerRadius!: Length = 32.vp,
        isModal!: Bool = true,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        borderWidth!: Length = 0.vp,
        borderColor!: ResourceColor = Color.Black,
        borderStyle!: EdgeStyles = EdgeStyles(),
        width!: ?Length = None,
        height!: ?Length = None,
        shadow!: ?ShadowOptions = None,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick
    )
}
```

**Function:** Declares parameters related to custom dialog settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Function:** The vertical alignment of the dialog.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var autoCancel

```cangjie
public var autoCancel: Bool
```

**Function:** Whether clicking the mask layer closes the dialog. `true` means the dialog will close, `false` means it will not.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** The blur material for the dialog's background panel.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Sets the background fill color of the dialog.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderColor

```cangjie
public var borderColor: ResourceColor
```

**Function:** Sets the border color of the dialog's background panel.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderStyle

```cangjie
public var borderStyle: EdgeStyles
```

**Function:** Sets the border style of the dialog's background panel.

**Type:** [EdgeStyles](./cj-common-types.md#class-edgestyles)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderWidth

```cangjie
public var borderWidth: Length
```

**Function:** Sets the border width of the dialog's background panel.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var cancel

```cangjie
public var cancel: VoidCallback
```

**Function:** Callback triggered when the dialog is closed via back button, ESC key, or mask layer click.

**Type:** [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var closeAnimation

```cangjie
public var closeAnimation:?AnimateParam
```

**Function:** Customizes the animation parameters for dialog closing.

**Type:** ?[AnimateParam](./cj-common-types.md#class-animateparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var cornerRadius

```cangjie
public var cornerRadius: Length
```

**Function:** Sets the corner radius of the background panel.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var customStyle

```cangjie
public var customStyle: Bool
```

**Function:** Whether the dialog container style is customized.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var gridCount

```cangjie
public var gridCount:?UInt32
```

**Function:** The number of grid widths occupied by the dialog.

**Type:** ?UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var height

```cangjie
public var height:?Length
```

**Function:** Sets the height of the dialog's background panel.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Whether the dialog is a modal window. Modal windows have a mask layer; non-modal windows do not.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskColor

```cangjie
public var maskColor: ResourceColor
```

**Function:** Customizes the mask layer color.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** The mask layer area of the dialog. Events within this area are not passed through; events outside are passed through.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var offset

```cangjie
public var offset: Offset
```

**Function:** The offset of the dialog relative to its alignment position.

**Type:** [Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onWillDismiss

```cangjie
public var onWillDismiss:?Callback<DismissDialogAction, Unit>
```

**Function:** Interactive close callback function.

**Type:** ?[Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction),Unit>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var openAnimation

```cangjie
public var openAnimation:?AnimateParam
```

**Function:** Customizes the animation parameters for dialog opening.

**Type:** ?[AnimateParam](./cj-common-types.md#class-animateparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var shadow

```cangjie
public var shadow:?ShadowOptions
```

**Function:** Sets the shadow of the dialog's background panel.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Whether to display the dialog in a sub-window when it needs to appear outside the main window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var width

```cangjie
public var width:?Length
```

**Function:** Sets the width of the dialog's background panel.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(VoidCallback, Bool, DialogAlignment, Offset, Bool, ?UInt32, ResourceColor, Rectangle, ?AnimateParam, ?AnimateParam, Bool, ResourceColor, Length, Bool, ?Callback\<DismissDialogAction,Unit>, Length, ResourceColor, EdgeStyles, ?Length, ?Length, ?ShadowOptions, BlurStyle)

```cangjie
public init(
    cancel!: VoidCallback = {=>},
    autoCancel!: Bool = true,
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0.vp, 0.vp),
    customStyle!: Bool = false,
    gridCount!: ?UInt32 = None,
    maskColor!: ResourceColor = Color(0x33000000),
    maskRect!: Rectangle = Rectangle(),
    openAnimation!: ?AnimateParam = None,
    closeAnimation!: ?AnimateParam = None,
    showInSubWindow!: Bool = false,
    backgroundColor!: ResourceColor = Color.Transparent,
    cornerRadius!: Length = 32.vp,
    isModal!: Bool = true,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    borderWidth!: Length = 0.vp,
    borderColor!: ResourceColor = Color.Black,
    borderStyle!: EdgeStyles = EdgeStyles(),
    width!: ?Length = None,
    height!: ?Length = None,
    shadow!: ?ShadowOptions = None,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick
)
```

**Function:** Creates a CustomDialogControllerOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| cancel | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | No | { => } | **Named parameter.** Callback triggered when the dialog is closed via back button, ESC key, or mask layer click. |
| autoCancel | Bool | No | true | **Named parameter.** Whether clicking the mask layer closes the dialog. `true` means the dialog will close. `false` means it will not. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | **Named parameter.** The vertical alignment of the dialog. |
| offset | [Offset](./cj-common-types.md#class-offset) | No | Offset(0.vp, 0.vp) | **Named parameter.** The offset of the dialog relative to its alignment position. |
| customStyle | Bool | No | false | **Named parameter.** Whether the dialog container style is customized.<br>When set to `false` (default):<br/>1. Corner radius is 32.vp.<br/>2. If dialog width/height is not set: The dialog width adapts to the grid system, and the height adapts to the custom content node.<br/>3. If dialog width/height is set: The dialog width does not exceed the maximum width in default style (custom node sets 100% width), and the height does not exceed the maximum height in default style (custom node sets 100% height).<br/>When set to `true`:<br/>1. Corner radius is 0, and the background color is transparent.<br/>2. Dialog width, height, border width, border style, border color, and shadow width cannot be set. |
| gridCount | ?UInt32 | No | None | **Named parameter.** The number of grid widths occupied by the dialog.<br>Defaults to adaptive based on window size. Invalid values are treated as defaults, with the maximum grid count being the system's maximum. |
| maskColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color(0x33000000) | **Named parameter.** Customizes the mask layer color. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle() | **Named parameter.** The mask layer area of the dialog. Events within this area are not passed through; events outside are passed through. <br/>**Note:**<br/>`maskRect` does not take effect when `showInSubWindow` is `true`. |
| openAnimation | ?[AnimateParam](./cj-common-types.md#class-animateparam) | No | None | **Named parameter.** Customizes the animation parameters for dialog opening.<br>**Note:**<br>`tempo` defaults to 1## Sample Code

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@CustomDialog
class MyDialog {
    var controller: Option<CustomDialogController> = Option.None
    func build() {
        Row(space: 60) {
            Button("cancel").onClick { evt =>
                controller?.releaseSelf()
            }

            Button("confirm").onClick { evt =>
                controller?.releaseSelf()
            }
        }.height(500.px)
    }
}

@Entry
@Component
class EntryView {
    var dialogController: CustomDialogController = CustomDialogController(CustomDialogControllerOptions(builder: MyDialog()))
    func build() {
        Column {
            Button("open dialog").onClick({evt =>
                dialogController.openDialog()
            })
        }
    }
}

```

![custom_dialog](./figures/custom_dialog.png)