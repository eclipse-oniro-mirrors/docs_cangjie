# Scroll

A scrollable container component that allows content to scroll when the layout dimensions of child components exceed those of the parent component.

> **Note:**
>
> - When this component nests a List child component for scrolling, if the List does not have width and height set, it will load all content by default. For performance-sensitive scenarios, it is recommended to specify the List's width and height.
> - Scrolling occurs only when the main axis size is smaller than the content size.
> - The default value of the Scroll component's [universal attribute clip](./cj-universal-attribute-shapclip.md#func-clipbool) is true.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Content can scroll when the layout dimensions of child components exceed those of the parent component.

> **Note:**
>
> - When this component nests a List child component for scrolling, if the List does not have width and height set, it will load all content by default. For performance-sensitive scenarios, it is recommended to specify the List's width and height.
> - Scrolling occurs only when the main axis size is smaller than the content size.
> - The default value of the Scroll component's [universal attribute clip](./cj-universal-attribute-shapclip.md#func-clipbool) is true.

## Creating Components

### init()

```cangjie
public init()
```

**Function:** Creates a Scroll container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a Scroll container with child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | Yes | - | Declares the child components within the container. |

### init(Scroller, () -> Unit)

```cangjie
public init(scroller: Scroller, child: () -> Unit)
```

