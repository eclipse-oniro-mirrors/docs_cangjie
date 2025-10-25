# RelativeContainer

A relative layout component used for aligning elements in complex scenarios.

> **Note:**
>
> The margin of child components within a relative layout container differs from the general [margin](cj-universal-attribute-size.md#func-marginlength) attribute. Here, it represents the distance to the anchor point in that direction. If there is no anchor point in that direction, the margin in that direction will not take effect.

## Child Components

Supports multiple child components.

## Creating the Component

### init(() -> Unit)

```cangjie
public init(child!: () -> Unit = {=>})
```

**Function:** Creates a RelativeContainer component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | No | { => } | Declares the child components of the container. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Component Attributes

### func barrier(Array\<BarrierStyle>)

```cangjie
public func barrier(value: Array<BarrierStyle>): This
```

**Function:** Sets barriers within the RelativeContainer. Each item in the Array represents a barrier.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[BarrierStyle](#class-barrierstyle)> | Yes | - | Barriers within the RelativeContainer. |

### func guideLine(Array\<GuideLineStyle>)

```cangjie
public func guideLine(value: Array<GuideLineStyle>): This
```

**Function:** Sets guidelines within the RelativeContainer. Each item in the Array represents a guideline.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[GuideLineStyle](#class-guidelinestyle)> | Yes | - | Guidelines within the RelativeContainer. |

## Basic Type Definitions

### class BarrierStyle

```cangjie
public class BarrierStyle {
    public var id: String
    public var direction: BarrierDirection
    public var referencedId: Array<String>

    public init(id: String, direction: BarrierDirection, referencedId: Array<String>)
}
```

**Function:** Barrier parameters, used to define the ID, direction, and dependent components of a barrier.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var direction

```cangjie
public var direction: BarrierDirection
```

**Function:** Specifies the direction of the barrier. Vertical barriers (TOP, BOTTOM) can only serve as horizontal anchor points for components, with a value of 0 when used as vertical anchor points. Horizontal barriers (LEFT, RIGHT) can only serve as vertical anchor points for components, with a value of 0 when used as horizontal anchor points.

**Type:** [BarrierDirection](cj-common-types.md#enum-barrierdirection)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var id

```cangjie
public var id: String
```

**Function:** The ID of the barrier, which must be unique and cannot duplicate any component names within the container.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var referencedId

```cangjie
public var referencedId: Array<String>
```

**Function:** Specifies the components on which the barrier depends.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(String, BarrierDirection, Array\<String>)

```cangjie
public init(id: String, direction: BarrierDirection, referencedId: Array<String>)
```

**Function:** Creates an object of type BarrierStyle.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | The ID of the barrier, which must be unique and cannot duplicate any component names within the container. |
| direction | [BarrierDirection](./cj-common-types.md#enum-barrierdirection) | Yes | - | Specifies the direction of the barrier.<br>Vertical barriers (TOP, BOTTOM) can only serve as horizontal anchor points for components, with a value of 0 when used as vertical anchor points. Horizontal barriers (LEFT, RIGHT) can only serve as vertical anchor points for components, with a value of 0 when used as horizontal anchor points.<br>Default: BarrierDirection.LEFT |
| referencedId | Array\<String> | Yes | - | Specifies the components on which the barrier depends. |

### class GuideLinePosition

```cangjie
public class GuideLinePosition {
    public var start:?Length = None
    public var end:?Length = None

    public init(start!: ?Length = None, end!: ?Length = None)
}
```

**Function:** Guideline position parameters, used to define the position of a guideline.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var end

```cangjie
public var end:?Length = None
```

**Function:** The distance from the guideline to the right or bottom of the container.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var start

```cangjie
public var start:?Length = None
```

**Function:** The distance from the guideline to the left or top of the container.

**Type:** ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(?Length, ?Length)

```cangjie
public init(start!: ?Length = None, end!: ?Length = None)
```

**Function:** Creates an object of type GuideLinePosition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| start | ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | None | **Named parameter.** The distance from the guideline to the left or top of the container. |
| end | ?[Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | None | **Named parameter.** The distance from the guideline to the right or bottom of the container. |

### class GuideLineStyle

```cangjie
public class GuideLineStyle {
    public var id: String
    public var direction: Axis
    public var position: GuideLinePosition

    public init(id: String, direction: Axis, position: GuideLinePosition)
}
```

**Function:** Guideline parameters, used to define the ID, direction, and position of a guideline.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var direction

```cangjie
public var direction: Axis
```

**Function:** Specifies the direction of the guideline. Vertical guidelines can only serve as horizontal anchor points for components, with a value of 0 when used as vertical anchor points. Horizontal guidelines can only serve as vertical anchor points for components, with a value of 0 when used as horizontal anchor points.

**Type:** [Axis](cj-common-types.md#enum-axis)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var id

```cangjie
public var id: String
```

**Function:** The ID of the guideline, which must be unique and cannot duplicate any component names within the container.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var position

```cangjie
public var position: GuideLinePosition
```

**Function:** Specifies the position of the guideline. If undeclared or declared with an invalid value (e.g., undefined), the guideline's position defaults to start: 0. Either start or end declaration can be used. If both are declared, only start takes effect. If the container's size in a direction is declared as "auto", the guideline's position in that direction can only be declared using start (percentage is not allowed).

**Type:** [GuideLinePosition](#class-guidelineposition)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(String, Axis, GuideLinePosition)

```cangjie
public init(id: String, direction: Axis, position: GuideLinePosition)
```

**Function:** Creates an object of type GuideLineStyle.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | The ID of the guideline, which must be unique and cannot duplicate any component names within the container. |
| direction | [Axis](./cj-common-types.md#enum-axis) | Yes | - | Specifies the direction of the guideline.<br>Vertical guidelines can only serve as horizontal anchor points for components, with a value of 0 when used as vertical anchor points. Horizontal guidelines can only serve as vertical anchor points for components, with a value of 0 when used as horizontal anchor points.<br>Default: Axis.Vertical |
| position | [GuideLinePosition](#class-guidelineposition) | Yes | - | Specifies the position of the guideline. If undeclared or declared with an invalid value, the guideline's position defaults to start: 0. Either start or end declaration can be used. If both are declared, only start takes effect.<br>Default: {start: 0} |

## Example Code

### Example 1 (Layout Using Container and Child Components as Anchor Points)

This example demonstrates layout functionality using the container and its child components as anchor points via the `alignRules` interface.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row().width(100).height(100)
                .backgroundColor(0xff3333)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("__container__", VerticalAlign.Top),
                        left: HorizontalAlignment("__container__", HorizontalAlign.Start)
                    )
                ).id("row1")
                Row().width(100).height(100)
                .backgroundColor(0xFFCC00)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("__container__", VerticalAlign.Top),
                        right: HorizontalAlignment("__container__", HorizontalAlign.End)
                    )
                ).id("row2")
                Row().height(100)
                .backgroundColor(0xFF6633)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row1", VerticalAlign.Bottom),
                        left: HorizontalAlignment("row1", HorizontalAlign.End),
                        right: HorizontalAlignment("row2", HorizontalAlign.Start)
                    )
                ).id("row3")
                Row()
                .backgroundColor(0xFF9966)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignment("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignment("__container__", HorizontalAlign.Start),
                        right: HorizontalAlignment("row1",  HorizontalAlign.End)
                    )
                ).id("row4")
                Row()
                .backgroundColor(0xff3333)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignment("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignment("row2", HorizontalAlign.Start),
                        right: HorizontalAlignment("__container__",  HorizontalAlign.End)
                    )
                ).id("row5")
            }
            .width(300).height(300)
            .margin(left: 50.vp)
            .border(width: 2.vp, color: Color(0x6699ff))
        }.height(100.percent)
    }
}
```

![relativecontainer1](figures/relativecontainer1.jpg)### Example 2 (Setting Margins for Child Components)

This example demonstrates the usage of setting margins for child components within a container.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row().width(100).height(100)
                .backgroundColor(0xff3333)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("__container__", VerticalAlign.Top),
                        left: HorizontalAlignment("__container__", HorizontalAlign.Start)
                    )
                ).id("row1")
                .margin(10)
                Row().width(100).height(100)
                .backgroundColor(0xFFCC00)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row1", VerticalAlign.Top),
                        left: HorizontalAlignment("row1", HorizontalAlign.End)
                    )
                ).id("row2")
                Row().height(100).width(100)
                .backgroundColor(0xFF6633)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row1", VerticalAlign.Bottom),
                        left: HorizontalAlignment("row1", HorizontalAlign.Start)
                    )
                ).id("row3")
                Row().width(100).height(100)
                .backgroundColor(0xFF9966)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row2", VerticalAlign.Bottom),
                        left: HorizontalAlignment("row3", HorizontalAlign.End),
                    )
                ).id("row4")
                .margin(10)
            }
            .width(300).height(300)
            .margin(left: 50.vp)
            .border(width: 2.vp, color: Color(0x6699ff))
        }.height(100.percent)
    }
}
```

