# Dimension Settings

Configure dimension-related properties such as component width, height, size, padding, and margin.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func width(Option\<Length>)

```cangjie
func width(value: Option<Length>): T
```

**Function:** Sets the width of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Option\<[Length](./cj-common-types.md#interface-length)> | Yes | - | Component width |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func height(?Length)

```cangjie
func height(value: Option<Length>): T
```

**Function:** Sets the height of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Option\<[Length](./cj-common-types.md#interface-length)> | Yes | - | Component height |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func size(?Length, ?Length)

```cangjie
func size(width!: ?Length, height!: ?Length): T
```

**Function:** Sets the dimensions of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Component width<br>Initial value: 0.0.vp. |
| height | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Component height<br>Initial value: 0.0.vp. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func padding(?Length)

```cangjie
func padding(value: ?Length): T
```

**Function:** Sets the padding of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Component padding |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func padding(?Length, ?Length, ?Length, ?Length)

```cangjie
func padding(top!: ?Length, right!: ?Length, bottom!: ?Length, left!: ?Length): T
```

**Function:** Sets the padding for each side of a component individually.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Top padding<br>Initial value: 0.vp. |
| right | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Right padding<br>Initial value: 0.vp. |
| bottom | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Bottom padding<br>Initial value: 0.vp. |
| left | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Left padding<br>Initial value: 0.vp. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func margin(?Length)

```cangjie
func margin(value: ?Length): T
```

**Function:** Sets the margin of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Component margin |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func margin(?Length, ?Length, ?Length, ?Length)

```cangjie
func margin(top!: ?Length, right!: ?Length, bottom!: ?Length, left!: ?Length): T
```

**Function:** Sets the margin for each side of a component individually.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Top margin<br>Initial value: 0.vp. |
| right | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Right margin<br>Initial value: 0.vp. |
| bottom | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Bottom margin<br>Initial value: 0.vp. |
| left | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter** Left margin<br>Initial value: 0.vp. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func layoutWeight(?Int32)

```cangjie
func layoutWeight(value: ?Int32): T
```

**Function:** Sets the layout weight of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Int32 | Yes | - | Component layout weight<br>Initial value: 0. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func aspectRatio(Float64)

```cangjie
func aspectRatio(value: Float64): T
```

**Function:** Sets the aspect ratio of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Component aspect ratio |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func displayPriority(?Int32)

```cangjie
func displayPriority(value: ?Int32): T
```

**Function:** Sets the display priority of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Int32 | Yes | - | Component display priority<br>Initial value: 1. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func responseRegion(?Rectangle)

```cangjie
func responseRegion(value: ?Rectangle): T
```

**Function:** Sets the response region of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Rectangle](./cj-common-types.md#class-rectangle) | Yes | - | Component response region<br>Initial value: [Rectangle()]. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |

## func responseRegion(?Array\<Rectangle>)

```cangjie
func responseRegion(value: ?Array<Rectangle>): T
```

**Function:** Sets the response region array of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Array\<[Rectangle](./cj-common-types.md#class-rectangle)> | Yes | - | Component response region array<br>Initial value: [Rectangle()]. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns generic method interface type |