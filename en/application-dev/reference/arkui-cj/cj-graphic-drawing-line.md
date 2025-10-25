# Line

A component for drawing straight lines.

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

**Function:** Draws a straight line within a fill area of specified width and height.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Width of the fill area, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or omitted, it will be processed according to the width required by its content. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Height of the fill area, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or omitted, it will be processed according to the height required by its content. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func endPoint((Float64,Float64))

```cangjie
public func endPoint(value: (Float64, Float64)): This
```

**Function:** Sets the end point coordinates of the line (relative coordinates). Abnormal values will be processed according to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | (Float64,Float64) | Yes | - | End point coordinates of the line (relative coordinates).<br>Initial value: [0.0, 0.0].<br>Unit: vp. |

### func initial()

```cangjie
public override func initial()
```

**Function:** Creates a line object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func startPoint((Float64,Float64))

```cangjie
public func startPoint(value: (Float64, Float64)): This
```

**Function:** Sets the start point coordinates of the line (relative coordinates). Abnormal values will be processed according to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | (Float64,Float64) | Yes | - | Start point coordinates of the line (relative coordinates).<br>Initial value: [0.0, 0.0].<br>Unit: vp. |

## Example Code

### Example 1 (Drawing with Component Attributes)

Using startPoint, endPoint, fillOpacity, stroke, strokeDashArray, and strokeDashOffset attributes to draw the start point, end point, opacity, line color, border gaps, and drawing start point of a line.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 10) {
            // The start and end coordinates of the line are relative to the drawing area of the Line component itself
            Line()
                .width(200)
                .height(150)
                .startPoint((0.0, 0.0))
                .endPoint((50.0, 100.0))
                .stroke(Color.Black)
                .backgroundColor(0xF5F5F5)
            Line()
                .width(200)
                .height(150)
                .startPoint((50.0, 50.0))
                .endPoint((150.0, 150.0))
                .strokeWidth(5)
                .stroke(Color.Red)
                .strokeOpacity(0.5)
                .backgroundColor(0xF5F5F5)
            // strokeDashOffset defines the offset when rendering the associated dashed line strokeDashArray
            Line()
                .width(200)
                .height(150)
                .startPoint((0.0, 0.0))
                .endPoint((100.0, 100.0))
                .stroke(Color.Black)
                .strokeWidth(3)
                .strokeDashArray([10, 3])
                .strokeDashOffset(5)
                .backgroundColor(0xF5F5F5)
            // When the coordinate values exceed the width and height range of the Line component, the line will extend beyond the component's drawing area
            Line()
                .width(50)
                .height(50)
                .startPoint((0.0, 0.0))
                .endPoint((100.0, 100.0))
                .stroke(Color.Black)
                .strokeWidth(3)
                .strokeDashArray([10, 3])
                .backgroundColor(0xF5F5F5)
        }.width(100.percent)
    }
}
```

![line2](./figures/line2.png)

### Example 2 (Drawing Border Endpoints)

Using strokeLineCap to draw the border endpoint style of a line.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Row(space: 10) {
            // When LineCapStyle is Butt
            Line()
                .width(100)
                .height(200)
                .startPoint((50.0, 50.0))
                .endPoint((50.0, 200.0))
                .stroke(Color.Black)
                .strokeWidth(20)
                .strokeLineCap(LineCapStyle.Butt)
                .backgroundColor(0xF5F5F5)
                .margin(10)
            // When LineCapStyle is Round
            Line()
                .width(100)
                .height(200)
                .startPoint((50.0, 50.0))
                .endPoint((50.0, 200.0))
                .stroke(Color.Black)
                .strokeWidth(20)
                .strokeLineCap(LineCapStyle.Round)
                .backgroundColor(0xF5F5F5)
            // When LineCapStyle is Square
            Line()
                .width(100)
                .height(200)
                .startPoint((50.0, 50.0))
                .endPoint((50.0, 200.0))
                .stroke(Color.Black)
                .strokeWidth(20)
                .strokeLineCap(LineCapStyle.Square)
                .backgroundColor(0xF5F5F5)
        }
    }
}
```

![line3](./figures/line3.png)

### Example 3 (Drawing Border Gaps)

Using strokeDashArray to draw the border gaps of a line.

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
            Line()
                .width(300)
                .height(30)
                .startPoint((50.0, 30.0))
                .endPoint((300.0, 30.0))
                .stroke(Color.Black)
                .strokeWidth(10)
            // Set the strokeDashArray interval to 50
            Line()
                .width(300)
                .height(30)
                .startPoint((50.0, 20.0))
                .endPoint((300.0, 20.0))
                .stroke(Color.Black)
                .strokeWidth(10)
                .strokeDashArray([50])
            // Set the strokeDashArray interval to 50, 10
            Line()
                .width(300)
                .height(30)
                .startPoint((50.0, 20.0))
                .endPoint((300.0, 20.0))
                .stroke(Color.Black)
                .strokeWidth(10)
                .strokeDashArray([50, 10])
            // Set the strokeDashArray interval to 50, 10, 20
            Line()
                .width(300)
                .height(30)
                .startPoint((50.0, 20.0))
                .endPoint((300.0, 20.0))
                .stroke(Color.Black)
                .strokeWidth(10)
                .strokeDashArray([50, 10, 20])
            // Set the strokeDashArray interval to 50, 10, 20, 30
            Line()
                .width(300)
                .height(30)
                .startPoint((50.0, 20.0))
                .endPoint((300.0, 20.0))
                .stroke(Color.Black)
                .strokeWidth(10)
                .strokeDashArray([50, 10, 20, 30])
        }
    }
}
```

![line4](./figures/line4.png)