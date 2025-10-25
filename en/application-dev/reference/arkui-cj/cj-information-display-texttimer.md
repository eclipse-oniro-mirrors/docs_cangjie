# TextTimer

A component that displays timing information through text and controls its timer state.

Time changes will stop when the component is invisible. The visibility state of the component is based on [onVisibleAreaChange](./cj-universal-event-visibleareachange.md#func-onvisibleareachangearrayfloat64-bool-float64-unit) processing. A visibility threshold ratio greater than 0 is considered as the visible state.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Subcomponents

None

## Creating the Component

### init(Bool, Int64, TextTimerController)

```cangjie
public init(isCountDown!: Bool = false, count!: Int64 = 60000,
    controller!: TextTimerController = TextTimerController())
```

**Function:** Creates a TextTimer component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| isCountDown | Bool | No | false | **Named parameter.** Whether it is a countdown. When set to true, the timer starts counting down, e.g., from 30 seconds to 0 seconds. When set to false, the timer starts counting up, e.g., from 0 seconds to 30 seconds. |
| count | Int64 | No | 60000 | **Named parameter.** Timer duration (effective when isCountDown is true), in milliseconds. The maximum duration should not exceed 86400000 milliseconds (24 hours). When 0 < count < 86400000, the count value is used as the initial timer value. Otherwise, the default value is used as the initial timer value. |
| controller | [TextTimerController](#class-texttimercontroller) | No | TextTimerController() | **Named parameter.** TextTimer controller. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func fontColor(ResourceColor)

```cangjie
public func fontColor(value: ResourceColor): This
```

**Function:** Sets the font color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Font color. |

### func fontFamily(ResourceStr)

```cangjie
public func fontFamily(value: ResourceStr): This
```

**Function:** Sets the font list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Font list.<br/>Initial font: 'HarmonyOS Sans'.<br/>Currently supports 'HarmonyOS Sans' font and [registering custom fonts](./cj-text-input-text.md#registering-custom-fonts). |

### func fontSize(Length)

```cangjie
public func fontSize(value: Length): This
```

**Function:** Sets the font size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Font size. When fontSize is of type Int64 or Float64, the fp unit is used. The initial font size is 16.fp. Percentage settings are not supported. |

### func fontStyle(FontStyle)

```cangjie
public func fontStyle(value: FontStyle): This
```

**Function:** Sets the font style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [FontStyle](./cj-common-types.md#enum-fontstyle) | Yes | - | Font style.<br/>Initial value: FontStyle.Normal |

### func fontWeight(FontWeight)

```cangjie
public func fontWeight(value: FontWeight): This
```

**Function:** Sets the font weight of the text. Setting it too large may result in truncation with different fonts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [FontWeight](./cj-common-types.md#enum-fontweight) | Yes | - | Font weight of the text.<br/>Initial value: FontWeight.Normal |

### func format(String)

```cangjie
public func format(value: String): This
```

**Function:** Sets a custom format, which must include at least one of the keywords HH, mm, ss, or SS. If date formats like yy, MM, dd are used, the default value will be applied.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | Custom format.<br/>Initial value: 'HH:mm:ss.SS' |

### func textShadow(Array\<ShadowOptions>)

```cangjie
public func textShadow(value: Array<ShadowOptions>): This
```

**Function:** Sets the text shadow effect. This interface supports array-type parameters to achieve multiple text shadows. The fill field is not supported, and the intelligent color picking mode is not supported.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[ShadowOptions](./cj-common-types.md#interface-shadowoptions)> | Yes | - | Text shadow effect. |

### func textShadow(ShadowOptions)

```cangjie
public func textShadow(value: ShadowOptions): This
```

**Function:** Sets the text shadow effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ShadowOptions](./cj-common-types.md#interface-shadowoptions) | Yes | - | Text shadow effect. |

## Component Events

### func onTimer((Int64,Int64) -> Unit)

```cangjie
public func onTimer(event: (Int64, Int64) -> Unit): This
```

**Function:** Triggered when the time text changes. This event will not be triggered in locked screen or background states. When setting a high-precision format (SSS, SS), the callback interval may fluctuate.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | (Int64,Int64)->Unit | Yes | - | The first Int64 parameter is the Linux timestamp, i.e., the time elapsed since January 1, 1970, in the smallest unit of the set format.<br/>The second Int64 parameter is the elapsed time of the timer, in the smallest unit of the set format. |

## Basic Type Definitions

### class TextTimerController

```cangjie
public class TextTimerController {
    public init()
}
```

**Function:** The controller for the TextTimer component, used to control the text timer. A TextTimer component can only be bound to one controller. Related commands can only be called after the component is created.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init()

```cangjie
public init()
```

**Function:** Creates a TextTimerController object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func pause()

```cangjie
public func pause(): Unit
```

**Function:** Pauses the timer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func reset()

```cangjie
public func reset(): Unit
```

**Function:** Resets the timer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func start()

```cangjie
public func start(): Unit
```

**Function:** Starts the timer.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## Example Code

### Example 1 (Text Timer with Manual Start/Stop)

This example demonstrates the basic usage of the TextTimer component, setting the text display format of the timer via the format attribute.

Users can start, pause, and reset the timer by clicking the "start", "pause", and "reset" buttons.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var textTimerController: TextTimerController = TextTimerController()
    @State var format: String = 'mm:ss.SS'
    func build() {
        Column {
            TextTimer(isCountDown: true, count: 30000, controller: this.textTimerController)
                .format(this.format)
                .fontColor(Color.Black)
                .fontSize(50)
                .onTimer({utc, elapsedTime =>
                    Hilog.info(0, "AppLogCj", "time has been changed")
                })
            Row() {
                Button("start").onClick{ evt =>
                  this.textTimerController.start()
                }
                Button("pause").onClick{ evt =>
                  this.textTimerController.pause()
                }
                Button("reset").onClick{ evt =>
                    this.textTimerController.reset()
                }
            }
        }
    }
}

```

![texttimer](figures/texttimer.gif)

### Example 2 (Setting Text Shadow Style)

This example sets the text shadow style of the timer via the textShadow attribute.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var textShadows: Array<ShadowOptions> = [
        ShadowOptions(
            radius: 10.0,
            color: Color.Red,
            offsetX: 10.0,
            offsetY: 0.0
        ),
        ShadowOptions(
            radius: 10.0,
            color: Color.Black,
            offsetX: 20.0,
            offsetY: 0.0
        ),
        ShadowOptions(
            radius: 10.0,
            color: Color.Gray,
            offsetX: 30.0,
            offsetY: 0.0
        ),
        ShadowOptions(
        radius: 10.0,
        color: Color.Green,
        offsetX: 40.0,
        offsetY: 0.0
        ),
        ShadowOptions(
        radius: 10.0,
        color: Color.Blue,
        offsetX: 100.0,
        offsetY: 0.0
        )]
    func build() {
        Column(space: 8) {
            TextTimer().fontSize(50).textShadow(this.textShadows)
        }
    }
}
```

![texttimer](figures/texttimer2.png)

### Example 3 (Starting Timer Immediately After Creation)

This example demonstrates how the TextTimer starts timing immediately after creation.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var textTimerController: TextTimerController = TextTimerController()
    @State var format: String = 'mm:ss.SS'

    func build() {
        Column(space: 8) {
            Scroll().height(20.percent)
            Button("openTextTimer").onClick({
                evt =>

            })
            TextTimer( isCountDown: true, count: 30000, controller: this.textTimerController )
                .format(this.format)
                .fontColor(Color.Black)
                .fontSize(50)
                .onTimer({
                    utc: Int64, elapsedTime: Int64 =>
                        Hilog.info(0, "AppLogCj", 'textTimer notCountDown utc is：${utc.toString()}, elapsedTime: ${elapsedTime.toString()}')
                })
                .onAppear({ =>
                    this.textTimerController.start()
                })
        }
    }
}
```

![texttimer](figures/texttimer3.gif)
```