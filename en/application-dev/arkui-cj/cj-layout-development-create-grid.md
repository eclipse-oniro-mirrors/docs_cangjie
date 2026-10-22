# Creating Grid Layout (Grid/GridItem)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

A grid layout consists of cells divided by "rows" and "columns", enabling diverse layouts by specifying which cells contain "items". Grid layouts excel at evenly distributing page space and controlling child component proportions, making them a crucial adaptive layout solution. Common use cases include 9-grid image displays, calendars, calculators, etc.

ArkUI provides the [Grid](../reference/arkui-cj/cj-scroll-swipe-grid.md) container component and its child component [GridItem](../reference/arkui-cj/cj-scroll-swipe-griditem.md) for constructing grid layouts. The Grid component configures layout parameters, while GridItem defines child component characteristics. Grid supports conditional rendering, iterative rendering, and lazy loading for generating child components.

## Layout and Constraints

The Grid component serves as the container, with each entry inside corresponding to a GridItem component, as shown in Figure 1.

**Figure 1** Relationship between Grid and GridItem Components

![GridItem](figures/GridItem.png)

> **Note:**
>
> Child components of Grid must be GridItem components.

As a two-dimensional layout system, Grid supports custom row/column counts and proportional sizing, enables child components to span multiple rows/columns, and provides both vertical and horizontal layout capabilities. When container dimensions change, all child components and spacing adjust proportionally for adaptive behavior. These features enable various grid styles, as illustrated in Figure 2.

**Figure 2** Grid Layout Examples

![GridItem1](figures/GridItem1.png)

If width/height properties are set, Grid adopts those dimensions. Otherwise, it defaults to matching its parent component's size.

Grid layouts can be configured in three ways based on row/column settings:

1. **Both row/column counts and proportions specified**: Displays fixed rows/columns (recommended approach)
2. **Only row or column configuration set**: Items arrange along specified axis with scrollable overflow
3. **No row/column configuration**: Layout determines rows/columns based on multiple factors, hiding overflow content without scrolling

## Arrangement Configuration

### Setting Row/Column Counts and Proportions

The rowsTemplate and columnsTemplate properties define grid structure using space-separated "nfr" values, where:
- Number of "fr" units determines row/column count
- Preceding numeric values calculate proportional width allocation

**Figure 3** Row/Column Proportion Example

![GridItem2](figures/GridItem2.png)

The 3x3 grid in Figure 3 divides vertically into equal thirds and horizontally into quarters (1:2:1 ratio):

```cangjie
Grid() {
  // ...
}
.rowsTemplate("1fr 1fr 1fr")
.columnsTemplate("1fr 2fr 1fr")
```

> **Note:**
>
> When rowsTemplate/columnsTemplate are set, layoutDirection and cellLength properties become ineffective (see [Grid Attributes](../reference/arkui-cj/cj-scroll-swipe-grid.md#component-attributes)).

## Displaying Data in Grid Layouts

Grids organize elements in two dimensions, as shown in Figure 5's office services example.

**Figure 5** General Office Services

![GridItem4](figures/GridItem4.png)

Basic implementation with explicit GridItems:

```cangjie
Grid() {
    GridItem() {
        Text("Meeting")
        //  ...
    }

    GridItem() {
        Text("Check-in")
        //  ...
    }

    GridItem() {
        Text("Voting")
        //  ...
    }

    GridItem() {
        Text("Print")
        //  ...
    }
}
.rowsTemplate("1fr 1fr")
.columnsTemplate("1fr 1fr")
```

For structurally similar items, prefer ForEach with nested GridItem:

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var services: Array<String> = ["Meeting", "Voting", "Check-in", "Print"]
    func build() {
            Column() {
                Grid() {
                    ForEach(this.services, itemGeneratorFunc: {service: String, _: Int64 =>
                        GridItem() {
                            Text(service)
                        }}
                    )
                }
                .rowsTemplate("1fr 1fr")
                .columnsTemplate("1fr 1fr")
            }
    }
}
```

## Configuring Row/Column Gaps

Row gaps (horizontal spacing) and column gaps (vertical spacing) between grid cells are shown in Figure 6.

**Figure 6** Grid Spacing

![GridItem5](figures/GridItem5.png)

Set gaps using rowsGap and columnsGap. The calculator in Figure 5 uses 15vp row gaps and 10vp column gaps:

```cangjie
Grid() {
  // ...
}
.columnsGap(10)
.rowsGap(15)
```

## Creating Scrollable Grids

Scrollable grids are common in file managers, shopping/video lists (Figure 7). When only rowsTemplate or columnsTemplate is set, overflow content becomes scrollable along the configured axis.

**Figure 7** Horizontally Scrollable Grid

![GridItem6](figures/GridItem6.gif)

- columnsTemplate only → vertical scrolling
- rowsTemplate only → horizontal scrolling

Implementation for Figure 7's horizontal scrolling:

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var services: Array<String> = ["Live", "Imports"]
    func build() {
            Column(space: 5) {
                Grid() {
                    ForEach(this.services, itemGeneratorFunc: {service: String, _: Int64 =>
                        GridItem() {
                            // Add content
                        }
                        .width(25.percent)
                        }
                    )
                }
                .rowsTemplate("1fr 1fr")
                .rowsGap(15)
        }
    }
}
```

## Scroll Position Control

Similar to news list "back to top" functionality, scroll control is useful for grid applications like calendar pagination (Figure 8).

**Figure 8** Calendar Pagination

![GridItem7](figures/GridItem7.gif)

Initialize Grid with a [Scroller](../reference/arkui-cj/cj-scroll-swipe-scroll.md#scroll) object for control. The scrollPage method handles page turns:

```cangjie
var scroller: Scroller = Scroller()
```

Calendar implementation for next/previous page navigation:

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    var scroller: Scroller = Scroller()
    func build() {
        Column() {
            Grid(scroller: this.scroller) {
              // Add content
            }
            .columnsTemplate("1fr 1fr 1fr 1fr 1fr 1fr 1fr")
            .height(85.percent)

            Row() {
              Row() {
                  Button("Previous")
                  .onClick({ evt =>
                      this.scroller.scrollPage(false, animation: false)
                  }).width(100)
              }.width(50.percent)
              .justifyContent(FlexAlign.Center)

              Row() {
                  Button("Next")
                  .onClick({ evt =>
                      this.scroller.scrollPage(true, animation: false)
                  }).width(100)
              }.width(50.percent)
              .justifyContent(FlexAlign.Center)
            }
            .height(15.percent)
        }.height(100.percent)
    }
}
```

## Performance Optimization

Like [long list handling](./cj-layout-development-create-list.md#long-list-processing), iterative rendering suits smaller datasets. For large scrollable grids, implement [lazy loading](./rendering_control/cj-rendering-control-lazyforeach.md) to load data on demand and improve performance.

Reference the [Lazy Loading](./rendering_control/cj-rendering-control-lazyforeach.md) chapter for implementation details.

When using lazy loading, set cachedCount to preload GridItems beyond the visible area (only effective with LazyForEach). This buffers cachedCount*columns items before/after the viewport, releasing others.

```cangjie
Grid() {
    LazyForEach(this.dataSource, itemGeneratorFunc: {dataSource: T, _: Int64 =>
        GridItem() {
        }
    })
}
.cachedCount(3)
```

> **Note:**
>
> Higher cachedCount values increase CPU/memory usage. Balance performance and user experience based on actual requirements.