![relativecontainer2](figures/relativecontainer2.jpg)

### Example 3 (Setting Offset)

This example achieves the effect of offsetting a child component's position between two vertical anchors using [bias](cj-universal-attribute-location.md#class-bias).

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row().width(100).height(100).backgroundColor(0xff3333).alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("__container__", VerticalAlign.Top),
                        bottom: VerticalAlignment("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignment("__container__", HorizontalAlign.Start),
                        right: HorizontalAlignment("__container__", HorizontalAlign.End),
                        bias: Bias(vertical: 0.3)
                    )
                ).id("row1")
            }
            .width(300).height(300)
            .margin(left: 50.vp)
            .border(width: 2.vp, color: Color(0x6699ff))
        }.height(100.percent)
    }
}
```

![relativecontainer4](figures/relativecontainer3.jpg)

### Example 4 (Setting Guidelines)

This example demonstrates the functionality of setting guidelines in a relative layout component using the [guideLine](#func-guidelinearrayguidelinestyle) interface, where child components use the guidelines as anchors.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row().width(100).height(100).backgroundColor(0xff3333).alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("guideline2", VerticalAlign.Top),
                        left: HorizontalAlignment("guideline1", HorizontalAlign.End),
                    )
                ).id("row1")
            }.width(300).height(300).margin(left: 50.vp).border(width: 2.vp, color: Color(0x6699ff))
            .guideLine(
                [GuideLineStyle("guideline1", Axis.Vertical, GuideLinePosition(start: 50.vp)),
                GuideLineStyle("guideline2", Axis.Horizontal, GuideLinePosition(start: 50.vp))])
        }.height(100.percent)
    }
}
```

