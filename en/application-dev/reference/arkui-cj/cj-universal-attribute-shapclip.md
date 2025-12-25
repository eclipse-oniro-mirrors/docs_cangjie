# Shape Clipping

Used for clipping and masking components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func clip(?Bool)

```cangjie
public func clip(value: ?Bool): T
```

**Function:** Whether to clip the areas of child components that exceed the bounds of the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | \- | Whether to clip according to the parent container's edge contour. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |


## func clipShape(?BaseShape)

```cangjie
func clipShape(value: ?BaseShape): T
```

**Function:** Clips the current component according to the specified shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[BaseShape](./cj-apis-shape.md#class-baseshape) | Yes | \- | The specified shape used to clip the current component. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |


## func maskShape(BaseShape)

```cangjie
public func maskShape(value: BaseShape): T
```

**Function:** Adds a mask of the specified shape to the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [BaseShape](./cj-apis-shape.md#class-baseshape) | Yes | \- | The specified shape used to mask the current component. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |