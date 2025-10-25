# Popup Control

Bind a popup dialog to a component and configure its content, interaction logic, and display state.

> **Note:**
>
> The display state of the popup dialog is reported in the `onStateChange` event callback. Its visibility has no strong correlation with the creation or destruction of the component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func bindPopup(Bool, CustomPopupOptions)

```cangjie
public func bindPopup(show: Bool, popup: CustomPopupOptions): This
```

**Function:** Binds a custom popup dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| show | Bool | Yes | - | Whether to display the popup. |
| popup | [CustomPopupOptions](#class-custompopupoptions) | Yes | - | Custom popup options. |

## func bindPopup(Bool, PopupOptions)

```cangjie
public func bindPopup(show: Bool, popup: PopupOptions): This
```

**Function:** Binds a popup dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| show | Bool | Yes | - | Whether to display the popup. |
| popup | [PopupOptions](#class-popupoptions) | Yes | - | Popup options. |

## Basic Type Definitions

### class CustomPopupOptions

```cangjie
public class CustomPopupOptions {
    public var builder: CustomBuilder = { => }
    public var placement: Placement = Placement.Bottom
    public var maskColor: ResourceColor = Color(0x1000000)
    public var backgroundColor: Color = Color(0x1000000)
    public var enableArrow: Bool = true
    public var autoCancel: Bool = true
    public var onStateChange: Option <(PopupStateChangeParam) -> Unit>= Option.None
    public var popupColor:?Color = None
    public var arrowOffset: Length = 0.vp
    public var showInSubWindow: Bool = false
    public var mask:?Color = None
    public var targetSpace: Length = 0.vp
    public var offset: Position = Position(x: 0.0, y: 0.0)
    public var width: Length = 0.vp
    public var arrowPointPosition: Option<ArrowPointPosition>= None
    public var arrowWidth: Length = 16.vp
    public var arrowHeight: Length = 8.vp
    public var radius: Length = 20.vp
    public var shadow: ShadowStyle = ShadowStyle.OuterDefaultMD
    public var backgroundBlurStyle: BlurStyle = BlurStyle.ComponentUltraThick
    public var focusable: Bool = false
    public var transition: Option<TransitionEffect>= Option.None
    public var onWillDismiss: Option <(DismissPopupAction) -> Unit>= None
    public var followTransformOfTarget: Bool = false
    public init(
        builder!: () -> Unit,
        placement!: Placement = Placement.Bottom,
        maskColor!: Color = Color(0x1000000),
        popupColor!: Color = Color(0x1000000),
        enableArrow!: Bool = true,
        autoCancel!: Bool = true,
        onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
        showInSubWindow!: Bool, // 5.1 start
        backgroundColor!: Color = Color(0x1000000),
        arrowOffset!: Length = 0.vp,
        mask!: ?Color = None,
        targetSpace!: Length = 0.vp,
        offset!: Position = Position(x: 0.0, y: 0.0),
        width!: Length = 0.vp,
        arrowPointPosition!: ?ArrowPointPosition = None,
        arrowWidth!: Length = 16.vp,
        arrowHeight!: Length = 16.vp,
        radius!: Length = 20.vp,
        shadow!: ShadowStyle = ShadowStyle.OuterDefaultMD,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        focusable!: Bool = false,
        transition!: Option<TransitionEffect> = Option.None,
        onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None,
        followTransformOfTarget!: Bool = false
    )
}
```

**Function:** Parameters for displaying a popup dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowHeight

```cangjie
public var arrowHeight: Length = 8.vp
```

**Function:** Sets the arrow height. Default: 8.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowOffset

```cangjie
public var arrowOffset: Length = 0.vp
```

**Function:** Sets the offset of the popup arrow on the dialog. When the arrow is above or below the bubble, a value of 0 means the arrow is aligned to the far left, and the offset is the distance from the arrow to the far left (default is centered). When the arrow is to the left or right of the bubble, the offset is the distance from the arrow to the top (default is centered). If displayed at the screen edge, the bubble will automatically shift left or right. A value of 0 means the arrow always points to the bound component.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowPointPosition

```cangjie
public var arrowPointPosition: Option<ArrowPointPosition>= None
```

**Function:** Sets the position of the bubble's arrow relative to the parent component. The arrow can be positioned at "Start", "Center", or "End" in both vertical and horizontal directions. All positions are within the parent component's bounds and will not exceed them.

**Type:** [ArrowPointPosition](cj-common-types.md#enum-arrowpointposition)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowWidth

```cangjie
public var arrowWidth: Length = 16.vp
```

**Function:** Sets the arrow width. If the set arrow width exceeds the length of the side minus twice the bubble's corner radius, the arrow will not be drawn. Default: 16.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var autoCancel

```cangjie
public var autoCancel: Bool = true
```

**Function:** Whether to automatically close the bubble when there is an operation on the page. Default: true.

**Type:** Bool

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle = BlurStyle.ComponentUltraThick
```

**Function:** Sets the bubble's blur background parameters. Default: BlurStyle.COMPONENT_ULTRA_THICK.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundColor

```cangjie
public var backgroundColor: Color = Color(0x1000000)
```

**Function:** Sets the background color of the bubble.

**Type:** [Color](cj-common-types.md#class-color)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var builder

```cangjie
public var builder: CustomBuilder = { => }
```

**Function:** Builder for the bubble's content.

> **Note:**
>
> Popup is a universal property. Custom popups do not support nested popups. The `position` property is not supported for the first-layer container components under `builder`. Using it will cause the bubble not to display. If custom components are used in `builder`, their `aboutToAppear` and `aboutToDisappear` lifecycles are unrelated to the popup's visibility and cannot be used to determine the popup's display state.

**Type:** [CustomBuilder](./cj-common-types.md#type-custombuilder)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var enableArrow

```cangjie
public var enableArrow: Bool = true
```

**Function:** Whether to display the arrow. If the bubble's length on the arrow's side is insufficient to display the arrow, it will not be shown by default. For example, if `placement` is set to `Left` and the bubble's height is less than the sum of the arrow's width (32.vp) and twice the bubble's corner radius (48.vp) (80.vp), the arrow will not be displayed. Default: true.

**Type:** Bool

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var focusable

```cangjie
public var focusable: Bool = false
```

**Function:** Whether the bubble gains focus after popping up. Default: false.

**Type:** Bool

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var followTransformOfTarget

```cangjie
public var followTransformOfTarget: Bool = false
```

**Function:** Whether the bubble can be displayed at the transformed position when the bound host component or its parent container has transformations like rotation or scaling. Default: false.

**Type:** Bool

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var mask

```cangjie
public var mask:?Color = None
```

**Function:** Sets the color of the mask layer.

**Type:** ?[Color](cj-common-types.md#class-color)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var maskColor

```cangjie
public var maskColor: ResourceColor = Color(0x1000000)
```

**Function:** Sets the color of the bubble's mask layer.

**Type:** [ResourceColor](cj-common-types.md#interface-resourcecolor)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offset

```cangjie
public var offset: Position = Position(x: 0.0, y: 0.0)
```

**Function:** Sets the offset of the popup component relative to the position set by `placement`. Percentage values are not supported.

**Type:** [Position](cj-common-types.md#class-position)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var onStateChange

```cangjie
public var onStateChange: Option <(PopupStateChangeParam) -> Unit>= Option.None
```

**Function:** Sets the callback for popup state changes, with the parameter being the current display state of the popup.

**Type:** ([PopupStateChangeParam](./cj-common-types.md#class-popupstatechangeparam))->Unit

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var onWillDismiss

```cangjie
public var onWillDismiss: Option <(DismissPopupAction) -> Unit>= None
```

**Function:** Sets the popup's interactive dismissal interception switch and callback function.

> **Note:**
>
> The `onWillDismiss` callback cannot perform another `onWillDismiss` interception.

**Type:** ([DismissPopupAction](#class-dismisspopupaction))->Unit

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var placement

```cangjie
public var placement: Placement = Placement.Bottom
```

**Function:** Sets the preferred display position of the bubble component. If the current position cannot accommodate it, the position will be adjusted automatically. Default: Placement.Bottom.

**Type:** [Placement](cj-common-types.md#enum-placement)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var popupColor

```cangjie
public var popupColor:?Color = None
```

**Function:** Sets the color of the bubble. To remove the blur background fill effect, set `backgroundBlurStyle` to `BlurStyle.NONE`.

**Type:** ?[Color](cj-common-types.md#class-color)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var radius

```cangjie
public var radius: Length = 20.vp
```

**Function:** Sets the corner radius of the bubble. Default: 20.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var shadow

```cangjie
public var shadow: ShadowStyle = ShadowStyle.OuterDefaultMD
```

**Function:** Sets the shadow of the bubble. Default: ShadowStyle.OUTER_DEFAULT_MD.

**Type:** [ShadowStyle](cj-common-types.md#enum-shadowstyle)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var showInSubWindow

```cangjie
public var showInSubWindow: Bool = false
```

**Function:** Whether to display the bubble in a sub-window. Default: false (not displayed).

**Type:** Bool

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var targetSpace

```cangjie
public var targetSpace: Length = 0.vp
```

**Function:** Sets the gap between the popup and the target.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var transition

```cangjie
public var transition: Option<TransitionEffect> = Option.None
```

**Function:** Customizes the animation effects for popup display and exit.

> **Note:**
>
> - If not set, the default display/exit animations are used.
> - Pressing the back key during the display animation will interrupt it and execute the exit animation, resulting in a combined effect of both animations.
> - Pressing the back key during the exit animation will not interrupt it; the exit animation continues, and the back key is not responded to.

**Type:** [TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var width

```cangjie
public var width: Length = 0.vp
```

**Function:** Sets the width of the popup.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read-Write Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(() -> Unit, Placement, Color, Color, Bool, Bool, Option\<(PopupStateChangeParam) -> Unit>, Bool, Color, Length, ?Color, Length, Position, Length, ?ArrowPointPosition, Length, Length, Length, ShadowStyle, BlurStyle, Bool, Option\<TransitionEffect>, Option\<(DismissPopupAction) -> Unit>, Bool)

```cangjie
public init(
    builder!: () -> Unit,
    placement!: Placement = Placement.Bottom,
    maskColor!: Color = Color(0x1000000),
    popupColor!: Color = Color(0x1000000),
    enableArrow!: Bool = true,
    autoCancel!: Bool = true,
    onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
    showInSubWindow!: Bool=false, // 5.1 start
    backgroundColor!: Color = Color(0x1000000),
    arrowOffset!: Length = 0.vp,
    mask!: ?Color = None,
    targetSpace!: Length = 0.vp,
    offset!: Position = Position(x: 0.0, y: 0.0),
    width!: Length = 0.vp,
    arrowPointPosition!: ?ArrowPointPosition = None,
    arrowWidth!: Length = 16.vp,
    arrowHeight!: Length = 16.vp,
    radius!: Length = 20.vp,
    shadow!: ShadowStyle = ShadowStyle.OuterDefaultMD,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    focusable!: Bool = false,
    transition!: Option<TransitionEffect> = Option.None,
    onWillDismiss!: Option<(Dismiss## func dismiss()

```cangjie
public func dismiss(): Unit
```

**Function:** Interactive popup dismissal interception switch and result type. Developers should call this when needing to exit, otherwise no call is required.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### class PopupMessageOptions

```cangjie
public class PopupMessageOptions {
    public var textColor: ResourceColor
    public var font: Font
    public init(textColor!: ResourceColor = Color(0x000000), font!: Font = Font())
}
```

**Function:** Popup message text parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var font

```cangjie
public var font: Font
```

**Function:** Sets font attributes for popup messages. Does not support setting family.

**Type:** [Font](cj-common-types.md#class-font)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var textColor

```cangjie
public var textColor: ResourceColor
```

**Function:** Sets text color for popup messages.

**Type:** [ResourceColor](cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(ResourceColor, Font)

```cangjie
public init(textColor!: ResourceColor = Color(0x000000), font!: Font = Font())
```

**Function:** Creates a PopupMessageOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| textColor | [ResourceColor](cj-common-types.md#interface-resourcecolor) | No | Color(0x000000) | Text color for popup messages. |
| font | [Font](cj-common-types.md#class-font) | No | Font() | Font attributes for popup messages. |

### class PopupOptions

```cangjie
public class PopupOptions {
    public var message: String = ""
    public var primaryButton: PopupButton = PopupButton(value: "", action: { => })
    public var secondaryButton: PopupButton = PopupButton(value: "", action: { => })
    public var onStateChange:?(PopupStateChangeParam) -> Unit = Option.None
    public var messageOptions: PopupMessageOptions = PopupMessageOptions()
    public var arrowOffset: Length = 0.vp
    public var showInSubWindow: Bool = false
    public var mask: ResourceColor = Color(0x1000000)
    public var targetSpace: Length = 0.vp
    public var placement: Placement = Placement.BottomLeft
    public var offset: Position = Position(x: 0.0, y: 0.0)
    public var enableArrow: Bool = true
    public var popupColor: ResourceColor = Color(0x1000000)
    public var autoCancel: Bool = true
    public var width: Length = 0.vp
    public var arrowPointPosition: Option<ArrowPointPosition>= None
    public var arrowWidth: Length = 16.0.vp
    public var arrowHeight: Length = 8.0.vp
    public var radius: Length = 20.0.vp
    public var shadow: ShadowStyle = ShadowStyle.OuterDefaultMD
    public var backgroundBlurStyle: BlurStyle = BlurStyle.ComponentUltraThick
    public var transition:?TransitionEffect = Option.None
    public var onWillDismiss:?(DismissPopupAction) -> Unit = None
    public var followTransformOfTarget: Bool = false
    public init(
        message!: String,
        primaryButton!: PopupButton = PopupButton(value: "", action: {=>}),
        secondaryButton!: PopupButton = PopupButton(value: "", action: {=>}),
        onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
        arrowOffset!: Length = 0.vp,
        showInSubWindow!: Bool,
        messageOptions!: PopupMessageOptions = PopupMessageOptions(),
        mask!: Color = Color(0x1000000),
        targetSpace!: Length = 0.vp,
        placement!: Placement = Placement.BottomLeft,
        offset!: Position = Position(x:0.0, y: 0.0),
        enableArrow!: Bool = true,
        popupColor!: Color = Color(0x1000000),
        autoCancel!: Bool = true,
        width!: Length = 0.vp,
        arrowPointPosition!: ?ArrowPointPosition = None,
        arrowWidth!: Length = 16.vp,
        arrowHeight!: Length = 8.vp,
        radius!: Length = 20.vp,
        shadow!: ShadowStyle = ShadowStyle.OuterDefaultMD,
        backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
        transition!: ?TransitionEffect = Option.None,
        onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None,
        followTransformOfTarget!: Bool = false
    )
}
```

**Function:** Parameters for popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowHeight

```cangjie
public var arrowHeight: Length = 8.0.vp
```

**Function:** Sets arrow height. Default: 8.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowOffset

```cangjie
public var arrowOffset: Length = 0.vp
```

**Function:** Sets popup arrow offset on the popup. When arrow is above/below bubble, 0 means arrow is leftmost, offset is distance from arrow to leftmost, default centered. When arrow is left/right of bubble, offset is distance from arrow to topmost, default centered. If displayed at screen edge, bubble auto-adjusts horizontally; at 0 arrow always points to bound component.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowPointPosition

```cangjie
public var arrowPointPosition: Option<ArrowPointPosition>= None
```

**Function:** Sets bubble arrow position relative to parent component. Arrow has "Start", "Center", "End" options vertically/horizontally. All positions are within parent component bounds.

**Type:** [ArrowPointPosition](cj-common-types.md#enum-arrowpointposition)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var arrowWidth

```cangjie
public var arrowWidth: Length = 16.0.vp
```

**Function:** Sets arrow width. If set width exceeds edge length minus twice bubble corner radius, arrow isn't drawn. Default: 16.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var autoCancel

```cangjie
public var autoCancel: Bool = true
```

**Function:** Sets whether bubble auto-closes on page interaction. Default: true.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: BlurStyle = BlurStyle.ComponentUltraThick
```

**Function:** Sets bubble blur background parameters. Default: BlurStyle.COMPONENT_ULTRA_THICK.

**Type:** [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var enableArrow

```cangjie
public var enableArrow: Bool = true
```

**Function:** Sets whether to show arrow. Default: true. When insufficient space prevents full bubble avoidance, bubble covers component without arrow.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var followTransformOfTarget

```cangjie
public var followTransformOfTarget: Bool = false
```

**Function:** When host component or its parent has rotation/scale transforms, sets whether bubble displays at transformed position. Default: false.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var mask

```cangjie
public var mask: ResourceColor = Color(0x1000000)
```

**Function:** Sets mask layer color.

**Type:** [ResourceColor](cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var message

```cangjie
public var message: String = ""
```

**Function:** Sets popup message content.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var messageOptions

```cangjie
public var messageOptions: PopupMessageOptions = PopupMessageOptions()
```

**Function:** Sets popup message text parameters.

**Type:** [PopupMessageOptions](#class-popupmessageoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offset

```cangjie
public var offset: Position = Position(x: 0.0, y: 0.0)
```

**Function:** Sets popup component offset relative to placement position. Percentage values not supported.

**Type:** [Position](cj-common-types.md#class-position)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var onStateChange

```cangjie
public var onStateChange:?(PopupStateChangeParam) -> Unit = Option.None
```

**Function:** Sets popup state change event callback, parameter is current display state.

**Type:** ?([PopupStateChangeParam](./cj-common-types.md#class-popupstatechangeparam))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var onWillDismiss

```cangjie
public var onWillDismiss:?(DismissPopupAction) -> Unit = None
```

**Function:** Sets interception of exit event and executes callback function.

> **Note:**
>
> Cannot perform onWillDismiss interception within onWillDismiss callback.

**Type:** ?([DismissPopupAction](#class-dismisspopupaction))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var placement

```cangjie
public var placement: Placement = Placement.BottomLeft
```

**Function:** Sets popup component display position relative to target. Default: Placement.Bottom. If both placementOnTop and placement are set, placement takes effect.

**Type:** [Placement](cj-common-types.md#enum-placement)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var popupColor

```cangjie
public var popupColor: ResourceColor = Color(0x1000000)
```

**Function:** Sets bubble color. To remove blur background effect, set backgroundBlurStyle to BlurStyle.NONE.

**Type:** [ResourceColor](cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21#### var primaryButton

```cangjie
public var primaryButton: PopupButton = PopupButton(value: "", action: { => })
```

**Function:** Sets the primary button.  
- `value`: The text displayed on the primary button in the popup.  
- `action`: The callback function triggered when the primary button is clicked.

**Type:** [PopupButton](./cj-common-types.md#class-popupbutton)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var radius

```cangjie
public var radius: Length = 20.0.vp
```

**Function:** Sets the corner radius of the bubble. Default value: 20.vp.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var secondaryButton

```cangjie
public var secondaryButton: PopupButton = PopupButton(value: "", action: { => })
```

**Function:** Sets the secondary button.  
- `value`: The text displayed on the secondary button in the popup.  
- `action`: The callback function triggered when the secondary button is clicked.

**Type:** [PopupButton](./cj-common-types.md#class-popupbutton)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var shadow

```cangjie
public var shadow: ShadowStyle = ShadowStyle.OuterDefaultMD
```

**Function:** Sets the shadow effect of the bubble. Default value: ShadowStyle.OUTER_DEFAULT_MD.

**Type:** [ShadowStyle](cj-common-types.md#enum-shadowstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var showInSubWindow

```cangjie
public var showInSubWindow: Bool = false
```

**Function:** Sets whether to display the bubble in a subwindow. Default value: false.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var targetSpace

```cangjie
public var targetSpace: Length = 0.vp
```

**Function:** Sets the gap between the popup and its target.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var transition

```cangjie
public var transition:?TransitionEffect = Option.None
```

**Function:** Customizes the animation effects for popup display and exit.

> **Note:**
> - If not set, the default display/exit animations will be used.
> - Pressing the back key during the display animation will interrupt it and trigger the exit animation, resulting in a combined effect of both animations.
> - Pressing the back key during the exit animation will not interrupt it; the exit animation will continue, and the back key event will not be processed.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var width

```cangjie
public var width: Length = 0.vp
```

**Function:** Sets the width of the popup.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(String, PopupButton, PopupButton, Option\<(PopupStateChangeParam) -> Unit>, Length, Bool, PopupMessageOptions, Color, Length, Placement, Position, Bool, Color, Bool, Length, ?ArrowPointPosition, Length, Length, Length, ShadowStyle, BlurStyle, ?TransitionEffect, Option\<(DismissPopupAction) -> Unit>, Bool)

```cangjie
public init(
    message!: String,
    primaryButton!: PopupButton = PopupButton(value: "", action: {=>}),
    secondaryButton!: PopupButton = PopupButton(value: "", action: {=>}),
    onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
    arrowOffset!: Length = 0.vp,
    showInSubWindow!: Bool,
    messageOptions!: PopupMessageOptions = PopupMessageOptions(),
    mask!: Color = Color(0x1000000),
    targetSpace!: Length = 0.vp,
    placement!: Placement = Placement.BottomLeft,
    offset!: Position = Position(x:0.0, y: 0.0),
    enableArrow!: Bool = true,
    popupColor!: Color = Color(0x1000000),
    autoCancel!: Bool = true,
    width!: Length = 0.vp,
    arrowPointPosition!: ?ArrowPointPosition = None,
    arrowWidth!: Length = 16.vp,
    arrowHeight!: Length = 8.vp,
    radius!: Length = 20.vp,
    shadow!: ShadowStyle = ShadowStyle.OuterDefaultMD,
    backgroundBlurStyle!: BlurStyle = BlurStyle.ComponentUltraThick,
    transition!: ?TransitionEffect = Option.None,
    onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None,
    followTransformOfTarget!: Bool = false
)
```

**Function:** Parameters for the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| message | String | Yes | - | Sets the content of the popup message |
| primaryButton | [PopupButton](./cj-common-types.md#class-popupbutton) | No | PopupButton(value: "", action: { => }) | Sets the primary button |
| secondaryButton | [PopupButton](./cj-common-types.md#class-popupbutton) | No | PopupButton(value: "", action: { => }) | Sets the secondary button |
| onStateChange | Option<(PopupStateChangeParam) -> Unit> | No | Option.None | Sets the callback for popup state changes |
| arrowOffset | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Sets the offset of the popup arrow relative to the popup |
| showInSubWindow | Bool | Yes | - | Sets whether to display the bubble in a subwindow |
| messageOptions | [PopupMessageOptions](#class-popupmessageoptions) | No | PopupMessageOptions() | Sets the text parameters for the popup message |
| mask | [Color](../BasicServicesKit/cj-apis-base.md#class-color) | No | Color(0x1000000) | Sets the color of the mask layer |
| targetSpace | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Sets the gap between the popup and its target |
| placement | [Placement](cj-common-types.md#enum-placement) | No | Placement.BottomLeft | Sets the display position of the popup relative to its target |
| offset | [Position](cj-common-types.md#class-position) | No | Position(x: 0.0, y: 0.0) | Sets the offset of the popup relative to the position defined by `placement` |
| enableArrow | Bool | No | true | Sets whether to display the arrow |
| popupColor | [Color](../BasicServicesKit/cj-apis-base.md#class-color) | No | Color(0x1000000) | Sets the color of the bubble |
| autoCancel | Bool | No | true | Sets whether to automatically close the bubble when an operation is performed on the page |
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Sets the width of the popup |
| arrowPointPosition | ?[ArrowPointPosition](cj-common-types.md#enum-arrowpointposition) | No | None | Sets the position of the bubble's arrow relative to its parent component |
| arrowWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | Sets the width of the arrow |
| arrowHeight | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 8.vp | Sets the height of the arrow |
| radius | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 20.vp | Sets the corner radius of the bubble |
| shadow | [ShadowStyle](cj-common-types.md#enum-shadowstyle) | No | ShadowStyle.OuterDefaultMD | Sets the shadow effect of the bubble |
| backgroundBlurStyle | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | No | BlurStyle.ComponentUltraThick | Sets the blur effect parameters for the bubble background |
| transition | ?[TransitionEffect](cj-animation-transition.md#class-transitioneffect) | No | Option.None | Customizes the animation effects for popup display and exit |
| onWillDismiss | Option<(DismissPopupAction) -> Unit> | No | None | Sets the callback function to intercept the exit event |
| followTransformOfTarget | Bool | No | false | Sets whether the bubble can be displayed at the transformed position when the target component or its parent container has transformations like rotation or scaling |