![relativecontainer5](figures/relativecontainer4.jpg)

### Example 5 (Setting Barriers)

This example demonstrates the usage of setting barriers in a relative layout component using the [barrier](#func-barrierarraybarrierstyle) interface, where child components use the barriers as anchors.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row().width(100).height(100)
                .backgroundColor(0xff3333)
                .id("row1")

                Row().width(100).height(100)
                .backgroundColor(0xFFCC00)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row1", VerticalAlign.Bottom),
                        middle: HorizontalAlignment("row1", HorizontalAlign.End)
                    )
                ).id("row2")

                Row().height(100).width(100)
                .backgroundColor(0xFF6633)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("row1", VerticalAlign.Top),
                        left: HorizontalAlignment("barrier1", HorizontalAlign.End)
                    )
                ).id("row3")

                Row().width(50).height(50)
                .backgroundColor(0xFF9966)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignment("barrier2", VerticalAlign.Bottom),
                        left: HorizontalAlignment("row1", HorizontalAlign.Start),
                    )
                ).id("row4")
            }.width(300).height(300)
            .margin(left: 50.vp)
            .border(width: 2.vp, color: Color(0x6699ff))
            .barrier(
                [BarrierStyle("barrier1", BarrierDirection.Right, ["row1", "row2"]),
                BarrierStyle("barrier2", BarrierDirection.Bottom, ["row1", "row2"])])
        }.height(100.percent)
    }
}
```

![relativecontainer6](figures/relativecontainer5.jpg)