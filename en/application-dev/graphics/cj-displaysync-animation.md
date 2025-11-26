# Requesting Animation Frame Rate

In application development, [Property Animation](../reference/arkui-cj/cj-animation-animation.md) and [Explicit Animation](../reference/arkui-cj/cj-apis-uicontext-uicontext.md) can use the optional parameter [ExpectedFrameRateRange](../reference/arkui-cj/cj-common-types.md#var-expectedframeraterange) to configure different expected frame rates for various animations.

## Requesting Frame Rate for Property Animation

Defining a property animation for a text component with a requested frame rate of 60, example as follows:

<!-- compile -->

```cangjie
import kit.ArkUI.*

let animateOpt1 = AnimateParam(
    duration: 1200,
    iterations: 10,
    expectedFrameRateRange: ExpectedFrameRateRange( // Set frame rate range for property animation
        min: 0, // Set frame rate range
        max: 120, // Set frame rate range
        expected: 60 // Set expected animation frame rate to 60hz
    )
)

@Entry
@Component
class EntryView {
    @State
    var message: String = "Hello World"
    func build() {
        Row {
            Column {
                Text(this.message)
                    .animationStart(animateOpt1)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick ({ evt => this.message = "Hello Cangjie"
                    })
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

## Requesting Frame Rate for Explicit Animation

Defining an explicit animation for a button component with a requested frame rate of 30, example as follows:

<!-- compile -->

```cangjie
import ohos.arkui.ui_context.*
import kit.ArkUI.*

@Entry
@Component
class EntryView {
    @State
    var rotateAngle: Float32 = 0.0
    @State
    var message: String = "Hello World"
    func build() {
        Row {
            Column {
                Text(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick ({
                        evt => getUIContext().animateTo(
                            AnimateParam(
                                duration: 1200,
                                iterations: 10,
                                expectedFrameRateRange: ExpectedFrameRateRange( // Set frame rate range for property animation
                                    min: 0, // Set frame rate range
                                    max: 120, // Set frame rate range
                                    expected: 30 // Set expected animation frame rate to 30hz
                                )
                            ),
                            {=> this.rotateAngle = 90.0}
                        )
                    })
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

## Complete Example

<!-- compile -->

```cangjie
import kit.ArkUI.*
import ohos.arkui.ui_context.*

let animateOpt1 = AnimateParam(
    duration: 1200,
    iterations: 10,
    expectedFrameRateRange: ExpectedFrameRateRange( // Set frame rate range for property animation
        min: 0, // Set frame rate range
        max: 120, // Set frame rate range
        expected: 60 // Set expected animation frame rate to 60hz
    )
)

@Entry
@Component
class EntryView {
    @State
    var isAnimation: Bool = false
    @State
    var translateX1: Int64 = -100
    @State
    var translateX2: Int64 = -100
    @State
    var translateX3: Int64 = -100
    func build() {
        Column {
            Row {
                Text('30')
                    .fontWeight(FontWeight.Bold)
                    .fontSize(16)
                    .fontColor(Color.White)
                    .textAlign(TextAlign.Center)
                    .borderRadius(10)
                    .backgroundColor(0xF56C6C)
                    .width(80)
                    .height(80)
                    .translate(x: translateX1)
            }.height(20.percent)
            Row() {
                Text('40')
                    .fontWeight(FontWeight.Bold)
                    .fontSize(16)
                    .fontColor(Color.White)
                    .textAlign(TextAlign.Center)
                    .borderRadius(10)
                    .backgroundColor(0x2E8B57)
                    .width(80)
                    .height(80)
                    .translate(x: translateX2)
            }.height(20.percent)
            Row() {
                Text('60')
                    .fontWeight(FontWeight.Bold)
                    .fontSize(16)
                    .fontColor(Color.White)
                    .textAlign(TextAlign.Center)
                    .borderRadius(10)
                    .backgroundColor(0x008B8B)
                    .width(80)
                    .height(80)
                    .translate(x: translateX3)
                    .animationStart(animateOpt1)
            }.height(20.percent)
            Row() {
                Button('Start')
                    .id('PropertyAnimationStart')
                    .fontSize(14)
                    .fontWeight(FontWeight.W500)
                    .margin(bottom: 10, left: 5)
                    .fontColor(Color.White)
                    .onClick(
                        {
                            evt =>
                            this.isAnimation = !this.isAnimation
                            if (this.isAnimation) {
                                let translateX3 = 100
                            } else {
                                let translateX3 = -100
                            }
                            getUIContext().animateTo(
                                AnimateParam(
                                    duration: 1200,
                                    iterations: 10,
                                    playMode: PlayMode.AlternateReverse,
                                    expectedFrameRateRange: ExpectedFrameRateRange( // Set frame rate range for property animation
                                        min: 0, // Set frame rate range
                                        max: 120, // Set frame rate range
                                        expected: 40 // Set expected animation frame rate to 30hz
                                    )
                                ),
                                {
                                    => if (this.isAnimation) {
                                        let translateX3 = 100
                                    } else {
                                        let translateX3 = -100
                                    }
                                }
                            )
                        }
                    )
                    .width(40.percent)
                    .height(40)
                    .shadow(radius: 10.0, color: Color(0x909399), offsetX: 1.0, offsetY: 1.0)
            }
                .width(100.percent)
                .justifyContent(FlexAlign.Center)
                .shadow(radius: 10.0, color: Color(0x909399), offsetX: 1.0, offsetY: 1.0)
                .alignItems(VerticalAlign.Bottom)
                .layoutWeight(1)
        }
            .width(100.percent)
            .justifyContent(FlexAlign.Center)
            .shadow(radius: 10.0, color: Color(0x909399), offsetX: 1.0, offsetY: 1.0)
            .layoutWeight(1)
    }
}
```