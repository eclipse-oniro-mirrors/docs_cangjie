# Creating Lists

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

A list is a complex container that automatically provides scrolling functionality when the number of list items exceeds the screen size. It is suitable for displaying homogeneous data types or datasets, such as images and text. Presenting data collections in lists is a common requirement in many applications (e.g., contact lists, music playlists, shopping lists, etc.).

Using lists enables efficient display of structured, scrollable information. By linearly arranging child components [ListItemGroup](../reference/arkui-cj/cj-scroll-swipe-listgroup.md) or [ListItem](../reference/arkui-cj/cj-scroll-swipe-listitem.md) vertically or horizontally within the [List](../reference/arkui-cj/cj-scroll-swipe-list.md) component, individual views can be provided for rows or columns in the list. Alternatively, [iterative rendering](./rendering_control/cj-rendering-control-foreach.md) can be used to iterate through a set of rows or columns, or a combination of single views and ForEach structures can be mixed to build a list. The List component supports rendering control methods such as conditional rendering, iterative rendering, and lazy loading to generate child components.

## Layout and Constraints

As a container, a list automatically arranges its child components along its scrolling direction. Adding or removing components from the list will reorder the child components.

As shown in **Figure 1**, in a vertical list, the List automatically arranges ListItemGroup or ListItem vertically.

ListItemGroup is used for grouped display of list data, and its child components are also ListItems. A ListItem represents a single list item and can contain one child component.

**Figure 1** Relationship Between List, ListItemGroup, and ListItem Components

![List](figures/List.png)

> **Note:**
>
> The child components of List must be ListItemGroup or ListItem. ListItem and ListItemGroup must be used in conjunction with List.

### Layout

In addition to providing vertical and horizontal layout capabilities and adaptive scrolling when content exceeds the screen, List also offers layout capabilities for adaptive cross-axis arrangement.

Vertical layout can be used to build single-column or multi-column vertical scrolling lists, as shown in **Figure 2**.

**Figure 2** Vertical Scrolling Lists (Left: Single Column; Right: Multiple Columns)

![List1](figures/List1.png)

Horizontal layout can be used to build single-row or multi-row horizontal scrolling lists, as shown in **Figure 3**.

**Figure 3** Horizontal Scrolling Lists (Left: Single Row; Right: Multiple Rows)

![List2](figures/List2.png)

Grid can also achieve single-column or multi-column layouts. If each column has equal width and no cross-row or cross-column layout is needed, List is recommended over Grid.

### Constraints

The main axis direction of a list refers to the arrangement direction of the child component columns and is also the scrolling direction of the list. The axis perpendicular to the main axis is called the cross axis, and its direction is orthogonal to the main axis.

As shown in **Figure 4**, the main axis of a vertical list is the vertical direction, and the cross axis is the horizontal direction. The main axis of a horizontal list is the horizontal direction, and the cross axis is the vertical direction.

**Figure 4** Main Axis and Cross Axis of a List

![List3](figures/List3.png)

If the List component has dimensions set for its main or cross axis, the corresponding dimension will be the set value.

If the List component's main axis dimension is not set, when the total main axis dimension of the List's child components is less than the parent component's dimension, the List's main axis dimension will automatically adapt to the total dimension of the child components.

As shown in **Figure 5**, when a vertical list B does not have a height set, and its parent component A has a height of 200.vp, if the total height of all its child components C is 150.vp, the height of list B will be 150.vp.

**Figure 5** Example 1 of Main Axis Height Constraint (**A**: Parent Component of List; **B**: List Component; **C**: All Child Components of List)

![List4](figures/List4.png)

If the total main axis dimension of the child components exceeds the parent component's dimension, the List's main axis dimension will adapt to the parent component's dimension.

As shown in **Figure 6**, for the same vertical list B without a set height, if its parent component A has a height of 200.vp and the total height of all its child components C is 300.vp, the height of list B will be 200.vp.

**Figure 6** Example 2 of Main Axis Height Constraint (**A**: Parent Component of List; **B**: List Component; **C**: All Child Components of List)

