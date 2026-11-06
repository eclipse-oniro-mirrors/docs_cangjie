# ohos.graphics.color_space_manager (Color Management)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides fundamental capabilities for managing abstract color gamut objects, including the creation of color gamut objects and retrieval of basic color gamut properties.

## Importing the Module

```cangjie
import kit.ArkGraphics2D.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## func create(ColorSpace)

```cangjie
public func create(colorSpaceName: ColorSpace): ColorSpaceManager
```

**Function:** Creates a standard color gamut object.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| colorSpaceName | [ColorSpace](#enum-colorspace) | Yes | - | Standard color gamut type enumeration value. UNKNOWN and CUSTOM cannot be used to directly create color gamut objects. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ColorSpaceManager](#class-colorspacemanager) | Returns the instance of the currently created color gamut object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Color Management Error Codes](./cj-errorcode-colorspace-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 18600001 | The parameter value is abnormal. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let colorSpaceManager = create(ColorSpace.Srgb)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func create(ColorSpacePrimaries, Float32)

```cangjie
public func create(primaries: ColorSpacePrimaries, gamma: Float32): ColorSpaceManager
```

**Function:** Creates a user-defined color gamut object.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| primaries | [ColorSpacePrimaries](#class-colorspaceprimaries) | Yes | - | Standard color gamut primaries. |
| gamma | Float32 | Yes | - | Color gamut gamma value. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ColorSpaceManager](#class-colorspacemanager) | Returns the instance of the currently created color gamut object. The color gamut type is defined as [ColorSpace.CUSTOM](#custom). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Color Management Error Codes](./cj-errorcode-colorspace-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 18600001 | The parameter value is abnormal. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let primaries = ColorSpacePrimaries(
        0.1,
        0.1,
        0.2,
        0.2,
        0.3,
        0.3,
        0.4,
        0.4
    )
    let gamma = 2.2f32
    let colorSpaceManager = create(primaries, gamma)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class ColorSpaceManager

```cangjie
public class ColorSpaceManager {}
```

**Function:** Represents the current color gamut object instance.

> **Note:**
>
> First use [create()](#func-createcolorspace) to obtain a ColorSpaceManager instance, then call the corresponding methods through this instance.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### func getColorSpaceName()

```cangjie
public func getColorSpaceName(): ColorSpace
```

**Function:** Retrieves the color gamut type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ColorSpace](#enum-colorspace) | Returns the color gamut type enumeration value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Color Management Error Codes](./cj-errorcode-colorspace-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 18600001 | The parameter value is abnormal. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let colorSpaceManagerInstance = create(ColorSpace.Srgb)
    let colorSpace: ColorSpace = colorSpaceManagerInstance.getColorSpaceName()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getGamma()

```cangjie
public func getGamma(): Float32
```

**Function:** Retrieves the color gamut gamma value.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Float32 | Returns the color gamut gamma value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Color Management Error Codes](./cj-errorcode-colorspace-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 18600001 | The parameter value is abnormal. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let colorSpaceManagerInstance = create(Srgb)
    let colorSpace = colorSpaceManagerInstance.getGamma()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getWhitePoint()

```cangjie
public func getWhitePoint(): Array<Float32>
```

**Function:** Retrieves the color gamut white point value.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Float32> | Returns the color gamut white point value [x, y]. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Color Management Error Codes](./cj-errorcode-colorspace-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 18600001 | The parameter value is abnormal. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let colorSpaceManagerInstance = create(Srgb)
    let colorSpace = colorSpaceManagerInstance.getWhitePoint()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class ColorSpacePrimaries

```cangjie
public class ColorSpacePrimaries {
    public var redX: Float32
    public var redY: Float32
    public var greenX: Float32
    public var greenY: Float32
    public var blueX: Float32
    public var blueY: Float32
    public var whitePointX: Float32
    public var whitePointY: Float32
    public init(redX: Float32, redY: Float32, greenX: Float32, greenY: Float32, blueX: Float32, blueY: Float32, whitePointX: Float32, whitePointY: Float32)
}
```

**Function:** Represents the standard color gamut primaries (red, green, blue) and white, using (x, y) coordinates to denote their positions in the CIE XYZ color space.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var blueX

```cangjie
public var blueX: Float32
```

**Function:** The x-coordinate value of standard blue in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var blueY

```cangjie
public var blueY: Float32
```

**Function:** The y-coordinate value of standard blue in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var greenX

```cangjie
public var greenX: Float32
```

**Function:** The x-coordinate value of standard green in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var greenY

```cangjie
public var greenY: Float32
```

**Function:** The y-coordinate value of standard green in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var redX

```cangjie
public var redX: Float32
```

**Function:** The x-coordinate value of standard red in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var redY

```cangjie
public var redY: Float32
```

**Function:** The y-coordinate value of standard red in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var whitePointX

```cangjie
public var whitePointX: Float32
```

**Function:** The x-coordinate value of standard white in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### var whitePointY

```cangjie
public var whitePointY: Float32
```

**Function:** The y-coordinate value of standard white in the color space.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### init(Float32, Float32, Float32, Float32, Float32, Float32, Float32, Float32)

```cangjie
public init(redX: Float32, redY: Float32, greenX: Float32, greenY: Float32, blueX: Float32, blueY: Float32, whitePointX: Float32, whitePointY: Float32)
```

**Function:** The primary constructor for ColorSpacePrimaries.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| redX | Float32 | Yes | - | Named parameter. The x-coordinate value of standard red in the color space. |
| redY | Float32 | Yes | - | Named parameter. The y-coordinate value of standard red in the color space. |
| greenX | Float32 | Yes | - | Named parameter. The x-coordinate value of standard green in the color space. |
| greenY | Float32 | Yes | - | Named parameter. The y-coordinate value of standard green in the color space. |
| blueX | Float32 | Yes | - | Named parameter. The x-coordinate value of standard blue in the color space. |
| blueY | Float32 | Yes | - | Named parameter. The y-coordinate value of standard blue in the color space. |
| whitePointX | Float32 | Yes | - | Named parameter. The x-coordinate value of standard white in the color space. |
| whitePointY | Float32 | Yes | - | Named parameter. The y-coordinate value of standard white in the color space. |## enum ColorSpace

```cangjie
public enum ColorSpace <: Equatable<ColorSpace> & ToString {
    | Unknown
    | AdobeRgb1998
    | DciP3
    | DisplayP3
    | Srgb
    | Custom
    | Bt709
    | Bt601Ebu
    | Bt601SmpteC
    | Bt2020Hlg
    | Bt2020Pq
    | P3Hlg
    | P3Pq
    | AdobeRgb1998Limit
    | DisplayP3Limit
    | SrgbLimit
    | Bt709Limit
    | Bt601EbuLimit
    | Bt601SmpteCLimit
    | Bt2020HlgLimit
    | Bt2020PqLimit
    | P3HlgLimit
    | P3PqLimit
    | LinearP3
    | LinearSrgb
    | LinearBt709
    | LinearBt2020
    | DisplaySrgb
    | DisplayP3Srgb
    | DisplayP3Hlg
    | DisplayP3Pq
    | ...
}
```

**Function:** Color gamut type enumeration.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

**Parent Types:**

- Equatable\<ColorSpace>
- ToString

### AdobeRgb1998

```cangjie
AdobeRgb1998
```

**Function:** RGB color gamut is Adobe RGB (1998) type; transfer function is Adobe RGB (1998) type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### AdobeRgb1998Limit

```cangjie
AdobeRgb1998Limit
```

**Function:** RGB color gamut is Adobe RGB (1998) type; transfer function is Adobe RGB (1998) type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt2020Hlg

```cangjie
Bt2020Hlg
```

**Function:** RGB color gamut is BT2020 type; transfer function is HLG type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt2020HlgLimit

```cangjie
Bt2020HlgLimit
```

**Function:** RGB color gamut is BT2020 type; transfer function is HLG type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt2020Pq

```cangjie
Bt2020Pq
```

**Function:** RGB color gamut is BT2020 type; transfer function is PQ type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt2020PqLimit

```cangjie
Bt2020PqLimit
```

**Function:** RGB color gamut is BT2020 type; transfer function is PQ type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt601Ebu

```cangjie
Bt601Ebu
```

**Function:** RGB color gamut is BT601_P type; transfer function is BT709 type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt601EbuLimit

```cangjie
Bt601EbuLimit
```

**Function:** RGB color gamut is BT601_P type; transfer function is BT709 type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt601SmpteC

```cangjie
Bt601SmpteC
```

**Function:** RGB color gamut is BT601_N type; transfer function is BT709 type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt601SmpteCLimit

```cangjie
Bt601SmpteCLimit
```

**Function:** RGB color gamut is BT601_N type; transfer function is BT709 type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt709

```cangjie
Bt709
```

**Function:** RGB color gamut is BT709 type; transfer function is BT709 type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Bt709Limit

```cangjie
Bt709Limit
```

**Function:** RGB color gamut is BT709 type; transfer function is BT709 type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Custom

```cangjie
Custom
```

**Function:** User-defined color gamut type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DciP3

```cangjie
DciP3
```

**Function:** RGB color gamut is DCI-P3 type; transfer function is Gamma 2.6 type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplayP3

```cangjie
DisplayP3
```

**Function:** RGB color gamut is Display P3 type; transfer function is Srgb type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplayP3Hlg

```cangjie
DisplayP3Hlg
```

**Function:** Same as P3_HLG; RGB color gamut is Display P3 type; transfer function is HLG type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplayP3Limit

```cangjie
DisplayP3Limit
```

**Function:** RGB color gamut is Display P3 type; transfer function is Srgb type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplayP3Pq

```cangjie
DisplayP3Pq
```

**Function:** Same as P3_PQ; RGB color gamut is Display P3 type; transfer function is PQ type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplayP3Srgb

```cangjie
DisplayP3Srgb
```

**Function:** Same as DisplayP3; RGB color gamut is Display P3 type; transfer function is Srgb type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### DisplaySrgb

```cangjie
DisplaySrgb
```

**Function:** Same as Srgb; RGB color gamut is Srgb type; transfer function is Srgb type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### LinearBt2020

```cangjie
LinearBt2020
```

**Function:** RGB color gamut is BT2020 type; transfer function is Linear type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### LinearBt709

```cangjie
LinearBt709
```

**Function:** Same as LINEAR_Srgb; RGB color gamut is BT709 type; transfer function is Linear type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### LinearP3

```cangjie
LinearP3
```

**Function:** RGB color gamut is Display P3 type; transfer function is Linear type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### LinearSrgb

```cangjie
LinearSrgb
```

**Function:** RGB color gamut is Srgb type; transfer function is Linear type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### P3Hlg

```cangjie
P3Hlg
```

**Function:** RGB color gamut is Display P3 type; transfer function is HLG type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### P3HlgLimit

```cangjie
P3HlgLimit
```

**Function:** RGB color gamut is Display P3 type; transfer function is HLG type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### P3Pq

```cangjie
P3Pq
```

**Function:** RGB color gamut is Display P3 type; transfer function is PQ type; encoding range is Full type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### P3PqLimit

```cangjie
P3PqLimit
```

**Function:** RGB color gamut is Display P3 type; transfer function is PQ type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### Srgb

```cangjie
Srgb
```

**Function:** RGB color gamut is Srgb type; transfer function is Srgb type; encoding range is Full type; default system color gamut type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### SrgbLimit

```cangjie
SrgbLimit
```

**Function:** RGB color gamut is Srgb type; transfer function is Srgb type; encoding range is Limit type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22### Unknown

```cangjie
Unknown
```

**Function:** Unknown color space type.

**System Capability:** SystemCapability.Graphic.Graphic2D.ColorManager.Core

**Since:** 22

### func !=(ColorSpace)

```cangjie
public operator func !=(other: ColorSpace): Bool
```

**Function:** Performs inequality comparison with another `ColorSpace` enumeration value.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ColorSpace](#enum-colorspace) | Yes | - | Another color space type for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if not equal, otherwise returns `false`. |

### func ==(ColorSpace)

```cangjie
public operator func ==(other: ColorSpace): Bool
```

**Function:** Performs equality comparison with another `ColorSpace` enumeration value.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ColorSpace](#enum-colorspace) | Yes | - | Another color space type for comparison. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the [ColorSpace](#enum-colorspace) enumeration value to a string.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string corresponding to the [ColorSpace](#enum-colorspace) enumeration value. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkGraphics2D.*

let value: String = ColorSpace.DisplayP3.toString()
```