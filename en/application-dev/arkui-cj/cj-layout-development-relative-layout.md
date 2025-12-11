# RelativeContainer

## Overview

During application development, complex interfaces often need to be designed, which involves nesting multiple identical or different components. If the nesting depth of layout components is too deep or the number of nested components is excessive, it can introduce additional overhead. Optimizing the layout approach can effectively improve performance and reduce time costs.

RelativeContainer is a container that adopts relative layout, supporting the setting of relative positional relationships among child elements within the container. It is suitable for complex interface scenarios, enabling alignment and arrangement of multiple child components. Child elements can specify sibling elements or the parent container as anchor points for relative positioning. Figure 1 illustrates a conceptual diagram of RelativeContainer, where dashed lines indicate positional dependencies.

**Figure 1** Relative Layout Schematic  
![relative-layout](figures/relative-layout.png)

Child elements do not strictly follow the dependency relationships shown above. For example, Item4 can depend on Item2 as an anchor point or use the RelativeContainer parent as its anchor point.

## Basic Concepts

- **Reference Boundary**: Specifies which boundary of the current component aligns with the anchor point.
  
- **Anchor Point**: Determines the element's position relative to another element.
  
- **Alignment Mode**: Sets whether the current element aligns with the anchor point's top, center, bottom (vertical) or left, center, right (horizontal).

## Setting Dependency Relationships

### Setting Reference Boundaries

Specifies which boundary of the current component aligns with the anchor point. The reference boundaries of child components within the container are differentiated by horizontal and vertical directions.

- **Horizontal Direction**: The component boundary can align with the anchor point based on start (left), middle (center), or end (right). When all three boundaries are set, only start (left) and middle (center) take effect.  
  ![relative-layout2](./figures/relative-layout2.png)

- **Vertical Direction**: The component boundary can align with the anchor point based on top, center, or bottom. When all three boundaries are set, only top and center take effect.  
  ![relative-layout3](./figures/relative-layout3.png)

### Setting Anchor Points

Anchor points define the positional dependencies of child elements relative to their parent or sibling elements. Specifically, child elements can anchor their positions to the RelativeContainer, guidelines, barriers, or other child elements.

To precisely define anchor points, child elements of RelativeContainer must have unique component IDs (`id`) to specify anchor information. The parent RelativeContainer's ID defaults to `__container__`, while other child elements' IDs are set via the [`id`](../reference/arkui-cj/cj-universal-attribute-componentid.md) attribute.

> **Note:**  
> - Components without an `id` can still be displayed but cannot be referenced as anchor points by other components. The RelativeContainer will auto-generate an `id`, but the pattern is not exposed to the application. Guideline and barrier IDs must be unique to avoid conflicts with any component. In case of duplicates, the priority order is: component > guideline > barrier.  
> - Avoid creating dependency loops (except for chain dependencies) when setting anchor points between components, as this may result in missing positioning references and ultimately prevent rendering.

