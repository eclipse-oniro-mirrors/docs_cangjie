# Badge

An information marker component that can be attached to a single component as a container for notification alerts.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Subcomponents

Supports a single subcomponent.

> **Note:**
>
> Subcomponent types: System components and custom components, including rendering control types ([if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), [LazyForEach](cj-state-rendering-lazyforeach.md)).

## Creating Components

### init(Int32, BadgeStyle, BadgePosition, Int32, () -> Unit)

```cangjie
public init(count!: Int32, style!: BadgeStyle, position!: BadgePosition = BadgePosition.RightTop,
    maxCount!: Int32 = 99, child!: () -> Unit)
```

**Function:** Creates a badge component based on a numeric value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| count | Int32 | Yes | - | **Named parameter.** Sets the notification count. The badge is hidden when the value is ≤ 0. |
| style | [BadgeStyle](#class-badgestyle) | Yes | - | **Named parameter.** Configurable styles for the Badge component, including text color, size, dot color, and size. |
| position | [BadgePosition](#enum-badgeposition) | No | BadgePosition.RightTop | **Named parameter.** Position of the notification dot. |
| maxCount | Int32 | No | 99 | **Named parameter.** Maximum notification count. Exceeding this value displays as "maxCount+". |
| child | () -> Unit | Yes | - | The child component of the container. |

### init(String, BadgeStyle, BadgePosition, () -> Unit)

```cangjie
public init(value!: String, style!: BadgeStyle, position!: BadgePosition = BadgePosition.RightTop, child!: () -> Unit)
```

**Function:** Creates a badge component based on a string value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | Parameter for the numeric badge component. |
| style | [BadgeStyle](#class-badgestyle) | Yes | - | **Named parameter.** Configurable styles for the Badge component, including text color, size, dot color, and size. |
| position | [BadgePosition](#enum-badgeposition) | No | BadgePosition.RightTop | **Named parameter.** Position of the notification dot. |
| child | () -> Unit | Yes | - | The child component of the container. |

## Common Attributes/Events

Common Attributes: All supported except text styles.

Common Events: All supported.

## Basic Type Definitions

### class BadgeStyle

```cangjie
public class BadgeStyle {
    public var color: ResourceColor
    public var fontSize: Length
    public var badgeSize: Length
    public var badgeColor: ResourceColor
    public var fontWeight: FontWeight
    public var borderColor: ResourceColor
    public var borderWidth: Length
    public init(color!: ResourceColor = Color.White, fontSize!: Length = 10.fp, badgeSize!: Length = 16.vp,
        badgeColor!: ResourceColor = Color.Red, fontWeight!: FontWeight = FontWeight.Normal,
        borderColor!: ResourceColor = Color.Red, borderWidth!: Length = 1.vp)
}
```

**Function:** Contains style parameters for the Badge component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var badgeColor

```cangjie
public var badgeColor: ResourceColor
```

**Function:** Color of the badge.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var badgeSize

```cangjie
public var badgeSize: Length
```

**Function:** Size of the badge, in vp units.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var borderColor

```cangjie
public var borderColor: ResourceColor
```

**Function:** Border color of the base plate.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var borderWidth

```cangjie
public var borderWidth: Length
```

**Function:** Border thickness of the base plate.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var color

```cangjie
public var color: ResourceColor
```

**Function:** Text color.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var fontSize

```cangjie
public var fontSize: Length
```

**Function:** Text size, in fp units.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var fontWeight

```cangjie
public var fontWeight: FontWeight
```

**Function:** Sets the font weight of the text.

**Type:** [FontWeight](./cj-common-types.md#enum-fontweight)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(ResourceColor, Length, Length, ResourceColor, FontWeight, ResourceColor, Length)

```cangjie
public init(color!: ResourceColor = Color.White, fontSize!: Length = 10.fp, badgeSize!: Length = 16.vp,
    badgeColor!: ResourceColor = Color.Red, fontWeight!: FontWeight = FontWeight.Normal,
    borderColor!: ResourceColor = Color.Red, borderWidth!: Length = 1.vp)
```

**Function:** Creates a BadgeStyle object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.White | **Named parameter.** Text color. |
| fontSize | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 10.fp | **Named parameter.** Text size.<br>Unit: fp. |
| badgeSize | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | **Named parameter.** Size of the badge.<br>Unit: fp. |
| badgeColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Red | **Named parameter.** Color of the badge. |
| fontWeight | [FontWeight](./cj-common-types.md#enum-fontweight) | No | FontWeight.Normal | **Named parameter.** Font weight of the text. |
| borderColor | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Red | **Named parameter.** Border color of the base plate. |
| borderWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 1.vp | **Named parameter.** Border thickness of the base plate.<br>Unit: vp. |

### enum BadgePosition

```cangjie
public enum BadgePosition {
    | RightTop
    | Right
    | Left
}
```

**Function:** Position of the notification dot.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### Left

```cangjie
Left
```

**Function:** The dot is displayed on the left side, vertically centered.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### Right

```cangjie
Right
```

**Function:** The dot is displayed on the right side, vertically centered.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### RightTop

```cangjie
RightTop
```

**Function:** The dot is displayed in the top-right corner.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### func ==(BadgePosition)

```cangjie
public operator func ==(other: BadgePosition): Bool
```

**Function:** Determines if two BadgePosition values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | BadgePosition | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the enum values are equal, otherwise `false`. |

## Example Code

### Example 1 (Setting Badge Content)

This example demonstrates different badge effects when passing empty values, strings, or numbers via the `value` and `count` properties.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Text("numberBadge").width(80.percent)
            Row(space: 10) {
                // Numeric superscript, maxCount defaults to 99. Values exceeding 99 display as "99+".
                Badge(
                    count: 1,
                    style: BadgeStyle(color: Color(0xFFFFFF), fontSize: 16, badgeSize: 20, badgeColor: Color.Red,
                        fontWeight: FontWeight.Bolder, borderColor: Color.Black, borderWidth: 2.vp),
                    position: BadgePosition.RightTop,
                    maxCount: 99
                ) {
                    Button("message").width(100).height(50).backgroundColor(0x317aff)
                }.width(100).height(50)
                Badge(
                    count: 1,
                    style: BadgeStyle(color: Color(0xFFFFFF), fontSize: 16, badgeSize: 20, badgeColor: Color.Red,
                        fontWeight: FontWeight.Bolder, borderColor: Color.Green, borderWidth: 2.vp),
                    position: BadgePosition.Left,
                    maxCount: 99
                ) {
                    Button("message").width(100).height(50).backgroundColor(0x317aff)
                }.width(100).height(50)
                // Numeric superscript
                Badge(
                    count: 1,
                    style: BadgeStyle(color: Color(0xFFFFFF), fontSize: 16, badgeSize: 20, badgeColor: Color.Red,
                        fontWeight: FontWeight.Regular, borderColor: Color.Gray, borderWidth: 4.vp),
                    position: BadgePosition.Right,
                    maxCount: 99
                ) {
                    Button("message").width(100).height(50).backgroundColor(0x317aff)
                }.width(100).height(50)
            }.margin(10)
            Text("stringBadge").width(80.percent)
            Row(space: 30) {
                Badge(
                    value: "new",
                    style: BadgeStyle(color: Color(0xFFFFFF), fontSize: 9, badgeSize: 20, badgeColor: Color.Blue)
                ) {
                    Text("message")
                        .width(80)
                        .height(50)
                        .fontSize(16)
                        .lineHeight(37)
                        .borderRadius(10)
                        .textAlign(TextAlign.Center)
                        .backgroundColor(0xF3F4ED)
                }.width(80).height(50)
                // Empty value: Displays a dot marker
                Badge(
                    value: "",
                    style: BadgeStyle(badgeSize: 6, badgeColor: Color.Blue),
                    position: BadgePosition.Right
                ) {
                    Text("message")
                        .width(90)
                        .height(50)
                        .fontSize(16)
                        .lineHeight(37)
                        .borderRadius(10)
                        .textAlign(TextAlign.Center)
                        .backgroundColor(0xF3F4ED)
                }.width(90).height(50)
            }.margin(10)
        }
    }
}
```

![badge](./figures/badge.png)

### Example 2 (Controlling Badge Visibility via Numeric Values)

This example demonstrates hiding and showing the badge by setting the `count` property to 0 and 1.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var badgeCount: Int32 = 1
    func build() {
        Column() {
            Badge(
                count: this.badgeCount,
                style: BadgeStyle(color: Color(0xFFFFFF), fontSize: 16, badgeSize: 20, badgeColor: Color.Red, fontWeight: FontWeight.Bolder, borderColor: Color.Black, borderWidth: 2.vp),
                position: BadgePosition.RightTop,
            ){
                Text("message")
                    .width(100)
                    .height(50)
                    .backgroundColor(0x317aff)
            }
                .width(100)
                .height(50)
            Button("count 0")
                .onClick{ evt => this.badgeCount = 0; }
            Button("count 1")
                .onClick{ evt => this.badgeCount = 1; }
        }.margin(10)
    }
}
```

![badge1](./figures/badge1.gif)
