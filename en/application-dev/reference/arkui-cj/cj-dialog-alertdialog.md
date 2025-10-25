# AlertDialog

Displays an alert dialog component, allowing configuration of text content and response callbacks.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Basic Type Definitions

### class AlertDialogButtonBaseOptions

```cangjie
public open class AlertDialogButtonBaseOptions {
    public var enabled: Bool
    public var defaultFocus: Bool
    public var style: DialogButtonStyle
    public var value: ResourceStr
    public var fontColor:?ResourceColor
    public var backgroundColor:?ResourceColor
    public var action: VoidCallback
    public init(
        enabled!: Bool = true,
        defaultFocus!: Bool = false,
        style!: DialogButtonStyle = DialogButtonStyle.Default,
        value!: ResourceStr,
        fontColor!: ?ResourceColor = None,
        backgroundColor!: ?ResourceColor = None,
        action!: VoidCallback
    )
}
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var action

```cangjie
public var action: VoidCallback
```

**Function:** Callback when the button is selected.

**Type:** VoidCallback

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundColor

```cangjie
public var backgroundColor:?ResourceColor
```

**Function:** Background color of the button.

**Type:** ?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var defaultFocus

```cangjie
public var defaultFocus: Bool
```

**Function:** Sets whether the button is the default focus.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var enabled

```cangjie
public var enabled: Bool
```

**Function:** Determines whether the button responds to clicks.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var fontColor

```cangjie
public var fontColor:?ResourceColor
```

**Function:** Text color of the button.

**Type:** ?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var style

```cangjie
public var style: DialogButtonStyle
```

**Function:** Sets the style of the button.

**Type:** DialogButtonStyle

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var value

```cangjie
public var value: ResourceStr
```

**Function:** Determines whether the button responds to clicks.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Bool, Bool, DialogButtonStyle, ResourceStr, ?ResourceColor, ?ResourceColor, VoidCallback)

```cangjie
public init(
    enabled!: Bool = true,
    defaultFocus!: Bool = false,
    style!: DialogButtonStyle = DialogButtonStyle.Default,
    value!: ResourceStr,
    fontColor!: ?ResourceColor = None,
    backgroundColor!: ?ResourceColor = None,
    action!: VoidCallback
)
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|enabled|Bool|No|true| **Named parameter.** Determines whether the button responds to clicks. |
|defaultFocus|Bool|No|false| **Named parameter.** Sets whether the button is the default focus. |
|style|DialogButtonStyle|No|DialogButtonStyle.Default| **Named parameter.** Sets the style of the button. |
|value|[ResourceStr](./cj-common-types.md#interface-resourcestr)|Yes|-| **Named parameter.** Text content of the button. |
|fontColor|?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)|No|None| **Named parameter.** Text color of the button. |
|backgroundColor|?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)|No|None| **Named parameter.** Background color of the button. |
|action|VoidCallback|Yes|-| **Named parameter.** Callback when the button is selected. |

### class AlertDialogButtonOptions

```cangjie
public class AlertDialogButtonOptions <: AlertDialogButtonBaseOptions {
    public var primary: Bool
    public init(
        enabled!: Bool = true,
        defaultFocus!: Bool = false,
        style!: DialogButtonStyle = DialogButtonStyle.Default,
        value!: ResourceStr,
        fontColor!: ?ResourceColor = None,
        backgroundColor!: ?ResourceColor = None,
        action!: VoidCallback,
        primary!: Bool = false
    )
}
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

#### var primary

```cangjie
public var primary: Bool
```

**Function:** Determines whether the button responds to the Enter key by default when the dialog is focused and no tab key navigation has occurred. For multiple buttons, only one button can have this field set to true; otherwise, none will respond. Nested dialogs can automatically focus and respond continuously. Does not take effect when defaultFocus is true.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Bool, Bool, DialogButtonStyle, ResourceStr, ?ResourceColor, ?ResourceColor, VoidCallback, Bool)

```cangjie
public init(
    enabled!: Bool = true,
    defaultFocus!: Bool = false,
    style!: DialogButtonStyle = DialogButtonStyle.Default,
    value!: ResourceStr,
    fontColor!: ?ResourceColor = None,
    backgroundColor!: ?ResourceColor = None,
    action!: VoidCallback,
    primary!: Bool = false
)
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|enabled|Bool|No|true| **Named parameter.** Determines whether the button responds to clicks. |
|defaultFocus|Bool|No|false| **Named parameter.** Sets whether the button is the default focus. |
|style|DialogButtonStyle|No|DialogButtonStyle.Default| **Named parameter.** Sets the style of the button. |
|value|[ResourceStr](./cj-common-types.md#interface-resourcestr)|Yes|-| **Named parameter.** Text content of the button. |
|fontColor|?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)|No|None| **Named parameter.** Text color of the button. |
|backgroundColor|?[ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)|No|None| **Named parameter.** Background color of the button. |
|action|VoidCallback|Yes|-| **Named parameter.** Callback when the button is selected. |
|primary|Bool|No|false| **Named parameter.** Determines whether the button responds to the Enter key by default when the dialog is focused and no tab key navigation has occurred. For multiple buttons, only one button can have this field set to true; otherwise, none will respond. Nested dialogs can automatically focus and respond continuously. Does not take effect when defaultFocus is true.|