- **Parent RelativeContainer as Anchor Point**: `__container__` represents the container's component ID.

  <!-- run -->  
  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      func build() {
          RelativeContainer() {
              Row() {
                  Text('row1')
              }
              .justifyContent(FlexAlign.Center)
              .width(100)
              .height(100)
              .backgroundColor(0xa3cf62)
              .alignRules(
                  AlignRuleOption(
                      top: VerticalAlignParam("__container__", VerticalAlign.Top),
                      left: HorizontalAlignParam("__container__", HorizontalAlign.Start)
                  )
              )
              .id("row1")

              Row() {
                  Text('row2')
              }
              .justifyContent(FlexAlign.Center)
              .width(100)
              .height(100)
              .backgroundColor(0x00ae9d)
              .alignRules(
                  AlignRuleOption(
                      top: VerticalAlignParam("__container__", VerticalAlign.Top),
                      right: HorizontalAlignParam("__container__", HorizontalAlign.End)
                  )
              )
              .id("row2")
          }
          .width(300)
          .height(300)
          .margin(left: 20)
          .border(width: 2, color: 0x6699FF)
      }
  }
  ```

  ![RelativeContainer](figures/RelativeContainer1.png)

- **Sibling Element as Anchor Point**:

  <!-- run -->  
  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      func build() {
          RelativeContainer() {
              Row() {
                  Text('row1')
              }
              .justifyContent(FlexAlign.Center)
              .width(100)
              .height(100)
              .backgroundColor(0x00ae9d)
              .alignRules(
                  AlignRuleOption(
                      top: VerticalAlignParam("__container__", VerticalAlign.Top),
                      left: HorizontalAlignParam("__container__", HorizontalAlign.Start)
                  )
              )
              .id("row1")

              Row() {
                  Text('row2')
              }
              .justifyContent(FlexAlign.Center)
              .width(100)
              .height(100)
              .backgroundColor(0xa3cf62)
              .alignRules(
                  AlignRuleOption(
                      top: VerticalAlignParam("row1", VerticalAlign.Bottom),
                      left: HorizontalAlignParam("row1", HorizontalAlign.Start)
                  )
              )
              .id("row2")
          }
          .width(300)
          .height(300)
          .margin(left: 20)
          .border(width: 2, color: 0x6699FF)
      }
  }
  ```

  ![RelativeContainer2](figures/RelativeContainer2.png)

