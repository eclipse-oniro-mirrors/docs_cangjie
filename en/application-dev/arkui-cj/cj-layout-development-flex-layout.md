# Flex Layout

## Overview

Flex layout ([Flex](../reference/arkui-cj/cj-row-column-stack-flex.md)) provides a more efficient way to arrange, align, and distribute space among items in a container. It is commonly used for evenly distributing navigation bars in page headers, building page frameworks, and arranging multi-line data.

By default, a container has a main axis and a cross axis. Child elements are arranged along the main axis by default. The size of a child element along the main axis is called the main size, while its size along the cross axis is called the cross size.

**Figure 1** Flex container with horizontal main axis

![flex-layout](figures/flex-layout.png)

## Basic Concepts

- **Main Axis**: The axis along which Flex container items are laid out. Child elements are arranged along the main axis by default. The starting point of the main axis is called the main start, and the ending point is called the main end.

- **Cross Axis**: The axis perpendicular to the main axis. The starting point of the cross axis is called the cross start, and the ending point is called the cross end.

## Layout Direction

In Flex layout, child elements of a container can be arranged in any direction. By setting the `direction` parameter, you can determine the direction of the main axis, thereby controlling the arrangement direction of child elements.

The Flex layout direction is illustrated below:

![flex-layout-direction](figures/flex-layout-direction.png)

- **FlexDirection.Row** (default): The main axis is horizontal, and child elements are arranged from the start along the horizontal direction.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(direction: FlexDirection.Row) {
                Text('1')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .height(70)
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex](figures/Flex.png)

- **FlexDirection.RowReverse**: The main axis is horizontal, and child elements are arranged from the end in the opposite direction of `FlexDirection.Row`.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(direction: FlexDirection.RowReverse) {
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('1')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .height(70)
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex](figures/Flex.png)

- **FlexDirection.Column**: The main axis is vertical, and child elements are arranged from the start along the vertical direction.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(direction: FlexDirection.Column) {
                Text('1')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .height(70)
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex1](figures/Flex1.png)

- **FlexDirection.ColumnReverse**: The main axis is vertical, and child elements are arranged from the end in the opposite direction of `FlexDirection.Column`.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(direction: FlexDirection.ColumnReverse) {
                Text('1')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(100.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .height(70)
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex2](figures/Flex2.png)

## Wrapping Behavior

Flex layout can be single-line or multi-line. By default, all child elements in a Flex container are laid out in a single line (also called the "axis"). The `wrap` property controls whether Flex uses single-line or multi-line layout when the sum of child elements' main sizes exceeds the container's main size. In multi-line layout, the cross axis determines the direction of new lines.

- **FlexWrap.NoWrap** (default): No wrapping. If the total width of child elements exceeds the parent's width, the child elements will be compressed.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(wrap: FlexWrap.NoWrap) {
                Text('1')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex3](figures/Flex3.png)

- **FlexWrap.Wrap**: Wrapping enabled. Each line of child elements is arranged along the main axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(wrap: FlexWrap.Wrap) {
                Text('1')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex4](figures/Flex4.png)

- **FlexWrap.WrapReverse**: Wrapping enabled. Each line of child elements is arranged in the reverse direction of the main axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(wrap: FlexWrap.WrapReverse) {
                Text('1')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            Text('2')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(50.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex5](figures/Flex5.png)

## Main Axis Alignment

Use the `justifyContent` parameter to set the alignment of child elements along the main axis.

![flex-spindle-alignment](figures/flex-spindle-alignment.png)

- **FlexAlign.Start** (default): Child elements are aligned to the start of the main axis. The first child element aligns with the container's edge, and other elements align with the previous one.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.Start) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex6](figures/Flex6.png)

- **FlexAlign.Center**: Child elements are centered along the main axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.Center) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex7](figures/Flex7.png)

- **FlexAlign.End**: Child elements are aligned to the end of the main axis. The last child element aligns with the container's edge, and other elements align with the next one.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.End) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex8](figures/Flex8.png)

- **FlexAlign.SpaceBetween**: Child elements are evenly distributed along the main axis, with equal space between adjacent elements. The first and last elements align with the container's edges.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex9](figures/Flex9.png)

- **FlexAlign.SpaceAround**: Child elements are evenly distributed along the main axis, with equal space between adjacent elements. The space between the first element and the main start (or the last element and the main end) is half the space between adjacent elements.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceAround) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex11](figures/Flex11.png)

