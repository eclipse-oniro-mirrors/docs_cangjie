# Color Gradient

Set the color gradient effect for components.

> **Note:**
>
> - Color gradient is part of the component content and is drawn above the background.
> - Color gradient does not support explicit width/height animations. When performing width/height animations, the color gradient will directly transition to the endpoint.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func linearGradient(?Float64, GradientDirection, Array\<(ResourceColor,Float64)>, Bool)

```cangjie
public func linearGradient(angle!: ?Float64 = None, direction!: GradientDirection = GradientDirection.Bottom,
    colors!: Array<(ResourceColor, Float64)> = [(Color.Transparent, 0.0)], repeating!: Bool = false): This
```

**Function:** Sets a linear gradient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| angle | ?Float64 | No | None | **Named parameter.** The starting angle of the linear gradient. Positive angles are measured clockwise from the 0-degree direction. |
| direction | [GradientDirection](./cj-common-types.md#enum-gradientdirection) | No | GradientDirection.Bottom | **Named parameter.** The direction of the linear gradient. This parameter becomes invalid when angle is set. |
| colors | Array\<([ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor),Float64)> | No | [(Color.Transparent, 0.0)] | **Named parameter.** An array specifying gradient colors and their corresponding percentage positions. Invalid colors will be skipped. |
| repeating | Bool | No | false | **Named parameter.** Repeats the gradient colors. |

## func radialGradient((Length,Length), Length, Array\<(ResourceColor,Float64)>, Bool)

```cangjie
public func radialGradient(center: (Length, Length), radius: Length, colors: Array<(ResourceColor, Float64)>,
    repeating!: Bool = false): This
```

**Function:** Sets a radial gradient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| center | ([Length](../BasicServicesKit/cj-apis-base.md#interface-length),[Length](../BasicServicesKit/cj-apis-base.md#interface-length)) | Yes | - | The center point of the radial gradient, i.e., the coordinates relative to the top-left corner of the current component. |
| radius | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The radius of the radial gradient.<br>Valid range: \[0.0,+∞).<br> **Note:** <br> Values less than 0 will be treated as 0. Default value: 0.0. |
| colors | Array\<([ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor),Float64)> | Yes | - | An array specifying gradient colors and their corresponding percentage positions. Invalid colors will be skipped. |
| repeating | Bool | No | false | **Named parameter.** Repeats the gradient colors. |

## func sweepGradient((Length,Length), Float64, Float64, Float64, Array\<(ResourceColor,Float64)>, Bool)

```cangjie
public func sweepGradient(center: (Length, Length), start!: Float64 = 0.0, end!: Float64 = 0.0,
    rotation!: Float64 = 0.0, colors!: Array<(ResourceColor, Float64)> = [(Color.Transparent, 0.0)],
    repeating!: Bool = false): This
```

**Function:** Sets an angular gradient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| center | ([Length](../BasicServicesKit/cj-apis-base.md#interface-length),[Length](../BasicServicesKit/cj-apis-base.md#interface-length)) | Yes | - | The center point of the angular gradient, i.e., the coordinates relative to the top-left corner of the current component. |
| start | Float64 | No | 0.0 | **Named parameter.** The starting point of the angular gradient. |
| end | Float64 | No | 0.0 | **Named parameter.** The ending point of the angular gradient. |
| rotation | Float64 | No | 0.0 | **Named parameter.** The rotation angle of the angular gradient. |
| colors | Array\<([ResourceColor](./cj-common-types.md),Float64)> | No | [(Color.Transparent, 0.0)] | **Named parameter.** An array specifying gradient colors and their corresponding percentage positions. Invalid colors will be skipped. |
| repeating | Bool | No | false | **Named parameter.** Repeats the gradient colors. |

> **Note:**
>
> When start, end, or rotation is set to a value less than 0, it will be treated as 0; when set to a value greater than 360, it will be treated as 360.