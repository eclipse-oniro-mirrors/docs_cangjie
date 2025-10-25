# Implicit Shared Element Transition Within Components (geometryTransition)

Provides smooth contextual inheritance transitions during view switching. While the generic transition mechanism offers effects like opacity and scale, geometryTransition establishes spatial connections between originally independent transition animations by coordinating the frames and positions of the bound in/out components (where "in" refers to the new view and "out" refers to the old view), thereby guiding the visual focus from the old view's position to the new view's position.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func geometryTransition(String, Bool)

```cangjie
public func geometryTransition(id: String, followWithoutTransition!: Bool = false): This
```

**Function:** Configures geometric transition animations.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Sets the binding relationship. Setting id to an empty string clears the binding to avoid participation in shared behavior. The id can be changed to re-establish binding relationships. Only two components can be bound to the same id, and they must play different in/out roles. Multiple components cannot share the same id. |
| followWithoutTransition | Bool | No | false | Whether to follow without transition animation. |

## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var isShow: Bool = false
    func build() {
        Stack(alignContent:Alignment.Center) {
            if (this.isShow) {
                Image(@r(app.media.startIcon))
                    .autoResize(false)
                    .clip(true)
                    .width(300)
                    .height(400)
                    .offset(x: 0, y: 100)
                    .geometryTransition("picture")
                    .transition(TransitionEffect.OPACITY)
            } else {
                Column() {
                    Column() {
                        Image(@r(app.media.startIcon))
                            .width(100.percent)
                            .height(100.percent)
                    }
                        .width(100.percent)
                        .height(100.percent)
                }
                    .width(80)
                    .height(80)
                    .borderRadius(20)
                    .clip(true)
                    .geometryTransition("picture")
                    .transition(TransitionEffect.OPACITY)
            }
        }.onClick({
            event => getUIContext().animateTo(AnimateParam(duration: 1000), ({=> this.isShow = !this.isShow}))
        })
    }
}
```

![geometrytransition](figures/geometrytransition.gif)