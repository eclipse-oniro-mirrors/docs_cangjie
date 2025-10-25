# Progress

A progress bar component used to display loading progress or operation processing status.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(Float64, Float64, ProgressType)

```cangjie
public init(value!: Float64, total!: Float64 = 100.0, progressType!: ProgressType = ProgressType.Linear)
```

**Function:** Creates a progress bar component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | **Named parameter.** Specifies the current progress value. Values less than 0 are set to 0.0, and values greater than total are set to total.<br/>Initial value: 0.0 |
| total | Float64 | No | 100.0 | **Named parameter.** Specifies the total length of the progress bar. Values less than or equal to 0 are set to 100.0. |
| progressType | [ProgressType](./cj-common-types.md#enum-progresstype) | No | ProgressType.Linear | Specifies the type of the progress bar. |

## Common Attributes/Common Events

Common Attributes: All supported.

> **Note:**
>
> This component overrides the common attribute backgroundColor. When added directly to the Progress component, it affects the background color of the progress bar. To set the background color of the entire Progress component, add backgroundColor to the outer container that wraps the Progress component.

Common Events: All supported.

## Component Attributes

### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the foreground color of the progress bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The foreground color of the progress bar.<br/>Initial value:<br/>- Capsule: '0x33007dff'<br/>- Ring: Start: '0xff86c1ff', End: '0xff254ff7'<br/>- Other styles: '0xff007dff' |

### func style(Length, Int32, Length)

```cangjie
public func style(strokeWidth!: Length = 10.vp, scaleCount!: Int32 = 120, scaleWidth!: Length = 2.vp): This
```

**Function:** Sets the style of the progress bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| strokeWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 10.vp | **Named parameter.** Sets the width of the progress bar (percentage values are not supported). |
| scaleCount | Int32 | No | 120 | **Named parameter.** Sets the total number of scale marks for the ring progress bar. |
| scaleWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 2.vp | **Named parameter.** Sets the thickness of the scale marks for the ring progress bar (percentage values are not supported). If the scale thickness exceeds the progress bar width, the system default thickness is used. |

### func style(RingStyleOptions)

```cangjie
public func style(value: RingStyleOptions): This
```

**Function:** Sets the style of the Ring progress bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [RingStyleOptions](#class-ringstyleoptions) | Yes | - | Sets the style of the Ring progress bar. |

### func value(Float64)

```cangjie
public func value(value: Float64): This
```

**Function:** Sets the current progress value. Values less than 0 are set to 0, and values greater than total are set to total. Invalid values have no effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Float64 | Yes | - | The current progress value.<br/>Initial value: 0 |

## Basic Type Definitions

### class RingStyleOptions

```cangjie
public class RingStyleOptions <: CommonProgressStyleOptions {
    public var strokeWidth: Length
    public var shadow: Bool
    public var status: ProgressStatus
    public var enableSmoothEffect: Bool
    public var enableScanEffect: Bool
    public init(strokeWidth!: Length = 4.vp, shadow!: Bool = false,
        status!: ProgressStatus = ProgressStatus.Progressing, enableSmoothEffect!: Bool = true,
        enableScanEffect!: Bool = false)
}
```

**Function:** Sets the style of the Ring progress bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [CommonProgressStyleOptions](./cj-common-types.md#class-commonprogressstyleoptions)

#### var enableScanEffect

```cangjie
public var enableScanEffect: Bool
```

**Function:** Toggles the scan light effect.

**Type:** Bool

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var enableSmoothEffect

```cangjie
public var enableSmoothEffect: Bool
```

**Function:** Toggles the smooth animation effect. When enabled, the progress transitions smoothly from the current value to the target value; otherwise, it changes abruptly.

**Type:** Bool

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var shadow

```cangjie
public var shadow: Bool
```

**Function:** Toggles the shadow effect of the progress bar.

**Type:** Bool

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var status

```cangjie
public var status: ProgressStatus
```

**Function:** Sets the status of the progress bar. When set to LOADING, the update check animation is enabled, and setting the progress value has no effect. When changed from LOADING to PROGRESSING, the update check animation completes before stopping.

**Type:** [ProgressStatus](#enum-progressstatus)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var strokeWidth

```cangjie
public var strokeWidth: Length
```

**Function:** Sets the width of the progress bar (percentage values are not supported).

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(Length, Bool, ProgressStatus, Bool, Bool)

```cangjie
public init(strokeWidth!: Length = 4.vp, shadow!: Bool = false,
    status!: ProgressStatus = ProgressStatus.Progressing, enableSmoothEffect!: Bool = true,
    enableScanEffect!: Bool = false)
```

**Function:** Creates a RingStyleOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| strokeWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 4.vp | **Named parameter.** Sets the width of the progress bar (percentage values are not supported). If the width is greater than or equal to the radius, it defaults to half the radius value. |
| shadow | Bool | No | false | **Named parameter.** Toggles the shadow effect of the progress bar. |
| status | [ProgressStatus](#enum-progressstatus) | No | ProgressStatus.Progressing | **Named parameter.** Sets the status of the progress bar. When set to LOADING, the update check animation is enabled, and setting the progress value has no effect. When changed from LOADING to PROGRESSING, the update check animation completes before stopping. |
| enableSmoothEffect | Bool | No | true | **Named parameter.** Toggles the smooth animation effect. When enabled, the progress transitions smoothly from the current value to the target value; otherwise, it changes abruptly. |
| enableScanEffect | Bool | No | false | **Named parameter.** Toggles the scan light effect. |

### enum ProgressStatus

```cangjie
public enum ProgressStatus {
    | Loading
    | Progressing
    | ...
}
```

**Function:** The status of the Progress component's progress bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Loading

```cangjie
Loading
```

**Function:** Loading status.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Progressing

```cangjie
Progressing
```

**Function:** Progress updating status.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## Example Code

### Example 1 (Setting the Progress Bar Type)

This example demonstrates setting the progress bar type using the type attribute.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let scaleStyle0 = RingStyleOptions(strokeWidth: 15.vp, enableSmoothEffect: true)
    let scaleStyle1 = RingStyleOptions(strokeWidth: 20.vp, enableSmoothEffect: true)
    let scaleStyle2 = RingStyleOptions(strokeWidth: 20.vp, enableSmoothEffect: true)
    let ringStyle = RingStyleOptions(strokeWidth: 20.vp)
    func build() {
        Column(space: 15) {
            Text("Linear Progress").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Progress(value: 10.0, progressType: ProgressType.Linear).width(200)
            Progress(value: 20.0, total: 150.0, progressType: ProgressType.Linear)
                .color(Color.Gray)
                .value(50.0)
                .width(200)

            Text("Eclipse Progress").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 10.0, progressType: ProgressType.Eclipse).width(100)
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.Eclipse)
                    .width(100)
                    .color(Color.Gray)
                    .value(50.0)
            }

            Text("ScaleRing Progress").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 10.0, progressType: ProgressType.ScaleRing).width(100)
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.ScaleRing)
                    .color(Color.Gray)
                    .value(50.0)
                    .width(100)
                    .style(scaleStyle0)
            }

            Row(space: 40) {
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.ScaleRing)
                    .color(Color.Gray)
                    .value(50.0)
                    .width(100)
                    .style(scaleStyle1)
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.ScaleRing)
                    .color(Color.Gray)
                    .value(50.0)
                    .width(100)
                    .style(scaleStyle2)
            }

            Text("Ring Progress").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 10.0, progressType: ProgressType.Ring).width(100)
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.Ring)
                    .color(Color.Gray)
                    .value(50.0)
                    .width(100)
                    .style(ringStyle)
            }

            Text("Capsule Progress").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 10.0, progressType: ProgressType.Capsule).width(100).height(50)
                Progress(value: 20.0, total: 150.0, progressType: ProgressType.Capsule)
                    .color(Color.Gray)
                    .value(50.0)
                    .width(100)
                    .height(50)
            }
        }
    }
}
```

![progress1](figures/progress1.jpg)

### Example 2 (Setting Ring Progress Bar Attributes)

This example demonstrates setting visual attributes of the ring progress bar using the strokeWidth and shadow properties of the style interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let ringStyle0 = RingStyleOptions(strokeWidth: 20.vp)
    let ringStyle1 = RingStyleOptions(strokeWidth: 20.vp, shadow: true)
    func build() {
        Column(space: 15) {
            Text("Gradient Color").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 70.0, progressType: ProgressType.Ring)
                    .width(100)
                    .style(ringStyle0)
                    .color(0X02fd03)
            }
            Text("Shadow").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 70.0, progressType: ProgressType.Ring).width(120).color(Color.Blue).style(ringStyle1)
            }
        }
    }
}
```

