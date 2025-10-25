# ohos.base (Common Callback Information)

This module defines common exception information that occurs during interface calls.

## Import Module

```cangjie
import ohos.base.*
```

## let Main

```cangjie
public let Main: MainThreadContext = MainThreadContext.instance_
```

**Function:** Main is actually an object of type MainThreadContext, indicating that the thread in this context will be bound to the main thread (UI thread).

**Type:** [MainThreadContext](#class-mainthreadcontext)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

## func launch(() -> Unit)

```cangjie
public func launch(task: () -> Unit): Unit
```

**Function:** Submits a task to the main thread for execution.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|task|()->Unit|Yes|-|The task to execute.|

## interface CollectionEx

```cangjie
public interface CollectionEx<T> {
    prop size: Int64
    operator func [](idx: Int64, value!: T): Unit
    operator func [](idx: Int64): T
}
```

**Function:** Array type. Internal interface, used by the framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop size

```cangjie
prop size: Int64
```

**Function:** Array size.

**Type:** Int64

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### func [](Int64, T)

```cangjie
operator func [](idx: Int64, value!: T): Unit
```

**Function:** Writes an array element at the specified index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|idx|Int64|Yes|-|Index value.|
|value|T|Yes|-| **Named parameter.** The value to write.|

### func \[](Int64)

```cangjie
operator func [](idx: Int64): T
```

**Function:** Retrieves an array element by index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|idx|Int64|Yes|-|Index value.|

**Return Value:**

|Type|Description|
|:----|:----|
|T|Array element.|

## interface Length

```cangjie
public interface Length {
    prop value: Float64
    prop unitType: LengthType
}
```

**Function:** Float64, Int64, and AppResource all implement the Length interface type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop unitType

```cangjie
prop unitType: LengthType
```

**Function:** Used by the UI framework.

**Type:** [LengthType](#enum-lengthtype)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop value

```cangjie
prop value: Float64
```

**Function:** Used by the UI framework.

**Type:** Float64

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

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

**Function:** Pixel units. Used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop fp

```cangjie
prop fp: Length
```

**Function:** Font pixel, similar to vp, adapts to screen density changes and varies with system font size settings.

**Type:** [Length](#interface-length)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop lpx

```cangjie
prop lpx: Length
```

**Function:** Logical pixel unit of the viewport. The l.px unit is the ratio of the actual screen width to the logical width (configured via designWidth), with the default designWidth value being 720. When designWidth is 720, on a screen with an actual width of 1440 physical pixels, 1l.px equals 2.px in size.

**Type:** [Length](#interface-length)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop percent

```cangjie
prop percent: Length
```

**Function:** Percentage type, used to describe lengths in percent pixel units.

**Type:** [Length](#interface-length)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop px

```cangjie
prop px: Length
```

**Function:** Physical pixel unit of the screen.

**Type:** [Length](#interface-length)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### prop vp

```cangjie
prop vp: Length
```

**Function:** Screen density-related pixel, converted to physical screen pixels based on screen pixel density. When a value has no unit, the default unit is vp. On a screen with an actual width of 1440 physical pixels, 1vp is approximately equal to 3px.<br/>**Note:** <br/> The ratio of vp to px depends on the screen pixel density.

**Type:** [Length](#interface-length)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

## interface ResourceColor

```cangjie
public interface ResourceColor {
    func toUInt32(): UInt32
}
```

**Function:** Color, UInt32, Int64, and AppResource all implement the ResourceColor interface type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### func toUInt32()

```cangjie
func toUInt32(): UInt32
```

**Function:** Converts to a Uint32 color value.

**Return Value:**

|Type|Description|
|:----|:----|
|UInt32|Uint32 color value.|

## interface ResourceStr

```cangjie
public interface ResourceStr {}
```

**Function:** String type, used to describe the types of string parameters that can be used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

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
    public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: Float32 = 1.0)
    public init(value: UInt32)
}
```

**Function:** Color type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parent Type:**

- [ResourceColor](#interface-resourcecolor)

### static let Black

```cangjie
public static let Black: Color = Color(0xff000000)
```

**Function:** Black.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let Blue

```cangjie
public static let Blue: Color = Color(0xff0000ff)
```

**Function:** Blue.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let Gray

```cangjie
public static let Gray: Color = Color(0xff808080)
```

**Function:** Gray.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let Green

```cangjie
public static let Green: Color = Color(0xff008000)
```

**Function:** Green.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let Red

```cangjie
public static let Red: Color = Color(0xffff0000)
```

**Function:** Red.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let Transparent

```cangjie
public static let Transparent: Color = Color(0, 0, 0, alpha: 0.0)
```

**Function:** Transparent.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### static let White

```cangjie
public static let White: Color = Color(0xffffffff)
```

**Function:** White.

**Type:** [Color](#class-color)

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

### init(UInt8, UInt8, UInt8, Float32)

```cangjie
public init(red: UInt8, green: UInt8, blue: UInt8, alpha!: Float32 = 1.0)
```

**Function:** Constructs a Color type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|red|UInt8|Yes|-|Red channel value in RGB.|
|green|UInt8|Yes|-|Green channel value in RGB.|
|blue|UInt8|Yes|-|Blue channel value in RGB.|
|alpha|Float32|No|1.0|***\*Named parameter.\**** Transparency channel value, range [0.0, 1.0].|

### init(UInt32)

```cangjie
public init(value: UInt32)
```

**Function:** Constructs a Color type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|value|UInt32|Yes|-|Uint32 color value. The alpha, R, G, and B channels each occupy 8 bits of the input in order. If only R, G, and B channels are input, the alpha channel defaults to 0xff.|

### func toUInt32()

```cangjie
public func toUInt32(): UInt32
```

**Function:** Converts to a Uint32 color value.

**Return Value:**

|Type|Description|
|:----|:----|
|UInt32|Uint32 color value.|## class MainThreadContext

```cangjie
public class MainThreadContext {}
```

**Function:** Thread context used by the framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func end()

```cangjie
public func end(): Unit
```

**Function:** Used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func hasEnded()

```cangjie
public func hasEnded(): Bool
```

**Function:** Used by the UI framework.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|-|

## class ReuseParams

```cangjie
public class ReuseParams {
    public init(arr: Array<(String, Any)>)
}
```

**Function:** Parameters for the aboutToReuse lifecycle function, from which developers can obtain the construction parameters of reusable components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Array\<(String,Any)>)

```cangjie
public init(arr: Array<(String, Any)>)
```

**Function:** Creates a ReuseParams object, typically not called by developers.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|arr| Array\<(String, Any)> |Yes|-|An array containing tuples of component construction parameters.|

### func get\<T>(String)

```cangjie
public func get<T>(key: String): ?T
```

**Function:** Retrieves the corresponding construction parameter by key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|key|String|Yes|-|The name of the construction parameter.|

**Return Value:**

|Type|Description|
|:----|:----|
|?T|The value of the construction parameter.|

## enum LengthType

```cangjie
public enum LengthType <: Length & Equatable<LengthType> {
    | px(Float64)
    | vp(Float64)
    | fp(Float64)
    | percent(Float64)
    | lpx(Float64)
    | ...
}
```

**Function:** Length type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Types:**

- [Length](#interface-length)
- Equatable\<LengthType>

### fp(Float64)

```cangjie
fp(Float64)
```

**Function:** Font pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### lpx(Float64)

```cangjie
lpx(Float64)
```

**Function:** Logical pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### percent(Float64)

```cangjie
percent(Float64)
```

**Function:** Percentage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### px(Float64)

```cangjie
px(Float64)
```

**Function:** Basic pixel unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### vp(Float64)

```cangjie
vp(Float64)
```

**Function:** Screen density unit.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop unitType

```cangjie
public prop unitType: LengthType
```

**Function:** Used by the UI framework.

**Type:** [LengthType](#enum-lengthtype)

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop value

```cangjie
public prop value: Float64
```

**Function:** Used by the UI framework.

**Type:** Float64

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### static func parse(Int32)

```cangjie
public static func parse(value: Int32): LengthType
```

**Function:** Constructs a LengthType instance based on the length type value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|value|Int32|Yes|-|The value of the length type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[LengthType](#enum-lengthtype)|The LengthType instance.|

### func !=(LengthType)

```cangjie
public operator func !=(other: LengthType): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[LengthType](#enum-lengthtype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise false.|

### func ==(LengthType)

```cangjie
public operator func ==(other: LengthType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[LengthType](#enum-lengthtype)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise false.|

### func getValue()

```cangjie
public func getValue(): Int32
```

**Function:** Retrieves the value of the enum.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|Int32|The value of the enum.|

## type Callback

```cangjie
public type Callback<T, V>=(T) -> V
```

**Function:** [Callback](#type-callback) is an alias for the [(T) -> V](#type-callback) type.

## type VoidCallback

```cangjie
public type VoidCallback =() -> Unit
```

**Function:** [VoidCallback](#type-voidcallback) is an alias for the [() -> Unit](#type-voidcallback) type.