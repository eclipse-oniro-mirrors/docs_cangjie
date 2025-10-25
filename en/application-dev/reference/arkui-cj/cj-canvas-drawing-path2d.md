# Path2D

A path object that supports describing paths through its interface and rendering them via the Canvas stroke or fill methods.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Path2D

```cangjie
public class Path2D {
    public init()
    public init(path: String)
}
```

**Description:** A path object that supports describing paths through its interface and rendering them via the Canvas stroke or fill methods.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init()

```cangjie
public init()
```

**Description:** Constructs an empty Path2D object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(String)

```cangjie
public init(path: String)
```

**Description:** Constructs a Path2D object using a path string compliant with SVG path description specifications.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | A path string compliant with SVG path description specifications. Format reference: SVG Path Description Specification in Path documentation. |

### func addPath(Path2D)

```cangjie
public func addPath(path2D: Path2D): Unit
```

**Description:** Adds another path to the current path object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path2D | [Path2D](./cj-canvas-drawing-path2d.md#class-path2d) | Yes | - | The path object to be added to the current path. Unit: px. |

### func arc(Float64, Float64, Float64, Float64, Float64, Bool)

```cangjie
public func arc(
    x: Float64,
    y: Float64,
    radius: Float64,
    startAngle: Float64,
    endAngle: Float64,
    counterclockwise!: Bool = false
): Unit
```

**Description:** Draws an arc path.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the arc's center.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the arc's center.<br>Default unit: vp. |
| radius | Float64 | Yes | - | The radius of the arc.<br>Default unit: vp. |
| startAngle | Float64 | Yes | - | The starting radian of the arc.<br>Unit: radians. |
| endAngle | Float64 | Yes | - | The ending radian of the arc.<br>Unit: radians. |
| counterclockwise | Bool | No | false | **Named parameter.** Whether to draw the arc counterclockwise.<br>true: Draw counterclockwise.<br>false: Draw clockwise. |

### func arcTo(Float64, Float64, Float64, Float64, Float64)

```cangjie
public func arcTo(
    x1: Float64,
    y1: Float64,
    x2: Float64,
    y2: Float64,
    radius: Float64
): Unit
```

**Description:** Creates an arc path based on points the arc passes through and its radius.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x1 | Float64 | Yes | - | The x-coordinate of the first point the arc passes through.<br>Default unit: vp. |
| y1 | Float64 | Yes | - | The y-coordinate of the first point the arc passes through.<br>Default unit: vp. |
| x2 | Float64 | Yes | - | The x-coordinate of the second point the arc passes through.<br>Default unit: vp. |
| y2 | Float64 | Yes | - | The y-coordinate of the second point the arc passes through.<br>Default unit: vp. |
| radius | Float64 | Yes | - | The radius of the arc.<br>Default unit: vp. |

### func bezierCurveTo(Float64, Float64, Float64, Float64, Float64, Float64)

```cangjie
public func bezierCurveTo(
    cp1x: Float64,
    cp1y: Float64,
    cp2x: Float64,
    cp2y: Float64,
    x: Float64,
    y: Float64
): Unit
```

**Description:** Creates a cubic Bézier curve path.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| cp1x | Float64 | Yes | - | The x-coordinate of the first Bézier parameter.<br>Default unit: vp. |
| cp1y | Float64 | Yes | - | The y-coordinate of the first Bézier parameter.<br>Default unit: vp. |
| cp2x | Float64 | Yes | - | The x-coordinate of the second Bézier parameter.<br>Default unit: vp. |
| cp2y | Float64 | Yes | - | The y-coordinate of the second Bézier parameter.<br>Default unit: vp. |
| x | Float64 | Yes | - | The x-coordinate of the path's endpoint.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the path's endpoint.<br>Default unit: vp. |

### func closePath()

```cangjie
public func closePath(): Unit
```

**Description:** Moves the current point of the path back to the starting point, drawing a straight line between them. If the shape is already closed or has only one point, this function does nothing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func ellipse(Float64, Float64, Float64, Float64, Float64, Float64, Float64, Bool)

```cangjie
public func ellipse(
    x: Float64,
    y: Float64,
    radiusX: Float64,
    radiusY: Float64,
    rotation: Float64,
    startAngle: Float64,
    endAngle: Float64,
    counterclockwise!: Bool = false
): Unit
```

**Description:** Draws an ellipse within the specified rectangular area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the ellipse's center.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the ellipse's center.<br>Default unit: vp. |
| radiusX | Float64 | Yes | - | The radius length along the x-axis.<br>Default unit: vp. |
| radiusY | Float64 | Yes | - | The radius length along the y-axis.<br>Default unit: vp. |
| rotation | Float64 | Yes | - | The rotation angle of the ellipse.<br>Unit: radians. |
| startAngle | Float64 | Yes | - | The starting angle for drawing the ellipse.<br>Unit: radians. |
| endAngle | Float64 | Yes | - | The ending angle for drawing the ellipse.<br>Unit: radians. |
| counterclockwise | Bool | No | false | **Named parameter.** Whether to draw the ellipse counterclockwise.<br>true: Draw counterclockwise.<br>false: Draw clockwise. |

### func lineTo(Float64, Float64)

```cangjie
public func lineTo(x: Float64, y: Float64): Unit
```

**Description:** Draws a straight line from the current point to the target point.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the target point.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the target point.<br>Default unit: vp. |

### func moveTo(Float64, Float64)

```cangjie
public func moveTo(x: Float64, y: Float64): Unit
```

**Description:** Moves the current coordinate point of the path to the target point without drawing a line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the target point.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the target point.<br>Default unit: vp. |

### func quadraticCurveTo(Float64, Float64, Float64, Float64)

```cangjie
public func quadraticCurveTo(
    cpx: Float64,
    cpy: Float64,
    x: Float64,
    y: Float64
): Unit
```

**Description:** Creates a quadratic Bézier curve path.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| cpx | Float64 | Yes | - | The x-coordinate of the Bézier parameter.<br>Default unit: vp. |
| cpy | Float64 | Yes | - | The y-coordinate of the Bézier parameter.<br>Default unit: vp. |
| x | Float64 | Yes | - | The x-coordinate of the path's endpoint.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the path's endpoint.<br>Default unit: vp. |

### func rect(Float64, Float64, Float64, Float64)

```cangjie
public func rect(x: Float64, y: Float64, width: Float64, height: Float64): Unit
```

**Description:** Creates a rectangular path.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float64 | Yes | - | The x-coordinate of the rectangle's top-left corner.<br>Default unit: vp. |
| y | Float64 | Yes | - | The y-coordinate of the rectangle's top-left corner.<br>Default unit: vp. |
| width | Float64 | Yes | - | The width of the rectangle.<br>Default unit: vp. |
| height | Float64 | Yes | - | The height of the rectangle.<br>Default unit: vp. |

### func setTransform(Float64, Float64, Float64, Float64, Float64, Float64)

```cangjie
public func setTransform(
    scaleX: Float64,
    skewX: Float64,
    skewY: Float64,
    scaleY: Float64,
    translateX: Float64,
    translateY: Float64
): Unit
```

**Description:** Performs scaling, skewing, and translation operations on the path object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| scaleX | Float64 | Yes | - | The scaling factor along the x-axis. |
| skewX | Float64 | Yes | - | The skew factor along the x-axis. |
| skewY | Float64 | Yes | - | The skew factor along the y-axis. |
| scaleY | Float64 | Yes | - | The scaling factor along the y-axis. |
| translateX | Float64 | Yes | - | The translation value along the x-axis. |
| translateY | Float64 | Yes | - | The translation value along the y-axis. |