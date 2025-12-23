# ohos.display (Screen Properties)

Provides screen property-related functionalities.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func getAllDisplays()

```cangjie
public func getAllDisplays(): Array<Display>
```

**Description:** Gets all displays.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Array\<[Display](#class-display)>|Returns the result of all displays.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |1400001|Invalid display or screen.|
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*

func getAllDisplaysExample() {
    try {
        let displayClass: Array<Display> = getAllDisplays()
        if (displayClass.size > 0) {
            println(displayClass[0].name)
        }
    } catch (exception: Exception) {
        AppLog.error(exception.toString())
    }
}
```

## func getCurrentFoldCreaseRegion()

```cangjie
public func getCurrentFoldCreaseRegion(): FoldCreaseRegion
```

**Description:** Gets the fold crease region in the current display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[FoldCreaseRegion](#class-foldcreaseregion)|Returns the fold crease region in the current display mode.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
func getCurrentFoldCreaseRegionExample() {
    try {
        let region = getCurrentFoldCreaseRegion()
        println(region.displayId)
    } catch (exception: Exception) {
        AppLog.error(exception.toString())
    }
}
```

## func getDefaultDisplaySync()

```cangjie
public func getDefaultDisplaySync(): Display
```

**Description:** Gets the default display.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[Display](#class-display)|Returns the result of the display.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |1400001|Invalid display or screen.|
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
func getDefaultDisplaySyncExample() {
    try {
        let displayClass: Display = getDefaultDisplaySync()
        println(displayClass.name)
    } catch (exception: Exception) {
        AppLog.error(exception.toString())
    }
}
```

## func getFoldDisplayMode()

```cangjie
public func getFoldDisplayMode(): FoldDisplayMode
```

**Description:** Gets the display mode of the foldable device.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[FoldDisplayMode](#enum-folddisplaymode)|Returns the display mode of the foldable device.|

## func getFoldStatus()

```cangjie
public func getFoldStatus(): FoldStatus
```

**Description:** Gets the current fold status of the foldable device.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|[FoldStatus](#enum-foldstatus)|Returns the fold status of the device.|

## func isFoldable()

```cangjie
public func isFoldable(): Bool
```

**Description:** Checks whether the device is foldable.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|true indicates the device is foldable.|

## func off(ListenerType)

```cangjie
public func off(listenerType: ListenerType): Unit
```

**Description:** Disables all listeners for display device changes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|listenerType|[ListenerType](#enum-listenertype)|Yes|-|Type of the listening event.|

## func off(ListenerType, Callback1Argument\<FoldDisplayMode>)

```cangjie
public func off(listenerType: ListenerType, callback: Callback1Argument<FoldDisplayMode>): Unit
```

**Description:** Unregisters the callback for fold display mode changes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|listenerType|[ListenerType](#enum-listenertype)|Yes|-|Event for fold display mode changes.|
|callback|Callback1Argument\<[FoldDisplayMode](#enum-folddisplaymode)>|Yes|-|Callback for returning the current fold display mode.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |401|Parameter error. Possible causes:<br> 1. Mandatory parameters are left unspecified. <br>2. Incorrect parameter types. |
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
class TestCallback <: Callback1Argument<FoldDisplayMode> {
    public init() {}
    public open func invoke(value: FoldDisplayMode): Unit {
        AppLog.info(
            "Display fold status changed, current fold status: " + match (value) {
                case FoldDisplayModeUnknown => "FoldDisplayModeUnknown"
                case FoldDisplayModeFull => "FoldDisplayModeFull"
                case FoldDisplayModeMain => "FoldDisplayModeMain"
                case FoldDisplayModeSub => "FoldDisplayModeSub"
                case FoldDisplayModeCoordination => "FoldDisplayModeCoordination"
                case _ => "Failed to get fold display mode."
            })
    }
}
let testCallback = TestCallback()
try {
    var temp: Unit = off(ListenerTypeFoldDisplayModeChange, testCallback)
} catch (e: BusinessException) {
    AppLog.error(exception.toString())
}
```

## func off(ListenerType, Callback1Argument\<FoldStatus>)

```cangjie
public func off(listenerType: ListenerType, callback: Callback1Argument<FoldStatus>): Unit
```

**Description:** Unregisters the callback for fold status changes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|listenerType|[ListenerType](#enum-listenertype)|Yes|-|Event for fold status changes.|
|callback|Callback1Argument\<[FoldStatus](#enum-foldstatus)>|Yes|-|Callback for returning the current fold status of the device.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |401|Parameter error. Possible causes:<br> 1. Mandatory parameters are left unspecified. <br>2. Incorrect parameter types. |
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
class TestCallback <: Callback1Argument<FoldStatus> {
    public init() {}
    public open func invoke(value: FoldStatus): Unit {
        AppLog.info(
            "Display fold status changed, current fold status: " + match (value) {
                case FoldDisplayModeUnknown => "FoldDisplayModeUnknown"
                case FoldDisplayModeFull => "FoldDisplayModeFull"
                case FoldDisplayModeMain => "FoldDisplayModeMain"
                case FoldDisplayModeSub => "FoldDisplayModeSub"
                case FoldDisplayModeCoordination => "FoldDisplayModeCoordination"
                case _ => "Failed to get fold display mode."
            })
    }
}
let testCallback = TestCallback()
try {
    var temp: Unit = off(ListenerTypeFoldStatusChange, testCallback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

## func on(ListenerType, Callback1Argument\<FoldDisplayMode>)

```cangjie
public func on(listenerType: ListenerType, callback: Callback1Argument<FoldDisplayMode>): Unit
```

**Description:** Registers the callback for fold display mode changes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|listenerType|[ListenerType](#enum-listenertype)|Yes|-|Event for fold display mode changes.|
|callback|Callback1Argument\<[FoldDisplayMode](#enum-folddisplaymode)>|Yes|-|Callback for returning the current fold display mode.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |401|Parameter error. Possible causes:<br> 1. Mandatory parameters are left unspecified. <br>2. Incorrect parameter types. |
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
class TestCallback <: Callback1Argument<FoldDisplayMode> {
    public init() {}
    public open func invoke(value: FoldDisplayMode): Unit {
        AppLog.info(
            "Display fold status changed, current fold status: " + match (value) {
                case FoldDisplayModeUnknown => "FoldDisplayModeUnknown"
                case FoldDisplayModeFull => "FoldDisplayModeFull"
                case FoldDisplayModeMain => "FoldDisplayModeMain"
                case FoldDisplayModeSub => "FoldDisplayModeSub"
                case FoldDisplayModeCoordination => "FoldDisplayModeCoordination"
                case _ => "Failed to get fold display mode."
            })
    }
}
let testCallback = TestCallback()
try {
    var temp: Unit = on(ListenerTypeFoldDisplayModeChange, testCallback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

## func on(ListenerType, Callback1Argument\<FoldStatus>)

```cangjie
public func on(listenerType: ListenerType, callback: Callback1Argument<FoldStatus>): Unit
```

**Description:** Registers the callback for fold status changes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|listenerType|[ListenerType](#enum-listenertype)|Yes|-|Event for fold status changes.|
|callback|Callback1Argument\<[FoldStatus](#enum-foldstatus)>|Yes|-|Callback for returning the current fold status of the device.|

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  |Error Code|Description|
  |:----|:----|
  |401|Parameter error. Possible causes:<br> 1. Mandatory parameters are left unspecified. <br>2. Incorrect parameter types. |
  |1400003|This display manager service works abnormally.|

**Example:**

```cangjie
import ohos.display.*
class TestCallback <: Callback1Argument<FoldStatus> {
    public init() {}
    public open func invoke(value: FoldStatus): Unit {
        AppLog.info(
            "Display fold status changed, current fold status: " + match (value) {
                case FoldDisplayModeUnknown => "FoldDisplayModeUnknown"
                case FoldDisplayModeFull => "FoldDisplayModeFull"
                case FoldDisplayModeMain => "FoldDisplayModeMain"
                case FoldDisplayModeSub => "FoldDisplayModeSub"
                case FoldDisplayModeCoordination => "FoldDisplayModeCoordination"
                case _ => "Failed to get fold display mode."
            })
    }
}
let testCallback = TestCallback()
try {
    var temp: Unit = on(ListenerTypeFoldStatusChange, testCallback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```## class CutoutInfo

```cangjie
public class CutoutInfo {
    public let boundingRects: Array<Rect>
    public let waterfallDisplayAreaRects: WaterfallDisplayAreaRects
    public init(
    boundingRects!: Array<Rect>,
    waterfallDisplayAreaRects!: WaterfallDisplayAreaRects
    )
}
```

**Function:** Information about the display notch.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let boundingRects

```cangjie
public let boundingRects: Array<Rect>
```

**Function:** Bounding rectangles of the display notch area.

**Type:** Array\<[Rect](#class-rect)>

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let waterfallDisplayAreaRects

```cangjie
public let waterfallDisplayAreaRects: WaterfallDisplayAreaRects
```

**Function:** Rectangles of the curved edges on waterfall display.

**Type:** [WaterfallDisplayAreaRects](#class-waterfalldisplayarearects)

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### init(Array\<Rect>, WaterfallDisplayAreaRects)

```cangjie
public init(
    boundingRects!: Array<Rect>,
    waterfallDisplayAreaRects!: WaterfallDisplayAreaRects
)
```

**Function:** Constructor for CutoutInfo.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| boundingRects | Array\<[Rect](#class-rect)> | Yes | - | **Named parameter.** Array of bounding rectangles for the notch area. |
| waterfallDisplayAreaRects | [WaterfallDisplayAreaRects](#class-waterfalldisplayarearects) | Yes | - | **Named parameter.** Rectangles of the curved edges on waterfall display. |

## class Display

```cangjie
public class Display {
}
```

**Function:** Defines display properties. These properties do not update automatically.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop alive

```cangjie
public prop alive: Bool
```

**Function:** Whether the display is active.

**Type:** Bool

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop densityDpi

```cangjie
public prop densityDpi: Float64
```

**Function:** Display density in pixels, representing the scaling factor between physical and logical pixels. The value is 1.0 for low-resolution displays.

**Type:** Float64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop densityPixels

```cangjie
public prop densityPixels: Float64
```

**Function:** Display resolution, measured in pixels per inch (PPI).

**Type:** Float64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop height

```cangjie
public prop height: Int64
```

**Function:** Display height in pixels.

**Type:** Int64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop id

```cangjie
public prop id: Int64
```

**Function:** Display ID.

**Type:** Int64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop name

```cangjie
public prop name: String
```

**Function:** Display name.

**Type:** String

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop orientation

```cangjie
public prop orientation: Orientation
```

**Function:** Display orientation.

**Type:** [Orientation](#enum-orientation)

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop refreshRate

```cangjie
public prop refreshRate: UInt32
```

**Function:** Refresh rate in Hz.

**Type:** UInt32

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop rotation

```cangjie
public prop rotation: UInt32
```

**Function:** Enumeration value for display rotation degrees.
- Value 0: 0° clockwise rotation.
- Value 1: 90° clockwise rotation.
- Value 2: 180° clockwise rotation.
- Value 3: 270° clockwise rotation.

**Type:** UInt32

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop scaledDensity

```cangjie
public prop scaledDensity: Float64
```

**Function:** Text scaling density for the display.

**Type:** Float64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop state

```cangjie
public prop state: DisplayState
```

**Function:** Display state.

**Type:** [DisplayState](#enum-displaystate)

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop width

```cangjie
public prop width: Int32
```

**Function:** Display width in pixels.

**Type:** Int32

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop xDpi

```cangjie
public prop xDpi: Float64
```

**Function:** DPI on the x-axis.

**Type:** Float64

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### prop yDpi

```cangjie
public prop yDpi: Float32
```

**Function:** Dpi on the y-axis.

**Type:** Float32

**Accessibility:** Read-only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### func getCutoutInfo()

```cangjie
public func getCutoutInfo(): CutoutInfo
```

**Function:** Retrieves the notch information of the display.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [CutoutInfo](#class-cutoutinfo) | Returns the notch information of the display. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Window Error Codes](./cj-errorcode-window.md).

  | Error Code | Description |
  |:----|:----|
  | 1400001 | Invalid display or screen. |
  | 1400003 | This display manager service works abnormally. |

**Example:**

```cangjie
import ohos.display.*

func getCutoutInfoExample() {
    try {
        let displayClass = getDefaultDisplaySync()
        let cutout = displayClass.getCutoutInfo()
        println(cutout.boundingRects.size)
    } catch (exception: Exception) {
        AppLog.error(exception.toString())
    }
}
```

## class FoldCreaseRegion

```cangjie
public class FoldCreaseRegion {
    public let creaseRects: Array<Rect>
    public let displayId: UInt32
    public init(
    displayId!: UInt32,
    creaseRects!: Array<Rect>
    )
}
```

**Function:** Fold crease region.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### let creaseRects

```cangjie
public let creaseRects: Array<Rect>
```

**Function:** Crease region.

**Type:** Array\<[Rect](#class-rect)>

**Accessibility:** Read-only

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### let displayId

```cangjie
public let displayId: UInt32
```

**Function:** Display ID, identifying the screen where the crease is located.

**Type:** UInt32

**Accessibility:** Read-only

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### init(UInt32, Array\<Rect>)

```cangjie
public init(
    displayId!: UInt32,
    creaseRects!: Array<Rect>
)
```

**Function:** Constructor for FoldCreaseRegion.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| displayId | UInt32 | Yes | - | **Named parameter.** Display ID. |
| creaseRects | Array\<[Rect](#class-rect)> | Yes | - | **Named parameter.** Crease region. |## class Rect

```cangjie
public class Rect {
    public var height: UInt32
    public var left: Int32
    public var top: Int32
    public var width: UInt32
    public init(
    left!: Int32,
    top!: Int32,
    width!: UInt32,
    height!: UInt32
    )
}
```

**Function:** Rectangle.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### var height

```cangjie
public var height: UInt32
```

**Function:** Rectangle height in pixels.

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### var left

```cangjie
public var left: Int32
```

**Function:** X-axis coordinate of the rectangle's top-left vertex in pixels.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### var top

```cangjie
public var top: Int32
```

**Function:** Y-axis coordinate of the rectangle's top-left vertex in pixels.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### var width

```cangjie
public var width: UInt32
```

**Function:** Rectangle width in pixels.

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### init(Int32, Int32, UInt32, UInt32)

```cangjie
public init(
    left!: Int32,
    top!: Int32,
    width!: UInt32,
    height!: UInt32
)
```

**Function:** Rect constructor.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| left | Int32 | Yes | - | **Named parameter.** Left boundary coordinate of the rectangle. |
| top | Int32 | Yes | - | **Named parameter.** Top boundary coordinate of the rectangle. |
| width | UInt32 | Yes | - | **Named parameter.** Width of the rectangle. |
| height | UInt32 | Yes | - | **Named parameter.** Height of the rectangle. |

## class WaterfallDisplayAreaRects

```cangjie
public class WaterfallDisplayAreaRects {
    public let bottom: Rect
    public let left: Rect
    public let right: Rect
    public let top: Rect
    public init(
    left!: Rect,
    top!: Rect,
    right!: Rect,
    bottom!: Rect
    )
}
```

**Function:** Curved area rectangles for waterfall screens.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let bottom

```cangjie
public let bottom: Rect
```

**Function:** Size of the bottom curved area in a waterfall screen.

**Type:** [Rect](#class-rect)

**Access:** Read-Only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let left

```cangjie
public let left: Rect
```

**Function:** Size of the left curved area in a waterfall screen.

**Type:** [Rect](#class-rect)

**Access:** Read-Only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let right

```cangjie
public let right: Rect
```

**Function:** Size of the right curved area in a waterfall screen.

**Type:** [Rect](#class-rect)

**Access:** Read-Only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### let top

```cangjie
public let top: Rect
```

**Function:** Size of the top curved area in a waterfall screen.

**Type:** [Rect](#class-rect)

**Access:** Read-Only

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### init(Rect, Rect, Rect, Rect)

```cangjie
public init(
    left!: Rect,
    top!: Rect,
    right!: Rect,
    bottom!: Rect
)
```

**Function:** WaterfallDisplayAreaRects constructor.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| left | [Rect](#class-rect) | Yes | - | **Named parameter.** Left curved area. |
| top | [Rect](#class-rect) | Yes | - | **Named parameter.** Top curved area. |
| right | [Rect](#class-rect) | Yes | - | **Named parameter.** Right curved area. |
| bottom | [Rect](#class-rect) | Yes | - | **Named parameter.** Bottom curved area. |

## enum DisplayState

```cangjie
public enum DisplayState <: Equatable<DisplayState> {
    | StateUnknown
    | StateOff
    | StateOn
    | StateDoze
    | StateDozeSuspend
    | StateVr
    | StateOnSuspend
    | ...
}
```

**Function:** Enumeration of display states.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parent Type:**

- Equatable\<[DisplayState](#enum-displaystate)>

### StateUnknown

```cangjie
StateUnknown
```

**Function:** Unknown state.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateOff

```cangjie
StateOff
```

**Function:** Screen is off.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateOn

```cangjie
StateOn
```

**Function:** Screen is on.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateDoze

```cangjie
StateDoze
```

**Function:** Screen is in doze mode but updates for important system messages.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateDozeSuspend

```cangjie
StateDozeSuspend
```

**Function:** Screen is in doze mode without updates.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateVr

```cangjie
StateVr
```

**Function:** VR mode.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### StateOnSuspend

```cangjie
StateOnSuspend
```

**Function:** Screen is on but not updating.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

### operator func !=(DisplayState)

```cangjie
public operator func !=(other: DisplayState): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DisplayState](#enum-displaystate) | Yes | - | Another DisplayState instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if not equal. |

### operator func ==(DisplayState)

```cangjie
public operator func ==(other: DisplayState): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.WindowManager.WindowManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DisplayState](#enum-displaystate) | Yes | - | Another DisplayState instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if equal. |

## enum FoldDisplayMode

```cangjie
public enum FoldDisplayMode <: Equatable<FoldDisplayMode> {
    | FoldDisplayModeUnknown
    | FoldDisplayModeFull
    | FoldDisplayModeMain
    | FoldDisplayModeSub
    | FoldDisplayModeCoordination
    | ...
}
```

**Function:** Enumeration of foldable display modes.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parent Type:**

- Equatable\<[FoldDisplayMode](#enum-folddisplaymode)>

### FoldDisplayModeUnknown

```cangjie
FoldDisplayModeUnknown
```

**Function:** Unknown display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### FoldDisplayModeFull

```cangjie
FoldDisplayModeFull
```

**Function:** Full-screen display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### FoldDisplayModeMain

```cangjie
FoldDisplayModeMain
```

**Function:** Main screen display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### FoldDisplayModeSub

```cangjie
FoldDisplayModeSub
```

**Function:** Secondary screen display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### FoldDisplayModeCoordination

```cangjie
FoldDisplayModeCoordination
```

**Function:** Coordinated display mode.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

### operator func !=(FoldDisplayMode)

```cangjie
public operator func !=(other: FoldDisplayMode): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FoldDisplayMode](#enum-folddisplaymode) | Yes | - | Another FoldDisplayMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if not equal. |

### operator func ==(FoldDisplayMode)

```cangjie
public operator func ==(other: FoldDisplayMode): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.Window.SessionManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FoldDisplayMode](#enum-folddisplaymode) | Yes | - | Another FoldDisplayMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if equal. ||类型|说明|
|:----|:----|
|Bool|Comparison result, returns true when equal.|  

## enum Orientation  

```cangjie  
public enum Orientation <: Equatable<Orientation> {  
    | Portrait  
    | Landscape  
    | PortraitInverted  
    | LandscapeInverted  
    | ...  
}  
```  

**Description:** Enumerates screen orientations.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

**Parent Type:**  

- Equatable\<[Orientation](#enum-orientation)>  

### Portrait  

```cangjie  
Portrait  
```  

**Description:** Portrait mode.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

### Landscape  

```cangjie  
Landscape  
```  

**Description:** Landscape mode.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

### PortraitInverted  

```cangjie  
PortraitInverted  
```  

**Description:** Inverted portrait mode.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

### LandscapeInverted  

```cangjie  
LandscapeInverted  
```  

**Description:** Inverted landscape mode.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

### operator func !=(Orientation)  

```cangjie  
public operator func !=(other: Orientation): Bool  
```  

**Description:** Inequality comparison operator.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| other | [Orientation](#enum-orientation) | Yes | - | Another Orientation instance to compare. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Comparison result, returns true when not equal. |  

### operator func ==(Orientation)  

```cangjie  
public operator func ==(other: Orientation): Bool  
```  

**Description:** Equality comparison operator.  

**System Capability:** SystemCapability.WindowManager.WindowManager.Core  

**Since:** 22  

**Parameters:**  

| Parameter | Type | Required | Default | Description |  
|:---|:---|:---|:---|:---|  
| other | [Orientation](#enum-orientation) | Yes | - | Another Orientation instance to compare. |  

**Return Value:**  

| Type | Description |  
|:----|:----|  
| Bool | Comparison result, returns true when equal. || Type       | Description                          |
|:-----------|:------------------------------------|
| Bool       | Comparison result, returns true when equal. |