- **FlexAlign.SpaceEvenly**: Child elements are evenly distributed along the main axis, with equal space between adjacent elements, as well as between the first/last elements and the container edges.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceEvenly) {
                Text('1')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(20.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .width(90.percent)
            .padding(top: 10, bottom: 10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex12](figures/Flex12.png)

## Cross-Axis Alignment

Both container and child elements can set cross-axis alignment, with child element alignment settings taking higher priority.

### Container Component Cross-Axis Alignment

The cross-axis alignment of child elements can be set via the `alignItems` parameter of the Flex component.

- `ItemAlign.Auto`: Uses the default configuration in the Flex container.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.Auto) {
                Text('1')
                    .width(33.percent)
                    .height(30)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(40)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex13](figures/Flex13.png)

- `ItemAlign.Start`: Aligns to the start of the cross-axis direction.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.Start) {
                Text('1')
                    .width(33.percent)
                    .height(30)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(40)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex14](figures/Flex14.png)

- `ItemAlign.Center`: Centers alignment along the cross-axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.Center) {
                Text('1')
                    .width(33.percent)
                    .height(30)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(40)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex15](figures/Flex15.png)

- `ItemAlign.End`: Aligns to the end of the cross-axis direction.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.End) {
                Text('1')
                    .width(33.percent)
                    .height(30)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(40)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex16](figures/Flex16.png)

- `ItemAlign.Stretch`: Stretches to fill the cross-axis direction, expanding to container size when dimensions are not set.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.Stretch) {
                Text('1')
                    .width(33.percent)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex17](figures/Flex17.png)

- `ItemAlign.Baseline`: Aligns text baselines along the cross-axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(alignItems: ItemAlign.Baseline) {
                Text('1')
                    .width(33.percent)
                    .height(30)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(33.percent)
                    .height(40)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(33.percent)
                    .height(50)
                    .backgroundColor(0xF5DEB3)
            }
            .size(width: 90.percent, height: 80)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex18](figures/Flex18.png)

### Child Element Cross-Axis Alignment