![List5](figures/List5.png)

When the List component's cross axis dimension is not set, its dimension defaults to adapting to the parent component's dimension.

## Developing Layouts

### Setting the Main Axis Direction

The main axis of the List component defaults to the vertical direction, meaning a vertical scrolling list can be built without manually setting the List direction.

For horizontal scrolling lists, set the listDirection property of List to Axis.Horizontal. The default value of listDirection is Axis.Vertical, meaning the main axis is vertical by default.

```cangjie
List() {
  // ...
}
.listDirection(Axis.Horizontal)
```

### Setting Cross-Axis Layout

The cross-axis layout of the List component can be configured using the lanes and alignListItem properties. The lanes property determines the number of list items arranged along the cross axis, and alignListItem sets the alignment of child components along the cross axis.

The lanes property of the List component is typically used to adaptively build lists with varying numbers of rows or columns across different device sizes, enabling one development for multiple deployments. The declaration method for the lanes property is described in [Declaration Method](../reference/arkui-cj/cj-scroll-swipe-list.md#func-lanesint32). For a vertical list, setting lanes to 2 means building a two-column vertical list, as shown in the right image of **Figure 2**. The default value of lanes is 1, meaning a vertical list defaults to one column.

```cangjie
List() {
  // ...
}
.lanes(2)
```

When using ".lanes(minLength: Length, maxLength: Length)" to declare the property, the number of rows or columns is adaptively determined based on minLength and maxLength relative to the List component's dimensions.

```cangjie
List() {
  // ...
}
.lanes(minLength: 200, maxLength: 300)
```

For example, suppose minLength is set to 200 and maxLength to 300 for a vertical list:
- When the List component's width is 300.vp, since minLength is 200.vp, the list will have one column.
- When the List component's width changes to 400.vp, meeting twice the minLength, the list will adaptively switch to two columns.

For a vertical list, setting alignListItem to ListItemAlign.Center means the list items are center-aligned horizontally. The default value of alignListItem is ListItemAlign.Start, meaning list items are aligned to the start of the cross axis by default.

```cangjie
List() {
  // ...
}
.alignListItem(ListItemAlign.Center)
```

## Displaying Data in Lists

List views display collections of items vertically or horizontally, providing scrolling functionality when rows or columns exceed the screen size, making them suitable for displaying large datasets. In its simplest form, a List statically creates the content of its ListItems.

**Figure 7** City List

![List6](figures/List6.png)

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
public class EntryView {
    func build() {
        List() {
            ListItem() {
                Text('Beijing').fontSize(24)
            }

            ListItem() {
                Text('Hangzhou').fontSize(24)
            }

            ListItem() {
                Text('Shanghai').fontSize(24)
            }
        }
        .backgroundColor(0xfff1f3f5)
        .alignListItem(ListItemAlign.Center)
    }
}
```

Since a ListItem can only have one root node component and does not support multiple components laid out flat, if a list item consists of multiple component elements, these elements must be combined into a container component or a custom component.

**Figure 8** Example of a Contact List Item

![List7](figures/List7.png)

As shown in **Figure 8**, each contact in the contact list has an avatar and a name. Here, the Image and Text must be encapsulated within a Row container.

```cangjie
List() {
    ListItem() {
        Row() {
            Image(@r(app.media.startIcon))
                .width(40)
                .height(40)
                .margin(10)
            Text('Xiao Ming').fontSize(20)
        }
    }
    ListItem() {
        Row() {
            Image(@r(app.media.startIcon))
                .width(40)
                .height(40)
                .margin(10)
            Text('Xiao Hong').fontSize(20)
        }
    }
}
```

## Iterating List Content

Typically, applications dynamically create lists from data collections. Using [iterative rendering](./rendering_control/cj-rendering-control-foreach.md), data can be iteratively fetched from a data source, and corresponding components can be created during each iteration, reducing code complexity.

Cangjie provides component iterative rendering capabilities through [ForEach](./rendering_control/cj-rendering-control-foreach.md). Taking a simple contact list as an example, contact names and avatar data are stored in the contacts array using the Contact class structure. ForEach nested with ListItem replaces multiple flat, similar ListItems, reducing repetitive code.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

public class Contact {
    var name: String
    var icon: AppResource

    public init(name: String, icon: AppResource) {
        this.name = name
        this.icon = icon
    }
}

@Entry
@Component
public class EntryView {
    private var contacts: Array<Contact> = [Contact('Xiao Ming', @r(app.media.startIcon)), Contact('Xiao Hong', @r(app.media.startIcon))]
    func build() {
        List() {
            ForEach(this.contacts, itemGeneratorFunc: { item: Contact, _: Int64 =>
                    ListItem() {
                        Row() {
                            Image(item.icon)
                                .width(40)
                                .height(40)
                                .margin(10)
                            Text(item.name).fontSize(20)
                        }
                            .width(100.percent)
                            .justifyContent(FlexAlign.Start)
                    }
                },
                keyGeneratorFunc: {item: Contact, idx: Int64 => idx.toString()}
            )
        }.width(100.percent)
    }
}
```

In the List component, ForEach can be used not only to iteratively render ListItems but also to render ListItemGroups. For detailed usage of iterative rendering for ListItemGroup, refer to [ListItemGroup](../arkui-cj/cj-layout-development-create-list.md#supporting-grouped-lists).

## Customizing List Styles

### Setting Content Spacing

When initializing a list, if spacing between list items is needed, the space parameter can be used. For example, adding 10.vp spacing along the main axis between each list item:

```cangjie
List(space: 10) {
  // ...
}
```

### Adding Dividers

Dividers separate interface elements, making individual elements easier to identify. As shown in **Figure 9**, when list items have icons (e.g., Bluetooth icons) on the left, the icons themselves provide good differentiation, so the divider can start displaying after the icon.

**Figure 9** Setting List Divider Styles

![List8](figures/List8.png)

The List component provides the divider property to add dividers between list items. When setting the divider property, the strokeWidth and color properties can be used to configure the thickness and color of the divider.

The startMargin and endMargin properties set the distance from the divider to the start and end edges of the list, respectively.

```cangjie
List() {
  // ...
}
.divider(strokeWidth: 1, color: 0xffe9f0f0, startMargin: 60, endMargin: 10)
```

This example draws a 1.vp thick divider starting 60.vp from the list's start edge and ending 10.vp from the end edge, achieving the divider style shown in **Figure 9**.

> **Note:**
>
> - The width of the divider creates spacing between ListItems. If the spacing set for the List is less than the divider width, the spacing between ListItems will use the divider width.
>
> - When the List has multiple columns, the startMargin and endMargin of the divider apply to each column.
>
> - The List component's divider is drawn between two ListItems. No divider is drawn above the first ListItem or below the last ListItem.

### Adding Scrollbars

When the height (or width) of list items exceeds the screen height (or width), the list can scroll vertically (or horizontally). When there is a lot of content, users can quickly locate items by dragging the scrollbar, as shown in **Figure 10**.

**Figure 10** List Scrollbar

![List9](figures/List9.gif)

For the List component, the scrollBar property controls the display of the scrollbar. The scrollBar property takes a value of type [BarState](../reference/arkui-cj/cj-common-types.md#enum-barstate). When set to BarState.Auto, the scrollbar is displayed on demand. In this case, the scrollbar appears when touching the scrollbar area, allowing quick content browsing by dragging up or down. The scrollbar thickens during dragging and disappears automatically after 2 seconds of inactivity.

```cangjie
List() {
    // ...
}
.scrollBar(BarState.Auto)
```

## Supporting Grouped Lists

Grouping data in lists enhances clarity and ease of navigation, improving efficiency. Grouped lists are common in real-world applications, as shown in the contact list in **Figure 11**.

**Figure 11** Grouped Contact List

![List10](figures/List10.png)

Using ListItemGroup within the List component to group items enables the creation of two-dimensional lists.

ListItemGroup components can be used directly within the List component, with their width defaulting to fill the List component. When initializing ListItemGroup, the header parameter can set the header component for the list group.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

@Entry
@Component
public class EntryView {
    @Builder
    public func itemHead(text: String) {
        // Header component for the list group, corresponding to the component for group labels like A, B, etc.
        Text(text)
            .fontSize(20)
            .backgroundColor(0xfff1f3f5)
            .width(100.percent)
            .padding(5)
    }

    func build() {
        List() {
            ListItemGroup(
                header: this.itemHead("A")){
                    =>
                    // Iteratively render ListItems for group A
                }

            ListItemGroup(
                header: this.itemHead("B")) {
                    =>
                    // Iteratively render ListItems for group B
                }
        }
    }
}
```

If multiple ListItemGroups have similar structures, the data for each group can be combined into an array, and ForEach can be used to iteratively render multiple groups. For example, in a contact list, combine the contacts data (refer to [Iterating List Content](#iterating-list-content)) and the corresponding group title into an array contactsGroups. Then, use ForEach to iteratively render contactsGroups, achieving a grouped contact list. Refer to the sample code in [Adding Sticky Headers](#adding-sticky-headers).

## Adding Sticky Headers

Sticky headers are a common pattern for positioning header elements in alphabetical lists. As shown in **Figure 12**, when scrolling section A in the contact list, the header for section B remains positioned below A. When scrolling section B begins, its header sticks to the top of the screen until all items in B have scrolled past, after which it is replaced by the next header.

Sticky headers not only clarify the representation and purpose of data in the list but also help users locate data within large information sets, avoiding repetitive scrolling between the top of the list and the area of interest.

**Figure 12** Sticky Headers

![List11](figures/List11.gif)

The sticky property of the List component works with ListItemGroup to set whether the header component of ListItemGroup sticks to the top or the footer component sticks to the bottom.

Setting the sticky property of the List component to StickyStyle.Header achieves sticky header effects. For sticky footer effects, initialize the footer component of ListItemGroup using the footer parameter and set the sticky property to StickyStyle.Footer.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import ohos.arkui.state_macro_manage.*
import ohos.resource.*
import kit.ArkUI.*

public class Contact {
    var name: String
    var icon: AppResource

    public init(name: String, icon: AppResource) {
        this.name = name
        this.icon = icon
    }
}

public class ContactGroup {
    var title: String
    var contacts: Array<Contact>

    public init(title: String, contacts: Array<Contact>) {
        this.title = title
        this.contacts = contacts
    }
}

@Entry
@Component
public class EntryView {
    // Define the grouped contacts data array contactsGroups
    private var contactsGroups : Array<ContactGroup> = [
            ContactGroup('A', [Contact('Ai Jia', @r(app.media.startIcon)),Contact('An An', @r(app.media.startIcon)),Contact('Angela', @r(app.media.startIcon))]),
            ContactGroup('B', [Contact('Bai Ye', @r(app.media.startIcon)),Contact('Bo Ming', @r(app.media.startIcon))])
        ]

    @Builder
    func itemHead(text: String) {
        // Header component for the list group, corresponding to the component for group labels like A, B, etc.
        Text(text)
          .fontSize(20)
          .backgroundColor(0xfff1f3f5)
          .width(100.percent)
          .padding(5)
    }

    @Builder
    func footertest(itemGroup: ContactGroup) {
        ForEach(itemGroup.contacts, itemGeneratorFunc: { item: Contact, _:Int64 =>
                ListItem() {
                    Row() {
                        Image(item.icon).width(36).height(36).margin(8)
                        itemHead(item.name)
                    }
                }.backgroundColor(Color(0XFFFFFFFF))
            }
        )
    }

    func build() {
        List() {
            ForEach(this.contactsGroups, itemGeneratorFunc: { itemGroup: ContactGroup, _: Int64 =>
                    ListItemGroup(header: this.itemHead(itemGroup.title)) {
                        this.footertest(itemGroup)
                    }
                    .divider(ListDividerOptions(strokeWidth: 1, color: Color(0X08000000), startMargin: 48, endMargin: 48))
                },
                keyGeneratorFunc: {item: ContactGroup, idx: Int64 => idx.toString()}
            )
        }
        .backgroundColor(Color(0X08000000))
        .divider(ListDividerOptions(strokeWidth: 1, color: Color(0X08000000), startMargin: 48, endMargin: 48))
        .sticky(StickyStyle.Header)
    }
}

```
## Controlling Scroll Position

Controlling scroll position is a common requirement in practical applications. For example, when a news page contains a large number of list items, users may want to quickly scroll to the bottom or return to the top of the list after scrolling to a certain position. This can be achieved by controlling the scroll position, as illustrated in Figure 13.

**Figure 13** Returning to the Top of the List

![List12](figures/List12.gif)

During List component initialization, a [Scroller](../reference/arkui-cj/cj-scroll-swipe-scroll.md) object can be bound via the `scroller` parameter to control list scrolling. For instance, when a user clicks the "Back to Top" button at the bottom of a news app page, the `scrollToIndex` method of the Scroller object can be used to scroll the list to a specified item index.

First, create a Scroller object named `listScroller`:

```cangjie
var listScroller: Scroller = Scroller()
```

Then, bind `listScroller` to the List component by passing it to the `scroller` parameter during initialization. To return to the top of the list, set the `scrollToIndex` parameter to 0.

```cangjie
Stack(alignContent: Alignment.Bottom) {
    List(space: 20, scroller: this.listScroller) {
        // ...
    }
}

Button() {
    // ...
}
.onClick({ event =>
    this.listScroller.scrollToIndex(0)
})
```

## Responding to Scroll Position

Many applications need to monitor changes in list scroll position and respond accordingly. For example, when scrolling through a contact list, if the user crosses a group boundary (e.g., from names starting with 'A' to 'B'), the sidebar letter index should update to reflect the current letter.

Beyond letter indexing, multi-level category indexing combined with scrollable lists is also common, such as in e-commerce product category pages where multi-level categories must track scroll position.

**Figure 14** Letter Index Responding to Contact List Scrolling

![List13](figures/List13.gif)

As shown in Figure 14, when the contact list scrolls from 'A' to 'B', the sidebar index should update from highlighting 'A' to 'B'. This can be achieved by listening to the List component's `onScrollIndex` event, with the sidebar implemented using the [AlphabetIndexer](../reference/arkui-cj/cj-information-display-alphabetindexer.md) component.

During scrolling, the `selectedIndex` of the AlphabetIndexer is recalculated based on the current `firstIndex` position. Since the AlphabetIndexer's `selected` property controls the highlighted letter, updating `selectedIndex` triggers a re-render to display the correct letter.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

@Entry
@Component
public class EntryView {
    let alphabets = ['#', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K','L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    @State var selectedIndex: Int32 = 0;
    private var listScroller:Scroller = Scroller()

    func build() {
        Stack(alignContent: Alignment.End) {
            List(scroller: this.listScroller) {}
                .onScrollIndex({ firstIndex, scrollState, _ =>
                    // Recalculate this.selectedIndex based on the current scroll position
                })

            // Alphabet index component
            AlphabetIndexer(arrayValue: this.alphabets, selected: 0)
                .selected(this.selectedIndex)
        }
    }
}
```

> **Note:**
>
> When calculating index values, a ListItemGroup counts as a single index, and its internal ListItems are not indexed separately.

## Responding to List Item Swipe

Swipe menus are widely used in applications. For example, messaging apps often provide swipe-to-delete functionality, where users can swipe a list item left to reveal a delete button (Figure 15). For badge implementation on list items, refer to [Adding Badges to List Items](#adding-badges-to-list-items).

**Figure 15** Swipe-to-Delete List Item

![List14](figures/List14.gif)

The `swipeAction` property of [ListItem](../reference/arkui-cj/cj-scroll-swipe-listitem.md#func-swipeaction---unit----unit-swipeedgeeffect-float64---unit) enables left/right swipe actions. The `SwipeActionOptions` parameter is required, where `start` sets the component swiped from the leading edge, and `end` sets the trailing edge component (e.g., a delete button).

In a message list, the `end` parameter configures the delete button. Passing the item's index to the delete component allows targeted data removal when clicked.

- Implement the trailing swipe component:

    ```cangjie
    @Builder
    func itemEnd(index: Int64) {
      // Build trailing swipe component
      Button(ButtonOptions(shape: ButtonType.Circle)) {
        Image(@r(app.media.ic_public_delete_filled))
          .width(20)
          .height(20)
      }
      .onClick({ event =>
        // this.messages is the data source. Remove the item at the specified index.
        this.message.remove(index)
      })
    }
    ```

- Bind `swipeAction` to swipeable ListItems:

    ```cangjie
    // Render ListItems via ForEach based on this.messages data source.
    ListItem(){
        Text('1111').height(20)
    }
    .swipeAction(end: this.itemEnd(index)) // index is the ListItem's position
    ```

## Adding Badges to List Items

Badges provide unobtrusive visual cues for notifications or areas requiring attention. For example, new messages in a contact list can be indicated by a badge on the avatar (Figure 16).

**Figure 16** Adding Badges to List Items

![List15](figures/List15.png)

The [Badge](../reference/arkui-cj/cj-information-display-badge.md) component attaches markers to list items. It acts as a container for displaying counts or indicators.

To badge an avatar in a message list, wrap the `Image` component with a `Badge`. The `count`, `position`, and `style` parameters customize the badge's appearance and location.

```cangjie
ListItem(){
  Badge(
    count: 1, style: BadgeStyle(color: 0xfa2a2d, badgeSize: 16),
        position: BadgePosition.RightTop,
        child: { =>
            Image(@r(app.media.startIcon))
        }
    )
}
```

## Pull-to-Refresh and Load-More

Pull-to-refresh and load-more functionality is ubiquitous in mobile apps (e.g., news feeds). Both operations respond to [touch events](../reference/arkui-cj/cj-universal-event-touch.md) by showing/hiding refresh/load indicators at the top or bottom.

Pull-to-refresh implementation involves three steps:

1. Track the initial touch position on press.
2. During movement, calculate the offset from the initial position. Positive values indicate downward pulls, with a maximum threshold.
3. On release, if the threshold is met, trigger data loading and display the refresh view. Hide it upon completion.

> **Note:**
>
> Use the [Refresh](../reference/arkui-cj/cj-scroll-swipe-refresh.md) component for pull-to-refresh implementations.

## Editing Lists

List editing modes are widely used in to-do lists, file managers, and note-taking apps. Core functionalities include adding and deleting items by modifying the underlying data collection.

## Handling Long Lists

[Loop rendering](./rendering_control/cj-rendering-control-foreach.md) suits short lists. For long lists, rendering all items upfront causes slow load times. Instead, use [lazy loading](./rendering_control/cj-rendering-control-lazyforeach.md) (LazyForEach) to load data incrementally, improving performance.

For optimization details, refer to [Lazy Data Loading](./rendering_control/cj-rendering-control-lazyforeach.md).

When using lazy loading, the `cachedCount` parameter pre-renders items outside the viewport to minimize blank areas during scrolling:

```cangjie
List() {
  // ...
}.cachedCount(3)
```

Behavior varies by list type:
- For `ListItem` lazy loading: In single-column mode, `cachedCount` items are cached before/after the viewport. Multi-column mode caches `cachedCount * columnCount` items.
- For `ListItemGroup` lazy loading: Always caches `cachedCount` groups before/after the viewport.

> **Note:**
>
> Higher `cachedCount` increases CPU/memory usage. Balance performance and user experience.
>
> With lazy loading, only visible and cached items remain rendered; others are destroyed.

## Collapsing and Expanding

List item collapse/expand functionality is useful for information displays and forms.

**Figure 17** Collapsing and Expanding List Items

![List16](figures/List16.gif)

Implementation steps:

1. Define the item data structure:

    ```cangjie
    open class ItemInfo {
        var index: Int64
        var name: String
        var label: String
        var `type`: String = ''

        init(index: Int64, name: String, label: String, `type`: String) {
            this.index = index
            this.name = name
            this.label = label
            this.`type` = `type`
        }
    }

    public class ItemGroupInfo <: ItemInfo {
        var children: Array<ItemInfo>

        init(index: Int64, name: String, label: String, children: Array<ItemInfo>) {
            super(index, name, label, '')
            this.children = children
        }
    }
    ```

2. Construct the list:

    ```cangjie
    @State var routes: Array<ItemGroupInfo> = [
        ItemGroupInfo(
            0,
            'basicInfo',
            'Basic Information',
            [
                ItemInfo(0, 'Nickname', 'xxxx', 'Text'),
                ItemInfo(1, 'Avatar', "resource://rawfile/startIcon.png", 'Image'),
                ItemInfo(2, 'Age', 'xxxx', 'Text'),
                ItemInfo(3, 'Birthday', 'xxxxxxxx', 'Text'),
                ItemInfo(4, 'Gender', 'xxxxxx', 'Text')
            ]
        ),
        ItemGroupInfo(1, 'equipInfo', 'Device Info', []),
        ItemGroupInfo(2, 'appInfo', 'App Usage', []),
        ItemGroupInfo(3, 'uploadInfo', 'Uploaded Data', []),
        ItemGroupInfo(4, 'tradeInfo', 'Transactions', []),
        ItemGroupInfo(5, 'otherInfo', 'Other', [])
    ]
    @State var expandedItems: ObservedArrayList<Float32> = ObservedArrayList<Float32>([0.0, 0.0, 0.0, 0.0, 0.0, 0.0])

    func build() {
        Column() {
            // ...
            List(space: 10) {
                ForEach(
                    this.routes,
                    itemGeneratorFunc: { itemGroup: ItemGroupInfo, _: Int64 =>
                        ListItemGroup(header: this.ListItemGroupHeader(itemGroup),
                            footer: {=>}, space: 0, style: ListItemGroupStyle.Card) {
                                if (this.expandedItems[itemGroup.index] == 180.0) {
                                    ForEach(itemGroup.children, itemGeneratorFunc: { item: ItemInfo, _: Int64 =>
                                        ListItem() {
                                                Row() {
                                                    Text(item.name)
                                                    Blank()
                                                    if (item.`type` == 'Image') {
                                                        Image(item.label)
                                                            .height(20)
                                                            .width(20)
                                                    } else {
                                                        Text(item.label)
                                                    }
                                                    Image(@r(sys.media.ohos_ic_public_arrow_right))
                                                        .fillColor(@r(sys.color.ohos_id_color_fourth))
                                                        .height(30)
                                                        .width(30)
                                                }
                                                .width(100.percent)
                                        }.width(100.percent)
                                    })
                                }
                            }
                    }
                )
            }.width(100.percent)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Start)
        .backgroundColor(@r(sys.color.ohos_id_color_sub_background))
    }
    ```

3. Control expansion state with animations:

    ```cangjie
    @Builder
    func ListItemGroupHeader(itemGroup: ItemGroupInfo) {
        Row() {
            Text(itemGroup.label)
            Blank()
            Image(@r(sys.media.ohos_ic_public_arrow_down))
                .fillColor(@r(sys.color.ohos_id_color_fourth))
                .height(30)
                .width(30)
                .rotate(x: this.expandedItems[itemGroup.index])
                .animation(AnimateParam(curve: Curve.EaseInOut, duration: 500))
        }
        .width(100.percent)
        .padding(10)
        .onClick({
            event => this.expandedItems[itemGroup.index] = 180.0 - this.expandedItems[itemGroup.index]
        })
    }
    ```
```