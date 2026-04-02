# Alert Dialog (AlertDialog)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Displays an alert dialog component, allowing configuration of text content and response callbacks.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class AlertDialogButtonBaseOptions

```cangjie
public open class AlertDialogButtonBaseOptions {
    public var enabled: ?Bool
    public var defaultFocus: ?Bool
    public var style: ?DialogButtonStyle
    public var value: ?ResourceStr
    public var fontColor: ?ResourceColor
    public var backgroundColor: ?ResourceColor
    public var action: ?VoidCallback
    public init(
        enabled!: ?Bool = None,
        defaultFocus!: ?Bool = None,
        style!: ?DialogButtonStyle = None,
        value!: ?ResourceStr,
        fontColor!: ?ResourceColor = None,
        backgroundColor!: ?ResourceColor = None,
        action!: ?VoidCallback
    )
}
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var action

```cangjie
public var action: ?VoidCallback
```

**Function:** Callback when the button is selected.

**Type:** ?[VoidCallback](./cj-common-types.md#type-voidcallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** Background color of the button.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var defaultFocus

```cangjie
public var defaultFocus: ?Bool
```

**Function:** Sets whether the button is the default focus.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enabled

```cangjie
public var enabled: ?Bool
```

**Function:** Determines if the button responds to clicks.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var fontColor

```cangjie
public var fontColor: ?ResourceColor
```

**Function:** Text color of the button.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var style

```cangjie
public var style: ?DialogButtonStyle
```

**Function:** Sets the style of the button.

**Type:** ?[DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var value

```cangjie
public var value: ?ResourceStr
```

**Function:** Text content of the button.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Bool, ?Bool, ?DialogButtonStyle, ?ResourceStr, ?ResourceColor, ?ResourceColor, ?VoidCallback)

```cangjie
public init(
    enabled!: ?Bool = None,
    defaultFocus!: ?Bool = None,
    style!: ?DialogButtonStyle = None,
    value!: ?ResourceStr,
    fontColor!: ?ResourceColor = None,
    backgroundColor!: ?ResourceColor = None,
    action!: ?VoidCallback
)
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| enabled | ?Bool | No | None | **Named parameter.** Determines if the button responds to clicks. Initial value: true |
| defaultFocus | ?Bool | No | None | **Named parameter.** Sets whether the button is the default focus. Initial value: false |
| style | ?[DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle) | No | None | **Named parameter.** Sets the style of the button. Initial value: DialogButtonStyle.Default |
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Text content of the button. |
| fontColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Text color of the button. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the button. |
| action | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | **Named parameter.** Callback when the button is selected. Initial value: {=>} |

## class AlertDialogButtonOptions

