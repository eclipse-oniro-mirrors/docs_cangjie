# Border Settings

Configure component border styles.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func border(Length, ResourceColor, Length, BorderStyle)

```cangjie
public func border(width!: Length, color!: ResourceColor = Color.Black, radius!: Length = 0.vp,
    style!: BorderStyle = BorderStyle.Solid): This
```

**Function:** Sets the border style of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Border width. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Black | Border color. |
| radius | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Border corner radius. |
| style | [BorderStyle](./cj-common-types.md#enum-borderstyle) | No | BorderStyle.Solid | Border style. |

## func borderColor(ResourceColor)

```cangjie
public func borderColor(value: ResourceColor): This
```

**Function:** Sets the border color of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Border color. |

## func borderRadius(Length)

```cangjie
public func borderRadius(value: Length): This
```

**Function:** Sets the corner radius of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Corner radius. |

## func borderRadius(Length, Length, Length, Length)

```cangjie
public func borderRadius(topLeft!: Length = 0.vp, topRight!: Length = 0.vp, bottomLeft!: Length = 0.vp,
    bottomRight!: Length = 0.vp): This
```

**Function:** Sets the corner radii for all four corners of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| topLeft | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Top-left corner radius. |
| topRight | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Top-right corner radius. |
| bottomLeft | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Bottom-left corner radius. |
| bottomRight | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Bottom-right corner radius. |

## func borderStyle(BBorderStyle)

```cangjie
public func borderStyle(value: BorderStyle): This
```

**Function:** Sets the border style of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [BorderStyle](./cj-common-types.md#enum-borderstyle) | Yes | - | Border style value. |

## func borderWidth(EdgeWidths)

```cangjie
public func borderWidth(value: EdgeWidths): This
```

**Function:** Sets the brightness of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [EdgeWidths](./cj-universal-attribute-border.md#class-edgewidths) | Yes | - | Edge widths. |

## func borderWidth(Length)

```cangjie
public func borderWidth(value: Length): This
```

**Function:** Sets the border width of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Border width. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Resolution Steps |
  | :---- | :--- | :--- |
  | Percentage values are not supported. | todo | todo |

## Basic Type Definitions

### class EdgeWidths

```cangjie
public class EdgeWidths {
    public var top: Length
    public var right: Length
    public var bottom: Length
    public var left: Length
    public init(top!: Length = 0.vp, right!: Length = 0.vp, bottom!: Length = 0.vp, left!: Length = 0.vp)
}
```

**Function:** Sets the border width of a popup backdrop. At least one parameter must be provided when instantiating this object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var bottom

```cangjie
public var bottom: Length
```

**Function:** Bottom border width.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var left

```cangjie
public var left: Length
```

**Function:** Left border width.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var right

```cangjie
public var right: Length
```

**Function:** Right border width.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var top

```cangjie
public var top: Length
```

**Function:** Top border width.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Length, Length, Length, Length)

```cangjie
public init(top!: Length = 0.vp, right!: Length = 0.vp, bottom!: Length = 0.vp, left!: Length = 0.vp)
```

**Function:** Constructs an EdgeWidths object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Top border width. |
| right | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Right border width. |
| bottom | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Bottom border width. |
| left | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Left border width. |