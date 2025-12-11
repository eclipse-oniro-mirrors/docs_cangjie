# Select

Provides a dropdown selection menu that allows users to choose among multiple options.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(?Array\<SelectOption>)

```cangjie
public init(options: ?Array<SelectOption>)
```

**Function:** Constructs a dropdown selection menu component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| options | ?Array\<[SelectOption](#class-selectoptions)> | Yes | - | Sets the dropdown options.<br>Initial value: []. |

## Universal Attributes/Events

Universal attributes: All supported.

Universal events: All supported.

## Component Attributes

### func selected(?Int32)

```cangjie
public func selected(value: ?Int32): This
```

**Function:** Sets the index of the initial selected option in the dropdown menu, where the first item has an index of 0. If the `selected` attribute is not set or an invalid value is provided, the initial selection value is -1, and no menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Int32 | Yes | - | The index of the initial selected option in the dropdown menu.<br>Initial value: 0. |

### func value(?ResourceStr)

```cangjie
public func value(value: ?ResourceStr): This
```

**Function:** Sets the text content of the dropdown button itself. By default, this text is replaced with the selected menu item's text when an option is chosen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | The text content of the dropdown button itself. If the text length exceeds the column width, it will be truncated.<br>Initial value: "". |

### func font(?FontStyle, ?FontWeight, ?Length, ?ResourceStr)

```cangjie
public func font(
    style!: ?FontStyle = None,
    weight!: ?FontWeight = None,
    size!: ?Length = None,
    family!: ?ResourceStr = None
): This
```

**Function:** Sets the text style of the dropdown button itself. If `size` is 0, the text is not displayed. If `size` is negative, the text size follows the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Specifies the font style.<br>Initial value: FontStyle.Normal. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Specifies the font weight.<br>Initial value: FontWeight.Medium. |
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Specifies the font size and line height. Percentage values are not supported.<br>Initial value: 16.vp. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Specifies the font family.<br>Initial value: "sans-serif". |

### func fontColor(?ResourceColor)

```cangjie
public func fontColor(value: ?ResourceColor): This
```

**Function:** Sets the text color of the dropdown button itself based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The text color of the dropdown button itself.<br>Initial value: @r(sys.color.ohos_id_color_text_primary) blended with the transparency of @r(sys.color.ohos_id_alpha_content_primary). |

### func selectedOptionBgColor(?ResourceColor)

```cangjie
public func selectedOptionBgColor(value: ?ResourceColor): This
```

**Function:** Sets the background color of the selected dropdown menu item based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The background color of the selected dropdown menu item.<br>Initial value: @r(sys.color.ohos_id_color_component_activated) blended with the transparency of @r(sys.color.ohos_id_alpha_highlight_bg). |

### func selectedOptionFont(?FontStyle, ?FontWeight, ?Length, ?String)

```cangjie
public func selectedOptionFont(
    style!: ?FontStyle = None,
    weight!: ?FontWeight = None,
    size!: ?Length = None,
    family!: ?String = None
): This
```

**Function:** Sets the text style of the selected dropdown menu item. If `size` is 0, the text is not displayed. If `size` is negative, the text size follows the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Specifies the font style.<br>Initial value: FontStyle.Normal. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Specifies the font weight.<br>Initial value: FontWeight.Medium. |
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Specifies the text size. Percentage values are not supported.<br>Initial value: 16.vp. |
| family | ?String | No | None | **Named parameter.** Specifies the font list.<br>Initial value: "sans-serif". |

### func selectedOptionFontColor(?ResourceColor)

```cangjie
public func selectedOptionFontColor(value: ?ResourceColor): This
```

**Function:** Sets the text color of the selected dropdown menu item based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The text color of the selected dropdown menu item.<br>Initial value: @r(sys.color.ohos_id_color_text_primary_activated). |

### func optionBgColor(?ResourceColor)

```cangjie
public func optionBgColor(value: ?ResourceColor): This
```

**Function:** Sets the background color of dropdown menu items based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The background color of dropdown menu items.<br>Initial value: Color.Transparent. |

### func optionFont(?FontStyle, ?FontWeight, ?Length, ?ResourceStr)

```cangjie
public func optionFont(
    style!: ?FontStyle = None,
    weight!: ?FontWeight = None,
    size!: ?Length = None,
    family!: ?ResourceStr = None
): This
```

**Function:** Sets the text style of dropdown menu items. If `size` is 0, the text is not displayed. If `size` is negative, the text size follows the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Specifies the font style.<br>Initial value: FontStyle.Normal. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Specifies the font weight.<br>Initial value: FontWeight.Medium. |
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Specifies the font size and line height. Percentage values are not supported.<br>Initial value: 16.vp. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Specifies the font family.<br>Initial value: "sans-serif". |

### func optionFontColor(?ResourceColor)

```cangjie
public func optionFontColor(value: ?ResourceColor): This
```

**Function:** Sets the text color of dropdown menu items based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The text color of dropdown menu items.<br>Initial value: @r(sys.color.ohos_id_color_text_primary). |

### func space(?Length)

```cangjie
public func space(value: ?Length): This
```

**Function:** Sets the spacing between the text and arrow of dropdown menu items based on the specified Length value. Percentage values are not supported. If the value is less than or equal to 8, the initial value is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The spacing between the text and arrow of dropdown menu items.<br>Initial value: 8.0.vp. |

### func arrowPosition(?ArrowPosition)

```cangjie
public func arrowPosition(value: ?ArrowPosition): This
```

**Function:** Sets the alignment between the text and arrow of dropdown menu items.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?ArrowPosition | Yes | - | The alignment between the text and arrow of dropdown menu items.<br>Initial value: ArrowPosition.End. |

### func menuAlign(?MenuAlignType, ?Offset)

```cangjie
public func menuAlign(alignType!: ?MenuAlignType, offset!: ?Offset): This
```

**Function:** Sets the alignment between the dropdown button and the dropdown menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| alignType | ?[MenuAlignType](./cj-common-types.md#enum-menualigntype) | Yes | - | **Named parameter.** The alignment type.<br>Initial value: MenuAlignType.Start. |
| offset | ?[Offset](./cj-common-types.md#class-offset) | Yes | - | **Named parameter.** The offset of the dropdown menu relative to the dropdown button after alignment.<br>Initial value: Offset(0.0.vp, 0.0.vp). |

### func optionWidth(?OptionWidthMode)

```cangjie
public func optionWidth(value: ?OptionWidthMode): This
```

**Function:** Sets the width of dropdown menu items. The `OptionWidthMode` type is an enumeration that determines whether the dropdown menu inherits the width of the dropdown button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[OptionWidthMode](./cj-common-types.md#enum-optionwidthmode) | Yes | - | The width of dropdown menu items. |

### func optionWidth(?Length)

```cangjie
public func optionWidth(value: ?Length): This
```

**Function:** Sets the width of dropdown menu items based on the specified Length value. Percentage values are not supported.

If an invalid value or a value less than the minimum width (56.vp) is provided, this attribute does not take effect, and the menu item width defaults to the initial value (i.e., the menu's initial width is 2 grid units).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The width of dropdown menu items. |

### func optionHeight(?Length)

```cangjie
public func optionHeight(value: ?Length): This
```

**Function:** Sets the maximum height of the dropdown menu based on the specified Length value. The initial maximum height of the dropdown menu is 80% of the available screen height. The set maximum height cannot exceed this initial value.

If a negative or zero value is provided, this attribute does not take effect, and the dropdown menu's maximum height defaults to the initial value (i.e., 80% of the available screen height).

Valid values are greater than 0. If the actual height of all dropdown menu options is less than the set height, the dropdown menu height adjusts to the actual height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The maximum height of the dropdown menu. |

### func menuBackgroundColor(?ResourceColor)

```cangjie
public func menuBackgroundColor(value: ?ResourceColor): This
```

**Function:** Sets the background color of the dropdown menu based on the specified Color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The background color of the dropdown menu.<br>Initial value: Color.Transparent. |

### func menuBackgroundBlurStyle(?BlurStyle)

```cangjie
public func menuBackgroundBlurStyle(value: ?BlurStyle): This
```

**Function:** Sets the background blur material of the dropdown menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | Yes | - | The background blur material of the dropdown menu.<br>Initial value: BlurStyle.ComponentUltraThick. |

## Component Events

### func onSelect(?OnSelectCallback)

```cangjie
public func onSelect(callback: ?OnSelectCallback): This
```

**Function:** Triggers this callback when an item in the dropdown menu is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[OnSelectCallback](#type-onselectcallback) | Yes | - | The index and value of the selected item.<br>Initial value: { _, _ => }. |## Basic Type Definitions

### class SelectOption

```cangjie
public class SelectOption {
    public var value: ?ResourceStr
    public var icon: ?ResourceStr
    public init(value!: ?ResourceStr, icon!: ?ResourceStr = None)
}
```

**Function:** An object for configuring dropdown menu component parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### var value

```cangjie
public var value: ?ResourceStr
```

**Function:** The content of the dropdown option.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### var icon

```cangjie
public var icon: ?ResourceStr
```

**Function:** The icon of the dropdown option.

**Type:** ?[ResourceStr](./cj-common-types.md#interface-resourcestr)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### init(?ResourceStr, ?ResourceStr)

```cangjie
public init(value!: ?ResourceStr, icon!: ?ResourceStr = None)
```

**Function:** Constructs a SelectOption object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** The content of the dropdown option. Initial value: "". |
| icon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** The icon of the dropdown option. Initial value: "". |

### type OnSelectCallback

```cangjie
public type OnSelectCallback = (Int32, String) -> Unit
```

**Function:** Defines the type of selection callback function.

**Type:** (Int32, String) -> Unit

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

## Example Code

### Example 1 (Configuring Dropdown Menu)

This example implements a dropdown menu by configuring SelectOption.

<!-- run -->

```cangjie

package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.i18n.*
import ohos.resource_manager.*
import ohos.hilog.*
import ohos.resource.__GenerateResource__

@Entry
@Component
class EntryView {
    @State var text: String = "TTTTT"
    @State var index: Int32 = 2
    @State var space: Int64 = 8

    @State var values1: Array<SelectOption> = [
            SelectOption(value: "aaa", icon: @r(app.media.startIcon)),
            SelectOption(value: "bbb", icon: @r(app.media.startIcon)),
            SelectOption(value: "ccc", icon: @r(app.media.startIcon)),
            SelectOption(value: "ddd", icon: @r(app.media.startIcon))]

    @State var arrow: ArrowPosition = ArrowPosition.End

    func build() {
        Column {
            Select(this.values1)
            .selected(1)
            .value(this.text)
            .font(size: 16.vp, weight: FontWeight.W500)
            .fontColor(0x182431)
            .selectedOptionFont(size: 16.vp, weight: FontWeight.W400)
            .space(this.space)
            .arrowPosition(this.arrow)
            .menuAlign(alignType: MenuAlignType.Start, offset: Offset(0, 0))
            .optionWidth(200)
            .optionHeight(300)
            .onSelect({ index: Int32, text: String =>
                Hilog.info(0, "AppLogCj", " ==================  Select ====================: ${index}")
                Hilog.info(0, "AppLogCj", " ==================  text ====================: ${text}")
                this.index = index;
                this.text = text;
            })
        }.width(100.percent)
    }
}
```

![selectExample](./figures/selectExample.gif)