# Component Content Filling Mode

Used to determine how the final animated component content is rendered on the component during width/height animations.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func renderFit(?RenderFit)

```cangjie
func renderFit(fitMode: ?RenderFit): T
```

**Function:** Sets the component content filling mode during width/height animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fitMode | ?[RenderFit](./cj-common-types.md#enum-renderfit)  | Yes  | - | The component content filling mode during width/height animations. <br/>Initial value: RenderFit.TopLeft. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |