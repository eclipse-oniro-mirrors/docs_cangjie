# Component Animation

ArkUI provides components with general-purpose attribute animation and transition animation capabilities, while also offering default animation effects for certain components. For example, the sliding animation of [List](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-list.md) and the click animation of [Button](../../../en/application-dev/reference/arkui-cj/cj-button-picker-button.md#button) are built-in default animation effects. Based on these default component animations, developers can further customize the animation effects of child components within container components using attribute animation and transition animation.

## Using Default Component Animations

Default component animations serve the following purposes:

- Providing user feedback on current states. For instance, when a user clicks a Button component, it turns gray by default to confirm the selection operation.

- Enhancing interface refinement and liveliness.

- Reducing developer workload. For example, list scrolling components come with built-in sliding animations that developers can directly utilize.

For more effects, refer to [Component Documentation](../../../en/application-dev/reference/arkui-cj/cj-row-column-stack-flex.md).

Example code:

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Row {
            Checkbox(name: 'checkbox1', group: "checkboxGroup")
                .select(true)
                .shape(CheckBoxShape.Circle)
                .size(width: 50, height: 50)
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
    }
}
```

![animation](figures/componentAnimation1.gif)

## Creating Customized Component Animations

Certain components support customizing animation effects for child Items through [attribute animation](./cj-attribute-animation-overview.md) and [transition animation](./cj-transition-overview.md), enabling tailored animation effects. For example, the [Scroll](../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-scroll.md) component allows customization of animation effects for each child component during scrolling.

- Achieve various effects by modifying the affine properties of each Scroll child component during scrolling or clicking operations.

- To customize animations during scrolling, monitor the scrolling distance in the onScroll callback and calculate the affine properties for each component. Alternatively, define custom gestures to track positions and manually adjust scrolling positions using ScrollTo.

- Fine-tune the final scrolling position in the onScrollStop callback or gesture end callback.