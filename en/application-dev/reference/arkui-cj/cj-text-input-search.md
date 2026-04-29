# Search

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides a search box component for users to input search content.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(?ResourceStr, ?ResourceStr, Option\<AppResource>, Option\<SearchController>)

```cangjie
public init(
    value!: ?ResourceStr = None,
    placeholder!: ?ResourceStr = None,
    icon!: Option<AppResource> = None,
    controller!: Option<SearchController> = None
)
```

**Function:** Creates a Search component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Currently displayed search text content. Initial value: "". |
| placeholder | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Hint text when there is no input. Initial value: "". |
| icon | Option\<[AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource)> | No | None | **Named parameter.** Search icon path, defaults to system search icon. |
| controller | Option\<[SearchController](#class-searchcontroller)> | No | None | **Named parameter.** Search component controller. |

## Common Attributes/Events

Common attributes: All supported.

Common events: All supported.

## Component Attributes

### func searchButton(?ResourceStr)

```cangjie
public func searchButton(value: ?ResourceStr): This
```

**Function:** Sets the search button at the end of the search box.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Text content of the search button at the end of the search box. Initial value: "". |

### func placeholderColor(?ResourceColor)

```cangjie
public func placeholderColor(value: ?ResourceColor): This
```

**Function:** Sets the placeholder text color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Target color. Initial value: '#99182431'. |

### func placeholderFont(?Length, ?FontWeight, ?FontStyle, ?ResourceStr)

```cangjie
public func placeholderFont(
    size!: ?Length = None,
    weight!: ?FontWeight = None,
    style!: ?FontStyle = None,
    family!: ?ResourceStr = None
): This
```

**Function:** Sets the placeholder style, including font size, font weight, font family, and font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Placeholder text size. When Length is Int64 or Float64, uses fp unit. Supports percentage strings. Initial value: 16.fp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Target font weight of the placeholder. Initial value: FontWeight.W400. |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Target font style of the placeholder. Initial value: FontStyle.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Font family of the placeholder. Initial value: "". |

### func textFont(?Length, ?FontWeight, ?FontStyle, ?ResourceStr)

```cangjie
public func textFont(
    size!: ?Length = None,
    weight!: ?FontWeight = None,
    style!: ?FontStyle = None,
    family!: ?ResourceStr = None
): This
```

**Function:** Sets the input text style in the search box, including font size, font weight, font family, and font style. Currently only supports default font family.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Text size. When Length is Int64 or Float64, uses fp unit. Supports percentage strings. Initial value: 16.fp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Target font weight of the input. Initial value: FontWeight.W400. |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Target font style of the input. Initial value: FontStyle.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Font family of the input. Initial value: "". |

### func copyOption(?CopyOptions)

```cangjie
public func copyOption(value: ?CopyOptions): This
```

**Function:** Sets whether the input text can be copied.

> **Note:**
>
> - When CopyOptions.None is set, text in the current Search cannot be copied, cut, translated, or assisted, only pasted.
> - When CopyOptions.None is set, dragging is not allowed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[CopyOptions](./cj-common-types.md#enum-copyoptions) | Yes | - | Copy options for the search component. Initial value: CopyOptions.LocalDevice, supports copying within the device. |

## Component Events

### func onSubmit(?(String) -> Unit)

```cangjie
public func onSubmit(callback: ?(String) -> Unit): This
```

**Function:** Triggered when clicking the search icon, search button, or pressing the soft keyboard search button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(String) -> Unit | Yes | - | Callback function, triggered when submitting search content. Parameter: Current text content in the search box. Initial value: { _ => }. |

### func onChange(?(String) -> Unit)

```cangjie
public func onChange(callback: ?(String) -> Unit): This
```

**Function:** Triggered when the input content changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(String) -> Unit | Yes | - | Callback function, triggered when the current input text content changes. Initial value: { _ => }. |

### func onCopy(?(String) -> Unit)

```cangjie
public func onCopy(callback: ?(String) -> Unit): This
```

**Function:** Triggered when performing a copy operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(String) -> Unit | Yes | - | Callback function, triggered when cutting. Parameter: Returns the cut text content. Initial value: { _ => }. |

### func onCut(?(String) -> Unit)

```cangjie
public func onCut(callback: ?(String) -> Unit): This
```

**Function:** Triggered when performing a cut operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(String) -> Unit | Yes | - | Callback function, triggered when cutting. Parameter: Returns the cut text content. Initial value: { _ => }. |

### func onPaste(?(String) -> Unit)

```cangjie
public func onPaste(callback: ?(String) -> Unit): This
```

**Function:** Triggered when performing a paste operation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(String) -> Unit | Yes | - | Callback function, triggered when the component triggers a system clipboard paste operation. Initial value: { _ => }. |

## Basic Type Definitions

### class SearchController

```cangjie
public class SearchController <: TextContentControllerBase {
    public init()
}
```

**Function:** Controller for the Search component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- [TextContentControllerBase](./cj-common-types.md#interface-textcontentcontrollerbase)

#### init()

```cangjie
public init()
```

**Function:** Creates an object of type SearchController.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### func caretPosition(?Int32)

```cangjie
public func caretPosition(value: ?Int32): Unit
```

**Function:** Sets the position of the input cursor.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Int32 | Yes | - | Character length from the start of the string to the cursor position. Initial value: 0. |

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
            //Set the search button text at the end of the search box to "SearchBtn"
            .searchButton("SearchBtn")
            //Width 300, height 35
            .width(300)
            .height(35)
            //Set the background color of the search component
            .backgroundColor(0xDDDDDD)
            //Set the placeholder text color
            .placeholderColor(0x000000)
            //Set the placeholder text style
            .placeholderFont(size: 26.px, weight: FontWeight.W100, family: "serif", style: FontStyle.Normal)
            .onSubmit({value =>
              submitValue = value
            })
            .onChange({value =>
              changeValue = value
            })
            //Set the outer margin, the top of the component is 30vp from the parent container
            .margin(top: 30)
            .id("searchComponent")
        }
    }
}
```

![search](figures/search.png)