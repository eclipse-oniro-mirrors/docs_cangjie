# ListItemGroup

This component is used to display grouped list items. By default, it fills the width of the [List](cj-scroll-swipe-list.md) component and must be used in conjunction with the List component.

> **Note:**
>
> - The parent component of this component can only be [List](cj-scroll-swipe-list.md).
> - The ListItemGroup component does not support setting the [universal attribute aspectRatio](cj-universal-attribute-layoutconstraints.md).
> - When the listDirection property of the parent List component is set to Axis.Vertical, setting the [universal attribute height](cj-universal-attribute-size.md) will not take effect. The height of ListItemGroup is the sum of the header height, footer height, and the total height of all ListItems after layout.
> - When the listDirection property of the parent List component is set to Axis.Horizontal, setting the [universal attribute width](cj-universal-attribute-size.md) will not take effect. The width of ListItemGroup is the sum of the header width, footer width, and the total width of all ListItems after layout.
> - The ListItem components within the current ListItemGroup do not support editing or dragging, meaning the editable property of ListItem components will not take effect.
> - Using the direction property to set the layout direction in ListItemGroup will not take effect. The layout direction of the ListItemGroup component follows the layout direction of its parent List component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Includes [ListItem](./cj-scroll-swipe-listitem.md) child components.

## Creating the Component

### init(CustomBuilder, CustomBuilder, Length, ListItemGroupStyle, () -> Unit)

```cangjie
public init(
    header!: CustomBuilder = {=>},
    footer!: CustomBuilder = {=>},
    space!: Length = 0.vp,
    style!: ListItemGroupStyle = ListItemGroupStyle.None,
    child!: () -> Unit
)
```

