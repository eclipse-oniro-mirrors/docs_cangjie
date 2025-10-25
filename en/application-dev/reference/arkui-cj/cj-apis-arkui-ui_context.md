# ohos.arkui.ui_context (UIContext)

Provides UI context-related functionalities.

## Import Module

```cangjie
import kit.UIKit.*
```

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

**Function:** Text properties to be calculated.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

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

**Function:** Creates a structure describing the text to be calculated.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| textContent | String | Yes | - | **Named parameter.** Sets the content of the text to be calculated. |
| fontWeight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Sets the font weight of the text to be calculated, using corresponding enumeration values from FontWeight. |
| fontFamily | String | No | "HarmonyOS Sans" | **Named parameter.** Sets the font list for the text to be calculated. Default font is 'HarmonyOS Sans', and currently only this font is supported. |
| constraintWidth | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | None | **Named parameter.** Sets the layout width for the text to be calculated.<br>**Note:** <br>Default unit is vp, percentage settings are not supported. If not set, the text SizeOption width will be the maximum width occupied by a single line layout; if set, it will use the specified value. |
| fontSize | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | 16.fp | **Named parameter.** Sets the font size of the text to be calculated.<br>**Note:** <br>Percentage settings are not supported; when using numeric types, the fp unit is applied. |
| lineHeight | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | None | **Named parameter.** Sets the line height of the text to be calculated, using vp units. |
| baselineOffset | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | 0.0.vp | **Named parameter.** Sets the baseline offset of the text to be calculated. |
| letterSpacing | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | None | **Named parameter.** Sets the letter spacing of the text to be calculated, using vp units. |
| textIndent | Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | No | None | **Named parameter.** Sets the indentation of the first line of text, using vp units. |
| maxLines | UInt32 | No | 0 | **Named parameter.** Sets the maximum number of lines for the text to be calculated. |
| textAlign | [TextAlign](./cj-common-types.md#enum-textalign) | No | TextAlign.Start | **Named parameter.** Sets the horizontal alignment of the text to be calculated. |
| fontStyle | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Sets the font style of the text to be calculated. |
| overflow | [TextOverflow](./cj-common-types.md#enum-textoverflow) | No | TextOverflow.Clip | **Named parameter.** Sets the truncation method for the text when it exceeds the limit. |
| textCase | [TextCase](./cj-common-types.md#enum-textcase) | No | TextCase.Normal | **Named parameter.** Sets the text case of the text to be calculated. |
| wordBreak | [WordBreak](./cj-common-types.md#enum-wordbreak) | No | WordBreak.BreakWord | **Named parameter.** Sets the line breaking rules. |

## class SizeOptions

```cangjie
public class SizeOptions {
    public var width: Length = 0
    public var height: Length = 0
    public init(width!: Length = 0, height!: Length = 0)
}
```

**Function:** Represents the layout size occupied by text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var height

```cangjie
public var height: Length = 0
```

**Function:** Represents the height of the text layout.

**Type:** Float64

**Read-Write Capability:** Read-Write

### var width

```cangjie
public var width: Length = 0
```

**Function:** Represents the width of the text layout.

**Type:** Float64

**Read-Write Capability:** Read-Write

### init(Length, Length)

```cangjie
public init(width!: Length = 0, height!: Length = 0)
```

**Function:** Main constructor for Size.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| width | Float64 | Yes | - | The width of the layout occupied by text.<br>Initial value: 0.0. |
| height | Float64 | Yes | - | The height of the layout occupied by text.<br>Initial value: 0.0. |