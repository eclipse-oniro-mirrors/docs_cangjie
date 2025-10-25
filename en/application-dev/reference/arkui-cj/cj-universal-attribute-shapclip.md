# Shape Clipping

Used for clipping and masking components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func clip(Bool)

```cangjie
public func clip(value: Bool): This
```

**Function:** Sets whether to clip content that exceeds the component boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to clip. |

## func clipShape(BaseShape)

```cangjie
public func clipShape(value: BaseShape): This
```

**Function:** Sets the clipping shape for the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [BaseShape](./cj-graphic-drawing-shape.md#class-baseshape) | Yes | - | Clipping shape. |

## func maskShape(BaseShape)

```cangjie
public func maskShape(value: BaseShape): This
```

**Function:** Adds a mask of the specified shape to the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | BaseShape | Yes | - | Adds a mask of the specified shape to the current component. |

### class CircleShape

```cangjie
public class CircleShape <: BaseShape {
    public init(width!: Length = 0.vp, height!: Length = 0.vp)
}
```

**Function:** Circular shape for clip and mask interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parent Type:**

[BaseShape](./cj-graphic-drawing-shape.md#class-baseshape)

#### init(length, length)

```cangjie
public init(width!: Length = 0.vp, height!: Length = 0.vp)
```

**Function:** Constructs a circle with specified width and height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Width.<br>Initial value: 0.vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Height.<br>Initial value: 0.vp. |

### class EllipseShape

```cangjie
public class EllipseShape <: BaseShape {
    public init(width!: Length, height!: Length)
}
```

**Function:** Elliptical shape for clip and mask interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parent Type:**

[BaseShape](./cj-graphic-drawing-shape.md#class-baseshape)

#### init(length, length)

```cangjie
public init(width!: Length, height!: Length)
```

**Function:** Constructs an ellipse with specified width and height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Width.<br>Initial value: 0.vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Height.<br>Initial value: 0.vp. |

### class RectShape

```cangjie
public class RectShape <: BaseShape {
    public init(width!: Length = 0.vp, height!: Length = 0.vp)
    public func radiusWidth(value: Length): This
    public func radiusHeight(value: Length): This
    public func radius(value: Length): This
}
```

**Function:** Rectangular shape for clip and mask interfaces.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parent Type:**

[BaseShape](./cj-graphic-drawing-shape.md#class-baseshape)

#### init(Length, Length)

```cangjie
public init(width!: Length = 0.vp, height!: Length = 0.vp)
```

**Function:** Constructs a rectangle with specified width and height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Width.<br>Initial value: 0.vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Height.<br>Initial value: 0.vp. |

#### func radiusWidth(Length)

```cangjie
public func radiusWidth(value: Length): This
```

**Function:** Sets the width of rounded corners. If only width is set, height will match width. Invalid values are treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Width of rounded corners.<br>Initial value: 0.vp. |

#### func radiusHeight(Length)

```cangjie
public func radiusHeight(value: Length): This
```

**Function:** Sets the height of rounded corners. If only height is set, width will match height. Invalid values are treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Height of rounded corners.<br>Initial value: 0.vp. |

#### func radius(Length)

```cangjie
public func radius(value: Length): This
```

**Function:** Sets the radius size of rounded corners. Invalid values are treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Radius size of rounded corners.<br>Initial value: 0.vp. |