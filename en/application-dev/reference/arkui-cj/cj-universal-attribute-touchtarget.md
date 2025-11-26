# Touch Hotspot Settings

Set the responsive hot zone of a component. In the ArkUI development framework, when handling touch and mouse events, a touch test is performed between the press point and the component's responsive hot zone before the event is triggered, in order to collect the components that need to respond to the event.

## Import Module

```cangjie
import kit.ArkUI.*
```

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
