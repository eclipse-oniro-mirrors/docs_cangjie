# Ellipse

An ellipse drawing component.

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

**Function:** Draws an ellipse with specified width and height. Invalid values will be processed as initial values.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Width, value range ≥0. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Height, value range ≥0. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Component Attributes

### func initial()

```cangjie
public override func initial()
```

**Function:** Draws an ellipse with width and height set to 0. Requires setting either the [width](./cj-universal-attribute-size.md#func-widthlength) or [height](./cj-universal-attribute-size.md#func-heightlength) attribute to a non-zero value for visibility.

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
        Column() {
            // Draws a 150 * 80 ellipse
            Ellipse(width: 150, height: 80)
            // Draws a 150 * 100 red elliptical ring
            Ellipse()
                .width(150)
                .height(100)
                .fillOpacity(0.0)
                .stroke(Color.Red)
                .strokeWidth(3)
                .padding(top: 10)
        }.width(100.percent)
    }
}
```

![ellipse](./figures/ellipse.png)