```cangjie
public class AlertDialogButtonOptions <: AlertDialogButtonBaseOptions {
    public var primary: ?Bool
    public init(
        enabled!: ?Bool = None,
        defaultFocus!: ?Bool = None,
        style!: ?DialogButtonStyle = None,
        value!: ?ResourceStr,
        fontColor!: ?ResourceColor = None,
        backgroundColor!: ?ResourceColor = None,
        action!: ?VoidCallback,
        primary!: ?Bool = None
    )
}
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

### var primary

```cangjie
public var primary: ?Bool
```

**Function:** Determines if the button responds to the Enter key by default when the dialog is focused and no tab key navigation has occurred. If multiple buttons are present, only one button can have this field set to true; otherwise, none will respond. Multiple dialogs can automatically focus and respond sequentially. Does not take effect if defaultFocus is true.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Bool, ?Bool, ?DialogButtonStyle, ?ResourceStr, ?ResourceColor, ?ResourceColor, ?VoidCallback, ?Bool)

```cangjie
public init(
    enabled!: ?Bool = None,
    defaultFocus!: ?Bool = None,
    style!: ?DialogButtonStyle = None,
    value!: ?ResourceStr,
    fontColor!: ?ResourceColor = None,
    backgroundColor!: ?ResourceColor = None,
    action!: ?VoidCallback,
    primary!: ?Bool = None
)
```

**Function:** Defines buttons in an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| enabled | ?Bool | No | None | **Named parameter.** Determines if the button responds to clicks. Initial value: true |
| defaultFocus | ?Bool | No | None | **Named parameter.** Sets whether the button is the default focus. Initial value: false |
| style | ?[DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle) | No | None | **Named parameter.** Sets the style of the button. Initial value: DialogButtonStyle.Default |
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Text content of the button. |
| fontColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Text color of the button. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the button. |
| action | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | **Named parameter.** Callback when the button is selected. Initial value: {=>} |
| primary | ?Bool | No | None | **Named parameter.** Determines if the button responds to the Enter key by default when the dialog is focused and no tab key navigation has occurred. If multiple buttons are present, only one button can have this field set to true; otherwise, none will respond. Multiple dialogs can automatically focus and respond sequentially. Does not take effect if defaultFocus is true. Initial value: false |

## class AlertDialogParam

```cangjie
public open class AlertDialogParam {
    public var title: ?ResourceStr
    public var subtitle: ?ResourceStr
    public var message: ?ResourceStr
    public var autoCancel: ?Bool
    public var cancel: ?VoidCallback
    public var alignment: ?DialogAlignment
    public var offset: ?Offset
    public var gridCount: ?UInt32
    public var maskRect: ?Rectangle
    public var showInSubWindow: ?Bool
    public var isModal: ?Bool
    public var backgroundColor: ?ResourceColor
    public var backgroundBlurStyle: ?BlurStyle
    public var onWillDismiss: ?Callback<DismissDialogAction, Unit>
    public var transition: ?TransitionEffect
    public var cornerRadius: ?BorderRadiuses
    public var width: ?Length
    public var height: ?Length
    public var borderWidth: ?Length
    public var borderColor: ?BorderColor
    public var borderStyle: ?EdgeStyles
    public var shadow: ?ShadowOptions
    public var textStyle: ?WordBreak
    public init(
        title!: ?ResourceStr = None,
        subtitle!: ?ResourceStr = None,
        message!: ?ResourceStr,
        autoCancel!: ?Bool = None,
        cancel!: ?VoidCallback = None,
        alignment!: ?DialogAlignment = None,
        offset!: ?Offset = None,
        gridCount!: ?UInt32 = None,
        maskRect!: ?Rectangle = None,
        showInSubWindow!: ?Bool = None,
        isModal!: ?Bool = None,
        backgroundColor!: ?ResourceColor = None,
        backgroundBlurStyle!: ?BlurStyle = None,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        transition!: ?TransitionEffect = None,
        cornerRadius!: ?BorderRadiuses = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: ?Length = None,
        borderColor!: ?BorderColor = None,
        borderStyle!: ?EdgeStyles = None,
        shadow!: ?ShadowOptions = None,
        textStyle!: ?WordBreak = None
    )
}
```

**Function:** Defines an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var alignment

```cangjie
public var alignment: ?DialogAlignment
```

**Function:** Vertical alignment of the dialog.

**Type:** ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var autoCancel

```cangjie
public var autoCancel: ?Bool
```

**Function:** Determines if the dialog closes when the mask layer is clicked.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Blur material of the dialog's background.

**Type:** ?[BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** Background color of the dialog.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderColor

```cangjie
public var borderColor: ?BorderColor
```

**Function:** Sets the border color of the dialog's background. If using the borderColor property, it must be used together with the borderWidth property.

**Type:** ?[BorderColor](#class-bordercolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22### var borderStyle

```cangjie
public var borderStyle: ?EdgeStyles
```

**Function:** Sets the border style of the popup backdrop. When using the borderStyle property, it must be used together with the borderWidth property.

**Type:** ?[EdgeStyles](./cj-common-types.md#class-edgestyles)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderWidth

```cangjie
public var borderWidth: ?Length
```

**Function:** Sets the border width of the popup backdrop.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var cancel

```cangjie
public var cancel: ?VoidCallback
```

**Function:** Callback when the dialog is closed by clicking the mask layer.

**Type:** ?[VoidCallback](./cj-common-types.md#type-voidcallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var cornerRadius

```cangjie
public var cornerRadius: ?BorderRadiuses
```

**Function:** Sets the corner radius of the backdrop. The radius of each of the four corners can be set separately.

**Type:** ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var gridCount

```cangjie
public var gridCount: ?UInt32
```

**Function:** The number of grid columns occupied by the popup container width.

**Type:** ?UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: ?Length
```

**Function:** Sets the height of the popup backdrop.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isModal

```cangjie
public var isModal: ?Bool
```

**Function:** Whether the popup is a modal window. Modal windows have a mask layer, while non-modal windows do not.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var maskRect

```cangjie
public var maskRect: ?Rectangle
```

**Function:** The area of the popup mask layer. Events within the mask layer area are not transmitted, while events outside the mask layer area are transmitted.

