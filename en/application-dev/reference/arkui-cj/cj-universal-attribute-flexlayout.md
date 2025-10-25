# Flex Layout

> **Note:**
>
> Only takes effect when the parent component is [Flex](./cj-row-column-stack-flex.md), [Column](./cj-row-column-stack-column.md), [Row](./cj-row-column-stack-row.md), or [GridRow](./cj-grid-layout-gridrow.md) (specifically for [alignSelf](./cj-universal-attribute-flexlayout.md#func-alignselfitemalign)).

## Import Module

```cangjie
import kit.ArkUI.*
```

## func alignSelf(ItemAlign)

```cangjie
public func alignSelf(value: ItemAlign): This
```

**Function:** Sets the alignment of the component itself.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ItemAlign](./cj-common-types.md#enum-itemalign) | Yes | - | Item alignment. |

## func flexBasis(Length)

```cangjie
public func flexBasis(value: Length): This
```

**Function:** Sets the flex basis size of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The basis size of the component in the main axis direction of the parent container. |

## func flexGrow(Float64)

```cangjie
public func flexGrow(value: Float64): This
```

**Function:** Sets the flex grow factor of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Grayscale value. |

## func flexGrow(Int64)

```cangjie
public func flexGrow(value: Int64): This
```

**Function:** Sets the flex grow factor of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int64 | Yes | - | The proportion of the remaining space in the main axis direction of the parent container allocated to the component where this attribute is set.<br>Range: (0, +∞), Initial value: 0. |

## func flexShrink(Float64)

```cangjie
public func flexShrink(value: Float64): This
```

**Function:** Sets the flex shrink factor of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Hue rotation angle. |

## func flexShrink(Int64)

```cangjie
public func flexShrink(value: Int64): This
```

**Function:** Sets the flex shrink factor of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int64 | Yes | - | The proportion of the compressed size of the parent container allocated to the component where this attribute is set.<br>Initial value: 0 when the parent container is Column or Row.<br>Initial value: 1 when the parent container is Flex. |