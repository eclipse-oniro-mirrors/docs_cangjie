# Position Settings

Configure the alignment, layout direction, and display position of components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func align(Alignment)

```cangjie
public func align(value: Alignment): This
```

**Function:** Sets the alignment of the component within its container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Alignment](./cj-common-types.md#enum-alignment) | Yes | - | Alignment method. |

## func alignRules(AlignRuleOption)

```cangjie
public func alignRules(value: AlignRuleOption): This
```

**Function:** Sets the alignment rules for the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [AlignRuleOption](./cj-universal-attribute-location.md#class-alignruleoption) | Yes | - | Alignment rule options. |

## func direction(Direction)

```cangjie
public func direction(value: Direction): This
```

**Function:** Sets the layout direction of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Direction](./cj-common-types.md#enum-direction) | Yes | - | Layout direction. |

## func markAnchor(Length, Length)

```cangjie
public func markAnchor(x!: Length, y!: Length): This
```

**Function:** Sets the anchor position of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** X-axis coordinate. |
| y | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Y-axis coordinate. |

## func offset(Length, Length)

```cangjie
public func offset(x!: Length, y!: Length): This
```

**Function:** Sets the offset of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** X-axis coordinate. |
| y | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Y-axis coordinate. |

## func position(Length, Length)

```cangjie
public func position(x!: Length, y!: Length): This
```

**Function:** Sets the position of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** X-axis coordinate. |
| y | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Y-axis coordinate. |

## Basic Type Definitions

### class AlignRuleOption

```cangjie
public class AlignRuleOption {
    public var left:?HorizontalAlignment
    public var right:?HorizontalAlignment
    public var middle:?HorizontalAlignment
    public var top:?VerticalAlignment
    public var bottom:?VerticalAlignment
    public var center:?VerticalAlignment 
    public var bias: Bias
    public init(left!: ?HorizontalAlignment = None, right!: ?HorizontalAlignment = None,
        middle!: ?HorizontalAlignment = None, top!: ?VerticalAlignment = None,
        bottom!: ?VerticalAlignment = None, center!: ?VerticalAlignment = None,
        bias!: Bias = Bias()
    )
}
```

**Function:** Configures alignment rule options for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var bias

```cangjie
public var bias: Bias = Bias()
```

**Function:** Sets the offset for component alignment.

**Type:** [Bias](#class-bias)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var bottom

```cangjie
public var bottom:?VerticalAlignment
```

**Function:** Sets the bottom alignment of the component.

**Type:** ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var center

```cangjie
public var center:?VerticalAlignment
```

**Function:** Sets the vertical center alignment of the component.

**Type:** ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var left

```cangjie
public var left:?HorizontalAlignment
```

**Function:** Sets the left alignment of the component.

**Type:** ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var middle

```cangjie
public var middle:?HorizontalAlignment
```

**Function:** Sets the horizontal center alignment of the component.

**Type:** ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var right

```cangjie
public var right:?HorizontalAlignment
```

**Function:** Sets the right alignment of the component.

**Type:** ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var top

```cangjie
public var top:?VerticalAlignment
```

**Function:** Sets the top alignment of the component.

**Type:** ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment)

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(?HorizontalAlignment, ?HorizontalAlignment, ?HorizontalAlignment, ?VerticalAlignment, ?VerticalAlignment, ?VerticalAlignment, Bias)

```cangjie
public init(left!: ?HorizontalAlignment = None, right!: ?HorizontalAlignment = None,
    middle!: ?HorizontalAlignment = None, top!: ?VerticalAlignment = None,
    bottom!: ?VerticalAlignment = None, center!: ?VerticalAlignment = None,
    bias!: Bias = Bias()
)
```

**Function:** Constructs an AlignRuleOption object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| left | ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment) | No | None | Sets the left alignment of the component. |
| right | ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment) | No | None | Sets the right alignment of the component. |
| middle | ?[HorizontalAlignment](./cj-common-types.md#class-horizontalalignment) | No | None | Sets the horizontal center alignment of the component. |
| top | ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment) | No | None | Sets the top alignment of the component. |
| bottom | ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment) | No | None | Sets the bottom alignment of the component. |
| center | ?[VerticalAlignment](./cj-common-types.md#class-verticalalignment) | No | None | Sets the vertical center alignment of the component. |
| bias | [Bias](#class-bias) | No | Bias() | Sets the offset for component alignment. |

### class Bias

```cangjie
public class Bias {
    public var horizontal: Float32, 
    public var vertical: Float32, 
    public init(horizontal!: Float32, vertical!: Float32)
}
```

**Function:** Sets the offset for component alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var horizontal

```cangjie
public var horizontal: Float32
```

**Function:** Sets the horizontal offset of the component.

**Type:** Float32

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var vertical

```cangjie
public var vertical: Float32
```

**Function:** Sets the vertical offset of the component.

**Type:** Float32

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Float32, Float32)

```cangjie
public init(horizontal!: Float32 = 0.5, vertical!: Float32 = 0.5)
```

**Function:** Constructs a Bias object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| horizontal | Float32 | No | 0.5 | Sets the horizontal offset of the component. |
| vertical | Float32 | No | 0.5 | Sets the vertical offset of the component. |