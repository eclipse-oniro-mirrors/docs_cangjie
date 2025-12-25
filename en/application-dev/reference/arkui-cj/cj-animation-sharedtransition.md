# Shared Element Transition (sharedTransition)

By setting the `sharedTransition` property of a component, the element can be marked as a shared element and configured with corresponding shared element transition effects. The `sharedTransition` effect only occurs during page routing ([router](cj-apis-uicontext-router.md#class-router)) navigation.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func sharedTransition(String, ?SharedTransitionOptions)

```cangjie
func sharedTransition(id: String, options!: ?SharedTransitionOptions): T
```

**Function:** Configures shared element transition effects.

> **Note:**
>
> The `motionPath` takes effect only when `effectType` is `SharedTransitionEffectType.Exchange`. When `effectType` is `SharedTransitionEffectType.Exchange`, the effect produces transitions in position and size for matched shared elements (observable via component border configuration), but does not support content transitions. For example, if a `Text` component uses different `fontSize` property values on two pages (i.e., the rendered content has size differences), the `fontSize` effect of the `Text` component will abruptly change to the target page's `fontSize` effect in the final frame after the `sharedTransition` animation completes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Components with the same non-empty `id` value across two pages are considered shared elements and will display shared element transition effects during page navigation. |
| options | ?[SharedTransitionOptions](./cj-common-types.md#class-sharedtransitionoptions) | No | None | **Named parameter.** Shared element transition animation parameters.<br>Default: `SharedTransitionOptions()`. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Returns the component instance. |

## Example Code

The example demonstrates a custom transition effect for a shared element image when clicking to navigate between pages.

<!-- run -->

```cangjie
// index.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.__GenerateResource__

@Entry
@Component
class EntryView {
    @State var active: Bool = false
    func build() {
        Column() {
            Image(@r(app.media.startIcon))
                .width(50)
                .height(50)
                .onClick({
                    e => getUIContext().getRouter().pushUrl(url:"Page1")
                })
                .sharedTransition("sharedImage",
                    options: SharedTransitionOptions(duration: 800, curve: Curve.Linear, delay: 100))
        }
    }
}
```

<!-- run -->

```cangjie
// Page1.cj
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.__GenerateResource__

@Entry
@Component
class Page1 {
    func build() {
        Stack() {
            Image(@r(app.media.startIcon))
                .width(150)
                .height(150)
                .sharedTransition(
                    "sharedImage",
                    options: SharedTransitionOptions(duration: 800, curve: Curve.Linear, delay: 100)
                )
        }
        .width(100.percent)
        .height(100.percent)
    }
}
```

![shared_transition](figures/sharedtransition.gif)