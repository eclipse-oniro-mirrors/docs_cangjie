# ImageData

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The ImageData object can store pixel data rendered by a canvas.

> **Note：**
>
> When creating ImageData, the width and height should not exceed 16384px, and the maximum area should not exceed 16000px*16000px. Exceeding the maximum area will prevent proper rendering.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ImageData

```cangjie
public class ImageData {
    public init(width: ?Float64, height: ?Float64, data!: ?Array<UInt8>, unit!: ?LengthMetricsUnit = None)
    public init(width: ?Float64, height: ?Float64, unit!: ?LengthMetricsUnit = None)
}
```

**Description:** The ImageData object can store pixel data rendered by a canvas.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop width

```cangjie
public prop width: Int32
```

**Description:** Width of the rectangular area, with vp as the default unit.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop height

```cangjie
public prop height: Int32
```

**Description:** Height of the rectangular area, with vp as the default unit.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop data

```cangjie
public prop data: Array<UInt8>
```

**Description:** A one-dimensional array containing corresponding color data, with values ranging from 0 to 255.

**Type:** Array\<UInt8>

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float64, ?Float64, ?Array\<UInt8>, ?LengthMetricsUnit)

```cangjie
public init(width: ?Float64, height: ?Float64, data!: ?Array<UInt8>,
    unit!: ?LengthMetricsUnit = None)
```

**Description:** Constructs an ImageData object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?Float64 | No | - | Width of the rectangular area, with vp as the default unit. |
| height | ?Float64 | No | - | Height of the rectangular area, with vp as the default unit. |
| data | ?Array\<UInt8> | No | - | **Named parameter.** A one-dimensional array containing corresponding color data, with values ranging from 0 to 255. |
| unit | ?[LengthMetricsUnit](./cj-common-types.md#enum-lengthmetricsunit) | No | None | **Named parameter.** Used to configure the unit mode of the ImageData object. Once configured, it cannot be dynamically changed. The configuration method is the same as [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

> **Note：**
>
> - width and height cannot be less than 0.0, otherwise there will be unexpected results.
> - The size of data must be equal to 4.0 * width * height, otherwise there will be unexpected results.

### init(?Float64, ?Float64, ?LengthMetricsUnit)

```cangjie
public init(width: ?Float64, height: ?Float64, unit!: ?LengthMetricsUnit = None)
```

**Description:** Constructs an ImageData object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?Float64 | No | - | Width of the rectangular area, with vp as the default unit. |
| height | ?Float64 | No | - | Height of the rectangular area, with vp as the default unit. |
| unit | ?[LengthMetricsUnit](./cj-common-types.md#enum-lengthmetricsunit) | No | None | **Named parameter.** Used to configure the unit mode of the ImageData object. Once configured, it cannot be dynamically changed. The configuration method is the same as [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

> **Note：**
>
> width and height cannot be less than 0.0, otherwise there will be unexpected results.
