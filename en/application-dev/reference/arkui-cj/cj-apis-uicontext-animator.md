# AnimatorResult

Provides the result of component animations, including starting animations, resetting animation parameters, and playing animations in reverse order.

> **NOTE:**
>
> The following APIs require first creating an AnimatorResult object using the [createAnimator()](./cj-apis-uicontext-uicontext.md#func-createanimatoranimatoroptions) method from [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext), then calling the corresponding methods through this object.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class AnimatorResult

```cangjie
public class AnimatorResult {
}
```

**Description:** Defines the Animator result type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop onFrame

```cangjie
public mut prop onFrame: (Float64) -> Unit
```

**Description:** Callback when a frame is received.

**Type:** (Float64) -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop onFinish

```cangjie
public mut prop onFinish: () -> Unit
```

**Description:** Callback when the animation completes.

**Type:** () -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop onCancel

```cangjie
public mut prop onCancel: () -> Unit
```

**Description:** Callback when the animation is canceled.

**Type:** () -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop onRepeat

```cangjie
public mut prop onRepeat: () -> Unit
```

**Description:** Callback when the animation repeats.

**Type:** () -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func reset(AnimatorOptions)

```cangjie
public func reset(options: AnimatorOptions): Unit
```

**Description:** Resets the current animator animation parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|options|[AnimatorOptions](#class-animatoroptions)|Yes|-|Animation options.|

### func play()

```cangjie
public func play(): Unit
```

**Description:** Starts the animation. The animation retains the previous playback state, such as the reverse state set during playback, which will be preserved when played again.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func finish()

```cangjie
public func finish(): Unit
```

**Description:** Ends the animation, triggering the [onFinish](#prop-onfinish) callback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func pause()

```cangjie
public func pause(): Unit
```

**Description:** Pauses the animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func cancel()

```cangjie
public func cancel(): Unit
```

**Description:** Cancels the animation, triggering the [onCancel](#prop-oncancel) callback. This interface is functionally identical to the [finish](#func-finish) interface, differing only in the callback triggered. It is recommended to use the [finish](#func-finish) interface to end animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func reverse()

```cangjie
public func reverse(): Unit
```

**Description:** Plays the animation in reverse order. This interface is invalid when using the interpolating-spring curve.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func setExpectedFrameRateRange(ExpectedFrameRateRange)

```cangjie
public func setExpectedFrameRateRange(rateRange: ExpectedFrameRateRange): Unit
```

**Description:** Sets the expected frame rate range.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|rateRange|[ExpectedFrameRateRange](./cj-common-types.md#class-expectedframeraterange)|Yes|-|Frame rate range.|

## class AnimatorOptions

```cangjie
public class AnimatorOptions {
    public var duration: Int32
    public var easing: String
    public var delay: Int32
    public var fill: AnimatorFill
    public var direction: AnimatorDirection
    public var iterations: Int32
    public var begin: Float64
    public var end: Float64
    public init(
        duration!: Int32,
        easing!: String,
        delay!: Int32,
        fill!: AnimatorFill,
        direction!: AnimatorDirection,
        iterations!: Int32,
        begin!: Float64,
        end!: Float64
    )
}
```

**Description:** Defines animation options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var duration

```cangjie
public var duration: Int32
```

**Description:** Duration of the animation playback, in milliseconds.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var easing

```cangjie
public var easing: String
```

**Description:** Animation interpolation curve.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var delay

```cangjie
public var delay: Int32
```

**Description:** Delay time before animation playback starts, in milliseconds.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var fill

```cangjie
public var fill: AnimatorFill
```

**Description:** Whether to restore to the initial state after animation execution. After execution, the state at the end of the animation (defined in the last keyframe) will be retained.

**Type:** [AnimatorFill](#enum-animatorfill)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var direction

```cangjie
public var direction: AnimatorDirection
```

**Description:** Animation playback mode.

**Type:** [AnimatorDirection](#enum-animatordirection)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var iterations

```cangjie
public var iterations: Int32
```

**Description:** Number of animation playback iterations.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var begin

```cangjie
public var begin: Float64
```

**Description:** Starting point of animation interpolation.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var end

```cangjie
public var end: Float64
```

**Description:** Ending point of animation interpolation.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Int32, String, Int32, AnimatorFill, AnimatorDirection, Int32, Float64, Float64)

```cangjie
public init(
    duration!: Int32,
    easing!: String,
    delay!: Int32,
    fill!: AnimatorFill,
    direction!: AnimatorDirection,
    iterations!: Int32,
    begin!: Float64,
    end!: Float64
)
```

**Description:** Creates an AnimatorOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|duration|Int32|Yes|-|**Named parameter.** Duration of the animation playback, in milliseconds. Value range: [0, +∞).|
|easing|String|Yes|-|**Named parameter.** Animation interpolation curve.|
|delay|Int32|Yes|-|**Named parameter.** Delay time before animation playback starts, in milliseconds. When set to 0, no delay occurs. When set to a negative value, the animation starts early. If the early start time exceeds the total duration, the animation transitions directly to the end.|
|fill|[AnimatorFill](#enum-animatorfill)|Yes|-|**Named parameter.** Whether to restore to the initial state after animation execution. After execution, the state at the end of the animation (defined in the last keyframe) will be retained.|
|direction|[AnimatorDirection](#enum-animatordirection)|Yes|-|**Named parameter.** Animation playback mode.|
|iterations|Int32|Yes|-|**Named parameter.** Number of animation playback iterations. When set to 0, no playback occurs. When set to -1, playback is infinite. When set to a value greater than 0, it represents the number of playback iterations.|
|begin|Float64|Yes|-|**Named parameter.** Starting point of animation interpolation.|
|end|Float64|Yes|-|**Named parameter.** Ending point of animation interpolation.|## enum AnimatorFill

```cangjie
public enum AnimatorFill <: Equatable<AnimatorFill> {
    | None
    | Forwards
    | Backwards
    | Both
    | ...
}
```

**Function:** The state after animation execution.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[AnimatorFill](#enum-animatorfill)>

### None

```cangjie
None
```

**Function:** No styles will be applied to the target before or after animation execution.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Forwards

```cangjie
Forwards
```

**Function:** After animation ends, the target will retain the state at the end of animation (defined in the last keyframe).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Backwards

```cangjie
Backwards
```

**Function:** During the delay period in [AnimatorOptions](#class-animatoroptions), the animation will apply values defined in the first keyframe. When the direction in [AnimatorOptions](#class-animatoroptions) is Normal or Alternate, values from the 'from' keyframe are applied; when direction is Reverse or AlternateReverse, values from the 'to' keyframe are applied.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Both

```cangjie
Both
```

**Function:** The animation will follow both Forwards and Backwards rules, extending animation properties in both directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(AnimatorFill)

```cangjie
public operator func !=(other: AnimatorFill): Bool
```

**Function:** Compares whether two enum values are unequal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorFill](#enum-animatorfill) | Yes | - | Another enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### operator func ==(AnimatorFill)

```cangjie
public operator func ==(other: AnimatorFill): Bool
```

**Function:** Compares whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorFill](#enum-animatorfill) | Yes | - | Another enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

## enum AnimatorDirection

```cangjie
public enum AnimatorDirection <: Equatable<AnimatorDirection> {
    | Normal
    | Reverse
    | Alternate
    | AlternateReverse
    | ...
}
```

**Function:** Animation playback mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[AnimatorDirection](#enum-animatordirection)>

### Normal

```cangjie
Normal
```

**Function:** Animation plays forward in a loop.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Reverse

```cangjie
Reverse
```

**Function:** Animation plays backward in a loop.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Alternate

```cangjie
Alternate
```

**Function:** Animation alternates playback direction, playing forward on odd iterations and backward on even iterations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### AlternateReverse

```cangjie
AlternateReverse
```

**Function:** Animation alternates playback direction in reverse, playing backward on odd iterations and forward on even iterations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(AnimatorDirection)

```cangjie
public operator func !=(other: AnimatorDirection): Bool
```

**Function:** Compares whether two enum values are unequal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorDirection](#enum-animatordirection) | Yes | - | Another enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are unequal, otherwise returns false. |

### operator func ==(AnimatorDirection)

```cangjie
public operator func ==(other: AnimatorDirection): Bool
```

**Function:** Compares whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorDirection](#enum-animatordirection) | Yes | - | Another enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |