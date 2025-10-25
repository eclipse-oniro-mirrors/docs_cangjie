# Image Effects

Configure blur, shadow, spherical effects for components, and set image effects.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func blur(Float64)

```cangjie
public func blur(value: Float64): This
```

**Description:** Sets the blur effect for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Blur radius. |

## func brightness(Float64)

```cangjie
public func brightness(value: Float64): This
```

**Description:** Sets the brightness for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Brightness value. |

## func colorBlend(ResourceColor)

```cangjie
public func colorBlend(value: ResourceColor): This
```

**Description:** Sets the color blend mode for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Color blend value. |

## func contrast(Float64)

```cangjie
public func contrast(value: Float64): This
```

**Description:** Sets the contrast for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Contrast value. |

## func grayscale(Float64)

```cangjie
public func grayscale(value: Float64): This
```

**Description:** Sets the grayscale value for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Inversion value. |

## func hueRotate(Float32)

```cangjie
public func hueRotate(value: Float32): This
```

**Description:** Sets the hue rotation for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float32 | Yes | - | Single-precision floating-point value. |

## func invert(Float64)

```cangjie
public func invert(value: Float64): This
```

**Description:** Sets the color inversion value for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Transparency. |

## func invert(Float64, Float64, Float64, Float64)

```cangjie
public func invert(low!: Float64, high!: Float64, threshold!: Float64, thresholdRange!: Float64): This
```

**Description:** Sets the inversion range and threshold for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| low | Float64 | Yes | - | Low threshold. |
| high | Float64 | Yes | - | High threshold. |
| threshold | Float64 | Yes | - | Threshold. |
| thresholdRange | Float64 | Yes | - | Threshold range. |

## func saturate(Float64)

```cangjie
public func saturate(value: Float64): This
```

**Description:** Sets the saturation for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Sepia tone value. |

## func sepia(Float64)

```cangjie
public func sepia(value: Float64): This
```

**Description:** Sets the sepia tone for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Converts the image to sepia, reducing color saturation to create a warm vintage style. A value of 1 results in full sepia, values ≤ 0 leave the image unchanged, and values > 1 amplify color shifts, making the image brighter with more yellow/red tones (non-standard sepia effect).<br> Value range: [0.0, +∞), recommended range: (0.0, 1.0]. |

## func shadow(Float64, ResourceColor, Float64, Float64)

```cangjie
public func shadow(radius!: Float64, color!: ResourceColor = Color(0x666666), offsetX!: Float64 = 0.0,
    offsetY!: Float64 = 0.0): This
```

**Description:** Sets the shadow for a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| radius | Float64 | Yes | - | Shadow blur radius. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color(0x666666) | Shadow color. |
| offsetX | Float64 | No | 0.0 | Shadow X-axis offset. |
| offsetY | Float64 | No | 0.0 | Shadow Y-axis offset. |