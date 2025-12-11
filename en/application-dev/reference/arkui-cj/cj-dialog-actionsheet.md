# Action Sheet Dialog (ActionSheet)

A list selection dialog.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class SheetInfo

```cangjie
public class SheetInfo {
    public var title: ?ResourceStr
    public var action: ?VoidCallback
    public var icon: ?ResourceStr
    public init(
        title!: ?ResourceStr,
        icon!: ?ResourceStr = None,
        action!: ?VoidCallback
    )
}
```

**Function:** Configures the content of each option, supporting image, text, and selection callback settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var action

```cangjie
public var action: ?VoidCallback
```

**Function:** Callback when an option is selected.

**Type:** ?[VoidCallback](./cj-common-types.md#type-voidcallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var icon

```cangjie
public var icon: ?ResourceStr
```

**Function:** Icon for the option. No icon is displayed by default.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var title

```cangjie
public var title: ?ResourceStr
```

**Function:** Text content of the option.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?VoidCallback)

```cangjie
public init(
    title!: ?ResourceStr,
    icon!: ?ResourceStr = None,
    action!: ?VoidCallback
)
```

**Function:** Constructor for the SheetInfo class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Text content of the option.<br/>A scrollbar appears when the text is too long. |
| icon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Icon for the option. No icon is displayed by default.<br/>The string format can be used to load network and local images, commonly used for network images. When referencing local images with relative paths, e.g., Image("common/test.jpg"). |
| action | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | **Named parameter.** Callback when the option is selected. |

## class ActionSheetButtonOptions

```cangjie
public class ActionSheetButtonOptions {
    public var value: ?ResourceStr
    public var action: ?VoidCallback
    public var enabled: ?Bool
    public var defaultFocus: ?Bool
    public var style: ?DialogButtonStyle
    public init(
        value!: ?ResourceStr,
        action!: ?VoidCallback,
        enabled!: ?Bool = None,
        defaultFocus!: ?Bool = None,
        style!: ?DialogButtonStyle = None
    )
}
```

**Function:** Style of buttons in the dialog.

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

### init(?ResourceStr, ?VoidCallback, ?Bool, ?Bool, ?DialogButtonStyle)

```cangjie
public init(
    value!: ?ResourceStr,
    action!: ?VoidCallback,
    enabled!: ?Bool = None,
    defaultFocus!: ?Bool = None,
    style!: ?DialogButtonStyle = None
)
```

**Function:** Constructor for the ActionSheetButtonOptions class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Text content of the button. |
| action | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | Yes | - | **Named parameter.** Callback when the button is selected. |
| enabled | ?Bool | No | None | **Named parameter.** Determines if the button responds to clicks. true means the button responds, false means it does not. |
| defaultFocus | ?Bool | No | None | **Named parameter.** Sets whether the button is the default focus. true means it is the default focus, false means it is not. |
| style | ?[DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle) | No | None | **Named parameter.** Sets the style of the button. |

## class DismissDialogAction

```cangjie
public class DismissDialogAction {
    public var reason: ?DismissReason
    public init(reason: ?DismissReason)
    public func dismiss(): Unit
}
```

**Function:** Information about dialog dismissal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var reason

```cangjie
public var reason: ?DismissReason
```

**Function:** Reason why the dialog cannot be dismissed. Determines whether the dialog should close based on developer needs under different operations.

