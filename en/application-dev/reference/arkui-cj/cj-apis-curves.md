# ohos.curves (Interpolation Calculation)

This module provides the functionality to set animation interpolation curves, used for constructing step curve objects, cubic Bézier curve objects, and spring curve objects.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Curves

```cangjie
public class Curves {}
```

**Description:** Animation interpolation curve types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### static func cubicBezierCurve(Float32, Float32, Float32, Float32)

```cangjie
public static func cubicBezierCurve(x1: Float32, y1: Float32, x2: Float32, y2: Float32): ICurve
```

**Description:** Constructs a cubic Bézier curve object. The curve values must be within the range [0, 1].

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x1 | Float32 | Yes | - | Determines the x-coordinate of the first point of the Bézier curve.<br>Range: [0, 1]<br>**Note:**<br>Values less than 0 are treated as 0; values greater than 1 are treated as 1. |
| y1 | Float32 | Yes | - | Determines the y-coordinate of the first point of the Bézier curve.<br>Range: (-∞, +∞). |
| x2 | Float32 | Yes | - | Determines the x-coordinate of the second point of the Bézier curve.<br>Range: [0, 1].<br>**Note:**<br>Values less than 0 are treated as 0; values greater than 1 are treated as 1. |
| y2 | Float32 | Yes | - | Determines the y-coordinate of the second point of the Bézier curve.<br>Range: (-∞, +∞). |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve. |

### static func customCurve((Float32) -> Float32)

```cangjie
public static func customCurve(interpolate: (Float32) -> Float32): ICurve
```

**Description:** Constructs a custom curve object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| interpolate | (Float32)->Float32 | Yes | - | User-defined interpolation callback function.<br>The input x value for interpolation at the start of the animation.<br>Range: [0, 1].<br>The return value is the y value of the curve.<br>Range: [0, 1].<br>**Note:**<br>When fraction equals 0, a return value of 0 corresponds to the animation start point. A non-zero return value will cause a jump effect at the start. When fraction equals 1, a return value of 1 corresponds to the animation end point. A non-1 return value will cause the animation's final value to deviate from the state variable's value, resulting in a jump effect to the state variable's value. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve. |

### static func initCurve(Curve)

```cangjie
public static func initCurve(curve!: Curve = Curve.Linear): ICurve
```

