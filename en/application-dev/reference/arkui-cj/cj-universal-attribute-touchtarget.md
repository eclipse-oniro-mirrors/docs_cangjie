# Touch Hot Zone Settings

Applicable to components that support generic click events, generic touch events, and generic gesture handling.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func responseRegion(Rectangle)

```cangjie
public func responseRegion(value: Rectangle): This
```

**Function:** Sets the response region of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Rectangle](./cj-common-types.md#class-rectangle) | Yes | - | Response region rectangle. |

## func responseRegion(Array\<Rectangle>)

```cangjie
public func responseRegion(value: Array<Rectangle>): This
```

**Function:** Sets the response region array for the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[Rectangle](./cj-common-types.md#class-rectangle)> | Yes | - | Array of rectangles. |