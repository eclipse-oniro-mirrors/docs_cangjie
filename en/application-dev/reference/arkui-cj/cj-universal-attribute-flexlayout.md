# Flex Layout

> **Note:**
>
> Only takes effect when the parent component is [Flex](./cj-row-column-stack-flex.md), [Column](./cj-row-column-stack-column.md), [Row](./cj-row-column-stack-row.md), or [GridRow](./cj-grid-layout-gridrow.md) (specifically for [alignSelf](./cj-universal-attribute-flexlayout.md#func-alignselfitemalign)).

## Import Module

```cangjie
import kit.ArkUI.*
```

## func alignSelf(?ItemAlign)

```cangjie
func alignSelf(value: ?ItemAlign): T
```

**Function:** Alignment format of child components along the cross axis of the parent container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ItemAlign](./cj-common-types.md#enum-itemalign) | Yes | - | Alignment format of child components along the cross axis of the parent container, overriding the alignItems setting in Flex, Column, Row, and GridRow layout containers.<br> GridCol can bind the alignsSelf property to change its layout along the cross axis.<br>Initial value: ItemAlign.Auto. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func flexBasis(?Length)

```cangjie
func flexBasis(value: ?Length): T
```

**Function:** Sets the base size of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Base size of the component along the main axis of the parent container.<br>Initial value: 'auto' (indicating that the base size of the component along the main axis is the component's original size).<br>Setting percent is not supported.<br>Value range: (0, +∞), default unit is vp.<br>Abnormal values: The actual layout effect is consistent with 'auto'.|

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func flexGrow(?Float64)

```cangjie
func flexGrow(value: ?Float64): T
```

**Function:** Sets the proportion of remaining space in the parent container allocated to the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Float64 | Yes | - | Proportion of remaining space along the main axis of the parent container allocated to the component where this property is set.<br>Range: (0,+∞), Initial value: 0.0. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func flexGrow(?Int64)

```cangjie
func flexGrow(value: ?Int64): T
```

**Function:** Sets the proportion of remaining space in the parent container allocated to the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Int64 | Yes | - | Proportion of remaining space along the main axis of the parent container allocated to the component where this property is set.<br>Range: (0,+∞), Initial value: 0. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func flexShrink(?Float64)

```cangjie
func flexShrink(value: ?Float64): T
```

**Function:** Sets the proportion of compressed size in the parent container allocated to the component where this property is set. When the parent container is Column or Row, the size along the main axis must be set.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Float64 | Yes | - | Proportion of compressed size in the parent container allocated to the component where this property is set.<br> When the parent container is [Column](./cj-row-column-stack-column.md) or [Row](./cj-row-column-stack-row.md), range: (0,+∞), initial value: 0.0.<br> When the parent container is [Flex](./cj-row-column-stack-flex.md), initial value: 1.0.<br>[constraintSize](./cj-universal-attribute-size.md#func-constraintsizelength-length-length-length) limits the size range of the component. Even if [constraintSize](./cj-universal-attribute-size.md#func-constraintsizelength-length-length-length) is set for [Column](./cj-row-column-stack-column.md) and [Row](./cj-row-column-stack-row.md), when the main axis size ([width](./cj-universal-attribute-size.md#func-widthlength)/[height](./cj-universal-attribute-size.md#func-heightlength)/[size](./cj-universal-attribute-size.md#func-sizelength-length)) is not set, the default layout behavior is followed, adapting to the child component size along the main axis, and flexShrink does not take effect. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func flexShrink(?Int64)

```cangjie
func flexShrink(value: ?Int64): T
```

**Function:** Sets the proportion of compressed size in the parent container allocated to the component where this property is set. When the parent container is Column or Row, the size along the main axis must be set.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Int64 | Yes | - | Proportion of compressed size in the parent container allocated to the component where this property is set.<br> When the parent container is Column or Row, initial value: 0.<br> When the parent container is Flex, initial value: 1. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |