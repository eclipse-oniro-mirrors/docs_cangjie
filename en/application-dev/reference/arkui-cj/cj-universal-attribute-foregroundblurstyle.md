# Component Content Blur

Adds a content blur effect to the current component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func foregroundBlurStyle(BlurStyle)

```cangjie
public func foregroundBlurStyle(value: BlurStyle): This
```

**Function:** Provides content blur capability for the current component using default blur options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | Yes | - | Content blur style. |

## func foregroundBlurStyle(BlurStyle, ForegroundBlurStyleOptions)

```cangjie
public func foregroundBlurStyle(value: BlurStyle, options: ForegroundBlurStyleOptions): This
```

**Function:** Provides content blur capability for the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [BlurStyle](./cj-universal-attribute-background.md#enum-blurstyle) | Yes | - | Content blur style. |
| options | [ForegroundBlurStyleOptions](#class-foregroundblurstyleoptions) | Yes | - | Content blur options. |

## Basic Type Definitions

### class BlurOptions

```cangjie
public class BlurOptions {
    public var grayscale: VArray<Float32, $2>
    public init(grayscale: VArray<Float32, $2>)
}
```

**Function:** Grayscale blur parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var grayscale

```cangjie
public var grayscale: VArray<Float32, $2>
```

**Function:** Grayscale blur parameters, with value range [0, 127].

**Type:** VArray\<Float32,$2>

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(VArray\<Float32,$2>)

```cangjie
public init(grayscale: VArray<Float32, $2>)
```

**Function:** Constructs a BlurOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| grayscale | VArray\<Float32,$2> | Yes | - | Grayscale blur parameters, with value range [0, 127]. |

### class ForegroundBlurStyleOptions

```cangjie
public class ForegroundBlurStyleOptions {
    public var colorMode: ThemeColorMode = ThemeColorMode.System
    public var adaptiveColor: AdaptiveColor = AdaptiveColor.Default
    public var blurOptions: BlurOptions = BlurOptions([0.0, 0.0])
    public var scale: Float32 = 1.0
    public init(
        colorMode!: ThemeColorMode = ThemeColorMode.System,
        adaptiveColor!: AdaptiveColor = AdaptiveColor.Default,
        blurOptions!: BlurOptions = BlurOptions([0.0, 0.0]),
        scale!: Float32 = 1.0
    )
}
```

**Function:** Content blur options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var adaptiveColor

```cangjie
public var adaptiveColor: AdaptiveColor = AdaptiveColor.Default
```

**Function:** Color sampling mode used for content blur effect.

**Type:** [AdaptiveColor](cj-common-types.md#enum-adaptivecolor)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var blurOptions

```cangjie
public var blurOptions: BlurOptions = BlurOptions([0.0, 0.0])
```

**Function:** Grayscale blur parameters.

**Type:** [BlurOptions](#class-bluroptions)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var colorMode

```cangjie
public var colorMode: ThemeColorMode = ThemeColorMode.System
```

**Function:** Light/dark color mode used for content blur effect.

**Type:** [ThemeColorMode](cj-common-types.md#enum-themecolormode)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var scale

```cangjie
public var scale: Float32 = 1.0
```

**Function:** Intensity of content blur effect. Value range: [0.0, 1.0].

**Type:** Float32

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(ThemeColorMode, AdaptiveColor, BlurOptions, Float32)

```cangjie
public init(
    colorMode!: ThemeColorMode = ThemeColorMode.System,
    adaptiveColor!: AdaptiveColor = AdaptiveColor.Default,
    blurOptions!: BlurOptions = BlurOptions([0.0, 0.0]),
    scale!: Float32 = 1.0
)
```

**Function:** Constructs a ForegroundBlurStyleOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| colorMode | [ThemeColorMode](cj-common-types.md#enum-themecolormode) | No | ThemeColorMode.System | Light/dark color mode used for content blur effect. |
| adaptiveColor | [AdaptiveColor](cj-common-types.md#enum-adaptivecolor) | No | AdaptiveColor.Default | Color sampling mode used for content blur effect. |
| blurOptions | [BlurOptions](#class-bluroptions) | No | BlurOptions([0.0, 0.0]) | Grayscale blur parameters. |
| scale | Float32 | No | 1.0 | Intensity of content blur effect.<br>Value range: [0.0, 1.0]. |