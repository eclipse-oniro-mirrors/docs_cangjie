# DataPanel

A data panel component used to display multiple data proportions using proportion charts.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(Array\<Float64>, Float64, DataPanelType)

```cangjie
public init(values!: Array<Float64>, max!: Float64 = 100.0, panelType!: DataPanelType = DataPanelType.Circle)
```

**Function:** Creates a data panel component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| values | Array\<Float64> | Yes | - | **Named parameter.** List of data values, containing up to 9 data points. If more than 9 data points are provided, only the first 9 will be used. If a data value is less than 0, it will be set to 0. |
| max | Float64 | No | 100.0 | **Named parameter.** <br> - If max > 0, it represents the maximum value of the data. <br> - If max ≤ 0, max equals the sum of all values in the array, displayed proportionally. |
| panelType | [DataPanelType](./cj-information-display-datapanel.md#enum-datapaneltype) | No | DataPanelType.Circle | **Named parameter.** The type of the data panel (dynamic modification is not supported). |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func closeEffect(Bool)

```cangjie
public func closeEffect(value: Bool): This
```

**Function:** Disables the rotation animation and shadow effect of the data proportion chart.

> **Note:**
>
> If the [trackShadow attribute](#func-trackshadowdatapanelshadowoptions) is not set, this attribute controls the shadow effect's toggle, with the default shadow effect enabled. If the trackShadow attribute is set, the shadow effect's toggle is controlled by the trackShadow attribute value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Disables the rotation animation and shadow effect of the data proportion chart.<br>Initial value: false, where false means disabled and true means enabled. |

### func strokeWidth(Length)

```cangjie
public func strokeWidth(value: Length): This
```

**Function:** Sets the thickness of the ring based on Length.

> **Note:**
>
> This attribute does not take effect when the data panel type is DataPanelType.Line.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The thickness of the ring.<br>Initial value: 24.vp.<br>Unit: vp.<br>If a value less than 0 is set, the default value will be displayed. |

### func trackBackgroundColor(ResourceColor)

```cangjie
public func trackBackgroundColor(value: ResourceColor): This
```

**Function:** Sets the background color of the track.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The background color of the track.<br>Initial value: 0x08182431. |

### func trackShadow(DataPanelShadowOptions)

```cangjie
public func trackShadow(value: DataPanelShadowOptions): This
```

**Function:** Sets the shadow style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [DataPanelShadowOptions](#class-datapanelshadowoptions) | Yes | - | The shadow style.<br>If not set, the shadow is disabled by default. |

### func valueColors(Array\<LinearGradient>)

```cangjie
public func valueColors(value: Array<LinearGradient>): This
```

**Function:** Sets the colors of each data segment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[LinearGradient](#class-lineargradient)> | Yes | - | The colors of each data segment, where ResourceColor represents a solid color and LinearGradient represents a gradient color. |

## Basic Type Definitions

### class ColorStop

```cangjie
public class ColorStop {
    public var color: ResourceColor
    public var offset: Length
    public init(color: ResourceColor, offset: Length)
}
```

**Function:** The color stop type, used to describe gradient color stops.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var color

```cangjie
public var color: ResourceColor
```

**Function:** The color value.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var offset

```cangjie
public var offset: Length
```

**Function:** The gradient color stop (a proportional value between 0 and 1; if the value is less than 0, it is set to 0; if the value is greater than 1, it is set to 1).

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(ResourceColor, Length)

```cangjie
public init(color: ResourceColor, offset: Length)
```

**Function:** Creates a ColorStop object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The color value. |
| offset | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The gradient color stop (a proportional value between 0 and 1; if the value is less than 0, it is set to 0; if the value is greater than 1, it is set to 1). |

### class DataPanelShadowOptions

```cangjie
public class DataPanelShadowOptions <: MultiShadowOptions {
    public var colors: Array<LinearGradient>
    public init(radius!: Length = 20.vp, colors!: Array<LinearGradient> = [], offsetX!: Length = 5.vp, offsetY!: Length = 5.vp)
}
```

**Function:** The shadow style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- [MultiShadowOptions](./cj-information-display-datapanel.md#class-multishadowoptions)

#### var colors

```cangjie
public var colors: Array<LinearGradient>
```

**Function:** The shadow colors for each data segment.

> **Note:**
>
> - If the number of shadow colors set is less than the number of data segments, the number of shadow colors displayed will match the number of shadow colors set.
> - If the number of shadow colors set is greater than the number of data segments, the number of shadow colors displayed will match the number of data segments.

**Type:** Array\<[LinearGradient](#class-lineargradient)>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Length, Array\<LinearGradient>, Length, Length)

```cangjie
public init(radius!: Length = 20.vp, colors!: Array<LinearGradient> = [], offsetX!: Length = 5.vp, offsetY!: Length = 5.vp)
```

**Function:** Creates a DataPanelShadowOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| radius | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 20.vp | **Named parameter.** The blur radius of the shadow. |
| colors | Array\<[LinearGradient](#class-lineargradient)> | No | [] | **Named parameter.** The shadow colors for each data segment.<br>If the number of shadow colors set is less than the number of data segments, the number of shadow colors displayed will match the number of shadow colors set.<br>If the number of shadow colors set is greater than the number of data segments, the number of shadow colors displayed will match the number of data segments. |
| offsetX | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 5.vp | **Named parameter.** The horizontal offset of the shadow. |
| offsetY | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 5.vp | **Named parameter.** The vertical offset of the shadow. |

### class LinearGradient

```cangjie
public class LinearGradient {
    public init(colorStops: Array<ColorStop>)
    public init(color: ResourceColor)
}
```

**Function:** Describes a linear gradient color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Array\<ColorStop>)

```cangjie
public init(colorStops: Array<ColorStop>)
```

**Function:** Describes a gradient color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| colorStops | Array\<[ColorStop](#class-colorstop)> | Yes | - | Stores the gradient colors and stops. |

#### init(ResourceColor)

```cangjie
public init(color: ResourceColor)
```

**Function:** Describes a gradient color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | A single gradient color. |

## class MultiShadowOptions

```cangjie
public open class MultiShadowOptions {
    public var radius: Length = 20.vp
    public var offsetX: Length = 5.vp
    public var offsetY: Length = 5.vp
}
```

**Function:** Multi-shadow options.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var offsetX

```cangjie
public var offsetX: Length = 5.vp
```

**Function:** Sets the horizontal offset of the shadow.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var offsetY

```cangjie
public var offsetY: Length = 5.vp
```

**Function:** Sets the vertical offset of the shadow.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var radius

```cangjie
public var radius: Length = 20.vp
```

**Function:** Sets the blur radius of the shadow.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## enum DataPanelType

```cangjie
public enum DataPanelType <: Equatable<DataPanelType> {
    | Circle
    | Line
    | ...
}
```

**Function:** The type of the data panel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- Equatable\<DataPanelType>

### Circle

```cangjie
Circle
```

**Function:** A circular data panel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Line

```cangjie
Line
```

**Function:** A linear data panel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### func !=(DataPanelType)

```cangjie
public operator func !=(other: DataPanelType): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DataPanelType](#enum-datapaneltype) | Yes | - | The enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal; otherwise, returns false. |

### func ==(DataPanelType)

```cangjie
public operator func ==(other: DataPanelType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DataPanelType](#enum-datapaneltype) | Yes | - | The enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal; otherwise, returns false. |## Sample Code

### Example 1 (Setting Data Panel Type)

This example demonstrates how to set the type of a data panel using the `type` attribute.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var valueArr: Array<Float64> = [10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0, 10.0]
    func build() {
        Column {
            Row() {
                Stack() {
                    DataPanel(values: [30.0], max: 100.0, panelType: DataPanelType.Circle).width(168).height(168)
                    Column() {
                        Text("30")
                            .fontSize(35)
                            .fontColor(0x182431)
                        Text("1.0.0")
                            .fontSize(9.33)
                            .lineHeight(12.83)
                            .fontWeight(FontWeight.W500)
                            .opacity(0.6)
                    }
                    Text("%")
                        .fontSize(9.33)
                        .lineHeight(12.83)
                        .fontWeight(FontWeight.W500)
                        .opacity(0.6)
                        .position(x: 104.42, y: 78.17)
                }.margin(right: 44)
                Stack() {
                    DataPanel(values: [50.0, 12.0, 8.0, 5.0], max: 100.0, panelType: DataPanelType.Circle)
                        .width(168)
                        .height(168)
                    Column() {
                        Text("75")
                            .fontSize(35)
                            .fontColor(0x182431)
                        Text("Used 98GB/128GB")
                            .fontSize(8.17)
                            .lineHeight(11.08)
                            .fontWeight(FontWeight.W500)
                            .opacity(0.6)
                    }
                    Text("%")
                        .fontSize(9.33)
                        .lineHeight(12.83)
                        .fontWeight(FontWeight.W500)
                        .opacity(0.6)
                        .position(x: 104.42, y: 78.17)
                }
            }
                .margin(bottom: 59)
            DataPanel(values: this.valueArr, max: 100.0, panelType: DataPanelType.Line)
                .width(300)
                .height(10)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

### Example 2 (Setting Gradient Colors and Shadows)

This example demonstrates how to set gradient color effects and shadow effects using the `valueColors` and `trackShadow` interfaces with `LinearGradient`.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var values1: Array<Float64> = [20.0, 20.0, 20.0, 20.0]
    var color1: LinearGradient = LinearGradient([ColorStop(0x65EEC9A3, 0), ColorStop(0xFFEF629F, 1)])
    var color2: LinearGradient = LinearGradient([ColorStop(0xFF67F9D4, 0), ColorStop(0xFFFF9554, 1)])
    var colorShadow1: LinearGradient = LinearGradient([ColorStop(0x65EEC9A3, 0), ColorStop(0x65EF629F, 1)])
    var colorShadow2: LinearGradient = LinearGradient([ColorStop(0x65e26709, 0), ColorStop(0x65efbd08, 1)])
    var colorShadow3: LinearGradient = LinearGradient([ColorStop(0x6572B513, 0), ColorStop(0x6508efa6, 1)])
    var colorShadow4: LinearGradient = LinearGradient([ColorStop(0x65ed08f5, 0), ColorStop(0x65ef0849, 1)])
    var color3: LinearGradient = LinearGradient(0x00FF00)
    var color4: LinearGradient = LinearGradient(0x20FF0000)
    @State var bgColor: UInt32 = 0x08182431
    @State var offsetX: Int64 = 15
    @State var offsetY: Int64 = 15
    @State var radius: Int64 = 5
    @State var colorArray: Array<LinearGradient> = [this.color1, this.color2, this.color3, this.color4]
    @State var shadowColorArray: Array<LinearGradient> = [this.colorShadow1, this.colorShadow2, this.colorShadow3,this.colorShadow4]
    func build() {
        Column {
            Text("LinearGradient")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .textAlign(TextAlign.Start)
                .width(100.percent)
                .margin(top: 20, left: 20)
            DataPanel(values: this.values1, max: 100.0, panelType: DataPanelType.Circle)
                .width(300)
                .height(300).
                valueColors(this.colorArray)
                .trackShadow(
                DataPanelShadowOptions(
                    radius: this.radius,
                    colors: this.shadowColorArray,
                    offsetX: this.offsetX,
                    offsetY: this.offsetY
                )
            )
                .strokeWidth(30)
                .trackBackgroundColor(this.bgColor)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![LinearGradientDataPanel](./figures/LinearGradientDataPanel.png)

### Example 3 (Disabling Animation and Shadows)

This example demonstrates how to disable data panel animations and shadows using the `closeEffect` interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var values1: Array<Float64> = [20.0, 20.0, 20.0, 20.0]
    var color1: LinearGradient = LinearGradient([ColorStop(0x65EEC9A3, 0), ColorStop(0xFFEF629F, 1)])
    var color2: LinearGradient = LinearGradient([ColorStop(0xFF67F9D4, 0), ColorStop(0xFFFF9554, 1)])
    var colorShadow1: LinearGradient = LinearGradient([ColorStop(0x65EEC9A3, 0), ColorStop(0x65EF629F, 1)])
    var colorShadow2: LinearGradient = LinearGradient([ColorStop(0x65e26709, 0), ColorStop(0x65efbd08, 1)])
    var colorShadow3: LinearGradient = LinearGradient([ColorStop(0x6572B513, 0), ColorStop(0x6508efa6, 1)])
    var colorShadow4: LinearGradient = LinearGradient([ColorStop(0x65ed08f5, 0), ColorStop(0x65ef0849, 1)])
    var color3: LinearGradient = LinearGradient(0x00FF00)
    var color4: LinearGradient = LinearGradient(0x20FF0000)
    @State var bgColor: UInt32 = 0x08182431
    @State var offsetX: Int64 = 15
    @State var offsetY: Int64 = 15
    @State var radius: Int64 = 5
    @State var colorArray: Array<LinearGradient> = [this.color1, this.color2, this.color3, this.color4]
    @State var shadowColorArray: Array<LinearGradient> = [this.colorShadow1, this.colorShadow2, this.colorShadow3,this.colorShadow4]
    func build() {
        Column {
            Text("LinearGradient")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .textAlign(TextAlign.Start)
                .width(100.percent)
                .margin(top: 20, left: 20)
            DataPanel(values: this.values1, max: 100.0, panelType: DataPanelType.Circle)
                .width(300)
                .height(300).
                valueColors(this.colorArray)
                .strokeWidth(30)
                .closeEffect(true)
                .trackBackgroundColor(this.bgColor)
        }
            .width(100.percent)
            .margin(top: 5)
    }
}
```

![LinearGradientDataPanel1](./figures/LinearGradientDataPanel1.png)