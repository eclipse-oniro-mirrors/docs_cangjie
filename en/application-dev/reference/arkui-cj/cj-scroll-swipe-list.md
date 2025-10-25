# List

A container component that contains a series of list items with the same width. Suitable for presenting homogeneous data continuously and multi-line, such as images and text.

## Subcomponents

Only supports [ListItem](./cj-scroll-swipe-listitem.md) and [ListItemGroup](./cj-scroll-swipe-listgroup.md) subcomponents. Supports rendering control types ([if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), [LazyForEach](./cj-state-rendering-lazyforeach.md)).

> **Note:**
>
> Index calculation rules for List subcomponents:
>
> * Increments sequentially according to the order of subcomponents.
> * In if/else statements, only subcomponents within the branch where the condition is met will participate in index calculation; subcomponents in branches where the condition is not met will not be calculated.
> * In ForEach/LazyForEach statements, all expanded subnode indices will be calculated.
> * After changes occur in [if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), or [LazyForEach](./cj-state-rendering-lazyforeach.md), subnode indices will be updated.
> * ListItemGroup is calculated as a whole with one index value; ListItems within ListItemGroup are not calculated.
> * Subcomponents with visibility set to Hidden or None will still be calculated in the index.

## Creating the Component

### init(Int64, Int32, ?Scroller, () -> Unit)

```cangjie
public init(
    space!: Int64 = 0,
    initialIndex!: Int32 = 0,
    scroller!: ?Scroller = Option<Scroller>.None,
    child!: () -> Unit
)
```