**Type:** ?[Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var message

```cangjie
public var message: ?ResourceStr
```

**Function:** The content of the popup.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: ?Offset
```

**Function:** The offset of the popup relative to the position specified by alignment.

**Type:** ?[Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillDismiss

```cangjie
public var onWillDismiss: ?Callback<DismissDialogAction, Unit>
```

**Function:** Interactive close callback function.

**Type:** ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction), Unit>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** Whether to display this popup in a sub-window when it needs to be displayed outside the main window.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var subtitle

```cangjie
public var subtitle: ?ResourceStr
```

**Function:** The subtitle of the popup.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Sets the shadow of the popup backdrop.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var textStyle

```cangjie
public var textStyle: ?WordBreak
```

**Function:** Sets the text style of the popup message content.

**Type:** ?[WordBreak](./cj-common-types.md#enum-wordbreak)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var title

```cangjie
public var title: ?ResourceStr
```

**Function:** The title of the popup.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: ?TransitionEffect
```

**Function:** Sets the transition effect for popup display and exit.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: ?Length
```

**Function:** Sets the width of the popup backdrop.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?Bool, ?VoidCallback, ?DialogAlignment, ?Offset, ?UInt32, ?Rectangle, ?Bool, ?Bool, ?ResourceColor, ?BlurStyle, ?Callback\<DismissDialogAction, Unit>, ?TransitionEffect, ?BorderRadiuses, ?Length, ?Length, ?Length, ?ResourceColor, ?EdgeStyles, ?ShadowOptions, ?WordBreak)

```cangjie
public init(
    title!: ?ResourceStr = None,
    subtitle!: ?ResourceStr = None,
    message!: ?ResourceStr,
    autoCancel!: ?Bool = None,
    cancel!: ?VoidCallback = None,
    alignment!: ?DialogAlignment = None,
    offset!: ?Offset = None,
    gridCount!: ?UInt32 = None,
    maskRect!: ?Rectangle = None,
    showInSubWindow!: ?Bool = None,
    isModal!: ?Bool = None,
    backgroundColor!: ?ResourceColor = None,
    backgroundBlurStyle!: ?BlurStyle = None,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    transition!: ?TransitionEffect = None,
    cornerRadius!: ?BorderRadiuses = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: ?Length = None,
    borderColor!: ?BorderColor = None,
    borderStyle!: ?EdgeStyles = None,
    shadow!: ?ShadowOptions = None,
    textStyle!: ?WordBreak = None
)
```

**Function:** Defines an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The title of the popup. Initial value: "" |
| subtitle | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The subtitle of the popup. Initial value: "" |
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | The content of the popup. |
| autoCancel | ?Bool | No | None | **Named parameter.** Whether to close the popup when clicking the mask layer. true means closing the popup, false means not closing the popup. Initial value: true |
| cancel | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | No | None | **Named parameter.** Callback when the dialog is closed by clicking the mask layer. Initial value: {=>} |
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | None | **Named parameter.** The vertical alignment of the popup. Initial value: DialogAlignment.Default |
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | None | **Named parameter.** The offset of the popup relative to the position specified by alignment. Initial value: Offset(0, 0) |
| gridCount | ?UInt32 | No | None | **Named parameter.** The number of grid columns occupied by the popup container width. Initial value: 4 |
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | None | **Named parameter.** The area of the popup mask layer. Events within the mask layer area are not transmitted, while events outside the mask layer area are transmitted. **Note:** maskRect does not take effect when showInSubWindow is true. Initial value: Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) |
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display this popup in a sub-window when it needs to be displayed outside the main window. Initial value: false, the popup is displayed within the application, not in an independent sub-window. **Note:** A popup with showInSubWindow set to true cannot trigger another popup with showInSubWindow set to true. |
| isModal | ?Bool | No | None | **Named parameter.** Whether the popup is a modal window. Modal windows have a mask layer, while non-modal windows do not. Initial value: true, meaning the popup has a mask layer. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** The background color of the popup. **Note:** When backgroundColor is set to a non-transparent color, backgroundBlurStyle should be set to BlurStyle.NONE; otherwise, the color display may not meet expectations. Initial value: Color.Transparent |
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | None | **Named parameter.** The blur material of the popup backdrop. **Note:** Set to BlurStyle.NONE to disable background blur. When backgroundBlurStyle is set to a non-NONE value, do not set backgroundColor; otherwise, the color display may not meet expectations. Initial value: BlurStyle.ComponentUltraThick |
| onWillDismiss | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction), Unit> | No | None | **Named parameter.** Interactive close callback function. **Note:** 1. When the user performs actions like clicking the mask layer to close, swiping left/right, pressing the back button, or pressing ESC to close, if this callback is registered, the popup will not close immediately. The callback can determine whether to close the popup based on the reason obtained. Currently, the reason returned by this component does not support the CLOSE_BUTTON enum value. 2. Within the onWillDismiss callback, another onWillDismiss interception cannot be performed. |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for popup display and exit. **Note:** 1. If not set, the default display/exit animation is used. 2. Pressing the back key during the display animation interrupts the display animation and executes the exit animation, with the effect being a combination of the display and exit animation curves. 3. Pressing the back key during the exit animation does not interrupt the exit animation; the exit animation continues, and pressing the back key again exits the application. |
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | None | **Named parameter.** Sets the corner radius of the backdrop. The radius of each of the four corners can be set separately. The corner radius is limited by the component size, with the maximum value being half of the component's width or height. Negative values are treated as default values. Percentage parameter: Sets the corner radius as a percentage of the parent popup's width and height. **Note:** When the cornerRadius property type is LocalizedBorderRadiuses, it supports changing the layout order according to language habits. Initial value: BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) |
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of the popup backdrop. **Note:** - Default maximum width: None. - Percentage parameter: The reference width is the window width, adjusted up or down based on this. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the height of the popup backdrop. **Note:** - Default maximum height: None. - Percentage parameter: The reference height is (window height - safe area), adjusted up or down based on this. |
| borderWidth | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of each of the four borders separately. Percentage parameter: Sets the border width as a percentage of the parent popup's width. If the left and right borders exceed the popup width or the top and bottom borders exceed the popup height, the display may not meet expectations. **Note:** When the borderWidth property type is LocalizedEdgeWidths, it supports changing the layout order according to language habits. Initial value: 0 |
| borderColor | ?[BorderColor](#class-bordercolor) | No | None | **Named parameter.** Sets the border color of the popup backdrop. If using borderColor, it must be used together with borderWidth. **Note:** When the borderColor property type is LocalizedEdgeColors, it supports changing the layout order according to language habits. Initial value: BorderColor(color: Color.Black) |
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | None | **Named parameter.** Sets the border style of the popup backdrop. If using borderStyle, it must be used together with borderWidth. Initial value: EdgeStyles() |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the popup backdrop.<br>Initial value:<br>Before API version 26, the initial value is ShadowOptions(radius: 0.0);<br>From API version 26 onward, the initial value is ShadowOptions(radius: -1.0). |
| textStyle | ?[WordBreak](./cj-common-types.md#enum-wordbreak) | No | None | **Named parameter.** Sets the text style of the popup message content. Initial value: WordBreak.BreakAll |

## class AlertDialogParamWithButtons

```cangjie
public class AlertDialogParamWithButtons <: AlertDialogParam {
    public var primaryButton: ?AlertDialogButtonBaseOptions
    public var secondaryButton: ?AlertDialogButtonBaseOptions
    public init(
        title!: ?ResourceStr = None,
        subtitle!: ?ResourceStr = None,
        message!: ?ResourceStr,
        autoCancel!: ?Bool = None,
        cancel!: ?VoidCallback = None,
        alignment!: ?DialogAlignment = None,
        offset!: ?Offset = None,
        gridCount!: ?UInt32 = None,
        maskRect!: ?Rectangle = None,
        showInSubWindow!: ?Bool = None,
        isModal!: ?Bool = None,
        backgroundColor!: ?ResourceColor = None,
        backgroundBlurStyle!: ?BlurStyle = None,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: ?BorderRadiuses = None,
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: ?Length = None,
        borderColor!: ?BorderColor = None,
        borderStyle!: ?EdgeStyles = None,
        shadow!: ?ShadowOptions = None,
        textStyle!: ?WordBreak = None,
        primaryButton!: ?AlertDialogButtonBaseOptions,
        secondaryButton!: ?AlertDialogButtonBaseOptions
    )
}
```

**Function:** Defines an alert dialog with two confirmation buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [AlertDialogParam](#class-alertdialogparam)

### var primaryButton

```cangjie
public var primaryButton: ?AlertDialogButtonBaseOptions
```

**Function:** The first button.

**Type:** ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var secondaryButton

```cangjie
public var secondaryButton: ?AlertDialogButtonBaseOptions
```

**Function:** The second button.

**Type:** ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?Bool, ?VoidCallback, ?DialogAlignment, ?Offset, ?UInt32, ?Rectangle, ?Bool, ?Bool, ?ResourceColor, ?BlurStyle, ?Callback\<DismissDialogAction, Unit>, ?BorderRadiuses, ?TransitionEffect, ?Length, ?Length, ?Length, ?BorderColor, ?EdgeStyles, ?ShadowOptions, ?WordBreak, ?AlertDialogButtonBaseOptions, ?AlertDialogButtonBaseOptions)

```cangjie
public init(
    title!: ?ResourceStr = None,
    subtitle!: ?ResourceStr = None,
    message!: ?ResourceStr,
    autoCancel!: ?Bool = None,
    cancel!: ?VoidCallback = None,
    alignment!: ?DialogAlignment = None,
    offset!: ?Offset = None,
    gridCount!: ?UInt32 = None,
    maskRect!: ?Rectangle = None,
    showInSubWindow!: ?Bool = None,
    isModal!: ?Bool = None,
    backgroundColor!: ?ResourceColor = None,
    backgroundBlurStyle!: ?BlurStyle = None,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: ?BorderRadiuses = None,
    transition!: ?TransitionEffect = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: ?Length = None,
    borderColor!: ?BorderColor = None,
    borderStyle!: ?EdgeStyles = None,
    shadow!: ?ShadowOptions = None,
    textStyle!: ?WordBreak = None,
    primaryButton!: ?AlertDialogButtonBaseOptions,
    secondaryButton!: ?AlertDialogButtonBaseOptions
)
```

**Function:** Defines an alert dialog with two confirmation buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog title. Initial value: "" |
| subtitle | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog subtitle. Initial value: "" |
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Dialog content. |
| autoCancel | ?Bool | No | None | **Named parameter.** Whether to close the dialog when clicking the mask layer. true: close the dialog; false: do not close the dialog. Initial value: true |
| cancel | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | No | None | **Named parameter.** Callback when closing the dialog by clicking the mask layer. Initial value: {=>} |
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | None | **Named parameter.** Vertical alignment of the dialog. Initial value: DialogAlignment.Default |
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | None | **Named parameter.** Offset of the dialog relative to the alignment position. Initial value: Offset(0, 0) |
| gridCount | ?UInt32 | No | None | **Named parameter.** Number of grid columns occupied by the dialog container width. Initial value: 4 |
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | None | **Named parameter.** Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside are transmitted. **Note:** maskRect does not take effect when showInSubWindow is true. Initial value: Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) |
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display the dialog in a sub-window when it needs to appear outside the main window. Initial value: false, meaning the dialog is displayed within the application rather than in an independent sub-window. **Note:** A dialog with showInSubWindow=true cannot trigger another dialog with showInSubWindow=true. |
| isModal | ?Bool | No | None | **Named parameter.** Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not. Initial value: true, meaning the dialog has a mask layer. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the dialog. **Note:** When backgroundColor is set to a non-transparent color, backgroundBlurStyle should be set to BlurStyle.NONE; otherwise, the color display may not meet expectations. Initial value: Color.Transparent |
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | None | **Named parameter.** Blur material of the dialog background. **Note:** Set to BlurStyle.NONE to disable background blur. When backgroundBlurStyle is set to a non-NONE value, do not set backgroundColor; otherwise, the color display may not meet expectations. Initial value: BlurStyle.ComponentUltraThick |
| onWillDismiss | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction), Unit> | No | None | **Named parameter.** Interactive close callback function. **Note:** 1. When users perform actions like clicking the mask layer to close, swiping left/right, pressing the back button, or pressing ESC to close, if this callback is registered, the dialog will not close immediately. The callback can determine whether to close the dialog based on the operation type obtained from reason. The current component does not support the CLOSE_BUTTON enum value in reason. 2. Do not perform onWillDismiss interception within the onWillDismiss callback. |
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | None | **Named parameter.** Sets the corner radius of the background. The radius of each corner can be set separately. The maximum corner radius is limited by the component size (half of the component width or height). Negative values are treated as default values. Percentage parameter: Sets the corner radius as a percentage of the parent dialog's width and height. **Note:** When cornerRadius is of type LocalizedBorderRadiuses, it supports layout order changes based on language habits. Initial value: BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for dialog display and exit. **Note:** 1. If not set, the default show/exit animation is used. 2. Pressing the back button during the show animation interrupts the show animation and executes the exit animation, resulting in a combined effect of both animations. 3. Pressing the back button during the exit animation does not interrupt it; the exit animation continues, and pressing back again exits the application. |
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of the dialog background. **Note:** - Default maximum dialog width: None. - Percentage parameter: Adjusts the dialog width relative to the window width. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the height of the dialog background. **Note:** - Default maximum dialog height: None. - Percentage parameter: Adjusts the dialog height relative to (window height - safe area). |
| borderWidth | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of each border separately. Percentage parameter: Sets the border width as a percentage of the parent dialog's width. If the left/right borders exceed the dialog width or the top/bottom borders exceed the dialog height, the display may not meet expectations. **Note:** When borderWidth is of type LocalizedEdgeWidths, it supports layout order changes based on language habits. Initial value: 0 |
| borderColor | ?[BorderColor](#class-bordercolor) | No | None | **Named parameter.** Sets the border color of the dialog background. Requires borderWidth to be set. **Note:** When borderColor is of type LocalizedEdgeColors, it supports layout order changes based on language habits. Initial value: BorderColor(color: Color.Black) |
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | None | **Named parameter.** Sets the border style of the dialog background. Requires borderWidth to be set. Initial value: EdgeStyles() |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the dialog background.<br>Initial value:<br>Before API version 26, the initial value is ShadowOptions(radius: 0.0);<br>From API version 26 onward, the initial value is ShadowOptions(radius: -1.0). |
| textStyle | ?[WordBreak](./cj-common-types.md#enum-wordbreak) | No | None | **Named parameter.** Sets the text style of the dialog message content. Initial value: WordBreak.BreakAll |
| primaryButton | ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions) | Yes | - | **Named parameter.** The first button. |
| secondaryButton | ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions) | Yes | - | **Named parameter.** The second button. |

## class AlertDialogParamWithConfirm

```cangjie
public class AlertDialogParamWithConfirm <: AlertDialogParam {
    public var confirm: ?AlertDialogButtonBaseOptions
    public init(
        title!: ?ResourceStr = None,
        subtitle!: ?ResourceStr = None,
        message!: ?ResourceStr,
        autoCancel!: ?Bool = None,
        cancel!: ?VoidCallback = None,
        alignment!: ?DialogAlignment = None,
        offset!: ?Offset = None,
        gridCount!: ?UInt32 = None,
        maskRect!: ?Rectangle = None,
        showInSubWindow!: ?Bool = None,
        isModal!: ?Bool = None,
        backgroundColor!: ?ResourceColor = None,
        backgroundBlurStyle!: ?BlurStyle = None,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: ?BorderRadiuses = None,
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: ?Length = None,
        borderColor!: ?BorderColor = None,
        borderStyle!: ?EdgeStyles = None,
        shadow!: ?ShadowOptions = None,
        textStyle!: ?WordBreak = None,
        confirm!: ?AlertDialogButtonBaseOptions = None
    )
}
```

**Function:** Defines an alert dialog with a confirmation button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [AlertDialogParam](#class-alertdialogparam)

### var confirm

```cangjie
public var confirm: ?AlertDialogButtonBaseOptions
```

**Function:** Enables/disables the confirmation button, sets default focus, button style, text content, text color, button background color, and click callback.

**Type:** ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?Bool, ?VoidCallback, ?DialogAlignment, ?Offset, ?UInt32, ?Rectangle, ?Bool, ?Bool, ?ResourceColor, ?BlurStyle, ?Callback\<DismissDialogAction, Unit>, ?BorderRadiuses, ?TransitionEffect, ?Length, ?Length, ?Length, ?ResourceColor, ?EdgeStyles, ?ShadowOptions, ?WordBreak, ?AlertDialogButtonBaseOptions)

```cangjie
public init(
    title!: ?ResourceStr = None,
    subtitle!: ?ResourceStr = None,
    message!: ?ResourceStr,
    autoCancel!: ?Bool = None,
    cancel!: ?VoidCallback = None,
    alignment!: ?DialogAlignment = None,
    offset!: ?Offset = None,
    gridCount!: ?UInt32 = None,
    maskRect!: ?Rectangle = None,
    showInSubWindow!: ?Bool = None,
    isModal!: ?Bool = None,
    backgroundColor!: ?ResourceColor = None,
    backgroundBlurStyle!: ?BlurStyle = None,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: ?BorderRadiuses = None,
    transition!: ?TransitionEffect = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: ?Length = None,
    borderColor!: ?BorderColor = None,
    borderStyle!: ?EdgeStyles = None,
    shadow!: ?ShadowOptions = None,
    textStyle!: ?WordBreak = None,
    confirm!: ?AlertDialogButtonBaseOptions = None
)
```

**Function:** Defines an alert dialog with a confirmation button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog title. Initial value: "" |
| subtitle | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog subtitle. Initial value: "" |
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Dialog content. |
| autoCancel | ?Bool | No | None | **Named parameter.** Whether to close the dialog when clicking the mask layer. true: close the dialog; false: do not close the dialog. Initial value: true |
| cancel | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | No | None | **Named parameter.** Callback when closing the dialog by clicking the mask layer. Initial value: {=>} |
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | None | **Named parameter.** Vertical alignment of the dialog. Initial value: DialogAlignment.Default |
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | None | **Named parameter.** Offset of the dialog relative to the alignment position. Initial value: Offset(0, 0) |
| gridCount | ?UInt32 | No | None | **Named parameter.** Number of grid columns occupied by the dialog container width. Initial value: 4 |
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | None | **Named parameter.** Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside are transmitted. **Note:** maskRect does not take effect when showInSubWindow is true. Initial value: Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) |
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display the dialog in a sub-window when it needs to appear outside the main window. Initial value: false, meaning the dialog is displayed within the application rather than in an independent sub-window. **Note:** A dialog with showInSubWindow=true cannot trigger another dialog with showInSubWindow=true. |
| isModal | ?Bool | No | None | **Named parameter.** Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not. Initial value: true, meaning the dialog has a mask layer. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the dialog. **Note:** When backgroundColor is set to a non-transparent color, backgroundBlurStyle should be set to BlurStyle.NONE; otherwise, the color display may not meet expectations. Initial value: Color.Transparent |
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | None | **Named parameter.** Blur material of the dialog background. **Note:** Set to BlurStyle.NONE to disable background blur. When backgroundBlurStyle is set to a non-NONE value, do not set backgroundColor; otherwise, the color display may not meet expectations. Initial value: BlurStyle.ComponentUltraThick |
| onWillDismiss | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction), Unit> | No | None | **Named parameter.** Interactive close callback function. **Note:** 1. When users perform actions like clicking the mask layer to close, swiping left/right, pressing the back button, or pressing ESC to close, if this callback is registered, the dialog will not close immediately. The callback can determine whether to close the dialog based on the operation type obtained from reason. The current component does not support the CLOSE_BUTTON enum value in reason. 2. Do not perform onWillDismiss interception within the onWillDismiss callback. |
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | None | **Named parameter.** Sets the corner radius of the background. The radius of each corner can be set separately. The maximum corner radius is limited by the component size (half of the component width or height). Negative values are treated as default values. Percentage parameter: Sets the corner radius as a percentage of the parent dialog's width and height. **Note:** When cornerRadius is of type LocalizedBorderRadiuses, it supports layout order changes based on language habits. Initial value: BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for dialog display and exit. **Note:** 1. If not set, the default show/exit animation is used. 2. Pressing the back button during the show animation interrupts the show animation and executes the exit animation, resulting in a combined effect of both animations. 3. Pressing the back button during the exit animation does not interrupt it; the exit animation continues, and pressing back again exits the application. |
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of the dialog background. **Note:** - Default maximum dialog width: None. - Percentage parameter: Adjusts the dialog width relative to the window width. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the height of the dialog background. **Note:** - Default maximum dialog height: None. - Percentage parameter: Adjusts the dialog height relative to (window height - safe area). |
| borderWidth | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of each border separately. Percentage parameter: Sets the border width as a percentage of the parent dialog's width. If the left/right borders exceed the dialog width or the top/bottom borders exceed the dialog height, the display may not meet expectations. **Note:** When borderWidth is of type LocalizedEdgeWidths, it supports layout order changes based on language habits. Initial value: 0 |
| borderColor | ?[BorderColor](#class-bordercolor) | No | None | **Named parameter.** Sets the border color of the dialog background. Requires borderWidth to be set. **Note:** When borderColor is of type LocalizedEdgeColors, it supports layout order changes based on language habits. Initial value: BorderColor(color: Color.Black) |
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | None | **Named parameter.** Sets the border style of the dialog background. Requires borderWidth to be set. Initial value: EdgeStyles() |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the dialog background.<br>Initial value:<br>Before API version 26, the initial value is ShadowOptions(radius: 0.0);<br>From API version 26 onward, the initial value is ShadowOptions(radius: -1.0). |
| textStyle | ?[WordBreak](./cj-common-types.md#enum-wordbreak) | No | None | **Named parameter.** Sets the text style of the dialog message content. Initial value: WordBreak.BreakAll |
| confirm | ?[AlertDialogButtonBaseOptions](#class-alertdialogbuttonbaseoptions) | No | None | **Named parameter.** Enables/disables the confirmation button, sets default focus, button style, text content, text color, button background color, and click callback. Initial value: AlertDialogButtonOptions(value: "", action: {=>}) |

## class AlertDialogParamWithOptions

```cangjie
public class AlertDialogParamWithOptions <: AlertDialogParam {
    public var buttons: ?Array<AlertDialogButtonOptions>
    public var buttonDirection: ?DialogButtonDirection
    public init(
        title!: ?ResourceStr = None,
        subtitle!: ?ResourceStr = None,
        message!: ?ResourceStr,
        autoCancel!: ?Bool = None,
        cancel!: ?VoidCallback = None,
        alignment!: ?DialogAlignment = None,
        offset!: ?Offset = None,
        gridCount!: ?UInt32 = None,
        maskRect!: ?Rectangle = None,
        showInSubWindow!: ?Bool = None,
        isModal!: ?Bool = None,
        backgroundColor!: ?ResourceColor = None,
        backgroundBlurStyle!: ?BlurStyle = None,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: ?BorderRadiuses = None,
        transition!: ?TransitionEffect = None,
        width!: ?Length = None,
        height!: ?Length = None,
        borderWidth!: ?Length = None,
        borderColor!: ?BorderColor = None,
        borderStyle!: ?EdgeStyles = None,
        shadow!: ?ShadowOptions = None,
        textStyle!: ?WordBreak = None,
        buttons!: ?Array<AlertDialogButtonOptions>,
        buttonDirection!: ?DialogButtonDirection = None
    )
}
```

**Function:** Defines an alert dialog with multiple buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [AlertDialogParam](#class-alertdialogparam)

### var buttonDirection

```cangjie
public var buttonDirection: ?DialogButtonDirection
```

**Function:** Default button arrangement direction is DialogButtonDirection.AUTO. For three or more buttons, Auto mode is recommended (switches to vertical mode for two or more buttons, usually displaying more buttons). In non-Auto mode, three or more buttons may not display fully, and buttons beyond the display range will be truncated.

**Type:** ?[DialogButtonDirection](#enum-dialogbuttondirection)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var buttons

```cangjie
public var buttons: ?Array<AlertDialogButtonOptions>
```

**Function:** Multiple buttons in the dialog container.

**Type:** ?Array\<[AlertDialogButtonOptions](#class-alertdialogbuttonoptions)>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?Bool, ?VoidCallback, ?DialogAlignment, ?Offset, ?UInt32, ?Rectangle, ?Bool, ?Bool, ?ResourceColor, ?BlurStyle, ?Callback\<DismissDialogAction, Unit>, ?BorderRadiuses, ?TransitionEffect, ?Length, ?Length, ?Length, ?BorderColor, ?EdgeStyles, ?ShadowOptions, ?WordBreak, ?Array\<AlertDialogButtonOptions>, ?DialogButtonDirection)

```cangjie
public init(
    title!: ?ResourceStr = None,
    subtitle!: ?ResourceStr = None,
    message!: ?ResourceStr,
    autoCancel!: ?Bool = None,
    cancel!: ?VoidCallback = None,
    alignment!: ?DialogAlignment = None,
    offset!: ?Offset = None,
    gridCount!: ?UInt32 = None,
    maskRect!: ?Rectangle = None,
    showInSubWindow!: ?Bool = None,
    isModal!: ?Bool = None,
    backgroundColor!: ?ResourceColor = None,
    backgroundBlurStyle!: ?BlurStyle = None,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: ?BorderRadiuses = None,
    transition!: ?TransitionEffect = None,
    width!: ?Length = None,
    height!: ?Length = None,
    borderWidth!: ?Length = None,
    borderColor!: ?BorderColor = None,
    borderStyle!: ?EdgeStyles = None,
    shadow!: ?ShadowOptions = None,
    textStyle!: ?WordBreak = None,
    buttons!: ?Array<AlertDialogButtonOptions>,
    buttonDirection!: ?DialogButtonDirection = None
)
```

**Function:** Defines an alert dialog with multiple buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog title. Initial value: "" |
| subtitle | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Dialog subtitle. Initial value: "" |
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Dialog content. |
| autoCancel | ?Bool | No | None | **Named parameter.** Whether to close the dialog when clicking the mask layer. true: close the dialog; false: do not close the dialog. Initial value: true |
| cancel | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | No | None | **Named parameter.** Callback when closing the dialog by clicking the mask layer. Initial value: {=>} |
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | None | **Named parameter.** Vertical alignment of the dialog. Initial value: DialogAlignment.Default |
| offset | ?[Offset](./cj-common-types.md#class-offset) | No | None | **Named parameter.** Offset of the dialog relative to the alignment position. Initial value: Offset(0, 0) |
| gridCount | ?UInt32 | No | None | **Named parameter.** Number of grid columns occupied by the dialog container width. Initial value: 4 |
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | None | **Named parameter.** Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside are transmitted. **Note:** maskRect does not take effect when showInSubWindow is true. Initial value: Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) |
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display the dialog in a sub-window when it needs to appear outside the main window. Initial value: false, meaning the dialog is displayed within the application rather than in an independent sub-window. **Note:** A dialog with showInSubWindow=true cannot trigger another dialog with showInSubWindow=true. |
| isModal | ?Bool | No | None | **Named parameter.** Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not. Initial value: true, meaning the dialog has a mask layer. |
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the dialog. **Note:** When backgroundColor is set to a non-transparent color, backgroundBlurStyle should be set to BlurStyle.NONE; otherwise, the color display may not meet expectations. Initial value: Color.Transparent |
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | None | **Named parameter.** Blur material of the dialog background. **Note:** Set to BlurStyle.NONE to disable background blur. When backgroundBlurStyle is set to a non-NONE value, do not set backgroundColor; otherwise, the color display may not meet expectations. Initial value: BlurStyle.ComponentUltraThick |
| onWillDismiss | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](./cj-dialog-actionsheet.md#class-dismissdialogaction), Unit> | No | None | **Named parameter.** Interactive close callback function. **Note:** 1. When users perform actions like clicking the mask layer to close, swiping left/right, pressing the back button, or pressing ESC to close, if this callback is registered, the dialog will not close immediately. The callback can determine whether to close the dialog based on the operation type obtained from reason. The current component does not support the CLOSE_BUTTON enum value in reason. 2. Do not perform onWillDismiss interception within the onWillDismiss callback. |
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | None | **Named parameter.** Sets the corner radius of the background. The radius of each corner can be set separately. The maximum corner radius is limited by the component size (half of the component width or height). Negative values are treated as default values. Percentage parameter: Sets the corner radius as a percentage of the parent dialog's width and height. **Note:** When cornerRadius is of type LocalizedBorderRadiuses, it supports layout order changes based on language habits. Initial value: BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for dialog display and exit. **Note:** 1. If not set, the default show/exit animation is used. 2. Pressing the back button during the show animation interrupts the show animation and executes the exit animation, resulting in a combined effect of both animations. 3. Pressing the back button during the exit animation does not interrupt it; the exit animation continues, and pressing back again exits the application. |
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of the dialog background. **Note:** - Default maximum dialog width: None. - Percentage parameter: Adjusts the dialog width relative to the window width. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the height of the dialog background. **Note:** - Default maximum dialog height: None. - Percentage parameter: Adjusts the dialog height relative to (window height - safe area). |
| borderWidth | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of each border separately. Percentage parameter: Sets the border width as a percentage of the parent dialog's width. If the left/right borders exceed the dialog width or the top/bottom borders exceed the dialog height, the display may not meet expectations. **Note:** When borderWidth is of type LocalizedEdgeWidths, it supports layout order changes based on language habits. Initial value: 0 |
| borderColor | ?[BorderColor](#class-bordercolor) | No | None | **Named parameter.** Sets the border color of the dialog background. Requires borderWidth to be set. **Note:** When borderColor is of type LocalizedEdgeColors, it supports layout order changes based on language habits. Initial value: BorderColor(color: Color.Black) |
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | None | **Named parameter.** Sets the border style of the dialog background. Requires borderWidth to be set. Initial value: EdgeStyles() |
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the dialog background.<br>Initial value:<br>Before API version 26, the initial value is ShadowOptions(radius: 0.0);<br>From API version 26 onward, the initial value is ShadowOptions(radius: -1.0). |
| textStyle | ?[WordBreak](./cj-common-types.md#enum-wordbreak) | No | None | **Named parameter.** Sets the text style of the dialog message content. Initial value: WordBreak.BreakAll |
| buttons | ?Array\<[AlertDialogButtonOptions](#class-alertdialogbuttonoptions)> | Yes | - | **Named parameter.** Multiple buttons in the dialog container. |
| buttonDirection | ?[DialogButtonDirection](#enum-dialogbuttondirection) | No | None | **Named parameter.** Default button arrangement direction is DialogButtonDirection.AUTO. For three or more buttons, Auto mode is recommended (switches to vertical mode for two or more buttons, usually displaying more buttons). In non-Auto mode, three or more buttons may not display fully, and buttons beyond the display range will be truncated. Initial value: DialogButtonDirection.AUTO |

### Example 1 (Dialog with Multiple Buttons)

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.hilog.*
import ohos.arkui.component.common.Offset as CommonOffset

@Entry
@Component
class EntryView {
    func build() {
        Column(space:5.vp) {
            Button("one button dialog")
                .onClick({ evt =>
                    getUIContext().showAlertDialog(
                        AlertDialogParamWithConfirm(message:"text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")}, alignment: DialogAlignment.Center,
                            offset: CommonOffset(0, -20),
                            gridCount: 4,
                            backgroundColor: Color.White,
                            onWillDismiss: {
                                dismissDialogAction: DismissDialogAction => match (dismissDialogAction.reason) {
                                    case PRESS_BACK => dismissDialogAction.dismiss()
                                    case TOUCH_OUTSIDE => dismissDialogAction.dismiss()
                                    case _ => ()
                                }
                            },
                            confirm: AlertDialogButtonOptions(value: "button",
                                action: {=> Hilog.info(0, "AppLogCj", "Button-clicking callback")}
                            )
                        )
                    )
                })
            .backgroundColor(0x317aff)
            Button("two button dialog")
                .onClick({ evt =>
                    getUIContext().showAlertDialog(
                        AlertDialogParamWithButtons(message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")},
                            alignment: DialogAlignment.Center,
                            offset: CommonOffset(0, -20),
                            gridCount: 4,
                            backgroundColor: Color.White,
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
                                action: {=> Hilog.info(0, "AppLogCj", "Callback when second button is clicked")}
                            )
                        )
                    )
                })
            .backgroundColor(0x317aff)
            Button("three button dialog")
                .onClick({ evt =>
                    getUIContext().showAlertDialog(
                        AlertDialogParamWithOptions(
                            message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Callback when third button is clicked")},
                            alignment: DialogAlignment.Center,
                            offset: CommonOffset(0, -20),
                            gridCount: 4,
                            backgroundColor: Color.White,
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
                    )
                })
                .backgroundColor(0x317aff)
        }
        .width(100.percent)
        .height(100.percent)
    }
}
```

![alertdialog1](./figures/alertDialog1.gif)

### Example 2 (Dialog That Can Pop Up Outside the Main Window)

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.hilog.*
import ohos.arkui.component.common.Offset as CommonOffset

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 5.vp) {
            Button("button dialog")
                .onClick({ evt =>
                    getUIContext().showAlertDialog(
                        AlertDialogParamWithOptions(
                            message: "text",
                            title: "title",
                            subtitle: "subtitle",
                            autoCancel: true,
                            cancel: {=> Hilog.info(0, "AppLogCj", "Closed callbacks")},
                            alignment: DialogAlignment.Center,
                            offset: CommonOffset(0, -20),
                            showInSubWindow: true,
                            buttonDirection: DialogButtonDirection.Horizontal,
                            gridCount: 4,
                            backgroundColor: Color.White,
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
                    )
                })
                .backgroundColor(0x317aff)
        }
        .width(100.percent)
        .height(100.percent)
    }
}

```

![alertdialog2](./figures/alertdialog2.gif)