**Description:** Initialization function for interpolation curves, creating an interpolation curve object based on the input parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| curve | [Curve](./cj-common-types.md#enum-curve) | No | Curve.Linear | **Named parameter.** The type of curve. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve. |

### static func interpolatingSpring(Float32, Float32, Float32, Float32)

```cangjie
public static func interpolatingSpring(velocity: Float32, mass: Float32, stiffness: Float32, damping: Float32): ICurve
```

**Description:** Constructs an interpolator spring curve object, generating an animation curve from 0 to 1. The actual animation value is calculated based on the curve interpolation. The animation duration is determined by the curve parameters and is not controlled by the duration parameter in animation or animateTo.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| velocity | Float32 | Yes | - | Initial velocity. A parameter representing external influences on the elastic effect, ensuring a smooth transition from the previous motion state to the elastic effect. This is a normalized velocity equal to the actual velocity at the start of the animation divided by the change in the animation property value.<br>Range: (-∞, +∞). |
| mass | Float32 | Yes | - | Mass. The object subjected to forces in the elastic system, affecting the system's inertia. Larger mass results in greater oscillation amplitude and slower return to equilibrium.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |
| stiffness | Float32 | Yes | - | Stiffness. Represents the object's resistance to deformation under applied force. Higher stiffness results in faster return to equilibrium.<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |
| damping | Float32 | Yes | - | Damping. Describes the oscillation and decay of the system after disturbance. Higher damping results in fewer oscillations and smaller amplitudes.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve.<br>**Note:** The elastic animation curve is a physical curve. The duration parameter in [animation](./cj-animation-animation.md), [animateTo](./cj-animation-animateto.md), or [pageTransition](./cj-animation-pagetransition.md) does not take effect. The animation duration depends on the interpolatingSpring curve parameters. Time cannot be normalized, so interpolation cannot be obtained via the curve's [interpolate](#func-interpolatefloat32) function. |

### static func responsiveSpringMotion(Float32, Float32, Float32)

```cangjie
public static func responsiveSpringMotion(response!: Float32 = 0.15, dampingFraction!: Float32 = 0.86,
    overlapDuration!: Float32 = 0.25): ICurve
```

**Description:** Constructs a responsive spring motion curve object, a special case of [springMotion](#static-func-springmotionfloat32-float32-float32) with different default parameters. It can be used interchangeably with [springMotion](#static-func-springmotionfloat32-float32-float32).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| response | Float32 | No | 0.15 | **Named parameter.** Same as response in springMotion.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as the default value 0.15. |
| dampingFraction | Float32 | No | 0.86 | **Named parameter.** Same as dampingFraction in springMotion.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as the default value 0.86. |
| overlapDuration | Float32 | No | 0.25 | **Named parameter.** Same as overlapDuration in springMotion.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>The responsive spring motion curve is a special case of springMotion with different default parameters. For custom elastic curves, use springMotion. For responsive animations, use the default parameters of responsiveSpringMotion.<br>The duration parameter in [animation](./cj-animation-animation.md), [animateTo](./cj-animation-animateto.md), or [pageTransition](./cj-animation-pagetransition.md) does not take effect. The animation duration depends on the responsiveSpringMotion curve parameters and previous velocity. Interpolation cannot be obtained via the curve's [interpolate](#func-interpolatefloat32) function. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The curve object.<br>**Note:**<br>1. The responsive spring motion curve is a special case of springMotion with different default parameters. For custom elastic curves, use springMotion; for responsive animations, use the default parameters of responsiveSpringMotion.<br>2. The duration parameter in [animation](./cj-animation-animation.md), [animateTo](./cj-animation-animateto.md), or [pageTransition](./cj-animation-pagetransition.md) does not take effect. The animation duration depends on the responsiveSpringMotion curve parameters and previous velocity. Interpolation cannot be obtained via the curve's [interpolate](#func-interpolatefloat32) function. |

### static func springCurve(Float32, Float32, Float32, Float32)

```cangjie
public static func springCurve(velocity: Float32, mass: Float32, stiffness: Float32, damping: Float32): ICurve
```

**Description:** Constructs a spring curve object. The curve shape is determined by the spring parameters, and the animation duration is controlled by the duration parameter in animation or animateTo.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| velocity | Float32 | Yes | - | Initial velocity. A parameter representing external influences on the elastic effect, ensuring a smooth transition from the previous motion state to the elastic effect. This is a normalized velocity equal to the actual velocity at the start of the animation divided by the change in the animation property value.<br>Range: (-∞, +∞). |
| mass | Float32 | Yes | - | Mass. The object subjected to forces in the elastic system, affecting the system's inertia. Larger mass results in greater oscillation amplitude and slower return to equilibrium.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |
| stiffness | Float32 | Yes | - | Stiffness. Represents the object's resistance to deformation under applied force. Higher stiffness results in faster return to equilibrium.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |
| damping | Float32 | Yes | - | Damping. Describes the oscillation and decay of the system after disturbance. Higher damping results in fewer oscillations and smaller amplitudes.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as 1. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve. |

### static func springMotion(Float32, Float32, Float32)

```cangjie
public static func springMotion(response!: Float32 = 0.55, dampingFraction!: Float32 = 0.825,
    overlapDuration!: Float32 = 0.0): ICurve
```

**Description:** Constructs an elastic animation curve object. If multiple elastic animations are applied to the same property of the same object, each animation will replace the previous one and inherit its velocity.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| response | Float32 | No | 0.55 | **Named parameter.** The natural oscillation period of the spring, determining the speed of reset.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as the default value 0.55. |
| dampingFraction | Float32 | No | 0.825 | **Named parameter.** Damping coefficient.<br>0 indicates no damping, resulting in continuous oscillation;<br>Values greater than 0 and less than 1 indicate underdamping, causing overshoot;<br>1 indicates critical damping;<br>Values greater than 1 indicate overdamping, causing gradual approach to the target value.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>Values less than or equal to 0 are treated as the default value 0.825. |
| overlapDuration | Float32 | No | 0.0 | **Named parameter.** Transition duration for elastic animations. When animation inheritance occurs, if the response parameters of consecutive elastic animations differ, the response parameter will smoothly transition over the overlapDuration.<br>Unit: seconds.<br>Range: (0, +∞).<br>**Note:**<br>Values less than 0 are treated as the default value 0.<br>The elastic animation curve is a physical curve. The duration parameter in [animation](./cj-animation-animation.md), [animateTo](./cj-animation-animateto.md), or [pageTransition](./cj-animation-pagetransition.md) does not take effect. The animation duration depends on the springMotion curve parameters and previous velocity. Time cannot be normalized, so interpolation cannot be obtained via the curve's [interpolate](#func-interpolatefloat32) function. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve.<br>**Note:** The elastic animation curve is a physical curve. The duration parameter in [animation](./cj-animation-animation.md), [animateTo](./cj-animation-animateto.md), or [pageTransition](./cj-animation-pagetransition.md) does not take effect. The animation duration depends on the interpolatingSpring curve parameters. Time cannot be normalized, so interpolation cannot be obtained via the curve's [interpolate](#func-interpolatefloat32) function. |

### static func stepsCurve(Int32, Bool)

```cangjie
public static func stepsCurve(count: Int32, end: Bool): ICurve
```

**Description:** Constructs a step curve object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| count | Int32 | Yes | - | The number of steps, which must be a positive integer.<br>Range: [1, +∞).<br>**Note:**<br>Values less than 1 are treated as 1. |
| end | Bool | Yes | - | Determines whether the step change occurs at the start or end of each interval.<br>- true: Step change occurs at the end.<br>- false: Step change occurs at the start. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ICurve](#class-icurve) | The interpolation object of the curve. |

## class ICurve

```cangjie
public class ICurve {}
```

**Description:** The type of curve object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func interpolate(Float32)

```cangjie
public func interpolate(fraction: Float32): Float32
```

**Description:** The interpolation calculation function of the interpolation curve, which returns the current interpolation value based on the input normalized time parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fraction | Float32 | Yes | - | The current normalized time parameter.<br>Range: [0, 1].<br>**Note:**<br>Values less than 0 are treated as 0; values greater than 1 are treated as 1. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float32 | Returns the curve interpolation value corresponding to the normalized time point. |

## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

let animateOpt1 = AnimateParam(
    duration: 1200,
    curve: Curve.EaseOut
)

@Entry
@Component
class EntryView {
    @State var widthSize: Float64 = 200.0
    @State var heightSize: Float64 = 200.0
    func build() {
        Column {
            Column()
                .margin(top: 100)
                .width(this.widthSize)
                .height(this.heightSize)
                .backgroundColor(Color.Red)
                .onClick(
                    {
                        evt =>
                        let curve = Curves.cubicBezierCurve(0.25, 0.1, 0.25, 1.0)
                        this.widthSize = Float64(curve.interpolate(0.5)) * this.widthSize
                        this.heightSize = Float64(curve.interpolate(0.5)) * this.heightSize
                   