# Explicit Animation (animateTo)

Provides a global `animateTo` explicit animation interface to specify transition effects for state changes caused by closure code. Similar to [property animation](./cj-animation-animation.md), layout-based animations that change width/height will directly display the final state for content (e.g., text, [Canvas](./cj-canvas-drawing-canvas.md) content). To make content follow width/height changes, use the [renderFit](./cj-universal-attribute-renderfit.md) attribute configuration.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func animateTo(AnimateParam, VoidCallback)

```cangjie
public func animateTo(value: AnimateParam, event: VoidCallback): Unit
```

**Function:** Provides a global `animateTo` explicit animation interface to specify transition effects for state changes caused by closure code.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| animation | [AnimateParam](./cj-common-types.md#class-animateparam) | Yes | - | Parameters for setting animation effects. |
| callback | VoidCallback | Yes | - | The closure function specifying the animation. State changes within this closure will automatically trigger transition animations. |

## class ExpectedFrameRateRange

```cangjie
public class ExpectedFrameRateRange {
    public var min: Int32
    public var max: Int32
    public var expected: Int32
    public init(
        min!: Int32,
        max!: Int32,
        expected!: Int32
    )
}
```

**Function:** Sets the expected frame rate range for animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var expected

```cangjie
public var expected: Int32
```

**Function:** The expected frame rate value.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var max

```cangjie
public var max: Int32
```

**Function:** The maximum frame rate value.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var min

```cangjie
public var min: Int32
```

**Function:** The minimum frame rate value.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Int32, Int32, Int32)

```cangjie
public init(
    min!: Int32,
    max!: Int32,
    expected!: Int32
)
```

**Function:** Constructs an `ExpectedFrameRateRange` object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| min | Int32 | Yes | - | Minimum frame rate value. |
| max | Int32 | Yes | - | Maximum frame rate value. |
| expected | Int32 | Yes | - | Expected frame rate value. |

## Example Code

### Example 1 (Creating Animation on Component Appearance)

This example demonstrates creating an animation effect when a component appears via the `onAppear` method.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.ui_context.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class EntryView {
    @State var isShow: Bool = true
    @State var widthSize: Length = 250.vp
    @State var heightSize: Length = 100.vp
    @State var rotateAngle: Float32 = 0.0

    func build() {
        Column() {
            Button("change size")
                .width(this.widthSize)
                .height(this.heightSize)
                .margin(30)
                .onClick(
                    {
                       evt =>
                        if (this.isShow) {
                            getUIContext().animateTo(
                                AnimateParam(
                                    duration: 2000,
                                    curve: Curve.EaseOut,
                                    iterations: 3,
                                    playMode: PlayMode.Normal,
                                    onFinish: {=> Hilog.info(0, "cangjie", "play end")}
                                ),
                                {
                                    =>
                                    this.widthSize = 150.vp
                                    this.heightSize = 60.vp
                                }
                            )
                        } else {
                            getUIContext().animateTo(
                                AnimateParam(),
                                {
                                    =>
                                    this.widthSize = 250.vp
                                    this.heightSize = 100.vp
                                }
                            )
                        }
                        this.isShow = !this.isShow
                    }
                )
            Button("change rotate angle")
                .margin(50)
                .rotate(x: 0.0, y: 0.0, z: 1.0, angle: this.rotateAngle)
                .onClick(
                    {
                       evt => getUIContext().animateTo(
                            AnimateParam(
                                duration: 1200,
                                curve: Curve.Friction,
                                delay: 500,
                                iterations: -1, // -1 means infinite loop
                                playMode: PlayMode.Alternate,
                                onFinish: {=> Hilog.info(0, "cangjie", "play end")},
                                expectedFrameRateRange: ExpectedFrameRateRange(
                                    min: 10,
                                    max: 120,
                                    expected: 60,
                                )
                            ),
                            {=> this.rotateAngle = 90.0}
                        )
                    })
        }
        .width(100.percent)
        .margin(top: 5)
    }
}
```

![animate](figures/animate.gif)

### Example 2 (Component Disappears After Animation Completion)

This example demonstrates how to make a component disappear after the animation completes.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.ui_context.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var isShow: Bool = true
    @State var heightSize: Length = 100.vp
    @State var count: Int = 0
    @State var isToBottom: Bool = true

    func build() {
        Column() {
            if (this.isShow) {
                Column()
                    .margin(50)
                    .width(200)
                    .height(this.heightSize)
                    .backgroundColor(Color.Blue)
                    .onClick(
                        {
                            evt => getUIContext().animateTo(
                                AnimateParam(
                                    duration: 2000,
                                    curve: Curve.EaseOut,
                                    iterations: 1,
                                    playMode: PlayMode.Normal,
                                    onFinish: {
                                        =>
                                        this.count--
                                        if (this.count == 0 && !this.isToBottom) {
                                            this.isShow = false
                                        }
                                    },
                                ),
                                {
                                    =>
                                    this.count++
                                    if (this.isToBottom) {
                                        this.heightSize = 60
                                    } else {
                                        this.heightSize = 100
                                    }
                                    this.isToBottom = !this.isToBottom
                                }
                            )
                        })
            }
        }
        .width(100.percent)
        .margin(top: 5)
        .justifyContent(FlexAlign.End)
    }
}
```

![animate2](figures/animate2.gif)