# Web Component Nested Scrolling

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

A typical application scenario for nested scrolling in web components is when a page contains multiple independent areas that require scrolling. When users scroll the content of a web area, it can drive other scrollable areas to achieve a seamless vertical page scrolling experience.

For web components embedded in scrollable containers ([Scroll](../reference/arkui-cj/cj-scroll-swipe-scroll.md), [List](../reference/arkui-cj/cj-scroll-swipe-list.md)), they need to handle swipe gesture events by interfacing with the ArkUI framework's [NestedScrollMode](../reference/arkui-cj/cj-common-types.md#enum-nestedscrollmode) enumeration type. This enables web components to nest within ArkUI scrollable containers for nested scrolling. Developers can specify the default nested scrolling mode during web component creation using the [nestedScroll](../reference/arkui-cj/cj-web-web.md#func-nestedscrollnestedscrollmode-nestedscrollmode) property interface, and can also dynamically change the nested scrolling mode during runtime.

The nestedScroll interface takes two parameters: scrollForward and scrollBackward, both of which are of the [NestedScrollMode](../reference/arkui-cj/cj-common-types.md#enum-nestedscrollmode) enumeration type.

When a web component is nested within multiple scrollable container components, any unconsumed offset or velocity values in the same direction as the parent component will be passed to the nearest parent component with matching direction, allowing the parent component to continue scrolling. A single gesture can only trigger nested scrolling along either the X-axis or Y-axis. When a gesture involves diagonal movement, the scrolling direction will follow the axis with the larger absolute value of offset or velocity. If the absolute values are equal on both axes, the scrolling direction will follow that of the nearest scrollable component to the web component.

> **Note:**
>
> - Containers supporting nested scrolling: [Grid](../reference/arkui-cj/cj-scroll-swipe-grid.md), [List](../reference/arkui-cj/cj-scroll-swipe-list.md), [Scroll](../reference/arkui-cj/cj-scroll-swipe-scroll.md), [Swiper](../reference/arkui-cj/cj-scroll-swipe-swiper.md), [Tabs](../reference/arkui-cj/cj-navigation-switching-tabs.md), [Refresh](../reference/arkui-cj/cj-scroll-swipe-refresh.md), [bindSheet](../reference/arkui-cj/cj-animation-transition.md).
> - Input events supporting nested scrolling: gestures, mouse, and touchpad.

<!-- compile -->

```cangjie
// index.cj
import ohos.arkui.state_macro_manage.*
import kit.ArkWeb.WebviewController
import kit.ArkUI.*

@Entry
@Component
class EntryView {
    var scrollerForScroll: Scroller = Scroller()
    let controller = WebviewController()
    let controller2 = WebviewController()
    // When NestedScrollMode is set to SelfOnly, the web page won't interact with parent components when reaching edges.
    @State
    var nestedScrollMode0: NestedScrollMode = NestedScrollMode.SelfOnly
    // When NestedScrollMode is set to SelfFirst, parent components continue scrolling after web page reaches edges.
    @State
    var nestedScrollMode1: NestedScrollMode = NestedScrollMode.SelfFirst
    // When NestedScrollMode is set to ParentFirst, parent components scroll first, then notify web to scroll after reaching edges.
    @State
    var nestedScrollMode2: NestedScrollMode = NestedScrollMode.ParentFirst
    // When NestedScrollMode is set to Parallel, parent components and web scroll simultaneously.
    @State
    var nestedScrollMode3: NestedScrollMode = NestedScrollMode.Parallel
    @State
    var nestedScrollModeF: NestedScrollMode = NestedScrollMode.SelfFirst
    @State
    var nestedScrollModeB: NestedScrollMode = NestedScrollMode.SelfFirst
    // Vertical scrolling for scroll
    @State
    var scrollDirection: ScrollDirection = ScrollDirection.Vertical

    func build() {
        Flex() {
            Scroll(this.scrollerForScroll) {
                Column(space: 5) {
                    Row() {
                        Text('Switch Forward Scroll Mode').fontSize(5)
                        Button("SelfOnly").onClick ({ evt =>
                            this.nestedScrollModeF = this.nestedScrollMode0
                        }).fontSize(5)
                        Button("SelfFirst").onClick ({ evt =>
                            this.nestedScrollModeF = this.nestedScrollMode1
                        }).fontSize(5)
                        Button("ParentFirst").onClick ({ evt =>
                            this.nestedScrollModeF = this.nestedScrollMode2
                        }).fontSize(5)
                        Button("Parallel").onClick ({ evt =>
                            this.nestedScrollModeF = this.nestedScrollMode3
                        }).fontSize(5)
                    }
                    Row() {
                        Text('Switch Backward Scroll Mode').fontSize(5)
                        Button("SelfOnly").onClick ({ evt =>
                            this.nestedScrollModeB = this.nestedScrollMode0
                        }).fontSize(5)
                        Button("SelfFirst").onClick ({ evt =>
                            this.nestedScrollModeB = this.nestedScrollMode1
                        }).fontSize(5)
                        Button("ParentFirst").onClick ({ evt =>
                            this.nestedScrollModeB = this.nestedScrollMode2
                        }).fontSize(5)
                        Button("Parallel").onClick ({ evt =>
                            this.nestedScrollModeB = this.nestedScrollMode3
                        }).fontSize(5)
                    }
                    Text('Current Forward Nested Scroll Mode ---nestedScrollModeF').fontSize(10)
                    Text('Current Backward Nested Scroll Mode ---nestedScrollModeB').fontSize(10)
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(10.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(10.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(10.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                    // Replace src with valid address or resource file
                    Web(src: "www.example.com", controller: this.controller)
                        .nestedScroll(
                            scrollForward: this.nestedScrollModeF,
                            scrollBackward: this.nestedScrollModeB
                        )
                        .height(40.percent)
                        .width(100.percent)

                    Text("Scroll Area")
                        .width(100.percent)
                        .height(20.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(20.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                    // Replace src with valid address or resource file
                    Web(src: "www.example.com", controller: this.controller2)
                        .nestedScroll(
                            scrollForward: this.nestedScrollModeF,
                            scrollBackward: this.nestedScrollModeB
                        )
                        .height(40.percent)
                        .width(90.percent)
                    Text("Scroll Area")
                        .width(100.percent)
                        .height(20.percent)
                        .backgroundColor(0X330000FF)
                        .fontSize(16)
                        .textAlign(TextAlign.Center)
                }.width(95.percent).border( width: 5 )
            }.width(100.percent).height(120.percent).border(width: 5).scrollable(this.scrollDirection)
        }.width(100.percent).height(100.percent).backgroundColor(0xDCDCDC).padding(20)
    }
}
```

![web-nested-scrolling](figures/web-nested-scrolling.gif)