# RowSplit

Arranges child components horizontally and inserts a vertical divider between each child component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain child components.

RowSplit restricts the width of child components through dividers. During initialization, divider positions are calculated based on the width of child components. After initialization, subsequent dynamic modifications to child component widths will not take effect—divider positions remain fixed, but child component widths can be adjusted by dragging adjacent dividers.

After initialization, dynamically modifying universal attributes such as [margin](../arkui-cj/cj-universal-attribute-size.md#func-marginlength), [border](../arkui-cj/cj-universal-attribute-border.md#func-borderlength-resourcecolor-length-borderstyle), or [padding](../arkui-cj/cj-universal-attribute-size.md#func-paddinglength) that cause a child component's width to exceed the spacing between adjacent dividers will prevent the divider from being dragged to adjust the child component's width.

## Creating the Component

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a RowSplit container that can contain child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | ()->Unit | Yes | - | Declares the child components within the container. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Component Attributes

### func resizeable(Bool)

```cangjie
public func resizeable(value: Bool): This
```

**Function:** Sets whether the divider is draggable.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the divider is draggable.<br>Default: false. |

> **Notes:**
>
> - The dividers in RowSplit can adjust the width of adjacent child components. The adjustable range depends on the minimum and maximum width constraints of the child components.
> - Supports universal attributes such as [clip](../arkui-cj/cj-universal-attribute-shapclip.md#func-clipbool) and [margin](../arkui-cj/cj-universal-attribute-size.md#func-marginlength). The default value for `clip` is `true` when not explicitly set.

## Example Code

Basic usage of RowSplit. Configures horizontally arranged child components with draggable dividers.

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
            Text("The second line can be dragged")
                .fontSize(9)
                .fontColor(0xCCCCCC)
                .width(90.percent)
            RowSplit() {
                Text("1")
                    .width(10.percent)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
                    .textAlign(TextAlign.Center)
                Text("2")
                    .width(10.percent)
                    .height(100)
                    .backgroundColor(0xD2B48C)
                    .textAlign(TextAlign.Center)
                Text("3")
                    .width(10.percent)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
                    .textAlign(TextAlign.Center)
                Text("4")
                    .width(10.percent)
                    .height(100)
                    .backgroundColor(0xD2B48C)
                    .textAlign(TextAlign.Center)
                Text("5")
                    .width(10.percent)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
                    .textAlign(TextAlign.Center)
            }
            .resizeable(true) // Draggable
            .width(90.percent).height(100)
        }
        .width(100.percent)
        .padding(top: 5)
    }
}
```

![row_split](figures/row_split.gif)