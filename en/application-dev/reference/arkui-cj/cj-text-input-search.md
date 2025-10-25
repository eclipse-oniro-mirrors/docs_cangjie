# Search

Provides a search box component for users to input search content.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Subcomponents

None

## Creating the Component

### init(String, String, Option\<AppResource>, Option\<SearchController>)

```cangjie

public init(
    value!: ResourceStr = "",
    placeholder!: ResourceStr = "",
    icon!: Option<AppResource> = Option.None,
    controller!: Option<SearchController> = Option.None
)
```

**Function:** Creates a Search component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ResourceStr | No | "" | **Named parameter.** Currently displayed search text content. |
| placeholder | ResourceStr | No | "" | **Named parameter.** Hint text when there is no input. |
| icon | Option\<[AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)> | No | Option.None | Search icon path, using the system search icon by default.<br>**Note:** <br>The icon data source supports local and network images.<br> - Supported image formats include png, jpg, bmp, svg, gif, pixelmap, and heif.<br> - Supports Base64 strings. Format: data:image/[png\|jpeg\|bmp\|webp\| **Named parameter.** heif];base64,[base64 data], where [base64 data] is the Base64 string data.<br>If set together with the searchIcon property, searchIcon takes precedence. |
| controller | [SearchController](#class-searchcontroller) | No | Option.None | **Named parameter.** Search component controller. |

## Common Properties/Common Events

Common properties: All supported.

Common events: All supported.

## Component Properties

### func copyOption(CopyOptions)

```cangjie

public func copyOption(value: CopyOptions): This
```

**Function:** Sets whether the input text can be copied.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [CopyOptions](./cj-common-types.md#enum-copyoptions) | Yes | - | Copy options for the search component.<br>Initial value: CopyOptions.LocalDevice, supports copying within the device. |

### func placeholderColor(ResourceColor)

```cangjie

public func placeholderColor(value: ResourceColor): This
```

**Function:** Sets the placeholder text color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Target color.<br>Initial value: 0x99000000. |

### func placeholderFont(Length, FontWeight, FontStyle, ResourceStr)

```cangjie

public func placeholderFont(
    size!: Length = 16.fp,
    weight!: FontWeight = FontWeight.W400,
    style!: FontStyle = FontStyle.Normal,
    family!: ResourceStr = ""
): This
```

**Function:** Sets the placeholder style, including font size, font weight, font family, and font style. Currently supports 'HarmonyOS Sans' font and [registered custom fonts](./cj-apis-font.md).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.fp | **Named parameter.** Placeholder text size. When Length is Int64 or Float64, uses fp unit. Supports percentage strings. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.W400 | **Named parameter.** Target font weight for the placeholder. |
| style | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Target font style for the placeholder. |
| family | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** Font family for the placeholder. |

### func searchButton(String)

```cangjie
public func searchButton(value: ResourceStr): This
```

**Function:** Sets the search button at the end of the search box.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ResourceStr | Yes | - | Text content of the search button at the end of the search box. |

### func textFont(Length, FontWeight, FontStyle, ResourceStr)

```cangjie

public func textFont(
    size!: Length = 16.fp,
    weight!: FontWeight = FontWeight.W400,
    style!: FontStyle = FontStyle.Normal,
    family!: ResourceStr = ""
): This
```

**Function:** Sets the style of the input text in the search box, including font size, font weight, font family, and font style. Currently only supports the default font family.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.fp | **Named parameter.** Text size. When Length is Int64 or Float64, uses fp unit. Supports percentage strings. |
| weight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.W400 | **Named parameter.** Target font weight for the input. |
| style | [FontStyle](./cj-common-types.md#enum-fontstyle) | No | FontStyle.Normal | **Named parameter.** Target font style for the input. |
| family | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** Font family for the input. |

## Component Events

### func onChange((String) -> Unit)

```cangjie

public func onChange(callback: (String) -> Unit): This
```

**Function:** Triggered when the input content changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (String)->Unit | Yes | - | Callback function, triggered when the current input text content changes. |

### func onCopy((String) -> Unit)

```cangjie

public func onCopy(callback: (String) -> Unit): This
```

**Function:** Triggered when a copy operation is performed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (String)->Unit | Yes | - | Callback function, triggered when cutting. Parameter: Returns the cut text content. |

### func onCut((String) -> Unit)

```cangjie

public func onCut(callback: (String) -> Unit): This
```

**Function:** Triggered when a cut operation is performed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (String)->Unit | Yes | - | Callback function, triggered when cutting. Parameter: Returns the cut text content. |

### func onPaste((String) -> Unit)

```cangjie

public func onPaste(callback: (String) -> Unit): This
```

**Function:** Triggered when a paste operation is performed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (String)->Unit | Yes | - | Callback function, triggered when the component triggers a system clipboard paste operation. |

### func onSubmit((String) -> Unit)

```cangjie

public func onSubmit(callback: (String) -> Unit): This
```

**Function:** Triggered when clicking the search icon, search button, or pressing the soft keyboard search button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (String)->Unit | Yes | - | Callback function, triggered when submitting search content. Parameter: Current text content input in the search box. |

## Basic Type Definitions

### class SearchController

```cangjie
public class SearchController TextContentControllerBase{

    public init()
}
```

**Function:** Controller for the Search component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init()

```cangjie

public init()
```

**Function:** Creates an object of type SearchController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func caretPosition(Int32)

```cangjie

public func caretPosition(value: Int32): Unit
```

**Function:** Sets the position of the input cursor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The character length from the start of the string to the cursor position. |

## Example Code

<!--run-->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var changeValue: String = ""
    @State var submitValue: String = ""

    let controller = SearchController()
    func build() {
        Flex(direction: FlexDirection.Row, justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center) {
          Text(submitValue)
          Text(changeValue)
          Search(value: "", placeholder: "Type to search", controller: controller)
            //Sets the search button text at the end of the search box to "SearchBtn"
            .searchButton("SearchBtn")
            //Width 300, height 35
            .width(300)
            .height(35)
            //Sets the background color of the search component
            .backgroundColor(0xDDDDDD)
            //Sets the placeholder text color
            .placeholderColor(0x000000)
            //Sets the placeholder text style
            .placeholderFont(size: 26.px, weight: FontWeight.W100, family: "serif", style: FontStyle.Normal)
            .onSubmit({value =>
              submitValue = value
            })
            .onChange({value =>
              changeValue = value
            })
            //Sets the margin, with the top of the component 30vp from the parent container
            .margin(top: 30)
            .id("searchComponent")
        }
    }
}
```

![search](figures/search.png)