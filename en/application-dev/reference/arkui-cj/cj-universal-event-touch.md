# Touch Event

Triggered when a finger presses, slides, or lifts on a component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func stopPropagation()

```cangjie
public func stopPropagation(): Unit
```

**Function:** Stops event propagation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## Permission List

None

## func onTouch((TouchEvent) -> Unit)

```cangjie
public func onTouch(event: (TouchEvent) -> Unit): This
```

**Function:** Triggered by finger touch actions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([TouchEvent](#class-touchevent))->Unit | Yes | - | Callback function triggered by finger touch actions. |

## Basic Type Definitions

### class TouchEvent

```cangjie
public class TouchEvent {
    public var eventType: TouchType
    public var touches: Array<TouchObject>
    public var changedTouches: Array<TouchObject>
    public var timestamp: Int64
    public var target: EventTarget
    public var source: SourceType
}
```

**Function:** In non-event injection scenarios, `changedTouches` contains points resampled at the screen refresh rate, while `touches` contains points reported at the device refresh rate. The data in `changedTouches` may differ from that in `touches`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var changedTouches

```cangjie
public var changedTouches: Array<TouchObject>
```

**Function:** Information about currently changed fingers.

**Type:** Array\<[TouchObject](#class-touchobject)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var eventType

```cangjie
public var eventType: TouchType
```

**Function:** Type of touch event.

**Type:** [TouchType](cj-common-types.md#enum-touchtype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var source

```cangjie
public var source: SourceType
```

**Function:** Event input device.

**Type:** [SourceType](cj-common-types.md#enum-sourcetype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var target

```cangjie
public var target: EventTarget
```

**Function:** Object of the touched element.

**Type:** [EventTarget](cj-universal-event-click.md#class-eventtarget)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Timestamp relative to system startup time, in milliseconds.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var touches

```cangjie
public var touches: Array<TouchObject>
```

**Function:** Information about all fingers.

**Type:** Array\<[TouchObject](#class-touchobject)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### class TouchObject

```cangjie
public class TouchObject {
    public var touchType: TouchType
    public var id: Int32
    public var screenX: Float64
    public var screenY: Float64
    public var x: Float64
    public var y: Float64
    public init(touchType: TouchType, id: Int32, screenX: Float64, screenY: Float64, x: Float64, y: Float64)
}
```

**Function:** Represents the type of information about currently changed fingers.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var id

```cangjie
public var id: Int32
```

**Function:** Unique identifier of the finger.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var screenX

```cangjie
public var screenX: Float64
```

**Function:** X-coordinate of the touch point relative to the left edge of the device screen.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var screenY

```cangjie
public var screenY: Float64
```

**Function:** Y-coordinate of the touch point relative to the top edge of the device screen.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var touchType

```cangjie
public var touchType: TouchType
```

**Function:** Type of touch event.

**Type:** [TouchType](cj-common-types.md#enum-touchtype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var x

```cangjie
public var x: Float64
```

**Function:** X-coordinate of the touch point relative to the left edge of the touched element.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var y

```cangjie
public var y: Float64
```

**Function:** Y-coordinate of the touch point relative to the top edge of the touched element.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(TouchType, Int32, Float64, Float64, Float64, Float64)

```cangjie
public init(touchType: TouchType, id: Int32, screenX: Float64, screenY: Float64, x: Float64, y: Float64)
```

**Function:** Constructs a touch event type object.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| touchType | [TouchType](cj-common-types.md#enum-touchtype) | Yes | - | Type of touch event. |
| id | Int32 | Yes | - | Unique identifier of the finger. |
| screenX | Float64 | Yes | - | X-coordinate of the touch point relative to the left edge of the device screen. |
| screenY | Float64 | Yes | - | Y-coordinate of the touch point relative to the top edge of the device screen. |
| x | Float64 | Yes | - | X-coordinate of the touch point relative to the left edge of the touched element. |
| y | Float64 | Yes | - | Y-coordinate of the touch point relative to the top edge of the touched element. |