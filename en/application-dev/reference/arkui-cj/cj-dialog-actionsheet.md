# Action Sheet Dialog (ActionSheet)

A list dialog component.

## class ActionSheetButtonOptions

```cangjie
public class ActionSheetButtonOptions {
    public var value: ResourceStr
    public var action: VoidCallback
    public var enabled: Bool
    public var defaultFocus: Bool
    public var style: DialogButtonStyle

    public init(
        value!: ResourceStr,
        action!: VoidCallback,
        enabled!: Bool = true,
        defaultFocus!: Bool = false,
        style!: DialogButtonStyle = DialogButtonStyle.Default
    )
}
```

**Description:** Styles for buttons in the dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var action

```cangjie
public var action: VoidCallback
```

**Description:** Callback when the button is selected.

**Type:** [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var defaultFocus

```cangjie
public var defaultFocus: Bool
```

**Description:** Sets whether the button is the default focus.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var enabled

```cangjie
public var enabled: Bool
```

**Description:** Determines whether the button responds to clicks.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var style

```cangjie
public var style: DialogButtonStyle
```

**Description:** Sets the style of the button.

**Type:** [DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var value

```cangjie
public var value: ResourceStr
```

**Description:** Text content of the button.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, VoidCallback, Bool, Bool, DialogButtonStyle)

```cangjie
public init(
    value!: ResourceStr,
    action!: VoidCallback,
    enabled!: Bool = true,
    defaultFocus!: Bool = false,
    style!: DialogButtonStyle = DialogButtonStyle.Default
)
```

**Description:** Button parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Text content of the button. |
| action | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | Yes | - | Callback when the button is selected. |
| enabled | Bool | No | true | **Named parameter.** Whether the button responds to clicks. `true` means the button responds, `false` means it doesn't. |
| defaultFocus | Bool | No | false | **Named parameter.** Sets whether the button is the default focus. `true` means it is the default focus, `false` means it isn't. |
| style | [DialogButtonStyle](./cj-common-types.md#enum-dialogbuttonstyle) | No | DialogButtonStyle.Default | **Named parameter.** Sets the style of the button. |

## class ActionSheetOffset

```cangjie
public class ActionSheetOffset {
    public var dx: Length
    public var dy: Length

    public init(
        dx!: Length,
        dy!: Length
    )
}
```

**Description:** Alignment settings for the dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var dx

```cangjie
public var dx: Length
```

**Description:** Horizontal offset of the dialog relative to the alignment position. Requires explicit pixel units (e.g., '10px') or percentage strings (e.g., '100%').

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var dy

```cangjie
public var dy: Length
```

**Description:** Vertical offset of the dialog relative to the alignment position. Requires explicit pixel units (e.g., '10px') or percentage strings (e.g., '100%').

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Length, Length)

```cangjie
public init(
    dx!: Length,
    dy!: Length
)
```

**Description:** Constructor for the ActionSheetOffset class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| dx | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Horizontal offset of the dialog relative to the alignment position. Requires explicit pixel units (e.g., '10px') or percentage strings (e.g., '100%'). |
| dy | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Vertical offset of the dialog relative to the alignment position. Requires explicit pixel units (e.g., '10px') or percentage strings (e.g., '100%'). |

## class ActionSheetOptions

```cangjie
public class ActionSheetOptions {
    public var title: ResourceStr
    public var message: ResourceStr
    public var sheets: Array<SheetInfo>
    public var subtitle: ResourceStr
    public var confirm: ActionSheetButtonOptions
    public var autoCancel: Bool
    public var cancel: VoidCallback
    public var alignment: DialogAlignment
    public var offset: ActionSheetOffset
    public var maskRect: Rectangle
    public var showInSubWindow: Bool
    public var isModal: Bool
    public var backgroundColor: ResourceColor
    public var backgroundBlurStyle: BlurStyle
    public var onWillDismiss:?Callback<DismissDialogAction, Unit>
    public var cornerRadius: BorderRadiuses
    public var borderWidth: Length
    public var borderColor: ResourceColor
    public var borderStyle: EdgeStyles
    public var width:?Length
    public var height:?Length
    public var shadow: ShadowOptions
    public var transition:?TransitionEffect

    /**
     * Constructor of ActionSheetOptions
     *
     * @param { ResourceStr } title
     * @param { ResourceStr } message
     * @param { Array<SheetInfo> } sheets
     * @param { ResourceStr } subtitle
     * @param { ActionSheetButtonOptions } confirm
     * @param { Bool } autoCancel
     * @param { VoidCallback } cancel
     * @param { DialogAlignment } alignment
     * @param { ?ActionSheetOffset } offset
     * @param { Rectangle } maskRect
     * @param { Bool } showInSubWindow
     * @param { ResourceColor } backgroundColor
     * @param { BlurStyle } backgroundBlurStyle
     * @param { ?Callback<DismissDialogAction, Unit> } onWillDismiss
     * @param { BorderRadiuses } cornerRadius
     * @param { Length } borderWidth
     * @param { ResourceColor } borderColor
     * @param { EdgeStyles } borderStyle
     * @param { ?Length } width
     * @param { ?Length } height
     * @param { ShadowOptions } shadow
     * @param { ?TransitionEffect } transition
     * @returns { ActionSheetOptions }
     * @relation interface ActionSheetOptions
     */
    public init(
        title!: ResourceStr,
        message!: ResourceStr,
        sheets!: Array<SheetInfo>,
        subtitle!: ResourceStr = "",
        confirm!: ActionSheetButtonOptions = ActionSheetButtonOptions(value: "", action: {=>}),
        autoCancel!: Bool = true,
        cancel!: VoidCallback = {=>},
        alignment!: DialogAlignment = DialogAlignment.Bottom,
        offset!: ?ActionSheetOffset = None,
        maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
        showInSubWindow!: Bool = false,
        isModal!: Bool = true,
        backgroundColor!: ResourceColor = Color.Transparent,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
        cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp,
            bottomLeft: 32.vp, bottomRight: 32.vp),
        borderWidth!: Length = 0.vp,
        borderColor!: ResourceColor = Color.Black,
        borderStyle!: EdgeStyles = EdgeStyles(),
        width!: ?Length = None,
        height!: ?Length = None,
        shadow!: ShadowOptions = ShadowOptions(radius: 0.0),
        transition!: ?TransitionEffect = None
    )
}
```

**Description:** Constructs an object of type ActionSheetOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Description:** Vertical alignment of the dialog.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var autoCancel

```cangjie
public var autoCancel: Bool
```

**Description:** Whether the dialog closes when clicking the mask layer.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Description:** Blur effect style for the dialog background.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Description:** Background color of the dialog.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderColor

```cangjie
public var borderColor: ResourceColor
```

**Description:** Sets the border color of the dialog background. Must be used with the `borderWidth` property.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderStyle

```cangjie
public var borderStyle: EdgeStyles
```

**Description:** Sets the border style of the dialog background. Must be used with the `borderWidth` property.

**Type:** [EdgeStyles](./cj-common-types.md#class-edgestyles)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21### var borderWidth

```cangjie
public var borderWidth: Length
```

**Function:** Sets the border width of the dialog backdrop.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var cancel

```cangjie
public var cancel: VoidCallback
```

**Function:** Callback triggered when clicking the mask layer to close the dialog.

**Type:** [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var confirm

```cangjie
public var confirm: ActionSheetButtonOptions
```

**Function:** Configures the enabled state, default focus, button style, text content, and click callback of the confirmation button. When the dialog gains focus and no tab key navigation is performed, this button responds to the Enter key by default, and multiple dialogs can automatically gain focus for continuous response.

**Type:** [ActionSheetButtonOptions](#class-actionsheetbuttonoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var cornerRadius

```cangjie
public var cornerRadius: BorderRadiuses
```

**Function:** Sets the corner radius of the backdrop. The radius of each corner can be set individually.

**Type:** [BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var height

```cangjie
public var height:?Length
```

**Function:** Sets the height of the dialog backdrop.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Indicates whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** Specifies the mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside the area are transmitted.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var message

```cangjie
public var message: ResourceStr
```

**Function:** Content of the dialog.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var offset

```cangjie
public var offset: ActionSheetOffset
```

**Function:** Offset of the dialog relative to the position specified by `alignment`.

**Type:** [ActionSheetOffset](#class-actionsheetoffset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onWillDismiss

```cangjie
public var onWillDismiss:?Callback<DismissDialogAction, Unit>
```

**Function:** Interactive close callback function.

**Type:** ?[Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[DismissDialogAction](#class-dismissdialogaction),Unit>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var shadow

```cangjie
public var shadow: ShadowOptions
```

**Function:** Sets the shadow of the dialog backdrop.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var sheets

```cangjie
public var sheets: Array<SheetInfo>
```

**Function:** Sets the option content. Each option supports configuring an image, text, and selection callback.

**Type:** Array\<[SheetInfo](#class-sheetinfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Determines whether the dialog should be displayed in a sub-window when it needs to appear outside the main window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var subtitle

```cangjie
public var subtitle: ResourceStr
```

**Function:** Subtitle of the dialog.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var title

```cangjie
public var title: ResourceStr
```

**Function:** Title of the dialog.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var transition

```cangjie
public var transition:?TransitionEffect
```

**Function:** Sets the transition effect for displaying and exiting the dialog.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var width

```cangjie
public var width:?Length
```

**Function:** Sets the width of the dialog backdrop.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, ResourceStr, Array\<SheetInfo>, ResourceStr, ActionSheetButtonOptions, Bool, VoidCallback, DialogAlignment, ?ActionSheetOffset, Rectangle, Bool, Bool, ResourceColor, BlurStyle, ?Callback\<DismissDialogAction,Unit>, BorderRadiuses, Length, ResourceColor, EdgeStyles, ?Length, ?Length, ?TransitionEffect)

```cangjie

/**
 * Constructor of ActionSheetOptions
 *
 * @param { ResourceStr } title
 * @param { ResourceStr } message
 * @param { Array<SheetInfo> } sheets
 * @param { ResourceStr } subtitle
 * @param { ActionSheetButtonOptions } confirm
 * @param { Bool } autoCancel
 * @param { VoidCallback } cancel
 * @param { DialogAlignment } alignment
 * @param { ?ActionSheetOffset } offset
 * @param { Rectangle } maskRect
 * @param { Bool } showInSubWindow
 * @param { ResourceColor } backgroundColor
 * @param { BlurStyle } backgroundBlurStyle
 * @param { ?Callback<DismissDialogAction, Unit> } onWillDismiss
 * @param { BorderRadiuses } cornerRadius
 * @param { Length } borderWidth
 * @param { ResourceColor } borderColor
 * @param { EdgeStyles } borderStyle
 * @param { ?Length } width
 * @param { ?Length } height
 * @param { ?TransitionEffect } transition
 * @returns { ActionSheetOptions }
 * @relation interface ActionSheetOptions
 */
public init(
    title!: ResourceStr,
    message!: ResourceStr,
    sheets!: Array<SheetInfo>,
    subtitle!: ResourceStr = "",
    confirm!: ActionSheetButtonOptions = ActionSheetButtonOptions(value: "", action: {=>}),
    autoCancel!: Bool = true,
    cancel!: VoidCallback = {=>},
    alignment!: DialogAlignment = DialogAlignment.Bottom,
    offset!: ?ActionSheetOffset = None,
    maskRect!: Rectangle = Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent),
    showInSubWindow!: Bool = false,
    isModal!: Bool = true,
    backgroundColor!: ResourceColor = Color.Transparent,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    onWillDismiss!: ?Callback<DismissDialogAction, Unit> = None,
    cornerRadius!: BorderRadiuses = BorderRadiuses(topLeft: 32.vp, topRight: 32.vp,
        bottomLeft: 32.vp, bottomRight: 32.vp),
    borderWidth!: Length = 0.vp,
    borderColor!: ResourceColor = Color.Black,
    borderStyle!: EdgeStyles = EdgeStyles(),
    width!: ?Length = None,
    height!: ?Length = None,
    transition!: ?TransitionEffect = None
)
```

**Function:** Constructs an object of type `ActionSheetOptions`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Title of the dialog. <br/>If the text is too long to display, an ellipsis replaces the hidden part. |
| message | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Content of the dialog. <br/>A scrollbar appears if the text exceeds the display area. |
| sheets | Array\<[SheetInfo](#class-sheetinfo)> | Yes | - | Sets the option content. Each option supports configuring an image, text, and selection callback. |
| subtitle | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** Subtitle of the dialog. <br/>If the text is too long to display, an ellipsis replaces the hidden part. |
| confirm | [ActionSheetButtonOptions](#class-actionsheetbuttonoptions) | No | ActionSheetButtonOptions(value: "", action: { => }) | **Named parameter.** Configures the enabled state, default focus, button style, text content, and click callback of the confirmation button. When the dialog gains focus and no tab key navigation is performed, this button responds to the Enter key by default, and multiple dialogs can automatically gain focus for continuous response. The default Enter key response does not take effect when `defaultFocus` is true. <br/>`enabled`: Determines whether the button responds to clicks. `true` means the button can respond; `false` means it cannot. <br/>Initial value: `true`. <br/>`defaultFocus`: Sets whether the button is the default focus. `true` means it is the default focus; `false` means it is not. <br/>Initial value: `false`. <br/>`style`: Sets the button's style. <br/>Initial value: `DialogButtonStyle.DEFAULT`. <br/>`value`: Text content of the button. If the text is too long to display, an ellipsis replaces the hidden part. <br/>`action`: Callback triggered when the button is selected. |
| autoCancel | Bool | No | true | **Named parameter.** Determines whether clicking the mask layer closes the dialog. <br/>`true` means clicking the mask layer closes the dialog; `false` means it does not. |
| cancel | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | No | { => } | **Named parameter.** Callback triggered when clicking the mask layer to close the dialog. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Bottom | **Named parameter.** Vertical alignment of the dialog. |
| offset | ?[ActionSheetOffset](#class-actionsheetoffset) | No | None | **Named parameter.** Requires explicit pixel units (e.g., `10.vp`) or percentage strings (e.g., `100.percent`). <br/>If no unit is specified, `vp` is used by default (e.g., `10` is equivalent to `10.vp`). <br/>Offset of the dialog relative to the position specified by `alignment`. <br/>Initial value: <br/>1. When `alignment` is set to `Top`, `TopStart`, or `TopEnd`, the default is `{dx: 0, dy: 40.vp}`. <br/>2. For other alignments, the default is `{dx: 0, dy: -40.vp}`. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0, y: 0, width: 100.percent, height: 100.percent) | **Named parameter.** Mask layer area of the dialog. Events within this area are not transmitted; events outside are transmitted. <br>**Note:** <br> `maskRect` does not take effect when `showInSubWindow` is `true`. |
| showInSubWindow | Bool | No | false | **Named parameter.** Determines whether the dialog should be displayed in a sub-window when it needs to appear outside the main window. <br>Initial value: `false`, meaning the dialog appears within the application, not in an independent sub-window. <br>**Note:** <br> A dialog with `showInSubWindow` set to `true` cannot trigger another dialog with `showInSubWindow` set to `true`. |
| isModal | Bool | No | true | **Named parameter.** Indicates whether the dialog is a modal window. Modal windows have a mask layer; non-modal windows do not. <br/>Initial value: `true`, meaning the dialog has a mask layer. |
| backgroundColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Transparent | **Named parameter.** Background color of the dialog backdrop. <br>**Note:** <br> When `backgroundColor` is set to a non-transparent color, `backgroundBlurStyle` must be set to `BlurStyle.NONE`; otherwise, the color display may not meet expectations. |
| backgroundBlurStyle | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | **Named parameter.** Blur material of the dialog backdrop. <br>**Note:** <br> Set to `BlurStyle.NONE` to disable background blurring. When `backgroundBlurStyle` is set to a non-`NONE` value, avoid setting `backgroundColor`; otherwise, the color display may not meet expectations. |
| onWillDismiss | ?[Callback](../BasicServicesKit/cj-apis-base.md#type-Callback)\<[DismissDialogAction](#class-dismissdialogaction),Unit> | No | None | **Named parameter.** Interactive close callback function. <br>**Note:** <br> 1. When the user performs actions like clicking the mask layer to close, swiping left/right, pressing the back button, or using the ESC key to close the dialog, if this callback is registered, the dialog will not close immediately. The callback provides the `reason` for the close attempt, allowing conditional closure based on the operation type. The current component does not support the `CLOSE_BUTTON` enum value in the `reason` parameter. <br> 2. The `onWillDismiss` callback cannot intercept itself. |
| cornerRadius | [BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) | **Named parameter.** Sets the corner radius of the backdrop. Each corner's radius can be set individually. <br>The maximum corner radius is limited by the component's dimensions (half of the width or height). Negative values are treated as the default. <br>Percentage-based parameters: The corner radius is calculated as a percentage of the dialog's width and height. <br>**Note:** <br> When `cornerRadius` is of type `LocalizedBorderRadiuses`, it supports layout adjustments based on language preferences. |
| borderWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Sets the border width of the dialog backdrop. <br>Percentage-based parameters: The border width is calculated as a percentage of the dialog's width and height. <br>If the left/right borders exceed the dialog's width or the top/bottom borders exceed its height, the display may not meet expectations. <br>**Note:** <br> When `borderWidth` is of type `LocalizedEdgeWidths`, it supports layout adjustments based on language preferences. |
| borderColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Sets the border color of the dialog backdrop. Requires `borderWidth` to be set. <br>**Note:** <br> When `borderColor` is of type `LocalizedEdgeColors`, it supports layout adjustments based on language preferences. |
| borderStyle | [EdgeStyles](./cj-common-types.md#class-edgestyles) | No | EdgeStyles() | **Named parameter.** Sets the border style of the dialog backdrop. Requires `borderWidth` to be set. |
| width | ?[Length](../BasicServices## class SheetInfo

```cangjie
public class SheetInfo {
    public var title: ResourceStr
    public var action: VoidCallback
    public var icon:?ResourceStr

    public init(
        title!: ResourceStr,
        action!: VoidCallback,
        icon!: ?ResourceStr = None
    )
}
```

**Function:** Configures option content, where each option supports setting an image, text, and selection callback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var action

```cangjie
public var action: VoidCallback
```

**Function:** Callback when the option is selected.

**Type:** [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var icon

```cangjie
public var icon:?ResourceStr
```

**Function:** Icon of the option. No icon is displayed by default.

**Type:** ?[ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var title

```cangjie
public var title: ResourceStr
```

**Function:** Text content of the option.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, VoidCallback, ?ResourceStr)

```cangjie
public init(
    title!: ResourceStr,
    action!: VoidCallback,
    icon!: ?ResourceStr = None
)
```

**Function:** Parameters for option content.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Text content of the option.<br/>A scroll bar appears when the text is too long. |
| action | [VoidCallback](../BasicServicesKit/cj-apis-base.md#type-VoidCallback) | Yes | - | Callback when the option is selected. |
| icon | ?[ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | None | **Named parameter.** Icon of the option. No icon is displayed by default.<br/>The string format can be used to load network images and local images, and is commonly used to load network images. When referencing a local image using a relative path, for example, Image("common/test.jpg"). |

## enum DismissReason

```cangjie
public enum DismissReason {
    | PressBack
    | TouchOutside
    | CloseButton
    | SlideDown
    | ...
}
```

**Function:** Reason for closing the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### CloseButton

```cangjie
CloseButton
```

**Function:** The close button was clicked.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### PressBack

```cangjie
PressBack
```

**Function:** Three-key back, left/right swipe, or ESC key was pressed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### SlideDown

```cangjie
SlideDown
```

**Function:** Closed by sliding down.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### TouchOutside

```cangjie
TouchOutside
```

**Function:** Clicked on the mask layer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21