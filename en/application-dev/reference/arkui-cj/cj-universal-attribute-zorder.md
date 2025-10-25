# Z-Order Control

The Z-order of a component determines its stacking order.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func zIndex(Int32)

```cangjie
public func zIndex(value: Int32): This
```

**Function:** Sets the Z-axis level of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Determines the display hierarchy among sibling components within the same container. A higher zIndex value indicates a higher display level, meaning components with larger zIndex values will overlay those with smaller values. Initial value: 0. |