### class AlertDialogParam

```cangjie
public open class AlertDialogParam {
    public var title: ResourceStr
    public var subtitle: ResourceStr
    public var message: ResourceStr
    public var autoCancel: Bool
    public var cancel: VoidCallback
    public var alignment: DialogAlignment
    public var offset: Offset
    public var gridCount: UInt32
    public var maskRect: Rectangle
    public var showInSubWindow: Bool
    public var isModal: Bool
    public var backgroundColor: ResourceColor
    public var backgroundBlurStyle: BlurStyle
    public var onWillDismiss:?Callback<DismissDialogAction, Unit>
    public var cornerRadius: BorderRadiuses
    public var transition:?TransitionEffect
    public var width:?Length
    public var height:?Length
    public var borderWidth: Length
    public var borderColor: ResourceColor
    public var borderStyle: EdgeStyles
    public var shadow: ShadowOptions
    public var textStyle: WordBreak
    public init(
        title!: ResourceStr = "",
        subtitle!:ResourceStr = "",
        message!: ResourceStr,
        autoCancel!: Bool = true,
        cancel!: VoidCallback = {=>},
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0, 0),
        gridCount!: UInt32 = 4,
        maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
        showInSubWindow!: Bool = false,
        isModal!: Bool = true,
        backgroundColor!: ResourceColor = Color.Transparent,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
            bottomRight: 32.vp),
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: Length = 0,
        borderColor!: ResourceColor = Color.Black,
        borderStyle!: EdgeStyles = EdgeStyles(),
        shadow!: ShadowOptions = ShadowOptions(radius: 0.0),
        textStyle!: WordBreak = WordBreak.BreakAll
    )
}
```

**Function:** Defines an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Function:** Vertical alignment of the dialog.

**Type:** DialogAlignment

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var autoCancel

```cangjie
public var autoCancel: Bool
```

**Function:** Determines whether the dialog closes when the mask layer is clicked.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Blur material for the dialog's background panel.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Background color of the dialog.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var borderColor

```cangjie
public var borderColor: ResourceColor
```

**Function:** Sets the border color of the dialog's background panel. If using borderColor, it must be used together with borderWidth.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var borderStyle

```cangjie
public var borderStyle: EdgeStyles
```

**Function:** Sets the border style of the dialog's background panel. If using borderStyle, it must be used together with borderWidth.

