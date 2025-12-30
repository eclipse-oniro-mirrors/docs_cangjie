# Visibility Control

Controls whether a component is visible.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func visibility(?Visibility)

```cangjie
func visibility(value: ?Visibility): T
```

**Function:** Sets the visibility of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Visibility](./cj-common-types.md#enum-visibility) | Yes | - | Controls the display or hiding of the current component. Conditional rendering can be used as an alternative depending on specific scenario requirements. Initial value: Visibility.Visible |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |