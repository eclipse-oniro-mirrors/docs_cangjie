# ImageData

The ImageData object can store pixel data rendered by a canvas.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ImageData

```cangjie
public class ImageData {
    public init(width: Float64, height: Float64, data!: Array<UInt8>, unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
    public init(width: Float64, height: Float64, unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
}
```

**Description:** The ImageData object can store pixel data rendered by a canvas.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop data

```cangjie
public prop data: Array<UInt8>
```

**Description:** A one-dimensional array containing corresponding color data, with values ranging from 0 to 255.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Array\<UInt8>

**Access:** Read-only

**Since:** 21

### prop height

```cangjie
public prop height: Int32
```

**Description:** The height of the rectangular area, with the default unit being vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Int32

**Access:** Read-only

**Since:** 21

### prop width

```cangjie
public prop width: Int32
```

**Description:** The width of the rectangular area, with the default unit being vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Int32

**Access:** Read-only

**Since:** 21

### init(Float64, Float64, Array\<UInt8>, LengthMetricsUnit)

```cangjie
public init(width: Float64, height: Float64, data!: Array<UInt8>,
    unit!: LengthMetricsUnit = LengthMetricsUnit.Default)
```

**Description:** Constructs an ImageData object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | Float64 | Yes | - | The width of the rectangular area, with the default unit being vp. |
| height | Float64 | Yes | - | The height of the rectangular area, with the default unit being vp. |
| data | Array\<UInt8> | Yes | - | **Named parameter.** A one-dimensional array containing corresponding color data, with values ranging from 0 to 255. |
| unit | [LengthMetricsUnit](./cj-common-types.md#enum-lengthmetricsunit) | No | LengthMetricsUnit.Default | **Named parameter.** Used to configure the unit mode of the ImageData object. Once configured, it cannot be dynamically changed. The configuration method is the same as [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

### init(Float64, Float64, LengthMetricsUnit)

```cangjie
public init(width: Float64, height: Float64, unit!: LengthMetricsUnit = LengthMetricsUnit.Default)
```

**Description:** Constructs an ImageData object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | Float64 | Yes | - | The width of the rectangular area, with the default unit being vp. |
| height | Float64 | Yes | - | The height of the rectangular area, with the default unit being vp. |
| unit | [LengthMetricsUnit](./cj-common-types.md#enum-lengthmetricsunit) | No | LengthMetricsUnit.Default | **Named parameter.** Used to configure the unit mode of the ImageData object. Once configured, it cannot be dynamically changed. The configuration method is the same as [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

## Example Code

<!-- run -->

```cangjie
public class ImageData {
    public init(width: Float64, height: Float64, data!: Array<UInt8>, unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
    public init(width: Float64, height: Float64, unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
}
```