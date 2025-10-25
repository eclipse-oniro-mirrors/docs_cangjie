# ListItem

Used to display specific items in a list, must be used in conjunction with List.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain a single child component.

## Creating Component

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a ListItem component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | ()->Unit | Yes | - | The child component within the ListItem container. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func selectable(Bool)

```cangjie
public func selectable(value: Bool): This
```

**Function:** Sets whether the current ListItem element is editable. In edit mode, list items can be deleted or moved.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the ListItem element is editable.<br/>Default: false. |

### func swipeAction(CustomBuilder, CustomBuilder, SwipeEdgeEffect, (Float64) -> Unit)

```cangjie
public func swipeAction(
    start!: CustomBuilder = {=>},
    end!: CustomBuilder = {=>},
    edgeEffect!: SwipeEdgeEffect = SwipeEdgeEffect.Spring,
    onOffsetChange!: (Float64) -> Unit = {_: Float64 =>}
): This
```

**Function:** Used to set the swipe-out component for ListItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| start | [CustomBuilder](./cj-common-types.md#type-custombuilder) | No | { => } | **Named parameter.** The component on the left side of the item when ListItem is swiped right (when List is vertically oriented) or the component above the item when ListItem is swiped down (when List is horizontally oriented). Use with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and bind method. |
| end | [CustomBuilder](./cj-common-types.md#type-custombuilder) | No | { => } | **Named parameter.** The component on the right side of the item when ListItem is swiped left (when List is vertically oriented) or the component below the item when ListItem is swiped up (when List is horizontally oriented). Use with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and bind method. |
| edgeEffect | [SwipeEdgeEffect](./cj-common-types.md#enum-swipeedgeeffect) | No | SwipeEdgeEffect.Spring | **Named parameter.** The swipe effect. |
| onOffsetChange | (Float64)->Unit | No | { _: Float64 => } | **Named parameter.** Called when the swipe operation offset changes.<br/> **Note:**<br/>Triggered when the position of the list item changes during left/right swipe (when list orientation is vertical) or up/down swipe (when list orientation is horizontal), measured in vp units. |

## Component Events

### func onSelect((Bool) -> Unit)

```cangjie
public func onSelect(event: (Bool) -> Unit): This
```

**Function:** Triggered when the selection state of the ListItem element changes via mouse selection.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | (Bool)->Unit | Yes | - | Callback triggered when the selection state of the ListItem element changes via mouse selection. Selected when entering the mouse selection range (true), deselected when exiting the mouse selection range (false). |

## Example Code

This example demonstrates the basic usage of creating a ListItem.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    func build() {
        Column() {
            List(space: 20, initialIndex: 0) {
                ForEach(this.arr,itemGeneratorFunc: {item: Int64, _: Int64 => ListItem() {
                            Text("${item}")
                            .width(100.percent)
                            .height(100)
                            .fontSize(16)
                            .textAlign(TextAlign.Center)
                            .borderRadius(10)
                            .backgroundColor(0xFFFFFF)
                        }
                    }
                )
            }
            .scrollBar(BarState.Off)
            .width(90.percent)
        }
        .width(100.percent)
        .height(100.percent)
        .backgroundColor(0xDCDCDC)
        .padding(top: 5.px)
    }
}
```

![list1](figures/list1.gif)