# ohos.prompt_action

Creates and displays text prompts, dialogs, and action menus.

> **Note:**
>
> ohos.prompt_action only supports pure Cangjie scenarios and cannot be used in mixed ArkTS and Cangjie development scenarios.

## Import Module

```cangjie
import kit.UIKit.*
```

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

**Function:** Options for action menus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var buttons

```cangjie
public var buttons: Array<ButtonInfo>
```

**Function:** Represents an array of menu item buttons in the menu, structured as: ButtonInfo("button", Color.BLACK), supporting 1-6 buttons. When the number of buttons exceeds 6, only the first 6 buttons are displayed, and subsequent buttons are hidden.

**Type:** Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Whether to display the action menu in modal mode.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Whether to display the action menu in a sub-window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var title

```cangjie
public var title: ResourceStr
```

**Function:** Title of the action menu.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, Array\<ButtonInfo>, Bool, Bool)

```cangjie
public init(
    title!: ResourceStr = '',
    buttons!: Array<ButtonInfo>,
    showInSubWindow!: Bool = false,
    isModal!: Bool = true
)
```

**Function:** Options for action menus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | Title of the action menu. |
| buttons | Array\<[ButtonInfo](#class-buttoninfo)> | Yes | - | Array of menu item buttons in the menu, structured as: ButtonInfo("button",Color.BLACK), supporting 1-6 buttons. When the number of buttons exceeds 6, only the first 6 buttons are displayed, and subsequent buttons are hidden. |
| showInSubWindow | Bool | No | false | Whether to display the dialog in a sub-window when it needs to appear outside the main window. By default, dialogs are displayed within the application, not in an independent sub-window.<br>**Note:** <br> - A dialog with showInSubWindow set to true cannot trigger another dialog with showInSubWindow set to true. |
| isModal | Bool | No | true | Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not. By default, dialogs have a mask layer. |

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
    public var onDidAppear:() -> Unit
    public var onDidDisappear:() -> Unit
    public var onWillAppear:() -> Unit
    public var onWillDisappear:() -> Unit
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

**Function:** Options for dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Function:** Represents the vertical alignment of the dialog.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var autoCancel

```cangjie
public var autoCancel: Bool
```

**Function:** Whether to close the dialog when clicking the mask layer. true means closing the dialog, false means not closing.<br>Initial value: true

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Function:** Whether to respond to hover state.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Function:** Represents the default display area of the dialog in hover state.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Whether the dialog is a modal window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var keyboardAvoidMode

```cangjie
public var keyboardAvoidMode: KeyboardAvoidMode
```

**Function:** Sets whether the dialog automatically avoids the soft keyboard when it pops up.

**Type:** [KeyboardAvoidMode](#enum-keyboardavoidmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskColor

```cangjie
public var maskColor: ResourceColor
```

**Function:** Custom mask layer color.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** Represents the mask layer area of the dialog.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var offset

```cangjie
public var offset: Offset
```

**Function:** Represents the offset of the dialog relative to the alignment position.

**Type:** [Offset](./cj-common-types.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onDidAppear

```cangjie
public var onDidAppear:() -> Unit
```

**Function:** Callback when the dialog pops up.

**Type:** ()->Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onDidDisappear

```cangjie
public var onDidDisappear:() -> Unit
```

**Function:** Callback when the dialog disappears.

**Type:** ()->Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onWillAppear

```cangjie
public var onWillAppear:() -> Unit
```

**Function:** Callback before the dialog's display animation.

**Type:** ()->Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var onWillDisappear

```cangjie
public var onWillDisappear:() -> Unit
```

**Function:** Callback before the dialog's exit animation.

**Type:** ()->Unit

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

### var transition

```cangjie
public var transition: TransitionEffect
```

**Function:** Transition effects for dialog display and exit.

**Type:** [TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

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

**Function:** Constructs a BaseDialogOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | Mask layer area of the dialog. Events within the mask layer area are not transmitted, while events outside are transmitted. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | Vertical alignment of the dialog. |
| offset | [Offset](./cj-apis-componentutils.md#class-offset) | No | Offset(0.vp, 0.vp) | Offset of the dialog relative to the alignment position. |
| isModal | Bool | No | true | Whether the dialog is a modal window. Modal windows have a mask layer, while non-modal windows do not. By default, dialogs have a mask layer. |
| showInSubWindow | Bool | No | false | Whether to display the dialog in a sub-window when it needs to appear outside the main window. By default, dialogs are displayed within the application, not in an independent sub-window. |
| autoCancel | Bool | No | true | Whether to close the dialog when clicking the mask layer. true means closing the dialog, false means not closing. |
| maskColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color(0x33000000) | Custom mask layer color. |
| transition | [TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | TransitionEffect.OPACITY | Transition effects for dialog display and exit. |
| onDidAppear | ()->Unit | No | { => } | Callback when the dialog pops up. |
| onDidDisappear | ()->Unit | No | { => } | Callback when the dialog disappears. |
| onWillAppear | ()->Unit | No | { => } | Callback before the dialog's display animation. |
| onWillDisappear | ()->Unit | No | { => } | Callback before the dialog's exit animation. |
| keyboardAvoidMode | [KeyboardAvoidMode](#enum-keyboardavoidmode) | No | KeyboardAvoidMode.Default | Sets whether the dialog automatically avoids the soft keyboard when it pops up. |
| enableHoverMode | Bool | No | false | Whether to respond to hover state. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | Default display area of the dialog in hover state. |## class ButtonInfo

```cangjie
public class ButtonInfo {
    public var text: ResourceStr
    public var color: ResourceColor
    public var primary: Bool
    public init(text!: ResourceStr, color!: ResourceColor, primary!: Bool = false)
}
```

**Function:** Menu item button in a menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var color

```cangjie
public var color: ResourceColor
```

**Function:** Represents the text color of the button.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var primary

```cangjie
public var primary: Bool
```

**Function:** Indicates whether the button responds to the Enter key by default when the dialog is focused and no tab navigation is performed. For multiple buttons, only one button can have this field set to true; otherwise, none will respond. Nested dialogs can automatically focus and respond consecutively.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var text

```cangjie
public var text: ResourceStr
```

**Function:** Represents the text content of the button.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, ResourceColor, Bool)

```cangjie
public init(text!: ResourceStr, color!: ResourceColor, primary!: Bool = false)
```

**Function:** Constructs a ButtonInfo object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| text | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Button text content. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Button text color. |
| primary | Bool | No | false | Whether the button responds to the Enter key by default when the dialog is focused and no tab navigation is performed. |

## class CustomDialogOptions

```cangjie
public class CustomDialogOptions <: BaseDialogOptions {
    public var builder:() -> Unit
    public var backgroundColor: ResourceColor
    public var cornerRadius: BorderRadiuses
    public var borderWidth: EdgeWidths
    public var borderColor: EdgeColors
    public var borderStyle: EdgeStyles
    public var width: Length
    public var height: Length
    public var shadow:?ShadowOptions
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

**Function:** Custom dialog content, inherits from BaseDialogOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [BaseDialogOptions](#class-basedialogoptions)

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Represents the blur material of the dialog backdrop.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Represents the background color of the dialog.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderColor

```cangjie
public var borderColor: EdgeColors
```

**Function:** Represents the border color of the dialog backdrop.

**Type:** [EdgeColors](#class-edgecolors)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderStyle

```cangjie
public var borderStyle: EdgeStyles
```

**Function:** Represents the border style of the dialog backdrop.

**Type:** [EdgeStyles](./cj-common-types.md#class-edgestyles)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var borderWidth

```cangjie
public var borderWidth: EdgeWidths
```

**Function:** Represents the border width of the dialog backdrop.

**Type:** EdgeWidths

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var builder

```cangjie
public var builder:() -> Unit
```

**Function:** Represents the content of the custom dialog.

**Type:** ()->Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var cornerRadius

```cangjie
public var cornerRadius: BorderRadiuses
```

**Function:** Represents the corner radius of the backdrop.

**Type:** [BorderRadiuses](./cj-common-types.md#class-borderradiuses)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var height

```cangjie
public var height: Length
```

**Function:** Represents the height of the dialog backdrop.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var shadow

```cangjie
public var shadow:?ShadowOptions
```

**Function:** Represents the shadow of the dialog backdrop.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var width

```cangjie
public var width: Length
```

**Function:** Represents the width of the dialog backdrop.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

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

**Function:** CustomDialogOptions constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| builder | ()->Unit | Yes | - | Sets the content of the custom dialog. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | The mask layer area of the dialog. Events within this area are not passed through; events outside are passed through. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | The vertical alignment of the dialog. |
| offset | [Offset](./cj-apis-componentutils.md#class-offset) | No | Offset(0.vp, 0.vp) | The offset of the dialog relative to the alignment position. |
| isModal | Bool | No | true | Whether the dialog is modal. Modal dialogs have a mask layer; non-modal dialogs do not. Default is modal. |
| showInSubWindow | Bool | No | false | Whether to display the dialog in a sub-window when it needs to appear outside the main window. Default is within the application, not in an independent sub-window. |
| autoCancel | Bool | No | true | Whether to close the dialog when clicking the mask layer. true means close; false means do not close. |
| maskColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color(0x33000000) | Custom mask color. |
| transition | [TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | TransitionEffect.OPACITY | Sets the transition effect for dialog appearance and disappearance. |
| onDidAppear | ()->Unit | No | { => } | Callback when the dialog appears. |
| onDidDisappear | ()->Unit | No | { => } | Callback when the dialog disappears. |
| onWillAppear | ()->Unit | No | { => } | Callback before the dialog appearance animation. |
| onWillDisappear | ()->Unit | No | { => } | Callback before the dialog disappearance animation. |
| keyboardAvoidMode | [KeyboardAvoidMode](#enum-keyboardavoidmode) | No | KeyboardAvoidMode.Default | Sets whether the dialog automatically avoids the soft keyboard when it appears. |
| enableHoverMode | Bool | No | false | Whether to respond to hover state. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | Default display area of the dialog in hover state. |
| backgroundColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Transparent | Sets the background color of the dialog. |
| cornerRadius | [BorderRadiuses](./cj-common-types.md#class-borderradiuses) | No | BorderRadiuses(topLeft: 32.vp, topRight: 32.vp, bottomLeft: 32.vp, bottomRight: 32.vp) | Sets the corner radius of the backdrop. |
| borderWidth | EdgeWidths | No | EdgeWidths(top: 0.vp, right: 0.vp, bottom: 0.vp, left: 0.vp) | Sets the border width of the dialog backdrop. |
| borderColor | [EdgeColors](#class-edgecolors) | No | EdgeColors(top: Color.Black, right: Color.Black, bottom: Color.Black, left: Color.Black) | Sets the border color of the dialog backdrop. |
| borderStyle | [EdgeStyles](./cj-common-types.md#class-edgestyles) | No | EdgeStyles() | Sets the border style of the dialog backdrop. |
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 400.vp | Sets the width of the dialog backdrop. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 100.vp | Sets the height of the dialog backdrop. |
| shadow | ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions) | No | None | Sets the shadow of the dialog backdrop. |
| backgroundBlurStyle | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | The blur material of the dialog backdrop. |

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

**Function:** Border colors, used to describe the colors of the four edges of a component's border.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var bottom

```cangjie
public var bottom: ResourceColor
```

**Function:** Sets the bottom border color of the component.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var left

```cangjie
public var left: ResourceColor
```

**Function:** Sets the left border color of the component.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var right

```cangjie
public var right: ResourceColor
```

**Function:** Sets the right border color of the component.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var top

```cangjie
public var top: ResourceColor
```

**Function:** Sets the top border color of the component.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceColor, ResourceColor, ResourceColor, ResourceColor)

```cangjie
public init(
    top!: ResourceColor = Color.Black,
    right!: ResourceColor = Color.Black,
    bottom!: ResourceColor = Color.Black,
    left!: ResourceColor = Color.Black
)
```

**Function:** Constructs an EdgeColor object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Black | Top border color of the component. |
| right | [ResourceColor](../BasicServicesKit/c## class PromptActionInner

```cangjie
public class PromptActionInner {}
```

**Function:** Creates pop-up windows and handles pop-up actions.

## class ShowDialogOptions

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
    public var shadow:?ShadowOptions
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

**Function:** Options for dialog boxes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var alignment

```cangjie
public var alignment: DialogAlignment
```

**Function:** Indicates the vertical alignment of the pop-up window.

**Type:** [DialogAlignment](./cj-common-types.md#enum-dialogalignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Indicates the blur material of the pop-up window's background panel.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Indicates the background color of the pop-up window.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var buttons

```cangjie
public var buttons: Array<ButtonInfo>
```

**Function:** Indicates an array of buttons in the dialog box, supporting 1-3 buttons.

**Type:** Array\<[ButtonInfo](#class-buttoninfo)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Function:** Indicates whether to respond to hover state.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Function:** Indicates the default display area of the pop-up window in hover state.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var isModal

```cangjie
public var isModal: Bool
```

**Function:** Indicates whether the pop-up window is modal.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var maskRect

```cangjie
public var maskRect: Rectangle
```

**Function:** Indicates the mask layer area of the pop-up window.

**Type:** [Rectangle](./cj-common-types.md#class-rectangle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var message

```cangjie
public var message: ResourceStr
```

**Function:** Indicates the message content of the dialog box.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var offset

```cangjie
public var offset: Offset
```

**Function:** Indicates the offset of the pop-up window relative to the alignment position.

**Type:** [Offset](./cj-apis-componentutils.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var shadow

```cangjie
public var shadow:?ShadowOptions
```

**Function:** Indicates the shadow of the pop-up window's background panel.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var showInSubWindow

```cangjie
public var showInSubWindow: Bool
```

**Function:** Indicates whether to display the pop-up window in a sub-window when it needs to be displayed outside the main window.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var title

```cangjie
public var title: ResourceStr
```

**Function:** Indicates the title of the dialog box.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(ResourceStr, ResourceStr, Array\<ButtonInfo>, DialogAlignment, Offset, Rectangle, Bool, Bool, Color, BlurStyle, ?ShadowOptions, Bool, HoverModeAreaType)

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

**Function:** Constructs a ShowDialogOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| title | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | The title text of the dialog box. |
| message | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | '' | The message content text of the dialog box. |
| buttons | Array\<[ButtonInfo](#class-buttoninfo)> | No | [] | An array of buttons in the dialog box, supporting 1-3 buttons. |
| alignment | [DialogAlignment](./cj-common-types.md#enum-dialogalignment) | No | DialogAlignment.Default | The vertical alignment of the pop-up window. |
| offset | [Offset](./cj-apis-componentutils.md#class-offset) | No | Offset(0.vp, 0.vp) | The offset of the pop-up window relative to the alignment position. |
| maskRect | [Rectangle](./cj-common-types.md#class-rectangle) | No | Rectangle(x: 0.vp, y: 0.vp, width: 100.percent, height: 100.percent) | The mask layer area of the pop-up window. Events within the mask layer area are not transmitted, while events outside the mask layer area are transmitted. |
| showInSubWindow | Bool | No | false | Whether to display the pop-up window in a sub-window when it needs to be displayed outside the main window. By default, the pop-up window is displayed within the application, not in an independent sub-window. |
| isModal | Bool | No | true | Whether the pop-up window is modal. Modal windows have a mask layer, while non-modal windows do not. By default, the pop-up window has a mask layer. |
| backgroundColor | [Color](./cj-common-types.md#class-color) | No | Color.Transparent | The background color of the pop-up window. |
| backgroundBlurStyle | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | The blur material of the pop-up window's background panel. |
| shadow | ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions) | No | None | The shadow of the pop-up window's background panel. |
| enableHoverMode | Bool | No | false | Whether to respond to hover state. |
| hoverModeArea | [HoverModeAreaType](#enum-hovermodeareatype) | No | HoverModeAreaType.BottomScreen | The default display area of the pop-up window in hover state. |

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
    public var shadow:?ShadowOptions = None
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

**Function:** Options for text prompt boxes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var alignment

```cangjie
public var alignment: Alignment
```

**Function:** Indicates the alignment of the text prompt box.

**Type:** [Alignment](./cj-common-types.md#enum-alignment)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle
```

**Function:** Indicates the blur material of the text prompt box's background panel.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var backgroundColor

```cangjie
public var backgroundColor: ResourceColor
```

**Function:** Indicates the background color of the text prompt box.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var bottom

```cangjie
public var bottom: Length
```

**Function:** Indicates the distance from the text prompt box to the bottom of the screen.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var duration

```cangjie
public var duration: UInt32
```

**Function:** Indicates the display duration of the text prompt box, in milliseconds.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var enableHoverMode

```cangjie
public var enableHoverMode: Bool
```

**Function:** Indicates whether to respond to hover state.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var hoverModeArea

```cangjie
public var hoverModeArea: HoverModeAreaType
```

**Function:** Indicates the default display area of the text prompt box in hover state.

**Type:** [HoverModeAreaType](#enum-hovermodeareatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var message

```cangjie
public var message: ResourceStr
```

**Function:** Indicates the message content of the text prompt box.

**Type:** [ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var offset

```cangjie
public var offset: Offset
```

**Function:** Indicates the offset of the text prompt box relative to the alignment position.

**Type:** [Offset](./cj-apis-componentutils.md#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var shadow

```cangjie
public var shadow:?ShadowOptions = None
```

**Function:** Indicates the shadow of the text prompt box's background panel.

**Type:** ?[ShadowOptions](./cj-text-input-text.md#class-shadowoptions)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var showMode

```cangjie
public var showMode: ToastShowMode
```

**Function:** Indicates the display mode of the text prompt box.

**Type:** [ToastShowMode](#enum-toastshowmode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var textColor

```cangjie
public var textColor: ResourceColor
```

**Function:** Indicates the text color of the text prompt box.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

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

**Function:** Constructs a ShowToastOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| message | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | The text message to display. |
| duration | UInt32 | No | 1500 | The duration of the pop-up window, in milliseconds. Valid range: 1500ms-10000ms. If less than 1500ms, the default value is used; if greater than 10000ms, the upper limit of 10000ms is used. |
| bottom | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 80.vp | Sets the height of the pop-up window's bottom border from the navigation bar. |
| showMode | [ToastShowMode](#enum-toastshowmode) | No | ToastShowMode.Default | Sets whether the pop-up window## enum HoverModeAreaType

## enum HoverModeAreaType

```cangjie
public enum HoverModeAreaType <: Equatable<HoverModeAreaType> {
    | TopScreen
    | BottomScreen
    | ...
}
```

**Function:** Specifies the default display area type for popups in hover state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<HoverModeAreaType>

### BottomScreen

```cangjie
BottomScreen
```

**Function:** Indicates the popup displays at the bottom of the screen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### TopScreen

```cangjie
TopScreen
```

**Function:** Indicates the popup displays at the top of the screen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(HoverModeAreaType)

```cangjie
public operator func !=(other: HoverModeAreaType): Bool
```

**Function:** Determines whether two HoverModeAreaType values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[HoverModeAreaType](#enum-hovermodeareatype)|Yes|-|Another HoverModeAreaType value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise returns false.|

### func ==(HoverModeAreaType)

```cangjie
public operator func ==(other: HoverModeAreaType): Bool
```

**Function:** Determines whether two HoverModeAreaType values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[HoverModeAreaType](#enum-hovermodeareatype)|Yes|-|Another HoverModeAreaType value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if equal, otherwise returns false.|

## enum KeyboardAvoidMode

```cangjie
public enum KeyboardAvoidMode <: Equatable<KeyboardAvoidMode> {
    | Default
    | None
    | ...
}
```

**Function:** Keyboard avoidance mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<KeyboardAvoidMode>

### Default

```cangjie
Default
```

**Function:** Indicates the default keyboard avoidance mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### None

```cangjie
None
```

**Function:** Indicates no keyboard avoidance.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(KeyboardAvoidMode)

```cangjie
public operator func !=(other: KeyboardAvoidMode): Bool
```

**Function:** Determines whether two KeyboardAvoidMode values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[KeyboardAvoidMode](#enum-keyboardavoidmode)|Yes|-|Another KeyboardAvoidMode value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise returns false.|

### func ==(KeyboardAvoidMode)

```cangjie
public operator func ==(other: KeyboardAvoidMode): Bool
```

**Function:** Determines whether two KeyboardAvoidMode values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[KeyboardAvoidMode](#enum-keyboardavoidmode)|Yes|-|Another KeyboardAvoidMode value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if equal, otherwise returns false.|

## enum ToastShowMode

```cangjie
public enum ToastShowMode <: Equatable<ToastShowMode> {
    | Default
    | TopMost
    | ...
}
```

**Function:** Toast display mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<ToastShowMode>

### Default

```cangjie
Default
```

**Function:** Indicates the default display mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### TopMost

```cangjie
TopMost
```

**Function:** Indicates topmost display mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(ToastShowMode)

```cangjie
public operator func !=(other: ToastShowMode): Bool
```

**Function:** Determines whether two ToastShowMode values are unequal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ToastShowMode](#enum-toastshowmode)|Yes|-|Another ToastShowMode value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise returns false.|

### func ==(ToastShowMode)

```cangjie
public operator func ==(other: ToastShowMode): Bool
```

**Function:** Determines whether two ToastShowMode values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ToastShowMode](#enum-toastshowmode)|Yes|-|Another ToastShowMode value to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if equal, otherwise returns false.|

## type ShowActionMenuCallBack

```cangjie
public type ShowActionMenuCallBack = AsyncCallback<Int32>
```

**Function:** [ShowActionMenuCallBack](#type-showactionmenucallback) is an alias of [AsyncCallback\<Int32>](../BasicServicesKit/cj-apis-base.md#type-asynccallback) type.

## type ShowDialogCallBack

```cangjie
public type ShowDialogCallBack = AsyncCallback<Int32>
```

**Function:** [ShowDialogCallBack](#type-showdialogcallback) is an alias of [AsyncCallback\<Int32>](../BasicServicesKit/cj-apis-base.md#type-asynccallback) type.