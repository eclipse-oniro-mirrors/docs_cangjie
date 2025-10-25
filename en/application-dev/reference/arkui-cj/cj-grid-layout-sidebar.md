# SideBarContainer

Provides a sidebar container that can be shown or hidden. The sidebar and content area are defined through child components, where the first child component represents the sidebar and the second represents the content area.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain child components.

> **Note:**
>
> - Child component types: System components and custom components. Rendering control types are not supported ([if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), [LazyForEach](cj-state-rendering-lazyforeach.md)).
> - Number of child components: Must and only contain 2 child components.
> - When the number of child components is abnormal: For 3 or more child components, the first and second will be displayed. For 1 child component, the sidebar will be displayed, and the content area will be blank.

## Creating the Component

### init(SideBarContainerType, () -> Unit)

```cangjie
public init(sideBarType!: SideBarContainerType = SideBarContainerType.Embed, child!: () -> Unit = {=>})
```

**Function:** Creates a sidebar container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sideBarType | [SideBarContainerType](./cj-common-types.md#enum-sidebarcontainertype) | No | SideBarContainerType.Embed | Sets the display type of the sidebar.<br/>Initial value: SideBarContainerType.Embed. |
| child | () -> Unit | No | {=>} | Defines the sidebar and content area. |

## Common Attributes/Common Events

Common attributes: All supported.

Common events: All supported.

## Component Attributes

### func autoHide(Bool)

```cangjie
public func autoHide(value: Bool): This
```

**Function:** Sets whether the sidebar automatically hides when dragged to a width smaller than the minimum width.

> **Note:**
>
> - Affected by the minSideBarWidth attribute method. If minSideBarWidth is not set, the initial value is used.
> - Determines whether to auto-hide during dragging. Damping effect triggers hiding when the width is less than the minimum width (exceeds a certain distance).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the sidebar automatically hides when dragged to a width smaller than the minimum width.<br>true: Auto-hides.<br>false: Does not auto-hide.<br>Initial value: true. |

### func controlButton(ButtonStyle)

```cangjie
public func controlButton(value: ButtonStyle): This
```

**Function:** Sets the attributes of the sidebar control button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [ButtonStyle](#class-buttonstyle) | Yes | - | The attributes of the sidebar control button. |

### func divider(?DividerStyle)

```cangjie
public func divider(value: ?DividerStyle): This
```

**Function:** Sets the style of the divider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[DividerStyle](#class-dividerstyle) | Yes | - | **Named parameter.** The style of the divider. The divider is displayed by default. If the input is None, no action is taken, and the divider style remains consistent with the default. |

### func maxSideBarWidth(Length)

```cangjie
public func maxSideBarWidth(value: Length): This
```

**Function:** Sets the maximum width of the sidebar.

> **Note:**
>
> - If set to a value less than 0, the default value is used. The value cannot exceed the width of the sidebar container itself; if it does, the width of the sidebar container is used.
> - maxSideBarWidth takes precedence over the maxWidth of the sidebar child component. If maxSideBarWidth is not set, the default value has higher priority than the maxWidth of the sidebar child component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | Sets the maximum width of the sidebar.<br>Initial value: 280.vp.<br>Unit: vp. |

### func minContentWidth(Length)

```cangjie
public func minContentWidth(value: Length): This
```

**Function:** Sets the minimum width of the content area that can be displayed in the SideBarContainer component.

> **Note:**
>
> - If the minimum width is set to less than 0, the minimum width of the content area is 360.vp. If this attribute is not set, the content area can shrink to 0.
> - In the Embed scenario, when increasing the component size, only the content area size increases.
> - When decreasing the component size, the content area width is first reduced to minContentWidth. If the component size continues to decrease:
>
>     - If autoHide is false, the sidebar width remains at minSideBarWidth and the content area width remains at minContentWidth, but the content area will be truncated.
>     - If autoHide is true, the sidebar is hidden first, and then the content area width is reduced to minContentWidth. After that, the content area width remains unchanged, but the content area will be truncated.
>
> - minContentWidth takes precedence over the maxSideBarWidth and sideBarWidth attributes of the sidebar. If minContentWidth is not set, the default value has lower priority than the set minSideBarWidth and maxSideBarWidth attributes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The minimum width of the content area that can be displayed in the SideBarContainer component.<br>Initial value: 360.vp.<br>Unit: vp. |

### func minSideBarWidth(Length)

```cangjie
public func minSideBarWidth(value: Length): This
```

**Function:** Sets the minimum width of the sidebar.

> **Note:**
>
> - If set to a value less than 0, the default value is used. The value cannot exceed the width of the sidebar container itself; if it does, the width of the sidebar container is used.
> - minSideBarWidth takes precedence over the minWidth of the sidebar child component. If minSideBarWidth is not set, the default value has higher priority than the minWidth of the sidebar child component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The minimum width of the sidebar.<br>Initial value: 240.vp. |

### func showControlButton(Bool)

```cangjie
public func showControlButton(value: Bool): This
```

**Function:** Sets whether to display the control button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to display the control button.<br/>true: Displays the control button.<br/>false: Does not display the control button.<br/>Initial value: true. |

### func showSideBar(Bool)

```cangjie
public func showSideBar(value: Bool): This
```

**Function:** Sets whether to display the sidebar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to display the sidebar.<br/>true: Displays the sidebar.<br/>false: Does not display the sidebar.<br/>Initial value: true. |

### func sideBarPosition(SideBarPosition)

```cangjie
public func sideBarPosition(value: SideBarPosition): This
```

**Function:** Sets the display position of the sidebar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [SideBarPosition](./cj-common-types.md#enum-sidebarposition) | Yes | - | The display position of the sidebar.<br>Initial value: SideBarPosition.Start. |

### func sideBarWidth(Length)

```cangjie
public func sideBarWidth(value: Length): This
```

**Function:** Sets the width of the sidebar.

> **Note:**
>
> If set to a value less than 0, the default value is used. Restricted by the minimum and maximum widths; if outside the restricted range, the closest value is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The width of the sidebar.<br>Initial value: 240.vp.<br>Unit: vp. |

## Component Events

### func onChange((Bool) -> Unit)

```cangjie
public func onChange(callback: (Bool) -> Unit): This
```

**Function:** Triggered when the sidebar state switches between shown and hidden.

> **Note:**
>
> This event is triggered under any of the following conditions:
>
> - When the showSideBar attribute value changes.
> - When the showSideBar attribute adaptive behavior changes.
> - When dragging the divider triggers autoHide.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | (Bool)->Unit | Yes | - | Callback function. When the sidebar state changes from hidden to shown, the parameter value is true; when it changes from shown to hidden, the parameter value is false. |

## Basic Type Definitions

### class ButtonIconOptions

```cangjie
public class ButtonIconOptions {
    public var shown: ResourceStr
    public var hidden: ResourceStr
    public var switching: ResourceStr
    public init(shown!: ResourceStr, hidden!: ResourceStr, switching!: ResourceStr = "")
}
```

**Function:** Sets the icon of the sidebar control button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var hidden

```cangjie
public var hidden: ResourceStr
```

**Function:** Sets the icon of the control button when the sidebar is hidden.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var shown

```cangjie
public var shown: ResourceStr
```

**Function:** Sets the icon of the control button when the sidebar is shown.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var switching

```cangjie
public var switching: ResourceStr
```

**Function:** Sets the icon of the control button when the sidebar state is switching between shown and hidden.

**Type:** [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr)

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(ResourceStr, ResourceStr, ResourceStr)

```cangjie
public init(shown!: ResourceStr, hidden!: ResourceStr, switching!: ResourceStr = "")
```

**Function:** Constructs a ButtonIconOptions object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| shown | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Sets the icon of the control button when the sidebar is shown. |
| hidden | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | Sets the icon of the control button when the sidebar is hidden. |
| switching | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | Sets the icon of the control button when the sidebar state is switching between shown and hidden. |

### class ButtonStyle

```cangjie
public class ButtonStyle {
    public var left: Float64
    public var top: Float64
    public var width: Float64
    public var height: Float64
    public var icons: ButtonIconOptions
    public init(
        left!: Float64 = 16.0,
        top!: Float64 = 48.0,
        width!: Float64 = 24.0,
        height!: Float64 = 24.0,
        icons!: ButtonIconOptions = ButtonIconOptions(shown: "", hidden: "")
    )
}
```

**Function:** The attribute type of the sidebar control button.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var height

```cangjie
public var height: Float64
```

**Function:** **Named parameter.** Sets the height of the sidebar control button.<br>Unit: vp.

**Type:** Float64

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var icons

```cangjie
public var icons: ButtonIconOptions
```

**Function:** **Named parameter.** Sets the icon of the sidebar control button.

**Type:** [ButtonIconOptions](#class-buttoniconoptions)

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var left

```cangjie
public var left: Float64
```

**Function:** **Named parameter.** Sets the left margin of the sidebar control button from the container boundary.<br>Unit: vp.

**Type:** Float64

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var top

```cangjie
public var top: Float64
```

**Function:** **Named parameter.** Sets the top margin of the sidebar control button from the container boundary.<br>Unit: vp.

**Type:** Float64

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var width

```cangjie
public var width: Float64
```

**Function:** **Named parameter.** Sets the width of the sidebar control button.<br>Unit: vp.

**Type:** Float64

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Float64, Float64, Float64, Float64, ButtonIconOptions)

```cangjie
public init(
    left!: Float64 = 16.0,
    top!: Float64 = 48.0,
    width!: Float64 = 24.0,
    height!: Float64 = 24.0,
    icons!: ButtonIconOptions = ButtonIconOptions(shown: "", hidden: "")
)
```

**Function:** Constructs a ButtonStyle object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| left | Float64 | No | 16.0 | **Named parameter.** Sets the left margin of the sidebar control button from the container boundary.<br>Unit: vp. |
| top | Float64 | No | 48.0 | **Named parameter.** Sets the top margin of the sidebar control button from the container boundary.<br>Unit: vp. |
| width | Float64 | No | 24.0 | **Named parameter.** Sets the width of the sidebar control button.<br>Unit: vp. |
| height | Float## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.AppResource

@Entry
@Component
class EntryView {
    @State var arr: Array<Int64> = [1, 2, 3]
    @State var current: Int64 = 1
    var normalIcon: AppResource = @r(app.media.startIcon)
    let ctrlButton: ButtonStyle = ButtonStyle(left: 17.0, top: 49.0, width: 20.0, height: 31.0,
        icons: ButtonIconOptions(shown: "", hidden: "", switching: ""))
    func build() {
        SideBarContainer() {
            Column() {
                ForEach(
                    this.arr,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => Column() {
                            Image(this.normalIcon)
                                .width(50)
                                .height(50)
                            Text("Index${item}")
                                .fontSize(25)
                                .fontColor(0x0A59F7)
                                .fontFamily("source-sans-pro,cursive,sans-serif")
                        }.onClick({
                            event => this.current = idx
                        })
                    }
                )
            }
                .width(100.percent)
                .justifyContent(FlexAlign.SpaceEvenly)
                .backgroundColor(0x19000000)
            Column() {
                Text('SideBarContainer content text1')
                    .fontSize(20)
                Text('SideBarContainer content text2')
                    .fontSize(20)
            }
        }
            .id("SideBarDefault")
            .showSideBar(true)
            .showControlButton(true)
            .showControlButton(true)
            .autoHide(false)
            .sideBarWidth(150.vp)
            .minSideBarWidth(50.vp)
            .maxSideBarWidth(300.vp)
            .minContentWidth(1.vp)
            .sideBarPosition(SideBarPosition.Start)
            .controlButton(ctrlButton)
            .width(90.percent)
            .height(85.percent)
    }
}
```

![SideBarContainer](./figures/sidebarcontainer.gif)