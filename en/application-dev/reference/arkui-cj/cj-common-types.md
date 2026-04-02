# Basic Type Definitions

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This page documents the public type definitions used by the UI framework.

## Import Module

```cangjie
import kit.ArkUI.*
```

## interface CollectionEx\<T>

```cangjie
public interface CollectionEx<T> {
    prop size: Int64
    operator func [](idx: Int64, value!: T): Unit
    operator func [](idx: Int64): T
}
```

**Functionality:** Collection extension interface.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### extend\<T> Array\<T> <: CollectionEx\<T>

```cangjie
extend<T> Array<T> <: CollectionEx<T> {}
```

**Functionality:** Extends generic Array as a subtype of CollectionEx.

### extend\<T> ArrayList\<T> <: CollectionEx\<T>

```cangjie
extend<T> ArrayList<T> <: CollectionEx<T> {}
```

**Functionality:** Extends generic ArrayList as a subtype of CollectionEx.

### prop size

```cangjie
prop size: Int64
```

**Functionality:** Collection size.

**Type:** Int64

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### operator func [](Int64, T)

```cangjie
operator func [](idx: Int64, value!: T): Unit
```

**Functionality:** Sets the element value at the specified index position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:--------|:-------------|:------------|
| idx | Int64 | Yes | - | Element index. |
| value | T | Yes | - | **Named parameter.** Element value. |

### operator func [](Int64)

```cangjie
operator func [](idx: Int64): T
```

**Functionality:** Gets the element value at the specified index position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:--------|:-------------|:------------|
| idx | Int64 | Yes | - | Element index. |

**Return Value:**

| Type | Description |
|:-----|:-----------|
| T | Element value at the specified index position. |

## interface Length

```cangjie
public interface Length {
    prop value: Float64
    prop unitType: LengthUnit
}
```

**Functionality:** Float64, Int64, and AppResource all implement the Length interface type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop value

```cangjie
prop value: Float64
```

**Functionality:** Value of the length property.

**Type:** Float64

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop unitType

```cangjie
prop unitType: LengthUnit
```

**Functionality:** Unit of the length property.