**Function:** Creates a Scroll container with child components and binds a scrollbar controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scroller | [Scroller](#class-scroller) | Yes | - | The scrollbar controller. |
| child | () -> Unit | Yes | - | Declares the child components within the container. |

## Component Attributes

### func scrollable(ScrollDirection)

```cangjie
public func scrollable(scrollDirection: ScrollDirection): This
```

**Function:** Sets the scrolling direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scrollDirection | [ScrollDirection](./cj-common-types.md#enum-scrolldirection) | Yes | - | The scrolling direction.<br>Initial value: ScrollDirection.Vertical. |

## Component Events

### func onDidScroll(ScrollOnScrollCallback)

```cangjie
public func onDidScroll(callback: ScrollOnScrollCallback): This
```

**Function:** Scroll event callback, triggered when Scroll scrolls.

Returns the offset of the current frame's scroll and the current scroll state.

Conditions for triggering this event:

1. Triggered when the scroll component initiates scrolling, supporting keyboard/mouse operations and other input settings that trigger scrolling.

2. Triggered when called via the scroll controller API.

3. Triggered during overscroll bounce-back.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ScrollOnScrollCallback | Yes | - | Callback function triggered when Scroll scrolls.<br>Parameter 1: Horizontal offset during each frame's scroll. Positive when content scrolls left, negative when content scrolls right. Unit: vp.<br>Parameter 2: Vertical offset during each frame's scroll. Positive when content scrolls up, negative when content scrolls down. Unit: vp.<br>Parameter 3: Current scroll state. |

### func onScrollEdge(OnScrollEdgeCallback)

```cangjie
public func onScrollEdge(event: OnScrollEdgeCallback): This
```

**Function:** Triggered when scrolling reaches the edge.

Conditions for triggering this event:

1. Triggered when the scroll component reaches the edge, supporting keyboard/mouse operations and other input settings that trigger scrolling.

2. Triggered when called via the scroll controller API.

3. Triggered during overscroll bounce-back.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | OnScrollEdgeCallback | Yes | - | The edge position reached during scrolling.<br>When Scroll is set to horizontal scrolling, Edge.Center indicates the starting position in the horizontal direction, and Edge.Baseline indicates the ending position in the horizontal direction. Since the Edge.Center and Edge.Baseline enum values are deprecated, it is recommended to use the onReachStart and onReachEnd events to monitor boundary scrolling. |

### func onScrollFrameBegin(OnScrollFrameBeginCallback)

```cangjie
public func onScrollFrameBegin(event: OnScrollFrameBeginCallback): This
```

**Function:** Triggered at the start of each frame's scroll. The event parameters include the upcoming scroll amount. The event handler can calculate the actual required scroll amount based on the application scenario and return it as the handler's return value. Scroll will proceed with the returned actual scroll amount.

Negative values for offsetRemain are supported.

If nested scrolling is implemented via the onScrollFrameBegin event and the scrollBy method, the child scroll node's EdgeEffect must be set to None. For example, when Scroll nests a List for scrolling, the List component's edgeEffect attribute must be set to EdgeEffect.None.

Conditions for triggering this event:

1. Triggered when the scroll component initiates scrolling, including keyboard/mouse operations and other input settings that trigger scrolling.

2. Not triggered when called via the controller API.

3. Not triggered during overscroll bounce-back.

4. Not triggered when dragging the scrollbar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | OnScrollFrameBeginCallback | Yes | - | Callback function triggered at the start of each frame's scroll. |

### func onWillScroll((Float64,Float64,ScrollState,ScrollSource) -> OffsetResult)

```cangjie
public func onWillScroll(handler: (Float64, Float64, ScrollState, ScrollSource) -> OffsetResult): This
```

**Function:** Scroll event callback, triggered before Scroll scrolls.

The callback returns the upcoming scroll offset for the current frame, the current scroll state, and the source of the scroll operation. The returned offset is the calculated upcoming scroll value, not the final actual scroll offset. The callback's return value can specify the upcoming scroll offset for Scroll.

Conditions for triggering this event:

1. Triggered when the scroll component initiates scrolling, supporting keyboard/mouse operations and other input settings that trigger scrolling.

2. Triggered when called via the scroll controller API.

3. Triggered during overscroll bounce-back.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| handler | (Float64,Float64,[ScrollState](./cj-common-types.md#enum-scrollstate),[ScrollSource](./cj-common-types.md#enum-scrollsource))->[OffsetResult](#class-offsetresult) | Yes | - | Callback function triggered before Scroll scrolls.<br>Parameter 1: Horizontal offset for the current frame's scroll. Positive when content scrolls left, negative when content scrolls right. Unit: vp.<br>Parameter 2: Vertical offset for the current frame's scroll. Positive when content scrolls up, negative when content scrolls down. Unit: vp.<br>Parameter 3: Current scroll state.<br>Parameter 4: Source of the current scroll operation.<br>Return value: Scroll offset object. Returns OffsetResult to scroll according to the developer-specified offset. |

### func onWillScroll((Float64,Float64,ScrollState,ScrollSource) -> Unit)

```cangjie
public func onWillScroll(handler: (Float64, Float64, ScrollState, ScrollSource) -> Unit): This
```

**Function:** Scroll event callback, triggered before Scroll scrolls.

The callback returns the upcoming scroll offset for the current frame, the current scroll state, and the source of the scroll operation. The returned offset is the calculated upcoming scroll value, not the final actual scroll offset. The callback's return value can specify the upcoming scroll offset for Scroll.

Conditions for triggering this event:

1. Triggered when the scroll component initiates scrolling, supporting keyboard/mouse operations and other input settings that trigger scrolling.

2. Triggered when called via the scroll controller API.

3. Triggered during overscroll bounce-back.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| handler | (Float64,Float64,[ScrollState](./cj-common-types.md#enum-scrollstate),[ScrollSource](./cj-common-types.md#enum-scrollsource))->Unit | Yes | - | Callback function triggered before Scroll scrolls.<br>Parameter 1: Horizontal offset for the current frame's scroll. Positive when content scrolls left, negative when content scrolls right. Unit: vp.<br>Parameter 2: Vertical offset for the current frame's scroll. Positive when content scrolls up, negative when content scrolls down. Unit: vp.<br>Parameter 3: Current scroll state.<br>Parameter 4: Source of the current scroll operation. |

## Basic Type Definitions

### class FadingEdgeOptions

```cangjie
public class FadingEdgeOptions {
    public var fadingEdgeLength: Length
    public init(fadingEdgeLength!: Length = 32.vp)
}
```

**Function:** Edge fading parameter object for the fadingEdge attribute.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var fadingEdgeLength

```cangjie
public var fadingEdgeLength: Length
```

**Function:** Sets the edge fading length. If set to a value less than 0, the default value is used. The default length is 32vp.
If the set length exceeds half the container height, the fading length is set to half the container height.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Length)

```cangjie
public init(fadingEdgeLength!: Length = 32.vp)
```

**Function:** Creates a FadingEdgeOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fadingEdgeLength | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 32.vp | Sets the edge fading length. If set to a value less than 0, the default value is used. The default length is 32vp. If the set length exceeds half the container height, the fading length is set to half the container height. |

### class NestedScrollOptions

```cangjie
public class NestedScrollOptions {
    public NestedScrollOptions(
        public var scrollForward: NestedScrollMode,
        public var scrollBackward: NestedScrollMode,
        public init(scrollForward: NestedScrollMode, scrollBackward: NestedScrollMode)
    )
}
```

**Function:** Parameter object for the nestedScroll attribute.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var scrollBackward

```cangjie
public var scrollBackward: NestedScrollMode
```

**Function:** Nested scroll options when the scroll component scrolls toward the start.

**Type:** [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var scrollForward

```cangjie
public var scrollForward: NestedScrollMode
```

**Function:** Nested scroll options when the scroll component scrolls toward the end.

**Type:** [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(NestedScrollMode, NestedScrollMode)

```cangjie
public init(scrollForward: NestedScrollMode, scrollBackward: NestedScrollMode)
```

**Function:** Constructs a NestedScrollOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scrollForward | NestedScrollMode | Yes | - | Nested scroll options when the scroll component scrolls toward the end. |
| scrollBackward | NestedScrollMode | Yes | - | Nested scroll options when the scroll component scrolls toward the start. |

#### NestedScrollOptions(NestedScrollMode, NestedScrollMode)

```cangjie
public class NestedScrollOptions(
    public var scrollForward: NestedScrollMode,
    public var scrollBackward: NestedScrollMode
)
```

**Function:** Nested scroll options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scrollForward | [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | Nested scroll options when the scroll component scrolls toward the end. |
| scrollBackward | [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | Nested scroll options when the scroll component scrolls toward the start. |

### class OffsetResult

```cangjie
public class OffsetResult {
    public var xOffset: Float64
    public var yOffset: Float64
    public init(xOffset: Float64, yOffset: Float64)
}
```

**Function:** Scroll offset object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var xOffset

```cangjie
public var xOffset: Float64
```

**Function:** Horizontal scroll offset.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var yOffset

```cangjie
public var yOffset: Float64
```

**Function:** Vertical scroll offset.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Float64, Float64)

```cangjie
public init(xOffset: Float64, yOffset: Float64)
```

**Function:** Constructs an OffsetResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| xOffset | Float64 | Yes | - | Horizontal scroll offset. Unit: vp. |
| yOffset | Float64 | Yes | - | Vertical scroll offset. Unit: vp. |### class RectResult

```cangjie
public class RectResult {
    public var x: Float64
    public var y: Float64
    public var width: Float64
    public var height: Float64
    public init(
        x: Float64,
        y: Float64,
        width: Float64,
        height: Float64
    )
}
```

**Description:** Size and position of a child component relative to its parent. Unit: vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var height

```cangjie
public var height: Float64
```

**Description:** Height of the component.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var width

```cangjie
public var width: Float64
```

**Description:** Width of the component.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var x

```cangjie
public var x: Float64
```

**Description:** Horizontal offset.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var y

```cangjie
public var y: Float64
```

**Description:** Vertical offset.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Float64, Float64, Float64, Float64)

```cangjie
public init(
    x: Float64,
    y: Float64,
    width: Float64,
    height: Float64
)
```

**Description:** Constructs a RectResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type    | Required | Default | Description           |
|:----------|:--------|:---------|:--------|:----------------------|
| x         | Float64 | Yes      | -       | Horizontal offset     |
| y         | Float64 | Yes      | -       | Vertical offset       |
| width     | Float64 | Yes      | -       | Width of the component|
| height    | Float64 | Yes      | -       | Height of the component|

### class ScrollAnimationOptions

```cangjie
public class ScrollAnimationOptions {
    public var duration: Float64
    public var curve: Curve
    public var canOverScroll: Bool
    public init(
        duration!: Float64 = 1000.0,
        curve!: Curve = Curve.Ease,
        canOverScroll!: Bool = false
    )
}
```

**Description:** Custom scroll animation parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var canOverScroll

```cangjie
public var canOverScroll: Bool
```

**Description:** Sets whether scrolling can overshoot boundaries.

**Type:** Bool

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var curve

```cangjie
public var curve: Curve
```

**Description:** Sets the scroll curve.

**Type:** [Curve](./cj-common-types.md#enum-curve)

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var duration

```cangjie
public var duration: Float64
```

**Description:** Sets the scroll duration.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Float64, Curve, Bool)

```cangjie
public init(
    duration!: Float64 = 1000.0,
    curve!: Curve = Curve.Ease,
    canOverScroll!: Bool = false
)
```

**Description:** Constructs a ScrollAnimationOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter    | Type                          | Required | Default    | Description                                                                 |
|:-------------|:------------------------------|:---------|:-----------|:----------------------------------------------------------------------------|
| duration     | Float64                       | No       | 1000.0     | **Named parameter.** Scroll duration. If set to a negative value, the default value is used. |
| curve        | [Curve](./cj-common-types.md#enum-curve) | No       | Curve.Ease | **Named parameter.** Scroll curve.                                          |
| canOverScroll| Bool                          | No       | false      | **Named parameter.** Sets whether scrolling can overshoot boundaries.<br>**Note:**<br>Overscrolling is only allowed when set to true and the component's edgeEffect is set to EdgeEffect.Spring, triggering a bounce animation upon overscroll. |

### class ScrollEdgeOptions

```cangjie
public class ScrollEdgeOptions {
    public var velocity: Float32 = 0.0
    public init(velocity!: Float32 = 0.0)
}
```

**Description:** Parameters for scrolling to the edge position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var velocity

```cangjie
public var velocity: Float32 = 0.0
```

**Description:** Sets the fixed speed for scrolling to the container edge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Type:** Float32

**Readable/Writable:** Yes


#### init(Float32)

```cangjie
public init(velocity!: Float32 = 0.0)
```

**Description:** Constructs a ScrollEdgeOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description                                                                 |
|:----------|:-------|:---------|:--------|:----------------------------------------------------------------------------|
| velocity  | Float32| No       | 0.0     | Fixed speed for scrolling to the container edge. If set to ≤0, this parameter is ignored.<br>Default: 0<br>Unit: vp/s |

### class ScrollResult

```cangjie
public class ScrollResult {
    public var offsetRemain: Float64
    public init(offsetRemain!: Float64)
}
```

**Description:** Return value object for OnWillScrollCallback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offsetRemain

```cangjie
public var offsetRemain: Float64
```

**Description:** Pending scroll offset.

**Type:** Float64

**Readable/Writable:** Yes

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Float64)

```cangjie
public init(offsetRemain!: Float64)
```

**Description:** Constructs a ScrollResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter    | Type    | Required | Default | Description                     |
|:-------------|:--------|:---------|:--------|:--------------------------------|
| offsetRemain | Float64 | Yes      | -       | Pending scroll offset. Unit: vp.|

### class ScrollToIndexOptions

```cangjie
public class ScrollToIndexOptions {
    public var extraOffset: Length = 0.vp
    public init(extraOffset!: Length = 0.vp)
}
```

**Description:** Parameters for scrolling to a specified index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var extraOffset

```cangjie
public var extraOffset: Length = 0.vp
```

**Description:** Extra offset for scrolling to the specified index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Readable/Writable:** Yes

#### init(Length)

```cangjie
public init(extraOffset!: Length = 0.vp)
```

**Description:** Constructs a ScrollToIndexOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter   | Type                                      | Required | Default | Description                                                                 |
|:------------|:------------------------------------------|:---------|:--------|:----------------------------------------------------------------------------|
| extraOffset | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No       | 0.vp    | Extra offset for scrolling to the specified index. Positive values add an offset toward the bottom; negative values add an offset toward the top. |

### class ScrollableBase

```cangjie
public abstract class ScrollableBase <: ContainerBase {}
```

**Description:** Describes common properties of scrollable components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [ContainerBase](./cj-ui-framework.md#containerbase)

#### func clipContent(ContentClipMode)

```cangjie
public func clipContent(clip: ContentClipMode): This
```

**Description:** Sets the clipping region for the content layer of a scrollable container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                          | Required | Default | Description                                                                 |
|:----------|:------------------------------|:---------|:--------|:----------------------------------------------------------------------------|
| clip      | [ContentClipMode](#enum-contentclipmode) | Yes      | -       | Default: ContentClipMode.BOUNDARY for Grid and Scroll; ContentClipMode.CONTENT_ONLY for List and WaterFlow. Clipping applies only to the container's content (child nodes); backgrounds are unaffected. When using RectShape to define a custom rectangular area, only width, height, and [offset](./cj-universal-attribute-location.md#func-offsetlength-length) relative to the component's top-left corner are supported; rounded corners are not supported. |

#### func clipContent(RectShape)

```cangjie
public func clipContent(clip: RectShape): This
```

**Description:** Sets the clipping region for the content layer of a scrollable container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type      | Required | Default | Description                                                                 |
|:----------|:----------|:---------|:--------|:----------------------------------------------------------------------------|
| clip      | RectShape | Yes      | -       | Default: ContentClipMode.BOUNDARY for Grid and Scroll; ContentClipMode.CONTENT_ONLY for List and WaterFlow. Clipping applies only to the container's content (child nodes); backgrounds are unaffected. When using RectShape to define a custom rectangular area, only width, height, and [offset](./cj-universal-attribute-location.md#func-offsetlength-length) relative to the component's top-left corner are supported; rounded corners are not supported. |

#### func enableScrollInteraction(Bool)

```cangjie
public func enableScrollInteraction(value: Bool): This
```

**Description:** Sets whether scroll gestures are supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description                                                                 |
|:----------|:-----|:---------|:--------|:----------------------------------------------------------------------------|
| value     | Bool | Yes      | -       | Whether scroll gestures are supported. When set to true, scrolling can be triggered via touch or mouse; when set to false, scrolling via touch or mouse is disabled, but scrolling via the [Scroller](https://docs.openharmony.cn/pages/v5.0/en/application-dev/reference/apis-arkui/arkui-ts/ts-container-scroll.md) controller remains unaffected. |

#### func fadingEdge(Option\<Bool>)

```cangjie
public func fadingEdge(enabled: Option<Bool>): This
```

**Description:** Enables/disables edge fading effects and sets the fading length.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type          | Required | Default | Description                                                                 |
|:----------|:--------------|:---------|:--------|:----------------------------------------------------------------------------|
| enabled   | Option\<Bool> | Yes      | -       | When fadingEdge is enabled, it overrides the component's .overlay() property.<br>When fadingEdge is enabled, avoid setting background-related properties on the component, as they may affect the fading effect.<br>When fadingEdge is enabled, the component is clipped to its boundaries, and setting clip to false has no effect.<br>Set to true to enable edge fading; set to false to disable it. |

#### func fadingEdge(Option\<Bool>, FadingEdgeOptions)

```cangjie
public func fadingEdge(enabled: Option<Bool>, options: FadingEdgeOptions): This
```

**Description:** Enables/disables edge fading effects and sets the fading length.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                   | Required | Default | Description                                                                 |
|:----------|:-----------------------|:---------|:--------|:----------------------------------------------------------------------------|
| enabled   | Option\<Bool>          | Yes      | -       | When fadingEdge is enabled, it overrides the component's .overlay() property.<br>When fadingEdge is enabled, avoid setting background-related properties on the component, as they may affect the fading effect.<br>When fadingEdge is enabled, the component is clipped to its boundaries, and setting clip to false has no effect.<br>Set to true to enable edge fading; set to false to disable it. |
| options   | [FadingEdgeOptions](#class-fadingedgeoptions) | Yes      | -       | Edge fading parameters. This object defines edge fading properties, such as fading length. |

#### func flingSpeedLimit(Float64)

```cangjie
public func flingSpeedLimit(speedLimit: Float64): This
```

**Description:** Limits the maximum initial speed when a fling animation starts after a scroll gesture ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter   | Type    | Required | Default | Description                                                                 |
|:------------|:--------|:---------|:--------|:----------------------------------------------------------------------------|
| speedLimit  | Float64 | Yes      | -       | Maximum initial speed when a fling animation starts. Unit: vp/s<br>Range: (0, +∞). If set to ≤0, the default value is used. |

#### func friction(Float64)

```cangjie
public func friction(value: Float64): This
```

**Description:** Sets the friction coefficient, which takes effect during manual scrolling and affects only the inertial scrolling process, indirectly influencing chained effects during inertial scrolling. If set to ≤0, the default value is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type    | Required | Default | Description                                                                 |
|:----------|:--------|:---------|:--------|:----------------------------------------------------------------------------|
| value     | Float64 | Yes      | -       | Friction coefficient. Default: 0.6 for non-wearable devices; 0.9 for wearable devices.<br>From API version 11, the default for non-wearable devices is 0.7.<br>From API version 12, the default for non-wearable devices is 0.75.<br>Range: (0, +∞). If set to ≤0, the default value is used. |

#### func friction(AppResource)

```cangjie
public func friction(value: AppResource): This
```

**Description:** Sets the friction coefficient, which takes effect during manual scrolling and affects only the inertial scrolling process, indirectly influencing chained effects during inertial scrolling. If set to ≤0, the default value is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                                | Required | Default | Description                                                                 |
|:----------|:------------------------------------|:---------|:--------|:----------------------------------------------------------------------------|
| value     | [AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes      | -       | Friction coefficient. Default: 0.6 for non-wearable devices; 0.9 for wearable devices.<br>From API version 11, the default for non-wearable devices is 0.7.<br>From API version 12, the default for non-wearable devices is 0.75.<br>Range: (0, +∞). If set to ≤0, the default value is used. |

#### func nestedScroll(NestedScrollOptions)

```cangjie
public func nestedScroll(value: NestedScrollOptions): This
```

**Description:** Sets the nested scroll mode for both directions to achieve coordinated scrolling with the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                              | Required | Default | Description                     |
|:----------|:----------------------------------|:---------|:--------|:--------------------------------|
| value     | [NestedScrollOptions](#class-nestedscrolloptions) | Yes      | -       | Nested scroll options.          |

#### func onDidScroll(OnScrollCallBack)

```cangjie
public func onDidScroll(handler: OnScrollCallBack): This
```

**Description:** Triggered when a scrollable component is scrolled, returning the offset of the current frame and the current scroll state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type              | Required | Default | Description                     |
|:----------|:------------------|:---------|:--------|:--------------------------------|
| handler   | OnScrollCallBack  | Yes      | -       | Callback triggered during scrolling. |

#### func onReachEnd(() -> Unit)

```cangjie
public func onReachEnd(event: () -> Unit): This
```

**Description:** Triggered when a scrollable component reaches the### class Scroller

```cangjie
public class Scroller {
    public init()
}
```

**Function:** Controller for scrollable container components. This component can be bound to a container component to control its scrolling behavior. A single controller cannot manage multiple container components. Currently supports binding to List, Scroll, ScrollBar, Grid, and WaterFlow.

> **Notes:**
>
> 1. The binding between the Scroller controller and the scrollable container component occurs during the component creation phase.
>
> 2. The Scroller methods can only be called normally after the controller is bound to the scrollable container component. Otherwise, depending on the interface called, the operation may either fail silently or throw an exception.
>
> 3. Taking [aboutToAppear](cj-universal-attribute-menu.md#func-abouttoappear) as an example, `aboutToAppear` executes after creating a new instance of a custom component but before its `build()` method is executed. Therefore, if the scrollable component is within the `build` method of a custom component, the Scroller methods cannot be called normally during the execution of `aboutToAppear` for that custom component, as the internal scrollable component has not yet been created.
>
> 4. Taking [onAppear](cj-ui-framework.md#func-Onappear---unit) as an example, this callback is triggered after the component is mounted and displayed. Thus, during the execution of the scrollable component's `onAppear` callback, the scrollable component has already been created and successfully bound to the Scroller, allowing normal invocation of Scroller methods.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init()

```cangjie
public init()
```

**Function:** Constructs a Scroller object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func currentOffset()

```cangjie
public func currentOffset(): OffsetResult
```

**Function:** Retrieves the current scroll offset.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
|[OffsetResult](#class-offsetresult)| Returns the current scroll offset.<br/>**Note:**<br/>If the Scroller controller is not bound to a container component or the container component is abnormally released, the return value of `currentOffset` will be empty.|

#### func fling(Float64)

```cangjie
public func fling(velocity: Float64): Unit
```

**Function:** Enables inertial scrolling for the scrollable component based on the provided initial velocity.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|velocity|Float64|Yes|-|If the `velocity` value is set to 0, it is treated as an invalid value, and scrolling will not occur. A positive value scrolls toward the top, while a negative value scrolls toward the bottom.<br/>Range: (-∞, +∞) Initial velocity for inertial scrolling. Unit: vp/s|

#### func getItemIndex(Float64, Float64)

```cangjie
public func getItemIndex(x: Float64, y: Float64): Int32
```

**Function:** Retrieves the index of a child component based on coordinates.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|x|Float64|Yes|-|X-axis coordinate, in vp.|
|y|Float64|Yes|-|Y-axis coordinate, in vp.|

**Notes:**

- Invalid values return an index of -1.

**Return Value:**

| Type | Description |
|:----|:----|
|Int32|Returns the index of the child component. Unit: vp.|

#### func getItemRect(Int32)

```cangjie
public func getItemRect(index: Int32): RectResult
```

**Function:** Retrieves the size and position of a child component relative to the container component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|index|Int32|Yes|-|Index value of the child component.|

**Return Value:**

| Type | Description |
|:----|:----|
|[RectResult](#class-rectresult)|Size and position of the child component relative to the container component.<br/>Unit: vp.|

#### func isAtEnd()

```cangjie
public func isAtEnd(): Bool
```

**Function:** Checks whether the component has scrolled to the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
|Bool|`true` indicates the component has scrolled to the bottom; `false` indicates it has not.|

#### func scrollBy(Length, Length)

```cangjie
public func scrollBy(xOffset!: Length, yOffset!: Length): Unit
```

**Function:** Scrolls by a specified distance.

**Notes:**

- Supports Scroll, List, Grid, and WaterFlow components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|xOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Horizontal scroll distance. Percentage values are not supported.<br/>Range: (-∞, +∞)|
|yOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Vertical scroll distance. Percentage values are not supported. Range: (-∞, +∞)|

#### func scrollEdge(Edge)

```cangjie
public func scrollEdge(value: Edge): Unit
```

**Function:** Scrolls to the edge of the container, regardless of the scroll axis direction. `Edge.Top` and `Edge.Start` behave the same, as do `Edge.Bottom` and `Edge.End`. Scroll components have animations by default, while Grid, List, and WaterFlow components do not.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|value|[Edge](./cj-common-types.md#enum-edge)|Yes|-| Edge position to scroll to. |

#### func scrollEdge(Edge, ScrollEdgeOptions)

```cangjie
public func scrollEdge(value: Edge, options: ScrollEdgeOptions): Unit
```

**Function:** Scrolls to the edge of the container, regardless of the scroll axis direction. `Edge.Top` and `Edge.Start` behave the same, as do `Edge.Bottom` and `Edge.End`. Scroll components have animations by default, while Grid, List, and WaterFlow components do not.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|value|[Edge](./cj-common-types.md#enum-edge)|Yes|-|Edge position to scroll to.|
|options|[ScrollEdgeOptions](#class-scrolledgeoptions)|Yes||Mode for scrolling to the edge position.|

#### func scrollPage(Bool)

```cangjie
public func scrollPage(next: Bool): Unit
```

**Function:** Scrolls to the next or previous page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|next|Bool|Yes|-|Whether to scroll to the next page. `true` scrolls to the next page; `false` scrolls to the previous page.|

#### func scrollPage(Bool, Bool)

```cangjie
public func scrollPage(next: Bool, animation!: Bool = false): Unit
```

**Function:** Scrolls to the next or previous page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|next|Bool|Yes|-|Whether to scroll to the next page. `true` scrolls to the next page; `false` scrolls to the previous page.|
|animation|Bool|No|false|Animation configuration.<br/>\- boolean: Enables the default spring animation.|

#### func scrollTo(Length, Length)

```cangjie
public func scrollTo(xOffset!: Length, yOffset!: Length): Unit
```

**Function:** Scrolls to a specified position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|xOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-| **Named parameter.** Horizontal scroll offset (Int64, Float64 values in vp).<br>**Note:**<br>Percentage values are not supported.<br>Only effective when the scroll axis is the x-axis.<br>For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position. |
|yOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-| **Named parameter.** Vertical scroll offset (Int64, Float64 values in vp).<br>**Note:**<br>Percentage values are not supported.<br>Only effective when the scroll axis is the y-axis.<br>For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position.|

#### func scrollTo(Length, Length, ScrollAnimationOptions)

```cangjie
public func scrollTo(xOffset!: Length, yOffset!: Length, animation!: ScrollAnimationOptions): Unit
```

**Function:** Scrolls to a specified position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|xOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Horizontal scroll offset.<br/>**Note:**<br/>Percentage values are not supported.<br/>Only effective when the scroll axis is the x-axis.<br/>Range: For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position, but the `animation` parameter can enable rebound animations when scrolling exceeds bounds.|
|yOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Vertical scroll offset.<br/>**Note:**<br/>Percentage values are not supported.<br/>Only effective when the scroll axis is the y-axis.<br/>Range: For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position, but the `animation` parameter can enable rebound animations when scrolling exceeds bounds.|
|animation|[ScrollAnimationOptions](#class-scrollanimationoptions)|Yes|-|Custom scroll animation. Initial value: ScrollAnimationOptions(duration: 1000, curve: Curve.Ease, canOverScroll: false)|

#### func scrollTo(Length, Length, Bool)

```cangjie
public func scrollTo(xOffset!: Length, yOffset!: Length, animation!: Bool): Unit
```

**Function:** Scrolls to a specified position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|xOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Horizontal scroll offset.<br/>**Note:**<br/>Percentage values are not supported.<br/>Only effective when the scroll axis is the x-axis.<br/>Range: For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position, but the `animation` parameter can enable rebound animations when scrolling exceeds bounds.|
|yOffset|[Length](../BasicServicesKit/cj-apis-base.md#interface-length)|Yes|-|Vertical scroll offset.<br/>**Note:**<br/>Percentage values are not supported.<br/>Only effective when the scroll axis is the y-axis.<br/>Range: For values less than 0, non-animated scrolling treats them as 0. Animated scrolling defaults to stopping at the starting position, but the `animation` parameter can enable rebound animations when scrolling exceeds bounds.|
| animation | Bool | Yes | - | **Named parameter.** Animation configuration, enabling the default spring animation.<br>Initial value: false.|

#### func scrollToIndex(Int32, Bool, ScrollAlign, ScrollToIndexOptions)

```cangjie
public func scrollToIndex(
    index: Int32,
    smooth!: Bool = false,
    align!: ScrollAlign = ScrollAlign.Start,
    options!: ScrollToIndexOptions = ScrollToIndexOptions()
): This
```

**Function:** Scrolls to a specified index, supporting additional offset configuration.

Enabling the `smooth` animation may cause performance issues when loading and laying out a large number of items.

> **Note:**
>
> Only supports Grid, List, and WaterFlow components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|index|Int32|Yes|-|Target element index within the current container.<br/>**Note:**<br/>Negative values or values exceeding the maximum child component index are treated as invalid, and the operation will not proceed.|
|smooth|Bool|No|false|Whether to enable animation when scrolling to the specified index. `true` enables animation; `false` disables it.<br/>Default: false.|
|align|[ScrollAlign](#enum-scrollalign)|No|ScrollAlign.Start|Default value for List: ScrollAlign.START. Default for Grid: ScrollAlign.AUTO. Default for WaterFlow: ScrollAlign.START. **Note:** Only List, Grid, and WaterFlow components support this parameter. Specifies the alignment of the target element relative to the container.|
|options|[ScrollToIndexOptions](#class-scrolltoindexoptions)|No|ScrollToIndexOptions()|Options for scrolling to the specified index, such as additional offsets.<br/>Default: 0, Unit: vp.|

### enum ContentClipMode

```cangjie
public enum ContentClipMode {
    | ContentOnly
    | Boundary
    | SafeArea
}
```

**Function:** Defines the clipping region enumeration for scrollable container content layers.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Boundary

```cangjie
Boundary
```

**Function:** Clips to the component boundary.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### ContentOnly

```cangjie
ContentOnly
```

**Function:** Clips to the content area only.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SafeArea

```cangjie
SafeArea
```

**Function:** Clips to the SafeArea region configured for the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### enum ScrollAlign

```cangjie
public enum ScrollAlign {
    | Start
    | Center
    | End
    | Auto
}
```

**Function:** Alignment method enumeration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Auto

```cangjie
Auto
```

**Function:** Auto alignment.

If the specified item is fully within the display area, no adjustment is made. Otherwise, it aligns the item's start or end with the List based on the shortest scroll distance, ensuring the item is fully visible.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Center

```cangjie
Center
```

**Function:** Center alignment. The specified item is center-aligned with the List along the main axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### End

```cangjie
End
```

**Function:** End alignment. The specified item's end is aligned with the List's end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Start

```cangjie
Start
```

**Function:** Start alignment. The specified item's start is aligned with the List's start.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21## Sample Code 1 (Setting Scroller Controller)

This example demonstrates the usage of some properties of the Scroll component and the scroller controller.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import kit.PerformanceAnalysisKit.Hilog

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

@Entry
@Component
class EntryView {
    let scroller = Scroller()
    var arr: ArrayList<String> = ArrayList(["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"])

    func build() {
        Stack(alignContent: Alignment.TopStart) {
            Scroll(this.scroller) {
                Column {
                    ForEach(
                        this.arr,
                        itemGeneratorFunc: {
                            item: String, idx: Int64 => Text(item)
                                .width(90.percent)
                                .height(150)
                                .backgroundColor(0xFFFFFF)
                                .borderRadius(15)
                                .textAlign(TextAlign.Center)
                                .fontSize(16)
                                .margin(top: 10)
                        }
                    )
                }
            }
                .scrollable(ScrollDirection.Vertical) // Vertical scroll direction
                .scrollBar(BarState.On) // Persistent scrollbar display
                .scrollBarColor(Color.Gray) // Scrollbar color
                .scrollBarWidth(10.px) // Scrollbar width
                .friction(0.6)
                .onScrollEdge(
                    {
                        edge => match (edge) {
                            case Edge.Top => loggerInfo("Top")
                            case Edge.Bottom => loggerInfo("Bottom")
                            case _ => loggerInfo("None")
                        }
                    })
                .onScrollStop({
                    => loggerInfo("Scroll Stop")
                })

            Button("scroll 150")
                .onClick({
                    evt => // Scroll down by specified distance 150.0vp after click
                    this
                        .scroller
                        .scrollBy(xOffset: 0, yOffset: 150)
                })
                .margin(top: 10, left: 20)

            Button("scroll 100")
                .onClick(
                    {
                        evt => // Scroll to specified position (down 100.0vp) after click
                        loggerInfo("current offset ${this.scroller.currentOffset().yOffset}")
                        loggerInfo("CALCULATE offset ${this.scroller.currentOffset().yOffset + 100.0}")
                        let curyOffset = this
                            .scroller
                            .currentOffset()
                            .yOffset
                        this
                            .scroller
                            .scrollTo(xOffset: 0.vp, yOffset: (curyOffset + 100.0).vp, animation: ScrollAnimationOptions(duration: 0.0, curve: Curve.Ease))
                    }
                )
                .margin(top: 60, left: 20)

            Button("back top")
                .onClick({
                    evt => // Return to top after click
                    this
                        .scroller
                        .scrollEdge(Edge.Top)
                })
                .margin(top: 110, left: 20)

            Button("next page")
                .onClick({
                    evt => // Scroll to next page after click
                    this
                        .scroller
                        .scrollPage(true, animation: false)
                })
                .margin(top: 160, left: 20)

            Button("fling -3000")
                .onClick({
                    evt => // Trigger inertial scrolling with initial velocity of -3000vp/s after click
                    this
                        .scroller
                        .fling(-3000.0)
                })
                .margin(top: 210, left: 20)

            Button("next page slowly")
                .onClick({
                    evt => // Scroll to next page with animation enabled after click
                    this
                        .scroller
                        .scrollPage(true, animation: true)
                })
                .margin(top: 260, left: 20)
        }
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xDCDCDC)
    }
}
```

## Sample Code 2 (Nested Scrolling Implementation Method 1)

This example uses the onScrollFrameBegin event to implement nested scrolling between the inner List component and outer Scroll component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
    @State
    var listPosition: Int32 = 0 // 0 means scrolled to List top, 1 means intermediate value, 2 means scrolled to List bottom.
    let scroller = Scroller()
    let scrollerForList = Scroller()
    var arr: ArrayList<String> = ArrayList(["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"])

    func build() {
        Flex() {
            Scroll(this.scroller) {
                Column() {
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(40.percent)
                        .backgroundColor(0x330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                        .onClick(
                            {
                                evt => this
                                    .scrollerForList
                                    .scrollToIndex(5, smooth: false, align: ScrollAlign.Start, options: ScrollToIndexOptions(extraOffset: 5.vp))
                            })

                    List(space: 20, scroller: this.scrollerForList) {
                        ForEach(
                            this.arr,
                        itemGeneratorFunc: {
                            item: String, idx: Int64 => ListItem() {
                                Text("ListItem" + item)
                                    .width(100.percent)
                                    .height(100.percent)
                                    .backgroundColor(Color.White)
                                    .borderRadius(15)
                                    .textAlign(TextAlign.Center)
                                    .fontSize(16)
                                    .margin(top: 10)
                            }
                                .width(100.percent)
                                .height(100)
                        }
                    )
                }
                    .width(100.percent)
                    .height(50.percent)
                    .edgeEffect(EdgeEffect.None)
                    .friction(0.6)
                    .onReachStart({
                        => this.listPosition = 0
                    })
                    .onReachEnd({
                        => this.listPosition = 2
                    })
                    .onScrollFrameBegin(
                        {
                            x: Float64, y: ScrollState =>
                            if ((this.listPosition == 0 && x <= 0.0) || (this.listPosition == 2 && x >= 0.0)) {
                                this
                                    .scroller
                                    .scrollBy(xOffset: 0.0, yOffset: x)
                                return onScrollFrameBeginHandleResult(offsetRemain: 0.0)
                            }
                            this.listPosition = 1
                            return onScrollFrameBeginHandleResult(offsetRemain: x)
                        }
                    )

                Text("Scroll Area")
                    .width(100.percent)
                    .height(40.percent)
                    .backgroundColor(0x330000FF)
                    .fontSize(16)
                    .textAlign(TextAlign.Center)
            }
        }
            .width(100.percent)
            .height(100.percent)
    }
        .width(100.percent)
        .height(100.percent)
        .backgroundColor(0xDCDCDC)
        .padding(20)
    }
}
```

## Sample Code 3 (Nested Scrolling Implementation Method 2)

This example uses the nestedScroll property to implement nested scrolling between the inner List component and outer Scroll component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
    @State
    var arr: ArrayList<Int64> = ArrayList<Int64>(30)

    func build() {
        Scroll {
            Column {
                Text("Scroll Area")
                    .width(100.percent)
                    .height(40.percent)
                    .backgroundColor(0x00800C)
                    .textAlign(TextAlign.Center)
                Tabs(barPosition: BarPosition.Start) {
                    TabContent {
                        List(space: 10) {
                            ForEach(
                                this.arr,
                                itemGeneratorFunc: {
                                    item: Int64, idx: Int64 => ListItem {
                                        Text("item" + item.toString()).fontSize(16)
                                    }
                                        .backgroundColor(Color.White)
                                        .height(72)
                                        .width(100.percent)
                                        .borderRadius(12)
                                },
                                keyGeneratorFunc: {
                                    item: Int64, idx: Int64 => item.toString()
                                }
                            )
                        }
                            .width(100.percent)
                            .edgeEffect(EdgeEffect.Spring)
                            .nestedScroll(
                                NestedScrollOptions(NestedScrollMode.ParentFirst, NestedScrollMode.SelfFirst))
                    }.tabBar("Tab1")

                    TabContent {
                    }.tabBar("Tab2")
                }
                    .vertical(false)
                    .height(100.percent)
            }.width(100.percent)
        }
            .friction(0.6)
            .backgroundColor(0xDCDCDC)
            .scrollBar(BarState.Off)
            .width(100.percent)
            .height(100.percent)
    }

    protected override func aboutToAppear() {
        for (i in 0..30) {
            this.arr.add(i)
        }
    }
}
```

## Sample Code 4 (Parent-to-Child Scrolling Transfer in Nested Scrolling)

This example uses the enableScrollInteraction property and onScrollFrameBegin event to implement scrolling transfer from parent component to child component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
    private var headerHeight: Float64 = 0.0
    private var arr: ArrayList<Int64> = ArrayList<Int64>()
    private var scrollerForParent: Scroller = Scroller()
    private var scrollerForChild: Scroller = Scroller()

    protected override func aboutToAppear() {
        for (i in 0..10) {
            this.arr.add(i)
        }
    }

    func build() {
        Scroll(this.scrollerForParent) {
            Column {
                Text("Scroll Area")
                    .width(100.percent)
                    .height(40.percent)
                    .backgroundColor(0x330000FF)
                    .fontSize(16)
                    .textAlign(TextAlign.Center)

                List(space: 20, scroller: this.scrollerForChild) {
                    ForEach(
                        this.arr,
                        itemGeneratorFunc: {
                            item: Int64, idx: Int64 => ListItem {
                                Text("ListItem" + item.toString())
                                    .width(100.percent)
                                    .height(100.percent)
                                    .borderRadius(15)
                                    .fontSize(16)
                                    .textAlign(TextAlign.Center)
                                    .backgroundColor(Color.White)
                            }
                                .width(100.percent)
                                .height(100)
                        },
                        keyGeneratorFunc: {
                            item: Int64, idx: Int64 => item.toString()
                        }
                    )
                }
                    .width(100.percent)
                    .height(100.percent)
                    .edgeEffect(EdgeEffect.None)
                    .scrollBar(BarState.Off)
                    .enableScrollInteraction(false)

                Text("Scroll Area")
                    .width(100.percent)
                    .height(40.percent)
                    .backgroundColor(0x330000FF)
                    .fontSize(16)
                    .textAlign(TextAlign.Center)
            }
        }
            .scrollBar(BarState.Off)
            .onScrollFrameBegin(
                {
                    offset: Float64, state: ScrollState =>
                    var retOffset = offset
                    var currentOffset = this
                        .scrollerForParent
                        .currentOffset()
                        .yOffset
                    var newOffset = currentOffset + offset
                    if (offset > 0.0) {
                        if (this
                            .scrollerForChild
                            .isAtEnd()) {
                            return offset
                        }
                        if (newOffset > this.headerHeight) {
                            this
                                .scrollerForChild
                                .scrollBy(xOffset: 0.0, yOffset: retOffset)
                            if (currentOffset < this.headerHeight) {
                                return this.headerHeight - currentOffset
                            } else {
                                return 0.0
                            }
                        }
                    } else {
                        if (this
                            .scrollerForChild
                            .currentOffset()
                            .yOffset <= 0.0) {
                            return offset
                        }
                        if (newOffset < this.headerHeight) {
                            this
                                .scrollerForChild
                                .scrollBy(xOffset: 0.0, yOffset: retOffset)
                            return 0.0
                            if (currentOffset > this.headerHeight) {
                                return this.headerHeight - currentOffset
                            } else {
                                return 0.0
                            }
                        }
                    }
                    return offset
                }
            )
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xDCDCDC)
    }
}
```## Sample Code 5 (Setting Scroll Boundary)

This example demonstrates the implementation of boundary-limited scrolling for the Scroll component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
    var scroller: Scroller = Scroller()
    private var arr: ArrayList<Int64> = ArrayList<Int64>(16, {i => i+1})
    func build() {
        Scroll(this.scroller) {
            Column {
                ForEach(this.arr, itemGeneratorFunc: {item: Int64, idx: Int64 =>
                            Text(item.toString())
                            .width(90.percent)
                            .height(200)
                            .backgroundColor(0xFFFFFF)
                            .borderWidth(1)
                            .borderRadius(15)
                            .fontSize(16)
                            .textAlign(TextAlign.Center)
                })
            }.width(100.percent).backgroundColor(0xDCDCDC)
        }
        .backgroundColor(Color.White)
        .height(100.percent)
    }
}
```

## Sample Code 7 (Setting Edge Fading Effect)

This example demonstrates enabling edge fading effect for the Scroll component and configuring the fading edge length.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
    var scroller: Scroller = Scroller()
    private var arr: ArrayList<Int64> = ArrayList<Int64>([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])

    func build() {
        Stack(alignContent: Alignment.TopStart) {
            Scroll(this.scroller) {
                Column {
                    ForEach(
                        this.arr,
                        itemGeneratorFunc: {
                            item: Int64, idx: Int64 => Text(item.toString())
                                .width(90.percent)
                                .height(150)
                                .backgroundColor(0xFFFFFF)
                                .borderRadius(15)
                                .fontSize(16)
                                .textAlign(TextAlign.Center)
                                .margin(top: 10)
                        }
                    )
                }.width(100.percent)
            }.fadingEdge(true, FadingEdgeOptions(fadingEdgeLength: 80))
        }
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xDCDCDC)
    }
}
```

![scroll7](./figures/scroll7.gif)