# Circle

A component for drawing circles.

## Subcomponents

None

## Creating the Component

### init(Length, Length)

```cangjie

public init(width!: Length = 0.vp, height!: Length = 0.vp)
```

**Function:** Draws a circle with specified width and height. When width and height are unequal, the shorter edge will be used as the diameter. Invalid values will be handled using initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Width, value range ≥0.<br>Initial value: 0.<br>Default unit: vp. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Height, value range ≥0.<br>Initial value: 0.<br>Default unit: vp. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func initial()

```cangjie

public override func initial()
```

**Function:** Creates an object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

## Example Code

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
            // Draws a circle with diameter of 150
            Circle(width: 150, height: 150)
            // Draws a red dashed circular ring with diameter of 150 (when width and height are unequal, the shorter edge is used as diameter)
            Circle()
                .width(150)
                .height(200)
                .fillOpacity(0.0)
                .strokeWidth(3)
                .stroke(Color.Red)
                .strokeDashArray([1, 2])
        }.width(100.percent)
    }
}
```

![circle2](./figures/circle2.png)