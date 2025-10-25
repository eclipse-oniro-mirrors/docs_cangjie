# Click Event

A click event refers to an event triggered when a component is clicked.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func onClick((ClickEvent) -> Unit)

```cangjie
public func onClick(event: (ClickEvent) -> Unit): This
```

**Function:** Triggered when the component is clicked.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | ([ClickEvent](#class-clickevent))->Unit | Yes | - | Callback function triggered when the component is clicked. |


## class ClickEvent

```cangjie
public class ClickEvent {
    public var x: Float64
    public var y: Float64
    public var timestamp: Int64
    public var source: SourceType
    public var target: EventTarget
    public var windowX: Float64
    public var windowY: Float64
    public var displayX: Float64
    public var displayY: Float64
}
```

**Function:** Describes the type of click event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var displayX

```cangjie
public var displayX: Float64
```

**Function:** Marks the horizontal absolute coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var displayY

```cangjie
public var displayY: Float64
```

**Function:** Marks the vertical absolute coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var source

```cangjie
public var source: SourceType
```

**Function:** Identifies the type of device that triggered the click.

**Type:** [SourceType](cj-common-types.md#enum-sourcetype)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var target

```cangjie
public var target: EventTarget
```

**Function:** The display area of the element object that triggered the event.

**Type:** [EventTarget](#class-eventtarget)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Records the time interval between the event occurrence and system startup.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var windowX

```cangjie
public var windowX: Float64
```

**Function:** Locates the horizontal coordinate of the click point relative to the top-left corner of the application window.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var windowY

```cangjie
public var windowY: Float64
```

**Function:** Locates the vertical coordinate of the click point relative to the top-left corner of the application window.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float64
```

**Function:** Records the horizontal position coordinate of the click point within the element.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float64
```

**Function:** Records the vertical position coordinate of the click point within the element.

**Type:** Float64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## class EventTarget

```cangjie
public class EventTarget {
    public var area: Area
    public init(area: Area)
}
```

**Function:** Event target object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var area

```cangjie
public var area: Area
```

**Function:** Event target area.

**Type:** [Area](./cj-common-types.md#class-area)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Area)

```cangjie
public init(area: Area)
```

**Function:** Constructs an EventTarget object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| area | [Area](./cj-common-types.md#class-area) | Yes | - | Event target area. |