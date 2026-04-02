# Shadow

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The shadow interface [shadow](../reference/arkui-cj/cj-universal-attribute-imageeffect.md#func-shadowfloat64-resourcecolor-float64-float64) can add shadow effects to the current component. Developers can configure [ShadowOptions](../reference/arkui-cj/cj-common-types.md#class-shadowoptions) for custom shadow effects. Before API version 26, when radius is less than or equal to 0 or the color's alpha is 0, there is no shadow; from API version 26 onward, when radius is less than 0 or the color's alpha is 0, there is no shadow.

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
            Column() {
                Column() {
                    Text('shadowOption').fontSize(12)
                }
                .width(100)
                .aspectRatio(1.0)
                .margin(10)
                .justifyContent(FlexAlign.Center)
                .backgroundColor(Color.White)
                .borderRadius(20)
                .shadow(radius: 10.0, color: Color.Gray)

                Column() {
                    Text('shadowOption').fontSize(12)
                }
                .width(100)
                .aspectRatio(1.0)
                .margin(10)
                .justifyContent(FlexAlign.Center)
                .backgroundColor(0xF48899)
                .borderRadius(20)
                .shadow(radius: 10.0, color: Color.Gray, offsetX: 20.0, offsetY: 20.0)
            }
            .width(100.percent)
            .height(100.percent)
            .justifyContent(FlexAlign.Center)
        }
        .height(100.percent)
    }
}
```

![shadow](./figures/shadow.png)