**Function:** Creates a List container that can contain subcomponents.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| space | Int64 | No | 0 | **Named parameter.** Spacing between subcomponents along the main axis.<br/>Initial value: 0.<br/>Unit: vp.<br/>**Note:**<br/>If set to a negative number or greater than or equal to the length of the List content area, the initial value will be used.<br/>If the space parameter is less than the List divider width, the spacing between subcomponents along the main axis will take the divider width.<br/>If a List subcomponent's visibility is set to None, it will not be displayed, but the space above and below it will still take effect. |
| initialIndex | Int32 | No | 0 | **Named parameter.** Sets the item displayed at the starting position of the viewport when the List is initially loaded, i.e., the first item. If the set value exceeds the index of the last item in the current List, it will not take effect.<br/>Initial value: 0.<br/>**Note:**<br/>If set to a negative number or exceeds the index of the last item in the current List, it will be treated as an invalid value and the initial value will be used. |
| scroller | ?[Scroller](cj-scroll-swipe-scroll.md#class-scroller) | No | Option\<Scroller>.None | **Named parameter.** Controller for scrollable components. Used to bind with scrollable components.<br/>**Note:**<br/>Cannot be bound to the same scroll control object as other scrollable components such as [List](./cj-scroll-swipe-list.md), [Grid](./cj-scroll-swipe-grid.md), and [Scroll](./cj-scroll-swipe-scroll.md). |
| child | () -> Unit | Yes | - | **Named parameter.** Declares the List subcomponents within the container. |

## Common Attributes/Common Events

Common Attributes: All supported. Also supports common attributes for scrollable components.

Common Events: All supported.

## Component Attributes

### func alignListItem(ListItemAlign)

```cangjie
public func alignListItem(value: ListItemAlign): This
```

**Function:** Sets the layout method for ListItems along the cross axis when the List's cross-axis width is greater than the ListItem's cross-axis width * lanes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ListItemAlign](cj-common-types.md#enum-listitemalign) | Yes | - | Layout method along the cross axis.<br/>Initial value: ListItemAlign.Start. |

### func cachedCount(Int32)

```cangjie
public func cachedCount(value: Int32): This
```

**Function:** Sets the number of ListItem/ListItemGroup components to preload in the list. In lazy loading scenarios, only content outside the List display area up to cachedCount will be preloaded. In non-lazy loading scenarios, all content will be loaded. Both lazy and non-lazy loading will only layout content within the List display area plus cachedCount content outside the display area.

After setting cachedCount for a List, ListItems outside the display area will be preloaded and laid out up and down by cachedCount rows. When calculating the number of ListItem rows, ListItems within ListItemGroup will be counted. If there are no ListItems within a ListItemGroup, the entire ListItemGroup will be counted as one row.

When using LazyForEach nested under List and ListItemGroup nested under LazyForEach, LazyForEach will create cachedCount ListItemGroups outside the List display area up and down.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Number of ListItem/ListItemGroup components to preload in the list.<br/>Initial value: Set based on the number of nodes displayed on the screen, with a maximum value of 16.<br/>Range: [0, +∞). |

### func chainAnimation(Bool)

```cangjie
public func chainAnimation(value: Bool): This
```

**Function:** Sets whether the current List enables chained linkage animation.

> **Note:**
>
> * Chained linkage effect refers to the process where, during finger scrolling, the ListItem being dragged by the finger is the active object, and adjacent ListItems are passive objects. The active object drives the passive objects to link, following the spring physics animation effect.
> * The chained animation effect is reflected in the spacing between ListItems. The spacing in the static state can be set via the List component's space parameter. If the space parameter is not set and chained animation is enabled, the initial spacing value is 20.vp.
> * After enabling chained animation, List dividers will not be displayed.
> * The prerequisite for chained animation to take effect is that the List is in single-column mode and the edge effect is of type EdgeEffect.Spring.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to enable chained linkage animation.<br/>Initial value: false, chained linkage is disabled. true, chained linkage is enabled. |

### func divider(Length, ResourceColor, Length, Length)

```cangjie
public func divider(strokeWidth!: Length, color!: ResourceColor = Color.Black, startMargin!: Length = 0.vp,
    endMargin!: Length = 0.vp): This
```

**Function:** Used to set the style of ListItem dividers. By default, there are no dividers.

List dividers are drawn between subcomponents along the main axis. Dividers will not be drawn above the first subcomponent or below the last subcomponent.

In multi-column mode, the starting margin of dividers between ListItems is calculated from the starting edge of each column along the cross axis. In single-column mode, it is calculated from the starting edge of the List along the cross axis.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| strokeWidth | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Width of the divider line.<br/>**Note:**<br/>If set to a negative number or greater than or equal to the length of the List content area, it will be treated as 0. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No | Color.Black | **Named parameter.** Color of the divider. |
| startMargin | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Distance from the divider to the starting edge of the list side.<br/>**Note:**<br/>If set to a negative number, the initial value will be used. |
| endMargin | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 0.vp | **Named parameter.** Distance from the divider to the ending edge of the list side.<br/>**Note:**<br/>If set to a negative number, the initial value will be used. |

### func edgeEffect(EdgeEffect)

```cangjie
public func edgeEffect(value: EdgeEffect): This
```

**Function:** Sets the edge scrolling effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [EdgeEffect](cj-common-types.md#enum-EdgeEffect) | Yes | - | Edge scrolling effect for the List component, supporting spring effect and shadow effect.<br/>Initial value: EdgeEffect.Spring. |

### func lanes(Int32)

```cangjie
public func lanes(value: Int32): This
```

**Function:** Sets the number of layout columns or rows for the List component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Number of layout columns or rows for the List component.<br/>Initial value: 1.<br/>Range: [1, +∞). |

### func lanes(Length, Length)

```cangjie
public func lanes(minLength!: Length, maxLength!: Length): This
```

**Function:** Sets the number of layout columns or rows for the List component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| minLength | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Minimum length of the component. |
| maxLength | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** Maximum length of the component. |

### func listDirection(Axis)

```cangjie
public func listDirection(value: Axis): This
```

**Function:** Sets the arrangement direction of the List component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Axis](cj-common-types.md#enum-axis) | Yes | - | Arrangement direction of the component.<br/>Initial value: Axis.Vertical. |

### func multiSelectable(Bool)

```cangjie
public func multiSelectable(value: Bool): This
```

**Function:** Whether to enable mouse box selection.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to enable mouse box selection.<br/>Initial value: false, box selection is disabled. true, box selection is enabled. |

### func sticky(StickyStyle)

```cangjie
public func sticky(value: StickyStyle): This
```

**Function:** Used in conjunction with the [ListItemGroup](./cj-scroll-swipe-listgroup.md) component to set whether the header and footer of ListItemGroup should stick to the top or bottom. The sticky attribute can be set to StickyStyle.Header | StickyStyle.Footer to support both header sticking to the top and footer sticking to the bottom.

> **Note:**
>
> Due to floating-point calculation precision, small gaps may occasionally appear during List scrolling after setting sticky. This can be resolved by specifying [pixelRound](./cj-common-types.md#enum-pixelroundcalcpolicy) for the current component to round down to the nearest pixel.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [StickyStyle](./cj-common-types.md#enum-stickystyle) | Yes | - | Sticky effect for ListItemGroup to the top or bottom.<br/>Initial value: StickyStyle.None. |

## Component Events

### func onScrollFrameBegin((Float64,ScrollState) -> onScrollFrameBeginHandleResult)

```cangjie
public func onScrollFrameBegin(event: (Float64, ScrollState) -> onScrollFrameBeginHandleResult): This
```

**Function:** Triggered when the list starts scrolling. The event parameters include the upcoming scroll amount. The event handler can calculate the actual required scroll amount based on the application scenario and return it as the return value of the event handler. The list will scroll according to the actual scroll amount returned.

When listDirection is set to Axis.Vertical, the vertical scroll amount is returned. When listDirection is set to Axis.Horizontal, the horizontal scroll amount is returned.

Conditions for triggering this event: Triggered at the start of each frame during finger dragging or inertial scrolling of the List; scrolling caused by List edge rebound, using the scroll controller, or dragging the scrollbar will not trigger this event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | (Float64,[ScrollState](cj-common-types.md#enum-scrollstate))->[onScrollFrameBeginHandleResult](#class-onscrollframebeginhandleresult) | Yes | - | Triggered when the list starts scrolling.<br/>Parameter 1: Upcoming scroll amount, unit: vp.<br/>Parameter 2: Current scroll state of the List component.<br/>Return value: Actual scroll amount, unit: vp. |

### func onScrollIndex((Int32,Int32,Int32) -> Unit)

```cangjie
public func onScrollIndex(event: (Int32, Int32, Int32) -> Unit): This
```

**Function:** Triggered when the list starts scrolling. Triggered when scrolling starts due to finger dragging or dragging the scrollbar of the list. For animated scrolling triggered by the Scroller controller, this event is triggered when the animation starts.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | (Int32,Int32,Int32)->Unit | Yes | - | List scroll event callback.<br/>Parameter 1: Index of the first subcomponent within the List display area.<br/>Parameter 2: Index of the last subcomponent within the List display area.<br/>Parameter 3: Index of the subcomponent at the middle position within the List display area. |

## Basic Type Definitions

### class onScrollFrameBeginHandleResult

```cangjie
public class onScrollFrameBeginHandleResult {
    public var offsetRemain: Float64

    public init(offsetRemain!: Float64)
}
```

**Function:** Returns the actual scroll amount.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var offsetRemain

```cangjie
public var offsetRemain: Float64
```

**Function:** Actual scroll offset.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

#### init(Float64)

```cangjie
public init(offsetRemain!: Float64)
```

**Function:** Creates an actual scroll amount object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| offsetRemain | Float64 | Yes | - | Actual scroll offset, unit: vp. |

## Example Code

### Example 1 (Adding Scroll Events)

This example implements a vertical list and calls back the index when the current display interface changes.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.PerformanceAnalysisKit.*

func loggerInfo(str: String) {
    Hilog.info(0, "Cangjie### Example 2 (Setting Child Element Alignment)

This example demonstrates the alignment effects of child elements along the cross-axis direction in a List component under different ListItemAlign enumeration values.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let arr: Array<String> = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "12", "13", "14", "15",
        "16", "17", "18", "19"]
    @State var alignListItem: ListItemAlign = ListItemAlign.Start

    func build() {
        Column() {
            List(space: 20, initialIndex: 0) {
                ForEach(
                    this.arr,
                    itemGeneratorFunc: {
                        item: String, _: Int64 => ListItem() {
                            Text("${item}")
                            .width(100.percent)
                            .height(100)
                            .fontSize(16)
                            .textAlign(TextAlign.Center)
                            .borderRadius(10).backgroundColor(0xFFFFFF)
                        }.border(width: 2.px, color: Color.Green).width(55)
                    }
                )
            }
            .height(300)
            .width(90.percent)
            .border(width: 3.px, color: Color.Red)
            .lanes(6)
            .alignListItem(
                this.alignListItem)
            .scrollBar(BarState.Off)
            Button("Click to change alignListItem}").onClick(
                {
                 evt => match (this.alignListItem) {
                    case ListItemAlign.Start =>
                        this.alignListItem = ListItemAlign.Center
                    case ListItemAlign.Center =>
                        this.alignListItem = ListItemAlign.End
                    case ListItemAlign.End =>
                        this.alignListItem = ListItemAlign.Start
                    case _ => return
                }
            })
        }.width(100.percent).height(100.percent).backgroundColor(0xDCDCDC).padding(top: 5.px)
    }
}
```

![list2](figures/list2.gif)

### Example 3 (Setting Edit Mode)

This example demonstrates how to configure whether the current List component is in editable mode.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
  @State var arr:ObservedArrayList<Int64> = ObservedArrayList<Int64>([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
  @State var editFlag: Bool = false

  func build() {
    Stack(alignContent: Alignment.TopStart ) {
      Column() {
        List(space: 20, initialIndex: 0 ) {
          ForEach(this.arr, itemGeneratorFunc:{item: Int64,index: Int64  =>
            ListItem() {
              Flex(direction:FlexDirection.Row, alignItems:ItemAlign.Center) {
                Text("${item}" )
                  .width(100.percent)
                  .height(80)
                  .fontSize(20)
                  .textAlign(TextAlign.Center)
                  .borderRadius(10)
                  .backgroundColor(0xFFFFFF)
                  .flexShrink(1)
                if (this.editFlag) {
                  Button() {
                    Text("delete").fontSize(16)
                  }.width(30.percent).height(40)
                  .onClick({event =>
                    if (index >=0 && index<this.arr.size) {
                      //BaseLog.info( "${this.arr[index]}Delete")
                      this.arr.remove(index)
                      //Hilog.info(0, "AppLogCj", this.arr.size.toString())
                      this.editFlag = false
                   }
                  }).stateEffect(true)
                }
              }
            }
          })
        }.width(90.percent)
        .scrollBar(BarState.Off)
      }.width(100.percent)

      Button("edit list")
        .onClick({event=>
          this.editFlag = !this.editFlag
        }).margin(top: 5, left: 20 )
    }.width(100.percent).height(100.percent).backgroundColor(0xDCDCDC).padding(top: 5)
  }
}
```

![list3](figures/list3.gif)

### Example 4 (Setting Limit Alignment)

This example demonstrates the implementation effect of setting center limit alignment for a List component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Entry
@Component
class EntryView {
   let arr: ArrayList<Int64> =  ArrayList<Int64>([0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19])
   let scrollerForList = Scroller()

  func build() {
    Column() {
      Row() {
        List(space: 20, initialIndex: 3, scroller: this.scrollerForList ) {
          ForEach(this.arr, itemGeneratorFunc:{item:Int64,_:Int64=>
            ListItem() {
              Text("${item}")
                .width(100.percent).height(100).fontSize(16)
                .textAlign(TextAlign.Center)
            }
            .borderRadius(10).backgroundColor(0xFFFFFF)
            .width(60.percent)
            .height(80.percent)
          } )
        }
        .chainAnimation(true)
        .edgeEffect(EdgeEffect.Spring)
        .listDirection(Axis.Horizontal)
        .height(100.percent)
        .width(100.percent)
        .borderRadius(10.px)
        .backgroundColor(0xDCDCDC)
      }
      .width(100.percent)
      .height(100.percent)
      .backgroundColor(0xDCDCDC)
      .padding(top: 10.px )
    }
  }
}
```

![list4](figures/list4.gif)