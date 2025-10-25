# Rating

A component that provides the ability to select a rating within a given range.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Subcomponents

None

## Creating the Component

### init(Float64, Bool)

```cangjie
public init(rating!: Float64, indicator!: Bool = false)
```

**Function:** Constructs a component for selecting ratings within a specified range.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rating | Float64 | Yes | - | **Named parameter.** Sets and receives the rating value.<br>Initial value: 0.<br>Valid range: [0, stars]. Values below 0 are set to 0, and values above stars are set to the maximum value stars. |
| indicator | Bool | No | false | **Named parameter.** Sets the rating component to be used as an indicator, preventing rating changes.<br>Initial value: false, allowing ratings.<br>**Note:**<br>When indicator=true, the default component height is height=12.0.vp, and component width=height * stars. When indicator=false, the default component height is height=28.0.vp, and component width=height * stars. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func starStyle(ResourceStr, ResourceStr, ResourceStr)

```cangjie
public func starStyle(backgroundUri!: ResourceStr, foregroundUri!: ResourceStr, secondaryUri!: ResourceStr = backgroundUri): This
```

**Function:** Sets the style of the rating. The image types supported by this attribute refer to the [Image](./cj-image-video-image.md#image) component. Supports loading local and network images but does not currently support PixelMap type or Resource resources.

Default image loading is asynchronous; synchronous loading is not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| backgroundUri | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | **Named parameter.** The image link for unselected stars, which can be customized by the user or use the system default image. |
| foregroundUri | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | **Named parameter.** The image path for selected stars, which can be customized by the user or use the system default image. |
| secondaryUri | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | backgroundUri | **Named parameter.** The image path for partially selected stars, which can be customized by the user or use the system default image. |

> **Notes:**
>
> - backgroundUri: The image link for unselected stars, which can be customized by the user or use the system default image.
> - foregroundUri: The image path for selected stars, which can be customized by the user or use the system default image.
> - secondaryUri: The image path for partially selected stars, which can be customized by the user or use the system default image.
> - When the rating dimensions are [width, height], the drawing area for a single image is [width / stars, height].
> - To specify a square drawing area, it is recommended to set custom dimensions as [height * stars, height], where width = height * stars.
> - If the image path set for backgroundUri, foregroundUri, or secondaryUri is incorrect, the image will not be displayed.
> - If backgroundUri or foregroundUri is set to an empty string, the rating component will load the system default star image.
> - If secondaryUri is not set or is set to an empty string, it defaults to backgroundUri, effectively equivalent to only setting foregroundUri and backgroundUri.

### func stars(Int32)

```cangjie
public func stars(starCount: Int32): This
```

**Function:** Sets the total number of stars. If set to a value less than or equal to 0, the initial value is displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| starCount | Int32 | Yes | - | Sets the total number of stars.<br>Initial value: 5. |

### func stepSize(Float64)

```cangjie
public func stepSize(size: Float64): This
```

**Function:** Sets the step size for rating operations. If set to a value less than 0.1, the initial value is displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | Float64 | Yes | - | The step size for rating operations.<br>Initial value: 0.5.<br>Valid range: [0.1, stars]. |

## Component Events

### func onChange((Float64) -> Unit)

```cangjie
public func onChange(callback: (Float64) -> Unit): This
```

**Function:** Triggers this callback when the rating of the rating bar changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (Float64)->Unit | Yes | - | The rating of the rating bar. |

## Example Code

### Example 1 (Setting Default Rating Style)

This example creates a default star rating style.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
internal import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var rating: Float64 = 3.5

    func build() {
        Column() {
            Column() {
                Rating(rating: rating,indicator: false)
                  .stars(5)
                  .stepSize(0.5)
                  .margin(24)
                  .onChange({value: Float64 =>
                    this.rating = value
                    })
                Text("current score is ${this.rating}")
                    .fontSize(16)
                    .fontColor(0x182431)
                    .margin( 16 )
              }.width(360).height(113).backgroundColor(Color.White).margin(top: 68 )
            Row() {
                Image(@r(app.media.startIcon))
                    .width(40)
                    .height(40)
                    .borderRadius(20)
                    .margin(left: 24 )
                Column() {
                    Text("Cangjie")
                        .fontSize(16)
                        .fontColor(Color.Black)
                        .fontWeight(FontWeight.Bold)
                    Row() {
                        Rating(rating: 3.5, indicator: false ).margin(top: 1, right: 8 )
                        Text("2024/07/01")
                            .fontSize(10)
                            .fontColor(Color.Black)
                        }
                }.margin(left: 12 ).alignItems(HorizontalAlign.Start)

                Text("1st Floor")
                    .fontSize(10)
                    .fontColor(Color.Black)
                    .position( x: 295, y: 8 )
             }.width(360).height(56).backgroundColor(Color.White).margin(top: 64 )
        }.width(100.percent).height(100.percent)
    }
}
```

![rating](figures/rating2.gif)

### Example 2 (Setting Rating Style)

This example customizes the star image links by configuring starStyle.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var rating: Float64 = 3.5
    @State var backPng: String = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAAXNSR0IArs4c6QAAAj1JREFUSEu11UuojWEUBuDnOC5nIISSQoQyQRIZIRSiiHCKESMiBiTFDCEZSZmgTGRAuSYdQq6JxEQhl1JCkmukfOv0/adtt8/ePzpf7f6997/Wetda71rv16SLT1MXx9cZQA9MyeCv8RI/q5LphqEYRnucW/hRnXA1wEBsSgFXIr4X5yv2YC/i++5sM6DC5iOOYAfeFv9XAgzCFYzGtQSwH+/QC/OxGu8xHcvz8wQeJuDeyXZt/u9Z8p+Zq+5oUQS5jlGYgXs1uBmDU7myObhTw2Ys2lIybzAZ34oKNmMXVqWeHqpD/OBcXV9MwvMattswKDs5V9cXk/C8hu0yHMPWaFcB8Ai/MD4RfV0BENmvR7So1rmLnun9uADonicken5dCYAyJvuwAc0B0C9l86EoqYx3CZstqYJjqYKdqY0tARCfL5nA1hLOZUyCg1kxEAUH5zAxzfHwYL5MhDo2LXiBy2gNgCU4nojeVjjZ/p8AoVmjKCOCtgIgntcRczyVPP5HkNiVkIwHqYJpEaNyk2ODY7xCe2JJPv0lSOjSzbz5oWNPqwHi91ycyXMeJQb5ZU7/nPkQTM2JtvvVUtMVOJok4yrm4XMDhBC8C5iABTnBDpfO5HopDicn+6ns2XUqieCXMncRM+Hzx6l34USpJ7MqLkaoZOUZiYv5TliUhuN0rUob3WixF2cxAiFiRZDQrPO5xQsTd7c7a2MjgPDrk0Ut7oEDWRTX4EkiNmR7VT2OygCEf3Mie2OW87hcDuZb7XujESsL0ChOp++7HOA3UEo7FoJcFikAAAAASUVORK5CYII="
    @State var forePng: String = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAAAXNSR0IArs4c6QAAAcdJREFUSEu11b9LVXEYx/GXKWU4RGAN4RBESFNQkEQUBkrRkOHUUtQ/EARNtbZFlDgKDjU4SSFOOilCRZBISxTYELUUQUuUVnQeOScO955z77l0/E7nx/N83t/n++PzdNnm0bXN+soAOzGEbvzGM/wqmMwADrKl8xybjTGNgP24jWvYkwv+lLw/wCR+4gIe4nAu5gumcQ/xvDXygANYxqEWy/Yao9iLRUQFjeMtziIm9Q/Qm5Z4tMKevEshsXyxLPsKclZxMqrNKriDuxXEs5D3OJMAzmOqJO8W7meANxjsABChHxCVF1UQ/1/heAB6ine/Q1hR+AZ2BaAfn2sQLJLoCcAOfA9azZCPccqyPVhIT0adjMe4mgEuJ5s8U6c6TmMlA8SZfhG7XhNkCcONN/kIXiZXve8/Id9wAnGjm8xuDE8Kvldlhk+FTYQ5NnlR9u0KHlVVzMWF617CfD63zK5vJIY20QHkD64XTaxVw7oZXlJhuX4ktnAxddemObXraCOYw+6SatYxjrWyatkBIi9c82naA/I6ceLCTb+2WsoqgMiPtjibVHMsFYs7cw5xJFuOqoAQCdc9laqtpL26nX5p02+bWDXgL/kuQxxwPkE6AAAAAElFTkSuQmCC"

    func build() {
        Column() {
            Rating(rating: rating,indicator: false)
                .stars(5)
                .stepSize(0.5)
                .starStyle(
                    backgroundUri: backPng,
                    foregroundUri: forePng
                )
                .margin(24)
                .onChange({value: Float64 =>
                    this.rating = value
                })
            Text("current score is ${this.rating}")
                .fontSize(16)
                .fontColor(0x182431)
                .margin(16)
        }
        .width(100.percent)
        .padding(top: 5)
    }
}
```

![rating](figures/rating1.gif)