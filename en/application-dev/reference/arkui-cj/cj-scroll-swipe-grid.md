# Grid

A grid container composed of cells divided by "rows" and "columns", capable of creating various layouts by specifying the cells where "items" are placed.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Only supports [GridItem](cj-scroll-swipe-griditem.md) child components, including rendering control types ([if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), [LazyForEach](cj-state-rendering-lazyforeach.md)).

> **Note:**
>
> - Index calculation rules for Grid child components:
>   - Increments sequentially based on the order of child components.
>   - In if/else statements, only child components within the condition-true branch participate in index calculation; those in the false branch are excluded.
>   - ForEach/LazyForEach statements calculate indices for all expanded child nodes.
>   - After changes occur in [if/else](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](../../../en/application-dev/arkui-cj/rendering_control/cj-rendering-control-foreach.md), or [LazyForEach](cj-state-rendering-lazyforeach.md), child node indices are updated.
>   - Child components with visibility set to Hidden or None still participate in index calculation.
>   - Child components with visibility set to None are not displayed but still occupy their corresponding grid cells.
>   - Child components with position attributes set will occupy their corresponding grid cells and display at an offset position relative to the top-left corner of the Grid. These components do not scroll with their grid cells and disappear when the cells scroll out of the Grid's display area.
>   - When gaps exist between Grid child components, the current display area will attempt to fill them as much as possible, causing GridItems to potentially change relative positions during grid scrolling.

## Creating Components

### init(Option\<Scroller>, <() -> Unit>)

```cangjie
public init(scroller!: Option<Scroller> = Option.None, child!: () -> Unit = {=>})
```

