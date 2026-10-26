# Component Transition

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Component transition is primarily configured through the `transition` property to display animation effects during component insertion and deletion. It is mainly used to enhance user experience when child components are inserted or deleted within container components.

> **Note:**
>
> Currently, there are two ways to trigger component transition:
>
> - When a component is inserted or deleted (e.g., due to `if` condition changes or `ForEach` adding/removing components), the transition effects of all newly inserted/deleted components will be triggered recursively.
> - When the [Visibility](./cj-universal-attribute-visibility.md) attribute of a component changes between visible and invisible ([Visibility.Hidden](./cj-common-types.md#enum-visibility) or [Visibility.None](./cj-common-types.md#enum-visibility)), only the transition effect of that component will be triggered. When switching between [Visibility.Visible](./cj-common-types.md#enum-visibility) and [Visibility.None](./cj-common-types.md#enum-visibility), setting directly to Visibility.None will make the component layout size 0, in which case the transition effect cannot be observed. When the visibility property is changed to [Visibility.None](./cj-common-types.md#enum-visibility) during the animation, the component layout becoming 0 is animated, presenting a combined effect of transition and layout animation—a composite of two animations.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func transition(?TransitionEffect)

```cangjie
func transition(value: ?TransitionEffect): T
```

**Function:** Sets the transition effect for component insertion and deletion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[TransitionEffect](#class-transitioneffect) | Yes | - | Sets the transition effect for component insertion display and deletion hide. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Returns the component instance. |

## func transition(?TransitionEffect, ?TransitionFinishCallback)

```cangjie
func transition(value: ?TransitionEffect, onFinish: ?TransitionFinishCallback): T
```

**Function:** Sets the transition effect for component insertion/deletion and the callback after the transition animation ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[TransitionEffect](#class-transitioneffect) | Yes | - | Sets the transition effect for component insertion display and deletion hide. |
| onFinish | ?[TransitionFinishCallback](./cj-common-types.md#type-transitionfinishcallback) | Yes | - | Callback type for the end of component transition animation.<br>When this parameter is `true`, it indicates the callback is for the appearance animation; when `false`, it indicates the callback is for the disappearance animation. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Returns the component instance. |

## class TranslateOptions

```cangjie
public class TranslateOptions {
    public var x: ?Length
    public var y: ?Length
    public var z: ?Length
    public init(x!: ?Length = None, y!: ?Length = None, z!: ?Length = None)
}
```

**Function:** Defines translation options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Length
```

**Function:** Translation distance along the x-axis. For numeric types, the unit is vp, with a range of (-∞, +∞).

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Length
```

**Function:** Translation distance along the y-axis. For numeric types, the unit is vp, with a range of (-∞, +∞).

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: ?Length
```

**Function:** Translation distance along the z-axis. For numeric types, the unit is vp, with a range of (-∞, +∞).

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length, ?Length)

```cangjie
public init(x!: ?Length = None, y!: ?Length = None, z!: ?Length = None)
```

**Function:** Constructor for `TranslateOptions`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Translation distance along the x-axis.<br>Initial value: 0.0.vp. |
| y | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Translation distance along the y-axis.<br>Initial value: 0.0.vp. |
| z | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Translation distance along the z-axis.<br>Initial value: 0.0.vp. |

## class ScaleOptions

```cangjie
public class ScaleOptions {
    public var x: ?Float32
    public var y: ?Float32
    public var z: ?Float32
    public var centerX: ?Length
    public var centerY: ?Length
    public init(x!: ?Float32 = None, y!: ?Float32 = None, z!: ?Float32 = None, centerX!: ?Length = None,
        centerY!: ?Length = None)
}
```

**Function:** Scaling parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Float32
```

**Function:** Scaling ratio along the x-axis.
- x > 1: Component scales up along the x-axis.
- 0 < x < 1: Component scales down along the x-axis.
- x < 0: Component scales in the opposite direction along the x-axis.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Float32
```

**Function:** Scaling ratio along the y-axis.
- y > 1: Component scales up along the y-axis.
- 0 < y < 1: Component scales down along the y-axis.
- y < 0: Component scales in the opposite direction along the y-axis.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: ?Float32
```

**Function:** Scaling ratio along the z-axis.
- z > 1: Component scales up along the z-axis.
- 0 < z < 1: Component scales down along the z-axis.
- z < 0: Component scales in the opposite direction along the z-axis.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerX

```cangjie
public var centerX: ?Length
```

**Function:** X-coordinate of the transformation center point (anchor point). Unit: vp.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerY

```cangjie
public var centerY: ?Length
```

**Function:** Y-coordinate of the transformation center point (anchor point). Unit: vp.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float32, ?Float32, ?Float32, ?Length, ?Length)

```cangjie
public init(x!: ?Float32 = None, y!: ?Float32 = None, z!: ?Float32 = None, centerX!: ?Length = None,
        centerY!: ?Length = None)
```

**Function:** Constructor for `ScaleOptions`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | ?Float32 | No | None | **Named parameter.** Scaling ratio along the x-axis. When x>1, scale up along the x-axis; when 0<x<1, scale down along the x-axis; when x<0, reflect and scale along the x-axis.<br>Initial value: 1.0. |
| y | ?Float32 | No | None | **Named parameter.** Scaling ratio along the y-axis. When y>1, scale up along the y-axis; when 0<y<1, scale down along the y-axis; when y<0, reflect and scale along the y-axis.<br>Initial value: 1.0. |
| z | ?Float32 | No | None | **Named parameter.** Scaling ratio along the z-axis. When z>1, scale up along the z-axis; when 0<z<1, scale down along the z-axis; when z<0, reflect and scale along the z-axis.<br>Initial value: 1.0. |
| centerX | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** X-coordinate of the transformation center point (anchor). For numeric types, unit is vp.<br>Initial value: 50.percent. |
| centerY | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Y-coordinate of the transformation center point (anchor). For numeric types, unit is vp.<br>Initial value: 50.percent. |

## class RotateOptions

```cangjie
public class RotateOptions {
    public var x: ?Float32
    public var y: ?Float32
    public var z: ?Float32
    public var centerX: ?Length
    public var centerY: ?Length
    public var centerZ: ?Length
    public var perspective: ?Float32
    public var angle: ?Float32
    public init(angle: ?Float32, x!: ?Float32 = None, y!: ?Float32 = None, z!: ?Float32 = None, centerX!: ?Length = None,
        centerY!: ?Length = None, centerZ!: ?Length = None, perspective!: ?Float32 = None)
}
```

**Function:** Rotation parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var angle

```cangjie
public var angle: ?Float32
```

**Function:** Rotation angle. A positive value indicates clockwise rotation relative to the rotation axis direction; a negative value indicates counterclockwise rotation.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Float32
```

**Function:** X-coordinate of the rotation axis vector.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Float32
```

**Function:** Y-coordinate of the rotation axis vector.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: ?Float32
```

**Function:** Z-coordinate of the rotation axis vector.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerX

```cangjie
public var centerX: ?Length
```

**Function:** X-coordinate of the transformation center point. Represents the x-coordinate of the component's transformation center point (i.e., anchor point).

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerY

```cangjie
public var centerY: ?Length
```

**Function:** Y-coordinate of the transformation center point. Represents the y-coordinate of the component's transformation center point (i.e., anchor point).

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerZ

```cangjie
public var centerZ: ?Length
```

**Function:** Z-axis anchor point, i.e., the z-component of the 3D rotation center point.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var perspective

```cangjie
public var perspective: ?Float32
```

**Function:** Z-coordinate of the camera position. The value represents the viewing distance, i.e., the distance from the camera to the z=0 plane. The sign determines the camera's viewing direction. When `perspective=0`, the system automatically calculates an appropriate camera z-position (negative value). The rotation axis and center point are based on the coordinate system, which remains fixed when the component moves.

**Type:** ?Float32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float32, ?Float32, ?Float32, ?Length, ?Length, ?Length, ?Float32)

```cangjie
public init(angle: ?Float32, x!: ?Float32 = None, y!: ?Float32 = None, z!: ?Float32 = None, centerX!: ?Length = None,
        centerY!: ?Length = None, centerZ!: ?Length = None, perspective!: ?Float32 = None)
```

**Function:** Constructor for `RotateOptions`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| angle | ?Float32 | Yes | - | Angle parameter. |
| x | ?Float32 | No | None | **Named parameter.** X-coordinate of the rotation axis vector. Initial value: 0.0 |
| y | ?Float32 | No | None | **Named parameter.** Y-coordinate of the rotation axis vector. Initial value: 0.0 |
| z | ?Float32 | No | None | **Named parameter.** Z-coordinate of the rotation axis vector. Initial value: 0.0 |
| centerX | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** X-coordinate of the transformation center point (anchor). For numeric types, unit is vp.<br>Initial value: 50.percent. |
| centerY | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Y-coordinate of the transformation center point (anchor). For numeric types, unit is vp.<br>Initial value: 50.percent. |
| centerZ | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Z-axis anchor point, i.e., the z-component of the 3D rotation center point. For numeric types, unit is vp.<br>Initial value: 0. |
| perspective | ?Float32 | No | None | **Named parameter.** Distance from the user to the z=0 plane. The axis and rotation center are based on the coordinate system, which remains fixed when the component moves.<br>Initial value: 0.0.<br>Unit: px. |

## class TransitionEffect

```cangjie
public class TransitionEffect {
    public static let IDENTITY: TransitionEffect
    public static let OPACITY: TransitionEffect = TransitionEffect.opacity(0.0)
    public static let SLIDE: TransitionEffect = TransitionEffect.asymmetric(TransitionEffect.move(TransitionEdge.Start),
        TransitionEffect.move(TransitionEdge.End))
    public static let SLIDE_SWITCH: TransitionEffect
}
```

**Function:** Specifies the type of transition effect in function form.

> **Note:**
>
> - Multiple transition effects can be combined using the `combine` function. The `animation` parameter can be specified separately for each effect, and the animation parameters of the preceding effect also apply to the subsequent effect. For example, `TransitionEffect.OPACITY.animation(AnimateParam(duration: 1000)).combine(TransitionEffect.translate(TranslateOptions(x:100)))` means the animation parameters with a duration of 1000ms apply to both `OPACITY` and `translate`.
>
> - The order of precedence for animation parameters is: the `animation` parameter of this TransitionEffect > the `animation` parameter of the preceding TransitionEffect > the animation parameters in the `animateTo` that triggers the component appearance/disappearance.
>
> - If the transition animation is not triggered by `animateTo` and there is no `animation` parameter in TransitionEffect, the component will appear or disappear directly.
>
> - If the property values specified in TransitionEffect are the same as the default values, that property will not produce a transition animation. For example, `TransitionEffect.opacity(1.0).animation(duration:1000)` — since the default opacity is also 1.0, no opacity animation is produced and the component appears or disappears directly.
>
> - For more details on scale and rotate effects, see [Transform](./cj-universal-attribute-transform.md).
>
> - If a component's attachment to or detachment from the tree or its visibility change is triggered within an animation scope ([animateTo](./cj-apis-uicontext-uicontext.md#func-animatetoanimateparam-voidcallback), [animation](./cj-animation-animation.md#func-animationanimateparam)) and the root component has no transition configured, a default opacity transition (TransitionEffect.OPACITY) will be applied to that component, with animation parameters following the surrounding animation environment. To disable this and make the component appear or disappear directly, explicitly configure TransitionEffect.IDENTITY.
>
> - When a disappear transition is triggered by removing an entire subtree, to see the full disappear transition, ensure the root component of the removed subtree has sufficient disappear transition duration; see Example 3.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let IDENTITY

```cangjie
public static let IDENTITY: TransitionEffect
```

**Function:** Disables the transition effect.

**Type:** [TransitionEffect](#class-transitioneffect)

**Read/Write:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let OPACITY

```cangjie
public static let OPACITY: TransitionEffect = TransitionEffect.opacity(0.0)
```

**Function:** Adds an opacity transition effect to the component: opacity goes from 0 to 1 on appearance and from 1 to 0 on disappearance, equivalent to `TransitionEffect.opacity(0.0)`.

**Type:** [TransitionEffect](#class-transitioneffect)

**Read/Write:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let SLIDE

```cangjie
public static let SLIDE: TransitionEffect = TransitionEffect.asymmetric(TransitionEffect.move(TransitionEdge.Start),
        TransitionEffect.move(TransitionEdge.End))
```

**Function:** Equivalent to `TransitionEffect.asymmetric(TransitionEffect.move(TransitionEdge.Start), TransitionEffect.move(TransitionEdge.End))`. Slides in from the Start edge and slides out from the End edge. In LTR mode: slides in from the left and out from the right; in RTL mode: slides in from the right and out from the left.

**Type:** [TransitionEffect](#class-transitioneffect)

**Read/Write:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let SLIDE_SWITCH

```cangjie
public static let SLIDE_SWITCH: TransitionEffect
```

**Function:** Specifies a transition effect where the component appears by sliding in from the right with first shrinking and then enlarging, and disappears by sliding out to the left with first shrinking and then enlarging. It comes with built-in animation parameters, which can also be overridden. The default animation duration is 600ms, with the animation curve set to `cubicBezierCurve(0.24, 0.0, 0.50, 1.0)` and the minimum scale factor set to 0.8.

**Type:** [TransitionEffect](#class-transitioneffect)

**Read/Write:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static func opacity(Float64)

```cangjie
public static func opacity(alpha: Float64): TransitionEffect
```

**Function:** Sets the opacity effect during component transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| alpha | Float64 | Yes | - | Sets the opacity effect during component transition, which is the value at the start of insertion and the end of deletion. Range: [0.0, 1.0].<br> **Note:** <br>Invalid values less than 0.0 are treated as 0.0, and values greater than 1.0 are treated as 1.0 |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### static func translate(TranslateOptions)

```cangjie
public static func translate(options: TranslateOptions): TransitionEffect
```

**Function:** Sets the translation effect during component transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [TranslateOptions](#class-translateoptions) | Yes | - | Sets the translation effect during component transition, which is the value at the start of insertion and the end of deletion. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### static func scale(?ScaleOptions)

```cangjie
public static func scale(options: ?ScaleOptions): TransitionEffect
```

**Function:** Sets the scaling effect during component transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | ?[ScaleOptions](#class-scaleoptions) | Yes | - | Scaling effect during component transition, which is the value at the start of insertion and the end of deletion. The set scale value is applied on top of the component's current scale property. For example, if the component's current scale is 0.8 and the transition scale is set to 0.5, the component's entrance animation will run from a scale of 0.4. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### static func rotate(?RotateOptions)

```cangjie
public static func rotate(options: ?RotateOptions): TransitionEffect
```

**Function:** Sets the rotation effect during component transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | ?[RotateOptions](#class-rotateoptions) | Yes | - | Sets the rotation effect during component transition, which is the value at the start of insertion and the end of deletion. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### static func move(TransitionEdge)

```cangjie
public static func move(edge: TransitionEdge): TransitionEffect
```

**Function:** Specifies the effect of sliding in and out from the screen edge during component transition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| edge | [TransitionEdge](#enum-transitionedge) | Yes | - | Specifies the effect of sliding in and out from the screen edge during component transition, which is essentially a translation effect, representing the value at the start of insertion and the end of deletion. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### static func asymmetric(TransitionEffect, TransitionEffect)

```cangjie
public static func asymmetric(appear: TransitionEffect, disappear: TransitionEffect): TransitionEffect
```

**Function:** Used to specify asymmetric transition effects.

> **Note:**
>
> If `TransitionEffect` is not constructed using the `asymmetric` function, it means the effect applies to both the appearance and disappearance of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| appear | [TransitionEffect](#class-transitioneffect) | Yes | - | Specifies the transition effect for appearance.<br>If TransitionEffect is not constructed using the asymmetric function, the effect applies to both component appearance and disappearance. |
| disappear | [TransitionEffect](#class-transitioneffect) | Yes | - | Specifies the transition effect for disappearance.<br>If TransitionEffect is not constructed using the asymmetric function, the effect applies to both component appearance and disappearance. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### func animation(?AnimateParam)

```cangjie
public func animation(param: ?AnimateParam): TransitionEffect
```

**Function:** Specifies the animation parameters for this `TransitionEffect`.

> **Note:**
>
> These parameters are only used to specify animation settings. The `onFinish` callback in `AnimateParam` does not take effect. If `TransitionEffect` is combined using `combine`, the animation parameters of the preceding `TransitionEffect` also apply to the subsequent one.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| param | ?[AnimateParam](./cj-common-types.md#class-animateparam) | Yes | - | Animation effect parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

### func combine(TransitionEffect)

```cangjie
public func combine(transitionEffect: TransitionEffect): TransitionEffect
```

**Function:** Used to chain `TransitionEffect` combinations to form a `TransitionEffect` that includes multiple transition effects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| transitionEffect | [TransitionEffect](#class-transitioneffect) | Yes | - | The component transition effect to be chained. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TransitionEffect](#class-transitioneffect) | Returns the transition effect. |

## enum TransitionEdge

```cangjie
public enum TransitionEdge <: Equatable<TransitionEdge> {
    | Top
    | Bottom
    | Start
    | End
    | ...
}
```

**Function:** Defines edge objects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TransitionEdge](#enum-transitionedge)>

### Top

```cangjie
Top
```

**Function:** The top edge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** The bottom edge of the window.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** The starting edge of the window, which is the left edge for left-to-right scripts and the right edge for right-to-left scripts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** The ending edge of the window, which is the right edge for left-to-right scripts and the left edge for right-to-left scripts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(TransitionEdge)

```cangjie
public operator func !=(other: TransitionEdge): Bool
```

**Function:** Compares whether two enum values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TransitionEdge](#enum-transitionedge) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are not equal, otherwise returns `false`. |

### operator func ==(TransitionEdge)

```cangjie
public operator func ==(other: TransitionEdge): Bool
```

**Function:** Compares whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TransitionEdge](#enum-transitionedge) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

## Example Code

### Example Code 1 (Using the Same Interface for Image Appearance and Disappearance)

This example demonstrates how to use the same TransitionEffect to achieve both the appearance and disappearance of an image, where these two processes are inverses of each other.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class EntryView {
    @State var flag = true
    @State var show = "show"
    func build() {
        Column {
            Button(this.show)
                .onClick({
                    evt =>
                    Hilog.info(0, "cangjie", "Hello Cangjie")
                    if (this.flag) {
                        this.show = "hide"
                    } else {
                        this.show = "show"
                    }
                    this.flag = !this.flag
                })
                .width(800.px)
                .height(400.px)

            if (this.flag) {
                Button("abc")
                    .width(800.px)
                    .height(400.px)
                    .transition(
                        TransitionEffect
                            .OPACITY
                            .animation(AnimateParam(duration: 2000, curve: Curve.Ease))
                            .combine(TransitionEffect.rotate(RotateOptions(180.0, z: 1.0))))
            }
        }
    }
}
```

![transition](figures/transition_api.gif)

### Example Code 2 (Using Different Interfaces for Image Appearance and Disappearance)

This example demonstrates how to use different TransitionEffects to achieve the appearance and disappearance of an image.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class EntryView {
    @State var flag = true
    @State var show = "show"
    func build() {
        Column {
            Button(this.show)
                .onClick({
                    evt =>
                    Hilog.info(0, "cangjie", "Hello Cangjie")
                    if (this.flag) {
                        this.show = "hide"
                    } else {
                        this.show = "show"
                    }
                    this.flag = !this.flag
                })
                .width(800.px)
                .height(400.px)
                .margin(left: 200.px, top: 100.px)

            if (this.flag) {
                Button("abc")
                    .width(800.px)
                    .height(400.px)
                    .margin(left: 200.px)
                    .transition(
                        TransitionEffect
                            .OPACITY
                            .animation(AnimateParam(duration: 2000, curve: Curve.Ease))
                            .combine(TransitionEffect.rotate(RotateOptions(180.0, z: 1.0))))

                Button("abc")
                    .width(800.px)
                    .height(400.px)
                    .margin(left: 200.px)
                    .transition(
                        TransitionEffect
                            .asymmetric(
                                TransitionEffect.scale(ScaleOptions()),
                                TransitionEffect.IDENTITY
                            )
                            .animation(AnimateParam(duration: 2000, curve: Curve.Ease)))
            }
        }
    }
}
```

![transition2](./figures/transition2_api.gif)

### Example Code 3 (Setting Parent and Child Components as Transitions)

This example demonstrates how to achieve image appearance and disappearance by configuring transitions for both parent and child components.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var flag = true
    @State var show = "show"
    func build() {
        Column {
            Button(this.show)
                .onClick({
                    evt =>
                    Hilog.info(0, "cangjie", "Hello Cangjie")
                    if (this.flag) {
                        this.show = "hide"
                    } else {
                        this.show = "show"
                    }
                    this.flag = !this.flag
                })
                .width(800.px)
                .height(400.px)
                .margin(left:50, top: 50)

            if (this.flag) {
                Column() {
                    Row() {
                        Image(@r(app.media.startIcon))
                            .width(150)
                            .height(150)
                            .id("image1")
                            .transition(TransitionEffect
                                .OPACITY
                                .animation(AnimateParam(duration: 2000)))
                    }
                    Image(@r(app.media.startIcon))
                        .width(150)
                        .height(150)
                        .id("image2")
                        .transition(TransitionEffect
                            .OPACITY
                            .animation(AnimateParam(duration: 1000)))
                }.transition(TransitionEffect
                    .OPACITY
                    .animation(AnimateParam(duration: 1000)))
                    .margin(left:50)
            }
        }
    }
}
```

![transition3](figures/transition3.gif)