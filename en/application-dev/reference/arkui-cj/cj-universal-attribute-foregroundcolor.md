# Foreground Color Settings

Sets the foreground color of a component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func foregroundColor(ColoringStrategy)

```cangjie
public func foregroundColor(value: ColoringStrategy): This
```

**Function:** Sets the foreground color strategy.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ColoringStrategy](./cj-common-types.md#enum-coloringstrategy) | Yes | - | Color strategy. |

## func foregroundColor(ResourceColor)

```cangjie
public func foregroundColor(value: ResourceColor): This
```

**Function:** Sets the foreground color of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The foreground color of the component or setting the foreground color based on intelligent color picking strategy. Property animation is not supported. |