**Function:** Creates a grid container with a scroll controller and child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name     | Type                          | Required | Default     | Description |
|:---------|:------------------------------|:---------|:------------|:------------|
| scroller | Option<[Scroller](./cj-scroll-swipe-scroll.md#class-scroller)> | No       | Option.None | Controller for scrollable components, bound to the scrollable component.<br> **Note:** <br>Cannot share the same scroll controller with other scrollable components like [List](cj-scroll-swipe-list.md), [Grid](cj-scroll-swipe-grid.md), or [Scroll](cj-scroll-swipe-scroll.md). |
| child    | Option<()->Unit>              | No       | Option.None | Child components of the grid container. |

## Common Attributes/Events

Common Attributes: Supports all common attributes.

Common Events: Fully supported.

## Component Attributes

### func cachedCount(Int32)

```cangjie
public func cachedCount(count: Int32): This
```

**Function:** Sets the number of preloaded GridItems, effective only in [LazyForEach](cj-state-rendering-lazyforeach.md).

After setting the cache, GridItems will be cached above and below the Grid display area by `cachedCount * column count`.

[LazyForEach](cj-state-rendering-lazyforeach.md) GridItems outside the display and cache range will be released.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type  | Required | Default | Description |
|:------|:------|:---------|:--------|:------------|
| count | Int32 | Yes      | -       | Number of preloaded GridItems.<br>Initial value: For vertical scrolling, it's the number of rows displayable on one screen; for horizontal scrolling, it's the number of columns displayable on one screen. Maximum value: 16.<br>Range: [0, +∞). Values less than 0 are treated as 1. |

### func cachedCount(Int32, Bool)

```cangjie
public func cachedCount(count: Int32, show: Bool): This
```

**Function:** Sets the number of preloaded GridItems and configures whether to display preloaded nodes.

After setting the cache, GridItems will be cached above and below the Grid display area by `cachedCount * column count`. Combined with [Clip](./cj-universal-attribute-shapclip.md#func-clip) or [Content Clip](./cj-universal-attribute-shapclip.md#func-clip) attributes, preloaded nodes can be displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type  | Required | Default | Description |
|:------|:------|:---------|:--------|:------------|
| count | Int32 | Yes      | -       | Number of preloaded GridItems.<br>Initial value: For vertical scrolling, it's the number of rows displayable on one screen; for horizontal scrolling, it's the number of columns displayable on one screen. Maximum value: 16.<br>Range: [0, +∞). Values less than 0 are treated as 1. |
| show  | Bool  | Yes      | -       | Whether to display preloaded GridItems.<br>Initial value: false (not displayed). |

### func columnsGap(Length)

```cangjie
public func columnsGap(value: Length): This
```

**Function:** Sets the gap between columns. Values less than 0 revert to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type                                     | Required | Default | Description |
|:------|:-----------------------------------------|:---------|:--------|:------------|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes      | -       | Gap between columns.<br>Initial value: 0<br>Range: [0, +∞) |

### func columnsTemplate(String)

```cangjie
public func columnsTemplate(value: String): This
```

**Function:** Sets the number of columns, fixed column width, or minimum column width for the current grid layout. Defaults to 1 column if not set.

For example, `'1fr 1fr 2fr'` divides the parent component into 3 columns, splitting the allowed width into 4 equal parts: the first column occupies 1 part, the second 1 part, and the third 2 parts.

- `columnsTemplate('repeat(auto-fit, track-size)')` sets the minimum column width to `track-size`, automatically calculating the number of columns and actual column width.
- `columnsTemplate('repeat(auto-fill, track-size)')` sets the fixed column width to `track-size`, automatically calculating the number of columns.
- `columnsTemplate('repeat(auto-stretch, track-size)')` sets the fixed column width to `track-size`, using `columnsGap` as the minimum column gap, and automatically calculates the number of columns and actual column gaps.

Here, `repeat`, `auto-fit`, `auto-fill`, and `auto-stretch` are keywords. `track-size` is the column width, supporting units like px, vp, %, or valid numbers (default unit: vp). `track-size` must include at least one valid column width value.

> **Note:**
>
> - `auto-stretch` mode only supports `track-size` as a single valid column width value and does not support %.
> - Setting `value` to `'0fr'` makes the column width 0, hiding GridItems. Other invalid values default to 1 fixed column.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type   | Required | Default | Description |
|:------|:-------|:---------|:--------|:------------|
| value | String | Yes      | -       | Number of columns or minimum column width for the current grid layout. |

### func rowsGap(Length)

```cangjie
public func rowsGap(value: Length): This
```

**Function:** Sets the gap between rows. Values less than 0 revert to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type                                     | Required | Default | Description |
|:------|:-----------------------------------------|:---------|:--------|:------------|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes      | -       | Gap between rows.<br>Initial value: 0<br>Range: [0, +∞) |

### func rowsTemplate(String)

```cangjie
public func rowsTemplate(value: String): This
```

**Function:** Sets the number of rows, fixed row height, or minimum row height for the current grid layout. Defaults to 1 row if not set.

For example, `'1fr 1fr 2fr'` divides the parent component into 3 rows, splitting the allowed height into 4 equal parts: the first row occupies 1 part, the second 1 part, and the third 2 parts.

- `rowsTemplate('repeat(auto-fit, track-size)')` sets the minimum row height to `track-size`, automatically calculating the number of rows and actual row height.
- `rowsTemplate('repeat(auto-fill, track-size)')` sets the fixed row height to `track-size`, automatically calculating the number of rows.
- `rowsTemplate('repeat(auto-stretch, track-size)')` sets the fixed row height to `track-size`, using `rowsGap` as the minimum row gap, and automatically calculates the number of rows and actual row gaps.

Here, `repeat`, `auto-fit`, `auto-fill`, and `auto-stretch` are keywords. `track-size` is the row height, supporting units like px, vp, %, or valid numbers (default unit: vp). `track-size` must include at least one valid row height value.

> **Note:**
>
> - `auto-stretch` mode only supports `track-size` as a single valid row height value and does not support %.
> - Setting `value` to `'0fr'` makes the row height 0, hiding GridItems. Other invalid values default to 1 fixed row.

The Grid component can be categorized into three layout modes based on `rowsTemplate` and `columnsTemplate` settings:

1. Both `rowsTemplate` and `columnsTemplate` are set:
   - Grid displays only fixed rows and columns; other elements are hidden, and the Grid is non-scrollable.
   - If Grid width/height is unset, it defaults to the parent component's dimensions.
   - Grid cell sizes are allocated proportionally after subtracting all row/column gaps from the Grid's content area.
   - GridItems fill their cells by default.

2. Only one of `rowsTemplate` or `columnsTemplate` is set:
   - Elements are arranged along the set direction. Overflowing elements can be displayed via scrolling.
   - If `columnsTemplate` is set, scrolling is vertical (main axis: vertical, cross axis: horizontal).
   - If `rowsTemplate` is set, scrolling is horizontal (main axis: horizontal, cross axis: vertical).
   - Cross-axis cell sizes are allocated proportionally after subtracting gaps from the Grid's cross-axis content area.
   - Main-axis cell sizes take the maximum height of all GridItems in the current cross-axis direction.

3. Neither `rowsTemplate` nor `columnsTemplate` is set:
   - Row count is determined by Grid height, first element height, and `rowsGap`. Elements beyond the row/column capacity are hidden and cannot be displayed via scrolling.
   - Only these attributes take effect: `columnsGap`, `rowsGap`.
   - If no GridItems exist under the Grid, its width/height is 0.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name  | Type   | Required | Default | Description |
|:------|:-------|:---------|:--------|:------------|
| value | String | Yes      | -       | Number of rows or minimum row height for the current grid layout. |

## Example Code

### Example 1 (Setting Adaptive Column Count)

Demonstrates the use of `auto-fill`, `auto-fit`, and `auto-stretch` in the [columnsTemplate](#func-columnstemplatestring) attribute.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import ohos.arkui.state_macro_manage.State
import ohos.arkui.state_macro_manage.r
import ohos.base.*
import ohos.arkui.component.*
import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*
import std.collection.{ArrayList, HashMap}

@Entry
@Component
class EntryView {
    var data: Array<Int64> = [0, 1, 2, 3, 4, 5]
    var data1: Array<Int64> = [0, 1, 2, 3, 4, 5]
    var data2: Array<Int64> = [0, 1, 2, 3, 4, 5]

    func build() {
        Column(space: 10) {
            Text("auto-fill calculates column count based on set column width").width(90.percent)
            Grid() {
                ForEach(
                    this.data,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => GridItem() {
                            Text("N ${item}").height(80)
                        }.backgroundColor(Color.Gray)
                    }
                )
            }
                .width(90.percent)
                .border(width: 1.vp, color: Color.Black)
                .columnsTemplate("repeat(auto-fill, 70)")
                .columnsGap(10)
                .rowsGap(10)
                .height(150)

            Text("auto-fit calculates column count first, then evenly distributes remaining space to each column").width(90.percent)
            Grid() {
                ForEach(
                    this.data1,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => GridItem() {
                            Text("N ${item}").height(80)
                        }.backgroundColor(Color.Gray)
                    }
                )
            }
                .width(90.percent)
                .border(width: 1.vp, color: Color.Black)
                .columnsTemplate("repeat(auto-fit, 70)")
                .columnsGap(10)
                .rowsGap(10)
                .height(150)

            Text("auto-stretch calculates column count first, then evenly distributes remaining space to each column gap").width(90.percent)
            Grid() {
                ForEach(
                    this.data2,
                    itemGeneratorFunc: {
                        item: Int64, idx: Int64 => GridItem() {
                            Text("N ${item}").height(80)
                        }.backgroundColor(Color.Gray)
                    }
                )
            }
                .width(90.percent)
                .border(width: 1.vp, color: Color.Black)
                .columnsTemplate('repeat(auto-stretch, 70)')
                .columnsGap(10)
                .rowsGap(10)
                .height(150)
        }.width(100.percent).height(100.percent)
    }
}
```

![griditem](figures/grid5_api.png)