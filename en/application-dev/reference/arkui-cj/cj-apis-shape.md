# ohos.arkui.shape

Provides fundamental capabilities for drawing shapes.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class BaseShape

```cangjie
public abstract class BaseShape {}
```

**Description:** The base class for shapes, providing basic properties and methods for graphical elements.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func fill(?ResourceColor)

```cangjie
public func fill(color: ?ResourceColor): This
```

**Description:** Sets the fill color for the shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| color | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The fill color of the shape. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func height(?Length)

```cangjie
public func height(height: ?Length): This
```

**Description:** Sets the height of the shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| height | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The height of the shape. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func offset(?Length, ?Length)

```cangjie
public func offset(x!: ?Length, y!: ?Length): This
```

**Description:** Sets the offset of the shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The x-axis offset.<br>Default: 0.0.px. |
| y | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The y-axis offset.<br>Default: 0.0.px. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func size(?Length, ?Length)

```cangjie
public func size(width!: ?Length, height!: ?Length): This
```

**Description:** Sets the dimensions of the shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The width of the shape.<br>Default: 0.0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The height of the shape.<br>Default: 0.0.vp. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func width(?Length)

```cangjie
public func width(width: ?Length): This
```

**Description:** Sets the width of the shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The width of the shape. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

## class CircleShape

```cangjie
public class CircleShape <: BaseShape {
    public init(width!: ?Length = None, height!: ?Length = None)
}
```

**Description:** Circular shape used for the [clipShape](./cj-universal-attribute-shapclip.md#func-clipshapebaseshape) and [maskShape](./cj-universal-attribute-shapclip.md#func-maskshapebaseshape) interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [BaseShape](#class-baseshape)

### init(?Length, ?Length)

```cangjie
public init(width!: ?Length = None, height!: ?Length = None)
```

**Description:** Constructor for CircleShape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The width of the circle.<br>Default: 0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The height of the circle.<br>Default: 0.vp. |

## class EllipseShape

```cangjie
public class EllipseShape <: BaseShape {
    public init(width!: ?Length = None, height!: ?Length = None)
}
```

**Description:** Elliptical shape used for the [clipShape](./cj-universal-attribute-shapclip.md#func-clipshapebaseshape) and [maskShape](./cj-universal-attribute-shapclip.md#func-maskshapebaseshape) interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [BaseShape](#class-baseshape)

### init(?Length, ?Length)

```cangjie
public init(width!: ?Length = None, height!: ?Length = None)
```

**Description:** Constructor for EllipseShape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The width of the ellipse.<br>Default: 0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The height of the ellipse.<br>Default: 0.vp. |

## class PathShape

```cangjie
public class PathShape <: BaseShape {
    public init(commands!: ?ResourceStr = None)
    public init(width!: ?Length, height!: ?Length, commands!: ?ResourceStr = None)
}
```

**Description:** Path used for the [clipShape](./cj-universal-attribute-shapclip.md#func-clipshapebaseshape) and [maskShape](./cj-universal-attribute-shapclip.md#func-maskshapebaseshape) interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [BaseShape](#class-baseshape)

### init(?ResourceStr)

```cangjie
public init(commands!: ?ResourceStr = None)
```

**Description:** Constructor for PathShape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| commands | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Drawing commands for the path.<br>Default: "". <br>For more information, see the [drawing commands]((./cj-graphic-drawing-path.md#func-commandsresourcestr)) supported by commands.|

### init(?Length, ?Length, ?ResourceStr)

```cangjie
public init(width!: ?Length, height!: ?Length, commands!: ?ResourceStr = None)
```

**Description:** Constructor for PathShape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The width of the path.<br>Default: 0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** The height of the path.<br>Default: 0.vp. |
| commands | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The path commands.<br>Default: "". <br>For more information, see the [drawing commands]((./cj-graphic-drawing-path.md#func-commandsresourcestr)) supported by commands.|

## class RectShape

```cangjie
public class RectShape <: BaseShape {
    public init(width!: ?Length = None, height!: ?Length = None)
}
```

**Description:** Rectangular shape used for the [clipShape](./cj-universal-attribute-shapclip.md#func-clipshapebaseshape) and [maskShape](./cj-universal-attribute-shapclip.md#func-maskshapebaseshape) interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Class:**

- [BaseShape](#class-baseshape)

### init(?Length, ?Length)

```cangjie
public init(width!: ?Length = None, height!: ?Length = None)
```

**Description:** Constructor for RectShape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The width of the rectangle.<br>Default: 0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The height of the rectangle.<br>Default: 0.vp. |

### func radius(?Length)

```cangjie
public func radius(value: ?Length): This
```

**Description:** Sets the corner radius of the rectangle.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The corner radius of the rectangle.<br>Default: 0.vp. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func radiusHeight(?Length)

```cangjie
public func radiusHeight(value: ?Length): This
```

**Description:** Sets the vertical corner radius of the rectangle.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The vertical corner radius of the rectangle.<br>Default: 0.vp. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |

### func radiusWidth(?Length)

```cangjie
public func radiusWidth(value: ?Length): This
```

**Description:** Sets the horizontal corner radius of the rectangle.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The horizontal corner radius of the rectangle.<br>Default: 0.vp. |

**Return Value:**

| Type | Description |
|:----|:----|
| This | Returns the current object. |