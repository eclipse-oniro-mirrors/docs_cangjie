# Row

A container that lays out its children horizontally.

## Child Components

Can contain child components.

## Creating the Component

### init(Length, () -> Unit)

```cangjie

public init(space!: Length = 0.vp, child!: () -> Unit = {=>})
```

**Function:** Creates a Row container containing child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| space | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | Horizontal spacing between elements. <br>Does not take effect when space is negative or justifyContent is set to FlexAlign.SpaceBetween, FlexAlign.SpaceAround, FlexAlign.SpaceEvenly. <br> Initial value: 0, Unit: vp <br> **Note:** Optional values are numbers greater than or equal to 0. |
| child | ()->Unit | No | { => } | Child components within the container. |

## Common Attributes/Common Events

Common Attributes: All supported

Common Events: All supported

## Component Attributes

### func alignItems(VerticalAlign)

```cangjie

public func alignItems(value: VerticalAlign): This
```

**Function:** Sets the vertical alignment format of child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [VerticalAlign](cj-common-types.md#enum-verticalalign) | Yes | - | Vertical alignment format of child components. <br> Initial value: FlexAlign.Start |

### func justifyContent(FlexAlign)

```cangjie

public func justifyContent(value: FlexAlign): This
```

**Function:** Sets the horizontal alignment format of child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [FlexAlign](cj-common-types.md#enum-flexalign) | Yes | - | Horizontal alignment format of child components. <br> Initial value: FlexAlign.Start |

## Example Code

This example demonstrates the usage of Row's alignItems and justifyContent properties.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
            Column(space: 5) {
            // Set horizontal spacing between child components to 5
                Text("space")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
                Row(space: 5) {
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0xAFEEEE)
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0x00FFFF)
                }
                .width(90.percent)
                .height(107)
                .border(width: 1.vp)

                // Set vertical alignment of child elements
                Text("alignItems(Bottom)")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
                Row() {
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0xAFEEEE)
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0x00FFFF)
                }
                .alignItems(VerticalAlign.Bottom)
                .width(90.percent)
                .height(15.percent)
                .border(width: 1.vp)

                Text("alignItems(Center)")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
                Row() {
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0xAFEEEE)
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0x00FFFF)
                }
                .alignItems(VerticalAlign.Center)
                .width(90.percent)
                .height(15.percent)
                .border(width: 1.vp)

              // Set horizontal alignment of child elements
                Text("justifyContent(End)")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
                Row() {
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0xAFEEEE)
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0x00FFFF)
                }
                .height(15.percent)
                .width(90.percent)
                .border(width: 1.vp)
                .justifyContent(FlexAlign.End)

                Text("justifyContent(Center)")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
                Row() {
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0xAFEEEE)
                    Row()
                    .width(30.percent)
                    .height(50)
                    .backgroundColor(0x00FFFF)
                }
                .width(90.percent)
                .border(width: 1.vp)
                .justifyContent(FlexAlign.Center)
            }
            .width(100.percent)
            .padding(top: 5)
        }
}
```

![row](figures/row.jpg)