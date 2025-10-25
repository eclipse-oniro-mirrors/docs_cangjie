# Tabs

A container component for switching content views through tabs, where each tab corresponds to a content view.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Custom components are not supported as child components. Only [TabContent](#class-tabcontent) child components are allowed, along with rendering control types [if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md) and [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md). Additionally, only TabContent is supported under if/else and ForEach, not custom components.

> **Note:**
>
> - When the visibility property of a Tabs child component is set to None or Hidden, the corresponding child component will not be displayed but will still occupy space within the viewport.
> - The TabContent child component of Tabs will not be destroyed after being displayed. For lazy loading and release of pages, refer to [Example 2](#示例2页面懒加载和释放).

## Creating the Component

### init(BarPosition, TabsController, Int32, () -> Unit)

```cangjie
public init(
    barPosition!: BarPosition = BarPosition.Start,
    controller!: TabsController = TabsController(),
    index!: Int32 = -1,
    child!: () -> Unit = {=>}
)
```

**Function:** Creates a Tabs container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| barPosition | [BarPosition](#enum-barposition) | No | BarPosition.Start | Sets the position of the Tabs' tab bar.<br/>Initial value: BarPosition.Start |
| controller | [TabsController](#class-tabscontroller) | No | TabsController() | Sets the Tabs controller.<br/>Initial value: TabsController() |
| index | Int32 | No | -1 | Sets the index of the currently displayed tab.<br/>Initial value: 0<br/>**Note:**<br/>Values less than 0 will display the initial value. Valid values are [0, number of TabContent child nodes - 1]. Directly modifying the index to switch pages will not trigger the transition animation. Using the TabController's changeIndex will enable the transition animation by default, which can be disabled by setting animationDuration to 0. |
| child | ()->Unit | No | { => } | Declares the child components within the container.<br/>Initial value: { => }. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func animationDuration(Float32)

```cangjie
public func animationDuration(value: Float32): This
```

**Function:** Sets the animation duration for switching TabContent when clicking the TabBar tab or calling the TabsController's changeIndex interface.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Float32 | Yes | - | The animation duration for switching TabContent when clicking the TabBar tab or calling the TabsController's changeIndex interface.<br/>Initial value: If this property is not set or set to an invalid value, and the TabBar is set to BottomTabBarStyle, the initial value is 0. For other TabBar styles, the initial value is 300.<br/>Unit: ms<br/>Range: [0, +∞). |

### func barHeight(Length)

```cangjie
public func barHeight(value: Length): This
```

**Function:** Sets the height of the TabBar. Values less than 0 or greater than the Tabs height will display the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The height of the TabBar.<br/>Initial value:<br/>When no styled TabBar is set and the vertical property is false, the initial value is 56.vp.<br/>When no styled TabBar is set and the vertical property is true, the initial value is the height of Tabs.<br/>When [SubTabBarStyle](./cj-common-types.md#enum-subtabbarstyle) is set and the vertical property is false, the initial value is 56.vp.<br/>When SubTabBarStyle is set and the vertical property is true, the initial value is the height of Tabs.<br/>When [BottomTabBarStyle](./cj-common-types.md#enum-bottomtabbarstyle) is set and the vertical property is true, the initial value is the height of Tabs.<br/>When BottomTabBarStyle is set and the vertical property is false, the initial value is 48.vp. |

### func barMode(BarMode)

```cangjie
public func barMode(value: BarMode): This
```

**Function:** Sets the layout mode of the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [BarMode](./cj-common-types.md#enum-barmode) | Yes | - | The layout mode. |

### func barWidth(Length)

```cangjie
public func barWidth(value: Length): This
```

**Function:** Sets the width of the TabBar. Values less than 0 or greater than the Tabs width will display the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The width of the TabBar.<br/>Initial value:<br/>When no [SubTabBarStyle](./cj-navigation-switching-tabs.md#class-subtabbarstyle) or [BottomTabBarStyle](./cj-navigation-switching-tabs.md#class-bottomtabbarstyle) is set and the vertical property is false, the initial value is the width of Tabs.<br/>When no SubTabBarStyle or BottomTabBarStyle is set and the vertical property is true, the initial value is 56.vp.<br/>When SubTabBarStyle is set and the vertical property is false, the initial value is the width of Tabs.<br/>When SubTabBarStyle is set and the vertical property is true, the initial value is 56.vp.<br/>When BottomTabBarStyle is set and the vertical property is true, the initial value is 96.vp.<br/>When BottomTabBarStyle is set and the vertical property is false, the initial value is the width of Tabs. |

### func scrollable(Bool)

```cangjie
public func scrollable(value: Bool): This
```

**Function:** Sets whether page switching can be performed by swiping the page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether page switching can be performed by swiping the page.<br/>Initial value: true, page switching can be performed by swiping. When false, page switching by swiping is disabled. |

### func vertical(Bool)

```cangjie
public func vertical(value: Bool): This
```

**Function:** Sets whether the Tab is vertical.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the Tab is vertical.<br/>Initial value: false, horizontal Tabs. When true, vertical Tabs.<br/>Try to keep the size of child components consistent across pages to avoid animation jumps during page switching. |

## Component Events

### func onChange(Callback\<Int32,Unit>)

```cangjie
public func onChange(event: Callback<Int32, Unit>): This
```

**Function:** Triggered after a Tab tab is switched.

This event is triggered under any of the following conditions:

1. When switching pages by swiping, the event is triggered after the component swipe animation ends.<br>

2. When the [controller](#class-tabscontroller) calls the [changeIndex](#func-changeindexint32) interface, the event is triggered after the Tab tab is switched.<br>

3. When dynamically modifying the index property value constructed by [state variables](./cj-state-rendering-appstatemanagement.md), the event is triggered after the Tab tab is switched.<br>

4. When clicking a TabBar tab, the event is triggered after the Tab tab is switched.

> **Note:**
>
> When using custom tabs, the onChange event may cause the tab linkage to execute only after the page is switched by swiping, resulting in a delay in the custom tab switching effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [Callback](../BasicServicesKit/cj-apis-base.md#type-callback)\<Int32,Unit> | Yes | - | The callback for the Tab tab switching event.<br/>Parameter:<br/>The index of the currently displayed tab, starting from 0. |

## Basic Type Definitions

### class TabContent

```cangjie
public class TabContent <: ContainerBase {
    public init(child: () -> Unit)
    public init()
}
```

**Function:** Used only within Tabs, corresponding to a content view for a switching tab.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [ContainerBase](./cj-ui-framework.md#containerbase)

#### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a TabContent container with child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| child | ()->Unit | Yes | - | Declares the child components within the container. |

#### init()

```cangjie
public init()
```

**Function:** Creates a TabContent container without child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func tabBar(ResourceStr)

```cangjie
public func tabBar(content: ResourceStr): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| content | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | The content displayed on the TabBar. |

#### func tabBar(ResourceStr, ResourceStr)

```cangjie
public func tabBar(icon!: ResourceStr = "", text!: ResourceStr = ""): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| icon | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The icon displayed on the TabBar.<br/>**Note:** If the icon uses an SVG image source, the SVG image source should remove its own width and height attributes. If an SVG image source with its own width and height attributes is used, the icon size will be the built-in width and height attribute values of the SVG itself. |
| text | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The text content displayed on the TabBar. |

#### func tabBar(CustomBuilder)

```cangjie
public func tabBar(content: CustomBuilder): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| content | [CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | The content displayed on the TabBar.<br/>CustomBuilder: A builder that can pass in components internally. |

### class TabsController

```cangjie
public class TabsController {
    public init()
}
```

**Function:** The controller for the Tabs component, used to control the Tabs component for tab switching. A single TabsController cannot control multiple Tabs components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init()

```cangjie
public init()
```

**Function:** Creates a Tabs controller.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func changeIndex(Int32)

```cangjie
public func changeIndex(value: Int32): Unit
```

**Function:** Controls the Tabs to switch to the specified tab.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The index value of the tab in Tabs, starting from 0.<br/>**Note:**<br/>Values less than 0 or greater than the maximum number will default to the initial value of 0. |

### enum BarMode

```cangjie
public enum BarMode <: Equatable<BarMode> {
    | Fixed
    | Scrollable
    | ...
}
```

**Function:** Enumeration for TabBar layout modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<BarMode>

#### Fixed

```cangjie
Fixed
```

**Function:** All TabBars evenly divide the screen width, and the TabBar cannot scroll.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Scrollable

```cangjie
Scrollable
```

**Function:** All TabBars are laid out according to their own dimensions, and the TabBar can scroll.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(BarMode)

```cangjie
public operator func !=(other: BarMode): Bool
```

**Function:** Compares whether two BarModes are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [BarMode](#enum-barmode) | Yes | - | The other BarMode value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two BarModes are not equal, otherwise returns false. |

#### func ==(BarMode)

```cangjie
public operator func ==(other: BarMode): Bool
```

**Function:** Compares whether two BarModes are equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [BarMode](#enum-barmode) | Yes | - | The other BarMode value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two BarModes are equal, otherwise returns false. |

### enum BarPosition

```cangjie
public enum BarPosition <: Equatable<BarPosition> {
    | Start
    | End
    | ...
}
```

**Function:** Sets the layout position of the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<BarPosition>

#### End

```cangjie
End
```

**Function:** Positioned at the end.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Start

```cangjie
Start
```

**Function:** Positioned at the start.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(BarPosition)

```cangjie
public operator func !=(other: BarPosition): Bool
```

**Function:** Compares whether two BarPositions are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [BarPosition](#enum-barposition) | Yes | - | The other BarPosition value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two BarPositions are not equal, otherwise returns false. |

#### func ==(BarPosition)

```cangjie
public operator func ==(other: BarPosition): Bool
```

**Function:** Compares whether two BarPositions are equal.

**Parameters:**

| Parameter Name | Type |## Sample Code

### Example 1 (Custom Tab Switching Synchronization)

This example demonstrates custom synchronization between tabBar and TabContent during switching via onChange.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import std.collection.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var fontColor: UInt32 = 0x182431
    @State var selectedFontColor: UInt32 = 0x007DFF
    @State var currentIndex: Int32 = 0
    @State var selectedIndex: Int32 = 0
    var controller: TabsController = TabsController()

    func getFontColor(index: Int32): UInt32 {
        if (this.selectedIndex == index) {
            return this.selectedFontColor
        }
        return this.fontColor
    }

    func getFontWeight(index: Int32): FontWeight {
        if (this.selectedIndex == index) {
            return FontWeight.W400
        }
        return FontWeight.W500
    }

    func getOpacity(index: Int32): Int64 {
        if (this.selectedIndex == index) {
            return 1
        }
        return 0
    }

    @Builder
    func tabBuilder(index: Int32, name: String) {
        Column() {
            Text(name)
            .fontColor(this.getFontColor(index))
            .fontSize(16)
            .fontWeight(this.getFontWeight(index))
            .lineHeight(22)
            .margin(top: 17, bottom: 7)
            Divider()
            .strokeWidth(2)
            .color(0x007DFF)
        }.width(100.percent)
    }

    func build() {
        Column() {
            Tabs(barPosition: BarPosition.Start, controller: this.controller, index: this.currentIndex) {
                TabContent() {
                    Column().width(100.percent).height(100.percent).backgroundColor(0x00CB87)
                }.tabBar({=>bind(this.tabBuilder, this)(0, "green")})

                TabContent() {
                    Column().width(100.percent).height(100.percent).backgroundColor(0x007DFF)
                }.tabBar({=>bind(this.tabBuilder, this)(1,"blue")})

                TabContent() {
                    Column().width(100.percent).height(100.percent).backgroundColor(0xFFBF00)
                }.tabBar({=>bind(this.tabBuilder, this)(2,"yellow")})

                TabContent() {
                    Column().width(100.percent).height(100.percent).backgroundColor(0xE67C92)
                }.tabBar({=>bind(this.tabBuilder, this)(3, "pink")})
              }
            .vertical(false)
            .barMode(BarMode.Fixed)
            .barWidth(360)
            .barHeight(56)
            .animationDuration(400.0)
            .onChange({index: Int32 =>
                // currentIndex controls the displayed tab of TabContent
                this.currentIndex = index
            })
            .width(360)
            .height(296)
            .margin(top: 52)
            .backgroundColor(0xF1F3F5)

        }.width(100.percent)
    }
}
```

![tab](figures/tabsExample1.gif)

### Example 2 (Lazy Loading and Release of Pages)

This example demonstrates lazy loading and release of pages using custom TabBar with Swiper and LazyForEach.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import kit.PerformanceAnalysisKit.Hilog
import std.collection.*
import ohos.arkui.state_macro_manage.*

class MyDataSource <: IDataSource<String> {
  public MyDataSource(let list: ArrayList<String> ) {}

  public func totalCount(): Int64 {
    return this.list.size
  }

  public func getData(index: Int64): String {
    return this.list[index]
  }

  public func onRegisterDataChangeListener(listener: DataChangeListener): Unit {
  }

  public func onUnregisterDataChangeListener(listener: DataChangeListener): Unit {
  }
}

@Entry
@Component
class EntryView {
    @State var fontColor: Color = Color(0x182431)
    @State var selectedFontColor: Color = Color(0x007DFF)
    @State var currentIndex: Int32 = 0
    var list: ArrayList<String> = ArrayList<String>()
    var tabsController: TabsController = TabsController()
    var swiperController: SwiperController = SwiperController()
    var swiperData: MyDataSource = MyDataSource(ArrayList<String>())

    protected override func aboutToAppear() {
        for (i in 0..9) {
          this.list.add("${i}");
        }
        this.swiperData = MyDataSource(this.list)
    }

    @Builder
    func tabBuilder(index: Int32, name: String) {
        Column() {
            Text(name)
            .fontColor(if(this.currentIndex == index) {this.selectedFontColor} else {this.fontColor})
            .fontSize(16)
            .fontWeight(if(this.currentIndex == index) {FontWeight.W500} else {FontWeight.W400})
            .lineHeight(22)
            .margin(top: 17, bottom: 7)

            Divider()
            .strokeWidth(2)
            .color(0x007DFF)
            .opacity(if(this.currentIndex == index) {1.0} else {0.0})
        }.width(20.percent)
    }

    func build() {
        Column() {
            Tabs(barPosition: BarPosition.Start, controller: this.tabsController) {
                ForEach(this.list, itemGeneratorFunc:{item: String, index: Int64 =>
                    TabContent(){}.tabBar({=>bind(this.tabBuilder, this)(Int32(index), 'Tab ${this.list[index]}')})
                })
            }
            .id("TabsExample12")
            .barMode(BarMode.Scrollable)
            .backgroundColor(0xF1F3F5)
            .height(56)
            .width(100.percent)

            Swiper(controller: this.swiperController) {
                LazyForEach(this.swiperData, itemGeneratorFunc: {item: String, idx: Int64 =>
                    Text(item)
                    .onAppear({=>
                      Hilog.info(0, "AppLogCj", 'onAppear ' + item)
                    })
                    .onDisAppear({=>
                      Hilog.info(0, "AppLogCj", 'onDisAppear ' + item)
                    })
                    .width(100.percent)
                    .height(100.percent)
                    .backgroundColor(0xAFEEEE)
                    .textAlign(TextAlign.Center)
                    .fontSize(30)
                })
            }
            .loop(false)
            .onChange({index: Int32 =>
                this.currentIndex = index
                this.tabsController.changeIndex(index)
            })
        }
    }
}
```

![tab](figures/tabsExample12.gif)

### Example 3 (Setting TabBar Layout Mode)

This example demonstrates both evenly distributed tab layout and actual-length-based layout via barMode, showing scrollable effects when the total tab length exceeds TabBar's width.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import std.collection.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView{
    @State var text: String = "Text"
    @State var barMode: BarMode = BarMode.Fixed

    func build(){
        Column(){
            Row(){
                Button("Add Text ")
                .width(47.percent)
                .height(50)
                .onClick({event => this.text += "Text"})
                .margin(right: 6.percent, bottom: 12)

                Button("Reset Text")
                .width(47.percent)
                .height(50)
                .onClick({event => this.text = "Text"})
                .margin(bottom: 12)
            }

            Row(){
                Button("BarMode.Fixed")
                .width(47.percent)
                .height(50)
                .onClick({event => this.barMode = BarMode.Fixed})
                .margin(right: 6.percent, bottom: 12)

                Button("BarMode.Scrollable")
                .width(47.percent)
                .height(50)
                .onClick({event => this.barMode = BarMode.Scrollable})
                .margin(bottom: 12)
            }
            Tabs(){
                TabContent(){
                    Column().width(100.percent).height(100.percent).backgroundColor(0xFEC0CD)
                }.tabBar(this.text)

                TabContent(){
                    Column().width(100.percent).height(100.percent).backgroundColor(Color.Green)
                }.tabBar(this.text)

                TabContent(){
                    Column().width(100.percent).height(100.percent).backgroundColor(Color.Blue)
                }.tabBar(this.text)
            }
            .height(60.percent)
            .backgroundColor(0xf1f3f5)
            .barMode(this.barMode)
        }
        .width(100.percent)
        .height(500)
        .padding(24)
    }
}
```

![tab](figures/tabsExample13.gif)