# Text

A component for displaying text content.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain [Span](./cj-text-input-span.md#span) and [ImageSpan](./cj-text-input-imagespan.md#imagespan) child components.

## Creating the Component

### init(ResourceStr, TextController)

```cangjie
public init(content: ResourceStr, controller!: TextController = TextController())
```

**Function:** Creates a Text component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| content | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Text content, referencing system resources or application resources. |
| controller | [TextController](#class-textcontroller) | No | TextController() | **Named parameter.** Controller for the Text component. |

### init(ResourceStr, TextController, () -> Unit)

```cangjie
public init(content: ResourceStr, controller!: TextController = TextController(), child!: () -> Unit)
```

**Function:** Creates a Text component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| content | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Text content. Does not take effect when containing Span child components without attribute strings, displaying Span content instead, and the Text component's styles will not apply.<br/>Initial value: ''. |
| controller | [TextController](#class-textcontroller) | No | TextController() | **Named parameter.** Controller for the Text component. |
| child | () -> Unit | No | { => } | Child components of the Text component. |

### init(TextController, () -> Unit)

```cangjie
public init(controller!: TextController = TextController(), child!: () -> Unit)
```

**Function:** Creates a Text component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| controller | [TextController](#class-textcontroller) | No | TextController() | **Named parameter.** Controller for the Text component. |
| child | () -> Unit | Yes | - | Child components of the Text component. |

### init(TextController)

```cangjie
public init(controller!: TextController = TextController())
```

**Function:** Creates a Text component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| controller | [TextController](#class-textcontroller) | No | TextController() | **Named parameter.** Controller for the Text component. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Component Attributes

### func baselineOffset(Length)

```cangjie
public func baselineOffset(value: Length): This
```

**Function:** Sets the baseline offset for text.

> **Note:**
>
> - Positive values shift the content upward, negative values shift it downward.
> - When set as a percentage, the default value is displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Baseline offset for text. When set as a percentage, the default value is displayed.<br>Initial value: 0. |

### func decoration(TextDecorationType, ResourceColor, TextDecorationStyle)

```cangjie
public func decoration(decorationType!: TextDecorationType, color!: ResourceColor,
    decorationStyle!: TextDecorationStyle = TextDecorationStyle.Solid): This
```

**Function:** Sets the text decoration line style and its color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| decorationType | [TextDecorationType](./cj-common-types.md#enum-textdecorationtype) | Yes | - | **Named parameter.** Text decoration line style.<br>Initial value: TextDecorationType.None. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | **Named parameter.** Text decoration line color.<br>Initial value: Color.Black. |
| decorationStyle | [TextDecorationStyle](./cj-common-types.md#enum-textdecorationstyle) | No | TextDecorationStyle.Solid | **Named parameter.** Text decoration line style. |

### func fontColor(ResourceColor)

```cangjie
public func fontColor(value: ResourceColor): This
```

**Function:** Sets the font color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Sets the font color using resource references.<br>Initial value: 'e6182431'. |

### func fontFamily(ResourceStr)

```cangjie
public func fontFamily(value: ResourceStr): This
```

**Function:** Sets the font family list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Font family list. Default font: 'HarmonyOS Sans'. |

### func fontSize(Length)

```cangjie
public func fontSize(value: Length): This
```

**Function:** Sets the font size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Font size. Percentage units are not supported.<br>Initial value: 16.fp. |

### func fontStyle(FontStyle)

```cangjie
public func fontStyle(value: FontStyle): This
```

**Function:** Sets the font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [FontStyle](./cj-common-types.md#enum-fontstyle) | Yes | - | Font style.<br>Initial value: FontStyle.Normal. |

### func fontWeight(FontWeight)

```cangjie
public func fontWeight(value: FontWeight): This
```

**Function:** Sets the font weight of the text. Setting too large a value may cause truncation in different fonts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [FontWeight](./cj-common-types.md#enum-fontweight) | Yes | - | Font weight of the text.<br>Initial value: FontWeight.Normal. |

### func lineHeight(Length)

```cangjie
public func lineHeight(value: Length): This
```

**Function:** Sets the line height of the text based on Length.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Line height of the text. When set to a value ≤ 0, the line height is not restricted and adapts to the font size. |

### func lineSpacing(Length)

```cangjie
public func lineSpacing(value: Length): This
```

**Function:** Sets the line spacing of the text. When set to a value ≤ 0, the default value of 0 is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Line spacing of the text.<br>Initial value: 0. |

### func maxFontSize(Length)

```cangjie
public func maxFontSize(value: Length): This
```

**Function:** Sets the maximum display font size for the text based on Length.

> **Note:**
>
> - Must be used in conjunction with [minFontSize](#func-minfontsizelength) and [maxLines](#func-maxfontsizelength) or layout size constraints. Does not take effect when used alone and does not apply to child components or attribute strings.
> - When adaptive font size is active, the fontSize setting does not take effect.
> - When maxFontSize is ≤ 0, adaptive font size is disabled, and the value set in [fontSize](#func-fontsizelength) takes effect. If not set, the default value applies.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Maximum display font size for the text. Unit: fp. |

### func maxLines(Int32)

```cangjie
public func maxLines(value: Int32): This
```

**Function:** Sets the maximum number of lines for the text.

> **Note:**
>
> By default, text wraps automatically. If this property is specified, the text will not exceed the specified number of lines. Excess text can be truncated using [textOverflow](#func-textoverflowtextoverflow).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Maximum number of lines for the text. |

### func minFontSize(Length)

```cangjie
public func minFontSize(value: Length): This
```

**Function:** Sets the minimum display font size for the text based on Length.

> **Note:**
>
> - Must be used in conjunction with [maxFontSize](#func-maxfontsizelength) and [maxLines](#func-maxlinesint32) or layout size constraints. Does not take effect when used alone and does not apply to child components or attribute strings.
> - When adaptive font size is active, the fontSize setting does not take effect.
> - When minFontSize is ≤ 0, adaptive font size is disabled, and the value set in [fontSize](#func-fontsizelength) takes effect. If not set, the default value applies.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Minimum display font size for the text. Unit: fp. |

### func textAlign(TextAlign)

```cangjie
public func textAlign(value: TextAlign): This
```

**Function:** Sets the horizontal alignment of the text paragraph.

> **Note:**
>
> - The text paragraph width fills the Text component width.
> - The vertical position of the text paragraph can be controlled using the [align](./cj-universal-attribute-location.md#func-alignalignment) attribute. However, the horizontal position cannot be controlled via the align attribute in this component. Specific effects are as follows:
Alignment.TopStart, Alignment.Top, Alignment.TopEnd: Content aligns to the top.
Alignment.Start, Alignment.Center, Alignment.End: Content is vertically centered.
Alignment.BottomStart, Alignment.Bottom, Alignment.BottomEnd: Content aligns to the bottom.
> - When textAlign is set to TextAlign.JUSTIFY, the [wordBreak](./cj-common-types.md#enum-wordbreak) attribute must be set based on the text content. The last line of text does not participate in justification and aligns to the start horizontally.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [TextAlign](./cj-common-types.md#enum-textalign) | Yes | - | Text alignment for multiline text.<br>Initial value: TextAlign.Start. |

### func textCase(TextCase)

```cangjie
public func textCase(value: TextCase): This
```

**Function:** Sets the text case.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [TextCase](./cj-common-types.md#enum-textcase) | Yes | - | Text case.<br>Initial value: TextCase.Normal. |

### func textOverflow(TextOverflow)

```cangjie
public func textOverflow(value: TextOverflow): This
```

**Function:** Sets the display mode for text overflow.

> **Note:**
>
> - Text truncation is character-based. For example, English words are truncated as whole units. To truncate by letters, add a zero-width space (\u200B) between letters. From API version 11, it is recommended to use the wordBreak attribute set to WordBreak.BREAK_ALL for letter-based truncation.
> - When overflow is set to TextOverflow.None, TextOverflow.Clip, or TextOverflow.Ellipsis, it must be used with maxLines. Does not take effect when used alone. Setting TextOverflow.None has the same effect as TextOverflow.Clip.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [TextOverflow](./cj-common-types.md#enum-textoverflow) | Yes | - | Display mode for text overflow. Must be used with maxLines. Does not take effect when used alone.<br>Initial value: TextOverflow.Clip. |## Basic Type Definitions

### class ShadowOptions

```cangjie
public class ShadowOptions {
    public var radius: Float64
    public var shadowType: ShadowType
    public var color: ResourceColor
    public var offsetX: Float64
    public var offsetY: Float64
    public var fill: Bool
    public init(
        radius!: Float64,
        shadowType!: ShadowType = ShadowType.Color,
        color!: ResourceColor = Color.Black,
        offsetX!: Float64 = 0.0,
        offsetY!: Float64 = 0.0,
        fill!: Bool = false
    )
}
```

**Function:** Shadow options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var color

```cangjie
public var color: ResourceColor
```

**Function:** Sets the shadow color.

**Type:** [ResourceColor](cj-common-types.md#interface-resourcecolor)

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var fill

```cangjie
public var fill: Bool
```

**Function:** Sets whether the shadow is filled.

**Type:** Bool

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offsetX

```cangjie
public var offsetX: Float64
```

**Function:** Sets the horizontal offset of the shadow.

**Type:** Float64

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offsetY

```cangjie
public var offsetY: Float64
```

**Function:** Sets the vertical offset of the shadow.

**Type:** Float64

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var radius

```cangjie
public var radius: Float64
```

**Function:** Sets the blur radius of the shadow.

**Type:** Float64

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var shadowType

```cangjie
public var shadowType: ShadowType
```

**Function:** Sets the shadow type.

**Type:** [ShadowType](cj-common-types.md#enum-shadowtype)

**Readable/Writable:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Float64, ShadowType, ResourceColor, Float64, Float64, Bool)

```cangjie
public init(
    radius!: Float64,
    shadowType!: ShadowType = ShadowType.Color,
    color!: ResourceColor = Color.Black,
    offsetX!: Float64 = 0.0,
    offsetY!: Float64 = 0.0,
    fill!: Bool = false
)
```

**Function:** Constructs a ShadowOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| radius | Float64 | Yes | - | Sets the blur radius of the shadow. |
| shadowType | [ShadowType](cj-common-types.md#enum-shadowtype) | No | ShadowType.Color | Sets the shadow type. |
| color | [ResourceColor](cj-common-types.md#interface-resourcecolor) | No | Color.Black | Sets the shadow color. |
| offsetX | Float64 | No | 0.0 | Sets the horizontal offset of the shadow. |
| offsetY | Float64 | No | 0.0 | Sets the vertical offset of the shadow. |
| fill | Bool | No | false | Sets whether the shadow is filled. |

### class TextController

```cangjie
public class TextController {
    public init()
}
```

**Function:** Controller for the Text component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init()

```cangjie
public init()
```

**Function:** Creates an object of type TextController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func closeSelectionMenu()

```cangjie
public func closeSelectionMenu(): Unit
```

**Function:** Closes the custom selection menu or the system default selection menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## Example Code

<!--run-->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.hilog.*
import ohos.arkui.component.CopyOptions as MyCopyOptions
import std.collection.ArrayList
import std.ast.Block

@Entry
@Component
class EntryView {
    @State
    var message: String = "Hello"
    let controller: TextController = TextController()
    @State var shadowOptionsArray: Array<ShadowOptions> = [ShadowOptions(radius: 10.0), ShadowOptions(radius: 10.0, shadowType: ShadowType.Blur, color: Color.Red, offsetX: 1.0, offsetY: 1.0, fill: true)]
    @Builder func LongPressTextCustomMenu() {
        Column() {
            Button('LongPress')
        }
    }

    @Builder func RightClickTextCustomMenu() {
        Column() {
            Button('RightClick')
        }
    }

    @Builder func SelectTextCustomMenu() {
        Column() {
            Button('Select')
        }
    }

    func build() {
        Scroll() {
            Column {
                //Display the set text style effects
                Text(message)
                    .fontFamily(@r(app.string.fontFamily))
                    .height(100.vp)
                    .width(100.vp)
                    .id("textComponent1")
                Text(message)
                    .fontSize(20)
                    .fontColor(0XFFFF0000)
                    .fontStyle(FontStyle.Italic)
                    .fontWeight(FontWeight.W900)
                    .id("textComponent2")
                //Set text line height
                Blank(min: 10)
                Text(message)
                    .textAlign(TextAlign.End).baselineOffset(10.vp)
                    .id("textComponent3")
                    .minFontSize(@r(app.string.font_size))
                    .lineHeight(@r(app.string.line_height))

                Text(message)
                    .decoration(decorationType: TextDecorationType.None, color: Color.Red)
                    .id("textComponent4")
                //Set text baseline offset
                Text(
                    "This is the text with the height adaptive policy set.This is the text with the height adaptive policy set."
                )
                    .minFontSize(10.fp)
                    .maxFontSize(30.fp)
                    .maxLines(1).id("textComponent5")
                    .baselineOffset(@r(app.string.baselineOffset))
                    .fontColor(@r(app.color.blue_23C452))
                //Set display method when text is too long
                Text(
                    "This is the text with the height adaptive policy set.This is the text with the height adaptive policy set"
                )
                    .fontSize(24.vp)
                    .maxLines(1)
                    .textOverflow(TextOverflow.Ellipsis)
                    .id("textComponent6")
                //Set text to display in all uppercase
                Text("Hello")
                    .textCase(TextCase.UpperCase)
                    .id("textComponent7")
                    .maxFontSize(@r(app.string.font_size))
                //Set text to display in all lowercase
                Text("Hello")
                    .foregroundColor(Color.Blue)
                    .id("textComponent8")
                    .fontSize(@r(app.string.font_size))
                    .textOverflow(TextOverflow.None)
                    .textCase(TextCase.LowerCase)
                //Set touch hot zone
                Text("Hello")
                    .responseRegion(Rectangle(x: 100.percent, y: 0.vp, width: 50.percent, height: 100.percent))
                    .responseRegion([Rectangle(x: 0.vp, y: 100.percent, width: 100.percent, height: 100.percent),Rectangle(x: 100.percent, y: 0.vp, width: 50.percent, height: 100.percent)])
                Text('This is the text content with given settings. This is the text content with given settings')
                    .baselineOffset(10)
                    .decoration(decorationType: TextDecorationType.Underline, color: Color.Red, decorationStyle: TextDecorationStyle.Dotted)
                    .fontColor(Color.Red)
                    .fontFamily("HarmonyOS Sans")
                    .fontSize(10.fp)
                    .fontStyle(FontStyle.Italic)
                    .fontWeight(FontWeight.Bolder)
                    .lineHeight(40)
                    .lineSpacing(20)
                    .maxLines(1)
                    .textAlign(TextAlign.Center)
                    .textCase(TextCase.LowerCase)
                    .textOverflow(TextOverflow.None)
                    .id("TextGivenSetting")
                //Display text style effects
                Text('This is the text content with given font settings.')
                    .size(width:15, height: 15)
                    .fontWeight(FontWeight.Bolder)
                    .fontFamily('HarmonyOS Sans')
                    .fontStyle(FontStyle.Italic)
                    .decoration(decorationType: TextDecorationType.LineThrough, color: Color.Red, decorationStyle: TextDecorationStyle.Dashed)
                    .textCase(TextCase.UpperCase)
                    .id("TextGivenFont")
                //Set text effects using resource calls and display
                Text(@r(app.string.module_desc))
                    .fontSize(@r(app.string.font_size))
                    .maxFontSize(@r(app.string.font_size))
                    .minFontSize(@r(app.string.font_size))
                    .fontFamily(@r(app.string.fontFamily))
                    .lineHeight(@r(app.string.line_height))
                    .baselineOffset(@r(app.string.baselineOffset))
                    .fontColor(@r(app.color.blue_23C452))
                    .id("TextResource")

                Text('Email: xxx@xxxxxx.com')
                    .textOverflow(TextOverflow.None)
                    .id("TextDetectConfig4")
                //Display default font style effects
                Text('This is the text content with default settings.')
                    .id("TextDefault1")
                //Set text offset
                Text('This is the text content with percent baselineOffset.')
                    .baselineOffset(10.percent)
                    .decoration(decorationType: TextDecorationType.Overline, color: Color.Red, decorationStyle: TextDecorationStyle.Double)
                    .id("TextBoundaryValue1")
                //Display text size set in percentage
                Text('This is the text content with percent fontSize.')
                    .fontSize(10.percent)
                    .id("TextBoundaryValue4")
                //Display effect when text line height is negative
                Text('This is the text content with -10 lineHeight.')
                    .lineHeight(-10)
                    .fontSize(20)
                    .id("TextBoundaryValue6")
                Text('This is the text content with -10 lineSpacing.')
                    .lineSpacing(-10)
                    .id("TextBoundaryValue7")
                //Set text to display ellipsis when too long
                Text("textOverflow line line line line line line line line line line line line line line line line line.")
                    .textOverflow(TextOverflow.Ellipsis)
                    .maxLines(1)
                    .id("TextCombine1")
                Text("This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content. ")
                    .minFontSize(10)
                    .maxFontSize(30)
                    .maxLines(1)
                    .fontSize(50)
                    .id("TextCombine6")
                Text("This is the setting of textOverflow to Clip text content This is the setting of textOverflow to None text content. ")
                    .minFontSize(-10)
                    .maxFontSize(30)
                    .maxLines(1)
                    .id("TextCombine7")
            }
        }.height(100.percent).width(100.percent)
    }
}
```