**Type:** ?[DismissReason](./cj-common-types.md#enum-dismissreason)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?DismissReason)

```cangjie
public init(reason: ?DismissReason)
```

**Function:** Constructor for the DismissDialogAction class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| reason | ?[DismissReason](./cj-common-types.md#enum-dismissreason) | Yes | - | Reason why the dialog cannot be dismissed. Determines whether the dialog should close based on developer needs under different operations. |

### func dismiss()

```cangjie
public func dismiss(): Unit
```

**Function:** Callback function for dialog dismissal. Called by the developer when exiting is needed; no call is required otherwise.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class ActionSheetOffset

```cangjie
public class ActionSheetOffset {
    public var dx: ?Length
    public var dy: ?Length
    public init(
        dx!: ?Length,
        dy!: ?Length
    )
}
```

**Function:** Alignment method for the dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var dx

```cangjie
public var dx: ?Length
```

**Function:** Horizontal offset of the popup window relative to the alignment position.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var dy

```cangjie
public var dy: ?Length
```

**Function:** Vertical offset of the popup window relative to the alignment position.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length)

```cangjie
public init(
    dx!: ?Length,
    dy!: ?Length
)
```

**Function:** Constructor for the ActionSheetOffset class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| dx | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Horizontal offset of the popup window relative to the alignment position. |
| dy | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Vertical offset of the popup window relative to the alignment position. |

## class ActionSheetOptions

```cangjie
public class ActionSheetOptions {
    public var title: ?ResourceStr
    public var message: ?ResourceStr
    public var sheets: ?Array<SheetInfo>
    public var subtitle: ?ResourceStr
    public var confirm: ?ActionSheetButtonOptions
    public var autoCancel: ?Bool
    public var cancel: ?VoidCallback
    public var alignment: ?DialogAlignment
    public var offset: ?ActionSheetOffset
    public var maskRect: ?Rectangle
    public var showInSubWindow: ?Bool
    public var isModal: ?Bool
    public var backgroundColor: ?ResourceColor
    public var backgroundBlurStyle: ?BlurStyle
    public var onWillDismiss: ?Callback<DismissDialogAction, Unit>
    public var cornerRadius: ?BorderRadiuses
    public var borderWidth: ?Length
    public var borderColor: ?ResourceColor
    public var borderStyle: ?EdgeStyles
    public var width: ?Length
    public var height: ?Length
    public var shadow: ?ShadowOptions
    public var transition: ?TransitionEffect
    public init(
        title!: ?ResourceStr,
        subtitle!: ?ResourceStr = None,
        message!: ?ResourceStr,
        confirm!: ?ActionSheetButtonOptions = None,
        cancel!: ?VoidCallback = None,
        sheets!: ?Array<SheetInfo>,
        autoCancel!: ?Bool = None,
        alignment!: ?DialogAlignment = None,
        offset!: ?ActionSheetOffset = None,
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
        borderColor!: ?ResourceColor = None,
        borderStyle!: ?EdgeStyles = None,
        shadow!: ?ShadowOptions = None
    )
}
```

**Function:** Configuration options for the ActionSheet dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22### var alignment

```cangjie
public var alignment: ?DialogAlignment
```

**Function:** Vertical alignment of the dialog.

**Type:** ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var autoCancel

```cangjie
public var autoCancel: ?Bool
```

**Function:** Whether to close the dialog when clicking the mask layer.

**Type:** ?Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Blur material of the dialog backplate.

**Type:** ?[BlurStyle](./cj-common-types.md#enum-blurstyle)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** Color of the dialog backplate.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderColor

```cangjie
public var borderColor: ?ResourceColor
```

**Function:** Sets the border color of the dialog backplate. If using the borderColor property, it must be used together with the borderWidth property.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderStyle

```cangjie
public var borderStyle: ?EdgeStyles
```

**Function:** Sets the border style of the dialog backplate. If using the borderStyle property, it must be used together with the borderWidth property.

**Type:** ?[EdgeStyles](./cj-common-types.md#class-edgestyles)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var borderWidth

```cangjie
public var borderWidth: ?Length
```

**Function:** Sets the border width of the dialog backplate.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var cancel

```cangjie
public var cancel: ?VoidCallback
```

**Function:** Callback when the dialog is closed by clicking the mask layer.

**Type:** ?[VoidCallback](./cj-common-types.md#type-voidcallback)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var confirm

```cangjie
public var confirm: ?ActionSheetButtonOptions
```

**Function:** Enables the state, default focus, button style, text content, and click callback of the confirmation button. When the dialog is focused and no tab key navigation is performed, this button responds to the Enter key by default, and multiple dialogs can automatically focus and respond continuously.

**Type:** ?[ActionSheetButtonOptions](#class-actionsheetbuttonoptions)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var cornerRadius

```cangjie
public var cornerRadius: ?BorderRadiuses
```

**Function:** Sets the corner radius of the backplate. The radius of each of the four corners can be set separately.

**Type:** ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: ?Length
```

**Function:** Sets the height of the dialog backplate.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isModal

```cangjie
public var isModal: ?Bool
```

**Function:** Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not.

**Type:** ?Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var maskRect

```cangjie
public var maskRect: ?Rectangle
```

**Function:** The area of the dialog mask layer. Events within the mask layer area are not transmitted, while events outside the mask layer area are transmitted.

**Type:** ?[Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var message

```cangjie
public var message: ?ResourceStr
```

**Function:** Content of the dialog.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: ?ActionSheetOffset
```

**Function:** Offset of the dialog relative to the alignment position.

**Type:** ?[ActionSheetOffset](#class-actionsheetoffset)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillDismiss

```cangjie
public var onWillDismiss: ?Callback<DismissDialogAction, Unit>
```

**Function:** Interactive close callback function.

**Type:** ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](#class-dismissdialogaction), Unit>

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowOptions
```

**Function:** Sets the shadow of the dialog backplate.

**Type:** ?[ShadowOptions](./cj-common-types.md#class-shadowoptions)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var sheets

```cangjie
public var sheets: ?Array<SheetInfo>
```

**Function:** Sets the option content. Each option supports setting an image, text, and a selected callback.

**Type:** ?Array\<[SheetInfo](#class-sheetinfo)>

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** Whether to display this dialog in a sub-window when it needs to be displayed outside the main window.

**Type:** ?Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var subtitle

```cangjie
public var subtitle: ?ResourceStr
```

**Function:** Subtitle of the dialog.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var title

```cangjie
public var title: ?ResourceStr
```

**Function:** Title of the dialog.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: ?TransitionEffect
```

**Function:** Sets the transition effect for dialog display and exit.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: ?Length
```

**Function:** Sets the width of the dialog backplate.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?ActionSheetButtonOptions, ?VoidCallback, ?Array\<SheetInfo>, ?Bool, ?DialogAlignment, ?ActionSheetOffset, ?Rectangle, ?Bool, ?Bool, ?ResourceColor, ?BlurStyle, ?Callback\<DismissDialogAction, Unit>, ?TransitionEffect, ?BorderRadiuses, ?Length, ?Length, ?Length, ?ResourceColor, ?EdgeStyles, ?ShadowOptions)

```cangjie
public init(
    title!: ?ResourceStr,
    subtitle!: ?ResourceStr = None,
    message!: ?ResourceStr,
    confirm!: ?ActionSheetButtonOptions = None,
    cancel!: ?VoidCallback = None,
    sheets!: ?Array<SheetInfo>,
    autoCancel!: ?Bool = None,
    alignment!: ?DialogAlignment = None,
    offset!: ?ActionSheetOffset = None,
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
    borderColor!: ?ResourceColor = None,
    borderStyle!: ?EdgeStyles = None,
    shadow!: ?ShadowOptions = None
)
```

**Function:** Constructor of the ActionSheetOptions class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full**Initial Version:** 22  

**Parameters:**  

| Parameter Name | Type | Required | Default Value | Description |  
|:---|:---|:---|:---|:---|  
| title | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Popup title. <br/>When the text content is too long to display, an ellipsis replaces the hidden portion. |  
| subtitle | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Popup subtitle. <br/>When the text content is too long to display, an ellipsis replaces the hidden portion. |  
| message | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Popup content. <br/>A scrollbar is triggered when the text exceeds the display limit. |  
| confirm | ?[ActionSheetButtonOptions](#class-actionsheetbuttonoptions) | No | None | **Named parameter.** Configures the enabled state, default focus, button style, text content, and click callback for the confirmation button. When the popup gains focus and no tab navigation is performed, this button responds to the Enter key by default, and multiple popups can gain focus consecutively for continuous response. The default Enter key response does not take effect when `defaultFocus` is true. <br/>`enabled`: Whether the button responds to clicks. `true` means the button is responsive; `false` means it is not. <br/>Default: `true`. <br/>`defaultFocus`: Sets whether the button is the default focus. `true` means it is the default focus; `false` means it is not. <br/>Default: `false`. <br/>`style`: Sets the button's style. <br/>Default: `DialogButtonStyle.DEFAULT`. <br/>`value`: Button text content. When the text is too long to display, an ellipsis replaces the hidden portion. <br/>`action`: Callback when the button is selected. |  
| cancel | ?[VoidCallback](./cj-common-types.md#type-voidcallback) | No | None | **Named parameter.** Callback when the popup is closed by clicking the overlay. |
| sheets | ?Array\<[SheetInfo](#class-sheetinfo)> | Yes | - | **Named parameter.** Sets the option content, where each selection supports configuring an image, text, and selection callback. |   
| autoCancel | ?Bool | No | None | **Named parameter.** Whether the popup closes when clicking the overlay. <br/>If `true`, clicking the overlay closes the popup; if `false`, it does not. |   
| alignment | ?[DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | None | **Named parameter.** Vertical alignment of the popup. |  
| offset | ?[ActionSheetOffset](#class-actionsheetoffset) | No | None | **Named parameter.** Offset of the popup relative to the `alignment` position. |  
| maskRect | ?[Rectangle](./cj-common-types.md#class-rectangle) | No | None | **Named parameter.** Overlay area of the popup. Events within this area are blocked, while events outside are passed through. <br>**Note:**<br> `maskRect` does not take effect when `showInSubWindow` is `true`. |  
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display the popup in a sub-window when it needs to appear outside the main window. <br>Default: `false`, meaning the popup appears within the application rather than in an independent sub-window. <br>**Note:**<br> A popup with `showInSubWindow` set to `true` cannot trigger another popup with `showInSubWindow` set to `true`. |  
| isModal | ?Bool | No | None | **Named parameter.** Whether the popup is a modal window. Modal windows have an overlay; non-modal windows do not. <br/>Default: `true`, meaning the popup has an overlay. |  
| backgroundColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Background color of the popup. <br>**Note:**<br> When `backgroundColor` is set to a non-transparent color, `backgroundBlurStyle` must be set to `BlurStyle.NONE`; otherwise, the color display may not meet expectations. |  
| backgroundBlurStyle | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | No | None | **Named parameter.** Blur material for the popup background. <br>**Note:**<br> Set to `BlurStyle.NONE` to disable background blurring. When `backgroundBlurStyle` is set to a non-`NONE` value, do not set `backgroundColor`; otherwise, the color display may not meet expectations. |  
| onWillDismiss | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[DismissDialogAction](#class-dismissdialogaction), Unit> | No | None | **Named parameter.** Interactive close callback function. <br>**Note:**<br> 1. When the user performs actions to close the popup (e.g., clicking the overlay, swiping left/right, pressing the back button, or pressing ESC), if this callback is registered, the popup will not close immediately. The callback can determine whether to allow closing based on the `reason` parameter, which indicates the operation type that triggered the close attempt. The current component does not support the `CLOSE_BUTTON` enum value in `reason`. <br> 2. The `onWillDismiss` callback cannot intercept itself. |  
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Sets the transition effect for popup display and exit. <br>**Note:**<br> 1. If not set, the default display/exit animation is used. <br>2. Pressing the back key during the display animation interrupts it and triggers the exit animation, resulting in a combined effect of both animations. <br>3. Pressing the back key during the exit animation does not interrupt it; the animation continues, and pressing back again exits the application. |
| cornerRadius | ?[BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | None | **Named parameter.** Sets the corner radius of the background. The radius of each corner can be configured separately. <br>The maximum corner radius is limited by the component dimensions and cannot exceed half the width or height. Negative values are treated as defaults. <br>Percentage parameter: Sets the corner radius as a percentage of the parent popup's width and height. |  
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the width of the popup background. <br>**Note:**<br>1. The default maximum popup width is `400.vp`. <br>2. Percentage parameter: The reference width is the window width, which can be adjusted up or down. |  
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the height of the popup background. <br>**Note:**<br>1. The default maximum popup height is `0.9 * (window height - safe area)`. <br>2. Percentage parameter: The reference height is `(window height - safe area)`, which can be adjusted up or down. |  
| borderWidth | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the border width of the popup background. <br>Percentage parameter: Sets the border width as a percentage of the parent popup's width and height. <br>If the left/right border exceeds the popup width or the top/bottom border exceeds the popup height, the display may not meet expectations. |  
| borderColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Sets the border color of the popup background. If `borderColor` is used, it must be paired with `borderWidth`. |  
| borderStyle | ?[EdgeStyles](./cj-common-types.md#class-edgestyles) | No | None | **Named parameter.** Sets the border style of the popup background. If `borderStyle` is used, it must be paired with `borderWidth`. |  
| shadow | ?[ShadowOptions](./cj-common-types.md#class-shadowoptions) | No | None | **Named parameter.** Sets the shadow of the popup background. |  