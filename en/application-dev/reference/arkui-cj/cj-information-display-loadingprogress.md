# LoadingProgress

A component for displaying loading animations.

The loading animation stops when the component is not visible. The visibility state of the component is determined by the [onVisibleAreaChange](./cj-ui-framework.md#func-onvisibleareachangearea-area-raitos-raitos---unit) handler, where a visibility threshold ratio greater than 0 is considered as the visible state.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init()

```cangjie
public init()
```

**Function:** Creates a loading progress component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## Common Attributes/Common Events

Common Attributes: All supported except text styles.

> **Note:**
>
> The component should have reasonable width and height settings. When the component's dimensions are set too large, the loading animation may not display as expected.

Common Events: All supported.

## Component Attributes

### func color(ResourceColor)

```cangjie
public func color(value: ResourceColor): This
```

**Function:** Sets the foreground color of the current loading progress bar using the ResourceColor type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | The default foreground color of the loading progress bar.<br>Initial value: 0xff666666. |

## Example Code

### Example 1

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column(space: 5) {
            Text("Orbital LoadingProgress")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
            LoadingProgress()
            .color(Color.Blue)
        }.width(100.percent).margin(top: 5)
    }
}
```

![loading_progress_1](figures/Loadingprogress_1.gif)