**Type:** [EdgeStyles](./cj-common-types.md#class-edgestyles)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var borderWidth

```cangjie
public var borderWidth: Length
```

**Function:** Sets the border width of the dialog's background panel.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var cancel

```cangjie
public var cancel: VoidCallback
```

**Function:** Callback when the dialog is closed by clicking the mask layer.

**Type:** VoidCallback

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var cornerRadius

```cangjie
public var cornerRadius: BorderRadiuses
```

**Function:** Sets the corner radius of the background panel. Can set the radius for each of the four corners separately.

**Type:** [BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var gridCount

```cangjie
public var gridCount: UInt32
```

**Function:** Number of grid columns occupied by the dialog container's width.

**Type:** UInt32

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var height

```cangjie
public var height:?Length
```

**Function:** Sets the height of the dialog's background panel.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Determines whether the dialog is a modal window. Modal windows have a mask layer; non-modal windows do not.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** Mask layer area of the dialog. Events within the mask layer area are not passed through; events outside are passed through.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle>)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var message

```cangjie
public var message: ResourceStr
```

**Function:** Content of the dialog.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offset

```cangjie
public var offset: Offset
```

**Function:** Offset of the dialog relative to the alignment position.

**Type:** Offset

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var onWillDismiss

```cangjie
public var onWillDismiss:?Callback<DismissDialogAction, Unit>
```

**Function:** Interactive close callback function.

**Type:** ?Callback\<DismissDialogAction,Unit>

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Determines whether the dialog is displayed in a sub-window when it needs to appear outside the main window.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var subtitle

```cangjie
public var subtitle: ResourceStr
```

**Function:** Subtitle of the dialog.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var shadow

```cangjie
public var shadow: ShadowOptions
```

**Function:** Sets the shadow of the dialog's background panel.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var textStyle

```cangjie
public var textStyle: WordBreak
```

**Function:** Sets the text style of the dialog's message content.

**Type:** WordBreak

**Read-Write Permission:** Readable### class AlertDialogParamWithButtons

```cangjie
public class AlertDialogParamWithButtons <: AlertDialogParam {
    public var primaryButton: AlertDialogButtonBaseOptions
    public var secondaryButton: AlertDialogButtonBaseOptions
    public init(
        title!: ResourceStr = "",
        subtitle!:ResourceStr = "",
        message!: ResourceStr,
        autoCancel!: Bool = true,
        cancel!: VoidCallback = {=>},
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0, 0),
        gridCount!: UInt32 = 4,
        maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
        showInSubWindow!: Bool = false,
        isModal!: Bool = true,
        backgroundColor!: ResourceColor = Color.Transparent,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
            bottomRight: 32.vp),
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: Length = 0,
        borderColor!: ResourceColor = Color.Black,
        borderStyle!: EdgeStyles = EdgeStyles(),
        textStyle!: WordBreak = WordBreak.BreakAll,
        primaryButton!: AlertDialogButtonBaseOptions,
        secondaryButton!: AlertDialogButtonBaseOptions
    )
}
```

**Function:** Defines an alert dialog with two confirmation buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [AlertDialogParam](#class-alertdialogparam)

#### var primaryButton

```cangjie
public var primaryButton: AlertDialogButtonBaseOptions
```

**Function:** Specifies the enabled state, default focus, button style, text content, text color, button background color, and click callback of the primary confirmation button.

**Type:** [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var secondaryButton

```cangjie
public var secondaryButton: AlertDialogButtonBaseOptions
```

**Function:** Specifies the enabled state, default focus, button style, text content, text color, button background color, and click callback of the secondary confirmation button.

**Type:** [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(ResourceStr, ResourceStr, ResourceStr, Bool, VoidCallback, DialogAlignment, Offset, UInt32, Rectangle, Bool, Bool, ResourceColor, BlurStyle, ?Callback\<DismissDialogAction,Unit>, BorderRadiuses, ?TransitionEffect, ?Length, ?Length, Length, ResourceColor, EdgeStyles, WordBreak, AlertDialogButtonBaseOptions, AlertDialogButtonBaseOptions)

```cangjie
public init(
    title!: ResourceStr = "",
    subtitle!:ResourceStr = "",
    message!: ResourceStr,
    autoCancel!: Bool = true,
    cancel!: VoidCallback = {=>},
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0, 0),
    gridCount!: UInt32 = 4,
    maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
    showInSubWindow!: Bool = false,
    isModal!: Bool = true,
    backgroundColor!: ResourceColor = Color.Transparent,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
        bottomRight: 32.vp),
    transition!: ?TransitionEffect = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: Length = 0,
    borderColor!: ResourceColor = Color.Black,
    borderStyle!: EdgeStyles = EdgeStyles(),
    textStyle!: WordBreak = WordBreak.BreakAll,
    primaryButton!: AlertDialogButtonBaseOptions,
    secondaryButton!: AlertDialogButtonBaseOptions
)
```

**Function:** Defines an alert dialog with two confirmation buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** Dialog title. |
| subtitle | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** Dialog subtitle. |
| message | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Dialog content. |
| autoCancel | Bool | No | true | **Named parameter.** Whether to close the dialog when clicking the mask layer. true means close the dialog, false means do not close the dialog. |
| cancel | VoidCallback | No | { => } | **Named parameter.** Callback when the dialog is closed by clicking the mask layer. |
| alignment | DialogAlignment | No | DialogAlignment.Default | **Named parameter.** Vertical alignment of the dialog. |
| offset | Offset | No | Offset(0, 0) | **Named parameter.** Offset of the dialog relative to the alignment position. |
| gridCount | UInt32 | No | 4 | **Named parameter.** Number of grid columns occupied by the dialog container width. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle>) | No | Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) | **Named parameter.** Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside the mask layer area are transmitted.<br/>**Note:**<br/>maskRect does not take effect when showInSubWindow is true. |
| showInSubWindow | Bool | No | false | **Named parameter.** Whether to display the dialog in a sub-window when it needs to be displayed outside the main window.<br/>Initial value: false, the dialog is displayed within the application, not in an independent sub-window.<br/>**Note:** A dialog with showInSubWindow set to true cannot trigger another dialog with showInSubWindow set to true. |
| isModal | Bool | No | true | **Named parameter.** Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not.<br/>Initial value: true, the dialog has a mask layer. |
| backgroundColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Transparent | **Named parameter.** Background color of the dialog.<br/>**Note:** <br/>When backgroundColor is set to a non-transparent color, backgroundBlurStyle should be set to BlurStyle.NONE; otherwise, the color display may not meet expectations. |
| backgroundBlurStyle | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Background blur material of the dialog.<br/>**Note:** <br/>Set to BlurStyle.NONE to disable background blur. When backgroundBlurStyle is set to a non-NONE value, do not set backgroundColor; otherwise, the color display may not meet expectations. |
| onWillDismiss | ?Callback\<DismissDialogAction,Unit> | No | None | **Named parameter.** Interactive close callback function.<br/>**Note:**<br/>1. When the user performs operations like clicking the mask layer to close, swiping left/right, pressing the back key, or pressing the ESC key to close the dialog, if this callback is registered, the dialog will not close immediately. The callback function can determine whether to close the dialog based on the operation type obtained from reason. Currently, the reason returned by this component does not support the CLOSE_BUTTON enumeration value.<br/>2. In the onWillDismiss callback, onWillDismiss interception cannot be performed again. |
| cornerRadius | [BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) | **Named parameter.** Sets the corner radius of the background panel.<br />The radius of each corner can be set separately.<br />The corner radius is limited by the component size, with the maximum value being half of the component width or height. Negative values are treated as default values.<br />Percentage parameter method: Sets the corner radius of the dialog as a percentage of the parent dialog's width and height.<br/>**Note:**<br/>When the cornerRadius property type is LocalizedBorderRadiuses, it supports changing the layout order according to language habits. |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for dialog display and exit.<br/>**Note:**<br/> 1. If not set, the default display/exit animation is used.<br/> 2. Pressing the back key during the display animation interrupts the display animation and executes the exit animation. The animation effect is a superposition of the display and exit animation curves.<br/> 3. Pressing the back key during the exit animation does not interrupt the exit animation. The exit animation continues, and pressing the back key again exits the application. |
| width | ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | None | **Named parameter.** Sets the width of the dialog background panel.<br />**Note:**<br>- Default maximum width of the dialog: None.<br />- Percentage parameter method: Adjusts the dialog width based on the window width. |
| height | ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | None | **Named parameter.** Sets the height of the dialog background panel.<br />**Note:**<br />- Default maximum height of the dialog: None.<br />- Percentage parameter method: Adjusts the dialog height based on (window height - safe area). |
| borderWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0 | **Named parameter.** Sets the width of each border separately.<br />Percentage parameter method: Sets the border width of the dialog as a percentage of the parent dialog's width.<br />When the left and right borders exceed the dialog width, or the top and bottom borders exceed the dialog height, the display may not meet expectations.<br/>**Note:**<br/>When the borderWidth property type is LocalizedEdgeWidths, it supports changing the layout order according to language habits. |
| borderColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Sets the border color of the dialog background panel.<br/> If the borderColor property is used, it must be used together with the borderWidth property.<br/>**Note:**<br/>When the borderColor property type is LocalizedEdgeColors, it supports changing the layout order according to language habits. |
| borderStyle | [EdgeStyles](./cj-common-types.md#class-edgestyles) | No | EdgeStyles() | **Named parameter.** Sets the border style of the dialog background panel.<br/>If the borderStyle property is used, it must be used together with the borderWidth property. |
| textStyle | WordBreak | No | WordBreak.BreakAll | **Named parameter.** Sets the text style of the dialog message content. |
| primaryButton | [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions) | Yes | - | **Named parameter.** Specifies the enabled state, default focus, button style, text content, text color, button background color, and click callback of the primary confirmation button. |
| secondaryButton | [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions) | Yes | - | **Named parameter.** Specifies the enabled state, default focus, button style, text content, text color, button background color, and click callback of the secondary confirmation button. |

### class AlertDialogParamWithConfirm

```cangjie
public class AlertDialogParamWithConfirm <: AlertDialogParam {
    public var confirm: AlertDialogButtonBaseOptions
    public init(
        title!: ResourceStr = "",
        subtitle!:ResourceStr = "",
        message!: ResourceStr,
        autoCancel!: Bool = true,
        cancel!: VoidCallback = {=>},
        alignment!: DialogAlignment = DialogAlignment.Default,
        offset!: Offset = Offset(0, 0),
        gridCount!: UInt32 = 4,
        maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
        showInSubWindow!: Bool = false,
        isModal!: Bool = true,
        backgroundColor!: ResourceColor = Color.Transparent,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
            bottomRight: 32.vp),
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: Length = 0,
        borderColor!: ResourceColor = Color.Black,
        borderStyle!: EdgeStyles = EdgeStyles(),
        textStyle!: WordBreak = WordBreak.BreakAll,
        confirm!: AlertDialogButtonBaseOptions = AlertDialogButtonOptions(value: "", action: {=>})
    )
}
```

**Function:** Defines an alert dialog with a confirmation button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [AlertDialogParam](#class-alertdialogparam)

#### var confirm

```cangjie
public var confirm: AlertDialogButtonBaseOptions
```

**Function:** Specifies the enabled state, default focus, button style, text content, text color, button background color, and click callback of the confirmation button.

**Type:** [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(ResourceStr, ResourceStr, ResourceStr, Bool, VoidCallback, DialogAlignment, Offset, UInt32, Rectangle, Bool, Bool, ResourceColor, BlurStyle, ?Callback\<DismissDialogAction,Unit>, BorderRadiuses, ?TransitionEffect, ?Length, ?Length, Length, ResourceColor, EdgeStyles, WordBreak, AlertDialogButtonBaseOptions)

```cangjie
public init(
    title!: ResourceStr = "",
    subtitle!:ResourceStr = "",
    message!: ResourceStr,
    autoCancel!: Bool = true,
    cancel!: VoidCallback = {=>},
    alignment!: DialogAlignment = DialogAlignment.Default,
    offset!: Offset = Offset(0, 0),
    gridCount!: UInt32 = 4,
    maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
    showInSubWindow!: Bool = false,
    isModal!: Bool = true,
    backgroundColor!: ResourceColor = Color.Transparent,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp,
        bottomRight: 32.vp),
    transition!: ?TransitionEffect = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: Length = 0,
    borderColor!: ResourceColor = Color.Black,
    borderStyle!: EdgeStyles = EdgeStyles(),
    textStyle!: WordBreak = WordBreak.BreakAll,
    confirm!: AlertDialogButtonBaseOptions = AlertDialogButtonOptions(value: "", action: {=>})
)
```

**Function:** Defines an alert dialog with a confirmation button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** Dialog title. |
| subtitle | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** Dialog subtitle. |
| message | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Dialog content. |
| autoCancel | Bool | No | true | **Named parameter.** Whether to close the dialog when clicking the mask layer. true means close the dialog, false means do not close the dialog. |
| cancel | VoidCallback | No | { => } | **Named parameter.** Callback when the dialog is closed by clicking the mask layer. |
| alignment | DialogAlignment | No | DialogAlignment.Default | **Named parameter.** Vertical alignment of the dialog. |
| offset | Offset | No | Offset(0, 0) | **Named parameter.** Offset of the dialog relative to the alignment position. |
| gridCount | UInt32 | No | 4 | **Named parameter.** Number of grid columns occupied by the dialog container width. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle>) | No | Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) | **Named parameter.** Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside## Sample Code

### Example 1 (Dialog with Multiple Buttons)

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        Column(space:5.vp) {
            Button("one button dialog")
                .onClick({ evt =>
                        AlertDialogParamWithConfirm(message:"text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")}, alignment: DialogAlignment.Center,
                            offset: Offset(0, -20), gridCount: 4,
                            onWillDismiss: {
                                dismissDialogAction: DismissDialogAction => match (dismissDialogAction.reason) {
                                    case PRESS_BACK => dismissDialogAction.dismiss()
                                    case TOUCH_OUTSIDE => dismissDialogAction.dismiss()
                                    case _ => ()
                                }
                            },
                            confirm: AlertDialogButtonOptions(value: "button",
                                action: {=> Hilog.info(0, "AppLogCj", "Button-clicking callback")}))
                })
            .backgroundColor(0x317aff)
            Button("two button dialog")
                .onClick({ evt =>
                        AlertDialogParamWithButtons(message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")},
                            alignment: DialogAlignment.Center,
                            offset: Offset(0, -20), gridCount: 4,
                            onWillDismiss: {
                                dismissDialogAction: DismissDialogAction => match (dismissDialogAction.reason) {
                                    case PRESS_BACK => dismissDialogAction.dismiss()
                                    case TOUCH_OUTSIDE => dismissDialogAction.dismiss()
                                    case _ => ()
                                }
                            },
                            primaryButton: AlertDialogButtonOptions(value: "Cancel",
                                action: {=> Hilog.info(0, "AppLogCj", "Callback when second button is clicked")}),
                            secondaryButton: AlertDialogButtonOptions(enabled: true, defaultFocus: true,
                                style: DialogButtonStyle.Highlight, value: "OK",
                                action: {=> Hilog.info(0, "AppLogCj", "Callback when second button is clicked")}))
                })
            .backgroundColor(0x317aff)
            Button("three button dialog")
                .onClick({ evt =>
                        AlertDialogParamWithOptions(
                            message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Callback when third button is clicked")},
                            alignment: DialogAlignment.Center,
                            offset: Offset(0, -20),
                            gridCount: 4,
                            onWillDismiss: {
                                dismissDialogAction: DismissDialogAction => match (dismissDialogAction.reason) {
                                    case PRESS_BACK => dismissDialogAction.dismiss()
                                    case TOUCH_OUTSIDE => dismissDialogAction.dismiss()
                                    case _ => ()
                                }
                            },
                            buttons: [
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")}),
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")}),
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")})
                            ]
                        )
                })
                .backgroundColor(0x317aff)
        }
    }
}
```

!alertdialog1

### Example 2 (Dialog That Can Pop Up Outside the Main Window)

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 5.vp) {
            Button("button dialog")
                .onClick({ evt =>
                        AlertDialogParamWithOptions(
                            message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")},
                            alignment: DialogAlignment.Center,
                            offset: Offset(0, -20),
                            showInSubWindow: true,
                            buttonDirection: DialogButtonDirection.Horizontal,
                            gridCount: 4,
                            onWillDismiss: {
                                dismissDialogAction: DismissDialogAction => match (dismissDialogAction.reason) {
                                    case PRESS_BACK => dismissDialogAction.dismiss()
                                    case TOUCH_OUTSIDE => dismissDialogAction.dismiss()
                                    case _ => ()
                                }
                            },
                            buttons: [
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")}),
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")}),
                                AlertDialogButtonOptions(value: "Button",
                                    action: {=> Hilog.info(0, "AppLogCj", "Callback when button1 is clicked")})
                            ]
                        )
                })
                .backgroundColor(0x317aff)
        }
    }
}

```

!alertdialog2