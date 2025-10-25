# Layout Constraints

Constrains component display effects through aspect ratio and display priority.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func aspectRatio(Float64)

```cangjie
public func aspectRatio(value: Float64): This
```

**Function:** Specifies the aspect ratio of the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | The aspect ratio value. |

## func displayPriority(Int32)

```cangjie
public func displayPriority(value: Int32): This
```

**Function:** Sets the display priority of the current component within a layout container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The display priority of the current component within the layout container.<br> Default: 1. <br> **Note:** <br> Only takes effect in [Row](./cj-row-column-stack-row.md#row)/[Column](./cj-row-column-stack-column.md#column)/[Flex (single-line)](./cj-row-column-stack-flex.md#flex) container components.<br>Decimal places are not considered for priority distinction, meaning numbers within the range [x, x + 1) are treated as having the same priority. For example: 1.0 and 1.9 have the same priority. When all child components have displayPriority ≤ 1, there is no priority distinction. When a child component's displayPriority > 1, higher values indicate higher priority. If parent container space is insufficient, lower-priority child components are hidden. If child components at a certain priority level are hidden, all lower-priority child components will also be hidden. |