**Function:** Creates a ListItemGroup component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type                                                                    | Required | Default Value                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|:--------- |:--------------------------------------------------------------------- |:-------- |:------------------------------ |:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| header    | [CustomBuilder](./cj-common-types.md#type-custombuilder) | No       | { => }                         | **Named parameter.** Sets the header component of ListItemGroup.<br/>**Note:**<br/>Can contain a single child component or no child component. Use in combination with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and the bind method.                                                                                                                                                                                                                        |
| footer    | [CustomBuilder](./cj-common-types.md#type-custombuilder) | No       | { => }                         | **Named parameter.** Sets the footer component of ListItemGroup.<br/>**Note:**<br/>Can contain a single child component or no child component. Use in combination with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and the bind method.                                                                                                                                                                                                                        |
| space     | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)        | No       | 0.vp                           | **Named parameter.** Spacing between list items. Only applies between ListItem components, not between header and ListItem or footer and ListItem.<br/>Initial value: 0.<br/>Unit: vp.<br/>**Note:**<br/>If set to a negative value or a value greater than or equal to the length of the List content area, the initial value will be displayed.                                                                                                                                                                                                                   |
| style     | [ListItemGroupStyle](#enum-listitemgroupstyle)                        | No       | ListItemGroupStyle.None        | **Named parameter.** Sets the card style for the List component.<br/>Initial value: ListItemGroupStyle.NONE<br/>When set to ListItemGroupStyle.NONE, no style is applied. When set to ListItemGroupStyle.CARD, it is recommended to use it in conjunction with ListItemStyle.CARD for ListItem to display the default card style.<br/>In card style, the initial specifications for ListItemGroup are: left and right margins of 12.vp, and top, bottom, left, and right padding of 4.vp.<br/>In card style, default focus, hover, press, selected, and disable styles are provided for list items within the card.<br/>**Note:**<br/>In the current card mode, the default Axis.Vertical arrangement direction is used. If the listDirection property is set to Axis.Horizontal, it may cause display issues; the List property alignListItem defaults to ListItemAlign.Center, displaying centered alignment. |
| child     | ()->Unit                                                              | Yes      | -                              | Declares the child components of the container.                                                                                                                                                                                                                                                                                                                                                                                                                             |

## Universal Attributes/Events

Universal Attributes: All supported.

> **Note:**
>
> Does not support [setting the universal attribute aspectRatio](./cj-universal-attribute-layoutconstraints.md#func-aspectratiofloat64).

Universal Events: All supported.

## Component Attributes

### func divider(Option\<ListDividerOptions>)

```cangjie
public func divider(value: Option<ListDividerOptions>): This
```

**Function:** Used to set the divider style for ListItem. By default, there is no divider.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type                                                                                                               | Required | Default Value | Description     |
|:--------- |:---------------------------------------------------------------------------------------------------------------- |:-------- |:------------- |:-------------- |
| value     |Option<ListDividerOptions> | Yes      | -             | Divider style. |

## Basic Type Definitions

### class ListDividerOptions

```cangjie
public class ListDividerOptions {
    public var strokeWidth: Length
    public var color: ResourceColor = Color(0X08000000)
    public var startMargin: Length = 0.vp
    public var endMargin: Length = 0.vp
    public init(
        strokeWidth!: Length,
        color!: ResourceColor = Color.Black,
        startMargin!: Length = 0.vp,
        endMargin!: Length = 0.vp
    )
}
```

**Function:** Divider style for ListItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var color

```cangjie
public var color: ResourceColor = Color(0X08000000)
```

**Function:** Sets the color of the divider.

**Type:** [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var endMargin

```cangjie
public var endMargin: Length = 0.vp
```

**Function:** Sets the distance from the end side of the list to the divider.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var startMargin

```cangjie
public var startMargin: Length = 0.vp
```

**Function:** Sets the distance from the start side of the list to the divider.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### var strokeWidth

```cangjie
public var strokeWidth: Length
```

**Function:** Sets the width of the divider line.

**Type:** [Length](../BasicServicesKit/cj-apis-base.md#interface-length)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### init(Length, ResourceColor, Length, Length)

```cangjie
public init(
    strokeWidth!: Length,
    color!: ResourceColor = Color.Black,
    startMargin!: Length = 0.vp,
    endMargin!: Length = 0.vp
)
```

**Function:** Constructs the divider style for ListItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter     | Type                                                                    | Required | Default Value         | Description               |
|:------------- |:--------------------------------------------------------------------- |:-------- |:--------------------- |:------------------------ |
| strokeWidth   | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)        | Yes      | -                     | Width of the divider line.          |
| color         | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | No       | Color.Black           | Color of the divider line.          |
| startMargin   | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)        | No       | 0.vp                  | Distance from the start side of the list to the divider. |
| endMargin     | [Length](../BasicServicesKit/cj-apis-base.md#interface-length)        | No       | 0.vp                  | Distance from the end side of the list to the divider. |

### enum ListItemGroupStyle

```cangjie
public enum ListItemGroupStyle {
    | None
    | Card
    | ...
}
```

**Function:** Sets the card style for the List component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### Card

```cangjie
Card
```

**Function:** Displays the default card style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

#### None

```cangjie
None
```

**Function:** No style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## Example Code

### Example 1 (Setting Sticky Header/Footer)

This example demonstrates the sticky header and footer effects using the stick property.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

class TimeTable {
  let title: String
  let projects: Array<String>

    public init(title:String,projects: Array<String>){
        this.title = title
        this.projects = projects
    }
}

@Entry
@Component

class EntryView {
     let timeTable = [
        TimeTable("Monday", ["Chinese", "Math", "English"]),
        TimeTable("Tuesday", ["Physics", "Chemistry", "Biology"]),
        TimeTable("Wednesday", ["History", "Geography", "Politics"]),
        TimeTable("Thursday", ["Art", "Music", "PE"])]

      @Builder func itemHead(text:String) {
        Text(text)
        .fontSize(20)
        .backgroundColor(0xAABBCC)
        .width(100.percent)
        .padding(10)
    }

    @Builder func itemFoot(num:Int64) {
        Text("Total ${num} classes")
        .fontSize(16)
        .backgroundColor(0xAABBCC)
        .width(100.percent)
        .padding(5)
  }

    func build() {
        Column() {
            List(space: 20) {
                ForEach(this.timeTable, itemGeneratorFunc: {item:TimeTable ,_:Int64 =>
                        ListItemGroup(header:{=>bind(this.itemHead,this)(item.title)},footer:{=>bind(this.itemFoot,this)(item.projects.size)}){
                            ForEach(item.projects,itemGeneratorFunc: {project:String,_:Int64=>
                                    ListItem(){
                                        Text(project)
                                        .width(100.percent)
                                        .height(100)
                                        .fontSize(20)
                                        .textAlign(TextAlign.Center)
                                        .backgroundColor(0xFFFFFF)
                                    }})
                        }
                        })
             }
        }
        .height(800.vp)
        .backgroundColor(Color(0XD3D3D3))
    }
}
```

![list_item_group](figures/listitem_group1.gif)