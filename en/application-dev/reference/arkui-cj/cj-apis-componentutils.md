# ohos.component_utils (ComponentUtils)

Provides the capability to obtain the coordinates and dimensions of a component's drawing area.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ComponentUtils

```cangjie
public class ComponentUtils {}
```

**Description:** Provides functionality to obtain the coordinates and dimensions of a specified component's drawing area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static func getRectangleById(String)

```cangjie
public static func getRectangleById(id: String): ComponentInfo
```

**Description:** Retrieves a component instance object by its ID and synchronously returns the obtained coordinate position and dimensions to the developer through the component instance object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | The specified component ID. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ComponentInfo](#class-componentinfo) | Information about the component's dimensions, position, translation, scaling, rotation, and affine matrix properties. |

## class ComponentInfo

```cangjie
public class ComponentInfo {
    public var size: Size
    public var localOffset: Offset
    public var windowOffset: Offset
    public var screenOffset: Offset
    public var translate: TranslateResult
    public var scale: ScaleResult
    public var rotate: RotateResult
    public var transform: Matrix4Result
    public init(size: Size, localOffset: Offset, windowOffset: Offset, screenOffset: Offset, translate: TranslateResult,
    scale: ScaleResult, rotate: RotateResult, transform: Matrix4Result)
}
```

**Description:** Information about the coordinate position and dimensions of a component instance object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var localOffset

```cangjie
public var localOffset: Offset
```

**Description:** Sets the component's information relative to its parent component.

**Type:** [Offset](#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var rotate

```cangjie
public var rotate: RotateResult
```

**Description:** Sets the component's rotation information.

**Type:** [RotateResult](#class-rotateresult)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var scale

```cangjie
public var scale: ScaleResult
```

**Description:** Sets the component's scaling information.

**Type:** [ScaleResult](#class-scaleresult)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var screenOffset

```cangjie
public var screenOffset: Offset
```

**Description:** Sets the component's information relative to the screen.

**Type:** [Offset](#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var size

```cangjie
public var size: Size
```

**Description:** Sets the component's dimension information.

**Type:** [Size](#class-size)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transform

```cangjie
public var transform: Matrix4Result
```

**Description:** Sets the component's transformation matrix information.

**Type:** [Matrix4Result](#type-matrix4result)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var translate

```cangjie
public var translate: TranslateResult
```

**Description:** Sets the component's translation information.

**Type:** [TranslateResult](#class-translateresult)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var windowOffset

```cangjie
public var windowOffset: Offset
```

**Description:** Sets the component's information relative to the window.

**Type:** [Offset](#class-offset)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Size, Offset, Offset, Offset, TranslateResult, ScaleResult, RotateResult, Matrix4Result)

```cangjie
public init(size: Size, localOffset: Offset, windowOffset: Offset, screenOffset: Offset, translate: TranslateResult,
    scale: ScaleResult, rotate: RotateResult, transform: Matrix4Result)
```

**Description:** Constructs an object of type ComponentInfo.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Size](#class-size) | Yes | - | The component's dimension information. |
| localOffset | [Offset](#class-offset) | Yes | - | The component's information relative to its parent component. |
| windowOffset | [Offset](#class-offset) | Yes | - | The component's information relative to the window. |
| screenOffset | [Offset](#class-offset) | Yes | - | The component's information relative to the screen. |
| translate | [TranslateResult](#class-translateresult) | Yes | - | The component's translation information. |
| scale | [ScaleResult](#class-scaleresult) | Yes | - | The component's scaling information. |
| rotate | [RotateResult](#class-rotateresult) | Yes | - | The component's rotation information. |
| transform | [Matrix4Result](#type-matrix4result) | Yes | - | The component's transformation matrix information. |

## class Offset

```cangjie
public class Offset {
    public var x: Float64
    public var y: Float64
    public init(x: Float64, y: Float64)
}
```

**Description:** Defines offset properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Description:** The x-coordinate of the position.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Description:** The y-coordinate of the position.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Float64, Float64)

```cangjie
public init(x: Float64, y: Float64)
```

**Description:** Constructs an object of type Offset.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the position. |
| y | Float64 | Yes | - | The y-coordinate of the position. |

## class RotateResult

```cangjie
public class RotateResult {
    public var x: Float64
    public var y: Float64
    public var z: Float64
    public var centerX: Float64
    public var centerY: Float64
    public var angle: Float64
    public init(x: Float64, y: Float64, z: Float64, centerX: Float64, centerY: Float64, angle: Float64)
}
```

**Description:** Rotation result.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var angle

```cangjie
public var angle: Float64
```

**Description:** The rotation angle.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerX

```cangjie
public var centerX: Float64
```

**Description:** The x-axis coordinate transformation of the center point.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerY

```cangjie
public var centerY: Float64
```

**Description:** The y-axis coordinate transformation of the center point.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Description:** The x-coordinate of the rotation axis vector.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Description:** The y-coordinate of the rotation axis vector.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: Float64
```

**Description:** The z-coordinate of the rotation axis vector.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Float64, Float64, Float64, Float64, Float64, Float64)

```cangjie
public init(x: Float64, y: Float64, z: Float64, centerX: Float64, centerY: Float64, angle: Float64)
```

**Description:** Constructs an object of type RotateResult.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the rotation axis vector. |
| y | Float64 | Yes | - | The y-coordinate of the rotation axis vector. |
| z | Float64 | Yes | - | The z-coordinate of the rotation axis vector. |
| centerX | Float64 | Yes | - | The x-axis coordinate transformation of the center point. |
| centerY | Float64 | Yes | - | The y-axis coordinate transformation of the center point. |
| angle | Float64 | Yes | - | The rotation angle. |## class ScaleResult

```cangjie
public class ScaleResult {
    public var x: Float64
    public var y: Float64
    public var z: Float64
    public var centerX: Float64
    public var centerY: Float64
    public init(x: Float64, y: Float64, z: Float64, centerX: Float64, centerY: Float64)
}
```

**Function:** Scaling result.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerX

```cangjie
public var centerX: Float64
```

**Function:** X-axis coordinate transformation of the center point.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var centerY

```cangjie
public var centerY: Float64
```

**Function:** Y-axis coordinate transformation of the center point.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Function:** X-axis scaling factor.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Function:** Y-axis scaling factor.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: Float64
```

**Function:** Z-axis scaling factor.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Float64, Float64, Float64, Float64, Float64)

```cangjie
public init(x: Float64, y: Float64, z: Float64, centerX: Float64, centerY: Float64)
```

**Function:** Constructs a ScaleResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|x|Float64|Yes|-|X-axis scaling factor.|
|y|Float64|Yes|-|Y-axis scaling factor.|
|z|Float64|Yes|-|Z-axis scaling factor.|
|centerX|Float64|Yes|-|X-axis coordinate transformation of the center point.|
|centerY|Float64|Yes|-|Y-axis coordinate transformation of the center point.|

## class Size

```cangjie
public class Size {
    public var width: Float64
    public var height: Float64
    public init(width: Float64, height: Float64)
}
```

**Function:** Defines size attributes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: Float64
```

**Function:** Height attribute.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: Float64
```

**Function:** Width attribute.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Float64, Float64)

```cangjie
public init(width: Float64, height: Float64)
```

**Function:** Constructs a Size object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|width|Float64|Yes|-|Width attribute.|
|height|Float64|Yes|-|Height attribute.|

## class TranslateResult

```cangjie
public class TranslateResult {
    public var x: Float64
    public var y: Float64
    public var z: Float64
    public init(x: Float64, y: Float64, z: Float64)
}
```

**Function:** Translation result.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Function:** X-axis translation distance.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Function:** Y-axis translation distance.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var z

```cangjie
public var z: Float64
```

**Function:** Z-axis translation distance.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Float64, Float64, Float64)

```cangjie
public init(x: Float64, y: Float64, z: Float64)
```

**Function:** Constructs a TranslateResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
|x|Float64|Yes|-|X-axis translation distance.<br>Unit: vp.|
|y|Float64|Yes|-|Y-axis translation distance.<br>Unit: vp.|
|z|Float64|Yes|-|Z-axis translation distance.<br>Unit: vp.|

## type Matrix4Result

```cangjie
public type Matrix4Result = VArray<Float64, $16>
```

**Function:** 4x4 transformation matrix result type.

**Type:** VArray<Float64, $16>

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22
