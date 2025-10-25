# Rect

A component for drawing rectangles.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(Length, Length)

```cangjie
public init(width!: Length = 0.vp, height!: Length = 0.vp)
```

**Function:** Draws a rectangle with specified width and height. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Width of the rectangle, value range ≥0. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Height of the rectangle, value range ≥0. |

## Common Attributes/Events

Common Attributes: Supports all common attributes.

Common Events: Fully supported.

## Component Attributes

### func initial()

```cangjie
public override func initial()
```

**Function:** Overrides the parent class's initial method for initialization logic.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func radius(Length)

```cangjie
public func radius(value: Length): This
```

**Function:** Sets the corner radius size, value range ≥0. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Corner radius size.<br>Initial value: 0.<br>Default unit: vp. |

### func radius(Array\<Length>)

```cangjie
public func radius(value: Array<Length>): This
```

**Function:** Sets the corner radius sizes, value range ≥0. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Array\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | Yes | - | Top-left, top-right, bottom-right, and bottom-left corner radius sizes.<br>Initial value: 0.<br>Default unit: vp. |

### func radius(Array\<(Length,Length)>)

```cangjie
public func radius(radiusArray: Array<(Length, Length)>): This
```

**Function:** Sets the corner radius sizes, value range ≥0. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| radiusArray | Array\<([Length](../BasicServicesKit/cj-apis-base.md#interface-length),[Length](../BasicServicesKit/cj-apis-base.md#interface-length))> | Yes | - | Width and height of top-left, top-right, bottom-right, and bottom-left corners.<br>Initial value: 0.<br>Default unit: vp. |

### func radiusHeight(Length)

```cangjie
public func radiusHeight(value: Length): This
```

**Function:** Sets the height of the corner radius. If only height is set, width and height will be equal. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Height of the corner radius.<br>Initial value: 0.<br>Default unit: vp. |

### func radiusWidth(Length)

```cangjie
public func radiusWidth(value: Length): This
```

**Function:** Sets the width of the corner radius. If only width is set, width and height will be equal. Invalid values will be treated as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Width of the corner radius.<br>Initial value: 0.<br>Default unit: vp. |

## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import ohos.base.*
import ohos.arkui.component.*
import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 10) {
            Text("normal").fontSize(11).fontColor(0xCCCCCC).width(90.percent)
            // Draw a 90% * 50 rectangle
            Column(space: 5) {
                Text("normal").fontSize(9).fontColor(0xCCCCCC).width(90.percent)
                // Draw a 90% * 50 rectangle
                Rect().width(90.percent).height(50).fill(Color.Green)
                // Draw a 90% * 50 rectangle frame
                Rect()
                .width(90.percent)
                .height(50)
                .fillOpacity(0.0)
                .stroke(Color.Red)
                .strokeWidth(3)

                Text("with rounded corners").fontSize(11).fontColor(0xCCCCCC).width(90.percent)
                // Draw a 90% * 80 rectangle with corner width 40 and height 20
                Rect()
                .width(90.percent)
                .height(50)
                .radiusHeight(20)
                .radiusWidth(40)
                .fill(Color.Green)
                // Draw a 90% * 80 rectangle with corner radius 20
                Rect()
                .width(90.percent)
                .height(80)
                .radius(20)
                .fill(Color.Green)
                .stroke(Color.Transparent)
            }.width(100.percent).margin(top: 10)
            // Draw a 90% * 50 rectangle with top-left corner (40,40), top-right (20,20), bottom-right (40,40), bottom-left (20,20)
            Rect()
            .width(90.percent)
            .height(80)
            .radius([(40, 40), (20, 20), (40, 40), (20, 20)])
            .fill(Color.Green)
        }.width(100.percent).margin(top: 5)
    }
}
```

![rect2](./figures/rect2.png)