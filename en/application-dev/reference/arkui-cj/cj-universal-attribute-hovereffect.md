# Hover Effect

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Sets the hover effect of a component. Multiple hover effect types such as scaling, fade-in and fade-out, and system default are supported. The hover effect presents visual feedback when the mouse pointer hovers over the component, helping users identify the current interaction area and improving the interface interaction experience.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func hoverEffect(?HoverEffect)

```cangjie
func hoverEffect(value: ?HoverEffect): T
```

**Description:** Sets the hover effect of a component. When hoverEffect is not set, the default hover effect of the component is HoverEffect.Auto. For components with a hover effect applied, the hover effect is hidden when the mouse hovers over the component and presses down; the hover effect is restored when the mouse button is released and the mouse pointer is still hovering over the component. When value is None, the default hover effect is retained.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[HoverEffect](./cj-common-types.md#enum-hovereffect) | Yes | - | Sets the hover effect of the current component in the hover state. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## Sample Code

This example sets the hover effect of components through hoverEffect.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State
    var isHoverVal: Bool = false

    func build() {
        Column(space: 5) {
            Column(space: 5) {
                Text('Scale').fontSize(20).fontColor(Color.Gray).width(90.percent).position(x: 0, y: 80)
                Column()
                    .width(80.percent)
                    .height(200)
                    .backgroundColor(Color.Gray)
                    .position(x: 40, y: 120)
                    // Set the hover effect to the scale-up and scale-down effect
                    .hoverEffect(HoverEffect.Scale)
                    .onHover({ isHover =>
                        Hilog.info(1, "info", "Scale isHover: ${isHover}")
                        this.isHoverVal = isHover
                    })

                Text('Board').fontSize(20).fontColor(Color.Gray).width(90.percent).position(x: 0, y: 380)
                Column()
                    .width(80.percent)
                    .height(200)
                    .backgroundColor(Color.Yellow)
                    // Set the hover effect to the background fade-in and fade-out emphasis effect
                    .hoverEffect(HoverEffect.Highlight)
                    .position(x: 40, y: 420)
                    .onHover({ isHover =>
                        Hilog.info(1, "info", "Highlight isHover: ${isHover}")
                        this.isHoverVal = isHover
                    })
            }
                // Set the hover effect to none
                .hoverEffect(HoverEffect.None)
                .width(100.percent)
                .height(100.percent)
                .border(width: 1)
                .onHover({ isHover =>
                    Hilog.info(1, "info", "HoverEffect.None")
                    this.isHoverVal = isHover
                })
        }
    }
}
```

![onHover](./figures/onHover.gif)
