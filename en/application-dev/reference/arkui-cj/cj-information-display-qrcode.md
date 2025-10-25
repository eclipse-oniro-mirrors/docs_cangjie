# QRCode

A component for displaying a single QR code.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(ResourceStr)

```cangjie
public init(value: ResourceStr)
```

**Function:** Creates a component for displaying a single QR code.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | The content string of the QR code. Supports up to 512 characters. If exceeded, only the first 512 characters will be used. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: Supports [Click Event](./cj-universal-event-click.md#func-onclick), [Touch Event](./cj-universal-event-touch.md#func-ontouch).

## Component Attributes

### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the color of the QR code.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The color of the QR code.<br/>Initial value: 0xff000000, and does not change with system light/dark mode switching. |

### func contentOpacity(Float64)

```cangjie
public func contentOpacity(value: Float64): This
```

**Function:** Sets the opacity of the QR code content color. The minimum opacity is 0.0, and the maximum is 1.0.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | The opacity of the QR code content color.<br/>Initial value: 1.0<br/>Valid range: [0.0, 1.0]. Values outside this range will be treated as the initial value. |

### func contentOpacity(AppResource)

```cangjie
public func contentOpacity(value: AppResource): This
```

**Function:** Sets the opacity of the QR code content color. The minimum opacity is 0, and the maximum is 1.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [AppResource](./cj-common-types.md#class-appresource) | Yes | - | The opacity of the QR code content color. |

## Example Code

This example demonstrates the basic usage of the QRCode component, including setting the QR code color via the `color` attribute, the background color via the `backgroundColor` attribute, and the opacity via the `contentOpacity` attribute.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    var value: String = "hello world";

    func build() {
        Scroll() {
            Column(space: 5) {
                Text("normal").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140)

                // Set QR code color
                Text("color").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).color(0xF7CE00).width(140).height(140)

                // Set QR code background color
                Text("backgroundColor").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140).backgroundColor(Color.Red)

                // Set QR code opacity
                Text("contentOpacity").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140).color(Color.Black).contentOpacity(0.1)

                // Set QR code opacity
                Text("contentOpacity").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140).color(Color.Black).contentOpacity(0.1)

                // Set QR code opacity
                Text("contentOpacity int").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140).color(Color.Black).contentOpacity(0.0)

                // Set QR code opacity
                Text("contentOpacity resource").fontSize(9).width(90.percent).fontColor(0xCCCCCC).fontSize(30)
                QRCode(this.value).width(140).height(140).color(Color.Black).contentOpacity(
                    @r(sys.float.alpha_40))
            }.width(100.percent).margin(top: 5)
        }
    }
}
```

![qrcode](figures/qrcode1.png)
![qrcode](figures/qrcode2.png)