**Type:** [LengthUnit](#enum-lengthunit)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## interface LengthProp

```cangjie
public interface LengthProp {
    prop px: Length
    prop vp: Length
    prop fp: Length
    prop percent: Length
    prop lpx: Length
}
```

**Functionality:** Standard interface for length properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop px

```cangjie
prop px: Length
```

**Functionality:** Length property in px units.

**Type:** [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop vp

```cangjie
prop vp: Length
```

**Functionality:** Length property in vp units.

**Type:** [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop fp

```cangjie
prop fp: Length
```

**Functionality:** Length property in fp units.

**Type:** [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop percent

```cangjie
prop percent: Length
```

**Functionality:** Length property in percentage units.

**Type:** [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### prop lpx

```cangjie
prop lpx: Length
```

**Functionality:** Length property in lpx units.

**Type:** [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## Float64

**Functionality:** The description of the Float64 type definition.

### extend Float64 <: LengthProp & Length

```cangjie
extend Float64 <: LengthProp & Length {}
```

**Functionality:** Extend `Float64` as a subclass of `LengthProp` and `Length`.

#### prop px

```cangjie
public prop px: Length
```

**Functionality:** Length properties in pixels (px).

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop vp

```cangjie
public prop vp: Length
```

**Functionality:** The length attribute in units of vp.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop fp

```cangjie
public prop fp: Length
```

**Functionality:** The length attribute in units of fp.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop percent

```cangjie
public prop percent: Length
```

**Functionality:** Length attribute in percentage.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop lpx

```cangjie
public prop lpx: Length
```

**Functionality:** The length attribute in units of lpx.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop value

```cangjie
public prop value: Float64
```

**Functionality:** The value of the length attribute.

**Type:**  Float64

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop unitType

```cangjie
public prop unitType: LengthUnit
```

**Functionality:** The unit of the length attribute.

**Type:**  [LengthUnit](#enum-lengthunit)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## Int64

**Functionality:** Description of the Int64 type definition.

### extend Int64 <: LengthProp & Length

```cangjie
extend Int64 <: LengthProp & Length {}
```

**Functionality:** Extend Int64 as a subclass of LengthProp and Length.

#### prop px

```cangjie
public prop px: Length
```

**Functionality:** The length attribute in units of px.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop vp

```cangjie
public prop vp: Length
```

**Functionality:** The length attribute in units of vp.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop fp

```cangjie
public prop fp: Length
```

**Functionality:** The length attribute in units of fp.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop percent

```cangjie
public prop percent: Length
```

**Functionality:** Length attribute in percentage.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop lpx

```cangjie
public prop lpx: Length
```

**Functionality:** The length attribute in units of lpx.

**Type:**  [Length](#interface-length)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop value

```cangjie
public prop value: Float64
```

**Functionality:** The value of the length attribute.

**Type:**  Float64

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### prop unitType

```cangjie
public prop unitType: LengthUnit
```

**Functionality:** The unit of the length attribute.

**Type:**  [LengthUnit](#enum-lengthunit)

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## interface ResourceColor

```cangjie
public interface ResourceColor {
    func toUInt32(): UInt32
}
```

**Functionality:** Color, UInt32, Int64, and AppResource all implement the ResourceColor interface type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### extend Int64 <: ResourceColor

```cangjie
extend Int64 <: ResourceColor {
    public func toUInt32(): UInt32
}
```

**Functionality:** Extends Int64 as a subtype of ResourceColor.

#### func toUInt32()

```cangjie
func toUInt32(): UInt32
```

**Functionality:** Converts to UInt32 color value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Return Value:**

| Type | Description |
|:-----|:-----------|
| UInt32 | UInt32 value of ResourceColor. |

### extend UInt32 <: ResourceColor

```cangjie
extend UInt32 <: ResourceColor {
    public func toUInt32(): UInt32
}
```

**Functionality:** Extends UInt32 as a subtype of ResourceColor.

#### func toUInt32()

```cangjie
func toUInt32(): UInt32
```

**Functionality:** Converts to UInt32 color value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Return Value:**

| Type | Description |
|:-----|:-----------|
| UInt32 | UInt32 value of ResourceColor. |

### func toUInt32()

```cangjie
func toUInt32(): UInt32
```

**Functionality:** Converts to UInt32 color value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Return Value:**

| Type | Description |
|:-----|:-----------|
| UInt32 | UInt32 value of ResourceColor. |

## interface ResourceStr

```cangjie
public interface ResourceStr {}
```

**Functionality:** String type, used to describe the types that can be used for string parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## interface TextContentControllerBase

```cangjie
public interface TextContentControllerBase {}
```

**Functionality:** Base interface for text content controllers.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## class Bindable\<T>

```cangjie
public class Bindable<T> {
    public let value: T
    public let onChange: (T) -> Unit
    public init(value: T, onChange: (T) -> Unit)
}
```

**Functionality:** Defines bindable properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### init(T, (T) -> Unit)

```cangjie
public init(value: T, onChange: (T) -> Unit)
```

**Functionality:** Bindable constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---------|:-----|:--------|:-------------|:------------|
| value | T | Yes | - | Value of the bindable property. |
| onChange | (T) -> Unit | Yes | - | Callback function for the bindable property, which will be called when the property changes. |

### let value

```cangjie
public let value: T
```

**Functionality:** Defines the value of the bindable property.

**Type:** T

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### let onChange

```cangjie
public let onChange: (T) -> Unit
```

**Functionality:** Callback function for the bindable property, which will be called when the property changes.

**Type:** (T) -> Unit

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22## class LengthMetrics

```cangjie
public class LengthMetrics <: Length {
    public init(value: Float64, unit!: LengthUnit = LengthUnit.Vp)
}
```

**Description:** Represents length attributes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [Length](#interface-length)

### init(Float64, LengthUnit)

```cangjie
public init(value: Float64, unit!: LengthUnit = LengthUnit.Vp)
```

**Description:** Constructor for length attributes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | Length value. |
| unit | [LengthUnit](#enum-lengthunit) | No | LengthUnit.Vp | **Named parameter.** Unit of length. |

### prop value

```cangjie
public prop value: Float64
```

**Description:** The value of the length attribute.

**Type:** Float64

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop unitType

```cangjie
public prop unitType: LengthUnit
```

**Description:** The unit of the length attribute.

**Type:** [LengthUnit](#enum-lengthunit)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class Color

```cangjie
public class Color <: ResourceColor {
    public static let Black: Color = Color(0xff000000)
    public static let Blue: Color = Color(0xff0000ff)
    public static let Gray: Color = Color(0xff808080)
    public static let Green: Color = Color(0xff008000)
    public static let Red: Color = Color(0xffff0000)
    public static let White: Color = Color(0xffffffff)
    public static let Transparent: Color = Color(0, 0, 0, alpha: 0.0)
    public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: ?Float32 = None)
    public init(value: UInt32)
}
```

**Description:** Color type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [ResourceColor](#interface-resourcecolor)

### static let Black

```cangjie
public static let Black: Color = Color(0xff000000)
```

**Description:** Black color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let Blue

```cangjie
public static let Blue: Color = Color(0xff0000ff)
```

**Description:** Blue color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let Gray

```cangjie
public static let Gray: Color = Color(0xff808080)
```

**Description:** Gray color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let Green

```cangjie
public static let Green: Color = Color(0xff008000)
```

**Description:** Green color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let Red

```cangjie
public static let Red: Color = Color(0xffff0000)
```

**Description:** Red color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let White

```cangjie
public static let White: Color = Color(0xffffffff)
```

**Description:** White color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static let Transparent

```cangjie
public static let Transparent: Color = Color(0, 0, 0, alpha: 0.0)
```

**Description:** Transparent color.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(UInt8, UInt8, UInt8, ?Float32)

```cangjie
public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: ?Float32 = None)
```

**Description:** Creates a color using red, green, blue, and alpha values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| red | UInt8 | Yes | - | Red channel value in RGB. |
| green | UInt8 | Yes | - | Green channel value in RGB. |
| blue | UInt8 | Yes | - | Blue channel value in RGB. |
| alpha | ?Float32 | No | None | **Named parameter.** Alpha channel value, range [0.0-1.0]. |

### init(UInt32)

```cangjie
public init(value: UInt32)
```

**Description:** Creates a color using a 32-bit unsigned integer value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | UInt32 | Yes | - | Uint32 color value. The alpha, R, G, and B channels each occupy 8 bits of the input in sequence. If only R, G, and B channels are input, the alpha channel defaults to 0xff. |

### func toUInt32()

```cangjie
public func toUInt32(): UInt32
```

**Description:** Converts to a UInt32 color value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | UInt32 color value. |

## class ReuseParams

```cangjie
public class ReuseParams {
    public init(arr: Array<(String, Any)>)
}
```

**Description:** Parameters for the aboutToReuse lifecycle function, from which developers can obtain the construction parameters of reusable components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Array\<(String, Any)>)

```cangjie
public init(arr: Array<(String, Any)>)
```

**Description:** Creates a ReuseParams object. Typically, developers will not call this.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| arr | Array\<(String, Any)> | Yes | - | Array containing tuples of component construction parameters. |

### func get\<T>(String)

```cangjie
public func get<T>(key: String): ?T
```

**Description:** Retrieves the corresponding construction parameter by key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Name of the construction parameter. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?T | Value of the construction parameter. |

## class KeyEvent

```cangjie
public class KeyEvent {
    public var keyType: KeyType
    public var keyCode: Int32
    public var keyText: String
    public var keySource: KeySource
    public var deviceId: Int64
    public var metaKey: Int32
    public var timestamp: Int64
    public init(keyText: String, keyType: KeyType, keyCode: Int32, keySource: KeySource, metaKey: Int32,
        deviceId: Int64, timestamp: Int64)
}
```

**Description:** Key event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var keyText

```cangjie
public var keyText: String
```

**Description:** Key value of the pressed key.

**Type:** String

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var keyType

```cangjie
public var keyType: KeyType
```

**Description:** Type of the pressed key.

**Type:** [KeyType](./cj-common-types.md#enum-keytype)

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var keyCode

```cangjie
public var keyCode: Int32
```

**Description:** Key code of the pressed key.

**Type:** Int32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var keySource

```cangjie
public var keySource: KeySource
```

**Description:** Type of input device that triggered the current key event.

**Type:** [KeySource](./cj-common-types.md#enum-keysource)

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var metaKey

```cangjie
public var metaKey: Int32
```

**Description:** State of the meta key when the key event occurred. 1 indicates pressed state, 0 indicates unpressed state.

**Type:** Int32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var deviceId

```cangjie
public var deviceId: Int64
```

**Description:** ID of the input device that triggered the current key event.

**Type:** Int64

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**Description:** Timestamp when the key event occurred.

**Type:** Int64

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(String, KeyType, Int32, KeySource, Int32, Int64, Int64)

```cangjie
public init(keyText: String, keyType: KeyType, keyCode: Int32, keySource: KeySource, metaKey: Int32,
        deviceId: Int64, timestamp: Int64)
```

**Description:** Constructs an object of the key event type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyText | String | Yes | - | Key value of the pressed key. |
| keyType | [KeyType](./cj-common-types.md#enum-keytype) | Yes | - | Type of the pressed key. |
| keyCode | Int32 | Yes | - | Key code of the pressed key. |
| keySource | [KeySource](./cj-common-types.md#enum-keysource) | Yes | - | Type of input device that triggered the current key event. |
| metaKey | Int32 | Yes | - | State of the meta key when the key event occurred. 1 indicates pressed state, 0 indicates unpressed state. |
| deviceId | Int64 | Yes | - | ID of the input device that triggered the current key event. |
| timestamp | Int64 | Yes | - | Timestamp when the key event occurred. |## class TouchObject

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

**Description:** Represents the type of finger information that has changed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var id

```cangjie
public var id: Int32
```

**Description:** Unique identifier for the finger.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var screenX

```cangjie
public var screenX: Float64
```

**Description:** X-coordinate of the touch point relative to the left edge of the device screen.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var screenY

```cangjie
public var screenY: Float64
```

**Description:** Y-coordinate of the touch point relative to the top edge of the device screen.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var touchType

```cangjie
public var touchType: TouchType
```

**Description:** Type of touch event.

**Type:** [TouchType](cj-common-types.md#enum-touchtype)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Description:** X-coordinate of the touch point relative to the left edge of the touched element.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Description:** Y-coordinate of the touch point relative to the top edge of the touched element.

**Type:** Float64

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(TouchType, Int32, Float64, Float64, Float64, Float64)

```cangjie
public init(touchType: TouchType, id: Int32, screenX: Float64, screenY: Float64, x: Float64, y: Float64)
```

**Description:** Constructs a touch event type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| touchType | [TouchType](cj-common-types.md#enum-touchtype) | Yes | - | Type of touch event. |
| id | Int32 | Yes | - | Unique identifier for the finger. |
| screenX | Float64 | Yes | - | X-coordinate relative to the left edge of the device screen. |
| screenY | Float64 | Yes | - | Y-coordinate relative to the top edge of the device screen. |
| x | Float64 | Yes | - | X-coordinate relative to the left edge of the touched element. |
| y | Float64 | Yes | - | Y-coordinate relative to the top edge of the touched element. |

## class BaseEvent

```cangjie
abstract sealed class BaseEvent {
    public var target: ?EventTarget
    public var timestamp: Int64
    public var source: ?SourceType
    public var deviceId: ?Int64
}
```

**Description:** Base event type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var target

```cangjie
public var target: ?EventTarget
```

**Description:** The element object that triggered the event.

**Type:** ?[EventTarget](#class-eventtarget)

**Access:** Read-write

**Since:** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**Description:** Event timestamp, representing the time interval since system startup when the event was triggered. Unit: ns.

**Type:** Int64

**Access:** Read-write

**Since:** 22

### var source

```cangjie
public var source: ?SourceType
```

**Description:** Type of input device that generated the event.

**Type:** ?[SourceType](#enum-sourcetype)

**Access:** Read-write

**Since:** 22

### var deviceId

```cangjie
public var deviceId: ?Int64
```

**Description:** ID of the input device that triggered the current event. Initial value: 0, valid range: [0, +∞).

**Type:** ?Int64

**Access:** Read-write

**Since:** 22

## class ClickEvent

```cangjie
public class ClickEvent <: BaseEvent {
    public var displayX: Float64
    public var displayY: Float64
    public var windowX: Float64
    public var windowY: Float64
    public var x: Float64
    public var y: Float64
}
```

**Description:** Describes the type of click event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [BaseEvent](#class-baseevent)

### var displayX

```cangjie
public var displayX: Float64
```

**Description:** Marks the absolute horizontal coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Access:** Read-write

**Since:** 22

### var displayY

```cangjie
public var displayY: Float64
```

**Description:** Marks the absolute vertical coordinate of the click point relative to the top-left corner of the screen.

**Type:** Float64

**Access:** Read-write

**Since:** 22

### var windowX

```cangjie
public var windowX: Float64
```

**Description:** Locates the horizontal coordinate of the click point relative to the top-left corner of the application window.

**Type:** Float64

**Access:** Read-write

**Since:** 22

### var windowY

```cangjie
public var windowY: Float64
```

**Description:** Locates the vertical coordinate of the click point relative to the top-left corner of the application window.

**Type:** Float64

**Access:** Read-write

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Description:** Records the horizontal position coordinate of the click point within the element.

**Type:** Float64

**Access:** Read-write

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Description:** Records the vertical position coordinate of the click point within the element.

**Type:** Float64

**Access:** Read-write

**Since:** 22

## class MouseEvent

```cangjie
public class MouseEvent <: BaseEvent {
    public var button: MouseButton
    public var screenX: Float64
    public var screenY: Float64
    public var x: Float64
    public var y: Float64
    public var action: MouseAction
    public init(timestamp: Int64, screenX: Float64, screenY: Float64, x: Float64, y: Float64, button: MouseButton, action: MouseAction)
}
```

**Description:** An object used to describe mouse events.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [BaseEvent](#class-baseevent)

### var action

```cangjie
public var action: MouseAction
```

**Description:** The event action.

**Type:** [MouseAction](./cj-common-types.md#enum-mouseaction)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var button

```cangjie
public var button: MouseButton
```

**Description:** The mouse button.

**Type:** [MouseButton](./cj-common-types.md#enum-mousebutton)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var screenX

```cangjie
public var screenX: Float64
```

**Description:** The x-coordinate of the touch point relative to the top-left corner of the screen.

**Type:** Float64

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var screenY

```cangjie
public var screenY: Float64
```

**Description:** The y-coordinate of the touch point relative to the top-left corner of the screen.

**Type:** Float64

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: Float64
```

**Description:** The x-coordinate of the touch point relative to the top-left corner of the current component.

**Type:** Float64

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: Float64
```

**Description:** The y-coordinate of the touch point relative to the top-left corner of the current component.

**Type:** Float64

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var action

```cangjie
public var action: MouseAction
```

**Description:** The event action.

**Type:** [MouseAction](./cj-common-types.md#enum-mouseaction)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Int64, Float64, Float64, Float64, Float64, MouseButton, MouseAction)

```cangjie
public init(timestamp: Int64, screenX: Float64, screenY: Float64, x: Float64, y: Float64, button: MouseButton,action: MouseAction)
```

**Description:** Constructs an object of the mouse event type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|timestamp|Int64|Yes|-|The timestamp when the event was triggered.|
|screenX|Float64|Yes|-|The x-coordinate of the touch point relative to the top-left corner of the screen.|
|screenY|Float64|Yes|-|The y-coordinate of the touch point relative to the top-left corner of the screen.|
|x|Float64|Yes|-|The x-coordinate of the touch point relative to the top-left corner of the current component.|
|y|Float64|Yes|-|The y-coordinate of the touch point relative to the top-left corner of the current component.|
|button|[MouseButton](./cj-common-types.md#enum-mousebutton)|Yes|-|The mouse button.|
|action|[MouseAction](./cj-common-types.md#enum-mouseaction)|Yes|-|The event action.|

## class TouchEvent

```cangjie
public class TouchEvent <: BaseEvent {
    public var eventType: TouchType
    public var touches: Array<TouchObject>
    public var changedTouches: Array<TouchObject>
}
```

**Description:** In non-event injection scenarios, `changedTouches` contains points resampled at the screen refresh rate, while `touches` contains points reported at the device refresh rate. The data in `changedTouches` may differ from that in `touches`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [BaseEvent](#class-baseevent)

### var eventType

```cangjie
public var eventType: TouchType
```

**Description:** The type of the touch event.

**Type:** [TouchType](cj-common-types.md#enum-touchtype)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var touches

```cangjie
public var touches: ArrayList<TouchObject>
```

**Description:** Information about all fingers.

**Type:** ArrayList\<[TouchObject](#class-touchobject)>

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var changedTouches

```cangjie
public var changedTouches: ArrayList<TouchObject>
```

**Description:** Information about the currently changed fingers.

**Type:** ArrayList\<[TouchObject](#class-touchobject)>

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func stopPropagation

```cangjie
public func stopPropagation(): Unit
```

**Description:** Stops event propagation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class EventTarget

```cangjie
public class EventTarget {
    public var area: Area
    public init(area: Area)
}
```

**Description:** The event target object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var area

```cangjie
public var area: Area
```

**Description:** The target area of the event.

**Type:** [Area](#class-area)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Area)

```cangjie
public init(area: Area)
```

**Description:** Constructs an EventTarget object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|area|[Area](#class-area)|Yes|-|The target area of the event.|

## class Area

```cangjie
public class Area {
    public var width: Length
    public var height: Length
    public var position: Position
    public var globalPosition: Position
    public init(width: Length, height: Length, position: Position, globalPosition: Position)
}
```

**Description:** The current target area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: Length
```

**Description:** Defines the width of the target element.

**Type:** [Length](./cj-common-types.md#interface-length)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: Length
```

**Description:** Defines the height of the target element.

**Type:** [Length](./cj-common-types.md#interface-length)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var position

```cangjie
public var position: Position
```

**Description:** Defines the relative position of the top-left corner of the target element to the top-left corner of its parent element.

**Type:** [Position](#class-position)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var globalPosition

```cangjie
public var globalPosition: Position
```

**Description:** Defines the position of the top-left corner of the target element relative to the top-left corner of the screen.

**Type:** [Position](#class-position)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Length, Length, Position, Position)

```cangjie
public init(width: Length, height: Length, position: Position, globalPosition: Position)
```

**Description:** Constructs an object of the Area type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|width|[Length](./cj-common-types.md#interface-length)|Yes|-|The width of the target element, in vp.|
|height|[Length](./cj-common-types.md#interface-length)|Yes|-|The height of the target element, in vp.|
|position|[Position](#class-position)|Yes|-|The position of the top-left corner of the target element relative to the top-left corner of its parent element.|
|globalPosition|[Position](#class-position)|Yes|-|The position of the top-left corner of the target element relative to the top-left corner of the page.|

## class Position

```cangjie
public class Position {
    public var x: ?Length
    public var y: ?Length
    public init(x!: ?Length = None, y!: ?Length = None)
}
```

**Description:** Position information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Length
```

**Description:** Defines the x-coordinate.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Length
```

**Description:** Defines the y-coordinate.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length)

```cangjie
public init(x!: ?Length = None, y!: ?Length = None)
```

**Description:** Constructs an object of the Position type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|x|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** The x-coordinate, in vp.|
|y|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** The y-coordinate, in vp.|## class MotionPathOptions

```cangjie
public class MotionPathOptions {
    public var path: ?String
    public var from: ?Float64
    public var to: ?Float64
    public var rotatable: ?Bool
    public init(path!: ?String, from!: ?Float64 = None, to!: ?Float64 = None, rotatable!: ?Bool = None)
}
```

**Function:** Configures animation path options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var path

```cangjie
public var path: ?String
```

**Function:** Sets the animation path.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var from

```cangjie
public var from: ?Float64
```

**Function:** Sets the starting position of the animation path.

**Type:** ?Float64

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var to

```cangjie
public var to: ?Float64
```

**Function:** Sets the ending position of the animation path.

**Type:** ?Float64

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var rotatable

```cangjie
public var rotatable: ?Bool
```

**Function:** Sets whether the animation path is rotatable.

**Type:** ?Bool

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String, ?Float64, ?Float64, ?Bool)

```cangjie
public init(path!: ?String, from!: ?Float64 = None, to!: ?Float64 = None, rotatable!: ?Bool = None)
```

**Function:** Constructs a MotionPathOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | ?String | Yes | - | **Named parameter.** Sets the starting position of the animation path. |
| from | ?Float64 | No | None | **Named parameter.** Sets the starting position of the animation path. Initial value is 0.0. |
| to | ?Float64 | No | None | **Named parameter.** Sets the ending position of the animation path. Initial value is 1.0. |
| rotatable | ?Bool | No | None | **Named parameter.** Sets whether the animation path is rotatable. Initial value is false. |

## class SharedTransitionOptions

```cangjie
public class SharedTransitionOptions {
    public var duration: ?Int32
    public var curve: ?Curve
    public var delay: ?Int32
    public var motionPath: ?MotionPathOptions
    public var zIndex: ?Int32
    public var effectType: ?SharedTransitionEffectType
    public init(duration!: ?Int32 = None, curve!: ?Curve = None, delay!: ?Int32 = None, motionPath!: ?MotionPathOptions = None, zIndex!: ?Int32 = None, effectType!: ?SharedTransitionEffectType = None)
}
```

**Function:** Shared transition options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var duration

```cangjie
public var duration: ?Int32
```

**Function:** Describes the playback duration of the shared element transition animation.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var curve

```cangjie
public var curve: ?Curve
```

**Function:** The animation curve.

**Type:** ?[Curve](#enum-curve)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var delay

```cangjie
public var delay: ?Int32
```

**Function:** Delay before playback.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var motionPath

```cangjie
public var motionPath: ?MotionPathOptions
```

**Function:** Sets the motion path for the shared transition.

**Type:** ?[MotionPathOptions](#class-motionpathoptions)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var zIndex

```cangjie
public var zIndex: ?Int32
```

**Function:** Sets the z-index.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var effectType

```cangjie
public var effectType: ?SharedTransitionEffectType
```

**Function:** The animation effect type.

**Type:** ?[SharedTransitionEffectType](#enum-sharedtransitioneffecttype)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Int32, ?Curve, ?Int32, ?MotionPathOptions, ?Int32, ?SharedTransitionEffectType)

```cangjie
public init(duration!: ?Int32 = None, curve!: ?Curve = None, delay!: ?Int32 = None, motionPath!: ?MotionPathOptions = None, zIndex!: ?Int32 = None, effectType!: ?SharedTransitionEffectType = None)
```

**Function:** Constructs a SharedTransitionOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| duration | ?Int32 | No | None | **Named parameter.** Describes the playback duration of the shared element transition animation.<br>Initial value: 1000.<br>Unit: milliseconds.<br>Value range: [0, +∞). |
| curve | ?[Curve](./cj-common-types.md#enum-curve) | No | None | **Named parameter.** The animation curve.<br>Initial value: Curve.Linear. |
| delay | ?Int32 | No | None | **Named parameter.** Delay before playback.<br>Initial value: 0.<br>Unit: milliseconds. |
| motionPath | ?[MotionPathOptions](#class-motionpathoptions) | No | None | **Named parameter.** Sets the motion path for the shared transition.<br>Initial value: MotionPathOptions(path: ""). |
| zIndex | ?Int32 | No | None | **Named parameter.** Sets the z-index.<br>Value range: (−∞, +∞).<br>Initial value: 0. |
| effectType | ?[SharedTransitionEffectType](./cj-common-types.md#enum-sharedtransitioneffecttype) | No | None | **Named parameter.** The animation effect type.<br>Initial value: SharedTransitionEffectType.Exchange. |

## class AnimateParam

```cangjie
public class AnimateParam {
    public var duration: ?Int32
    public var tempo: ?Float32
    public var curve: ?Curve
    public var delay: ?Int32
    public var iterations: ?Int32
    public var playMode: ?PlayMode
    public var onFinish: Option<() -> Unit>
    public var finishCallbackType: ?FinishCallbackType
    public var expectedFrameRateRange: Option<ExpectedFrameRateRange>
    public init(duration!: ?Int32 = None, tempo!: ?Float32 = None, curve!: ?Curve = None, delay!: ?Int32 = None, iterations!: ?Int32 = None, playMode!: ?PlayMode = None, onFinish!: Option<() -> Unit> = Option.None, finishCallbackType!: ?FinishCallbackType = None, expectedFrameRateRange!: Option<ExpectedFrameRateRange> = Option.None)
}
```

**Function:** Configures animation effect parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var duration

```cangjie
public var duration: ?Int32
```

**Function:** Animation duration in milliseconds. Values less than 0 are treated as 0.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var tempo

```cangjie
public var tempo: ?Float32
```

**Function:** Animation playback speed. Higher values play faster, lower values play slower. A value of 0 disables animation.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var curve

```cangjie
public var curve: ?Curve
```

**Function:** Animation curve.

**Type:** ?[Curve](#enum-curve)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var delay

```cangjie
public var delay: ?Int32
```

**Function:** Animation delay time in milliseconds. Default is no delay.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var iterations

```cangjie
public var iterations: ?Int32
```

**Function:** Number of animation iterations. Default is 1. -1 means infinite iterations. 0 disables animation.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var playMode

```cangjie
public var playMode: ?PlayMode
```

**Function:** Animation play mode. Default is restart from beginning after completion.

**Type:** ?[PlayMode](#enum-playmode)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onFinish

```cangjie
public var onFinish: Option<() -> Unit>
```

**Function:** Callback when animation completes.

**Type:** Option\<() -> Unit>

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var finishCallbackType

```cangjie
public var finishCallbackType: ?FinishCallbackType
```

**Function:** Defines the type of onFinish callback in animations.

**Type:** ?[FinishCallbackType](#enum-finishcallbacktype)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var expectedFrameRateRange

```cangjie
public var expectedFrameRateRange: Option<ExpectedFrameRateRange>
```

**Function:** Sets the expected frame rate for animations.

**Type:** Option<[ExpectedFrameRateRange](#class-expectedframeraterange)>

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Int32, ?Float32, ?Curve, ?Int32, ?Int32, ?PlayMode, Option\<() -> Unit>, ?FinishCallbackType, Option\<ExpectedFrameRateRange>)

```cangjie
public init(duration!: ?Int32 = None, tempo!: ?Float32 = None, curve!: ?Curve = None, delay!: ?Int32 = None, iterations!: ?Int32 = None, playMode!: ?PlayMode = None, onFinish!: Option<() -> Unit> = Option.None, finishCallbackType!: ?FinishCallbackType = None, expectedFrameRateRange!: Option<ExpectedFrameRateRange> = Option.None)
```

**Function:** Constructs an AnimateParam object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| duration | ?Int32 | No | None | **Named parameter.** Animation duration in milliseconds. Values less than 0 are treated as 0.<br>Initial value: 1000.<br>**Note:**<br>1. You can change a property inside an animation closure with duration 0 to achieve the effect of stopping that property's animation.<br>2. Values less than 0 are treated as 0. |
| tempo | ?Float32 | No | None | **Named parameter.** Animation playback speed. Higher values play faster, lower values play slower. A value of 0 disables animation.<br>Initial value: 1.0.<br>Value range: [0, +∞). |
| curve | ?[Curve](./cj-common-types.md#enum-curve) | No | None | **Named parameter.** Animation curve. Initial value: Curve.EaseInOut. |
| delay | ?Int32 | No | None | **Named parameter.** Animation delay time in ms (milliseconds).<br>Initial value: 0.<br>Value range: (−∞, +∞).<br>**Note:**<br>delay≥0 means delayed playback; delay<0 means advanced playback. For delay<0: when the absolute value of delay is less than the actual animation duration, the animation will jump to the state at the time of the absolute value of delay in the first frame after start; when the absolute value of delay is greater than or equal to the actual animation duration, the animation will jump to the end state in the first frame after start. The actual animation duration equals the single animation duration multiplied by the number of iterations. |
| iterations | ?Int32 | No | None | **Named parameter.** Number of animation iterations. -1 means infinite playback. 0 disables animation.<br>Initial value: 1.<br>Value range: [-1, +∞). |
| playMode | ?[PlayMode](./cj-common-types.md#enum-playmode) | No | None | **Named parameter.** Animation play mode. By default, playback restarts from the beginning after completion.<br>Initial value: PlayMode.Normal. |
| onFinish | Option\<() -> Unit> | No | Option.None | **Named parameter.** Callback when animation completes. |
| finishCallbackType | ?[FinishCallbackType](./cj-common-types.md#enum-finishcallbacktype) | No | None | **Named parameter.** Defines the type of onFinish callback in animations.<br>Initial value: FinishCallbackType.Removed. |
| expectedFrameRateRange | Option<[ExpectedFrameRateRange](./cj-animation-animation.md#class-expectedframeraterange)> | No | Option.None | **Named parameter.** Sets the expected frame rate for animations. |

## class HorizontalAlignParam

```cangjie
public class HorizontalAlignParam {
    public var anchor: ?String
    public var align: ?HorizontalAlign
    public init(anchor: ?String, align: ?HorizontalAlign)
}
```

**Function:** Horizontal alignment configuration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var anchor

```cangjie
public var anchor: ?String
```

**Function:** Sets the anchor point for horizontal alignment of components.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var align

```cangjie
public var align: ?HorizontalAlign
```

**Function:** Sets the horizontal alignment mode for components.

**Type:** ?[HorizontalAlign](#enum-horizontalalign)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String, ?HorizontalAlign)

```cangjie
public init(anchor: ?String, align: ?HorizontalAlign)
```

**Function:** Constructs a HorizontalAlignment object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| anchor | ?String | Yes | - | Sets the anchor point for horizontal alignment of components. |
| align | ?[HorizontalAlign](#enum-horizontalalign) | Yes | - | Sets the horizontal alignment mode for components. |

## class VerticalAlignParam

```cangjie
public class VerticalAlignParam {
    public var anchor: ?String
    public var align: ?VerticalAlign
    public init(anchor: ?String, align: ?VerticalAlign)
}
```

**Function:** Vertical alignment configuration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var anchor

```cangjie
public var anchor: ?String
```

**Function:** Sets the anchor point for vertical alignment of components.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var align

```cangjie
public var align: ?VerticalAlign
```

**Function:** Sets the vertical alignment mode for components.

**Type:** ?[VerticalAlign](#enum-verticalalign)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String, ?VerticalAlign)

```cangjie
public init(anchor: ?String, align: ?VerticalAlign)
```

**Function:** Constructs a VerticalAlignment object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| anchor | ?String | Yes | - | Sets the anchor point for vertical alignment of components. |
| align | ?[VerticalAlign](#enum-verticalalign) | Yes | - | Sets the vertical alignment mode for components. |

## class Bias

```cangjie
public class Bias {
    public var horizontal: ?Float32
    public var vertical: ?Float32
    public init(horizontal!: ?Float32 = None, vertical!: ?Float32 = None)
}
```

**Function:** Sets the offset for component alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var horizontal

```cangjie
public var horizontal: ?Float32
```

**Function:** Sets the horizontal offset for components.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var vertical

```cangjie
public var vertical: ?Float32
```

**Function:** Sets the vertical offset for components.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float32, ?Float32)

```cangjie
public init(horizontal!: ?Float32 = None, vertical!: ?Float32 = None)
```

**Function:** Constructs a Bias object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| horizontal | ?Float32 | No | None | **Named parameter.** Sets the horizontal offset for components. Initial value is 0.5. |
| vertical | ?Float32 | No | None | **Named parameter.** Sets the vertical offset for components. Initial value is 0.5. |

## class Fonts

```cangjie
public class Fonts {
    public var size: ?Length
    public var weight: ?FontWeight
    public var family: ?String
    public var style: ?FontStyle
    public init(size!: ?Length = None, weight!: ?FontWeight = None, family!: ?ResourceStr = None, style!: ?FontStyle = None)
}
```

**Function:** Text style configuration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var size

```cangjie
public var size: ?Length
```

**Function:** Sets the text size in fp units.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var weight

```cangjie
public var weight: ?FontWeight
```

**Function:** Sets the font weight of the text.

**Type:** ?[FontWeight](#enum-fontweight)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var family

```cangjie
public var family: ?String
```

**Function:** Sets the font family list for the text.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var style

```cangjie
public var style: ?FontStyle
```

**Function:** Sets the font style of the text.

**Type:** ?[FontStyle](#enum-fontstyle)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?FontWeight, ?ResourceStr, ?FontStyle)

```cangjie
public init(size!: ?Length = None, weight!: ?FontWeight = None, family!: ?ResourceStr = None, style!: ?FontStyle = None)
```

**Function:** Constructs a Fonts object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the text size in fp units when Length is Int64 or Float64. Percentage values are not supported. Initial value is 16.fp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Sets the font weight of the text. Initial value is FontWeight.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the font family list for the text. Multiple fonts can be specified, separated by commas, with priority given in order. Example: 'Arial, HarmonyOS Sans'. Currently supports 'HarmonyOS Sans' font. Initial value is "HarmonyOS Sans". |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Sets the font style of the text. Initial value is FontStyle.Normal. |

## class BorderRadiuses

```cangjie
public class BorderRadiuses {
    public var topLeft: ?Length
    public var topRight: ?Length
    public var bottomLeft: ?Length
    public var bottomRight: ?Length
    public init(topLeft!: ?Length = None, topRight!: ?Length = None, bottomLeft!: ?Length = None, bottomRight!: ?Length = None)
}
```

**Function:** Border radius type, used to describe the corner radius of component borders.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var topLeft

```cangjie
public var topLeft: ?Length
```

**Function:** Top-left corner radius of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var topRight

```cangjie
public var topRight: ?Length
```

**Function:** Top-right corner radius of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottomLeft

```cangjie
public var bottomLeft: ?Length
```

**Function:** Bottom-left corner radius of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottomRight

```cangjie
public var bottomRight: ?Length
```

**Function:** Bottom-right corner radius of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length, ?Length, ?Length)

```cangjie
public init(topLeft!: ?Length = None, topRight!: ?Length = None, bottomLeft!: ?Length = None, bottomRight!: ?Length = None)
```

**Function:** Initializes a BorderRadiuses object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| topLeft | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Top-left corner radius of the component. Initial value is 0.vp. |
| topRight | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Top-right corner radius of the component. Initial value is 0.vp. |
| bottomLeft | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Bottom-left corner radius of the component. Initial value is 0.v2. |
| bottomRight | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Bottom-right corner radius of the component. Initial value is 0.vp. |

## class Margin

```cangjie
public class Margin {
    public init(top!: ?Length = None, right!: ?Length = None, bottom!: ?Length = None, left!: ?Length = None)
}
```

**Function:** Margin type, used to describe the margins of a component in different directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length, ?Length, ?Length)

```cangjie
public init(top!: ?Length = None, right!: ?Length = None, bottom!: ?Length = None, left!: ?Length = None)
```

**Function:** Initializes a Margin object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Top margin, the distance from the component's top to external elements. Initial value is 0.vp. |
| right | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Right margin, the distance from the component's right boundary to external elements. Initial value is 0.vp. |
| bottom | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Bottom margin, the distance from the component's bottom to external elements. Initial value is 0.vp. |
| left | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Left margin, the distance from the component's left boundary to external elements. Initial value is 0.vp. |

## class ShadowOptions

```cangjie
public class ShadowOptions {
    public var radius: ?Float64
    public var shadowType: ?ShadowType
    public var color: ?ResourceColor
    public var offsetX: ?Float64
    public var offsetY: ?Float64
    public var fill: ?Bool
    public init(radius!: ?Float64, shadowType!: ?ShadowType = None, color!: ?ResourceColor = None, offsetX!: ?Float64 = None, offsetY!: ?Float64 = None, fill!: ?Bool = None)
}
```

**Function:** Shadow options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var radius

```cangjie
public var radius: ?Float64
```

**Function:** Sets the blur radius of the shadow.

**Type:** ?Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadowType

```cangjie
public var shadowType: ?ShadowType
```

**Function:** Sets the shadow type.

**Type:** ?[ShadowType](#enum-shadowtype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var color

```cangjie
public var color: ?ResourceColor
```

**Function:** Sets the shadow color.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offsetX

```cangjie
public var offsetX: ?Float64
```

**Function:** Sets the horizontal offset of the shadow.

**Type:** ?Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offsetY

```cangjie
public var offsetY: ?Float64
```

**Function:** Sets the vertical offset of the shadow.

**Type:** ?Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var fill

```cangjie
public var fill: ?Bool
```

**Function:** Whether to fill.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float64, ?ShadowType, ?ResourceColor, ?Float64, ?Float64, ?Bool)

```cangjie
public init(radius!: ?Float64, shadowType!: ?ShadowType = None, color!: ?ResourceColor = None, offsetX!: ?Float64 = None, offsetY!: ?Float64 = None, fill!: ?Bool = None)
```

**Function:** Constructs a ShadowOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| radius | ?Float64 | Yes | - | **Named parameter.** Sets the blur radius of the shadow.<br>Initial value:<br>Before API version 26, the initial value is 0.0; the shadow takes effect when the value is greater than 0.0.<br>From API version 26 onward, the initial value is -1.0; the shadow takes effect when the value is greater than or equal to 0.0. |
| shadowType | ?[ShadowType](./cj-common-types.md#enum-shadowtype) | No | None | **Named parameter.** Sets the shadow type. Initial value is ShadowType.Color. |
| color | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Sets the shadow color. Initial value is Color.Black. |
| offsetX | ?Float64 | No | None | **Named parameter.** Sets the horizontal offset of the shadow. Initial value is 0.0. |
| offsetY | ?Float64 | No | None | **Named parameter.** Sets the vertical offset of the shadow. Initial value is 0.0. |
| fill | ?Bool | No | None | **Named parameter.** Sets whether to fill the shadow. Initial value is false. |

## class Offset

```cangjie
public class Offset {
    public var dx: ?Length
    public var dy: ?Length
    public init(dx: ?Length, dy: ?Length)
}
```

**Function:** Coordinate offset for relative layout completion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var dx

```cangjie
public var dx: ?Length
```

**Function:** Horizontal offset.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var dy

```cangjie
public var dy: ?Length
```

**Function:** Vertical offset.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length)

```cangjie
public init(dx: ?Length, dy: ?Length)
```

**Function:** Constructs an Offset object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| dx | ?[Length](./cj-common-types.md#interface-length) | Yes | - | X-coordinate. |
| dy | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Y-coordinate. |

## class ExpectedFrameRateRange

```cangjie
public class ExpectedFrameRateRange {
    public var min: ?Int32
    public var max: ?Int32
    public var expected: ?Int32
    public init(min!: ?Int32, max!: ?Int32, expected!: ?Int32)
}
```

**Function:** Sets the expected frame rate range for animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var min

```cangjie
public var min: ?Int32
```

**Function:** Minimum frame rate value.

**Type:** ?Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var max

```cangjie
public var max: ?Int32
```

**Function:** Maximum frame rate value.

**Type:** ?Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var expected

```cangjie
public var expected: ?Int32
```

**Function:** Expected frame rate value.

**Type:** ?Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Int32, ?Int32, ?Int32)

```cangjie
public init(min!: ?Int32, max!: ?Int32, expected!: ?Int32)
```

**Function:** Constructs an ExpectedFrameRateRange object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| min | ?Int32 | Yes | - | **Named parameter.** Minimum frame rate value. |
| max | ?Int32 | Yes | - | **Named parameter.** Maximum frame rate value. |
| expected | ?Int32 | Yes | - | **Named parameter.** Expected frame rate value. |

## class AlignRuleOption

```cangjie
public class AlignRuleOption {
    public var left: ?HorizontalAlignParam
    public var right: ?HorizontalAlignParam
    public var middle: ?HorizontalAlignParam
    public var top: ?VerticalAlignParam
    public var bottom: ?VerticalAlignParam
    public var center: ?VerticalAlignParam
    public var bias: ?Bias
    public init(left!: ?HorizontalAlignParam = None, right!: ?HorizontalAlignParam = None, middle!: ?HorizontalAlignParam = None, top!: ?VerticalAlignParam = None, bottom!: ?VerticalAlignParam = None, center!: ?VerticalAlignParam = None, bias!: ?Bias = None)
}
```

**Function:** Sets component alignment rule options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var left

```cangjie
public var left: ?HorizontalAlignParam
```

**Function:** Sets the left alignment of the component.

**Type:** ?[HorizontalAlignParam](#class-horizontalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var right

```cangjie
public var right: ?HorizontalAlignParam
```

**Function:** Sets the right alignment of the component.

**Type:** ?[HorizontalAlignParam](#class-horizontalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var middle

```cangjie
public var middle: ?HorizontalAlignParam
```

**Function:** Sets the horizontal center alignment of the component.

**Type:** ?[HorizontalAlignParam](#class-horizontalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var top

```cangjie
public var top: ?VerticalAlignParam
```

**Function:** Sets the top alignment of the component.

**Type:** ?[VerticalAlignParam](#class-verticalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottom

```cangjie
public var bottom: ?VerticalAlignParam
```

**Function:** Sets the bottom alignment of the component.

**Type:** ?[VerticalAlignParam](#class-verticalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var center

```cangjie
public var center: ?VerticalAlignParam
```

**Function:** Sets the vertical center alignment of the component.

**Type:** ?[VerticalAlignParam](#class-verticalalignparam)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bias

```cangjie
public var bias: ?Bias
```

**Function:** Sets the alignment offset of the component.

**Type:** ?[Bias](#class-bias)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?HorizontalAlignParam, ?HorizontalAlignParam, ?HorizontalAlignParam, ?VerticalAlignParam, ?VerticalAlignParam, ?VerticalAlignParam, ?Bias)

```cangjie
public init(left!: ?HorizontalAlignParam = None, right!: ?HorizontalAlignParam = None, middle!: ?HorizontalAlignParam = None, top!: ?VerticalAlignParam = None, bottom!: ?VerticalAlignParam = None, center!: ?VerticalAlignParam = None, bias!: ?Bias = None)
```

**Function:** Constructs an AlignRuleOption object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| left | ?[HorizontalAlignParam](#class-horizontalalignparam) | No | None | **Named parameter.** Sets the left alignment of the component. |
| right | ?[HorizontalAlignParam](#class-horizontalalignparam) | No | None | **Named parameter.** Sets the right alignment of the component. |
| middle | ?[HorizontalAlignParam](#class-horizontalalignparam) | No | None | **Named parameter.** Sets the horizontal center alignment of the component. |
| top | ?[VerticalAlignParam](#class-verticalalignparam) | No | None | **Named parameter.** Sets the top alignment of the component. |
| bottom | ?[VerticalAlignParam](#class-verticalalignparam) | No | None | **Named parameter.** Sets the bottom alignment of the component. |
| center | ?[VerticalAlignParam](#class-verticalalignparam) | No | None | **Named parameter.** Sets the vertical center alignment of the component. |
| bias | ?[Bias](#class-bias) | No | None | **Named parameter.** Sets the alignment offset of the component. Initial value is Bias(). |## class EdgeStyles

```cangjie
public class EdgeStyles {
    public var top: ?BorderStyle
    public var right: ?BorderStyle
    public var bottom: ?BorderStyle
    public var left: ?BorderStyle
    public init(top!: ?BorderStyle = None, right!: ?BorderStyle = None, bottom!: ?BorderStyle = None, left!: ?BorderStyle = None)
}
```

**Function:** Border styles used to describe the styling of a component's four edges.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var top

```cangjie
public var top: ?BorderStyle
```

**Function:** Sets the top border style of a component.

**Type:** ?[BorderStyle](#enum-borderstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var right

```cangjie
public var right: ?BorderStyle
```

**Function:** Sets the right border style of a component.

**Type:** ?[BorderStyle](#enum-borderstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var bottom

```cangjie
public var bottom: ?BorderStyle
```

**Function:** Sets the bottom border style of a component.

**Type:** ?[BorderStyle](#enum-borderstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var left

```cangjie
public var left: ?BorderStyle
```

**Function:** Sets the left border style of a component.

**Type:** ?[BorderStyle](#enum-borderstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?BorderStyle, ?BorderStyle, ?BorderStyle, ?BorderStyle)

```cangjie
public init(top!: ?BorderStyle = None, right!: ?BorderStyle = None, bottom!: ?BorderStyle = None, left!: ?BorderStyle = None)
```

**Function:** Constructs an EdgeStyles object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| top | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | No | None | **Named parameter.** Top border style of the component. Initial value is BorderStyle.Solid. |
| right | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | No | None | **Named parameter.** Right border style of the component. Initial value is BorderStyle.Solid. |
| bottom | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | No | None | **Named parameter.** Bottom border style of the component. Initial value is BorderStyle.Solid. |
| left | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | No | None | **Named parameter.** Left border style of the component. Initial value is BorderStyle.Solid. |

## class MultiShadowOptions

```cangjie
public open class MultiShadowOptions {
    public var radius: ?Length
    public var offsetX: ?Length
    public var offsetY: ?Length
    protected init(radius: ?Length, offsetX: ?Length, offsetY: ?Length)
}
```

**Function:** Multiple shadow options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var radius

```cangjie
public var radius: ?Length
```

**Function:** Shadow blur radius.
Unit: vp.
<p>**NOTE:**
<br>Values less than or equal to 0 will be treated as default values.
</p>

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offsetX

```cangjie
public var offsetX: ?Length
```

**Function:** Sets the horizontal offset of the shadow.
Unit: vp.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offsetY

```cangjie
public var offsetY: ?Length
```

**Function:** Sets the vertical offset of the shadow.
Unit: vp.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length, ?Length)

```cangjie
protected init(radius: ?Length, offsetX: ?Length, offsetY: ?Length)
```

**Function:** Constructs a MultiShadowOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| radius | ?[Length](./cj-common-types.md#interface-length) | Yes | - | - |
| offsetX | ?[Length](./cj-common-types.md#interface-length) | Yes | - | - |
| offsetY | ?[Length](./cj-common-types.md#interface-length) | Yes | - | - |

## class PickerTextStyle

```cangjie
public class PickerTextStyle {
    public var color: ?ResourceColor
    public var font: ?Font
    public init(color!: ?ResourceColor = None, font!: ?Font = None)
}
```

**Function:** Picker text style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var color

```cangjie
public var color: ?ResourceColor
```

**Function:** Sets the text color of the picker.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var font

```cangjie
public var font: ?Font
```

**Function:** Sets the text font of the picker.

**Type:** ?[Font](#class-font)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceColor, ?Font)

```cangjie
public init(color!: ?ResourceColor = None, font!: ?Font = None)
```

**Function:** Constructs a PickerTextStyle object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| color | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Sets the text color of the picker. |
| font | ?[Font](#class-font) | No | None | **Named parameter.** Sets the text font of the picker. |

## class Font

```cangjie
public class Font {
    public var size: ?Length
    public var weight: ?FontWeight
    public var family: ?ResourceStr
    public var style: ?FontStyle
    public init(size!: ?Length = None, weight!: ?FontWeight = None, family!: ?ResourceStr = None, style!: ?FontStyle = None)
}
```

**Function:** Font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var size

```cangjie
public var size: ?Length
```

**Function:** Sets the text size using fp units.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var weight

```cangjie
public var weight: ?FontWeight
```

**Function:** Sets the font weight of the text.

**Type:** ?[FontWeight](#enum-fontweight)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var family

```cangjie
public var family: ?ResourceStr
```

**Function:** Sets the font family list of the text.

**Type:** ?[ResourceStr](#interface-resourcestr)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var style

```cangjie
public var style: ?FontStyle
```

**Function:** Sets the font style of the text.

**Type:** ?[FontStyle](#enum-fontstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?FontWeight, ?ResourceStr, ?FontStyle)

```cangjie
public init(size!: ?Length = None, weight!: ?FontWeight = None, family!: ?ResourceStr = None, style!: ?FontStyle = None)
```

**Function:** Constructs a Font object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the text size. When Length is Int64 or Float64, fp units are used. Percentage settings are not supported. Initial value is 16.fp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Sets the font weight of the text. Initial value is FontWeight.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the font family list of the text. Multiple fonts can be specified, separated by commas, with priority given in order. Example: 'Arial, HarmonyOS Sans'. Initial value is "HarmonyOS Sans". |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Sets the font style of the text. Initial value is FontStyle.Normal. |

## class BlurOptions

```cangjie
public class BlurOptions {
    public var grayscale: ?VArray<Float32, $2>
    public init(grayscale: ?VArray<Float32, $2>)
}
```

**Function:** Grayscale blur parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var grayscale

```cangjie
public var grayscale: ?VArray<Float32, $2>
```

**Function:** Grayscale blur parameters, with value range [0, 127].

**Type:** ?VArray<Float32, $2>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(VArray\<Float32, $2>)

```cangjie
public init(grayscale: ?VArray<Float32, $2>)
```

**Function:** Constructs a BlurOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| grayscale | ?VArray<Float32, $2> | Yes | - | Grayscale blur parameters, with value range [0, 127]. |## class ForegroundBlurStyleOptions

```cangjie
public class ForegroundBlurStyleOptions {
    public var colorMode: ?ThemeColorMode
    public var adaptiveColor: ?AdaptiveColor
    public var blurOptions: ?BlurOptions
    public var scale: ?Float32
    public init(colorMode!: ?ThemeColorMode = None, adaptiveColor!: ?AdaptiveColor = None, blurOptions!: ?BlurOptions = None, scale!: ?Float32 = None)
}
```

**Function:** Content blur options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var colorMode

```cangjie
public var colorMode: ?ThemeColorMode
```

**Function:** The dark/light color mode used for content blur effect.

**Type:** ?[ThemeColorMode](#enum-themecolormode)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var adaptiveColor

```cangjie
public var adaptiveColor: ?AdaptiveColor
```

**Function:** The color sampling mode used for content blur effect.

**Type:** ?[AdaptiveColor](#enum-adaptivecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var blurOptions

```cangjie
public var blurOptions: ?BlurOptions
```

**Function:** Grayscale blur parameters.

**Type:** ?[BlurOptions](#class-bluroptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var scale

```cangjie
public var scale: ?Float32
```

**Function:** The intensity of content blur effect. Value range: [0.0, 1.0].

**Type:** ?Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ThemeColorMode, ?AdaptiveColor, ?BlurOptions, ?Float32)

```cangjie
public init(colorMode!: ?ThemeColorMode = None, adaptiveColor!: ?AdaptiveColor = None, blurOptions!: ?BlurOptions = None, scale!: ?Float32 = None)
```

**Function:** Constructs a ForegroundBlurStyleOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|colorMode|?[ThemeColorMode](./cj-common-types.md#enum-themecolormode)|No|None|**Named parameter.** The dark/light color mode used for content blur effect. Initial value: ThemeColorMode.System.|
|adaptiveColor|?[AdaptiveColor](./cj-common-types.md#enum-adaptivecolor)|No|None|**Named parameter.** The color sampling mode used for content blur effect. Initial value: AdaptiveColor.Default.|
|blurOptions|?[BlurOptions](#class-bluroptions)|No|None|**Named parameter.** Grayscale blur parameters. Initial value: BlurOptions([0.0, 0.0]).|
|scale|?Float32|No|None|**Named parameter.** The intensity of content blur effect.<br>Value range: [0.0, 1.0]. Initial value: 1.0.|

## class PopupButton

```cangjie
public class PopupButton {
    public init(value!: ?String, action!: () -> Unit)
}
```

**Function:** Constructs a popup button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String, () -> Unit)

```cangjie
public init(value!: ?String, action!: () -> Unit)
```

**Function:** Constructs a popup button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|value|?String|Yes|-|**Named parameter.** The text content of the button.|
|action|() -> Unit|Yes|-|**Named parameter.** The click event handler of the button.|

## class PopupStateChangeParam

```cangjie
public class PopupStateChangeParam {
    public var isVisible: Bool
    public init(value: Bool)
}
```

**Function:** The click event of the button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var isVisible

```cangjie
public var isVisible: Bool
```

**Function:** Whether the popup is visible.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Bool)

```cangjie
public init(value: Bool)
```

**Function:** Sets the popup state parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|value|Bool|Yes|-|Whether the popup is visible.|

## class PopupOptions

```cangjie
public class PopupOptions {
    public var message: ?String
    public var placement: ?Placement
    public var primaryButton: ?PopupButton
    public var secondaryButton: ?PopupButton
    public var onStateChange: ?(PopupStateChangeParam) -> Unit
    public var arrowOffset: ?Length
    public var showInSubWindow: ?Bool
    public var mask: ?ResourceColor
    public var messageOptions: ?PopupMessageOptions
    public var targetSpace: ?Length
    public var enableArrow: ?Bool
    public var offset: ?Position
    public var popupColor: ?ResourceColor
    public var autoCancel: ?Bool
    public var width: ?Length
    public var arrowPointPosition: Option<ArrowPointPosition>
    public var arrowWidth: ?Length
    public var arrowHeight: ?Length
    public var radius: ?Length
    public var shadow: ?ShadowStyle
    public var backgroundBlurStyle: ?BlurStyle
    public var transition: ?TransitionEffect
    public var onWillDismiss: ?(DismissPopupAction) -> Unit
    public var followTransformOfTarget: ?Bool
    public init(
        message!: ?String,
        placement!: ?Placement = Option.None,
        primaryButton!: ?PopupButton = None,
        secondaryButton!: ?PopupButton = None,
        onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
        arrowOffset!: ?Length = None,
        showInSubWindow!: ?Bool = None,
        mask!: ?Color = None,
        messageOptions!: ?PopupMessageOptions = None,
        targetSpace!: ?Length = None,
        enableArrow!: ?Bool = None,
        offset!: ?Position = None,
        popupColor!: ?Color = None,
        autoCancel!: ?Bool = None,
        width!: ?Length = None,
        arrowPointPosition!: ?ArrowPointPosition = None,
        arrowWidth!: ?Length = None,
        arrowHeight!: ?Length = None,
        radius!: ?Length = None,
        shadow!: ?ShadowStyle = None,
        backgroundBlurStyle!: ?BlurStyle = Option.None,
        transition!: ?TransitionEffect = Option.None,
        onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None,
        followTransformOfTarget!: ?Bool = None
    )
}
```

**Function:** Parameters for the popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var message

```cangjie
public var message: ?String
```

**Function:** Sets the content of the popup message.

**Type:** ?String

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var placement

```cangjie
public var placement: ?Placement
```

**Function:** Sets the display position of the popup component relative to the target. Default value: Placement.Bottom. If both placementOnTop and placement are set, the placement setting takes effect.

**Type:** ?[Placement](#enum-placement)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var primaryButton

```cangjie
public var primaryButton: ?PopupButton
```

**Function:** Sets the first button. value: The text of the primary button in the popup. action: The callback function when the primary button is clicked.

**Type:** ?[PopupButton](#class-popupbutton)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var secondaryButton

```cangjie
public var secondaryButton: ?PopupButton
```

**Function:** Sets the second button. value: The text of the secondary button in the popup. action: The callback function when the secondary button is clicked.

**Type:** ?[PopupButton](#class-popupbutton)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onStateChange

```cangjie
public var onStateChange: ?(PopupStateChangeParam) -> Unit
```

**Function:** Sets the callback for popup state changes, with the parameter being the current display state of the popup.

**Type:** ?([PopupStateChangeParam](#class-popupstatechangeparam)) -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowOffset

```cangjie
public var arrowOffset: ?Length
```

**Function:** Sets the offset of the popup arrow at the popup position. When the arrow is above or below the bubble, a value of 0 means the arrow is at the far left, and the offset is the distance from the arrow to the far left, defaulting to center. When the arrow is to the left or right of the bubble, the offset is the distance from the arrow to the top, defaulting to center. If displayed at the screen edge, the bubble will automatically shift left or right, with the arrow always pointing to the bound component when the value is 0.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** Sets whether to display the bubble in a sub-window. Default value: false (not displayed).

**Type:** ?Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var mask

```cangjie
public var mask: ?ResourceColor
```

**Function:** Sets the color of the mask layer.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var messageOptions

```cangjie
public var messageOptions: ?PopupMessageOptions
```

**Function:** Sets the text parameters for the popup message.

**Type:** ?[PopupMessageOptions](#class-popupmessageoptions)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var targetSpace

```cangjie
public var targetSpace: ?Length
```

**Function:** Sets the gap between the popup and the target.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableArrow

```cangjie
public var enableArrow: ?Bool
```

**Function:** Sets whether to display the arrow. Default value: true. When there is insufficient space on the page to fully avoid the bubble, the bubble will cover the component and the arrow will not be displayed.

**Type:** ?Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: ?Position
```

**Function:** Sets the offset of the popup component relative to the display position set by placement. Percentage values are not supported.

**Type:** ?[Position](#class-position)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var popupColor

```cangjie
public var popupColor: ?ResourceColor
```

**Function:** Sets the color of the tooltip bubble. To remove the blur background fill effect, set backgroundBlurStyle to BlurStyle.NONE.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var autoCancel

```cangjie
public var autoCancel: ?Bool
```

**Function:** Whether to automatically close the bubble when there is an operation on the page. Default value: true.

**Type:** ?Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: ?Length
```

**Function:** Sets the width of the popup window.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowPointPosition

```cangjie
public var arrowPointPosition: Option<ArrowPointPosition>
```

**Function:** Sets the display position of the bubble arrow relative to the parent component. The arrow can be positioned at "Start", "Center", or "End" in both vertical and horizontal directions. All these positions are within the bounds of the parent component area and will not exceed the parent component's boundaries.

**Type:** Option<[ArrowPointPosition](#enum-arrowpointposition)>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowWidth

```cangjie
public var arrowWidth: ?Length
```

**Function:** The width of the arrow.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowHeight

```cangjie
public var arrowHeight: ?Length
```

**Function:** The height of the arrow.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var radius

```cangjie
public var radius: ?Length
```

**Function:** The corner radius of the popup window.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowStyle
```

**Function:** Sets the shadow of the bubble.

**Type:** ?[ShadowStyle](#enum-shadowstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Sets the blur background parameters for the bubble.

**Type:** ?[BlurStyle](#enum-blurstyle)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: ?TransitionEffect
```

**Function:** Customizes the animation effects for popup display and exit.

> **Note:**
>
> - If not set, the default display/exit animations will be used.
> - Pressing the back key during the display animation will interrupt the display animation and execute the exit animation, with the effect being a combination of both animation curves.
> - Pressing the back key during the exit animation will not interrupt the exit animation, and the back key will not be responded to.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillDismiss

```cangjie
public var onWillDismiss: ?(DismissPopupAction) -> Unit
```

**Function:** Sets the callback function to intercept the exit event.

> **Note:**
>
> The onWillDismiss callback cannot perform another onWillDismiss interception.

**Type:** ?([DismissPopupAction](#class-dismisspopupaction)) -> Unit

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var followTransformOfTarget

```cangjie
public var followTransformOfTarget: ?Bool
```

**Function:** When the host component bound to the bubble or its parent container has transformations like rotation or scaling, sets whether the bubble can be displayed at the corresponding transformed position. Default value: false.

**Type:** ?Bool

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String, ?Placement, ?PopupButton, ?PopupButton, Option\<(PopupStateChangeParam) -> Unit>, ?Length, ?Bool, ?Color, ?PopupMessageOptions, ?Length, ?Bool, ?Position, ?Color, ?Bool, ?Length, ?ArrowPointPosition, ?Length, ?Length, ?Length, ?ShadowStyle, ?BlurStyle, ?TransitionEffect, Option\<(DismissPopupAction) -> Unit>, ?Bool)

```cangjie
public init(
    message!: ?String,
    placement!: ?Placement = Option.None,
    primaryButton!: ?PopupButton = None,
    secondaryButton!: ?PopupButton = None,
    onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None,
    arrowOffset!: ?Length = None,
    showInSubWindow!: ?Bool = None,
    mask!: ?Color = None,
    messageOptions!: ?PopupMessageOptions = None,
    targetSpace!: ?Length = None,
    enableArrow!: ?Bool = None,
    offset!: ?Position = None,
    popupColor!: ?Color = None,
    autoCancel!: ?Bool = None,
    width!: ?Length = None,
    arrowPointPosition!: ?ArrowPointPosition = None,
    arrowWidth!: ?Length = None,
    arrowHeight!: ?Length = None,
    radius!: ?Length = None,
    shadow!: ?ShadowStyle = None,
    backgroundBlurStyle!: ?BlurStyle = Option.None,
    transition!: ?TransitionEffect = Option.None,
    onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None,
    followTransformOfTarget!: ?Bool = None
)
```

**Function:** Creates a PopupOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
|message|?String|Yes|-|**Named parameter.** Sets the content of the popup message.|
|placement|?[Placement](#enum-placement)|No|Option.None|**Named parameter.** Sets the display position of the popup component relative to the target.|
|primaryButton|?[PopupButton](#class-popupbutton)|No|None|**Named parameter.** Sets the first button. Initial value is PopupButton(value: "", action: {=>}).|
|secondaryButton|?[PopupButton](#class-popupbutton)|No|None|**Named parameter.** Sets the second button. Initial value is PopupButton(value: "", action: {=>}).|
|onStateChange|Option<([PopupStateChangeParam](#class-popupstatechangeparam)) -> Unit>|No|Option.None|**Named parameter.** Sets the callback for popup state change events.|
|arrowOffset|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Sets the offset of the popup arrow on the popup window. Initial value is 0.vp.|
|showInSubWindow|?Bool|No|None|**Named parameter.** Sets whether to display the bubble in a sub-window. Initial value is false.|
|mask|?[Color](./cj-common-types.md#class-color)|No|None|**Named parameter.** Sets the color of the mask layer. Initial value is Color(0x1000000).|
|messageOptions|?[PopupMessageOptions](#class-popupmessageoptions)|No|None|**Named parameter.** Sets the parameters for popup message text. Initial value is PopupMessageOptions().|
|targetSpace|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Sets the gap between the popup and the target. Initial value is 0.vp.|
|enableArrow|?Bool|No|None|**Named parameter.** Whether to enable the arrow. Initial value is true.|
|offset|?[Position](#class-position)|No|None|**Named parameter.** Sets the offset of the popup component relative to the display position set by placement. Initial value is Position(x:0.0, y: 0.0).|
|popupColor|?[Color](./cj-common-types.md#class-color)|No|None|**Named parameter.** Sets the color of the tooltip bubble. Initial value is Color(0x1000000).|
|autoCancel|?Bool|No|None|**Named parameter.** Sets whether to automatically close the bubble when there is an operation on the page. Initial value is true.|
|width|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Sets the popup width. Initial value is 0.vp.|
|arrowPointPosition|?[ArrowPointPosition](./cj-common-types.md#enum-arrowpointposition)|No|None|**Named parameter.** Sets the display position of the bubble arrow point relative to the parent component.|
|arrowWidth|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Arrow width. Initial value is 16.vp.|
|arrowHeight|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Arrow height. Initial value is 8.vp.|
|radius|?[Length](./cj-common-types.md#interface-length)|No|None|**Named parameter.** Sets the border radius of the bubble. Initial value is 20.vp.|
|shadow|?[ShadowStyle](./cj-common-types.md#enum-shadowstyle)|No|None|**Named parameter.** Sets the bubble shadow. Initial value is ShadowStyle.OuterDefaultMD.|
|backgroundBlurStyle|?[BlurStyle](#enum-blurstyle)|No|Option.None|**Named parameter.** Sets the blur background parameters for the bubble. Initial value is BlurStyle.ComponentUltraThick.|
|transition|?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)|No|Option.None|**Named parameter.** Customizes the animation effect for popup display and exit.|
|onWillDismiss|Option\<([DismissPopupAction](#class-dismisspopupaction)) -> Unit>|No|None|**Named parameter.** Sets the callback function to intercept the dismiss event.|
|followTransformOfTarget|?Bool|No|None|**Named parameter.** When the host component bound to the bubble or the parent container of the host component has transformations such as rotation or scaling applied, sets whether the bubble can be displayed at the corresponding transformed position.|

## class MenuElement

```cangjie
public class MenuElement {
    public init(value!: ?ResourceStr, action!: () -> Unit)
}
```

**Function:** Configures menu item icons and text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceStr, () -> Unit)

```cangjie
public init(value!: ?ResourceStr, action!: () -> Unit)
```

**Function:** Creates a MenuElement object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Menu item text. |
| action | () -> Unit | Yes | - | **Named parameter.** Callback for menu item click events. |

## class CustomPopupOptions

```cangjie
public class CustomPopupOptions {
    public var builder: CustomBuilder
    public var placement: ?Placement
    public var backgroundColor: ?Color
    public var enableArrow: ?Bool
    public var autoCancel: ?Bool
    public var onStateChange: Option<(PopupStateChangeParam) -> Unit>
    public var popupColor: ?Color
    public var arrowOffset: ?Length
    public var showInSubWindow: ?Bool
    public var mask: ?Color
    public var targetSpace: ?Length
    public var offset: ?Position
    public var width: ?Length
    public var arrowPointPosition: Option<ArrowPointPosition>
    public var arrowWidth: ?Length
    public var arrowHeight: ?Length
    public var radius: ?Length
    public var shadow: ?ShadowStyle
    public var backgroundBlurStyle: ?BlurStyle
    public var focusable: ?Bool
    public var transition: Option<TransitionEffect>
    public var onWillDismiss: Option<(DismissPopupAction) -> Unit>
    public var followTransformOfTarget: ?Bool
    public init(builder!: () -> Unit, placement!: ?Placement = Option.None, popupColor!: ?Color = None, enableArrow!: ?Bool = None, autoCancel!: ?Bool = None, onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None, showInSubWindow!: ?Bool = None, backgroundColor!: ?Color = None, arrowOffset!: ?Length = None, mask!: ?Color = None, targetSpace!: ?Length = None, offset!: ?Position = None, width!: ?Length = None, arrowPointPosition!: ?ArrowPointPosition = None, arrowWidth!: ?Length = None, arrowHeight!: ?Length = None, radius!: ?Length = None, shadow!: ?ShadowStyle = None, backgroundBlurStyle!: ?BlurStyle = Option.None, focusable!: ?Bool = None, transition!: Option<TransitionEffect> = Option.None, onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None, followTransformOfTarget!: ?Bool = None)
}
```

**Function:** Parameters for displaying popup windows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var builder

```cangjie
public var builder: CustomBuilder
```

**Function:** Builder for the content of the tooltip bubble.

> **Note:**
>
> popup is a common attribute, and nested popups are not supported in custom popups. The position property is not supported for the first-level container components under builder; using it will prevent the bubble from displaying. If custom components are used in the builder, the aboutToAppear and aboutToDisappear lifecycle methods of the custom components are unrelated to the visibility of the popup window and cannot be used to determine the popup's visibility.

**Type:** [CustomBuilder](#type-custombuilder)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var placement

```cangjie
public var placement: ?Placement
```

**Function:** Sets the preferred display position of the bubble component. If the current position cannot accommodate it, the position will be automatically adjusted.

**Type:** ?[Placement](#enum-placement)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ?Color
```

**Function:** Sets the background color of the tooltip bubble.

**Type:** ?[Color](./cj-common-types.md#class-color)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableArrow

```cangjie
public var enableArrow: ?Bool
```

**Function:** Sets whether to display the arrow. If the length of the bubble on the side where the arrow is located is insufficient to display the arrow, the arrow will not be shown by default. For example, if placement is set to Left and the bubble height is less than the sum of the arrow width (32.vp) and twice the bubble corner radius (48.vp) (80.vp), the arrow will not be displayed.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var autoCancel

```cangjie
public var autoCancel: ?Bool
```

**Function:** Sets whether to automatically close the bubble when there is an operation on the page.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onStateChange

```cangjie
public var onStateChange: Option<(PopupStateChangeParam) -> Unit>
```

**Function:** Sets the callback for popup state changes, with the parameter being the current display state of the popup.

**Type:** Option<([PopupStateChangeParam](#class-popupstatechangeparam)) -> Unit>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var popupColor

```cangjie
public var popupColor: ?Color
```

**Function:** Sets the color of the tooltip bubble. To remove the blur background effect, set backgroundBlurStyle to BlurStyle.NONE.

**Type:** ?[Color](./cj-common-types.md#class-color)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowOffset

```cangjie
public var arrowOffset: ?Length
```

**Function:** Sets the offset of the popup arrow on the popup window. When the arrow is above or below the bubble, a value of 0 means the arrow is aligned to the far left, and the offset is the distance from the arrow to the far left, defaulting to center alignment. When the arrow is to the left or right of the bubble, the offset is the distance from the arrow to the top, defaulting to center alignment. If displayed at the edge of the screen, the bubble will automatically shift left or right, and a value of 0 means the arrow will always point to the bound component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var showInSubWindow

```cangjie
public var showInSubWindow: ?Bool
```

**Function:** Sets whether to display the bubble in a sub-window. The default value is false (not displayed).

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var mask

```cangjie
public var mask: ?Color
```

**Function:** Sets the color of the mask layer.

**Type:** ?[Color](./cj-common-types.md#class-color)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var targetSpace

```cangjie
public var targetSpace: ?Length
```

**Function:** Sets the gap between the popup and the target.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: ?Position
```

**Function:** Sets the offset of the popup component relative to the display position set by placement. Percentage values are not supported.

**Type:** ?[Position](#class-position)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: ?Length
```

**Function:** Sets the width of the popup window.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowPointPosition

```cangjie
public var arrowPointPosition: Option<ArrowPointPosition>
```

**Function:** Sets the position of the bubble's arrow relative to the parent component's display position. The arrow can be positioned at "Start", "Center", or "End" in both vertical and horizontal directions. All these positions are within the bounds of the parent component and will not exceed its boundaries.

**Type:** Option<[ArrowPointPosition](#enum-arrowpointposition)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowWidth

```cangjie
public var arrowWidth: ?Length
```

**Function:** Sets the width of the arrow. If the set arrow width exceeds the length of the side minus twice the bubble's corner radius, the arrow will not be drawn.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowHeight

```cangjie
public var arrowHeight: ?Length
```

**Function:** Sets the height of the arrow.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var radius

```cangjie
public var radius: ?Length
```

**Function:** Sets the corner radius of the popup window.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var shadow

```cangjie
public var shadow: ?ShadowStyle
```

**Function:** Sets the shadow style of the popup window.

**Type:** ?[ShadowStyle](#enum-shadowstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** Sets the background blur style of the popup window.

**Type:** ?[BlurStyle](#enum-blurstyle)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var focusable

```cangjie
public var focusable: ?Bool
```

**Function:** Sets whether the bubble gains focus after popping up.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: Option<TransitionEffect>
```

**Function:** Customizes the animation effects for popup window display and exit.

**Type:** Option<[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onWillDismiss

```cangjie
public var onWillDismiss: Option<(DismissPopupAction) -> Unit>
```

**Function:** Sets the callback function to intercept the exit event.

> **Note:**
>
> Within the onWillDismiss callback, you cannot perform another onWillDismiss interception.

**Type:** Option<([DismissPopupAction](#class-dismisspopupaction)) -> Unit>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var followTransformOfTarget

```cangjie
public var followTransformOfTarget: ?Bool
```

**Function:** Determines whether the bubble can be displayed at the transformed position when the host component it is bound to or the parent container of the host component has transformations such as rotation or scaling applied.

**Type:** ?Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(() -> Unit, Option\<Placement>, ?Color, ?Bool, ?Bool, Option\<(PopupStateChangeParam) -> Unit>, ?Bool, ?Color, ?Length, ?Color, ?Length, ?Position, ?Length, ?ArrowPointPosition, ?Length, ?Length, ?Length, ?ShadowStyle, Option\<BlurStyle>, ?Bool, Option\<TransitionEffect>, Option\<(DismissPopupAction) -> Unit>, ?Bool)

```cangjie
public init(builder!: () -> Unit, placement!: ?Placement = Option.None, popupColor!: ?Color = None, enableArrow!: ?Bool = None, autoCancel!: ?Bool = None, onStateChange!: Option<(PopupStateChangeParam) -> Unit> = Option.None, showInSubWindow!: ?Bool = None, backgroundColor!: ?Color = None, arrowOffset!: ?Length = None, mask!: ?Color = None, targetSpace!: ?Length = None, offset!: ?Position = None, width!: ?Length = None, arrowPointPosition!: ?ArrowPointPosition = None, arrowWidth!: ?Length = None, arrowHeight!: ?Length = None, radius!: ?Length = None, shadow!: ?ShadowStyle = None, backgroundBlurStyle!: ?BlurStyle = Option.None, focusable!: ?Bool = None, transition!: Option<TransitionEffect> = Option.None, onWillDismiss!: Option<(DismissPopupAction) -> Unit> = None, followTransformOfTarget!: ?Bool = None)
```

**Function:** Constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | () -> Unit | Yes | - | **Named parameter.** Builder for the content of the tooltip bubble.<br>**Note:** Only supports receiving custom builder functions decorated with @Builder. |
| placement | Option<[Placement](#enum-placement)> | No | Option.None | **Named parameter.** Preferred display position of the bubble component.<br>**Note:** If the current position cannot accommodate it, the position will be automatically adjusted. Initial value is Placement.Bottom. |
| popupColor | ?[Color](./cj-common-types.md#class-color) | No | None | **Named parameter.** Background color of the tooltip bubble. Initial value is Color(0x1000000). |
| enableArrow | ?Bool | No | None | **Named parameter.** Whether to display the arrow.<br>**Note:** If the length of the bubble on the side where the arrow is located is insufficient to display the arrow, the arrow will not be shown by default. For example, if placement is set to Left but the bubble height is less than the arrow width (32vp), the arrow will not be displayed. Initial value is true. |
| autoCancel | ?Bool | No | None | **Named parameter.** Whether to automatically close the bubble when there is an operation on the page. Initial value is true. |
| onStateChange | Option<([PopupStateChangeParam](#class-popupstatechangeparam)) -> Unit> | No | Option.None | **Named parameter.** Callback for popup state changes, with the parameter being the current display state of the popup. |
| showInSubWindow | ?Bool | No | None | **Named parameter.** Whether to display the bubble in a sub-window. Initial value is false. |
| backgroundColor | ?[Color](./cj-common-types.md#class-color) | No | None | **Named parameter.** Background color of the tooltip bubble. Initial value is Color(0x1000000). |
| arrowOffset | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Offset of the popup arrow on the popup window.<br>**Note:** When the arrow is above or below the bubble, a value of 0 means the arrow is aligned to the far left, and the offset is the distance from the arrow to the far left, defaulting to center alignment. When the arrow is to the left or right of the bubble, the offset is the distance from the arrow to the top, defaulting to center alignment. If displayed at the edge of the screen, the bubble will automatically shift left or right, and a value of 0 means the arrow will always point to the bound component. Initial value is 0.vp. |
| mask | ?[Color](./cj-common-types.md#class-color) | No | None | **Named parameter.** Color of the tooltip bubble's mask layer. |
| targetSpace | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the gap between the popup and the target. Initial value is 0.vp.|

## class SheetOptions

```cangjie
public class SheetOptions <: BindOptions {
    public init(backgroundColor!: Option<ResourceColor> = Option.None, onAppear!: Option<() -> Unit> = Option.None, onDisappear!: Option<() -> Unit> = Option.None, onWillAppear!: Option<() -> Unit> = Option.None, onWillDisappear!: Option<() -> Unit> = Option.None, height!: Option<SheetSize> = Option.None, detents!: Option<Array<SheetSize>> = Option.None, preferType!: Option<SheetType> = Option.None, showClose!: Option<Bool> = Option.None, dragBar!: Option<Bool> = Option.None, blurStyle!: Option<BlurStyle> = Option.None, maskColor!: Option<Color> = Option.None, title!: Option<() -> Unit> = Option.None, enableOutsideInteractive!: Option<Bool> = Option.None, shouldDismiss!: Option<(SheetDismiss) -> Unit> = Option.None, onWillDismiss!: Option<(DismissSheetAction) -> Unit> = Option.None, onWillSpringBackWhenDismiss!: Option<(SpringBackAction) -> Unit> = Option.None, onHeightDidChange!: Option<(Float32) -> Unit> = Option.None, onDetentsDidChange!: Option<(Float32) -> Unit> = Option.None, onWidthDidChange!: Option<(Float32) -> Unit> = Option.None, onTypeDidChange!: Option<(Float32) -> Unit> = Option.None, borderWidth!: Option<Length> = None, borderColor!: Option<Color> = None, borderStyle!: Option<EdgeStyles> = None, width!: Option<Length> = None, shadow!: Option<ShadowOptions> = None, mode!: Option<SheetMode> = None, scrollSizeMode!: Option<ScrollSizeMode> = None)
}
```

**Function:** Configures optional properties for semi-modal pages.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [BindOptions](#class-bindoptions)

### init(Option\<ResourceColor>, Option\<() -> Unit>, Option\<() -> Unit>, Option\<() -> Unit>, Option\<() -> Unit>, Option\<SheetSize>, Option\<Array\<SheetSize>>, Option\<SheetType>, Option\<Bool>, Option\<Bool>, Option\<BlurStyle>, Option\<Color>, Option\<() -> Unit>, Option\<Bool>, Option\<(SheetDismiss) -> Unit>, Option\<(DismissSheetAction) -> Unit>, Option\<(SpringBackAction) -> Unit>, Option\<(Float32) -> Unit>, Option\<(Float32) -> Unit>, Option\<(Float32) -> Unit>, Option\<(Float32) -> Unit>, Option\<Length>, Option\<Color>, Option\<EdgeStyles>, Option\<Length>, Option\<ShadowOptions>, Option\<SheetMode>, Option\<ScrollSizeMode>)

```cangjie
public init(backgroundColor!: Option<ResourceColor> = Option.None, onAppear!: Option<() -> Unit> = Option.None, onDisappear!: Option<() -> Unit> = Option.None, onWillAppear!: Option<() -> Unit> = Option.None, onWillDisappear!: Option<() -> Unit> = Option.None, height!: Option<SheetSize> = Option.None, detents!: Option<Array<SheetSize>> = Option.None, preferType!: Option<SheetType> = Option.None, showClose!: Option<Bool> = Option.None, dragBar!: Option<Bool> = Option.None, blurStyle!: Option<BlurStyle> = Option.None, maskColor!: Option<Color> = Option.None, title!: Option<() -> Unit> = Option.None, enableOutsideInteractive!: Option<Bool> = Option.None, shouldDismiss!: Option<(SheetDismiss) -> Unit> = Option.None, onWillDismiss!: Option<(DismissSheetAction) -> Unit> = Option.None, onWillSpringBackWhenDismiss!: Option<(SpringBackAction) -> Unit> = Option.None, onHeightDidChange!: Option<(Float32) -> Unit> = Option.None, onDetentsDidChange!: Option<(Float32) -> Unit> = Option.None, onWidthDidChange!: Option<(Float32) -> Unit> = Option.None, onTypeDidChange!: Option<(Float32) -> Unit> = Option.None, borderWidth!: Option<Length> = None, borderColor!: Option<Color> = None, borderStyle!: Option<EdgeStyles> = None, width!: Option<Length> = None, shadow!: Option<ShadowOptions> = None, mode!: Option<SheetMode> = None, scrollSizeMode!: Option<ScrollSizeMode> = None)
```

**Function:** Constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| backgroundColor | Option<[ResourceColor](./cj-common-types.md#interface-resourcecolor)> | No | Option.None | **Named parameter.** Background color of the semi-modal page. Default value is Color.White. |
| onAppear | Option\<() -> Unit> | No | Option.None | **Named parameter.** Callback function when the semi-modal page appears (after animation ends). |
| onDisappear | Option\<() -> Unit> | No | Option.None | **Named parameter.** Callback function when the semi-modal page disappears (after animation ends). |
| onWillAppear | Option\<() -> Unit> | No | Option.None | **Named parameter.** Callback function when the semi-modal page is about to appear (before animation starts). |
| onWillDisappear | Option\<() -> Unit> | No | Option.None | **Named parameter.** Callback function when the semi-modal page is about to disappear (before animation starts).<br>**Note:**<br>Modifying state variables in the onWillDisappear function is not allowed, as it may cause unstable component behavior. |
| height | Option<[SheetSize](#enum-sheetsize)> | No | Option.None | **Named parameter.** Height of the semi-modal.<br>**Note:**<br>For bottom sheets in portrait mode, this property is invalid when detents is set.<br>For bottom sheets in portrait mode, the maximum height is 8vp from the signal bar.<br>For bottom sheets in landscape mode, this property is invalid, and the height is 8vp from the top of the screen.<br>For center sheets and follow sheets, setting the type to SheetSize.Large and SheetSize.Medium is invalid, and the default height is 560vp. The minimum height for center sheets and follow sheets is 320vp, and the maximum height is 90% of the window's short side. When using Length to set the height or SheetSize.FitContent for adaptive height, if the height exceeds the maximum, the maximum height is displayed; if it is less than the minimum, the minimum height is displayed. |
| detents | Option<Array<[SheetSize](#enum-sheetsize)>> | No | Option.None | **Named parameter.** Height presets for the semi-modal page.<br>**Note:**<br>Effective for bottom sheets in portrait mode. The first height in the array is the initial height.<br>The panel can be dragged to switch between presets. Whether it snaps to the target preset after release depends on two conditions: speed and distance. If the speed exceeds the threshold, it snaps to the target preset in the direction of the drag; if the speed is below the threshold, the distance condition is applied. If the displacement distance > 1/2 of the current position to the target position, it snaps to the target preset; otherwise, it returns to the current preset. Speed threshold: 1000, distance threshold: 50%. |
| preferType | Option<[SheetType](#enum-sheettype)> | No | Option.None | **Named parameter.** Style of the semi-modal page.<br>**Note:**<br>preferType cannot be set to SheetType.Bottom. |
| showClose | Option\<Bool> | No | Option.None | **Named parameter.** Whether to show the close icon. The close icon is displayed by default. When using the close icon to close the semi-modal page, set the isShow parameter to false in the onDisappear callback function. |
| dragBar | Option\<Bool> | No | Option.None | **Named parameter.** Whether to show the control bar.<br>**Note:**<br>The control bar is displayed by default when the detents property is set with multiple heights. Otherwise, the control bar is not displayed. |
| blurStyle | Option\<[BlurStyle](#enum-blurstyle)> | No | Option.None | **Named parameter.** Blur background for the semi-modal panel. |
| maskColor | Option<[Color](./cj-common-types.md#class-color)> | No | Option.None | **Named parameter.** Background mask color for the semi-modal page. |
| title | Option\<() -> Unit> | No | Option.None | **Named parameter.** Title of the semi-modal panel.<br>**Note:** Only supports receiving custom builder functions decorated with @Builder. |
| enableOutsideInteractive | Option\<Bool> | No | Option.None | **Named parameter.** Whether the page where the semi-modal is located allows interaction.<br>**Note:**<br>When set to true, interaction is allowed, and the mask is not displayed; when set to false, interaction is not allowed, and the mask is displayed. If not set, bottom sheets and center sheets do not allow interaction by default, while follow sheets allow interaction. When set to true, maskColor settings are invalid. |
| shouldDismiss | Option<([SheetDismiss](#class-sheetdismiss)) -> Unit> | No | Option.None | **Named parameter.** Callback function for interactive closing of the semi-modal page.<br>**Note:**<br>When the user performs actions like pull-down to close, back event, click mask to close, or close button to close, if this callback is registered, the page will not close immediately. |
| onWillDismiss | Option<([DismissSheetAction](#class-dismisssheetaction)) -> Unit> | No | Option.None | **Named parameter.** Callback function for interactive closing of the semi-modal page, allowing developers to register and obtain the type of closing operation to decide whether to close the semi-modal state.<br>**Note:**<br>When the user triggers a close operation, if this callback is registered, the page will not close immediately. Instead, the developer can determine the type of closing operation through the reason parameter in the callback and decide whether to close the semi-modal page. If this callback is not registered, the semi-modal page closes normally when the user performs a close operation. In the onWillDismiss callback, onWillDismiss interception cannot be performed again. Recommended for secondary confirmation scenarios. |
| onWillSpringBackWhenDismiss | Option<([SpringBackAction](#class-springbackaction)) -> Unit> | No | Option.None | **Named parameter.** Callback function to control the springback effect before interactive closing of the semi-modal page, allowing developers to register and control the springback effect during interactive closing.<br>Note:<br>When the user triggers a pull-down close operation and both this callback and shouldDismiss or onWillDismiss are registered, the developer can control whether to spring back during pull-down closing. The springBack method can be called in the callback to achieve the springback effect. Alternatively, not calling springBack cancels the springback effect.<br>If this callback is not registered but shouldDismiss or onWillDismiss is registered, the default behavior is to trigger a springback effect during pull-down closing, and then decide whether to close the semi-modal based on the behavior in shouldDismiss or onWillDismiss.<br>If this callback is not registered and neither shouldDismiss nor onWillDismiss is registered, the default behavior is to close the semi-modal during pull-down closing. |
| onHeightDidChange | Option\<(Float32) -> Unit> | No | Option.None | **Named parameter.** Callback function for height changes of the semi-modal page.<br>Note:<br>For bottom sheets, height changes are returned frame by frame only during preset changes and drag operations. For semi-modal pull-up and soft keyboard avoidance, only the final height is returned. For other sheets, only the final height is returned during pull-up. The return value is in px. |
| onDetentsDidChange | Option\<(Float32) -> Unit> | No | Option.None | **Named parameter.** Callback function for preset changes of the semi-modal page.<br>Note:<br>For bottom sheets, the final height is returned during preset changes. The return value is in px. |
| onWidthDidChange | Option\<(Float32) -> Unit> | No | Option.None | **Named parameter.** Callback function for width changes of the semi-modal page.<br>Note:<br>The final width is returned during width changes. The return value is in px. |
| onTypeDidChange | Option\<(Float32) -> Unit> | No | Option.None | **Named parameter.** Callback function for form changes of the semi-modal page.<br>Note:<br>The final form is returned during form changes. |
| borderWidth | Option<[Length](./cj-common-types.md#interface-length)> | No | None | **Named parameter.** Border width of the semi-modal page. The width of each of the four borders can be set separately.<br>Percentage parameter: Sets the border width of the semi-modal page as a percentage of the parent element's width.<br>When the left and right borders of the semi-modal page exceed its width, or the top and bottom borders exceed its height, the display may not meet expectations.<br>Note:<br>For bottom sheets, the bottom border width setting is invalid. |
| borderColor | Option<[Color](./cj-common-types.md#class-color)> | No | None | **Named parameter.** Border color of the semi-modal page. If using the borderColor property, it must be used together with the borderWidth property.<br>Note:<br>For bottom sheets, the bottom border color setting is invalid. |
| borderStyle | Option<[EdgeStyles](#class-edgestyles)> | No | None | **Named parameter.** Border style of the semi-modal page. If using the borderStyle property, it must be used together with the borderWidth property.<br>Note:<br>For bottom sheets, the bottom border style setting is invalid. |
| width | Option<[Length](./cj-common-types.md#interface-length)> | No | None | **Named parameter.** Width of the semi-modal page. Percentage parameter: Sets the width of the semi-modal page as a percentage of the parent element's width. |
| shadow | Option<[ShadowOptions](#class-shadowoptions)> | No | None | **Named parameter.** Shadow effect.<br>Initial value:<br>Before API version 26, the initial value is ShadowOptions(radius: 0.0);<br>From API version 26 onward, the initial value is ShadowOptions(radius: -1.0). |
| mode | Option<[SheetMode](#enum-sheetmode)> | No | None | **Named parameter.** Shadow of the semi-modal page. |
| scrollSizeMode | Option<[ScrollSizeMode](#enum-scrollsizemode)> | No | None | **Named parameter.** Refresh timing of the content area during semi-modal panel scrolling. |

## class PopupMessageOptions

```cangjie
public class PopupMessageOptions {
    public var textColor: ?ResourceColor
    public var font: ?Font
    public init(textColor!: ?ResourceColor = None, font!: ?Font = None)
}
```

**Function:** Parameters for popup message text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var textColor

```cangjie
public var textColor: ?ResourceColor
```

**Function:** Sets the text color of the popup message.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var font

```cangjie
public var font: ?Font
```

**Function:** Sets the font properties of the popup message. Does not support setting the family.

**Type:** ?[Font](#class-font)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?ResourceColor, ?Font)

```cangjie
public init(textColor!: ?ResourceColor = None, font!: ?Font = None)
```

**Function:** Constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| textColor | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Text color of the popup message. Initial value is Color(0x000000). |
| font | ?[Font](#class-font) | No | None | **Named parameter.** Font properties of the popup message. Initial value is Font(). |

## class OverlayOffset

```cangjie
public class OverlayOffset {
    public var x: ?Float64
    public var y: ?Float64
    public init(x!: ?Float64 = None, y!: ?Float64 = None)
}
```

**Function:** Sets the offset of the overlay.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Float64
```

**Function:** Horizontal offset.

**Type:** ?Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Float64
```

**Function:** Vertical offset.

**Type:** ?Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Float64, ?Float64)

```cangjie
public init(x!: ?Float64 = None, y!: ?Float64 = None)
```

**Function:** Constructs the overlay offset.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | ?Float64 |## class SpringBackAction

```cangjie
public class SpringBackAction {}
```

**Function:** Controls the rebound type before semi-modal closure.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func springBack()

```cangjie
public func springBack(): Unit
```

**Function:** Controls the rebound function before semi-modal page closure. Developers should call this when semi-modal rebound is needed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class Rectangle

```cangjie
public class Rectangle {
    public var x: ?Length
    public var y: ?Length
    public var width: ?Length
    public var height: ?Length
    public init(x!: ?Length = None, y!: ?Length = None, width!: ?Length = None, height!: ?Length = None)
}
```

**Function:** Defines the region position type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var x

```cangjie
public var x: ?Length
```

**Function:** The x-axis coordinate of the touch point relative to the top-left corner of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var y

```cangjie
public var y: ?Length
```

**Function:** The y-axis coordinate of the touch point relative to the top-left corner of the component.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: ?Length
```

**Function:** The width of the touch hotspot.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: ?Length
```

**Function:** The height of the touch hotspot.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Length, ?Length, ?Length, ?Length)

```cangjie
public init(x!: ?Length = None, y!: ?Length = None, width!: ?Length = None, height!: ?Length = None)
```

**Function:** Constructs a Rectangle-type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The x-axis coordinate of the touch point relative to the top-left corner of the component. Initial value is 0.vp. |
| y | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The y-axis coordinate of the touch point relative to the top-left corner of the component. Initial value is 0.vp. |
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The width of the touch hotspot. Initial value is 100.percent. |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The height of the touch hotspot. Initial value is 100.percent. |

## class DismissPopupAction

```cangjie
public class DismissPopupAction {
    public let reason: DismissReason
}
```

**Function:** Sets the popup interactive closure interception switch and interception callback function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### let reason

```cangjie
public let reason: DismissReason
```

**Function:** The closure reason, returns the event reason for intercepting popup disappearance.

**Type:** [DismissReason](#enum-dismissreason)

**Read-Write Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func dismiss()

```cangjie
public func dismiss(): Unit
```

**Function:** The semi-modal page closure callback function. Developers should call this when exiting the page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class ContextMenuOptions

```cangjie
public class ContextMenuOptions {
    public var offset: ?Position
    public var placement: Option<Placement>
    public var enableArrow: ?Bool
    public var arrowOffset: ?Length
    public var preview: ?CustomBuilder
    public var previewAnimationOptions: ?ContextMenuAnimationOptions
    public var onAppear: ?() -> Unit
    public var onDisappear: ?() -> Unit
    public var aboutToAppear: ?() -> Unit
    public var aboutToDisappear: ?() -> Unit
    public var backgroundColor: ?ResourceColor
    public var backgroundBlurStyle: ?BlurStyle
    public var transition: ?TransitionEffect
    public init(offset!: ?Position = None, placement!: Option<Placement> = Option.None, enableArrow!: ?Bool = None, arrowOffset!: ?Length = None, preview!: Option<() -> Unit> = Option.None, previewAnimationOptions!: ?ContextMenuAnimationOptions = None, onAppear!: ?() -> Unit = None, onDisappear!: ?() -> Unit = None, aboutToAppear!: ?() -> Unit = None, aboutToDisappear!: ?() -> Unit = None, backgroundColor!: ?ResourceColor = None, backgroundBlurStyle!: ?BlurStyle = Option.None, transition!: ?TransitionEffect = None, borderRadius!: ?BorderRadiuses = None, layoutRegionMargin!: ?Margin = None)
}
```

**Function:** Configures parameters for the popup menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var offset

```cangjie
public var offset: ?Position
```

**Function:** The offset of the popup menu position, which does not cause the menu to display beyond the screen boundaries.

**Type:** ?[Position](#class-position)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var placement

```cangjie
public var placement: Option<Placement>
```

**Function:** The preferred display position of the menu component. If the current position cannot accommodate it, the position will be automatically adjusted.

**Type:** Option<[Placement](#enum-placement)>

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var enableArrow

```cangjie
public var enableArrow: ?Bool
```

**Function:** Whether to display the arrow. If the menu size and position are insufficient to place the arrow, it will not be displayed.

**Type:** ?Bool

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var arrowOffset

```cangjie
public var arrowOffset: ?Length
```

**Function:** The offset of the arrow at the menu. The offset must be valid and greater than 0 when converted to a specific value. Additionally, this value will not cause the arrow to exceed the safe distance around the menu when it takes effect.

**Type:** ?[Length](./cj-common-types.md#interface-length)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var preview

```cangjie
public var preview: ?CustomBuilder
```

**Function:** The preview content style for long-press floating menus or menus displayed using bindContextMenu, which is user-defined content.

**Type:** ?[CustomBuilder](#type-custombuilder)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var previewAnimationOptions

```cangjie
public var previewAnimationOptions: ?ContextMenuAnimationOptions
```

**Function:** Controls the start and end scaling factors (relative to the original preview image) for the long-press preview display animation.

**Type:** ?[ContextMenuAnimationOptions](#class-contextmenuanimationoptions)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onAppear

```cangjie
public var onAppear: ?() -> Unit
```

**Function:** The event callback when the menu pops up.

**Type:** ?() -> Unit

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var onDisappear

```cangjie
public var onDisappear: ?() -> Unit
```

**Function:** The event callback when the menu disappears.

**Type:** ?() -> Unit

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var aboutToAppear

```cangjie
public var aboutToAppear: ?() -> Unit
```

**Function:** The event callback before the menu display animation.

**Type:** ?() -> Unit

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var aboutToDisappear

```cangjie
public var aboutToDisappear: ?() -> Unit
```

**Function:** The event callback before the menu exit animation.

**Type:** ?() -> Unit

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundColor

```cangjie
public var backgroundColor: ?ResourceColor
```

**Function:** The background color of the popup.

**Type:** ?[ResourceColor](./cj-common-types.md#interface-resourcecolor)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var backgroundBlurStyle

```cangjie
public var backgroundBlurStyle: ?BlurStyle
```

**Function:** The blur material of the popup background.

**Type:** ?[BlurStyle](#enum-blurstyle)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: ?TransitionEffect
```

**Function:** Sets the transition effect for menu display and exit.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Read-Write Access:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?Position, Option\<Placement>, ?Bool, ?Length, Option\<() -> Unit>, ?ContextMenuAnimationOptions, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?() -> Unit, ?ResourceColor, Option\<BlurStyle>, ?TransitionEffect, ?BorderRadiuses, ?Margin)

```cangjie
public init(offset!: ?Position = None, placement!: Option<Placement> = Option.None, enableArrow!: ?Bool = None, arrowOffset!: ?Length = None, preview!: Option<() -> Unit> = Option.None, previewAnimationOptions!: ?ContextMenuAnimationOptions = None, onAppear!: ?() -> Unit = None, onDisappear!: ?() -> Unit = None, aboutToAppear!: ?() -> Unit = None, aboutToDisappear!: ?() -> Unit = None, backgroundColor!: ?ResourceColor = None, backgroundBlurStyle!: ?BlurStyle = Option.None, transition!: ?TransitionEffect = None, borderRadius!: ?BorderRadiuses = None, layoutRegionMargin!: ?Margin = None)
```

**Function:** Creates a ContextMenuOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| offset | ?[Position](#class-position) | No | None | **Named parameter.** The offset of the popup menu position, which does not cause the menu to display beyond the screen boundaries.<br> **Note:**<br> When the menu type is a popup relative to the parent component area, the width or height of the area is automatically included in the offset based on the menu position property (placement).<br> When the menu appears above the parent component (placement set to Placement.TopLeft, Placement.Top, Placement.TopRight), a positive x value offsets the menu to the right relative to the component, and a positive y value offsets the menu upward relative to the component.<br> When the menu appears below the parent component (placement set to Placement.BottomLeft, Placement.Bottom, Placement.BottomRight), a positive x value offsets the menu to the right relative to the component, and a positive y value offsets the menu downward relative to the component.<br> When the menu appears to the left of the parent component (placement set to Placement.LeftTop, Placement.Left, Placement.LeftBottom), a positive x value offsets the menu to the left relative to the component, and a positive y value offsets the menu downward relative to the component.<br> When the menu appears to the right of the parent component (placement set to Placement.RightTop, Placement.Right, Placement.RightBottom), a positive x value offsets the menu to the right relative to the component, and a positive y value offsets the menu downward relative to the component.<br> If the menu adjusts its display position (inconsistent with the initial main direction of placement), the offset value (offset) becomes invalid. |
| placement | Option\<[Placement](#enum-placement)> | No | Option.None | **Named parameter.** The preferred display position of the menu component. If the current position cannot accommodate it, the position will be automatically adjusted.<br> **Note:**<br> When the placement value is set to undefined, null, or this option is not set, it is treated as unset. When using bindMenu, it is set to the initial value: Placement.BottomLeft. |
| enableArrow | ?Bool | No | None | **Named parameter.** Whether to display the arrow. If the menu size and position are insufficient to place the arrow, it will not be displayed.<br> **Note:** <br> When enableArrow is true and placement is unset or has an invalid value, the menu is displayed above the target by default. Otherwise, it is displayed according to the placement position. If the current position cannot accommodate it, the position will be automatically adjusted. When enableArrow is undefined, the arrow is not displayed. |
| arrowOffset | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** The offset of the arrow at the menu. The offset must be valid and greater than 0 when converted to a specific value. Additionally, this value will not cause the arrow to exceed the safe distance around the menu when it takes effect.<br> Unit: vp<br> **Note:**<br> The safe distance around the menu is the sum of the menu corner radius and half the arrow width.<br> The offset is calculated in the horizontal or vertical direction based on the configured placement.<br> When the arrow is in the horizontal direction of the menu, the offset is the distance from the arrow to the leftmost safe distance of the arrow. When the arrow is in the vertical direction of the menu, the offset is the distance from the arrow to the topmost safe distance of the arrow.<br> The default position of the arrow varies based on the configured placement:<br> When the menu does not avoid, and placement is set to Placement.Top or Placement.Bottom, the arrow is displayed horizontally and centered by default;<br> When placement is set to Placement.Left or Placement.Right, the arrow is displayed vertically and centered by default;<br> When placement is set to Placement.TopLeft or Placement.BottomLeft, the arrow is displayed horizontally by default, and the distance from the left edge of the menu is the arrow safe distance;<br> When placement is set to Placement.TopRight or Placement.BottomRight, the arrow is displayed horizontally by default, and the distance from the right edge of the menu is the arrow safe distance;<br> When placement is set to Placement.LeftTop or Placement.RightTop, the arrow is displayed vertically by default, and the distance from the top edge of the menu is the arrow safe distance;<br> When placement is set to Placement.LeftBottom or Placement.RightBottom, the arrow is displayed vertically by default, and the distance from the bottom edge of the menu is the arrow safe distance. |
| preview | Option\<() -> Unit> | No | Option.None | **Named parameter.** The preview content style for long-press floating menus or menus displayed using bindContextMenu, which is user-defined content.<br> **Note:** <br> - Only supports receiving custom builder functions decorated with @Builder.<br> - Not supported when triggered by responseType as ResponseType.RightClick. If responseType is ResponseType.RightClick, the preview content will not be displayed.<br> - When the preview parameter is not set, the enableArrow parameter takes effect.<br> - When the preview parameter is set to CustomBuilder, the arrow is not displayed even if enableArrow is true. |
| previewAnimationOptions | ?[ContextMenuAnimationOptions](#class-contextmenuanimationoptions) | No | None | **Named parameter.** Controls the start and end scaling factors (relative to the original preview image) for the long-press preview display animation. |
| onAppear | ?() -> Unit |## class DismissContentCoverAction

```cangjie
public class DismissContentCoverAction {
    public let reason: DismissReason
}
```

**Function:** Core callback class for handling full-screen modal page dismissal logic, responsible for intercepting close operations through callback mechanisms when triggered by user actions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### let reason

```cangjie
public let reason: DismissReason
```

**Function:** Type of dismissal reason.

**Type:** [DismissReason](#enum-dismissreason)

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func dismiss()

```cangjie
public func dismiss(): Unit
```

**Function:** Explicitly triggers the modal page dismissal operation, serving as the sole entry point for controlling closure.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## class ContextMenuAnimationOptions

```cangjie
public class ContextMenuAnimationOptions {
    public var scale: ?VArray<Float64, $2>
    public var transition: ?TransitionEffect
    public var hoverScale: ?VArray<Float64, $2>
    public init(scale!: ?VArray<Float64, $2> = None, transition!: ?TransitionEffect = None, hoverScale!: ?VArray<Float64, $2> = None)
}
```

**Function:** Controls the start and end scaling ratios (relative to the original preview image) for long-press preview display animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var scale

```cangjie
public var scale: ?VArray<Float64, $2>
```

**Function:** Scaling ratio relative to the original preview image at the start and end of the animation.

**Type:** ?VArray<Float64, $2>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var transition

```cangjie
public var transition: ?TransitionEffect
```

**Function:** Sets the transition effect for menu display and exit.

**Type:** ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var hoverScale

```cangjie
public var hoverScale: ?VArray<Float64, $2>
```

**Function:** Sets the scaling animation ratio (relative to the original preview image) for floating component screenshots in custom long-press scenarios, with transition effects between the preview and the screenshot.

**Type:** ?VArray<Float64, $2>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?VArray\<Float64, \$2>, ?TransitionEffect, ?VArray\<Float64, \$2>)

```cangjie
public init(scale!: ?VArray<Float64, $2> = None, transition!: ?TransitionEffect = None, hoverScale!: ?VArray<Float64, $2> = None)
```

**Function:** Constructor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scale | ?VArray<Float64, $2> | No | None | **Named parameter.** Scaling ratio relative to the original preview image at the start and end of the animation.<br> **Note:** The scaling ratio should be set according to actual development scenarios. It is recommended to set values smaller than the preview image width or layout constraints. |
| transition | ?[TransitionEffect](./cj-animation-transition.md#class-transitioneffect) | No | None | **Named parameter.** Transition effect for menu display and exit.<br> **Note:** During menu exit animation, landscape/portrait switching will be avoided. Secondary menus do not inherit custom animations. Clicking secondary menus is allowed during pop-up but not during exit animation execution. For details, refer to the TransitionEffect object description. |
| hoverScale | ?VArray<Float64, $2> | No | None | **Named parameter.** Scaling animation ratio (relative to the original preview image) for floating component screenshots in custom long-press scenarios, with transition effects between the preview and the screenshot.<br> **Note:** If the scaling parameter is ≤0, it will not take effect.<br> When the transition interface is used, this parameter will not take effect.<br> When used alongside the scale interface, the scale interface's start value will not take effect.<br> For optimal experience, the final preview size should not be smaller than the original component screenshot size. The current preview animation dimensions are affected by component screenshots and custom preview sizes. Ensure display effects according to actual usage. |

## class DismissSheetAction

```cangjie
public class DismissSheetAction {
    public var reason: ?DismissReason
}
```

**Function:** Callback function type for semi-modal page dismissal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var reason

```cangjie
public var reason: ?DismissReason
```

**Function:** Reason for semi-modal page dismissal.

**Type:** ?[DismissReason](#enum-dismissreason)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func dismiss()

```cangjie
public func dismiss(): Unit
```

**Function:** Callback function for semi-modal page dismissal. Developers should call this when exiting the page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## enum LengthUnit

```cangjie
public enum LengthUnit <: Equatable<LengthUnit> {
    | Px
    | Vp
    | Fp
    | Percent
    | Lpx
    | ...
}
```

**Function:** Length unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:** Equatable\<[LengthUnit](#enum-lengthunit)>

### Px

```cangjie
Px
```

**Function:** Basic pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Vp

```cangjie
Vp
```

**Function:** Screen density unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Fp

```cangjie
Fp
```

**Function:** Font pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Percent

```cangjie
Percent
```

**Function:** Percentage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Lpx

```cangjie
Lpx
```

**Function:** Logical pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(LengthUnit)

```cangjie
public operator func !=(other: LengthUnit): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LengthUnit](#enum-lengthunit) | Yes | - | Another LengthUnit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal. |

### operator func ==(LengthUnit)

```cangjie
public operator func ==(other: LengthUnit): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LengthUnit](#enum-lengthunit) | Yes | - | Another LengthUnit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal. |

### func getValue()

```cangjie
public func getValue(): Int32
```

**Function:** Gets the value of LengthUnit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The value of LengthUnit. |

### static func parse(Int32)

```cangjie
public static func parse(value: Int32): LengthUnit
```

**Function:** Parses an Int32 value into a LengthUnit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The value to parse. |

**Return Value:**

| Type | Description |
|:----|:----|
| [LengthUnit](#enum-lengthunit) | The parsed LengthUnit. |

## enum ModalTransition

```cangjie
public enum ModalTransition <: Equatable<ModalTransition> {
    | Default
    | None
    | Alpha
    | ...
}
```

**Function:** Full-screen modal transition animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Types:**

- Equatable\<[ModalTransition](#enum-modaltransition)>

### Default

```cangjie
Default
```

**Function:** Vertical slide transition animation for full-screen modal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** No transition animation for full-screen modal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Alpha

```cangjie
Alpha
```

**Function:** Opacity fade transition animation for full-screen modal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ModalTransition)

```cangjie
public operator func ==(other: ModalTransition): Bool
```

**Function:** Checks if two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ModalTransition](#enum-modaltransition) | Yes | - | Another ModalTransition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal, otherwise false. |

### operator func !=(ModalTransition)

```cangjie
public operator func !=(other: ModalTransition): Bool
```

**Function:** Checks if two enum values are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ModalTransition](#enum-modaltransition) | Yes | - | Another ModalTransition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal, otherwise false. |```markdown
## enum SheetSize

```cangjie
public enum SheetSize <: Equatable<SheetSize> {
    | Medium
    | Large
    | FitContent
    | ...
}
```

**Function:** Sets the height levels for semi-modal page transitions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SheetSize](#enum-sheetsize)>

### Medium

```cangjie
Medium
```

**Function:** Specifies the semi-modal height as half of the screen height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Large

```cangjie
Large
```

**Function:** Specifies the semi-modal height to be nearly the full screen height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FitContent

```cangjie
FitContent
```

**Function:** Specifies the semi-modal height to adapt to the content height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SheetSize)

```cangjie
public operator func ==(other: SheetSize): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetSize](#enum-sheetsize)|Yes|-|Another SheetSize enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise false.|

### operator func !=(SheetSize)

```cangjie
public operator func !=(other: SheetSize): Bool
```

**Function:** Determines whether two enum values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetSize](#enum-sheetsize)|Yes|-|Another SheetSize enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise false.|

## enum SheetType

```cangjie
public enum SheetType <: Equatable<SheetType> {
    | Bottom
    | Center
    | Popup
    | ...
}
```

**Function:** Sets the style of semi-modal dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SheetType](#enum-sheettype)>

### Bottom

```cangjie
Bottom
```

**Function:** Bottom dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Centered dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Popup

```cangjie
Popup
```

**Function:** Follow-hand dialog. The follow-hand dialog panel does not support follow-hand sliding, and the panel does not close when swiped downward.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SheetType)

```cangjie
public operator func ==(other: SheetType): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetType](#enum-sheettype)|Yes|-|Another SheetType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise false.|

### operator func !=(SheetType)

```cangjie
public operator func !=(other: SheetType): Bool
```

**Function:** Determines whether two enum values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetType](#enum-sheettype)|Yes|-|Another SheetType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise false.|

## enum SheetMode

```cangjie
public enum SheetMode <: Equatable<SheetMode> {
    | Overlay
    | Embedded
    | ...
}
```

**Function:** Sets the display hierarchy of semi-modal pages.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SheetMode](#enum-sheetmode)>

### Overlay

```cangjie
Overlay
```

**Function:** Sets the semi-modal panel to display at the top level within the current UIContext, above all pages. It shares the same hierarchy as dialog components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Embedded

```cangjie
Embedded
```

**Function:** Sets the semi-modal panel to display at the top level within the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SheetMode)

```cangjie
public operator func ==(other: SheetMode): Bool
```

**Function:** Determines whether two SheetMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetMode](#enum-sheetmode)|Yes|-|Another SheetMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise false.|

### operator func !=(SheetMode)

```cangjie
public operator func !=(other: SheetMode): Bool
```

**Function:** Determines whether two SheetMode enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SheetMode](#enum-sheetmode)|Yes|-|Another SheetMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise false.|

## enum ScrollSizeMode

```cangjie
public enum ScrollSizeMode <: Equatable<ScrollSizeMode> {
    | FollowDetent
    | Continuous
    | ...
}
```

**Function:** Sets the refresh timing of the content area during semi-modal panel sliding.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ScrollSizeMode](enum-scrollsizemode)>

### FollowDetent

```cangjie
FollowDetent
```

**Function:** Sets the semi-modal panel to update the content display area after follow-hand sliding ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Continuous

```cangjie
Continuous
```

**Function:** Sets the semi-modal panel to continuously update the content display area during sliding.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ScrollSizeMode)

```cangjie
public operator func ==(other: ScrollSizeMode): Bool
```

**Function:** Determines whether two ScrollSizeMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScrollSizeMode](./cj-common-types.md#enum-scrollsizemode)|Yes|-|Another ScrollSizeMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise false.|

### operator func !=(ScrollSizeMode)

```cangjie
public operator func !=(other: ScrollSizeMode): Bool
```

**Function:** Determines whether two ScrollSizeMode enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScrollSizeMode](./cj-common-types.md#enum-scrollsizemode)|Yes|-|Another ScrollSizeMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise false.|

## enum KeySource

```cangjie
public enum KeySource <: Equatable<KeySource> {
    | Unknown
    | Keyboard
    | ...
}
```

**Function:** Key source.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[KeySource](#enum-keysource)>

### Unknown

```cangjie
Unknown
```

**Function:** Unknown input device type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Keyboard

```cangjie
Keyboard
```

**Function:** Keyboard key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(KeySource)

```cangjie
public operator func ==(other: KeySource): Bool
```

**Function:** Determines whether two KeySource enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[KeySource](#enum-keysource)|Yes|-|Another KeySource enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise false.|

### operator func !=(KeySource)

```cangjie
public operator func !=(other: KeySource): Bool
```

**Function:** Determines whether two KeySource enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[KeySource](#enum-keysource)|Yes|-|Another KeySource enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise false.|
```## enum KeyType

```cangjie
public enum KeyType <: Equatable<KeyType> {
    | Unknown
    | Down
    | Up
    | ...
}
```

**Function:** Type of key event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<KeyType>

### Unknown

```cangjie
Unknown
```

**Function:** Unknown type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Down

```cangjie
Down
```

**Function:** Key press down event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Up

```cangjie
Up
```

**Function:** Key release event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(KeyType)

```cangjie
public operator func ==(other: KeyType): Bool
```

**Function:** Determines whether two KeyType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [KeyType](#enum-keytype) | Yes | - | Another KeyType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(KeyType)

```cangjie
public operator func !=(other: KeyType): Bool
```

**Function:** Determines whether two KeyType enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [KeyType](#enum-keytype) | Yes | - | Another KeyType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ModifierKey

```cangjie
public enum ModifierKey <: Equatable<ModifierKey> {
    | Ctrl
    | Shift
    | Alt
    | ...
}
```

**Function:** Input method modifier key types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ModifierKey](#enum-modifierkey)>

### Ctrl

```cangjie
Ctrl
```

**Function:** Represents the Ctrl key on the keyboard.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Shift

```cangjie
Shift
```

**Function:** Represents the Shift key on the keyboard.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Alt

```cangjie
Alt
```

**Function:** Represents the Alt key on the keyboard.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ModifierKey)

```cangjie
public operator func ==(other: ModifierKey): Bool
```

**Function:** Determines whether two ModifierKey enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ModifierKey](#enum-modifierkey) | Yes | - | Another ModifierKey enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ModifierKey)

```cangjie
public operator func !=(other: ModifierKey): Bool
```

**Function:** Determines whether two ModifierKey enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ModifierKey](#enum-modifierkey) | Yes | - | Another ModifierKey enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum FunctionKey

```cangjie
public enum FunctionKey <: Equatable<FunctionKey> {
    | Esc
    | F1
    | F2
    | F3
    | F4
    | F5
    | F6
    | F7
    | F8
    | F9
    | F10
    | F11
    | F12
    | Tab
    | ...
}
```

**Function:** Keyboard function keys.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FunctionKey](#enum-functionkey)>

### Esc

```cangjie
Esc
```

**Function:** Escape key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F1

```cangjie
F1
```

**Function:** F1 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F2

```cangjie
F2
```

**Function:** F2 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F3

```cangjie
F3
```

**Function:** F3 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F4

```cangjie
F4
```

**Function:** F4 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F5

```cangjie
F5
```

**Function:** F5 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F6

```cangjie
F6
```

**Function:** F6 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F7

```cangjie
F7
```

**Function:** F7 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F8

```cangjie
F8
```

**Function:** F8 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F9

```cangjie
F9
```

**Function:** F9 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F10

```cangjie
F10
```

**Function:** F10 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F11

```cangjie
F11
```

**Function:** F11 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### F12

```cangjie
F12
```

**Function:** F12 key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Tab

```cangjie
Tab
```

**Function:** Tab key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FunctionKey)

```cangjie
public operator func ==(other: FunctionKey): Bool
```

**Function:** Determines whether two FunctionKey enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FunctionKey](#enum-functionkey) | Yes | - | Another FunctionKey enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(FunctionKey)

```cangjie
public operator func !=(other: FunctionKey): Bool
```

**Function:** Determines whether two FunctionKey enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FunctionKey](#enum-functionkey) | Yes | - | Another FunctionKey enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum DataPanelType

```cangjie
public enum DataPanelType <: Equatable<DataPanelType> {
    | Circle
    | Line
    | ...
}
```

**Function:** Data panel type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[DataPanelType](#enum-datapaneltype)>

### Circle

```cangjie
Circle
```

**Function:** Circular data panel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Line

```cangjie
Line
```

**Function:** Linear data panel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(DataPanelType)

```cangjie
public operator func ==(other: DataPanelType): Bool
```

**Function:** Determines whether two DataPanelType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[DataPanelType](#enum-datapaneltype)|Yes|-|Another DataPanelType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(DataPanelType)

```cangjie
public operator func !=(other: DataPanelType): Bool
```

**Function:** Determines whether two DataPanelType enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[DataPanelType](#enum-datapaneltype)|Yes|-|Another DataPanelType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ItemState

```cangjie
public enum ItemState <: Equatable<ItemState> {
    | Normal
    | Disabled
    | Waiting
    | Skip
    | ...
}
```

**Function:** Item state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ItemState](#enum-itemstate)>

### Normal

```cangjie
Normal
```

**Function:** Normal state, where the right-side text button is displayed normally and can be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Disabled

```cangjie
Disabled
```

**Function:** Disabled state, where the right-side text button is displayed in gray and cannot be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Waiting

```cangjie
Waiting
```

**Function:** Waiting state, where the right-side text button is not displayed, and a progress bar is shown instead. The button cannot be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Skip

```cangjie
Skip
```

**Function:** Skip state, where the right-side text button displays "Skip" by default. Custom logic can be defined in the Stepper's onSkip callback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ItemState)

```cangjie
public operator func ==(other: ItemState): Bool
```

**Function:** Determines whether two ItemState enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ItemState](#enum-itemstate)|Yes|-|Another ItemState enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ItemState)

```cangjie
public operator func !=(other: ItemState): Bool
```

**Function:** Determines whether two ItemState enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ItemState](#enum-itemstate)|Yes|-|Another ItemState enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum RefreshStatus

```cangjie
public enum RefreshStatus <: Equatable<RefreshStatus> {
    | Inactive
    | Drag
    | OverDrag
    | Refresh
    | Done
    | ...
}
```

**Function:** Pull-down refresh status.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[RefreshStatus](#enum-refreshstatus)>

### Inactive

```cangjie
Inactive
```

**Function:** The refresh state of pull-down refresh.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Drag

```cangjie
Drag
```

**Function:** Pulling down, with the distance less than the refresh threshold.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OverDrag

```cangjie
OverDrag
```

**Function:** Pulling down, with the distance exceeding the refresh threshold.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Refresh

```cangjie
Refresh
```

**Function:** After pulling down, bouncing back to the refresh threshold and entering the refresh state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Done

```cangjie
Done
```

**Function:** Refresh completed, returning to the initial state (top).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(RefreshStatus)

```cangjie
public operator func ==(other: RefreshStatus): Bool
```

**Function:** Determines whether two RefreshStatus enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[RefreshStatus](#enum-refreshstatus)|Yes|-|Another RefreshStatus enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(RefreshStatus)

```cangjie
public operator func !=(other: RefreshStatus): Bool
```

**Function:** Determines whether two RefreshStatus enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[RefreshStatus](#enum-refreshstatus)|Yes|-|Another RefreshStatus enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SeekMode

```cangjie
public enum SeekMode <: Equatable<SeekMode> {
    | PreviousKeyframe
    | NextKeyframe
    | ClosestKeyframe
    | Accurate
    | ...
}
```

**Function:** Seek mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SeekMode](#enum-seekmode)>

### PreviousKeyframe

```cangjie
PreviousKeyframe
```

**Function:** Seeks to the previous nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NextKeyframe

```cangjie
NextKeyframe
```

**Function:** Seeks to the next nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ClosestKeyframe

```cangjie
ClosestKeyframe
```

**Function:** Seeks to the nearest keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Accurate

```cangjie
Accurate
```

**Function:** Precise seeking, regardless of whether it is a keyframe.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SeekMode)

```cangjie
public operator func ==(other: SeekMode): Bool
```

**Function:** Determines whether two SeekMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SeekMode](#enum-seekmode)|Yes|-|Another SeekMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SeekMode)

```cangjie
public operator func !=(other: SeekMode): Bool
```

**Function:** Determines whether two SeekMode enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SeekMode](#enum-seekmode)|Yes|-|Another SeekMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|```markdown
## enum PlaybackSpeed

```cangjie
public enum PlaybackSpeed <: Equatable<PlaybackSpeed> {
    | SpeedForward075X
    | SpeedForward100X
    | SpeedForward125X
    | SpeedForward175X
    | SpeedForward200X
    | ...
}
```

**Function:** Defines playback speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[PlaybackSpeed](#enum-playbackspeed)>

### SpeedForward075X

```cangjie
SpeedForward075X
```

**Function:** Plays at 0.75x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpeedForward100X

```cangjie
SpeedForward100X
```

**Function:** Plays at 1.00x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpeedForward125X

```cangjie
SpeedForward125X
```

**Function:** Plays at 1.25x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpeedForward175X

```cangjie
SpeedForward175X
```

**Function:** Plays at 1.75x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpeedForward200X

```cangjie
SpeedForward200X
```

**Function:** Plays at 2.00x speed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(PlaybackSpeed)

```cangjie
public operator func ==(other: PlaybackSpeed): Bool
```

**Function:** Determines whether two PlaybackSpeed enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PlaybackSpeed](#enum-playbackspeed) | Yes | - | Another PlaybackSpeed enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(PlaybackSpeed)

```cangjie
public operator func !=(other: PlaybackSpeed): Bool
```

**Function:** Determines whether two PlaybackSpeed enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PlaybackSpeed](#enum-playbackspeed) | Yes | - | Another PlaybackSpeed enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum SelectStatus

```cangjie
public enum SelectStatus <: Equatable<SelectStatus> {
    | All
    | Part
    | None
    | ...
}
```

**Function:** Defines the selection status type for checkboxes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SelectStatus](#enum-selectstatus)>

### All

```cangjie
All
```

**Function:** All checkboxes in a group are selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Part

```cangjie
Part
```

**Function:** Some checkboxes in a group are selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** No checkboxes in a group are selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SelectStatus)

```cangjie
public operator func ==(other: SelectStatus): Bool
```

**Function:** Determines whether two SelectStatus enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SelectStatus](#enum-selectstatus) | Yes | - | Another SelectStatus enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(SelectStatus)

```cangjie
public operator func !=(other: SelectStatus): Bool
```

**Function:** Determines whether two SelectStatus enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SelectStatus](#enum-selectstatus) | Yes | - | Another SelectStatus enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum AnimationStatus

```cangjie
public enum AnimationStatus <: Equatable<AnimationStatus> {
    | Initial
    | Running
    | Paused
    | Stopped
    | ...
}
```

**Function:** Defines animation playback status.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[AnimationStatus](#enum-animationstatus)>

### Initial

```cangjie
Initial
```

**Function:** Initial state of animation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Running

```cangjie
Running
```

**Function:** Animation is playing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Paused

```cangjie
Paused
```

**Function:** Animation is paused.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Stopped

```cangjie
Stopped
```

**Function:** Animation is stopped.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(AnimationStatus)

```cangjie
public operator func ==(other: AnimationStatus): Bool
```

**Function:** Determines whether two AnimationStatus enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimationStatus](#enum-animationstatus) | Yes | - | Another AnimationStatus enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(AnimationStatus)

```cangjie
public operator func !=(other: AnimationStatus): Bool
```

**Function:** Determines whether two AnimationStatus enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AnimationStatus](#enum-animationstatus) | Yes | - | Another AnimationStatus enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum FillMode

```cangjie
public enum FillMode <: Equatable<FillMode> {
    | None
    | Forwards
    | Backwards
    | Both
    | ...
}
```

**Function:** Defines the state before animation starts and after it ends in the current playback direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FillMode](#enum-fillmode)>

### None

```cangjie
None
```

**Function:** No styles are applied to the target when animation is not executed, and the initial default state is restored after animation completes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Forwards

```cangjie
Forwards
```

**Function:** The target retains the state of the last keyframe during animation execution.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Backwards

```cangjie
Backwards
```

**Function:** The animation immediately applies the value defined in the first keyframe when applied to the target and retains this value during the delay period. The first keyframe depends on playMode: it's the 'from' state when playMode is Normal or Alternate, and the 'to' state when playMode is Reverse or AlternateReverse.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Both

```cangjie
Both
```

**Function:** The animation follows both Forwards and Backwards rules, extending animation properties in both directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FillMode)

```cangjie
public operator func ==(other: FillMode): Bool
```

**Function:** Determines whether two FillMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FillMode](#enum-fillmode) | Yes | - | Another FillMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(FillMode)

```cangjie
public operator func !=(other: FillMode): Bool
```

**Function:** Determines whether two FillMode enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FillMode](#enum-fillmode) | Yes | - | Another FillMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |
```## enum SwipeEdgeEffect

```cangjie
public enum SwipeEdgeEffect <: Equatable<SwipeEdgeEffect> {
    | Spring
    | None
    | ...
}
```

**Function:** Swipe effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SwipeEdgeEffect](#enum-swipeedgeeffect)>

### Spring

```cangjie
Spring
```

**Function:** When the swipe distance of a ListItem exceeds the size of the swiped-out component, it can continue to be swiped. Upon release, it rebounds according to the spring damping curve.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** The swipe distance of a ListItem cannot exceed the size of the swiped-out component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SwipeEdgeEffect)

```cangjie
public operator func ==(other: SwipeEdgeEffect): Bool
```

**Function:** Determines whether two SwipeEdgeEffect enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeEdgeEffect](#enum-swipeedgeeffect) | Yes | - | The other SwipeEdgeEffect enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are equal; otherwise, returns `false`. |

### operator func !=(SwipeEdgeEffect)

```cangjie
public operator func !=(other: SwipeEdgeEffect): Bool
```

**Function:** Determines whether two SwipeEdgeEffect enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeEdgeEffect](#enum-swipeedgeeffect) | Yes | - | The other SwipeEdgeEffect enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are not equal; otherwise, returns `false`. |

## enum SharedTransitionEffectType

```cangjie
public enum SharedTransitionEffectType <: Equatable<SharedTransitionEffectType> {
    | Static
    | Exchange
    | ...
}
```

**Function:** Shared element transition animation type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SharedTransitionEffectType](#enum-sharedtransitioneffecttype)>

### Static

```cangjie
Static
```

**Function:** The position of the target page element remains unchanged, and opacity animation can be configured. Currently, only static effects configured for redirecting to the target page will take effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Exchange

```cangjie
Exchange
```

**Function:** Moves the source page element to the position of the target page element and scales it appropriately.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SharedTransitionEffectType)

```cangjie
public operator func ==(other: SharedTransitionEffectType): Bool
```

**Function:** Determines whether two SharedTransitionEffectType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SharedTransitionEffectType](#enum-sharedtransitioneffecttype) | Yes | - | The other SharedTransitionEffectType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are equal; otherwise, returns `false`. |

### operator func !=(SharedTransitionEffectType)

```cangjie
public operator func !=(other: SharedTransitionEffectType): Bool
```

**Function:** Determines whether two SharedTransitionEffectType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SharedTransitionEffectType](#enum-sharedtransitioneffecttype) | Yes | - | The other SharedTransitionEffectType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are not equal; otherwise, returns `false`. |

## enum ScrollState

```cangjie
public enum ScrollState <: Equatable<ScrollState> {
    | Idle
    | Scroll
    | Fling
    | ...
}
```

**Function:** Sets the current scroll state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ScrollState](#enum-scrollstate)>

### Idle

```cangjie
Idle
```

**Function:** Non-scrolling state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Scroll

```cangjie
Scroll
```

**Function:** Finger dragging state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Fling

```cangjie
Fling
```

**Function:** Inertial scrolling after dragging ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ScrollState)

```cangjie
public operator func ==(other: ScrollState): Bool
```

**Function:** Determines whether two ScrollState enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollState](#enum-scrollstate) | Yes | - | The other ScrollState enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are equal; otherwise, returns `false`. |

### operator func !=(ScrollState)

```cangjie
public operator func !=(other: ScrollState): Bool
```

**Function:** Determines whether two ScrollState enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollState](#enum-scrollstate) | Yes | - | The other ScrollState enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are not equal; otherwise, returns `false`. |

## enum ImageSmoothingQuality

```cangjie
public enum ImageSmoothingQuality <: Equatable<ImageSmoothingQuality> {
    | Low
    | Medium
    | High
    | ...
}
```

**Function:** Sets the image smoothing quality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageSmoothingQuality](#enum-imagesmoothingquality)>

### Low

```cangjie
Low
```

**Function:** Low quality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Medium

```cangjie
Medium
```

**Function:** Medium quality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### High

```cangjie
High
```

**Function:** High quality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageSmoothingQuality)

```cangjie
public operator func ==(other: ImageSmoothingQuality): Bool
```

**Function:** Determines whether two ImageSmoothingQuality enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSmoothingQuality](#enum-imagesmoothingquality) | Yes | - | The other ImageSmoothingQuality enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are equal; otherwise, returns `false`. |

### operator func !=(ImageSmoothingQuality)

```cangjie
public operator func !=(other: ImageSmoothingQuality): Bool
```

**Function:** Determines whether two ImageSmoothingQuality enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSmoothingQuality](#enum-imagesmoothingquality) | Yes | - | The other ImageSmoothingQuality enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are not equal; otherwise, returns `false`. |

## enum GestureMask

```cangjie
public enum GestureMask <: Equatable<GestureMask> {
    | Normal
    | IgnoreInternal
    | ...
}
```

**Function:** Gesture mask.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[GestureMask](#enum-gesturemask)>

### Normal

```cangjie
Normal
```

**Function:** Does not block child component gestures; recognizes gestures according to the default gesture recognition order.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### IgnoreInternal

```cangjie
IgnoreInternal
```

**Function:** Blocks child component gestures, including system-built-in gestures on child components (e.g., swipe gestures on List components). If parent and child components overlap partially, only the overlapping area is blocked.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(GestureMask)

```cangjie
public operator func ==(other: GestureMask): Bool
```

**Function:** Determines whether two GestureMask enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GestureMask](#enum-gesturemask) | Yes | - | The other GestureMask enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are equal; otherwise, returns `false`. |

### operator func !=(GestureMask)

```cangjie
public operator func !=(other: GestureMask): Bool
```

**Function:** Determines whether two GestureMask enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GestureMask](#enum-gesturemask) | Yes | - | The other GestureMask enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enums are not equal; otherwise, returns `false`. |## enum SwipeDirection

```cangjie
public enum SwipeDirection <: Equatable<SwipeDirection> {
    | Horizontal
    | Vertical
    | All
    | ...
}
```

**Function:** Specifies the swipe direction for triggering swipe gestures.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SwipeDirection](#enum-swipedirection)>

### Horizontal

```cangjie
Horizontal
```

**Function:** Horizontal direction. Triggered when the angle between the finger swipe direction and the x-axis is less than 45 degrees.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Vertical

```cangjie
Vertical
```

**Function:** Vertical direction. Triggered when the angle between the finger swipe direction and the y-axis is less than 45 degrees.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### All

```cangjie
All
```

**Function:** All directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SwipeDirection)

```cangjie
public operator func ==(other: SwipeDirection): Bool
```

**Function:** Determines whether two SwipeDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeDirection](#enum-swipedirection) | Yes | - | The other SwipeDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(SwipeDirection)

```cangjie
public operator func !=(other: SwipeDirection): Bool
```

**Function:** Determines whether two SwipeDirection enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeDirection](#enum-swipedirection) | Yes | - | The other SwipeDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum PanDirection

```cangjie
public enum PanDirection <: Equatable<PanDirection> {
    | None
    | Left
    | Right
    | Horizontal
    | Up
    | Down
    | Vertical
    | All
    | Computed(UInt32)
    | ...
}
```

**Function:** Specifies the direction for pan gestures.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[PanDirection](#enum-pandirection)>

### None

```cangjie
None
```

**Function:** All directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Left

```cangjie
Left
```

**Function:** Pan to the left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** Pan to the right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Horizontal

```cangjie
Horizontal
```

**Function:** Horizontal direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Up

```cangjie
Up
```

**Function:** Pan upward.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Down

```cangjie
Down
```

**Function:** Pan downward.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Vertical

```cangjie
Vertical
```

**Function:** Vertical direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### All

```cangjie
All
```

**Function:** All directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Computed(UInt32)

```cangjie
Computed(UInt32)
```

**Function:** Supports logical AND (&) and logical OR (|) operations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(PanDirection)

```cangjie
public operator func ==(other: PanDirection): Bool
```

**Function:** Determines whether two PanDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PanDirection](#enum-pandirection) | Yes | - | The other PanDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(PanDirection)

```cangjie
public operator func !=(other: PanDirection): Bool
```

**Function:** Determines whether two PanDirection enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [PanDirection](#enum-pandirection) | Yes | - | The other PanDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

### operator func |(PanDirection)

```cangjie
public operator func |(right: PanDirection): PanDirection
```

**Function:** Performs a logical OR (|) operation on PanDirection.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| right | [PanDirection](#enum-pandirection) | Yes | - | The PanDirection enum for the logical OR operation. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PanDirection](#enum-pandirection) | The result of the logical OR operation. |

### operator func &(PanDirection)

```cangjie
public operator func &(right: PanDirection): PanDirection
```

**Function:** Performs a logical AND (&) operation on PanDirection.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| right | [PanDirection](#enum-pandirection) | Yes | - | The PanDirection enum for the logical AND operation. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PanDirection](#enum-pandirection) | The result of the logical AND operation. |

## enum GestureMode

```cangjie
public enum GestureMode <: Equatable<GestureMode> {
    | Sequence
    | Parallel
    | Exclusive
    | ...
}
```

**Function:** Specifies the recognition mode for combined gestures.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[GestureMode](#enum-gesturemode)>

### Sequence

```cangjie
Sequence
```

**Function:** Sequential recognition. Gestures are recognized in the order they are registered until all gestures are successfully recognized. If any gesture fails, subsequent gestures will also fail. Only the last gesture in a sequential recognition group can respond to onActionEnd.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Parallel

```cangjie
Parallel
```

**Function:** Concurrent recognition. All registered gestures are recognized simultaneously until all gestures complete, without affecting each other.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Exclusive

```cangjie
Exclusive
```

**Function:** Mutually exclusive recognition. All registered gestures are recognized simultaneously. If any gesture is successfully recognized, the gesture recognition process ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(GestureMode)

```cangjie
public operator func ==(other: GestureMode): Bool
```

**Function:** Determines whether two GestureMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GestureMode](#enum-gesturemode) | Yes | - | The other GestureMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(GestureMode)

```cangjie
public operator func !=(other: GestureMode): Bool
```

**Function:** Determines whether two GestureMode enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GestureMode](#enum-gesturemode) | Yes | - | The other GestureMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum Axis

```cangjie
public enum Axis <: Equatable<Axis> {
    | Vertical
    | Horizontal
    | ...
}
```

**Function:** Axis direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Axis](#enum-axis)>

### Vertical

```cangjie
Vertical
```

**Function:** Vertical direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Horizontal

```cangjie
Horizontal
```

**Function:** Horizontal direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Axis)

```cangjie
public operator func ==(other: Axis): Bool
```

**Function:** Determines whether two Axis enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Axis](#enum-axis) | Yes | - | Another Axis enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(Axis)

```cangjie
public operator func !=(other: Axis): Bool
```

**Function:** Determines whether two Axis enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Axis](#enum-axis) | Yes | - | Another Axis enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ResponseType

```cangjie
public enum ResponseType <: Equatable<ResponseType> {
    | RightClick
    | LongPress
    | ...
}
```

**Function:** Response type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ResponseType](#enum-responsetype)>

### RightClick

```cangjie
RightClick
```

**Function:** Triggers menu popup via right mouse click.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LongPress

```cangjie
LongPress
```

**Function:** Triggers menu popup via long press.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ResponseType)

```cangjie
public operator func ==(other: ResponseType): Bool
```

**Function:** Determines whether two ResponseType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ResponseType](#enum-responsetype) | Yes | - | Another ResponseType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ResponseType)

```cangjie
public operator func !=(other: ResponseType): Bool
```

**Function:** Determines whether two ResponseType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ResponseType](#enum-responsetype) | Yes | - | Another ResponseType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum CopyOptions

```cangjie
public enum CopyOptions <: Equatable<CopyOptions> {
    | None
    | InApp
    | LocalDevice
    | ...
}
```

**Function:** Text copy mode for input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[CopyOptions](#enum-copyoptions)>

### None

```cangjie
None
```

**Function:** Copying is not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### InApp

```cangjie
InApp
```

**Function:** Supports in-app copying.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LocalDevice

```cangjie
LocalDevice
```

**Function:** Supports copying within the device.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(CopyOptions)

```cangjie
public operator func ==(other: CopyOptions): Bool
```

**Function:** Determines whether two CopyOptions enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CopyOptions](#enum-copyoptions) | Yes | - | Another CopyOptions enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(CopyOptions)

```cangjie
public operator func !=(other: CopyOptions): Bool
```

**Function:** Determines whether two CopyOptions enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CopyOptions](#enum-copyoptions) | Yes | - | Another CopyOptions enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum TouchType

```cangjie
public enum TouchType <: Equatable<TouchType> {
    | Down
    | Up
    | Move
    | Cancel
    | Unknown
    | ...
}
```

**Function:** Touch trigger method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TouchType](#enum-touchtype)>

### Down

```cangjie
Down
```

**Function:** Triggered when a finger presses down.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Up

```cangjie
Up
```

**Function:** Triggered when a finger lifts up.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Move

```cangjie
Move
```

**Function:** Triggered when a pressed finger moves on the screen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Cancel

```cangjie
Cancel
```

**Function:** Triggered when a touch event is canceled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Unknown

```cangjie
Unknown
```

**Function:** Triggered for unknown touch operations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TouchType)

```cangjie
public operator func ==(other: TouchType): Bool
```

**Function:** Determines whether two TouchType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TouchType](#enum-touchtype) | Yes | - | Another TouchType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TouchType)

```cangjie
public operator func !=(other: TouchType): Bool
```

**Function:** Determines whether two TouchType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TouchType](#enum-touchtype) | Yes | - | Another TouchType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum SideBarContainerType

```cangjie
public enum SideBarContainerType <: Equatable<SideBarContainerType> {
    | Embed
    | Overlay
    | Auto
    | ...
}
```

**Function:** Enumeration for sidebar container styles.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SideBarContainerType](#enum-sidebarcontainertype)>

### Embed

```cangjie
Embed
```

**Function:** The sidebar is embedded within the component and displayed alongside the content area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Overlay

```cangjie
Overlay
```

**Function:** The sidebar floats above the content area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Function:** Web dark mode follows the system settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SideBarContainerType)

```cangjie
public operator func ==(other: SideBarContainerType): Bool
```

**Function:** Determines whether two SideBarContainerType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SideBarContainerType](#enum-sidebarcontainertype)|Yes|-|The other SideBarContainerType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SideBarContainerType)

```cangjie
public operator func !=(other: SideBarContainerType): Bool
```

**Function:** Determines whether two SideBarContainerType enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SideBarContainerType](#enum-sidebarcontainertype)|Yes|-|The other SideBarContainerType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SideBarPosition

```cangjie
public enum SideBarPosition <: Equatable<SideBarPosition> {
    | Start
    | End
    | ...
}
```

**Function:** Sets the display position of the sidebar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SideBarPosition](#enum-sidebarposition)>

### Start

```cangjie
Start
```

**Function:** The sidebar is positioned on the left side of the container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** The sidebar is positioned on the right side of the container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SideBarPosition)

```cangjie
public operator func ==(other: SideBarPosition): Bool
```

**Function:** Determines whether two SideBarPosition enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SideBarPosition](#enum-sidebarposition)|Yes|-|The other SideBarPosition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SideBarPosition)

```cangjie
public operator func !=(other: SideBarPosition): Bool
```

**Function:** Determines whether two SideBarPosition enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SideBarPosition](#enum-sidebarposition)|Yes|-|The other SideBarPosition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SourceType

```cangjie
public enum SourceType <: Equatable<SourceType> {
    | Unknown
    | Mouse
    | TouchScreen
    | ...
}
```

**Function:** Event input device.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SourceType](#enum-sourcetype)>

### Unknown

```cangjie
Unknown
```

**Function:** Unknown device.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Mouse

```cangjie
Mouse
```

**Function:** Mouse input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TouchScreen

```cangjie
TouchScreen
```

**Function:** Touchscreen type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SourceType)

```cangjie
public operator func ==(other: SourceType): Bool
```

**Function:** Determines whether two SourceType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SourceType](#enum-sourcetype)|Yes|-|The other SourceType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SourceType)

```cangjie
public operator func !=(other: SourceType): Bool
```

**Function:** Determines whether two SourceType enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[SourceType](#enum-sourcetype)|Yes|-|The other SourceType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum MouseButton

```cangjie
public enum MouseButton <: Equatable<MouseButton> {
    | None
    | Left
    | Right
    | Middle
    | Back
    | Forward
    | ...
}
```

**Function:** Mouse buttons.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[MouseButton](#enum-mousebutton)>

### None

```cangjie
None
```

**Function:** No button pressed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Left

```cangjie
Left
```

**Function:** Left mouse button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** Right mouse button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Middle

```cangjie
Middle
```

**Function:** Middle mouse button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Back

```cangjie
Back
```

**Function:** Mouse back button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Forward

```cangjie
Forward
```

**Function:** Mouse forward button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(MouseButton)

```cangjie
public operator func ==(other: MouseButton): Bool
```

**Function:** Determines whether two MouseButton enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MouseButton](#enum-mousebutton)|Yes|-|The other MouseButton enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(MouseButton)

```cangjie
public operator func !=(other: MouseButton): Bool
```

**Function:** Determines whether two MouseButton enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MouseButton](#enum-mousebutton)|Yes|-|The other MouseButton enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum MouseAction

```cangjie
public enum MouseAction <: Equatable<MouseAction> {
    | None
    | Press
    | Release
    | Move
    | Hover
    | ...
}
```

**Description:** Mouse actions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[MouseAction](#enum-mouseaction)>

### None

```cangjie
None
```

**Description:** No operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Press

```cangjie
Press
```

**Description:** Mouse button pressed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Release

```cangjie
Release
```

**Description:** Mouse button released.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Move

```cangjie
Move
```

**Description:** Mouse movement.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Hover

```cangjie
Hover
```

**Description:** Mouse hover. **Note:** This enum value is invalid.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(MouseAction)

```cangjie
public operator func ==(other: MouseAction): Bool
```

**Description:** Determines whether two MouseAction enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MouseAction](#enum-mouseaction) | Yes | - | Another MouseAction enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(MouseAction)

```cangjie
public operator func !=(other: MouseAction): Bool
```

**Description:** Determines whether two MouseAction enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MouseAction](#enum-mouseaction) | Yes | - | Another MouseAction enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum SliderStyle

```cangjie
public enum SliderStyle <: Equatable<SliderStyle> {
    | OutSet
    | InSet
    | ...
}
```

**Description:** Display style of the slider and track in Slider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SliderStyle](#enum-sliderstyle)>

### OutSet

```cangjie
OutSet
```

**Description:** Slider is inside the track.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### InSet

```cangjie
InSet
```

**Description:** Knob-in style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SliderStyle)

```cangjie
public operator func ==(other: SliderStyle): Bool
```

**Description:** Determines whether two SliderStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SliderStyle](#enum-sliderstyle) | Yes | - | Another SliderStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(SliderStyle)

```cangjie
public operator func !=(other: SliderStyle): Bool
```

**Description:** Determines whether two SliderStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SliderStyle](#enum-sliderstyle) | Yes | - | Another SliderStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ImageInterpolation

```cangjie
public enum ImageInterpolation <: Equatable<ImageInterpolation> {
    | None
    | High
    | Medium
    | Low
    | ...
}
```

**Description:** Image interpolation method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageInterpolation](#enum-imageinterpolation)>

### None

```cangjie
None
```

**Description:** No interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### High

```cangjie
High
```

**Description:** High-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Medium

```cangjie
Medium
```

**Description:** Medium-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Low

```cangjie
Low
```

**Description:** Low-quality interpolation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageInterpolation)

```cangjie
public operator func ==(other: ImageInterpolation): Bool
```

**Description:** Determines whether two ImageInterpolation enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageInterpolation](#enum-imageinterpolation) | Yes | - | Another ImageInterpolation enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ImageInterpolation)

```cangjie
public operator func !=(other: ImageInterpolation): Bool
```

**Description:** Determines whether two ImageInterpolation enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageInterpolation](#enum-imageinterpolation) | Yes | - | Another ImageInterpolation enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum BarState

```cangjie
public enum BarState <: Equatable<BarState> {
    | Off
    | Auto
    | On
    | ...
}
```

**Description:** Display mode of the scrollbar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BarState](#enum-barstate)>

### Off

```cangjie
Off
```

**Description:** Not displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Description:** Displayed on demand (shown when touched, disappears after 2 seconds).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### On

```cangjie
On
```

**Description:** Always displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BarState)

```cangjie
public operator func ==(other: BarState): Bool
```

**Description:** Determines whether two BarState enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BarState](#enum-barstate) | Yes | - | Another BarState enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(BarState)

```cangjie
public operator func !=(other: BarState): Bool
```

**Description:** Determines whether two BarState enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BarState](#enum-barstate) | Yes | - | Another BarState enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum Visibility

```cangjie
public enum Visibility <: Equatable<Visibility> {
    | Visible
    | Hidden
    | None
    | ...
}
```

**Function:** Controls the display or hiding of the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Visibility](#enum-visibility)>

### Visible

```cangjie
Visible
```

**Function:** Display the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Hidden

```cangjie
Hidden
```

**Function:** Hide the component while still occupying space in the layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** Hide the component without occupying space in the layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Visibility)

```cangjie
public operator func ==(other: Visibility): Bool
```

**Function:** Determines whether two Visibility enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Visibility](#enum-visibility)|Yes|-|The other Visibility enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(Visibility)

```cangjie
public operator func !=(other: Visibility): Bool
```

**Function:** Determines whether two Visibility enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Visibility](#enum-visibility)|Yes|-|The other Visibility enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum LineCapStyle

```cangjie
public enum LineCapStyle <: Equatable<LineCapStyle> {
    | Butt
    | Round
    | Square
    | ...
}
```

**Function:** Line cap style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[LineCapStyle](#enum-linecapstyle)>

### Butt

```cangjie
Butt
```

**Function:** The line ends are squared off and do not extend beyond the endpoints.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Round

```cangjie
Round
```

**Function:** The line ends are rounded with a semicircle whose diameter equals the line width.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Square

```cangjie
Square
```

**Function:** The line ends are squared off and extended by half the line width.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(LineCapStyle)

```cangjie
public operator func ==(other: LineCapStyle): Bool
```

**Function:** Determines whether two LineCapStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[LineCapStyle](#enum-linecapstyle)|Yes|-|The other LineCapStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(LineCapStyle)

```cangjie
public operator func !=(other: LineCapStyle): Bool
```

**Function:** Determines whether two LineCapStyle enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[LineCapStyle](#enum-linecapstyle)|Yes|-|The other LineCapStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ProgressType

```cangjie
public enum ProgressType <: Equatable<ProgressType> {
    | Linear
    | Ring
    | Eclipse
    | ScaleRing
    | Capsule
    | ...
}
```

**Function:** Style type of the Progress component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ProgressType](#enum-progresstype)>

### Linear

```cangjie
Linear
```

**Function:** Linear style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Ring

```cangjie
Ring
```

**Function:** Ring style without scales, displaying a gradually filling circular ring effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Eclipse

```cangjie
Eclipse
```

**Function:** Circular style, displaying a progress effect similar to the phases of the moon, transitioning from a crescent to a full moon.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ScaleRing

```cangjie
ScaleRing
```

**Function:** Ring style with scales, displaying a progress effect similar to clock ticks.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Capsule

```cangjie
Capsule
```

**Function:** Capsule style, where the progress display effect at the rounded ends is the same as Eclipse, and the middle section follows the Linear style. Automatically adjusts to vertical display when height exceeds width.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ProgressType)

```cangjie
public operator func ==(other: ProgressType): Bool
```

**Function:** Determines whether two ProgressType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ProgressType](#enum-progresstype)|Yes|-|The other ProgressType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ProgressType)

```cangjie
public operator func !=(other: ProgressType): Bool
```

**Function:** Determines whether two ProgressType enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ProgressType](#enum-progresstype)|Yes|-|The other ProgressType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ImageRenderMode

```cangjie
public enum ImageRenderMode <: Equatable<ImageRenderMode> {
    | Original
    | Template
    | ...
}
```

**Function:** Image rendering mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageRenderMode](#enum-imagerendermode)>

### Original

```cangjie
Original
```

**Function:** Renders the image as-is, including its colors.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Template

```cangjie
Template
```

**Function:** Renders the image as a template, ignoring its color information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageRenderMode)

```cangjie
public operator func ==(other: ImageRenderMode): Bool
```

**Function:** Determines whether two ImageRenderMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRenderMode](#enum-imagerendermode)|Yes|-|The other ImageRenderMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ImageRenderMode)

```cangjie
public operator func !=(other: ImageRenderMode): Bool
```

**Function:** Determines whether two ImageRenderMode enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ImageRenderMode](#enum-imagerendermode)|Yes|-|The other ImageRenderMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum NavigationType

```cangjie
public enum NavigationType <: Equatable<NavigationType> {
    | Push
    | Replace
    | Back
    | ...
}
```

**Function:** Page navigation method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[NavigationType](#enum-navigationtype)>

### Push

```cangjie
Push
```

**Function:** Navigates to a specified page within the application.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Replace

```cangjie
Replace
```

**Function:** Replaces the current page with another page within the application and destroys the replaced page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Back

```cangjie
Back
```

**Function:** Returns to a specified page. No response if the specified page does not exist in the stack. Returns to the previous page when no target page is specified.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(NavigationType)

```cangjie
public operator func ==(other: NavigationType): Bool
```

**Function:** Determines whether two NavigationType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NavigationType](#enum-navigationtype)|Yes|-|Another NavigationType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(NavigationType)

```cangjie
public operator func !=(other: NavigationType): Bool
```

**Function:** Determines whether two NavigationType enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NavigationType](#enum-navigationtype)|Yes|-|Another NavigationType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SwiperDisplayMode

```cangjie
public enum SwiperDisplayMode <: Equatable<SwiperDisplayMode> {
    | Stretch
    | ...
}
```

**Function:** Enumeration for Swiper's size mode on the main axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SwiperDisplayMode](#enum-swiperdisplaymode)>

### Stretch

```cangjie
Stretch
```

**Function:** The width of one swipe page equals the width of the Swiper component itself.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SwiperDisplayMode)

```cangjie
public operator func ==(other: SwiperDisplayMode): Bool
```

**Function:** Determines whether two SwiperDisplayMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SwiperDisplayMode](#enum-swiperdisplaymode)|Yes|-|Another SwiperDisplayMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SwiperDisplayMode)

```cangjie
public operator func !=(other: SwiperDisplayMode): Bool
```

**Function:** Determines whether two SwiperDisplayMode enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SwiperDisplayMode](#enum-swiperdisplaymode)|Yes|-|Another SwiperDisplayMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum Curve

```cangjie
public enum Curve <: Equatable<Curve> {
    | Linear
    | Ease
    | EaseIn
    | EaseOut
    | EaseInOut
    | FastOutSlowIn
    | LinearOutSlowIn
    | FastOutLinearIn
    | ExtremeDeceleration
    | Sharp
    | Rhythm
    | Smooth
    | Friction
    | ...
}
```

**Function:** Animation curves.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Curve](#enum-curve)>

### Linear

```cangjie
Linear
```

**Function:** Indicates an animation with constant speed from start to end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Ease

```cangjie
Ease
```

**Function:** Indicates an animation that starts slowly, accelerates, then slows down before ending (CubicBezier(0.25, 0.1, 0.25, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### EaseIn

```cangjie
EaseIn
```

**Function:** Indicates an animation that starts slowly (CubicBezier(0.42, 0.0, 1.0, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### EaseOut

```cangjie
EaseOut
```

**Function:** Indicates an animation that ends slowly (CubicBezier(0.0, 0.0, 0.58, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### EaseInOut

```cangjie
EaseInOut
```

**Function:** Indicates an animation that starts and ends slowly (CubicBezier(0.42, 0.0, 0.58, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FastOutSlowIn

```cangjie
FastOutSlowIn
```

**Function:** Standard curve (cubic-bezier(0.4, 0.0, 0.2, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LinearOutSlowIn

```cangjie
LinearOutSlowIn
```

**Function:** Deceleration curve (cubic-bezier(0.0, 0.0, 0.2, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FastOutLinearIn

```cangjie
FastOutLinearIn
```

**Function:** Acceleration curve (cubic-bezier(0.4, 0.0, 1.0, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ExtremeDeceleration

```cangjie
ExtremeDeceleration
```

**Function:** Extreme deceleration curve (cubic-bezier(0.0, 0.0, 0.0, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Sharp

```cangjie
Sharp
```

**Function:** Sharp curve (CubicBezier(0.4, 0.0, 0.6, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Rhythm

```cangjie
Rhythm
```

**Function:** Rhythm curve (CubicBezier(0.7, 0.0, 0.2, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Smooth

```cangjie
Smooth
```

**Function:** Smooth curve (CubicBezier(0.4, 0.0, 0.2, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Friction

```cangjie
Friction
```

**Function:** Friction curve (CubicBezier(0.2, 0.0, 0.2, 1.0)).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Curve)

```cangjie
public operator func ==(other: Curve): Bool
```

**Function:** Determines whether two Curve enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Curve](#enum-curve)|Yes|-|Another Curve enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(Curve)

```cangjie
public operator func !=(other: Curve): Bool
```

**Function:** Determines whether two Curve enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Curve](#enum-curve)|Yes|-|Another Curve enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum EdgeEffect

```cangjie
public enum EdgeEffect <: Equatable<EdgeEffect> {
    | Spring
    | Fade
    | None
    | ...
}
```

**Function:** Edge scrolling effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[EdgeEffect](#enum-edgeeffect)>

### Spring

```cangjie
Spring
```

**Function:** Elastic physics animation effect. When scrolling to the edge, it can continue scrolling for a distance based on initial velocity or touch events, then bounce back upon release.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Fade

```cangjie
Fade
```

**Function:** Shadow effect. When scrolling to the edge, a circular arc-shaped shadow appears.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** No effect when scrolling to the edge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(EdgeEffect)

```cangjie
public operator func ==(other: EdgeEffect): Bool
```

**Function:** Determines whether two EdgeEffect enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[EdgeEffect](#enum-edgeeffect)|Yes|-|Another EdgeEffect enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(EdgeEffect)

```cangjie
public operator func !=(other: EdgeEffect): Bool
```

**Function:** Determines whether two EdgeEffect enums are not equal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[EdgeEffect](#enum-edgeeffect)|Yes|-|Another EdgeEffect enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum Edge

```cangjie
public enum Edge <: Equatable<Edge> {
    | Top
    | Start
    | Bottom
    | End
    | ...
}
```

**Function:** Scrolling to container edges.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Edge](#enum-edge)>

### Top

```cangjie
Top
```

**Function:** Top edge in the vertical direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** Starting position in the horizontal direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Bottom edge in the vertical direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Ending position in the horizontal direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Edge)

```cangjie
public operator func ==(other: Edge): Bool
```

**Function:** Determines whether two Edge enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Edge](#enum-edge)|Yes|-|Another Edge enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(Edge)

```cangjie
public operator func !=(other: Edge): Bool
```

**Function:** Determines whether two Edge enums are not equal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Edge](#enum-edge)|Yes|-|Another Edge enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum Placement

```cangjie
public enum Placement <: Equatable<Placement> {
    | Left
    | Right
    | Top
    | Bottom
    | TopLeft
    | TopRight
    | BottomLeft
    | BottomRight
    | LeftTop
    | LeftBottom
    | RightTop
    | RightBottom
    | ...
}
```

**Function:** Bubble prompt position setting.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Placement](#enum-placement)>

### Left

```cangjie
Left
```

**Function:** Bubble prompt is positioned to the left of the component, aligned with the left center of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** Bubble prompt is positioned to the right of the component, aligned with the right center of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Top

```cangjie
Top
```

**Function:** Bubble prompt is positioned above the component, aligned with the top center of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Bubble prompt is positioned below the component, aligned with the bottom center of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopLeft

```cangjie
TopLeft
```

**Function:** Bubble prompt is positioned above the component, aligned with the left edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopRight

```cangjie
TopRight
```

**Function:** Bubble prompt is positioned above the component, aligned with the right edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomLeft

```cangjie
BottomLeft
```

**Function:** Bubble prompt is positioned below the component, aligned with the left edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomRight

```cangjie
BottomRight
```

**Function:** Bubble prompt is positioned below the component, aligned with the right edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LeftTop

```cangjie
LeftTop
```

**Function:** Bubble prompt is positioned to the left of the component, aligned with the top edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LeftBottom

```cangjie
LeftBottom
```

**Function:** Bubble prompt is positioned to the left of the component, aligned with the bottom edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RightTop

```cangjie
RightTop
```

**Function:** Bubble prompt is positioned to the right of the component, aligned with the top edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RightBottom

```cangjie
RightBottom
```

**Function:** Bubble prompt is positioned to the right of the component, aligned with the bottom edge of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Placement)

```cangjie
public operator func ==(other: Placement): Bool
```

**Function:** Determines whether two Placement enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Placement](#enum-placement)|Yes|-|Another Placement enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(Placement)

```cangjie
public operator func !=(other: Placement): Bool
```

**Function:** Determines whether two Placement enums are not equal.

**Parameters:**

|Parameter|Type|Mandatory|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Placement](#enum-placement)|Yes|-|Another Placement enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum LineJoinStyle

```cangjie
public enum LineJoinStyle <: Equatable<LineJoinStyle> {
    | Miter
    | Round
    | Bevel
    | ...
}
```

**Description:** Path segment joining style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[LineJoinStyle](#enum-linejoinstyle)>

### Miter

```cangjie
Miter
```

**Description:** Joins path segments with sharp corners.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Round

```cangjie
Round
```

**Description:** Joins path segments with rounded corners.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bevel

```cangjie
Bevel
```

**Description:** Joins path segments with beveled edges.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(LineJoinStyle)

```cangjie
public operator func ==(other: LineJoinStyle): Bool
```

**Description:** Determines whether two LineJoinStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[LineJoinStyle](#enum-linejoinstyle)|Yes|-|Another LineJoinStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(LineJoinStyle)

```cangjie
public operator func !=(other: LineJoinStyle): Bool
```

**Description:** Determines whether two LineJoinStyle enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[LineJoinStyle](#enum-linejoinstyle)|Yes|-|Another LineJoinStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum BarPosition

```cangjie
public enum BarPosition <: Equatable<BarPosition> {
    | Start
    | End
    | ...
}
```

**Description:** Sets the layout position of TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BarPosition](#enum-barposition)>

### Start

```cangjie
Start
```

**Description:** Positioned at the start.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Description:** Positioned at the end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BarPosition)

```cangjie
public operator func ==(other: BarPosition): Bool
```

**Description:** Determines whether two BarPosition enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarPosition](#enum-barposition)|Yes|-|Another BarPosition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(BarPosition)

```cangjie
public operator func !=(other: BarPosition): Bool
```

**Description:** Determines whether two BarPosition enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarPosition](#enum-barposition)|Yes|-|Another BarPosition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum BarMode

```cangjie
public enum BarMode <: Equatable<BarMode> {
    | Fixed
    | Scrollable
    | ...
}
```

**Description:** TabBar layout mode enumeration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BarMode](#enum-barmode)>

### Fixed

```cangjie
Fixed
```

**Description:** All TabBars evenly divide the screen width, and TabBars are not scrollable.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Scrollable

```cangjie
Scrollable
```

**Description:** All TabBars are laid out according to their own dimensions, and TabBars are scrollable.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BarMode)

```cangjie
public operator func ==(other: BarMode): Bool
```

**Description:** Determines whether two BarMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarMode](#enum-barmode)|Yes|-|Another BarMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(BarMode)

```cangjie
public operator func !=(other: BarMode): Bool
```

**Description:** Determines whether two BarMode enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarMode](#enum-barmode)|Yes|-|Another BarMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ShadowType

```cangjie
public enum ShadowType <: Equatable<ShadowType> {
    | Color
    | Blur
    | ...
}
```

**Description:** Shadow type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ShadowType](#enum-shadowtype)>

### Color

```cangjie
Color
```

**Description:** Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Blur

```cangjie
Blur
```

**Description:** Blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ShadowType)

```cangjie
public operator func ==(other: ShadowType): Bool
```

**Description:** Determines whether two ShadowType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ShadowType](#enum-shadowtype)|Yes|-|Another ShadowType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ShadowType)

```cangjie
public operator func !=(other: ShadowType): Bool
```

**Description:** Determines whether two ShadowType enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ShadowType](#enum-shadowtype)|Yes|-|Another ShadowType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum TextDecorationType

```cangjie
public enum TextDecorationType <: Equatable<TextDecorationType> {
    | None
    | Underline
    | Overline
    | LineThrough
    | ...
}
```

**Description:** Text decoration line type enumeration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextDecorationType](#enum-textdecorationtype)>

### None

```cangjie
None
```

**Description:** No text decoration line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Underline

```cangjie
Underline
```

**Description:** Underline below the text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Overline

```cangjie
Overline
```

**Description:** Overline above the text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LineThrough

```cangjie
LineThrough
```

**Description:** Line through the text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextDecorationType)

```cangjie
public operator func ==(other: TextDecorationType): Bool
```

**Description:** Determines whether two TextDecorationType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[TextDecorationType](#enum-textdecorationtype)|Yes|-|Another TextDecorationType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(TextDecorationType)

```cangjie
public operator func !=(other: TextDecorationType): Bool
```

**Description:** Determines whether two TextDecorationType enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[TextDecorationType](#enum-textdecorationtype)|Yes|-|Another TextDecorationType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum TextAlign

```cangjie
public enum TextAlign <: Equatable<TextAlign> {
    | Start
    | Center
    | End
    | ...
}
```

**Description:** Text alignment mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextAlign](#enum-textalign)>

### Start

```cangjie
Start
```

**Description:** Align text horizontally to the start.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Description:** Align text horizontally to the center.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Description:** Align text horizontally to the end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextAlign)

```cangjie
public operator func ==(other: TextAlign): Bool
```

**Description:** Determines whether two TextAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextAlign](#enum-textalign) | Yes | - | Another TextAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextAlign)

```cangjie
public operator func !=(other: TextAlign): Bool
```

**Description:** Determines whether two TextAlign enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextAlign](#enum-textalign) | Yes | - | Another TextAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum TextOverflow

```cangjie
public enum TextOverflow <: Equatable<TextOverflow> {
    | Clip
    | Ellipsis
    | None
    | ...
}
```

**Description:** Display mode when text overflows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextOverflow](#enum-textoverflow)>

### Clip

```cangjie
Clip
```

**Description:** Truncate text at the maximum line when it overflows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Ellipsis

```cangjie
Ellipsis
```

**Description:** Replace overflowing text with ellipsis when it exceeds the display area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Description:** Truncate text at the maximum line when it overflows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextOverflow)

```cangjie
public operator func ==(other: TextOverflow): Bool
```

**Description:** Determines whether two TextOverflow enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextOverflow](#enum-textoverflow) | Yes | - | Another TextOverflow enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextOverflow)

```cangjie
public operator func !=(other: TextOverflow): Bool
```

**Description:** Determines whether two TextOverflow enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextOverflow](#enum-textoverflow) | Yes | - | Another TextOverflow enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum WordBreak

```cangjie
public enum WordBreak <: Equatable<WordBreak> {
    | Normal
    | BreakAll
    | BreakWord
    | ...
}
```

**Description:** Sets text line-breaking rules.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[WordBreak](#enum-wordbreak)>

### Normal

```cangjie
Normal
```

**Description:** CJK (Chinese, Japanese, Korean) text can break between any two characters, while Non-CJK text (e.g., English) can only break at whitespace.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BreakAll

```cangjie
BreakAll
```

**Description:** For Non-CJK text, can break between any two characters. For CJK text, behaves the same as NORMAL.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BreakWord

```cangjie
BreakWord
```

**Description:** Same as BREAKALL for Non-CJK text, can break between any two characters. If a line has break points (e.g., whitespace), it prioritizes breaking at those points to ensure word integrity. If no break points exist in a line, it breaks between any two characters. For CJK text, behaves the same as NORMAL.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(WordBreak)

```cangjie
public operator func ==(other: WordBreak): Bool
```

**Description:** Determines whether two WordBreak enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WordBreak](#enum-wordbreak) | Yes | - | Another WordBreak enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(WordBreak)

```cangjie
public operator func !=(other: WordBreak): Bool
```

**Description:** Determines whether two WordBreak enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WordBreak](#enum-wordbreak) | Yes | - | Another WordBreak enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ImageRepeat

```cangjie
public enum ImageRepeat <: Equatable<ImageRepeat> {
    | NoRepeat
    | X
    | Y
    | XY
    | ...
}
```

**Description:** Image repetition mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageRepeat](#enum-imagerepeat)>

### NoRepeat

```cangjie
NoRepeat
```

**Description:** Do not repeat the image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### X

```cangjie
X
```

**Description:** Repeat the image only on the horizontal axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Y

```cangjie
Y
```

**Description:** Repeat the image only on the vertical axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### XY

```cangjie
XY
```

**Description:** Repeat the image on both axes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageRepeat)

```cangjie
public operator func ==(other: ImageRepeat): Bool
```

**Description:** Determines whether two ImageRepeat enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageRepeat](#enum-imagerepeat) | Yes | - | Another ImageRepeat enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ImageRepeat)

```cangjie
public operator func !=(other: ImageRepeat): Bool
```

**Description:** Determines whether two ImageRepeat enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageRepeat](#enum-imagerepeat) | Yes | - | Another ImageRepeat enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum ImageSize

```cangjie
public enum ImageSize <: Equatable<ImageSize> {
    | Contain
    | Cover
    | Auto
    | ...
}
```

**Function:** Image display size settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageSize](#enum-imagesize)>

### Contain

```cangjie
Contain
```

**Function:** Scales the image while maintaining its aspect ratio to ensure it is fully displayed within the boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Cover

```cangjie
Cover
```

**Function:** Scales the image while maintaining its aspect ratio to ensure both sides are equal to or larger than the display boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Function:** Uses the default configuration in the Flex container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageSize)

```cangjie
public operator func ==(other: ImageSize): Bool
```

**Function:** Determines whether two ImageSize enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSize](#enum-imagesize) | Yes | - | Another ImageSize enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ImageSize)

```cangjie
public operator func !=(other: ImageSize): Bool
```

**Function:** Determines whether two ImageSize enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSize](#enum-imagesize) | Yes | - | Another ImageSize enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ShadowStyle

```cangjie
public enum ShadowStyle <: Equatable<ShadowStyle> {
    | OuterDefaultXS
    | OuterDefaultSM
    | OuterDefaultMD
    | OuterDefaultLG
    | OuterFloatingSM
    | OuterFloatingMD
    | ...
}
```

**Function:** Shadow style settings.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ShadowStyle](#enum-shadowstyle)>

### OuterDefaultXS

```cangjie
OuterDefaultXS
```

**Function:** Extra small shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OuterDefaultSM

```cangjie
OuterDefaultSM
```

**Function:** Small shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OuterDefaultMD

```cangjie
OuterDefaultMD
```

**Function:** Medium shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OuterDefaultLG

```cangjie
OuterDefaultLG
```

**Function:** Large shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OuterFloatingSM

```cangjie
OuterFloatingSM
```

**Function:** Small floating shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OuterFloatingMD

```cangjie
OuterFloatingMD
```

**Function:** Medium floating shadow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ShadowStyle)

```cangjie
public operator func ==(other: ShadowStyle): Bool
```

**Function:** Determines whether two ShadowStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ShadowStyle](#enum-shadowstyle) | Yes | - | Another ShadowStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ShadowStyle)

```cangjie
public operator func !=(other: ShadowStyle): Bool
```

**Function:** Determines whether two ShadowStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ShadowStyle](#enum-shadowstyle) | Yes | - | Another ShadowStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum TextCase

```cangjie
public enum TextCase <: Equatable<TextCase> {
    | Normal
    | LowerCase
    | UpperCase
    | ...
}
```

**Function:** Text case formatting.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextCase](#enum-textcase)>

### Normal

```cangjie
Normal
```

**Function:** Preserves the original text case.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LowerCase

```cangjie
LowerCase
```

**Function:** Converts text to all lowercase.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### UpperCase

```cangjie
UpperCase
```

**Function:** Converts text to all uppercase.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextCase)

```cangjie
public operator func ==(other: TextCase): Bool
```

**Function:** Determines whether two TextCase enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextCase](#enum-textcase) | Yes | - | Another TextCase enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextCase)

```cangjie
public operator func !=(other: TextCase): Bool
```

**Function:** Determines whether two TextCase enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextCase](#enum-textcase) | Yes | - | Another TextCase enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum BorderStyle

```cangjie
public enum BorderStyle <: Equatable<BorderStyle> {
    | Solid
    | Dashed
    | Dotted
    | ...
}
```

**Function:** Border style settings, used to describe the style of all four borders of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BorderStyle](#enum-borderstyle)>

### Solid

```cangjie
Solid
```

**Function:** Displays as a solid line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dashed

```cangjie
Dashed
```

**Function:** Displays as a series of short square dashes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dotted

```cangjie
Dotted
```

**Function:** Displays as a series of dots, with the dot radius being half of the borderWidth.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BorderStyle)

```cangjie
public operator func ==(other: BorderStyle): Bool
```

**Function:** Determines whether two BorderStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BorderStyle](#enum-borderstyle) | Yes | - | Another BorderStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(BorderStyle)

```cangjie
public operator func !=(other: BorderStyle): Bool
```

**Function:** Determines whether two BorderStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BorderStyle](#enum-borderstyle) | Yes | - | Another BorderStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum ImageFit

```cangjie
public enum ImageFit <: Equatable<ImageFit> {
    | Fill
    | Contain
    | Cover
    | Auto
    | None
    | ScaleDown
    | ...
}
```

**Description:** Image display adaptation modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageFit](#enum-imagefit)>

### Fill

```cangjie
Fill
```

**Description:** Scales the image without maintaining aspect ratio, stretching it to fill the entire display boundary.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Contain

```cangjie
Contain
```

**Description:** Scales the image while maintaining aspect ratio, ensuring the entire image is displayed within the boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Cover

```cangjie
Cover
```

**Description:** Scales the image while maintaining aspect ratio, ensuring both dimensions are equal to or larger than the display boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Description:** Default value. Preserves the original image proportions without scaling.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Description:** Displays the image at its original dimensions without any scaling.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ScaleDown

```cangjie
ScaleDown
```

**Description:** Scales down the image proportionally but never scales up, maintaining aspect ratio.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageFit)

```cangjie
public operator func ==(other: ImageFit): Bool
```

**Description:** Determines whether two ImageFit enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFit](#enum-imagefit) | Yes | - | The other ImageFit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are equal, otherwise false. |

### operator func !=(ImageFit)

```cangjie
public operator func !=(other: ImageFit): Bool
```

**Description:** Determines whether two ImageFit enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageFit](#enum-imagefit) | Yes | - | The other ImageFit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are not equal, otherwise false. |

## enum Direction

```cangjie
public enum Direction <: Equatable<Direction> {
    | Ltr
    | Rtl
    | Auto
    | ...
}
```

**Description:** Element layout direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Direction](#enum-direction)>

### Ltr

```cangjie
Ltr
```

**Description:** Elements are laid out from left to right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Rtl

```cangjie
Rtl
```

**Description:** Elements are laid out from right to left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Description:** Uses the default layout direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Direction)

```cangjie
public operator func ==(other: Direction): Bool
```

**Description:** Determines whether two Direction enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Direction](#enum-direction) | Yes | - | The other Direction enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are equal, otherwise false. |

### operator func !=(Direction)

```cangjie
public operator func !=(other: Direction): Bool
```

**Description:** Determines whether two Direction enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Direction](#enum-direction) | Yes | - | The other Direction enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are not equal, otherwise false. |

## enum ScrollDirection

```cangjie
public enum ScrollDirection <: Equatable<ScrollDirection> {
    | Vertical
    | Horizontal
    | ...
}
```

**Description:** Scroll direction enumeration.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ScrollDirection](#enum-scrolldirection)>

### Vertical

```cangjie
Vertical
```

**Description:** Supports vertical scrolling only.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Horizontal

```cangjie
Horizontal
```

**Description:** Supports horizontal scrolling only.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ScrollDirection)

```cangjie
public operator func ==(other: ScrollDirection): Bool
```

**Description:** Determines whether two ScrollDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollDirection](#enum-scrolldirection) | Yes | - | The other ScrollDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are equal, otherwise false. |

### operator func !=(ScrollDirection)

```cangjie
public operator func !=(other: ScrollDirection): Bool
```

**Description:** Determines whether two ScrollDirection enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollDirection](#enum-scrolldirection) | Yes | - | The other ScrollDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are not equal, otherwise false. |

## enum ScrollBarDirection

```cangjie
public enum ScrollBarDirection <: Equatable<ScrollBarDirection> {
    | Vertical
    | Horizontal
    | ...
}
```

**Description:** Sets the scrollbar direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ScrollBarDirection](#enum-scrollbardirection)>

### Vertical

```cangjie
Vertical
```

**Description:** Sets the scrollbar direction to vertical.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Horizontal

```cangjie
Horizontal
```

**Description:** Sets the scrollbar direction to horizontal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ScrollBarDirection)

```cangjie
public operator func ==(other: ScrollBarDirection): Bool
```

**Description:** Determines whether two ScrollBarDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollBarDirection](#enum-scrollbardirection) | Yes | - | The other ScrollBarDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are equal, otherwise false. |

### operator func !=(ScrollBarDirection)

```cangjie
public operator func !=(other: ScrollBarDirection): Bool
```

**Description:** Determines whether two ScrollBarDirection enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollBarDirection](#enum-scrollbardirection) | Yes | - | The other ScrollBarDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enums are not equal, otherwise false. |## enum SliderChangeMode

```cangjie
public enum SliderChangeMode <: Equatable<SliderChangeMode> {
    | Begin
    | Moving
    | End
    | Click
    | ...
}
```

**Function:** State values triggered when the Slider is dragged or clicked.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SliderChangeMode](#enum-sliderchangemode)>

### Begin

```cangjie
Begin
```

**Function:** Mouse contact or pressing down on the slider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Moving

```cangjie
Moving
```

**Function:** During the process of dragging the slider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Gesture/mouse leaves the slider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Click

```cangjie
Click
```

**Function:** Clicking the slider track to move the slider position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SliderChangeMode)

```cangjie
public operator func ==(other: SliderChangeMode): Bool
```

**Function:** Determines whether two SliderChangeMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SliderChangeMode](#enum-sliderchangemode) | Yes | - | Another SliderChangeMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(SliderChangeMode)

```cangjie
public operator func !=(other: SliderChangeMode): Bool
```

**Function:** Determines whether two SliderChangeMode enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SliderChangeMode](#enum-sliderchangemode) | Yes | - | Another SliderChangeMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum IndexerAlign

```cangjie
public enum IndexerAlign <: Equatable<IndexerAlign> {
    | Left
    | Right
    | ...
}
```

**Function:** Indexer alignment mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[IndexerAlign](#enum-indexeralign)>

### Left

```cangjie
Left
```

**Function:** Left alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** Right alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(IndexerAlign)

```cangjie
public operator func ==(other: IndexerAlign): Bool
```

**Function:** Determines whether two IndexerAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [IndexerAlign](#enum-indexeralign) | Yes | - | Another IndexerAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(IndexerAlign)

```cangjie
public operator func !=(other: IndexerAlign): Bool
```

**Function:** Determines whether two IndexerAlign enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [IndexerAlign](#enum-indexeralign) | Yes | - | Another IndexerAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum InputType

```cangjie
public enum InputType <: Equatable<InputType> {
    | Normal
    | Number
    | Email
    | Password
    | PhoneNumber
    | ...
}
```

**Function:** Represents the type of input box.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[InputType](#enum-inputtype)>

### Normal

```cangjie
Normal
```

**Function:** Represents basic input mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Number

```cangjie
Number
```

**Function:** Represents numeric-only input mode, allowing only characters that represent numbers.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Email

```cangjie
Email
```

**Function:** Email address input mode, allowing only characters supported by standard email formats.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Password

```cangjie
Password
```

**Function:** Represents password input mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PhoneNumber

```cangjie
PhoneNumber
```

**Function:** Represents phone number input mode. Supports input of digits, spaces, +, -, *, #, (, ), with no length limit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(InputType)

```cangjie
public operator func ==(other: InputType): Bool
```

**Function:** Determines whether two InputType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [InputType](#enum-inputtype) | Yes | - | Another InputType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(InputType)

```cangjie
public operator func !=(other: InputType): Bool
```

**Function:** Determines whether two InputType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [InputType](#enum-inputtype) | Yes | - | Another InputType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum EnterKeyType

```cangjie
public enum EnterKeyType <: Equatable<EnterKeyType> {
    | Go
    | Search
    | Send
    | Next
    | Done
    | Previous
    | NewLine
    | ...
}
```

**Function:** Represents the type of keyboard action button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[EnterKeyType](#enum-enterkeytype)>

### Go

```cangjie
Go
```

**Function:** Displays as a "Go" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Search

```cangjie
Search
```

**Function:** Displays as a "Search" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Send

```cangjie
Send
```

**Function:** c

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Next

```cangjie
Next
```

**Function:** Displays as a "Next" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Done

```cangjie
Done
```

**Function:** Displays as a "Done" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Previous

```cangjie
Previous
```

**Function:** Displays as a "Previous" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NewLine

```cangjie
NewLine
```

**Function:** Displays as a "New Line" style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(EnterKeyType)

```cangjie
public operator func ==(other: EnterKeyType): Bool
```

**Function:** Determines whether two EnterKeyType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [EnterKeyType](#enum-enterkeytype) | Yes | - | Another EnterKeyType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(EnterKeyType)

```cangjie
public operator func !=(other: EnterKeyType): Bool
```

**Function:** Determines whether two EnterKeyType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [EnterKeyType](#enum-enterkeytype) | Yes | - | Another EnterKeyType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum FlexDirection

```cangjie
public enum FlexDirection <: Equatable<FlexDirection> {
    | Row
    | Column
    | RowReverse
    | ColumnReverse
    | ...
}
```

**Function:** Flex container direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FlexDirection](#enum-flexdirection)>

### Row

```cangjie
Row
```

**Function:** Sets the main axis to follow the row direction as the layout mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Column

```cangjie
Column
```

**Function:** Sets the main axis to follow the column direction as the layout mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RowReverse

```cangjie
RowReverse
```

**Function:** Layout in the opposite direction of Row.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ColumnReverse

```cangjie
ColumnReverse
```

**Function:** Layout in the opposite direction of Column.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FlexDirection)

```cangjie
public operator func ==(other: FlexDirection): Bool
```

**Function:** Determines whether two FlexDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexDirection](#enum-flexdirection)|Yes|-|Another FlexDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(FlexDirection)

```cangjie
public operator func !=(other: FlexDirection): Bool
```

**Function:** Determines whether two FlexDirection enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexDirection](#enum-flexdirection)|Yes|-|Another FlexDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum FlexWrap

```cangjie
public enum FlexWrap <: Equatable<FlexWrap> {
    | NoWrap
    | Wrap
    | WrapReverse
    | ...
}
```

**Function:** Description of FlexWrap enum.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FlexWrap](#enum-flexwrap)>

### NoWrap

```cangjie
NoWrap
```

**Function:** Single-row/column layout for Flex container elements, with child elements constrained within the container as much as possible. When child elements have minimum size constraints, the Flex container will not forcibly compress them.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Wrap

```cangjie
Wrap
```

**Function:** Multi-row/column layout for Flex container elements, allowing child elements to exceed the container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### WrapReverse

```cangjie
WrapReverse
```

**Function:** Layout in the opposite direction of Wrap.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FlexWrap)

```cangjie
public operator func ==(other: FlexWrap): Bool
```

**Function:** Determines whether two FlexWrap enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexWrap](#enum-flexwrap)|Yes|-|Another FlexWrap enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(FlexWrap)

```cangjie
public operator func !=(other: FlexWrap): Bool
```

**Function:** Determines whether two FlexWrap enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexWrap](#enum-flexwrap)|Yes|-|Another FlexWrap enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum FlexAlign

```cangjie
public enum FlexAlign <: Equatable<FlexAlign> {
    | Start
    | Center
    | End
    | SpaceBetween
    | SpaceAround
    | SpaceEvenly
    | ...
}
```

**Function:** Flex container alignment method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FlexAlign](#enum-flexalign)>

### Start

```cangjie
Start
```

**Function:** Aligns elements to the start of the main axis. The first element aligns with the start of the row, and other elements align with the previous one.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Aligns elements to the center of the main axis. The distance from the first element to the start of the row equals the distance from the last element to the end of the row.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Aligns elements to the end of the main axis. The last element aligns with the end of the row, and other elements align with the next one.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpaceBetween

```cangjie
SpaceBetween
```

**Function:** Evenly distributes flex elements along the main axis, with equal spacing between adjacent elements. The first element aligns with the start of the row, and the last element aligns with the end of the row.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpaceAround

```cangjie
SpaceAround
```

**Function:** Evenly distributes flex elements along the main axis, with equal spacing between adjacent elements. The distance from the first element to the start of the row and from the last element to the end of the row is half the spacing between adjacent elements.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SpaceEvenly

```cangjie
SpaceEvenly
```

**Function:** Evenly distributes flex elements along the main axis, with equal spacing between adjacent elements. The distance from the first element to the start of the row and from the last element to the end of the row equals the spacing between adjacent elements.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FlexAlign)

```cangjie
public operator func ==(other: FlexAlign): Bool
```

**Function:** Determines whether two FlexAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexAlign](#enum-flexalign)|Yes|-|Another FlexAlign enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(FlexAlign)

```cangjie
public operator func !=(other: FlexAlign): Bool
```

**Function:** Determines whether two FlexAlign enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[FlexAlign](#enum-flexalign)|Yes|-|Another FlexAlign enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ItemAlign

```cangjie
public enum ItemAlign <: Equatable<ItemAlign> {
    | Auto
    | Start
    | Center
    | End
    | Stretch
    | Baseline
    | ...
}
```

**Function:** Element alignment method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ItemAlign](#enum-itemalign)>

### Auto

```cangjie
Auto
```

**Function:** Uses the default configuration in the Flex container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** Aligns elements to the start of the cross axis in the Flex container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Centers ListItem along the cross axis in the List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Aligns ListItem to the end of the cross axis in the List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Stretch

```cangjie
Stretch
```

**Function:** Stretches elements to fill the cross axis in the Flex container. When the container is Flex and Wrap is set to FlexWrap.Wrap or FlexWrap.WrapReverse, elements stretch to match the longest element in the current row/column. Otherwise, elements stretch to the container size regardless of their set dimensions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Baseline

```cangjie
Baseline
```

**Function:** Aligns the bottom edge of an image with the text baseline.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ItemAlign)

```cangjie
public operator func ==(other: ItemAlign): Bool
```

**Function:** Determines whether two ItemAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ItemAlign](#enum-itemalign)|Yes|-|Another ItemAlign enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ItemAlign)

```cangjie
public operator func !=(other: ItemAlign): Bool
```

**Function:** Determines whether two ItemAlign enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ItemAlign](#enum-itemalign)|Yes|-|Another ItemAlign enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum ToggleType

```cangjie
public enum ToggleType <: Equatable<ToggleType> {
    | Checkbox
    | Switch
    | Button
    | ...
}
```

**Function:** Toggle component types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ToggleType](#enum-toggletype)>

### Checkbox

```cangjie
Checkbox
```

**Function:** Provides radio button style.
The default Checkbox style is circular.
Default margin values for common properties: top 14.px, right 14.px, bottom 14.px, left 14.px.
Default dimensions: width 20.vp, height 20.vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Switch

```cangjie
Switch
```

**Function:** Provides toggle switch style.
Default margin values for common properties: top 6.px, right 14.px, bottom 6.px, left 14.px.
Default dimensions: width 36.vp, height 20.vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Button

```cangjie
Button
```

**Function:** Provides state button style. If child components have text settings, the corresponding text content will be displayed inside the button.
Initial dimensions: height 28.vp, width has no initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ToggleType)

```cangjie
public operator func ==(other: ToggleType): Bool
```

**Function:** Determines whether two ToggleType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ToggleType](#enum-toggletype) | Yes | - | Another ToggleType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ToggleType)

```cangjie
public operator func !=(other: ToggleType): Bool
```

**Function:** Determines whether two ToggleType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ToggleType](#enum-toggletype) | Yes | - | Another ToggleType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum FontStyle

```cangjie
public enum FontStyle <: Equatable<FontStyle> {
    | Normal
    | Italic
    | ...
}
```

**Function:** Font styles.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FontStyle](#enum-fontstyle)>

### Normal

```cangjie
Normal
```

**Function:** Standard font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Italic

```cangjie
Italic
```

**Function:** Italic font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FontStyle)

```cangjie
public operator func ==(other: FontStyle): Bool
```

**Function:** Determines whether two FontStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FontStyle](#enum-fontstyle) | Yes | - | Another FontStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(FontStyle)

```cangjie
public operator func !=(other: FontStyle): Bool
```

**Function:** Determines whether two FontStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FontStyle](#enum-fontstyle) | Yes | - | Another FontStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum Alignment

```cangjie
public enum Alignment <: Equatable<Alignment> {
    | TopStart
    | Top
    | TopEnd
    | Start
    | Center
    | End
    | BottomStart
    | Bottom
    | BottomEnd
    | ...
}
```

**Function:** Alignment methods.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Alignment](#enum-alignment)>

### TopStart

```cangjie
TopStart
```

**Function:** Top start alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Top

```cangjie
Top
```

**Function:** Top horizontal center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopEnd

```cangjie
TopEnd
```

**Function:** Top end alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** Start alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Horizontal and vertical center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** End alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomStart

```cangjie
BottomStart
```

**Function:** Bottom start alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Bottom horizontal center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomEnd

```cangjie
BottomEnd
```

**Function:** Bottom end alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Alignment)

```cangjie
public operator func ==(other: Alignment): Bool
```

**Function:** Determines whether two Alignment enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Alignment](#enum-alignment) | Yes | - | Another Alignment enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(Alignment)

```cangjie
public operator func !=(other: Alignment): Bool
```

**Function:** Determines whether two Alignment enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [Alignment](#enum-alignment) | Yes | - | Another Alignment enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum HorizontalAlign

```cangjie
public enum HorizontalAlign <: Equatable<HorizontalAlign> {
    | Start
    | Center
    | End
    | ...
}
```

**Function:** Horizontal alignment methods.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[HorizontalAlign](#enum-horizontalalign)>

### Start

```cangjie
Start
```

**Function:** Aligns to the start according to language direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Center alignment. Uses default alignment mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Aligns to the end according to language direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(HorizontalAlign)

```cangjie
public operator func ==(other: HorizontalAlign): Bool
```

**Function:** Determines whether two HorizontalAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HorizontalAlign](#enum-horizontalalign) | Yes | - | Another HorizontalAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(HorizontalAlign)

```cangjie
public operator func !=(other: HorizontalAlign): Bool
```

**Function:** Determines whether two HorizontalAlign enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HorizontalAlign](#enum-horizontalalign) | Yes | - | Another HorizontalAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum VerticalAlign

```cangjie
public enum VerticalAlign <: Equatable<VerticalAlign> {
    | Top
    | Center
    | Bottom
    | ...
}
```

**Function:** Vertical alignment method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[VerticalAlign](#enum-verticalalign)>

### Top

```cangjie
Top
```

**Function:** Top alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Center alignment (default alignment method).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Bottom alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(VerticalAlign)

```cangjie
public operator func ==(other: VerticalAlign): Bool
```

**Function:** Determines whether two VerticalAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [VerticalAlign](#enum-verticalalign) | Yes | - | Another VerticalAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(VerticalAlign)

```cangjie
public operator func !=(other: VerticalAlign): Bool
```

**Function:** Determines whether two VerticalAlign enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [VerticalAlign](#enum-verticalalign) | Yes | - | Another VerticalAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum FontWeight

```cangjie
public enum FontWeight <: Equatable<FontWeight> {
    | Normal
    | Bold
    | Bolder
    | Lighter
    | Medium
    | Regular
    | W100
    | W200
    | W300
    | W400
    | W500
    | W600
    | W700
    | W800
    | W900
    | ...
}
```

**Function:** Sets the font weight of text. Setting too large may result in truncation with different fonts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FontWeight](#enum-fontweight)>

### Normal

```cangjie
Normal
```

**Function:** Normal font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bold

```cangjie
Bold
```

**Function:** Bold font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bolder

```cangjie
Bolder
```

**Function:** Very bold font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Lighter

```cangjie
Lighter
```

**Function:** Light font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Medium

```cangjie
Medium
```

**Function:** Medium font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Regular

```cangjie
Regular
```

**Function:** Slightly bold font weight.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W100

```cangjie
W100
```

**Function:** 100 (lightest).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W200

```cangjie
W200
```

**Function:** 200.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W300

```cangjie
W300
```

**Function:** 300.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W400

```cangjie
W400
```

**Function:** 400 (normal).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W500

```cangjie
W500
```

**Function:** 500.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W600

```cangjie
W600
```

**Function:** 600.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W700

```cangjie
W700
```

**Function:** 700.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W800

```cangjie
W800
```

**Function:** 800.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### W900

```cangjie
W900
```

**Function:** 900 (boldest).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FontWeight)

```cangjie
public operator func ==(other: FontWeight): Bool
```

**Function:** Determines whether two FontWeight enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FontWeight](#enum-fontweight) | Yes | - | Another FontWeight enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(FontWeight)

```cangjie
public operator func !=(other: FontWeight): Bool
```

**Function:** Determines whether two FontWeight enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FontWeight](#enum-fontweight) | Yes | - | Another FontWeight enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ListItemAlign

```cangjie
public enum ListItemAlign <: Equatable<ListItemAlign> {
    | Start
    | Center
    | End
    | ...
}
```

**Function:** Alignment method of ListItem along the cross axis in a List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ListItemAlign](#enum-listitemalign)>

### Start

```cangjie
Start
```

**Function:** Aligns ListItem to the start of the cross axis in a List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Aligns ListItem to the center of the cross axis in a List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Aligns ListItem to the end of the cross axis in a List.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ListItemAlign)

```cangjie
public operator func ==(other: ListItemAlign): Bool
```

**Function:** Determines whether two ListItemAlign enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ListItemAlign](#enum-listitemalign) | Yes | - | Another ListItemAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ListItemAlign)

```cangjie
public operator func !=(other: ListItemAlign): Bool
```

**Function:** Determines whether two ListItemAlign enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ListItemAlign](#enum-listitemalign) | Yes | - | Another ListItemAlign enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum StickyStyle

```cangjie
public enum StickyStyle <: Equatable<StickyStyle> {
    | None
    | Header
    | Footer
    | ...
}
```

**Function:** Sets whether the header and footer in ListItemGroup should stick to the top or bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[StickyStyle](#enum-stickystyle)>

### None

```cangjie
None
```

**Function:** Sets the ListItemGroup's header not to stick to the top and footer not to stick to the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Header

```cangjie
Header
```

**Function:** Sets the ListItemGroup's header to stick to the top.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Footer

```cangjie
Footer
```

**Function:** Sets the ListItemGroup's footer to stick to the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(StickyStyle)

```cangjie
public operator func ==(other: StickyStyle): Bool
```

**Function:** Determines whether two StickyStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [StickyStyle](#enum-stickystyle) | Yes | - | Another StickyStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(StickyStyle)

```cangjie
public operator func !=(other: StickyStyle): Bool
```

**Function:** Determines whether two StickyStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [StickyStyle](#enum-stickystyle) | Yes | - | Another StickyStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum RichEditorSpanType

```cangjie
public enum RichEditorSpanType <: Equatable<RichEditorSpanType> {
    | Text
    | Image
    | Mixed
    | ...
}
```

**Function:** Represents the type information of a Span.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[RichEditorSpanType](#enum-richeditorspantype)>

### Text

```cangjie
Text
```

**Function:** Indicates that the Span is of text type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Image

```cangjie
Image
```

**Function:** Indicates that the Span is of image type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Mixed

```cangjie
Mixed
```

**Function:** Indicates that the Span is of mixed text and image type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(RichEditorSpanType)

```cangjie
public operator func ==(other: RichEditorSpanType): Bool
```

**Function:** Determines whether two RichEditorSpanType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RichEditorSpanType](#enum-richeditorspantype) | Yes | - | Another RichEditorSpanType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(RichEditorSpanType)

```cangjie
public operator func !=(other: RichEditorSpanType): Bool
```

**Function:** Determines whether two RichEditorSpanType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RichEditorSpanType](#enum-richeditorspantype) | Yes | - | Another RichEditorSpanType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ImageSpanAlignment

```cangjie
public enum ImageSpanAlignment <: Equatable<ImageSpanAlignment> {
    | Top
    | Center
    | Bottom
    | Baseline
    | ...
}
```

**Function:** The alignment of an image relative to the line height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ImageSpanAlignment](#enum-imagespanalignment)>

### Top

```cangjie
Top
```

**Function:** Aligns the top edge of the image with the top edge of the line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Aligns the center of the image with the center of the line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Aligns the bottom edge of the image with the bottom edge of the line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Baseline

```cangjie
Baseline
```

**Function:** Aligns the bottom edge of the image with the text baseline.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ImageSpanAlignment)

```cangjie
public operator func ==(other: ImageSpanAlignment): Bool
```

**Function:** Determines whether two ImageSpanAlignment enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSpanAlignment](#enum-imagespanalignment) | Yes | - | Another ImageSpanAlignment enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ImageSpanAlignment)

```cangjie
public operator func !=(other: ImageSpanAlignment): Bool
```

**Function:** Determines whether two ImageSpanAlignment enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ImageSpanAlignment](#enum-imagespanalignment) | Yes | - | Another ImageSpanAlignment enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum RichEditorDeleteDirection

```cangjie
public enum RichEditorDeleteDirection <: Equatable<RichEditorDeleteDirection> {
    | Backward
    | Forward
    | ...
}
```

**Function:** Represents the direction of a delete operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[RichEditorDeleteDirection](#enum-richeditordeletedirection)>

### Backward

```cangjie
Backward
```

**Function:** Represents backward deletion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Forward

```cangjie
Forward
```

**Function:** Represents forward deletion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(RichEditorDeleteDirection)

```cangjie
public operator func ==(other: RichEditorDeleteDirection): Bool
```

**Function:** Determines whether two RichEditorDeleteDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RichEditorDeleteDirection](#enum-richeditordeletedirection) | Yes | - | Another RichEditorDeleteDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(RichEditorDeleteDirection)

```cangjie
public operator func !=(other: RichEditorDeleteDirection): Bool
```

**Function:** Determines whether two RichEditorDeleteDirection enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RichEditorDeleteDirection](#enum-richeditordeletedirection) | Yes | - | Another RichEditorDeleteDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum MixedMode

```cangjie
public enum MixedMode <: Equatable<MixedMode> {
    | All
    | Compatible
    | None
    | ...
}
```

**Function:** Sets the security loading mode for mixed content.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parent Type:**

- Equatable\<[MixedMode](#enum-mixedmode)>

### All

```cangjie
All
```

**Function:** Permissive mode: Allows loading both HTTP and HTTPS mixed content. All insecure content can be loaded.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Compatible

```cangjie
Compatible
```

**Function:** Compatibility mode: Mixed content compatibility mode where some insecure content may be loaded.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### None

```cangjie
None
```

**Function:** Strict mode: Disallows loading HTTP and HTTPS mixed content. Secure origins are not allowed to load content from insecure origins.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### operator func ==(MixedMode)

```cangjie
public operator func ==(other: MixedMode): Bool
```

**Function:** Determines whether two MixedMode enums are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MixedMode](#enum-mixedmode)|Yes|-|The other MixedMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(MixedMode)

```cangjie
public operator func !=(other: MixedMode): Bool
```

**Function:** Determines whether two MixedMode enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MixedMode](#enum-mixedmode)|Yes|-|The other MixedMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum PlayMode

```cangjie
public enum PlayMode <: Equatable<PlayMode> {
    | Normal
    | Reverse
    | Alternate
    | AlternateReverse
    | ...
}
```

**Function:** Sets the animation playback direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[PlayMode](#enum-playmode)>

### Normal

```cangjie
Normal
```

**Function:** Animation plays forward.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Reverse

```cangjie
Reverse
```

**Function:** Animation plays in reverse.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Alternate

```cangjie
Alternate
```

**Function:** Animation plays forward on odd iterations (1, 3, 7...) and in reverse on even iterations (2, 4, 6...).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### AlternateReverse

```cangjie
AlternateReverse
```

**Function:** Animation plays in reverse on odd iterations (1, 3, 7...) and forward on even iterations (2, 4, 6...).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(PlayMode)

```cangjie
public operator func ==(other: PlayMode): Bool
```

**Function:** Determines whether two PlayMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PlayMode](#enum-playmode)|Yes|-|The other PlayMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(PlayMode)

```cangjie
public operator func !=(other: PlayMode): Bool
```

**Function:** Determines whether two PlayMode enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PlayMode](#enum-playmode)|Yes|-|The other PlayMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum GradientDirection

```cangjie
public enum GradientDirection <: Equatable<GradientDirection> {
    | Left
    | Top
    | Right
    | Bottom
    | LeftTop
    | LeftBottom
    | RightTop
    | RightBottom
    | None
    | ...
}
```

**Function:** Gradient direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[GradientDirection](#enum-gradientdirection)>

### Left

```cangjie
Left
```

**Function:** From right to left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Top

```cangjie
Top
```

**Function:** From bottom to top.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** From left to right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** From top to bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LeftTop

```cangjie
LeftTop
```

**Function:** Top-left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LeftBottom

```cangjie
LeftBottom
```

**Function:** Bottom-left.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RightTop

```cangjie
RightTop
```

**Function:** Top-right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RightBottom

```cangjie
RightBottom
```

**Function:** Bottom-right.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Function:** None.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(GradientDirection)

```cangjie
public operator func ==(other: GradientDirection): Bool
```

**Function:** Determines whether two GradientDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[GradientDirection](#enum-gradientdirection)|Yes|-|The other GradientDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(GradientDirection)

```cangjie
public operator func !=(other: GradientDirection): Bool
```

**Function:** Determines whether two GradientDirection enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[GradientDirection](#enum-gradientdirection)|Yes|-|The other GradientDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum RenderFit

```cangjie
public enum RenderFit <: Equatable<RenderFit> {
    | Center
    | Top
    | Bottom
    | Left
    | Right
    | TopLeft
    | TopRight
    | BottomLeft
    | BottomRight
    | ResizeFill
    | ResizeContain
    | ResizeContainTopLeft
    | ResizeContainBottomRight
    | ResizeCover
    | ResizeCoverTopLeft
    | ResizeCoverBottomRight
    | ...
}
```

**Function:** Component content fill style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[RenderFit](#enum-renderfit)>

### Center

```cangjie
Center
```

**Function:** Maintains the content size at the animation's end state and keeps the content center-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Top

```cangjie
Top
```

**Function:** Maintains the content size at the animation's end state and keeps the content top-center-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Maintains the content size at the animation's end state and keeps the content bottom-center-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Left

```cangjie
Left
```

**Function:** Maintains the content size at the animation's end state and keeps the content left-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Function:** Maintains the content size at the animation's end state and keeps the content right-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopLeft

```cangjie
TopLeft
```

**Function:** Maintains the content size at the animation's end state and keeps the content top-left-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopRight

```cangjie
TopRight
```

**Function:** Maintains the content size at the animation's end state and keeps the content top-right-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomLeft

```cangjie
BottomLeft
```

**Function:** Maintains the content size at the animation's end state and keeps the content bottom-left-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomRight

```cangjie
BottomRight
```

**Function:** Maintains the content size at the animation's end state and keeps the content bottom-right-aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeFill

```cangjie
ResizeFill
```

**Function:** Ignores the aspect ratio of the content at the animation's end state and scales the content to fit the component size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeContain

```cangjie
ResizeContain
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it fits entirely within the component, keeping it center-aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeContainTopLeft

```cangjie
ResizeContainTopLeft
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it fits entirely within the component. If there is extra width, the content is left-aligned; if there is extra height, the content is top-aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeContainBottomRight

```cangjie
ResizeContainBottomRight
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it fits entirely within the component. If there is extra width, the content is right-aligned; if there is extra height, the content is bottom-aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeCover

```cangjie
ResizeCover
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it covers the component entirely, keeping it center-aligned and showing the middle portion of the content.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeCoverTopLeft

```cangjie
ResizeCoverTopLeft
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it fits entirely within the component. If there is extra width, the content is left-aligned; if there is extra height, the content is top-aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ResizeCoverBottomRight

```cangjie
ResizeCoverBottomRight
```

**Function:** Scales the content at the animation's end state while maintaining its aspect ratio to ensure it fits entirely within the component. If there is extra width, the content is right-aligned; if there is extra height, the content is bottom-aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(RenderFit)

```cangjie
public operator func ==(other: RenderFit): Bool
```

**Function:** Determines whether two RenderFit enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[RenderFit](#enum-renderfit)|Yes|-|The other RenderFit enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(RenderFit)

```cangjie
public operator func !=(other: RenderFit): Bool
```

**Function:** Determines whether two RenderFit enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[RenderFit](#enum-renderfit)|Yes|-|The other RenderFit enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum DialogAlignment

```cangjie
public enum DialogAlignment <: Equatable<DialogAlignment> {
    | Top
    | Center
    | Bottom
    | Default
    | TopStart
    | TopEnd
    | CenterStart
    | CenterEnd
    | BottomStart
    | BottomEnd
    | ...
}
```

**Description:** Vertical alignment method for dialogs.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[DialogAlignment](#enum-dialogalignment)>

### Top

```cangjie
Top
```

**Description:** Align to the top vertically.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Description:** Center alignment vertically.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Description:** Horizontal center alignment at the bottom.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Default

```cangjie
Default
```

**Description:** Default alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopStart

```cangjie
TopStart
```

**Description:** Align to the top-left corner.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TopEnd

```cangjie
TopEnd
```

**Description:** Align to the top-right corner.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### CenterStart

```cangjie
CenterStart
```

**Description:** Left-center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### CenterEnd

```cangjie
CenterEnd
```

**Description:** Right-center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomStart

```cangjie
BottomStart
```

**Description:** Bottom starting edge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BottomEnd

```cangjie
BottomEnd
```

**Description:** Bottom ending edge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(DialogAlignment)

```cangjie
public operator func ==(other: DialogAlignment): Bool
```

**Description:** Determines whether two DialogAlignment enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[DialogAlignment](#enum-dialogalignment)|Yes|-|Another DialogAlignment enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(DialogAlignment)

```cangjie
public operator func !=(other: DialogAlignment): Bool
```

**Description:** Determines whether two DialogAlignment enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[DialogAlignment](#enum-dialogalignment)|Yes|-|Another DialogAlignment enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum BarrierDirection

```cangjie
public enum BarrierDirection <: Equatable<BarrierDirection> {
    | Left
    | Right
    | Top
    | Bottom
    | ...
}
```

**Description:** Defines the direction of barrier lines.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BarrierDirection](#enum-barrierdirection)>

### Left

```cangjie
Left
```

**Description:** The barrier is positioned at the leftmost of all its referencedId components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Right

```cangjie
Right
```

**Description:** The barrier is positioned at the rightmost of all its referencedId components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Top

```cangjie
Top
```

**Description:** The barrier is positioned at the topmost of all its referencedId components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Description:** The barrier will be positioned at the bottom of all referenced components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BarrierDirection)

```cangjie
public operator func ==(other: BarrierDirection): Bool
```

**Description:** Determines whether two BarrierDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarrierDirection](#enum-barrierdirection)|Yes|-|Another BarrierDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(BarrierDirection)

```cangjie
public operator func !=(other: BarrierDirection): Bool
```

**Description:** Determines whether two BarrierDirection enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BarrierDirection](#enum-barrierdirection)|Yes|-|Another BarrierDirection enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SafeAreaType

```cangjie
public enum SafeAreaType <: Equatable<SafeAreaType> {
    | System
    | Cutout
    | Keyboard
    | ...
}
```

**Description:** Enumeration type for extended safe areas.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SafeAreaType](#enum-safeareatype)>

### System

```cangjie
System
```

**Description:** Default system non-safe area, including status bar and navigation bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Cutout

```cangjie
Cutout
```

**Description:** Device's non-safe area, such as notch screens or punch-hole screens.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Keyboard

```cangjie
Keyboard
```

**Description:** Soft keyboard area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SafeAreaType)

```cangjie
public operator func ==(other: SafeAreaType): Bool
```

**Description:** Determines whether two SafeAreaType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SafeAreaType](#enum-safeareatype)|Yes|-|Another SafeAreaType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SafeAreaType)

```cangjie
public operator func !=(other: SafeAreaType): Bool
```

**Description:** Determines whether two SafeAreaType enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SafeAreaType](#enum-safeareatype)|Yes|-|Another SafeAreaType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SafeAreaEdge

```cangjie
public enum SafeAreaEdge <: Equatable<SafeAreaEdge> {
    | Top
    | Bottom
    | Start
    | End
    | ...
}
```

**Function:** Extends the direction of the safe area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SafeAreaEdge](#enum-safeareaedge)>

### Top

```cangjie
Top
```

**Function:** Top area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Bottom

```cangjie
Bottom
```

**Function:** Bottom area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** Front area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Rear area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SafeAreaEdge)

```cangjie
public operator func ==(other: SafeAreaEdge): Bool
```

**Function:** Determines whether two SafeAreaEdge enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SafeAreaEdge](#enum-safeareaedge)|Yes|-|Another SafeAreaEdge enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SafeAreaEdge)

```cangjie
public operator func !=(other: SafeAreaEdge): Bool
```

**Function:** Determines whether two SafeAreaEdge enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SafeAreaEdge](#enum-safeareaedge)|Yes|-|Another SafeAreaEdge enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ColoringStrategy

```cangjie
public enum ColoringStrategy <: Equatable<ColoringStrategy> {
    | Invert
    | ...
}
```

**Function:** Smart color selection enum type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ColoringStrategy](#enum-coloringstrategy)>

### Invert

```cangjie
Invert
```

**Function:** Sets the foreground color to the inverse of the control's background color. This enum can only be set in foregroundColor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ColoringStrategy)

```cangjie
public operator func ==(other: ColoringStrategy): Bool
```

**Function:** Determines whether two ColoringStrategy enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ColoringStrategy](#enum-coloringstrategy)|Yes|-|Another ColoringStrategy enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ColoringStrategy)

```cangjie
public operator func !=(other: ColoringStrategy): Bool
```

**Function:** Determines whether two ColoringStrategy enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ColoringStrategy](#enum-coloringstrategy)|Yes|-|Another ColoringStrategy enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum NestedScrollMode

```cangjie
public enum NestedScrollMode <: Equatable<NestedScrollMode> {
    | SelfOnly
    | SelfFirst
    | ParentFirst
    | Parallel
    | ...
}
```

**Function:** Nested scrolling options when a scrollable component scrolls to the end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[NestedScrollMode](#enum-nestedscrollmode)>

### SelfOnly

```cangjie
SelfOnly
```

**Function:** Only scrolls itself without interacting with the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SelfFirst

```cangjie
SelfFirst
```

**Function:** Scrolls itself first. After reaching its edge, the parent component scrolls. If the parent component has an edge effect, it triggers the edge effect; otherwise, the child component triggers the edge effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ParentFirst

```cangjie
ParentFirst
```

**Function:** The parent component scrolls first. After reaching its edge, the child component scrolls. If the child component has an edge effect, it triggers the edge effect; otherwise, the parent component triggers the edge effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Parallel

```cangjie
Parallel
```

**Function:** Both the child and parent components scroll simultaneously. After both reach their edges, if the child component has an edge effect, it triggers the edge effect; otherwise, the parent component triggers the edge effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(NestedScrollMode)

```cangjie
public operator func ==(other: NestedScrollMode): Bool
```

**Function:** Determines whether two NestedScrollMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NestedScrollMode](#enum-nestedscrollmode)|Yes|-|Another NestedScrollMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(NestedScrollMode)

```cangjie
public operator func !=(other: NestedScrollMode): Bool
```

**Function:** Determines whether two NestedScrollMode enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[NestedScrollMode](#enum-nestedscrollmode)|Yes|-|Another NestedScrollMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ThemeColorMode

```cangjie
public enum ThemeColorMode <: Equatable<ThemeColorMode> {
    | System
    | Light
    | Dark
    | ...
}
```

**Function:** Theme color mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ThemeColorMode](#enum-themecolormode)>

### System

```cangjie
System
```

**Function:** Follows the system's light/dark mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Light

```cangjie
Light
```

**Function:** Uses light mode exclusively.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dark

```cangjie
Dark
```

**Function:** Uses dark mode exclusively.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ThemeColorMode)

```cangjie
public operator func ==(other: ThemeColorMode): Bool
```

**Function:** Determines whether two ThemeColorMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ThemeColorMode](#enum-themecolormode)|Yes|-|Another ThemeColorMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ThemeColorMode)

```cangjie
public operator func !=(other: ThemeColorMode): Bool
```

**Function:** Determines whether two ThemeColorMode enums are not equal.

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ThemeColorMode](#enum-themecolormode)|Yes|-|Another ThemeColorMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|## enum AdaptiveColor

```cangjie
public enum AdaptiveColor <: Equatable<AdaptiveColor> {
    | Default
    | Average
    | ...
}
```

**Function:** Color sampling mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[AdaptiveColor](#enum-adaptivecolor)>

### Default

```cangjie
Default
```

**Function:** Disables color sampling blur. Uses the default color as the mask color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Average

```cangjie
Average
```

**Function:** Enables color sampling blur. Uses the average color of the sampled area as the mask color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(AdaptiveColor)

```cangjie
public operator func ==(other: AdaptiveColor): Bool
```

**Function:** Determines whether two AdaptiveColor enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AdaptiveColor](#enum-adaptivecolor) | Yes | - | Another AdaptiveColor enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(AdaptiveColor)

```cangjie
public operator func !=(other: AdaptiveColor): Bool
```

**Function:** Determines whether two AdaptiveColor enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AdaptiveColor](#enum-adaptivecolor) | Yes | - | Another AdaptiveColor enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ControlSize

```cangjie
public enum ControlSize <: Equatable<ControlSize> {
    | Small
    | Normal
    | ...
}
```

**Function:** Control size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ControlSize](#enum-controlsize)>

### Small

```cangjie
Small
```

**Function:** Small size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Normal

```cangjie
Normal
```

**Function:** Normal size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ControlSize)

```cangjie
public operator func ==(other: ControlSize): Bool
```

**Function:** Determines whether two ControlSize enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ControlSize](#enum-controlsize) | Yes | - | Another ControlSize enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ControlSize)

```cangjie
public operator func !=(other: ControlSize): Bool
```

**Function:** Determines whether two ControlSize enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ControlSize](#enum-controlsize) | Yes | - | Another ControlSize enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum OptionWidthMode

```cangjie
public enum OptionWidthMode <: Equatable<OptionWidthMode> {
    | FitContent
    | FitTrigger
    | ...
}
```

**Function:** Dropdown menu width setting.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[OptionWidthMode](#enum-optionwidthmode)>

### FitContent

```cangjie
FitContent
```

**Function:** When set, the dropdown menu width displays by default in 2-grid layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FitTrigger

```cangjie
FitTrigger
```

**Function:** Sets the dropdown menu to inherit the width of the dropdown button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(OptionWidthMode)

```cangjie
public operator func ==(other: OptionWidthMode): Bool
```

**Function:** Determines whether two OptionWidthMode enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [OptionWidthMode](#enum-optionwidthmode) | Yes | - | Another OptionWidthMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(OptionWidthMode)

```cangjie
public operator func !=(other: OptionWidthMode): Bool
```

**Function:** Determines whether two OptionWidthMode enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [OptionWidthMode](#enum-optionwidthmode) | Yes | - | Another OptionWidthMode enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ArrowPosition

```cangjie
public enum ArrowPosition <: Equatable<ArrowPosition> {
    | End
    | Start
    | ...
}
```

**Function:** Alignment between dropdown menu item text and arrow.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ArrowPosition](#enum-arrowposition)>

### End

```cangjie
End
```

**Function:** Text first, arrow follows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Start

```cangjie
Start
```

**Function:** Arrow first, text follows.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ArrowPosition)

```cangjie
public operator func ==(other: ArrowPosition): Bool
```

**Function:** Determines whether two ArrowPosition enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ArrowPosition](#enum-arrowposition) | Yes | - | Another ArrowPosition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ArrowPosition)

```cangjie
public operator func !=(other: ArrowPosition): Bool
```

**Function:** Determines whether two ArrowPosition enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ArrowPosition](#enum-arrowposition) | Yes | - | Another ArrowPosition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum MenuAlignType

```cangjie
public enum MenuAlignType <: Equatable<MenuAlignType> {
    | Start
    | Center
    | End
    | ...
}
```

**Function:** Menu alignment type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[MenuAlignType](#enum-menualigntype)>

### Start

```cangjie
Start
```

**Function:** Aligns to the start according to language direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Aligns to the end according to language direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(MenuAlignType)

```cangjie
public operator func ==(other: MenuAlignType): Bool
```

**Function:** Determines whether two MenuAlignType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MenuAlignType](#enum-menualigntype) | Yes | - | Another MenuAlignType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(MenuAlignType)

```cangjie
public operator func !=(other: MenuAlignType): Bool
```

**Function:** Determines whether two MenuAlignType enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MenuAlignType](#enum-menualigntype) | Yes | - | Another MenuAlignType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |```markdown
## enum WebDarkMode

```cangjie
public enum WebDarkMode <: Equatable<WebDarkMode> {
    | Off
    | On
    | Auto
    | ...
}
```

**Description:** Web dark mode, disabled by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parent Type:**

- Equatable\<[WebDarkMode](#enum-webdarkmode)>

### Off

```cangjie
Off
```

**Description:** Web dark mode is disabled.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### On

```cangjie
On
```

**Description:** Web dark mode is enabled.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Auto

```cangjie
Auto
```

**Description:** Web dark mode follows system settings.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### operator func ==(WebDarkMode)

```cangjie
public operator func ==(other: WebDarkMode): Bool
```

**Description:** Determines whether two WebDarkMode enums are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[WebDarkMode](#enum-webdarkmode)|Yes|-|Another WebDarkMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(WebDarkMode)

```cangjie
public operator func !=(other: WebDarkMode): Bool
```

**Description:** Determines whether two WebDarkMode enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[WebDarkMode](#enum-webdarkmode)|Yes|-|Another WebDarkMode enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum SourceTool

```cangjie
public enum SourceTool <: Equatable<SourceTool> {
    | Unknown
    | Finger
    | Pen
    | Mouse
    | Touchpad
    | Joystick
    | ...
}
```

**Description:** Event input source.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[SourceTool](#enum-sourcetool)>

### Unknown

```cangjie
Unknown
```

**Description:** Unknown input source.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Finger

```cangjie
Finger
```

**Description:** Finger input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Pen

```cangjie
Pen
```

**Description:** Stylus input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Mouse

```cangjie
Mouse
```

**Description:** Mouse input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Touchpad

```cangjie
Touchpad
```

**Description:** Touchpad input. Single-finger input on touchpad is treated as mouse input operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Joystick

```cangjie
Joystick
```

**Description:** Joystick input.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(SourceTool)

```cangjie
public operator func ==(other: SourceTool): Bool
```

**Description:** Determines whether two SourceTool enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SourceTool](#enum-sourcetool)|Yes|-|Another SourceTool enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(SourceTool)

```cangjie
public operator func !=(other: SourceTool): Bool
```

**Description:** Determines whether two SourceTool enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SourceTool](#enum-sourcetool)|Yes|-|Another SourceTool enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum Repetition

```cangjie
public enum Repetition <: Equatable<Repetition> {
    | Repeat
    | RepeatX
    | RepeatY
    | NoRepeat
    | Clamp
    | Mirror
    | ...
}
```

**Description:** Sets the image repetition method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[Repetition](#enum-repetition)>

### Repeat

```cangjie
Repeat
```

**Description:** Repeats the image along both x-axis and y-axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RepeatX

```cangjie
RepeatX
```

**Description:** Repeats the image along the x-axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RepeatY

```cangjie
RepeatY
```

**Description:** Repeats the image along the y-axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NoRepeat

```cangjie
NoRepeat
```

**Description:** Does not repeat the image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Clamp

```cangjie
Clamp
```

**Description:** Uses edge colors for drawing when exceeding original boundaries.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Mirror

```cangjie
Mirror
```

**Description:** Repeats and flips the image along both x-axis and y-axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(Repetition)

```cangjie
public operator func ==(other: Repetition): Bool
```

**Description:** Determines whether two Repetition enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Repetition](#enum-repetition)|Yes|-|Another Repetition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(Repetition)

```cangjie
public operator func !=(other: Repetition): Bool
```

**Description:** Determines whether two Repetition enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[Repetition](#enum-repetition)|Yes|-|Another Repetition enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|

## enum ScrollSource

```cangjie
public enum ScrollSource <: Equatable<ScrollSource> {
    | Drag
    | Fling
    | EdgeEffect
    | OtherUserInput
    | ScrollBar
    | ScrollBarFling
    | Scroller
    | ScrollerAnimation
    | ...
}
```

**Description:** Source of scroll operations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ScrollSource](#enum-scrollsource)>

### Drag

```cangjie
Drag
```

**Description:** Drag event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Fling

```cangjie
Fling
```

**Description:** Inertial scrolling after drag ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### EdgeEffect

```cangjie
EdgeEffect
```

**Description:** Edge scrolling effect of EdgeEffect.Spring.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### OtherUserInput

```cangjie
OtherUserInput
```

**Description:** Other user inputs besides drag, such as mouse wheel, keyboard events, etc.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ScrollBar

```cangjie
ScrollBar
```

**Description:** Scrollbar drag event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ScrollBarFling

```cangjie
ScrollBarFling
```

**Description:** Velocity-based inertial scrolling after scrollbar drag ends.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Scroller

```cangjie
Scroller
```

**Description:** Scroller methods without animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ScrollerAnimation

```cangjie
ScrollerAnimation
```

**Description:** Scroller methods with animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ScrollSource)

```cangjie
public operator func ==(other: ScrollSource): Bool
```

**Description:** Determines whether two ScrollSource enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ScrollSource](#enum-scrollsource)|Yes|-|Another ScrollSource enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are equal, otherwise returns false.|

### operator func !=(ScrollSource)

```cangjie
public operator func !=(other: ScrollSource): Bool
```

**Description:** Determines whether two ScrollSource enums are not equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ScrollSource](#enum-scrollsource)|Yes|-|Another ScrollSource enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enums are not equal, otherwise returns false.|
```## enum ContentType

```cangjie
public enum ContentType <: Equatable<ContentType> {
    | UserName
    | Password
    | NewPassword
    | FullStreetAddress
    | HouseNumber
    | DistrictAddress
    | CityAddress
    | ProvinceAddress
    | CountryAddress
    | PersonFullName
    | PersonLastName
    | PersonFirstName
    | PhoneNumber
    | PhoneCountryCode
    | FullPhoneNumber
    | EmailAddress
    | BankCardNumber
    | IdCardNumber
    | Nickname
    | DetailInfoWithoutStreet
    | FormatAddress
    | ...
}
```

**Function:** Auto-fill content types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ContentType](#enum-contenttype)>

### UserName

```cangjie
UserName
```

**Function:** [Username] Supports automatic saving and filling of usernames when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Password

```cangjie
Password
```

**Function:** [Password] Supports automatic saving and filling of passwords when password vault is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NewPassword

```cangjie
NewPassword
```

**Function:** [New Password] Supports automatic generation of new passwords when password vault is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FullStreetAddress

```cangjie
FullStreetAddress
```

**Function:** [Full Street Address] Supports automatic saving and filling of detailed addresses when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### HouseNumber

```cangjie
HouseNumber
```

**Function:** [House Number] Supports automatic saving and filling of house numbers when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### DistrictAddress

```cangjie
DistrictAddress
```

**Function:** [District/County] Supports automatic saving and filling of districts/counties when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### CityAddress

```cangjie
CityAddress
```

**Function:** [City] Supports automatic saving and filling of cities when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ProvinceAddress

```cangjie
ProvinceAddress
```

**Function:** [Province] Supports automatic saving and filling of provinces when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### CountryAddress

```cangjie
CountryAddress
```

**Function:** [Country] Supports automatic saving and filling of countries when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PersonFullName

```cangjie
PersonFullName
```

**Function:** [Full Name] Supports automatic saving and filling of full names when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PersonLastName

```cangjie
PersonLastName
```

**Function:** [Last Name] Supports automatic saving and filling of last names when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PersonFirstName

```cangjie
PersonFirstName
```

**Function:** [First Name] Supports automatic saving and filling of first names when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PhoneNumber

```cangjie
PhoneNumber
```

**Function:** [Phone Number] Supports automatic saving and filling of phone numbers when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PhoneCountryCode

```cangjie
PhoneCountryCode
```

**Function:** [Country Code] Supports automatic saving and filling of country codes when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FullPhoneNumber

```cangjie
FullPhoneNumber
```

**Function:** [Phone Number with Country Code] Supports automatic saving and filling of phone numbers including country codes when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### EmailAddress

```cangjie
EmailAddress
```

**Function:** [Email Address] Supports automatic saving and filling of email addresses when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BankCardNumber

```cangjie
BankCardNumber
```

**Function:** [Bank Card Number] Supports automatic saving and filling of bank card numbers when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### IdCardNumber

```cangjie
IdCardNumber
```

**Function:** [ID Card Number] Supports automatic saving and filling of ID card numbers when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Nickname

```cangjie
Nickname
```

**Function:** [Nickname] Supports automatic saving and filling of nicknames when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### DetailInfoWithoutStreet

```cangjie
DetailInfoWithoutStreet
```

**Function:** [Address Without Street] Supports automatic saving and filling of addresses without street information when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### FormatAddress

```cangjie
FormatAddress
```

**Function:** [Standardized Address] Supports automatic saving and filling of standardized addresses when contextual auto-fill is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ContentType)

```cangjie
public operator func ==(other: ContentType): Bool
```

**Function:** Determines whether two ContentType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ContentType](#enum-contenttype) | Yes | - | The other ContentType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ContentType)

```cangjie
public operator func !=(other: ContentType): Bool
```

**Function:** Determines whether two ContentType enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ContentType](#enum-contenttype) | Yes | - | The other ContentType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum MenuPolicy

```cangjie
public enum MenuPolicy <: Equatable<MenuPolicy> {
    | Default
    | Hide
    | Show
    | ...
}
```

**Function:** Menu display policy.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[MenuPolicy](#enum-menupolicy)>

### Default

```cangjie
Default
```

**Function:** Determines whether to show the menu based on the default underlying logic.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Hide

```cangjie
Hide
```

**Function:** Always hides the menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Show

```cangjie
Show
```

**Function:** Always shows the menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(MenuPolicy)

```cangjie
public operator func ==(other: MenuPolicy): Bool
```

**Function:** Determines whether two MenuPolicy enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MenuPolicy](#enum-menupolicy) | Yes | - | The other MenuPolicy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(MenuPolicy)

```cangjie
public operator func !=(other: MenuPolicy): Bool
```

**Function:** Determines whether two MenuPolicy enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [MenuPolicy](#enum-menupolicy) | Yes | - | The other MenuPolicy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum TextDecorationStyle

```cangjie
public enum TextDecorationStyle <: Equatable<TextDecorationStyle> {
    | Solid
    | Double
    | Dotted
    | Dashed
    | Wavy
    | ...
}
```

**Description:** Sets the style of text decoration lines.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextDecorationStyle](#enum-textdecorationstyle)>

### Solid

```cangjie
Solid
```

**Description:** Single solid line (default value).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Double

```cangjie
Double
```

**Description:** Double solid lines.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dotted

```cangjie
Dotted
```

**Description:** Dotted line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dashed

```cangjie
Dashed
```

**Description:** Dashed line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Wavy

```cangjie
Wavy
```

**Description:** Wavy line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextDecorationStyle)

```cangjie
public operator func ==(other: TextDecorationStyle): Bool
```

**Description:** Determines whether two TextDecorationStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextDecorationStyle](#enum-textdecorationstyle) | Yes | - | The other TextDecorationStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextDecorationStyle)

```cangjie
public operator func !=(other: TextDecorationStyle): Bool
```

**Description:** Determines whether two TextDecorationStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextDecorationStyle](#enum-textdecorationstyle) | Yes | - | The other TextDecorationStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum LineBreakStrategy

```cangjie
public enum LineBreakStrategy <: Equatable<LineBreakStrategy> {
    | Greedy
    | HighQuality
    | Balanced
    | ...
}
```

**Description:** Text line breaking rules.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[LineBreakStrategy](#enum-linebreakstrategy)>

### Greedy

```cangjie
Greedy
```

**Description:** Displays as many characters as possible on each line before breaking to the next line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### HighQuality

```cangjie
HighQuality
```

**Description:** Based on BALANCED, fills lines as much as possible, with lower weight on the last line, which may result in more whitespace on the last line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Balanced

```cangjie
Balanced
```

**Description:** Ensures that each line in a paragraph has the same width as much as possible without breaking words.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(LineBreakStrategy)

```cangjie
public operator func ==(other: LineBreakStrategy): Bool
```

**Description:** Determines whether two LineBreakStrategy enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LineBreakStrategy](#enum-linebreakstrategy) | Yes | - | The other LineBreakStrategy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(LineBreakStrategy)

```cangjie
public operator func !=(other: LineBreakStrategy): Bool
```

**Description:** Determines whether two LineBreakStrategy enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LineBreakStrategy](#enum-linebreakstrategy) | Yes | - | The other LineBreakStrategy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum TextContentStyle

```cangjie
public enum TextContentStyle <: Equatable<TextContentStyle> {
    | Default
    | Inline
    | ...
}
```

**Description:** Polymorphic styles for text boxes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextContentStyle](#enum-textcontentstyle)>

### Default

```cangjie
Default
```

**Description:** Default style. The cursor width is 1.5vp, and the cursor height is related to the text selection background height and font size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Inline

```cangjie
Inline
```

**Description:** Inline input style. The text selection background height matches the input box height.
Inline input is used in scenarios with clear distinctions between edit and non-edit states, such as renaming in a file list view.
The showError property is not supported.
Text dragging is not supported in inline mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextContentStyle)

```cangjie
public operator func ==(other: TextContentStyle): Bool
```

**Description:** Determines whether two TextContentStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextContentStyle](#enum-textcontentstyle) | Yes | - | The other TextContentStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextContentStyle)

```cangjie
public operator func !=(other: TextContentStyle): Bool
```

**Description:** Determines whether two TextContentStyle enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TextContentStyle](#enum-textcontentstyle) | Yes | - | The other TextContentStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum CheckBoxShape

```cangjie
public enum CheckBoxShape <: Equatable<CheckBoxShape> {
    | Circle
    | RoundedSquare
    | ...
}
```

**Description:** Checkbox shape types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[CheckBoxShape](#enum-checkboxshape)>

### Circle

```cangjie
Circle
```

**Description:** Circular shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### RoundedSquare

```cangjie
RoundedSquare
```

**Description:** Rounded square shape.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(CheckBoxShape)

```cangjie
public operator func ==(other: CheckBoxShape): Bool
```

**Description:** Determines whether two CheckBoxShape enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CheckBoxShape](#enum-checkboxshape) | Yes | - | The other CheckBoxShape enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(CheckBoxShape)

```cangjie
public operator func !=(other: CheckBoxShape): Bool
```

**Description:** Determines whether two CheckBoxShape enums are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CheckBoxShape](#enum-checkboxshape) | Yes | - | The other CheckBoxShape enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum TextHeightAdaptivePolicy

```cangjie
public enum TextHeightAdaptivePolicy <: Equatable<TextHeightAdaptivePolicy> {
    | MaxLinesFirst
    | MinFontSizeFirst
    | LayoutConstraintFirst
    | ...
}
```

**Function:** Sets the text height adaptation method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextHeightAdaptivePolicy](#enum-textheightadaptivepolicy)>

### MaxLinesFirst

```cangjie
MaxLinesFirst
```

**Function:** Sets the text height adaptation method to prioritize MaxLines.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### MinFontSizeFirst

```cangjie
MinFontSizeFirst
```

**Function:** Sets the text height adaptation method to prioritize font size reduction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### LayoutConstraintFirst

```cangjie
LayoutConstraintFirst
```

**Function:** Sets the text height adaptation method to prioritize layout constraints (height).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextHeightAdaptivePolicy)

```cangjie
public operator func ==(other: TextHeightAdaptivePolicy): Bool
```

**Function:** Determines whether two TextHeightAdaptivePolicy enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [TextHeightAdaptivePolicy](#enum-textheightadaptivepolicy) | Yes | - | The other TextHeightAdaptivePolicy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TextHeightAdaptivePolicy)

```cangjie
public operator func !=(other: TextHeightAdaptivePolicy): Bool
```

**Function:** Determines whether two TextHeightAdaptivePolicy enums are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [TextHeightAdaptivePolicy](#enum-textheightadaptivepolicy) | Yes | - | The other TextHeightAdaptivePolicy enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum ArrowPointPosition

```cangjie
public enum ArrowPointPosition <: Equatable<ArrowPointPosition> {
    | Start
    | Center
    | End
    | ...
}
```

**Function:** Arrow pointing position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ArrowPointPosition](#enum-arrowpointposition)>

### Start

```cangjie
Start
```

**Function:** Horizontal direction: located at the far left of the parent component; vertical direction: located at the top of the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Center

```cangjie
Center
```

**Function:** Located at the center of the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### End

```cangjie
End
```

**Function:** Horizontal direction: located at the far right of the parent component; vertical direction: located at the bottom of the parent component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(ArrowPointPosition)

```cangjie
public operator func ==(other: ArrowPointPosition): Bool
```

**Function:** Determines whether two ArrowPointPosition enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ArrowPointPosition](#enum-arrowpointposition) | Yes | - | The other ArrowPointPosition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(ArrowPointPosition)

```cangjie
public operator func !=(other: ArrowPointPosition): Bool
```

**Function:** Determines whether two ArrowPointPosition enums are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ArrowPointPosition](#enum-arrowpointposition) | Yes | - | The other ArrowPointPosition enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum TitleHeight

```cangjie
public enum TitleHeight <: Equatable<TitleHeight> {
    | MainOnly
    | MainWithSub
    | ...
}
```

**Function:** Sets the title bar height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TitleHeight](#enum-titleheight)>

### MainOnly

```cangjie
MainOnly
```

**Function:** Recommended height (56vp) for the title bar when only the main title is present.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### MainWithSub

```cangjie
MainWithSub
```

**Function:** Recommended height (82vp) for the title bar when both the main and sub titles are present.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TitleHeight)

```cangjie
public operator func ==(other: TitleHeight): Bool
```

**Function:** Determines whether two TitleHeight enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [TitleHeight](#enum-titleheight) | Yes | - | The other TitleHeight enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TitleHeight)

```cangjie
public operator func !=(other: TitleHeight): Bool
```

**Function:** Determines whether two TitleHeight enums are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [TitleHeight](#enum-titleheight) | Yes | - | The other TitleHeight enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum DialogButtonStyle

```cangjie
public enum DialogButtonStyle <: Equatable<DialogButtonStyle> {
    | Default
    | Highlight
    | ...
}
```

**Function:** Dialog button style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[DialogButtonStyle](#enum-dialogbuttonstyle)>

### Default

```cangjie
Default
```

**Function:** White background with blue text (dark theme: white background = black background).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Highlight

```cangjie
Highlight
```

**Function:** Blue background with white text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(DialogButtonStyle)

```cangjie
public operator func ==(other: DialogButtonStyle): Bool
```

**Function:** Determines whether two DialogButtonStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DialogButtonStyle](#enum-dialogbuttonstyle) | Yes | - | The other DialogButtonStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(DialogButtonStyle)

```cangjie
public operator func !=(other: DialogButtonStyle): Bool
```

**Function:** Determines whether two DialogButtonStyle enums are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DialogButtonStyle](#enum-dialogbuttonstyle) | Yes | - | The other DialogButtonStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum LengthMetricsUnit

```cangjie
public enum LengthMetricsUnit <: Equatable<LengthMetricsUnit> {
    | Default
    | Px
    | ...
}
```

**Function:** Length metrics unit enum.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[LengthMetricsUnit](#enum-lengthmetricsunit)>

### Default

```cangjie
Default
```

**Function:** Length type, used to describe lengths in the default vp pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Px

```cangjie
Px
```

**Function:** Length type, used to describe lengths in the px pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(LengthMetricsUnit)

```cangjie
public operator func ==(other: LengthMetricsUnit): Bool
```

**Function:** Determines whether two LengthMetricsUnit enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LengthMetricsUnit](#enum-lengthmetricsunit) | Yes | - | The other LengthMetricsUnit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(LengthMetricsUnit)

```cangjie
public operator func !=(other: LengthMetricsUnit): Bool
```

**Function:** Determines whether two LengthMetricsUnit enums are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LengthMetricsUnit](#enum-lengthmetricsunit) | Yes | - | The other LengthMetricsUnit enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum CanvasDirection

```cangjie
public enum CanvasDirection <: Equatable<CanvasDirection> {
    | Inherit
    | Ltr
    | Rtl
    | ...
}
```

**Description:** Sets the text direction for drawing text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[CanvasDirection](#enum-canvasdirection)>

### Inherit

```cangjie
Inherit
```

**Description:** Inherits the text direction set in the canvas component's common properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Ltr

```cangjie
Ltr
```

**Description:** Left-to-right direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Rtl

```cangjie
Rtl
```

**Description:** Right-to-left direction.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(CanvasDirection)

```cangjie
public operator func ==(other: CanvasDirection): Bool
```

**Description:** Determines whether two CanvasDirection enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CanvasDirection](#enum-canvasdirection) | Yes | - | The other CanvasDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(CanvasDirection)

```cangjie
public operator func !=(other: CanvasDirection): Bool
```

**Description:** Determines whether two CanvasDirection enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CanvasDirection](#enum-canvasdirection) | Yes | - | The other CanvasDirection enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum CanvasFillRule

```cangjie
public enum CanvasFillRule <: Equatable<CanvasFillRule> {
    | EvenOdd
    | NonZero
    | ...
}
```

**Description:** Specifies the rule for filling objects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[CanvasFillRule](#enum-canvasfillrule)>

### EvenOdd

```cangjie
EvenOdd
```

**Description:** Even-odd rule.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NonZero

```cangjie
NonZero
```

**Description:** Non-zero rule.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(CanvasFillRule)

```cangjie
public operator func ==(other: CanvasFillRule): Bool
```

**Description:** Determines whether two CanvasFillRule enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CanvasFillRule](#enum-canvasfillrule) | Yes | - | The other CanvasFillRule enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(CanvasFillRule)

```cangjie
public operator func !=(other: CanvasFillRule): Bool
```

**Description:** Determines whether two CanvasFillRule enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CanvasFillRule](#enum-canvasfillrule) | Yes | - | The other CanvasFillRule enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum FinishCallbackType

```cangjie
public enum FinishCallbackType <: Equatable<FinishCallbackType> {
    | Removed
    | Logically
    | ...
}
```

**Description:** Callback type when an animation finishes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[FinishCallbackType](#enum-finishcallbacktype)>

### Removed

```cangjie
Removed
```

**Description:** Triggers the callback when the entire animation finishes and is immediately removed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Logically

```cangjie
Logically
```

**Description:** Triggers the callback when the animation is in a logically descending state but may still be in its long tail state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(FinishCallbackType)

```cangjie
public operator func ==(other: FinishCallbackType): Bool
```

**Description:** Determines whether two FinishCallbackType enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FinishCallbackType](#enum-finishcallbacktype) | Yes | - | The other FinishCallbackType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(FinishCallbackType)

```cangjie
public operator func !=(other: FinishCallbackType): Bool
```

**Description:** Determines whether two FinishCallbackType enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [FinishCallbackType](#enum-finishcallbacktype) | Yes | - | The other FinishCallbackType enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## enum BlurStyle

```cangjie
public enum BlurStyle <: Equatable<BlurStyle> {
    | Thin
    | Regular
    | Thick
    | BackgroundThin
    | BackgroundRegular
    | BackgroundThick
    | BackgroundUltraThick
    | None
    | ComponentUltraThin
    | ComponentThin
    | ComponentRegular
    | ComponentThick
    | ComponentUltraThick
    | ...
}
```

**Description:** Foreground blur style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[BlurStyle](#enum-blurstyle)>

### Thin

```cangjie
Thin
```

**Description:** Thin blur effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Regular

```cangjie
Regular
```

**Description:** Regular blur effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Thick

```cangjie
Thick
```

**Description:** Thick blur effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BackgroundThin

```cangjie
BackgroundThin
```

**Description:** Close-range depth-of-field blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BackgroundRegular

```cangjie
BackgroundRegular
```

**Description:** Medium-range depth-of-field blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BackgroundThick

```cangjie
BackgroundThick
```

**Description:** Far-range depth-of-field blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### BackgroundUltraThick

```cangjie
BackgroundUltraThick
```

**Description:** Ultra-far-range depth-of-field blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### None

```cangjie
None
```

**Description:** No blur effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ComponentUltraThin

```cangjie
ComponentUltraThin
```

**Description:** Component ultra-thin material blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ComponentThin

```cangjie
ComponentThin
```

**Description:** Component thin material blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ComponentRegular

```cangjie
ComponentRegular
```

**Description:** Component regular material blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ComponentThick

```cangjie
ComponentThick
```

**Description:** Component thick material blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### ComponentUltraThick

```cangjie
ComponentUltraThick
```

**Description:** Component ultra-thick material blur.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(BlurStyle)

```cangjie
public operator func ==(other: BlurStyle): Bool
```

**Description:** Determines whether two BlurStyle enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BlurStyle](#enum-blurstyle) | Yes | - | The other BlurStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(BlurStyle)

```cangjie
public operator func !=(other: BlurStyle): Bool
```

**Description:** Determines whether two BlurStyle enums are not equal.

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [BlurStyle](#enum-blurstyle) | Yes | - | The other BlurStyle enum to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |## enum DismissReason

```cangjie
public enum DismissReason <: Equatable<DismissReason> {
    | PressBack
    | TouchOutside
    | CloseButton
    | SlideDown
    | ...
}
```

**Function:** Reasons for popup dismissal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[DismissReason](#enum-dismissreason)>

### PressBack

```cangjie
PressBack
```

**Function:** Triggered by pressing the back button, left/right swipe gestures, or ESC key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### TouchOutside

```cangjie
TouchOutside
```

**Function:** Triggered when clicking the overlay mask.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### CloseButton

```cangjie
CloseButton
```

**Function:** Triggered by clicking the close button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### SlideDown

```cangjie
SlideDown
```

**Function:** Triggered by swipe-down gesture to dismiss.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(DismissReason)

```cangjie
public operator func ==(other: DismissReason): Bool
```

**Function:** Compares two DismissReason enums for equality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DismissReason](#enum-dismissreason)|Yes|-|Another DismissReason enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are equal, otherwise false.|

### operator func !=(DismissReason)

```cangjie
public operator func !=(other: DismissReason): Bool
```

**Function:** Compares two DismissReason enums for inequality.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[DismissReason](#enum-dismissreason)|Yes|-|Another DismissReason enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are not equal, otherwise false.|

## enum TextInputStyle

```cangjie
public enum TextInputStyle <: Equatable<TextInputStyle> {
    | Default
    | Inline
    | ...
}
```

**Function:** Represents text input styles.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextInputStyle](#enum-textinputstyle)>

### Default

```cangjie
Default
```

**Function:** Default style with 1.5vp cursor width. Cursor height relates to text selection background height and font size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Inline

```cangjie
Inline
```

**Function:** Inline input style where text selection background matches input field height. Suitable for scenarios requiring clear distinction between edit/non-edit states (e.g., renaming in file lists). Doesn't support `showError` property or text drag-and-drop in this mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextInputStyle)

```cangjie
public operator func ==(other: TextInputStyle): Bool
```

**Function:** Compares two TextInputStyle enums for equality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TextInputStyle](#enum-textinputstyle)|Yes|-|Another TextInputStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are equal, otherwise false.|

### operator func !=(TextInputStyle)

```cangjie
public operator func !=(other: TextInputStyle): Bool
```

**Function:** Compares two TextInputStyle enums for inequality.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TextInputStyle](#enum-textinputstyle)|Yes|-|Another TextInputStyle enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are not equal, otherwise false.|

## enum TextAreaType

```cangjie
public enum TextAreaType <: Equatable<TextAreaType> {
    | Normal
    | Number
    | PhoneNumber
    | Email
    | NumberDecimal
    | Url
    | ...
}
```

**Function:** Represents input field types.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[TextAreaType](#enum-textareatype)>

### Normal

```cangjie
Normal
```

**Function:** Basic input mode supporting numbers, letters, underscores, spaces, and special characters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Number

```cangjie
Number
```

**Function:** Numeric-only input mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### PhoneNumber

```cangjie
PhoneNumber
```

**Function:** Phone number input mode supporting digits, spaces, +, -, *, #, (, ), with unlimited length.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Email

```cangjie
Email
```

**Function:** Email address input mode supporting numbers, letters, underscores, dots, !, #, $, %, &, ', *, +, -, /, =, ?, ^, `, {, |, }, ~, and @ (only one @ allowed).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### NumberDecimal

```cangjie
NumberDecimal
```

**Function:** Decimal number input mode supporting digits and decimal point (only one allowed).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Url

```cangjie
Url
```

**Function:** URL input mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func ==(TextAreaType)

```cangjie
public operator func ==(other: TextAreaType): Bool
```

**Function:** Compares two TextAreaType enums for equality.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TextAreaType](#enum-textareatype)|Yes|-|Another TextAreaType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are equal, otherwise false.|

### operator func !=(TextAreaType)

```cangjie
public operator func !=(other: TextAreaType): Bool
```

**Function:** Compares two TextAreaType enums for inequality.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[TextAreaType](#enum-textareatype)|Yes|-|Another TextAreaType enum to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the enums are not equal, otherwise false.|

## type VoidCallback

```cangjie
public type VoidCallback = () -> Unit
```

**Function:** [VoidCallback](#type-voidcallback) is a type alias for [() -> Unit](#type-voidcallback).

**Type:** () -> Unit

## type Callback\<T, V>

```cangjie
public type Callback<T, V> = (T) -> V
```

**Function:** Callback\<T, V> is a type alias for (T) -> V.

**Type:** (T) -> V

## type CustomBuilder

```cangjie
public type CustomBuilder = () -> Unit
```

**Function:** CustomBuilder is a type alias for () -> Unit.

**Type:** () -> Unit

## type TransitionFinishCallback

```cangjie
public type TransitionFinishCallback = (Bool) -> Unit
```

**Function:** [TransitionFinishCallback](#type-transitionfinishcallback) is a type alias for (Bool) -> Unit.

**Type:** (Bool) -> Unit

## type ItemGeneratorFunc\<T>

```cangjie
public type ItemGeneratorFunc<T> = (T, Int64) -> Unit
```

**Function:** Defines an item generator function.

**Type:** (T, Int64) -> Unit

## type KeyGeneratorFunc\<T>

```cangjie
public type KeyGeneratorFunc<T> = (T, Int64) -> String
```

**Function:** Defines a key generator function.

**Type:** (T, Int64) -> String