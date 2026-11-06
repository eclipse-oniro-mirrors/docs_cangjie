# Custom Event Dispatch

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Before a touch event is triggered, ArkUI performs a [touch test](../../arkui-cj/cj-common-events-distribute.md#touch-testing) on the press point against the component area, collects the components that need to respond to the touch event, and then distributes the corresponding touch events based on the touch test result. On a parent node, you can use onChildTouchTest to determine the touch test mode of child nodes, affecting the touch testing of child components and thus the subsequent touch event distribution. For details about the effects, see the [TouchTestStrategy](#enum-touchteststrategy) enum description.

> **Note:**
>
> - The array of child node information contains only information about named nodes, that is, nodes for which the developer has set an id through the [id](./cj-universal-attribute-componentid.md#func-idstring) attribute.
> - After custom event dispatch, onClick and rotation/pinch gestures may fail to respond because the touch hot zone is not hit.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func onChildTouchTest(?(Array\<TouchTestInfo>) -> TouchResult)

```cangjie
func onChildTouchTest(callback: ?(Array<TouchTestInfo>) -> TouchResult): T
```

**Description:** Allows the current component to customize the touch test and control child component behavior during the test by setting a callback. The callback receives an array containing the touch test information of child nodes, and the array contains only information about named nodes (nodes with an id set through the id attribute). The callback returns a [TouchResult](#class-touchresult) to control the event dispatch strategy of child nodes. When callback is None, events are distributed according to the system default strategy.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | ?(Array\<[TouchTestInfo](#class-touchtestinfo)>) -> [TouchResult](#class-touchresult) | Yes | - | Callback function for customizing the touch test. It is called on each touch test. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## class ComponentRect

```cangjie
public class ComponentRect {
    public var x: Float64
    public var y: Float64
    public var width: Float64
    public var height: Float64
}
```

**Description:** Describes the position, width, and height of a component. Objects of this class are created by the framework and returned in the rect field of [TouchTestInfo](#class-touchtestinfo). Developers do not need to construct such objects.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var x

```cangjie
public var x: Float64
```

**Description:** Horizontal coordinate.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var y

```cangjie
public var y: Float64
```

**Description:** Vertical coordinate.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var width

```cangjie
public var width: Float64
```

**Description:** Content width.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var height

```cangjie
public var height: Float64
```

**Description:** Content height.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

## class TouchResult

```cangjie
public class TouchResult {
    public var strategy: TouchTestStrategy
    public var id: ?String
    public init(strategy: TouchTestStrategy, id!: ?String = None)
}
```

**Description:** Custom event dispatch result. Developers affect event dispatch by returning this result.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var strategy

```cangjie
public var strategy: TouchTestStrategy
```

**Description:** Event dispatch strategy.

**Type:** [TouchTestStrategy](#enum-touchteststrategy)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var id

```cangjie
public var id: ?String
```

**Description:** Unique ID of the child component. When strategy is TouchTestStrategy.Default, id is optional; when strategy is TouchTestStrategy.ForwardCompetition or TouchTestStrategy.Forward, id is mandatory (if id is not returned, the event dispatch is processed as TouchTestStrategy.Default).

**Type:** ?String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### init(TouchTestStrategy, ?String)

```cangjie
public init(strategy: TouchTestStrategy, id!: ?String = None)
```

**Description:** Constructs a TouchResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| strategy | [TouchTestStrategy](#enum-touchteststrategy) | Yes | - | Event dispatch strategy. |
| id | ?String | No | None | **Named parameter.** Unique ID of the child component. |

## class TouchTestInfo

```cangjie
public class TouchTestInfo {
    public var windowX: Float64
    public var windowY: Float64
    public var parentX: Float64
    public var parentY: Float64
    public var x: Float64
    public var y: Float64
    public var rect: ComponentRect
    public var id: String
}
```

**Description:** Coordinates of the current touch point relative to the window, parent component, and child component, as well as the ID, position, and size information of the child component. Objects of this class are created by the framework and passed to the developer in the [onChildTouchTest](#func-onchildtouchtestarraytouchtestinfo---touchresult) callback.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var windowX

```cangjie
public var windowX: Float64
```

**Description:** X-coordinate of the touch point relative to the upper left corner of the window.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var windowY

```cangjie
public var windowY: Float64
```

**Description:** Y-coordinate of the touch point relative to the upper left corner of the window.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var parentX

```cangjie
public var parentX: Float64
```

**Description:** X-coordinate of the touch point relative to the upper left corner of the parent component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var parentY

```cangjie
public var parentY: Float64
```

**Description:** Y-coordinate of the touch point relative to the upper left corner of the parent component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var x

```cangjie
public var x: Float64
```

**Description:** X-coordinate of the touch point relative to the upper left corner of the child component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var y

```cangjie
public var y: Float64
```

**Description:** Y-coordinate of the touch point relative to the upper left corner of the child component.

**Type:** Float64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var rect

```cangjie
public var rect: ComponentRect
```

**Description:** Position, width, and height of the child component.

**Type:** [ComponentRect](#class-componentrect)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### var id

```cangjie
public var id: String
```

**Description:** Unique ID of the child component.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

## enum TouchTestStrategy

```cangjie
public enum TouchTestStrategy <: Equatable<TouchTestStrategy> {
    | Default
    | ForwardCompetition
    | Forward
    | ...
}
```

**Description:** Event dispatch strategy.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parent Type:**

- Equatable\<[TouchTestStrategy](#enum-touchteststrategy)>

### Default

```cangjie
Default
```

**Description:** Custom dispatch has no effect; the system dispatches events based on the hit status of the current node.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### ForwardCompetition

```cangjie
ForwardCompetition
```

**Description:** The application specifies dispatching events to a child node, and the system decides whether to continue dispatching events to other sibling nodes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### Forward

```cangjie
Forward
```

**Description:** The application specifies dispatching events to a child node, and the system no longer dispatches events to other sibling nodes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

### operator func ==(TouchTestStrategy)

```cangjie
public operator func ==(other: TouchTestStrategy): Bool
```

**Description:** Determines whether two TouchTestStrategy enums are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TouchTestStrategy](#enum-touchteststrategy) | Yes | - | The other TouchTestStrategy enum to compare. |

**Return Value:**

| Type | Description |
|:---|:---|
| Bool | Returns true if the two enums are equal, otherwise returns false. |

### operator func !=(TouchTestStrategy)

```cangjie
public operator func !=(other: TouchTestStrategy): Bool
```

**Description:** Determines whether two TouchTestStrategy enums are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [TouchTestStrategy](#enum-touchteststrategy) | Yes | - | The other TouchTestStrategy enum to compare. |

**Return Value:**

| Type | Description |
|:---|:---|
| Bool | Returns true if the two enums are not equal, otherwise returns false. |

## Sample Code

### Example 1 (Setting the Event Dispatch Strategy to ForwardCompetition)

In this example, click the blank area below the List and drag to make the List scroll. When the Button is pressed, the Button responds to the onClick event.

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
    let arr: Array<Int64> = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    @State
    var text: String = 'Button'

    func build() {
        Column {
            List(space: 12, initialIndex: 0) {
                ForEach(this.arr, itemGeneratorFunc: {
                    item: Int64, _: Int64 =>
                        ListItem {
                            Text('Item ' + item.toString())
                                .width(100.percent)
                                .height(56)
                                .fontSize(16)
                                .textAlign(TextAlign.Start)
                        }
                            .borderRadius(24)
                            .backgroundColor(Color.White)
                            .padding(left: 12, right: 12)
                }, keyGeneratorFunc: {
                    item: Int64, _: Int64 => item.toString()
                })
            }
                .listDirection(Axis.Vertical)
                .scrollBar(BarState.Off)
                .edgeEffect(EdgeEffect.Spring)
                .onScrollIndex({
                    firstIndex: Int32, lastIndex: Int32, _: Int32 =>
                        Hilog.info(0, 'cangjie', "first ${firstIndex}")
                        Hilog.info(0, 'cangjie', "last ${lastIndex}")
                })
                .onDidScroll({
                    scrollOffset: Float64, scrollState: ScrollState =>
                        let stateStr = match (scrollState) {
                            case ScrollState.Idle => "Idle"
                            case ScrollState.Scroll => "Scroll"
                            case ScrollState.Fling => "Fling"
                            case _ => ""
                        }
                        Hilog.info(0, 'cangjie', "onScroll scrollState = ScrollState ${stateStr}, scrollOffset = ${scrollOffset}")
                })
                .width(100.percent)
                .height(70.percent)
                .id('MyList')

            Button(this.text)
                .width(312)
                .height(40)
                .id('MyButton')
                .fontSize(16)
                .fontWeight(FontWeight.Medium)
                .margin(top: 80)
                .onClick({ _ =>
                    this.text = 'click the button'
                    getUIContext()
                        .getPromptAction()
                        .showToast(
                            ShowToastOptions(
                                message: 'you click the button.',
                                duration: 3000
                            )
                        )
                })
        }
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xF1F3F5)
            .justifyContent(FlexAlign.End)
            .padding(left: 12, right: 12, bottom: 24)
            .onChildTouchTest({ touchInfo: Array<TouchTestInfo> =>
                for (info in touchInfo) {
                    if (info.id == 'MyList') {
                        return TouchResult(TouchTestStrategy.ForwardCompetition, id: info.id)
                    }
                }
                return TouchResult(TouchTestStrategy.Default)
            })
    }
}
```

![onchildtouchtest](figures/on-child-touch-test-competition.gif)

### Example 2 (Setting the Event Dispatch Strategy to Forward)

In this example, clicking and dragging in the blank area below the **List** component causes the **List** component to scroll. The **Button** component does not respond to **onClick** events.

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
    let arr: Array<Int64> = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    @State
    var text: String = 'Button'

    func build() {
        Column {
            List(space: 12, initialIndex: 0) {
                ForEach(this.arr, itemGeneratorFunc: {
                    item: Int64, _: Int64 =>
                        ListItem {
                            Text('Item ' + item.toString())
                                .width(100.percent)
                                .height(56)
                                .fontSize(16)
                                .textAlign(TextAlign.Start)
                        }
                            .borderRadius(24)
                            .backgroundColor(Color.White)
                            .padding(left: 12, right: 12)
                }, keyGeneratorFunc: {
                    item: Int64, _: Int64 => item.toString()
                })
            }
                .listDirection(Axis.Vertical)
                .scrollBar(BarState.Off)
                .edgeEffect(EdgeEffect.Spring)
                .onScrollIndex({
                    firstIndex: Int32, lastIndex: Int32, _: Int32 =>
                        Hilog.info(0, 'cangjie', "first ${firstIndex}")
                        Hilog.info(0, 'cangjie', "last ${lastIndex}")
                })
                .onDidScroll({
                    scrollOffset: Float64, scrollState: ScrollState =>
                        let stateStr = match (scrollState) {
                            case ScrollState.Idle => "Idle"
                            case ScrollState.Scroll => "Scroll"
                            case ScrollState.Fling => "Fling"
                            case _ => ""
                        }
                        Hilog.info(0, 'cangjie', "onScroll scrollState = ScrollState ${stateStr}, scrollOffset = ${scrollOffset}")
                })
                .width(100.percent)
                .height(70.percent)
                .id('MyList')

            Button(this.text)
                .width(312)
                .height(40)
                .id('MyButton')
                .fontSize(16)
                .fontWeight(FontWeight.Medium)
                .margin(top: 80)
                .onClick({ _ =>
                    this.text = 'click the button'
                    getUIContext()
                        .getPromptAction()
                        .showToast(
                            ShowToastOptions(
                                message: 'you click the button.',
                                duration: 3000
                            )
                        )
                })
        }
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xF1F3F5)
            .justifyContent(FlexAlign.End)
            .padding(left: 12, right: 12, bottom: 24)
            .onChildTouchTest({ touchInfo: Array<TouchTestInfo> =>
                for (info in touchInfo) {
                    if (info.id == 'MyList') {
                        return TouchResult(TouchTestStrategy.Forward, id: info.id)
                    }
                }
                return TouchResult(TouchTestStrategy.Default)
            })
    }
}
```

![onchildtouchtest](figures/on-child-touch-test-forward.gif)

### Example 3 (Setting the Event Dispatch Strategy to Default)

In this example, clicking and dragging in the blank area below the **List** component does not cause the **List** component to scroll. The **Button** component still responds to **onClick** events.

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
    let arr: Array<Int64> = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    @State
    var text: String = 'Button'

    func build() {
        Column {
            List(space: 12, initialIndex: 0) {
                ForEach(this.arr, itemGeneratorFunc: {
                    item: Int64, _: Int64 =>
                        ListItem {
                            Text('Item ' + item.toString())
                                .width(100.percent)
                                .height(56)
                                .fontSize(16)
                                .textAlign(TextAlign.Start)
                        }
                            .borderRadius(24)
                            .backgroundColor(Color.White)
                            .padding(left: 12, right: 12)
                }, keyGeneratorFunc: {
                    item: Int64, _: Int64 => item.toString()
                })
            }
                .listDirection(Axis.Vertical)
                .scrollBar(BarState.Off)
                .edgeEffect(EdgeEffect.Spring)
                .onScrollIndex({
                    firstIndex: Int32, lastIndex: Int32, _: Int32 =>
                        Hilog.info(0, 'cangjie', "first ${firstIndex}")
                        Hilog.info(0, 'cangjie', "last ${lastIndex}")
                })
                .onDidScroll({
                    scrollOffset: Float64, scrollState: ScrollState =>
                        let stateStr = match (scrollState) {
                            case ScrollState.Idle => "Idle"
                            case ScrollState.Scroll => "Scroll"
                            case ScrollState.Fling => "Fling"
                            case _ => ""
                        }
                        Hilog.info(0, 'cangjie', "onScroll scrollState = ScrollState ${stateStr}, scrollOffset = ${scrollOffset}")
                })
                .width(100.percent)
                .height(70.percent)
                .id('MyList')

            Button(this.text)
                .width(312)
                .height(40)
                .id('MyButton')
                .fontSize(16)
                .fontWeight(FontWeight.Medium)
                .margin(top: 80)
                .onClick({ _ =>
                    this.text = 'click the button'
                    getUIContext()
                        .getPromptAction()
                        .showToast(
                            ShowToastOptions(
                                message: 'you click the button.',
                                duration: 3000
                            )
                        )
                })
        }
            .width(100.percent)
            .height(100.percent)
            .backgroundColor(0xF1F3F5)
            .justifyContent(FlexAlign.End)
            .padding(left: 12, right: 12, bottom: 24)
            .onChildTouchTest({ _: Array<TouchTestInfo> =>
                return TouchResult(TouchTestStrategy.Default)
            })
    }
}
```

![onchildtouchtest](figures/on-child-touch-test-default.gif)