The [`alignSelf`](../reference/arkui-cj/cj-universal-attribute-flexlayout.md#func-alignselfitemalign) attribute of child elements can also set their alignment format along the parent container's cross-axis, overriding the `alignItems` configuration in the Flex layout container. As shown in the following example:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Flex(direction: FlexDirection.Row, alignItems: ItemAlign.Center) { // Container sets child elements to center
            Text('alignSelf Start')
                .width(25.percent)
                .height(80)
                .alignSelf(ItemAlign.Start)
                .backgroundColor(0xF5DEB3)
            Text('alignSelf Baseline')
                .alignSelf(ItemAlign.Baseline)
                .width(25.percent)
                .height(80)
                .backgroundColor(0xD2B48C)
            Text('alignSelf Baseline')
                .width(25.percent)
                .height(100)
                .backgroundColor(0xF5DEB3)
                .alignSelf(ItemAlign.Baseline)
            Text('no alignSelf')
                .width(25.percent)
                .height(100)
                .backgroundColor(0xD2B48C)
            Text('no alignSelf')
                .width(25.percent)
                .height(100)
                .backgroundColor(0xF5DEB3)
        }
        .width(90.percent)
        .height(220)
        .backgroundColor(0xAFEEEE)
    }
}
```

![Flex19](figures/Flex19.png)

In the above example, the Flex container's `alignItems` sets the cross-axis alignment of child elements to center. When child elements have their own `alignSelf` attributes, they override the parent component's `alignItems` value, displaying as defined by `alignSelf`.

### Content Alignment

The [`alignContent`](../reference/arkui-cj/cj-row-column-stack-flex.md#initflexdirection-flexwrap-flexalign-itemalign-flexalign----unit) parameter can set the alignment of child element rows within the remaining space of the cross-axis, only effective in multi-line Flex layouts. Optional values include:

- `FlexAlign.Start`: Aligns child element rows to the start of the cross-axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.Start) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex20](figures/Flex20.png)

- `FlexAlign.Center`: Centers child element rows along the cross-axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.Center) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex21](figures/Flex21.png)

- FlexAlign.End: Child elements are aligned to the end of the cross axis.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.End) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex22](figures/Flex22.png)

- FlexAlign.SpaceBetween: Child elements are aligned to both ends of the cross axis, with vertical spacing evenly distributed between rows.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.SpaceBetween) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex23](figures/Flex23.png)

- FlexAlign.SpaceAround: Equal spacing between child element rows, with the distance between the first/last row and the cross axis ends being twice the spacing between rows.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.SpaceAround) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex24](figures/Flex24.png)

- FlexAlign.SpaceEvenly: Equal spacing between child element rows, with the distance between the first/last row and the cross axis ends being the same as the spacing between rows.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(justifyContent: FlexAlign.SpaceBetween, wrap: FlexWrap.Wrap, alignContent: FlexAlign.SpaceEvenly) {
                Text('1')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('2')
                    .width(60.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('3')
                    .width(40.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
                Text('4')
                    .width(30.percent)
                    .height(20)
                    .backgroundColor(0xF5DEB3)
                Text('5')
                    .width(20.percent)
                    .height(20)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(100)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex25](figures/Flex25.png)

## Adaptive Stretching

When the size of a flex layout parent component is too small, the following properties of child elements can be used to set their proportion within the parent container, achieving adaptive layout.

- [flexBasis](../reference/arkui-cj/cj-universal-attribute-flexlayout.md#func-flexbasislength): Sets the base size of a child element along the main axis of the parent container. If this property is set, the space occupied by the child element will be the value specified by this property; if not set, the space will be determined by the width/height value.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex() {
                Text('flexBasis("auto")')
                    .flexBasis(0) // If width is not set and flexBasis is 0, the width is determined by the content itself
                    .height(100)
                    .backgroundColor(0xF5DEB3)
                Text('flexBasis("auto")' + ' width("40%")')
                    .width(40.percent)
                    .flexBasis(0) // If width is set and flexBasis is 0, the width value is used
                    .height(100)
                    .backgroundColor(0xD2B48C)

                Text('flexBasis(100)') // If width is not set and flexBasis is 100, the width is 100.vp
                    .flexBasis(100)
                    .height(100)
                    .backgroundColor(0xF5DEB3)

                Text('flexBasis(100)')
                    .flexBasis(100)
                    .width(200) // If flexBasis is 100, it overrides the width setting, and the width is 100.vp
                    .height(100)
                    .backgroundColor(0xD2B48C)
            }
            .width(90.percent)
            .height(120)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex26](figures/Flex26.png)

- [flexGrow](../reference/arkui-cj/cj-universal-attribute-flexlayout.md#func-flexgrowfloat64): Sets the proportion of the parent container's remaining space allocated to the component with this property. Used to distribute the remaining space of the parent component.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex() {
                Text('flexGrow(2)')
                    .flexGrow(2)
                    .width(100)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
                Text('flexGrow(3)')
                    .flexGrow(3)
                    .width(100)
                    .height(100)
                    .backgroundColor(0xD2B48C)

                Text('no flexGrow')
                    .width(100)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
            }
            .width(380)
            .height(120)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex27](figures/Flex27.png)

    The parent container width is 420.vp, the original width of the three child elements is 100.vp, and the left and right padding is 20.vp, totaling 320.vp. The remaining 100.vp is distributed among the child elements based on the flexGrow ratio. Child elements without flexGrow set do not participate in the distribution.

    The first and second elements distribute the remaining 100.vp in a 2:3 ratio. The first element is 100.vp + 100.vp * 2/5 = 140.vp, and the second element is 100.vp + 100.vp * 3/5 = 160.vp.

- [flexShrink](../reference/arkui-cj/cj-universal-attribute-flexlayout.md#func-flexshrinkfloat64): Sets the compression ratio of child elements when the parent container space is insufficient.

    <!-- run -->

    ```cangjie
    package ohos_app_cangjie_entry
    import kit.ArkUI.*
    import ohos.arkui.state_macro_manage.*

    @Entry
    @Component
    class EntryView {
        func build() {
            Flex(direction: FlexDirection.Row) {
                Text('flexShrink(3)')
                    .flexShrink(3)
                    .width(200)
                    .height(100)
                    .backgroundColor(0xF5DEB3)

                Text('no flexShrink')
                    .width(200)
                    .height(100)
                    .backgroundColor(0xD2B48C)

                Text('flexShrink(2)')
                    .flexShrink(2)
                    .width(200)
                    .height(100)
                    .backgroundColor(0xF5DEB3)
            }
            .width(380)
            .height(120)
            .padding(10)
            .backgroundColor(0xAFEEEE)
        }
    }
    ```

    ![Flex28](figures/Flex28.png)

## Scenario Example

Using flex layout, child elements can be arranged horizontally with justified alignment, evenly distributed spacing, and centered vertically.

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
            Column(space: 5) {
                Flex(
                    direction: FlexDirection.Row, wrap: FlexWrap.NoWrap,
                        justifyContent: FlexAlign.SpaceBetween, alignItems: ItemAlign.Center) {
                    Text('1')
                        .width(30.percent)
                        .height(50)
                        .backgroundColor(0xF5DEB3)
                    Text('2')
                        .width(30.percent)
                        .height(50)
                        .backgroundColor(0xD2B48C)
                    Text('3')
                        .width(30.percent)
                        .height(50)
                        .backgroundColor(0xF5DEB3)
                }
                .height(70)
                .width(90.percent)
                .backgroundColor(0xAFEEEE)
            }
            .width(100.percent)
            .margin(top: 5)
        }.width(100.percent)
    }
}
```

![Flex29](figures/Flex29.png)
