# Dimension Settings

Configure the width, height, and margins of components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func constraintSize(Length, Length, Length, Length)

```cangjie
public func constraintSize(minWidth!: Length = 0.vp, maxWidth!: Length = (Float64.Inf).vp,
    minHeight!: Length = 0.vp, maxHeight!: Length = (Float64.Inf).vp): This
```

**Function:** Sets dimension constraints for the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| minWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Minimum width. |
| maxWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | (Float64.Inf).vp | Maximum width. |
| minHeight | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Minimum height. |
| maxHeight | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | (Float64.Inf).vp | Maximum height. |

## func height(Option\<Length>)

```cangjie
public func height(value: Option<Length>): This
```

**Function:** Sets the height of the component. If omitted, the height will be determined by the content. If the child component's height exceeds the parent's, it will be drawn outside the parent's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | Yes | - | Component height.<br>Unit: vp. |

## func layoutWeight(Int32)

```cangjie
public func layoutWeight(value: Int32): This
```

**Function:** Sets the layout weight of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | When the parent container's dimensions are determined, child elements with layoutWeight will distribute the main axis space according to their weights, ignoring their own size settings, and adaptively fill the remaining space.<br>**Note:** Only effective in [Row](./cj-common-types.md#row)/[Column](./cj-common-types.md#column)/[Flex](./cj-row-column-stack-flex.md#flex) layouts. The value must be a number ≥ 0 or a string convertible to a number. If any child element has layoutWeight > 0, flexShrink and flexGrow layouts will be disabled for all children. |

## func margin(Length)

```cangjie
public func margin(value: Length): This
```

**Function:** Sets the margins of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Component margins, applied uniformly to all four sides.<br>Unit: vp. |

## func margin(Length, Length, Length, Length)

```cangjie
public func margin(top!: Length = 0.vp, right!: Length = 0.vp, bottom!: Length = 0.vp, left!: Length = 0.vp): This
```

**Function:** Sets the margins for all four sides of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Top margin: distance from the component's top to external elements. |
| right | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Right margin: distance from the component's right boundary to external elements. |
| bottom | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Bottom margin: distance from the component's bottom to external elements. |
| left | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Left margin: distance from the component's left boundary to external elements. |

## func padding(Length)

```cangjie
public func padding(value: Length): This
```

**Function:** Sets the padding of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Component padding, applied uniformly to all four sides.<br>Unit: vp. |

## func padding(Length, Length, Length, Length)

```cangjie
public func padding(top!: Length = 0.vp, right!: Length = 0.vp, bottom!: Length = 0.vp, left!: Length = 0.vp): This
```

**Function:** Sets the padding for all four sides of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Top padding: distance from internal elements to the component's top.<br>Default: 0.vp. |
| right | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Right padding: distance from internal elements to the component's right boundary.<br>Default: 0.vp. |
| bottom | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Bottom padding: distance from internal elements to the component's bottom.<br>Default: 0.vp. |
| left | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Left padding: distance from internal elements to the component's left boundary.<br>Default: 0.vp. |

> **Note:**
>
> When setting padding as a percentage, all four sides use the parent container's width as the base value.

## func size(Length, Length)

```cangjie
public func size(width!: Length, height!: Length): This
```

**Function:** Sets the dimensions of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Component width.<br>Unit: vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Component height.<br>Unit: vp. |

## func width(Option\<Length>)

```cangjie
public func width(value: Option<Length>): This
```

**Function:** Sets the width of the component. If omitted, the width will be determined by the content. If the child component's width exceeds the parent's, it will be drawn outside the parent's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | Yes | - | Component width.<br>Default unit: vp. |