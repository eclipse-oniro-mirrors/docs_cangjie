# MeasureUtils

Provides calculations related to text width, height, etc.

> **Note:**
>
> The following APIs require first obtaining a MeasureUtils instance via the [getMeasureUtils()](./cj-apis-uicontext-uicontext.md#func-getmeasureutils) method from [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext), then calling corresponding methods through this instance.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class MeasureUtils

```cangjie
public class MeasureUtils {}
```

**Function:** Provides calculations related to text width, height, etc.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func measureText(MeasureOptions)

```cangjie
public func measureText(options: MeasureOptions): Float64
```

**Function:** Calculates the width of specified text in single-line layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|options|[MeasureOptions](#class-measureoptions)|Yes|-|Text description information to be calculated.|

**Return Value:**

|Type|Description|
|:----|:----|
|Float64|Text width. Unit: px.|

### func measureTextSize(MeasureOptions)

```cangjie
public func measureTextSize(options: MeasureOptions): SizeOptions
```

**Function:** Measures the width and height of text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|options|[MeasureOptions](#class-measureoptions)|Yes|-|Text description information to be calculated.|

**Return Value:**

|Type|Description|
|:----|:----|
|[SizeOptions](#class-sizeoptions)|Returns the layout width and height occupied by the text. Unit: px.|

## class MeasureOptions

```cangjie
public class MeasureOptions {
    public init(
        textContent!: String,
        fontWeight!: FontWeight = FontWeight.Normal,
        fontFamily!: String = "HarmonyOS Sans",
        constraintWidth!: ?Length = None,
        fontSize!: ?Length = 16.fp,
        lineHeight!: ?Length = None,
        baselineOffset!: ?Length = 0.0.vp,
        letterSpacing!: ?Length = None,
        textIndent!: ?Length = None,
        maxLines!: UInt32 = 0,
        textAlign!: TextAlign = TextAlign.Start,
        fontStyle!: FontStyle = FontStyle.Normal,
        overflow!: TextOverflow = TextOverflow.Clip,
        textCase!: TextCase = TextCase.Normal,
        wordBreak!: WordBreak = WordBreak.BreakWord
    )
}
```

**Function:** Attributes of the text to be calculated.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(String, FontWeight, String, ?Length, ?Length, ?Length, ?Length, ?Length, ?Length, UInt32, TextAlign, FontStyle, TextOverflow, TextCase, WordBreak)

```cangjie
public init(
    textContent!: String,
    fontWeight!: FontWeight = FontWeight.Normal,
    fontFamily!: String = "HarmonyOS Sans",
    constraintWidth!: ?Length = None,
    fontSize!: ?Length = 16.fp,
    lineHeight!: ?Length = None,
    baselineOffset!: ?Length = 0.0.vp,
    letterSpacing!: ?Length = None,
    textIndent!: ?Length = None,
    maxLines!: UInt32 = 0,
    textAlign!: TextAlign = TextAlign.Start,
    fontStyle!: FontStyle = FontStyle.Normal,
    overflow!: TextOverflow = TextOverflow.Clip,
    textCase!: TextCase = TextCase.Normal,
    wordBreak!: WordBreak = WordBreak.BreakWord
)
```

**Function:** Creates a MeasureOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|textContent|String|Yes|-| **Named parameter.** Text content.|
|fontWeight|[FontWeight](./cj-common-types.md#enum-fontweight)|No|FontWeight.Normal| **Named parameter.** Font weight. Initial value: FontWeight.Normal.|
|fontFamily|String|No|"HarmonyOS Sans"| **Named parameter.** Font family. Initial value: "HarmonyOS Sans".|
|constraintWidth|?[Length](./cj-common-types.md#interface-length)|No|None| **Named parameter.** Constraint width for text. Initial value: 0.|
|fontSize|?[Length](./cj-common-types.md#interface-length)|No|16.fp| **Named parameter.** Font size. Initial value: 16.fp|
|lineHeight|?[Length](./cj-common-types.md#interface-length)|No|None| **Named parameter.** Line height. Initial value: 0.|
|baselineOffset|?[Length](./cj-common-types.md#interface-length)|No|0.0.vp| **Named parameter.** Text baseline offset. Initial value: 0.0.vp.|
|letterSpacing|?[Length](./cj-common-types.md#interface-length)|No|None| **Named parameter.** Letter spacing. Initial value: 0.|
|textIndent|?[Length](./cj-common-types.md#interface-length)|No|None| **Named parameter.** Text indentation. Initial value: 0.|
|maxLines|UInt32|No|0| **Named parameter.** Maximum lines. Initial value: 0.|
|textAlign|[TextAlign](./cj-common-types.md#enum-textalign)|No|TextAlign.Start| **Named parameter.** Text alignment. Initial value: TextAlign.Start.|
|fontStyle|[FontStyle](./cj-common-types.md#enum-fontstyle)|No|FontStyle.Normal| **Named parameter.** Font style. Initial value: FontStyle.Normal.|
|overflow|[TextOverflow](./cj-common-types.md#enum-textoverflow)|No|TextOverflow.Clip| **Named parameter.** Text overflow handling. Initial value: TextOverflow.Clip.|
|textCase|[TextCase](./cj-common-types.md#enum-textcase)|No|TextCase.Normal| **Named parameter.** Text case style. Initial value: TextCase.Normal.|
|wordBreak|[WordBreak](./cj-common-types.md#enum-wordbreak)|No|WordBreak.BreakWord| **Named parameter.** Word breaking method. Initial value: WordBreak.BreakWord.|

## class SizeOptions

```cangjie
public class SizeOptions {
    public var height: Length
    public var width: Length
    public init(Length, Length)
}
```

**Function:** Width and height dimension type, used to describe the size dimensions of components during layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var height

```cangjie
public var height: Length
```

**Function:** Height.

**Type:** [Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### var width

```cangjie
public var width: Length
```

**Function:** Width.

**Type:** [Length](./cj-common-types.md#interface-length)

**Access:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(Length, Length)

```cangjie
public init(width!: Length = 0, height!: Length = 0)
```

**Function:** Constructor for SizeOptions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|width|[Length](./cj-common-types.md#interface-length)|No|0| **Named parameter.** Width. Initial value: 0|
|height|[Length](./cj-common-types.md#interface-length)|No|0| **Named parameter.** Height. Initial value: 0|