![progress2](figures/progress2.jpg)### Example 3 (Setting Circular Progress Bar Animation)

This example demonstrates the toggle functionality for circular progress bar animations through the `status` and `enableScanEffect` properties of the style interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*
import ohos.arkui.component.*
import ohos.base.*
import ohos.resource_manager.*

@Entry
@Component
class EntryView {
    let ringStyle0 = RingStyleOptions(strokeWidth: 20.vp, status: ProgressStatus.Loading)
    let ringStyle1 = RingStyleOptions(strokeWidth: 20.vp, enableScanEffect: true)
    func build() {
        Column(space: 15) {
            Text("Loading Effect").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 0.0, progressType: ProgressType.Ring).width(100).style(ringStyle0).color(Color.Blue)
            }
            Text("Shadow").fontSize(20).fontColor(0xCCCCCC).width(90.percent)
            Row(space: 40) {
                Progress(value: 30.0, progressType: ProgressType.Ring).width(100).color(0X02fd03).style(ringStyle1)
            }
        }
    }
}
```

![progress3](figures/progress3.gif)

### Example 4 (Setting Smooth Progress Animation)

This example demonstrates the toggle functionality for smooth progress animations through the `enableSmoothEffect` property of the style interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State
    var value: Float64 = 0.0

    func build() {
        Column(space: 10) {
            Text('enableSmoothEffect: true').fontSize(9).fontColor(0xCCCCCC).width(90.percent).margin(5).margin( top: 20 )
            Progress( value: this.value, total: 100.0, progressType: ProgressType.Linear ).style(RingStyleOptions(strokeWidth: 10, enableSmoothEffect: true ))
            Text('enableSmoothEffect: false').fontSize(9).fontColor(0xCCCCCC).width(90.percent).margin(5)
            Progress( value: this.value, total: 100.0, progressType: ProgressType.Linear ).style(RingStyleOptions(strokeWidth: 10, enableSmoothEffect: false ))
            Button('value +10')
                .onClick{ evt =>
                    this.value += 10.0
            }.width(75).height(15).fontSize(9)
        }.width(50.percent).height(100.percent).margin( left: 20 )
    }
}
```

![progress5](figures/progress5.gif)