- **Child Components Can Freely Choose Anchor Points**, but avoid mutual dependencies.

  <!-- run -->  
  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      func build() {
          Row() {
              RelativeContainer() {
                  Row() {Text('row1')}
                  .justifyContent(FlexAlign.Center)
                  .width(100)
                  .height(100)
                  .backgroundColor(0xa3cf62)
                  .alignRules(
                      AlignRuleOption(
                          top: VerticalAlignParam("__container__", VerticalAlign.Top),
                          left: HorizontalAlignParam("__container__",HorizontalAlign.Start)
                      )
                  )
                  .id("row1")
                  Row() {Text('row2')}
                  .justifyContent(FlexAlign.Center)
                  .width(100)
                  .backgroundColor(0x00ae9d)
                  .alignRules(
                      AlignRuleOption(
                          top: VerticalAlignParam("__container__", VerticalAlign.Top),
                          right: HorizontalAlignParam("__container__",HorizontalAlign.End),
                          bottom: VerticalAlignParam("row1", VerticalAlign.Center),
                      )
                  )
                  .id("row2")
                  Row() {Text('row3')}
                  .justifyContent(FlexAlign.Center)
                  .height(100)
                  .backgroundColor(0x0a59f7)
                  .alignRules(
                      AlignRuleOption(
                          top: VerticalAlignParam("row1", VerticalAlign.Bottom),
                          left: HorizontalAlignParam("row1", HorizontalAlign.Start),
                          right: HorizontalAlignParam("row2", HorizontalAlign.Start)
                      )
                  )
                  .id("row3")
                  Row() {Text('row4')}
                  .justifyContent(FlexAlign.Center)
                  .backgroundColor(0x2ca9e0)
                  .alignRules(
                      AlignRuleOption(
                          top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                          left: HorizontalAlignParam("row1", HorizontalAlign.Center),
                          right: HorizontalAlignParam("row2", HorizontalAlign.End)
                      )
                  )
                  .id("row4")
              }
              .width(300)
              .height(300)
              .margin(left: 50)
              .border(width: 2, color: 0x6699FF)
          }.height(100.percent)
      }
  }
  ```

  ![Simplify-Component-Layout](figures/simplify-component-layout-image1.png)

### Setting Alignment Relative to Anchor Points

After setting anchor points, use the [`alignRules`](../reference/arkui-cj/cj-universal-attribute-location.md#func-alignrulesalignruleoption) attribute to specify alignment relative to the anchor point.

- **Horizontal Alignment**: Options include `HorizontalAlign.Start`, `HorizontalAlign.Center`, and `HorizontalAlign.End`.  
  ![alignment-relative-anchor-horizontal](figures/alignment-relative-anchor-horizontal.png)

- **Vertical Alignment**: Options include `VerticalAlign.Top`, `VerticalAlign.Center`, and `VerticalAlign.Bottom`.  
  ![alignment-relative-anchor-vertical](figures/alignment-relative-anchor-vertical.png)

### Child Component Position Offset

After relative alignment, a child component's position may still not meet the target requirements. Developers can apply additional offsets (`offset`) as needed. When an offset-adjusted component serves as an anchor point, the alignment reference remains its pre-offset position. It is recommended to use [`bias`](../reference/arkui-cj/cj-universal-attribute-location.md#class-bias) for additional offsets.

 <!-- run -->  
```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row() {
                    Text('row1')
                }
                .justifyContent(FlexAlign.Center)
                .width(100)
                .height(100)
                .backgroundColor(0xa3cf62)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start)
                    )
                )
                .id("row1")

                Row() {
                    Text('row2')
                }
                .justifyContent(FlexAlign.Center)
                .width(100)
                .backgroundColor(0x00ae9d)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        right: HorizontalAlignParam("__container__",HorizontalAlign.End),
                        bottom: VerticalAlignParam("row1", VerticalAlign.Center)
                    )
                )
                .offset(x: -40, y: -20)
                .id("row2")

                Row() {
                    Text('row3')
                }
                .justifyContent(FlexAlign.Center)
                .height(100)
                .backgroundColor(0x0a59f7)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row1", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row1", HorizontalAlign.End),
                        right: HorizontalAlignParam("row2", HorizontalAlign.Start)
                    )
                )
                .offset(x: -10, y: -20)
                .id("row3")

                Row() {
                    Text('row4')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0x2ca9e0)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start),
                        right: HorizontalAlignParam("row1", HorizontalAlign.End)
                    )
                )
                .offset(x: -10, y: -30)
                .id("row4")
                Row() {
                    Text('row5')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0x30c9f7)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row2", HorizontalAlign.Start),
                        right: HorizontalAlignParam("row2", HorizontalAlign.End)
                    )
                )
                .offset(x: 10, y: 20)
                .id("row5")
                Row() {
                    Text('row6')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0xff33ffb5)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("row4", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row3", HorizontalAlign.Start),
                        right: HorizontalAlignParam("row3", HorizontalAlign.End)
                    )
                )
                .offset(x: -15, y: 10)
                .backgroundImagePosition(Alignment.Bottom)
                .backgroundImageSize(ImageSize.Cover)
                .id("row6")
            }
            .width(300)
            .height(300)
            .margin(left: 50)
            .border(width: 2, color: 0x6699FF)
        }.height(100.percent)
    }
}
```

![Simplify-Component-Layout](figures/simplify-component-layout-image2.png)

## Alignment Layout for Multiple Components

Components like `Row`, `Column`, `Flex`, and `Stack` can be aligned and arranged according to RelativeContainer rules.

 <!-- run -->  
```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row()
                .width(100)
                .height(100)
                .backgroundColor(0xa3cf62)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start)
                    )
                )
                .id("row1")
                Column()
                .width(50.percent)
                .height(30)
                .backgroundColor(0x00ae9d)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Center)
                    )
                )
                .id("row2")

                Flex(direction: FlexDirection.Row) {
                    Text('1')
                        .width(20.percent)
                        .height(50)
                        .backgroundColor(0x0a59f7)
                    Text('2')
                        .width(20.percent)
                        .height(50)
                        .backgroundColor(0x2ca9e0)
                    Text('3')
                        .width(20.percent)
                        .height(50)
                        .backgroundColor(0x0a59f7)
                    Text('4')
                        .width(20.percent)
                        .height(50)
                        .backgroundColor(0x2ca9e0)
                }
                .padding(10)
                .backgroundColor(0x30c9f7)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row2", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Center),
                        right: HorizontalAlignParam("row2", HorizontalAlign.Center)
                    )
                )
                .id("row3")

                Stack(alignContent: Alignment.Bottom) {
                    Text('First child, show in bottom')
                        .width(90.percent)
                        .height(100.percent)
                        .backgroundColor(0xa3cf62)
                        .align(Alignment.Top)
                    Text('Second child, show in top')
                        .width(70.percent)
                        .height(60.percent)
                        .backgroundColor(0x00ae9d)
                        .align(Alignment.Top)
                }
                .margin(top: 5)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Bottom),
                        right: HorizontalAlignParam("row3", HorizontalAlign.End)
                    )
                )
                .id("row4")
            }
            .width(300)
            .height(300)
            .margin(left: 50)
            .border(width: 2, color: 0x6699FF)
        }.height(100.percent)
    }
}
```

![Simplify-Component-Layout](figures/simplify-component-layout-image3.png)## Component Size

When both the child component size set by the frontend page and relative layout rules exist, the rendering size of the child component is determined based on constraint rules. The size set by the child component itself takes precedence over the alignment anchor size in relative layout rules. Therefore, to ensure strict alignment between the child component and the anchor point, only `alignRules` should be used, avoiding the [size setting](../reference/arkui-cj/cj-universal-attribute-size.md).

> **Note:**
>
> - If the size of the child component cannot be determined based on the constraints and its own `size` property, the child component will not be rendered.
> - When two or more anchor points are set in the same direction, if the order of these anchor points is incorrect, the child component will be considered to have a size of 0 and will not be rendered.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Row() {
            RelativeContainer() {
                Row() {
                    Text('row1')
                }
                .justifyContent(FlexAlign.Center)
                .width(100)
                .height(100)
                .backgroundColor(0xa3cf62)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start)
                    )
                )
                .id("row1")

                Row() {
                    Text('row2')
                }
                .justifyContent(FlexAlign.Center)
                .width(100)
                .backgroundColor(0x00ae9d)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("__container__", VerticalAlign.Top),
                        right: HorizontalAlignParam("__container__",HorizontalAlign.End),
                        bottom: VerticalAlignParam("row1", VerticalAlign.Center)
                    )
                )
                .id("row2")

                Row() {
                    Text('row3')
                }
                .justifyContent(FlexAlign.Center)
                .height(100)
                .backgroundColor(0x0a59f7)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row1", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row1", HorizontalAlign.End),
                        right: HorizontalAlignParam("row2", HorizontalAlign.Start),
                    )
                )
                .id("row3")

                Row() {
                    Text('row4')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0x2ca9e0)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("__container__",HorizontalAlign.Start),
                        right: HorizontalAlignParam("row1", HorizontalAlign.End)
                    )
                )
                .id("row4")

                Row() {
                    Text('row5')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0x30c9f7)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("__container__", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row2", HorizontalAlign.Start),
                        right: HorizontalAlignParam("row2", HorizontalAlign.End)
                    )
                )
                .id("row5")

                Row() {
                    Text('row6')
                }
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0xff33ffb5)
                .alignRules(
                    AlignRuleOption(
                        top: VerticalAlignParam("row3", VerticalAlign.Bottom),
                        bottom: VerticalAlignParam("row4", VerticalAlign.Bottom),
                        left: HorizontalAlignParam("row3", HorizontalAlign.Start),
                        right: HorizontalAlignParam("row3", HorizontalAlign.End)
                    )
                )
                .id("row6")
                .backgroundImagePosition(Alignment.Bottom)
                .backgroundImageSize(ImageSize.Cover)
            }
            .width(300)
            .height(300)
            .margin(left: 50)
            .border(width: 2, color: 0x6699FF)
        }.height(100.percent)
    }
}
```

![Simplify-Component-Layout](figures/simplify-component-layout-image4.png)