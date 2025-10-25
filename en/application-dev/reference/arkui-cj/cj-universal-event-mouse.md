# Mouse Events

When a single action triggers multiple events, the order of events is fixed, and mouse events are transmitted by default.

> Note:
>
> Currently, only external mouse triggers are supported.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Permission List

None

## func onHover((Bool) -> Unit)

```cangjie
public func onHover(event: (Bool) -> Unit): This
```

**Function:** Triggered when the mouse hovers over the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | (Bool)->Unit | Yes | - | Callback function triggered when the mouse hover state changes. |

## func onMouse((MouseEvent) -> Unit)

```cangjie
public func onMouse(event: (MouseEvent) -> Unit): This
```

**Function:** Triggered when the component is clicked by a mouse button or when the mouse moves over the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | ([MouseEvent](#class-mouseevent))->Unit | Yes | - | Callback triggered when the component is clicked by a mouse button or when the mouse moves over the component. The MouseEvent parameter includes the timestamp when the event was triggered, the mouse button, the action, the coordinates of the click point relative to the entire screen, and the coordinates of the click point relative to the current component. |

## class MouseEvent

```cangjie
public class MouseEvent {
    public var timestamp: Int64
    public var screenX: Float64
    public var screenY: Float64
    public var x: Float64
    public var y: Float64
    public var button: MouseButton
    public var action: MouseAction
    public init(timestamp: Int64, screenX: Float64, screenY: Float64, x: Float64, y: Float64, button: MouseButton,
        action: MouseAction)
}
```

**Function:** Object used to describe mouse events.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var action

```cangjie
public var action: MouseAction
```

**Function:** Event action.

**Type:** [MouseAction](./cj-common-types.md#enum-mouseaction)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var button

```cangjie
public var button: MouseButton
```

**Function:** Mouse button.

**Type:** [MouseButton](./cj-common-types.md#enum-mousebutton)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var screenX

```cangjie
public var screenX: Float64
```

**Function:** X-coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var screenY

```cangjie
public var screenY: Float64
```

**Function:** Y-coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Timestamp when the event was triggered.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float64
```

**Function:** X-coordinate of the click point relative to the top-left corner of the current component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float64
```

**Function:** Y-coordinate of the click point relative to the top-left corner of the current component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Int64, Float64, Float64, Float64, Float64, MouseButton, MouseAction)

```cangjie
public init(timestamp: Int64, screenX: Float64, screenY: Float64, x: Float64, y: Float64, button: MouseButton,
    action: MouseAction)
```

**Function:** Constructs an object of the mouse event type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| timestamp | Int64 | Yes | - | Timestamp when the event was triggered. |
| screenX | Float64 | Yes | - | X-coordinate of the click point relative to the top-left corner of the screen. |
| screenY | Float64 | Yes | - | Y-coordinate of the click point relative to the top-left corner of the screen. |
| x | Float64 | Yes | - | X-coordinate of the click point relative to the top-left corner of the current component. |
| y | Float64 | Yes | - | Y-coordinate of the click point relative to the top-left corner of the current component. |
| button | [MouseButton](./cj-common-types.md#enum-mousebutton) | Yes | - | Mouse button. |
| action | [MouseAction](./cj-common-types.md#enum-mouseaction) | Yes | - | Event action. |