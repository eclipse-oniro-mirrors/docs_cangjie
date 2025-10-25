# Swiper

A sliding view container that provides the ability to display child components in a carousel through swiping.

> **Note:**
>
> The Swiper component includes [PanGesture](./cj-universal-gesture-pangesture.md) drag events for carousel sliding of child components. Setting the [disableSwipe](#func-disableswipebool) property to true will cancel the internal PanGesture event listeners.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain child components.

> **Notes:**
>
> - Child component types: System components and custom components, supporting rendering control types ([if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), and [LazyForEach](cj-state-rendering-lazyforeach.md)). It is not recommended to mix lazy-load components (including LazyForEach) with non-lazy-load components in child components, or to use multiple lazy-load components in child components, as this may cause issues such as the preloading capability of lazy-load components to fail. Avoid performing data source operations during component animations, as this may lead to layout abnormalities.
> - When the [visibility](./cj-universal-attribute-visibility.md) property of a Swiper child component is set to Visibility.None and the Swiper's displayCount property is set to 'auto', the corresponding child component does not occupy space within the viewport but still affects the number of navigation dots. When the visibility property is set to Visibility.None or Visibility.Hidden, the corresponding child component is not displayed but still occupies space within the viewport.
> - When a Swiper child component has the [offset](./cj-universal-attribute-location.md#func-offsetlength-length) property set, the components are drawn according to their hierarchy, with higher-level components overlapping lower-level ones. For example, if a Swiper contains three child components and the third one has offset({ x : 100 }) set, during horizontal cyclic sliding, the third component will overlap the first. In this case, you can set the [zIndex](./cj-universal-attribute-location.md#func-zindexint32) property of the first child component to a value higher than the third to ensure it overlaps the third component.

## Creating the Component

### init(?SwiperController, () -> Unit)

```cangjie
public init(controller!: ?SwiperController = Option.None, child!: () -> Unit)
```

**Function:** Creates a Swiper object containing a Swiper controller and child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| controller | ?[SwiperController](#class-swipercontroller) | No | Option.None | Binds a controller to the component for controlling page flipping. |
| child | ()->Unit | Yes | - | Child components of the Swiper container. |

## Common Attributes/Events

Common Attributes: All supported.

> **Note:**
>
> The initial value of the [clip](./cj-universal-attribute-shapclip.md#func-clip) common attribute for the Swiper component is true.

Common Events: All supported.

## Component Attributes

### func autoPlay(Bool)

```cangjie
public func autoPlay(value: Bool): This
```

**Function:** Sets whether child components automatically play. When [loop](#func-loopbool) is false, auto-play stops at the last page. Play resumes if the current page is not the last after a gesture switch. Auto-play stops when the Swiper is not visible.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether child components automatically play.<br>Initial value: false (no auto-play). |

### func cachedCount(Int32)

```cangjie
public func cachedCount(value: Int32): This
```

**Function:** Sets the number of preloaded child components, loading components before and after the currently displayed page. For example, when cachedCount=1, the components before and after the current page are preloaded. If swipeByGroup is set to true in displayCount, preloading is done by group. For example, when cachedCount=1 and swipeByGroup=true, the groups before and after the current group are preloaded.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Number of preloaded child components.<br>Initial value: 1.<br>Range: [0, +∞). Values less than 0 are treated as the initial value. |

### func curve(Curve)

```cangjie
public func curve(value: Curve): This
```

**Function:** Sets the animation curve for Swiper, defaulting to a spring interpolation curve. Common curves are described in [Curve Enumeration](./cj-common-types.md#enum-curve).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Curve](./cj-common-types.md#enum-curve) | Yes | - | Animation curve for Swiper. |

### func disableSwipe(Bool)

```cangjie
public func disableSwipe(value: Bool): This
```

**Function:** Disables the swipe-to-switch functionality of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to disable swipe-to-switch. true disables, false enables.<br>Initial value: false. |

### func displayCount(Int32, Bool)

```cangjie
public func displayCount(value: Int32, swipeByGroup!: Bool = false): This
```

**Function:** Sets the number of elements displayed within the Swiper viewport.

When using Int32, child components are stretched (or shrunk) along the main axis by equally dividing the Swiper width (minus displayCount-1 itemSpace). Values less than or equal to 0 default to the initial value of 1.

When flipping by group, the drag distance threshold for flipping is adjusted to 50% of the Swiper width (compared to 50% of the child element width when flipping by element). If the last group has fewer child elements than displayCount, placeholder elements are used for layout positioning. Placeholder elements do not display any content and show the Swiper's background style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Number of child elements displayed in the viewport. Values less than or equal to 0 default to the initial value.<br>Initial value: 1.<br>Range: (0, +∞). Values less than or equal to 0 default to the initial value. |
| swipeByGroup | Bool | No | false | Whether to flip by group. If true, flipping is done by group, with each group containing displayCount value elements. If false, flipping is done by element (default behavior).<br>Initial value: false. |

### func displayMode(SwiperDisplayMode)

```cangjie
public func displayMode(value: SwiperDisplayMode): This
```

**Function:** Sets the arrangement mode of elements along the main axis. This takes effect only if displayCount is not set.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [SwiperDisplayMode](#enum-swiperdisplaymode) | Yes | - | Arrangement mode of elements along the main axis.<br>Initial value: SwiperDisplayMode.STRETCH. |

### func duration(UInt32)

```cangjie
public func duration(value: UInt32): This
```

**Function:** Sets the animation duration for child component switching.

duration must be used with [curve](#func-curvecurve).

The default curve is [interpolatingSpring](./cj-apis-curves.md#func-interpolatingspring), where the animation duration is only affected by the curve's parameters and not by duration. Curves not controlled by duration can be found in the [Interpolation Calculation](./cj-apis-curves.md) module, such as [springMotion](./cj-apis-curves.md#func-springmotion), [responsiveSpringMotion](./cj-apis-curves.md#func-responsivespringmotion), and interpolatingSpring curves. To have the animation duration controlled by duration, set other curves for curve.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | UInt32 | Yes | - | Animation duration for child component switching, in milliseconds. Values less than 0 default to the initial value.<br>Initial value: 400.<br>Range: [0, +∞). Values less than 0 default to the initial value. |

### func effectMode(EdgeEffect)

```cangjie
public func effectMode(value: EdgeEffect): This
```

**Function:** Sets the edge swipe effect, effective when [loop](#func-loopbool) = false. The bounce effect is not triggered when using SwiperController.changeIndex(), SwiperController.showNext(), or SwiperController.showPrevious() to navigate to the first or last page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [EdgeEffect](./cj-common-types.md#enum-edgeeffect) | Yes | - | Edge swipe effect.<br>Initial value: EdgeEffect.Spring. |

### func index(UInt32)

```cangjie
public func index(value: UInt32): This
```

**Function:** Sets the index of the currently displayed child component in the container. Values greater than or equal to the number of child components default to the initial value of 0.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | UInt32 | Yes | - | Index of the currently displayed child component.<br> **Note:**<br>Values less than 0 or greater than the maximum page index default to 0.<br>Initial value: 0. |

### func indicator(Bool)

```cangjie
public func indicator(indicator: Bool): This
```

**Function:** Sets the optional navigation dot indicator style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| indicator | Bool | Yes | - | Optional navigation dot indicator style.<br/>\- boolean: Whether to enable the navigation dot indicator. true enables, false disables.<br/>Initial value: true. |

### func indicator(DotIndicator)

```cangjie
public func indicator(indicator: DotIndicator): This
```

**Function:** Sets the externally bound navigation dot component controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| indicator | [DotIndicator](#class-dotindicator) | Yes | - | Optional navigation dot indicator style.<br/>\- DotIndicator: Dot indicator style. |

### func indicator(DigitIndicator)

```cangjie
public func indicator(indicator: DigitIndicator): This
```

**Function:** Sets the externally bound navigation dot component controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| indicator | [DigitIndicator](#class-digitindicator) | Yes | - | Optional navigation dot indicator style.<br/>\- DigitIndicator: Digit indicator style. |

### func interval(UInt32)

```cangjie
public func interval(value: UInt32): This
```

**Function:** Sets the time interval for auto-play.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | UInt32 | Yes | - | Time interval for auto-play. If less than [duration](#func-durationuint32), the next carousel starts immediately after the current page flip completes.<br>Initial value: 3000.<br>Unit: milliseconds.<br>Values less than 0 default to the initial value. |

### func itemSpace(Length)

```cangjie
public func itemSpace(value: Length): This
```

**Function:** Sets the gap between child components. Percentage values are not supported.

For Int64 and Float64 types, the default unit is vp. For string types, pixel units must be explicitly specified (e.g., '10px'). If no unit is specified (e.g., '10'), the unit is vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Gap between child components.<br/>For Int64 and Float64 types, the default unit is vp.<br>Values less than 0 or exceeding the Swiper component width default to the initial value.<br>Initial value: 0. |

### func loop(Bool)

```cangjie
public func loop(value: Bool): This
```

**Function:** Sets whether to enable looping. true enables looping. In LazyForEach lazy-load mode, it is recommended to load more than 5 components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to enable looping. true enables, false disables.<br>Initial value: true. |

### func vertical(Bool)

```cangjie
public func vertical(value: Bool): This
```

**Function:** Sets whether to enable vertical sliding.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to enable vertical sliding. true enables, false enables horizontal sliding.<br>Initial value: false. |

## Component Events

### func onChange((Int32) -> Unit)

```cangjie
public func onChange(callback: (Int32) -> Unit): This
```

**Function:** Triggered when the index of the currently displayed child component changes, returning the index of the currently displayed child component.

When using Swiper with LazyForEach, do not trigger child page UI refreshes in the onChange event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | (Int32)->Unit | Yes | - | Callback function triggered when the index of the currently displayed child component changes.<br>Parameter: Index of the currently displayed element. |

## Basic Type Definitions

### class DigitIndicator

```cangjie
public class DigitIndicator <: Indicator {
    public init()
}
```

**Function:** Constructs the style of a digit indicator.

> **Note:**
>
> When flipping by group, the number of child nodes displayed in the digit navigation dots excludes placeholder nodes. The maximum font scaling factor [maxFontScale](./cj-common-types.md#var-maxfontscale) for digit navigation dot text is 2.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- [Indicator](#class-indicator)

#### init()

```cangjie
public init()
```

**Function:** Constructor for DigitIndicator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func digitFont(FontOptions)

```cangjie
public func digitFont(value: FontOptions): This
```

**Function:** Font style for digit navigation dots in the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [FontOptions](#class-fontoptions) | Yes | - | Sets the font style for digit navigation dots in the Swiper component. |

#### func fontColor(ResourceColor)

```cangjie
public func fontColor(value: ResourceColor): This
```

**Function:** Font color for digit navigation dots in the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.F### class DotIndicator

```cangjie
public class DotIndicator <: Indicator {
    public init()
}
```

**Function:** Constructor for DotIndicator.

> **Note:**
>
>When a navigation dot is pressed, it scales up to 1.33 times its original size. Therefore, there is a certain distance between the visible boundary of the non-pressed state and the actual boundary. This distance increases as parameters like `itemWidth`, `itemHeight`, `selectedItemWidth`, and `selectedItemHeight` grow larger.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [Indicator](#class-indicator)

#### init()

```cangjie
public init()
```

**Function:** Constructor for DigitIndicator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the color of the dot navigation indicator for the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Sets the color of the dot navigation indicator for the Swiper component.<br>Initial value: 0x182431 (10% opacity). |

#### func itemHeight(Length)

```cangjie
public func itemHeight(value: Length): This
```

**Function:** Sets the height of the dot navigation indicator for the Swiper component. Percentage values are not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the height of the dot navigation indicator for the Swiper component. Percentage values are not supported.<br>Initial value: 6.<br>Unit: vp. |

#### func itemWidth(Length)

```cangjie
public func itemWidth(value: Length): This
```

**Function:** Sets the width of the dot navigation indicator for the Swiper component. Percentage values are not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the width of the dot navigation indicator for the Swiper component. Percentage values are not supported.<br>Initial value: 6.<br>Unit: vp. |

#### func mask(Bool)

```cangjie
public func mask(value: Bool): This
```

**Function:** Determines whether to display the mask style for the dot navigation indicator of the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Sets whether to display the mask style for the dot navigation indicator of the Swiper component.<br>Initial value: false. |

#### func maxDisplayCount(UInt32)

```cangjie
public func maxDisplayCount(value: UInt32): This
```

**Function:** Sets the maximum number of navigation dots to display in the dot navigation indicator style.

This property does not take effect when the standalone navigation dot component is not bound to a Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | UInt32 | Yes | - | Sets the maximum number of navigation dots to display in the dot navigation indicator style. When the actual number of navigation dots exceeds this maximum, an overflow effect style will be applied, as shown in Example 4.<br>Initial value: This property has no initial value. Invalid values will result in no overflow effect.<br>Valid range: 6-9.<br> **Notes:**<br>1. Overflow scenarios currently do not support interactive features (e.g., touch dragging, mouse operations).<br>2. In overflow scenarios, the position of the selected navigation dot for the middle page is not completely fixed and depends on the previous page-turning sequence.<br>3. Currently, only `displayCount` = 1 is supported. |

#### func selectedColor(ResourceColor)

```cangjie
public func selectedColor(value: ResourceColor): This
```

**Function:** Sets the color of the selected dot navigation indicator for the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Sets the color of the selected dot navigation indicator for the Swiper component.<br>Initial value: 0x007DFF. |

#### func selectedItemHeight(Length)

```cangjie
public func selectedItemHeight(value: Length): This
```

**Function:** Sets the height of the selected dot navigation indicator for the Swiper component. Percentage values are not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the height of the selected dot navigation indicator for the Swiper component. Percentage values are not supported.<br>Initial value: 6.<br>Unit: vp. |

#### func selectedItemWidth(Length)

```cangjie
public func selectedItemWidth(value: Length): This
```

**Function:** Sets the width of the selected dot navigation indicator for the Swiper component. Percentage values are not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the width of the selected dot navigation indicator for the Swiper component. Percentage values are not supported.<br>Initial value: 12.<br>Unit: vp. |

### class FontOptions

```cangjie
public class FontOptions {
    public var size: Length
    public var weight: FontWeight
    public init(size!: Length = 14.vp, weight!: FontWeight = FontWeight.Normal)
}
```

**Function:** Defines the font style for the numeric navigation dots in the Swiper component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var size

```cangjie
public var size: Length
```

**Function:** Sets the font size for the numeric navigation dot indicator. Percentage values are not supported.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var weight

```cangjie
public var weight: FontWeight
```

**Function:** Sets the font weight for the selected numeric navigation dot indicator.

**Type:** [FontWeight](./cj-common-types.md#enum-fontweight)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Length, FontWeight)

```cangjie
public init(size!: Length = 14.vp, weight!: FontWeight = FontWeight.Normal)
```

**Function:** Constructor for FontOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 14.vp | **Named parameter.** Sets the font size for the numeric navigation dot indicator. Percentage values are not supported. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Sets the font weight for the selected numeric navigation dot indicator. |

### class Indicator

```cangjie
public open class Indicator {}
```

**Function:** Sets the distance between the navigation dots and the Swiper component. Due to the default interactive area of the navigation dots (32 vp in height), the visible part cannot be completely flush with the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### static func digit()

```cangjie
public static func digit(): DigitIndicator
```

**Function:** Returns a DigitIndicator object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [DigitIndicator](#class-digitindicator) | A numeric indicator. |

#### static func dot()

```cangjie
public static func dot(): DotIndicator
```

**Function:** Returns a DotIndicator object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [DotIndicator](#class-dotindicator) | A dot indicator. |

#### func bottom(Length)

```cangjie
public func bottom(value: Length): This
```

**Function:** Sets the position of the navigation dots relative to the bottom of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the position of the navigation dots relative to the bottom of the Swiper.<br>If neither `top` nor `bottom` is set, adaptive layout is applied, placing the indicator at the bottom in the cross-axis direction (same effect as `bottom=0`).<br>When set to 0: Layout is calculated based on the 0 position.<br>Priority: Lower than the `top` property.<br>Valid range: [0, Swiper height - navigation dot area height]. Values outside this range are clamped to the nearest boundary. |

#### func end(Length)

```cangjie
public func end(value: Length): This
```

**Function:** In RTL mode, sets the distance between the navigation dots and the left side of the Swiper. In LTR mode, sets the distance between the navigation dots and the right side of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | In RTL mode, sets the distance between the navigation dots and the left side of the Swiper. In LTR mode, sets the distance between the navigation dots and the right side of the Swiper.<br>Initial value: 0.<br>Unit: vp. |

#### func left(Length)

```cangjie
public func left(value: Length): This
```

**Function:** Sets the position of the navigation dots relative to the left side of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the position of the navigation dots relative to the left side of the Swiper.<br>If neither `left` nor `right` is set, adaptive layout is applied, centering the indicator along the main axis.<br>When set to 0: Layout is calculated based on the 0 position.<br>Priority: Higher than the `right` property.<br>Valid range: [0, Swiper width - navigation dot area width]. Values outside this range are clamped to the nearest boundary. |

#### func right(Length)

```cangjie
public func right(value: Length): This
```

**Function:** Sets the position of the navigation dots relative to the right side of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the position of the navigation dots relative to the right side of the Swiper.<br>If neither `left` nor `right` is set, adaptive layout is applied, centering the indicator along the main axis.<br>When set to 0: Layout is calculated based on the 0 position.<br>Priority: Lower than the `left` property.<br>Valid range: [0, Swiper width - navigation dot area width]. Values outside this range are clamped to the nearest boundary. |

#### func start(Length)

```cangjie
public func start(value: Length): This
```

**Function:** In RTL mode, sets the distance between the navigation dots and the right side of the Swiper. In LTR mode, sets the distance between the navigation dots and the left side of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | In RTL mode, sets the distance between the navigation dots and the right side of the Swiper. In LTR mode, sets the distance between the navigation dots and the left side of the Swiper.<br>Initial value: 0.<br>Unit: vp. |

#### func top(Length)

```cangjie
public func top(value: Length): This
```

**Function:** Sets the position of the navigation dots relative to the top of the Swiper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the position of the navigation dots relative to the top of the Swiper.<br>If neither `top` nor `bottom` is set, adaptive layout is applied, placing the indicator at the bottom in the cross-axis direction (same effect as `bottom=0`).<br>When set to 0: Layout is calculated based on the 0 position.<br>Priority: Higher than the `bottom` property.<br>Valid range: [0, Swiper height - navigation dot area height]. Values outside this range are clamped to the nearest boundary. |

### class SwiperController

```cangjie
public class SwiperController {
    public init()
}
```

**Function:** SwiperController is the controller for the Swiper container component. An object of this type can be defined and bound to a Swiper component to control page-turning for child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init()

```cangjie
public init()
```

**Function:** Constructor for SwiperController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func finishAnimation()

```cangjie
public func finishAnimation(): Unit
```

**Function:** Stops the animation playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func finishAnimation(VoidCallback)

```cangjie
public func finishAnimation(callback: VoidCallback): Unit
```

**Function:** Stops the animation playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | VoidCallback | Yes | - | Callback function triggered when the animation ends. |

#### func showNext()

```cangjie
public func showNext(): Unit
```

**Function:** Turns to the next page. The page-turning animation duration is set via the Swiper's [duration](#func-durationuint32) property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func showPrevious()

```cangjie
public func showPrevious(): Unit
```

**Function:** Turns to the previous page. The page-turning animation duration is set via the Swiper's [duration](#func-durationuint32) property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## enum SwiperDisplayMode

```cangjie
public enum SwiperDisplayMode <: Equatable<SwiperDisplayMode> {
    | Stretch
    | AutoLinear
    | ...
}
```

**Description:** Enumeration defining the size mode of Swiper along the main axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<SwiperDisplayMode>

### AutoLinear

```cangjie
AutoLinear
```

**Description:** The width of one swipe page equals the width of the leftmost child component within the viewport. Deprecated, recommended to use [Scroller.scrollto](./cj-scroll-swipe-scroll.md#func-scrolltoindexint32-bool-scrollalign-length) instead.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Stretch

```cangjie
Stretch
```

**Description:** The width of one swipe page equals the width of the Swiper component itself.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(SwiperDisplayMode)

```cangjie
public operator func !=(other: SwiperDisplayMode): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwiperDisplayMode](#enum-swiperdisplaymode) | Yes | - | Enum value to compare |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if unequal, otherwise false. |

### func ==(SwiperDisplayMode)

```cangjie
public operator func ==(other: SwiperDisplayMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwiperDisplayMode](#enum-swiperdisplaymode) | Yes | - | Enum value to compare |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal, otherwise false. |

## Sample Code

### Sample 1 (Setting Navigation Dot Interaction & Page Transition Effects)

This sample implements page transition to a specified page in Swiper component by configuring SwiperAnimationMode via the changeIndex interface.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource<T> <: IDataSource<T> {
    private var list: ArrayList<T> = ArrayList<T>([])

    MyDataSource(list: ArrayList<T>) {
        this.list = list
    }

    public func totalCount(): Int64 {
        return this.list.size
    }

    public func getData(index: Int64): T {
        return this.list[index]
    }

    public func onRegisterDataChangeListener(listener: DataChangeListener): Unit {
    }

    public func onUnregisterDataChangeListener(listener: DataChangeListener): Unit {
    }
}

@Entry
@Component
class EntryView {
    private var swiperController: SwiperController = SwiperController()
    private var data: MyDataSource<Int64> = MyDataSource<Int64>(ArrayList<Int64>([]))

    protected override func aboutToAppear() {
        var list: ArrayList<Int64> = ArrayList<Int64>([])
        for (i in 0..10) {
            list.add(i)
        }
        this.data = MyDataSource<Int64>(list)
    }

    func build() {
        Column(space: 5) {
            Swiper(controller: this.swiperController) {
                LazyForEach(
                    this.data,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => Text(item.toString())
                            .width(90.percent)
                            .height(160)
                            .backgroundColor(0xAFEEEE)
                            .textAlign(TextAlign.Center)
                            .fontSize(30)
                    }
                )
            }
                .cachedCount(2)
                .index(1)
                .autoPlay(true)
                .interval(4000)
                .loop(true)
                .duration(1000)
                .itemSpace(0)
                .indicator( // Configure dot navigation style
                    DotIndicator()
                        .itemWidth(15)
                        .itemHeight(15)
                        .selectedItemWidth(15)
                        .selectedItemHeight(15)
                        .color(Color.Gray)
                        .selectedColor(Color.Blue))
                .curve(Curve.Linear)

            Row(space: 12) {
                Button("showNext").onClick({
                    _ => this
                        .swiperController
                        .showNext()
                })

                Button("showPrevious").onClick({
                    _ => this
                        .swiperController
                        .showPrevious()
                })
            }.margin(5)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![swiper1](./figures/swiper1.gif)

### Sample 2 (Setting Digital Indicator)

This sample implements digital indicator functionality via the DigitIndicator interface.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource<T> <: IDataSource<T> {
    private var list: ArrayList<T> = ArrayList<T>([])

    MyDataSource(list: ArrayList<T>) {
        this.list = list
    }

    public func totalCount(): Int64 {
        return this
            .list
            .size
    }

    public func getData(index: Int64): T {
        return this.list[index]
    }

    public func onRegisterDataChangeListener(listener: DataChangeListener): Unit {
    }

    public func onUnregisterDataChangeListener(listener: DataChangeListener): Unit {
    }
}

@Entry
@Component
class EntryView {
    private var swiperController: SwiperController = SwiperController()
    private var data: MyDataSource<Int64> = MyDataSource<Int64>(ArrayList<Int64>([]))

    protected override func aboutToAppear() {
        var list: ArrayList<Int64> = ArrayList<Int64>([])
        for (i in 1..=10) {
            list.add(i)
        }
        this.data = MyDataSource<Int64>(list)
    }

    func build() {
        Column(space: 5) {
            Swiper(controller: this.swiperController) {
                LazyForEach(
                    this.data,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => Text(item.toString())
                            .width(90.percent)
                            .height(160)
                            .backgroundColor(0xAFEEEE)
                            .textAlign(TextAlign.Center)
                            .fontSize(30)
                    }
                )
            }
                .cachedCount(2)
                .index(1)
                .autoPlay(true)
                .interval(4000)
                .indicator( // Configure digital navigation style
                    Indicator
                        .digit()
                        .top(200)
                        .fontColor(Color.Gray)
                        .selectedFontColor(Color.Gray)
                        .digitFont(FontOptions(size: 20, weight: FontWeight.Bold)))
                .loop(true)
                .duration(1000)
                .itemSpace(0)

            Row(space: 12) {
                Button("showNext").onClick({
                    _ => this
                        .swiperController
                        .showNext()
                })

                Button("showPrevious").onClick({
                    _ => this
                        .swiperController
                        .showPrevious()
                })
            }.margin(5)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![swiper2](./figures/swiper2.gif)

### Sample 3 (Setting Group-based Paging)

This sample implements group-based paging via the displayCount property.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource<T> <: IDataSource<T> {
    private var list: ArrayList<T> = ArrayList<T>([])

    MyDataSource(list: ArrayList<T>) {
        this.list = list
    }

    public func totalCount(): Int64 {
        return this
            .list
            .size
    }

    public func getData(index: Int64): T {
        return this.list[index]
    }

    public func onRegisterDataChangeListener(listener: DataChangeListener): Unit {
    }

    public func onUnregisterDataChangeListener(listener: DataChangeListener): Unit {
    }
}

@Entry
@Component
class EntryView {
    private var swiperController: SwiperController = SwiperController()
    private var data: MyDataSource<Int64> = MyDataSource<Int64>(ArrayList<Int64>([]))

    protected override func aboutToAppear() {
        var list: ArrayList<Int64> = ArrayList<Int64>([])
        for (i in 1..=10) {
            list.add(i)
        }
        this.data = MyDataSource<Int64>(list)
    }

    func build() {
        Column(space: 5) {
            Swiper(controller: this.swiperController) {
                LazyForEach(
                    this.data,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => Text(item.toString())
                            .width(90.percent)
                            .height(160)
                            .backgroundColor(0xAFEEEE)
                            .textAlign(TextAlign.Center)
                            .fontSize(30)
                    }
                )
            }
                .displayCount(3, swipeByGroup: true)
                .autoPlay(true)
                .interval(4000)
                .indicator( // Configure dot navigation style
                    DotIndicator()
                        .itemWidth(15)
                        .itemHeight(15)
                        .selectedItemWidth(15)
                        .selectedItemHeight(15)
                        .color(Color.Gray)
                        .selectedColor(Color.Blue))
                .loop(true)
                .duration(1000)

            Row(space: 12) {
                Button("showNext").onClick({
                    _ => this
                        .swiperController
                        .showNext()
                })

                Button("showPrevious").onClick({
                    _ => this
                        .swiperController
                        .showPrevious()
                })
            }.margin(5)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![swiper3](./figures/swiper3.gif)

### Sample 4 (Setting Oversized Dot Navigation)

This sample implements animated oversized dot navigation via the maxDisplayCount property of DotIndicator interface.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

class MyDataSource<T> <: IDataSource<T> {
    private var list: ArrayList<T> = ArrayList<T>([])

    MyDataSource(list: ArrayList<T>) {
        this.list = list
    }

    public func totalCount(): Int64 {
        return this
            .list
            .size
    }

    public func getData(index: Int64): T {
        return this.list[index]
    }

    public func onRegisterDataChangeListener(listener: DataChangeListener): Unit {
    }

    public func onUnregisterDataChangeListener(listener: DataChangeListener): Unit {
    }
}

@Entry
@Component
class EntryView {
    private var swiperController: SwiperController = SwiperController()
    private var data: MyDataSource<Int64> = MyDataSource<Int64>(ArrayList<Int64>([]))

    protected override func aboutToAppear() {
        var list: ArrayList<Int64> = ArrayList<Int64>([])
        for (i in 1..=10) {
            list.add(i)
        }
        this.data = MyDataSource<Int64>(list)
    }

    func build() {
        Column(space: 5) {
            Swiper(controller: this.swiperController) {
                LazyForEach(
                    this.data,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => Text(item.toString())
                            .width(90.percent)
                            .height(160)
                            .backgroundColor(0xAFEEEE)
                            .textAlign(TextAlign.Center)
                            .fontSize(30)
                    }
                )
            }
                .cachedCount(2)
                .index(5)
                .autoPlay(true)
                .interval(4000)
                .loop(true)
                .duration(1000)
                .itemSpace(0)
                .indicator(
                    DotIndicator()
                        .itemWidth(8)
                        .itemHeight(8)
                        .selectedItemWidth(16)
                        .selectedItemHeight(8)
                        .color(Color.Gray)
                        .selectedColor(Color.Blue)
                        .maxDisplayCount(9))
                .curve(Curve.Linear)

            Row(space: 12) {
                Button("showNext").onClick({
                    _ => this
                        .swiperController
                        .showNext()
                })

                Button("showPrevious").onClick({
                    _ => this
                        .swiperController
                        .showPrevious()
                })
            }.margin(5)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![swiper5](./figures/swiper5.gif)
```