# Radio

A radio button component that provides corresponding user interaction options.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(String, String)

```cangjie
public init(value!: String, group!: String)
```

**Function:** Creates a radio button component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | **Named parameter.** The value of the current radio button. |
| group | String | Yes | - | **Named parameter.** The group name to which the current radio button belongs. Only one radio button with the same group can be selected. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func checked(Bool)

```cangjie
public func checked(value: Bool): This
```

**Function:** The selected state of the radio button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Sets the selected state of the radio button.<br>Initial value: false.<br/>**Note:**<br/>When value is true, it indicates a change from unselected to selected. When value is false, it indicates a change from selected to unselected. |

## Component Events

### func onChange((Bool) -> Unit)

```cangjie
public func onChange(callback: (Bool) -> Unit): This
```

**Function:** Triggered when the selected state of the radio button changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | (Bool)->Unit | Yes | - | The state of the radio button. |

## Example (Setting Background Color)

This example demonstrates customizing the background color of radio buttons by configuring `checkedBackgroundColor`.

<!-- run -->

```cangjie

package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var radioName: String = "Null"

    func build() {
        Flex(direction: FlexDirection.Row, justifyContent: FlexAlign.Center, alignItems: ItemAlign.Center) {
            Column() {
                Text("Radio1")
                Radio(group: "radioGroup", value: "Radio1").checked(true).height(50).width(50)
            }
            Column() {
                Text("Radio2")
                Radio(group: "radioGroup", value: "Radio2").checked(true).height(50).width(50)
            }
            Column() {
                Text("Radio3")
                Radio(group: "radioGroup", value: "Radio3").checked(true).height(50).width(50)
            }
        }
    }
}
```

![radio](figures/radio.gif)