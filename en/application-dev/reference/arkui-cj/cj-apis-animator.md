# ohos.animator (Animation)

This module provides component animation effects, including defining animations, starting animations, and playing animations in reverse order.

## Import Module

```cangjie
import kit.UIKit.*
```

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

**Function:** Animation option type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var begin

```cangjie
public var begin: Float64
```

**Function:** Sets the starting point for animation interpolation.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var delay

```cangjie
public var delay: Int32
```

**Function:** Sets the delay time before animation playback.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var direction

```cangjie
public var direction: AnimatorDirection
```

**Function:** Sets the animation playback mode.

**Type:** [AnimatorDirection](#enum-animatordirection)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var duration

```cangjie
public var duration: Int32
```

**Function:** Sets the duration of animation playback.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var easing

```cangjie
public var easing: String
```

**Function:** Sets the animation interpolation curve.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var end

```cangjie
public var end: Float64
```

**Function:** Sets the ending point for animation interpolation.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var fill

```cangjie
public var fill: AnimatorFill
```

**Function:** Sets whether the animation should return to its initial state after execution.

**Type:** [AnimatorFill](#enum-animatorfill)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var iterations

```cangjie
public var iterations: Int32
```

**Function:** Sets the number of times the animation should play.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

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

**Function:** Creates an animation options object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| duration | Int32 | No | 0 | **Named parameter.** Duration of animation playback in milliseconds.<br>Range: [0, +∞). |
| easing | String | No | "ease" | **Named parameter.** Animation interpolation curve.<br>"linear": Linear animation change.<br>"ease": Animation starts and ends slowly, cubic-bezier(0.25, 0.1, 0.25, 1.0).<br>"ease-in": Animation starts slowly and speeds up, cubic-bezier(0.42, 0.0, 1.0, 1.0).<br>"ease-out": Animation starts fast and slows down, cubic-bezier(0.0, 0.0, 0.58, 1.0).<br>"ease-in-out": Animation speeds up then slows down, cubic-bezier(0.42, 0.0, 0.58, 1.0).<br>"fast-out-slow-in": Standard curve, cubic-bezier(0.4, 0.0, 0.2, 1.0).<br>"linear-out-slow-in": Deceleration curve, cubic-bezier(0.0, 0.0, 0.2, 1.0).<br>"fast-out-linear-in": Acceleration curve, cubic-bezier(0.4, 0.0, 1.0, 1.0).<br>"friction": Damping curve, cubic-bezier(0.2, 0.0, 0.2, 1.0).<br>"extreme-deceleration": Sharp deceleration curve, cubic-bezier(0.0, 0.0, 0.0, 1.0).<br>"rhythm": Rhythm curve, cubic-bezier(0.7, 0.0, 0.2, 1.0).<br>"sharp": Sharp curve, cubic-bezier(0.33, 0.0, 0.67, 1.0).<br>"smooth": Smooth curve, cubic-bezier(0.4, 0.0, 0.4, 1.0).<br>"cubic-bezier(x1,y1,x2,y2)": Cubic Bezier curve, x1 and x2 values must be between 0-1. Example: "cubic-bezier(0.42,0.0,0.58,1.0)".<br>"steps(number,step-position)": Step curve, number must be set as a positive integer, step-position is optional (start or end, default is end). Example: "steps(3,start)".<br>"interpolating-spring(velocity,mass,stiffness,damping)": Interpolating spring curve. velocity, mass, stiffness, damping are numerical values, with mass, stiffness, damping > 0. Refer to [Interpolating Spring Curve](./cj-apis-curves.md#static-func-interpolatingspringfloat32-float32-float32-float32) for details. When using interpolating-spring, duration is ineffective (determined by spring parameters); fill, direction, iterations settings are invalid (fill is fixed to "forwards", direction to "normal", iterations to 1), and [reverse](#reverse) function calls are invalid. Animator with interpolating-spring can only play forward once. |
| delay | Int32 | No | 0 | **Named parameter.** Delay time before animation playback in milliseconds. 0 means no delay. Negative values mean animation starts early; if early start time exceeds total duration, animation transitions directly to end state. |
| fill | [AnimatorFill](#enum-animatorfill) | No | AnimatorFill.None | **Named parameter.** Whether animation should return to initial state after execution. After execution, the end state (defined in the last keyframe) is retained. |
| direction | [AnimatorDirection](#enum-animatordirection) | No | AnimatorDirection.Normal | **Named parameter.** Animation playback mode. |
| iterations | Int32 | No | 0 | **Named parameter.** Number of animation plays. 0 means no play, -1 means infinite plays, >0 means play count.<br>**Note:**<br>Negative values other than -1 are invalid and default to 1 play. |
| begin | Float64 | No | 0.0 | **Named parameter.** Starting point for animation interpolation. |
| end | Float64 | No | 1.0 | **Named parameter.** Ending point for animation interpolation. |

## class AnimatorResult

```cangjie
public class AnimatorResult {}
```

**Function:** Defines the initialization class for animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop onCancel

```cangjie
public mut prop onCancel: () -> Unit
```

**Function:** Callback when animation is canceled. (Deprecated, recommended to use onCancel.)

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop onFinish

```cangjie
public mut prop onFinish: () -> Unit
```

**Function:** Callback when animation completes. (Deprecated, recommended to use onFinish.)

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop onFrame

```cangjie
public mut prop onFrame: (Float64) -> Unit
```

**Function:** Callback when a frame is received. (Deprecated, recommended to use onFrame.)

**Type:** (Float64) -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop onRepeat

```cangjie
public mut prop onRepeat: () -> Unit
```

**Function:** Callback when animation repeats. (Deprecated, recommended to use onRepeat.)

**Type:** () -> Unit

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func cancel()

```cangjie
public func cancel(): Unit
```

**Function:** Cancels the animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func finish()

```cangjie
public func finish(): Unit
```

**Function:** Finishes the animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func pause()

```cangjie
public func pause(): Unit
```

**Function:** Pauses the animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func play()

```cangjie
public func play(): Unit
```

**Function:** Starts the animation. The animation retains the previous playback state (e.g., reverse state).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func reset(AnimatorOptions)

```cangjie
public func reset(options: AnimatorOptions): Unit
```

**Function:** Updates the current animator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | [AnimatorOptions](#class-animatoroptions) | Yes | - | Defines animation options. |

### func reverse()

```cangjie
public func reverse(): Unit
```

**Function:** Plays the animation in reverse order. Invalid when using interpolating-spring curve.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func setExpectedFrameRateRange(ExpectedFrameRateRange)

```cangjie
public func setExpectedFrameRateRange(rateRange: ExpectedFrameRateRange): Unit
```

**Function:** Sets the expected frame rate range.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rateRange | [ExpectedFrameRateRange](./cj-animation-animateto.md#class-expectedframeraterange) | Yes | - | Sets the expected frame rate range. Constraints: 0 < ExpectedFrameRateRange.min <= ExpectedFrameRateRange.expected <= ExpectedFrameRateRange.max. If not met, defaults to ExpectedFrameRateRange(min:60, max:120, expected:60). |

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

**Since:** 21

### Alternate

```cangjie
Alternate
```

**Function:** Sets the animation to alternate playback (forward on odd counts, reverse on even counts).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### AlternateReverse

```cangjie
AlternateReverse
```

**Function:** Sets the animation to reverse alternate playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Normal

```cangjie
Normal
```

**Function:** Sets the animation to forward playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Reverse

```cangjie
Reverse
```

**Function:** Sets the animation to reverse playback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(AnimatorDirection)

```cangjie
public operator func !=(other: AnimatorDirection): Bool
```

**Function:** Compares whether two AnimatorDirection values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorDirection](#enum-animatordirection) | Yes | - | **Named parameter.** Animation playback mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether two AnimatorDirection values are not equal. |

### func ==(AnimatorDirection)

```cangjie
public operator func ==(other: AnimatorDirection): Bool
```

**Function:** Compares whether two AnimatorDirection values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorDirection](#enum-animatordirection) | Yes | - | **Named parameter.** Animation playback mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether two AnimatorDirection values are equal. |## enum AnimatorFill

```cangjie
public enum AnimatorFill <: Equatable<AnimatorFill> {
    | None
    | Forwards
    | Backwards
    | Both
    | ...
}
```

**Function:** Specifies whether the animation should return to its initial state after execution. When enabled, the end state of the animation (defined in the last keyframe) will be preserved.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Backwards

```cangjie
Backwards
```

**Function:** Sets the animation to apply the value defined in the first keyframe during the animation-delay period. When animation-direction is Normal or Alternate, it applies the value from the 'from' keyframe; when animation-direction is Reverse or AlternateReverse, it applies the value from the 'to' keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Both

```cangjie
Both
```

**Function:** Sets the animation to follow both forwards and backwards rules, thereby extending animation properties in both directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Forwards

```cangjie
Forwards
```

**Function:** After the animation ends, the target will retain the state at the end of the animation (defined in the last keyframe).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### None

```cangjie
None
```

**Function:** No styles will be applied to the target before or after animation execution.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(AnimatorFill)

```cangjie
public operator func !=(other: AnimatorFill): Bool
```

**Function:** Compares whether two AnimatorFill values are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorFill](#enum-animatorfill) | Yes | - | **Named parameter.** Specifies whether to return to the initial state after animation execution. After execution, the end state of the animation (defined in the last keyframe) will be preserved. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Indicates whether two AnimatorFill values are not equal. |

### func ==(AnimatorFill)

```cangjie
public operator func ==(other: AnimatorFill): Bool
```

**Function:** Compares whether two AnimatorFill values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimatorFill](#enum-animatorfill) | Yes | - | **Named parameter.** Specifies whether to return to the initial state after animation execution. After execution, the end state of the animation (defined in the last keyframe) will be preserved. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Indicates whether two AnimatorFill values are equal. |