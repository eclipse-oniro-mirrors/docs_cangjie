# Binding Half-Modal Page (bindSheet)

[The half-modal page (bindSheet)](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-sheettransition.md#func-bindsheetbool----unit-sheetoptions) is by default a non-fullscreen popup-style interactive page in modal form, allowing partial visibility of the underlying parent view to help users retain their parent view context while interacting with the half-modal.

Half-modal pages are suitable for displaying simple tasks or information panels, such as personal information, text introductions, sharing panels, creating schedules, adding content, etc. If there is a need to display a half-modal page that may affect the parent view, the half-modal supports configuration as a non-modal interactive form.

Half-modal pages exhibit different behavioral capabilities on devices with varying widths. Developers with different form requirements for devices of different widths should refer to the ([preferType](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-sheettransition.md#class-sheetoptions)) attribute. The bindSheet can be used to construct half-modal transition effects; for details, see [Modal Transition](./cj-modal-transition.md). For complex or lengthy user flows, it is recommended to consider alternative transition methods instead of half-modal, such as [Full-Modal Transition](./cj-contentcover-page.md).

## Usage Constraints

- If there are no scenarios requiring secondary confirmation or custom close behavior, it is not recommended to use the [shouldDismiss/onWilDismiss](../../../en/application-dev/reference/arkui-cj/cj-universal-attribute-sheettransition.md#class-sheetoptions) interface.

## Lifecycle

The half-modal page provides lifecycle functions to notify users of the popup's lifecycle status. The lifecycle triggers occur in the following order: onWillAppear -> onAppear -> onWillDisappear -> onDisappear.

| Name | Type | Description |
|:---|:---|:---|
| onWillAppear | () -> Unit | Callback function triggered before the half-modal page appears (before animation starts). |
| onAppear | () -> Unit | Callback function triggered after the half-modal page appears (after animation ends). |
| onWillDisappear | () -> Unit | Callback function triggered before the half-modal page retreats (before animation starts). |
| onDisappear | () -> Unit | Callback function triggered after the half-modal page retreats (after animation ends). |

## Using Nested Scroll Interaction

Operation priority when sliding in the content area of a half-modal panel:

1. Content is at the top (handled in this state when content is not scrollable)<br> When sliding up, priority is given to expanding the panel level upwards. If no level can be expanded, the content is scrolled.<br> When sliding down, priority is given to contracting the panel level downwards. If no level can be contracted, the panel is closed.

2. Content is in the middle position (can scroll up and down)<br> When sliding up/down, priority is given to scrolling the content until the page content reaches the bottom/top.

3. Content is at the bottom position (when content is scrollable)<br> When sliding up, a rebound effect is presented in the content area without switching levels.<br> When sliding down, the content is scrolled until it reaches the top.

The default nested mode for the above half-modal interaction is: {Forward: PARENT_FIRST, Backward: SELF_FIRST}

If developers wish to define a scroll container, such as List or Scroll, in the panel content's builder and combine it with the above interaction capabilities of the half-modal, they need to set the nested scroll attribute for the scroll container in the vertical direction.

```cangjie
.nestedScroll(
    NestedScrollOptions(
        // Nested scroll option when the scrollable component scrolls towards the end (gesture up)
        NestedScrollMode.ParentFirst,
        // Nested scroll option when the scrollable component scrolls towards the start (gesture down)
        NestedScrollMode.SelfFirst,
    )
)
```

Complete example code is as follows:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*

@Entry
@Component
class EntryView {
    @State var isShowSheet: Bool = false
    private var items: Array<Int64> = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

    @Builder
    func SheetBuilder() {
        Column() {
            // Step 1: Custom scroll container
            List(space: 10) {
                ForEach(
                    this.items,
                    itemGeneratorFunc: {
                        item: Int64, _: Int64 => ListItem() {
                            Text(item.toString())
                                .fontSize(16)
                                .fontWeight(FontWeight.Bold)
                        }
                        .width(90.percent)
                        .height(80.vp)
                        .backgroundColor(Color.Blue)
                        .borderRadius(10)
                    }
                )
            }
            .alignListItem(ListItemAlign.Center)
            .margin(top: 10)
            .width(100.percent)
            .height(900.px)
            // Step 2: Set nested scroll attributes for the scroll component
            .nestedScroll(
                NestedScrollOptions(
                    NestedScrollMode.ParentFirst,
                    NestedScrollMode.SelfFirst,
                )
            )

            Text("Non-scrollable area")
                .width(100.percent)
                .backgroundColor(Color.Gray)
                .layoutWeight(1)
                .textAlign(TextAlign.Center)
                .align(Alignment.Top)
        }
        .width(100.percent)
        .height(100.percent)
    }

    func build() {
        Column() {
            Button("Open Sheet")
                .width(90.percent)
                .height(80.vp)
                .onClick({
                    evt => this.isShowSheet = !this.isShowSheet
                })
                .bindSheet(
                    this.isShowSheet,
                    this.SheetBuilder,
                    options: SheetOptions(
                        detents: [SheetSize.Medium, SheetSize.Large, FitContent],
                        preferType: SheetType.Bottom,
                        title: {=> Text("Nested Scroll Scenario")}
                    )
                )
        }
        .width(100.percent)
        .height(100.percent)
        .justifyContent(FlexAlign.Center)
    }
}
```

![page](figures/page.gif)

## Secondary Confirmation Capability

It is recommended to use the onWillDismiss interface, which supports handling secondary confirmation or custom close behavior in the callback.

```cangjie
// Step 1: Declare onWillDismiss callback
onWillDismiss: {
    // Step 2: Confirm secondary callback interaction capability, here using AlertDialog to prompt "Do you want to close the half-modal?"
    dismissSheetAction: DismissSheetAction => {
        AlertDialog.show(
            AlertDialogParamWithButtons(
                "text",
                title: 'Do you want to close the half-modal?',
                primaryButton: AlertDialogButtonOptions(
                    value: 'cancel',
                    action: {
                        => Hilog.info(0, "cangjie", "Callback when the cancel button is clicked")
                    }
                ),
                secondaryButton: AlertDialogButtonOptions(
                    value: 'ok',
                    // Step 3: Confirm the logic for closing the half-modal, here in the AlertDialog's Button callback
                    action: {
                        => {
                            // Step 4: When the logic in Step 3 is triggered, call dismiss() to close the half-modal
                            dismissSheetAction.dismiss(),
                            Hilog.info(0, "cangjie", "Callback when the ok button is clicked")
                        }
                    }
                ),
                cancel: {
                    => Hilog.info(0, "cangjie", "AlertDialog Closed callbacks")
                }
            )
        )
    }
}
```

![page](figures/page.gif)

## Blocking Partial Close Behaviors

Since the onWillDismiss interface is declared, all close behaviors of the half-modal require dismiss handling. The close logic can be customized using if statements or other logic.

The following example shows the half-modal page closing only when sliding down.

```cangjie
onWillDismiss: {
    dismissSheetAction: DismissSheetAction => {
        if (dismissSheetAction.reason == DismissReason.SLIDE_DOWN) {
            DismissSheetAction.dismiss() // Register dismiss behavior
        }
    }
}
```

Similarly, a better sliding-down experience can be achieved by combining it with the onWillSpringBackWhenDismiss interface.

Analogous to onWillDismiss, after declaring onWillSpringBackWhenDismiss, the rebound operation during half-modal sliding down requires handling with SpringBackAction.springBack(). Without this logic, there will be no rebound.

The specific code is as follows, where the half-modal does not rebound when sliding down.

```cangjie
onWillDismiss: {
    dismissSheetAction: DismissSheetAction => {
        if (dismissSheetAction.reason == DismissReason.SLIDE_DOWN) {
            dismissSheetAction.dismiss() // Register dismiss behavior
        }
    }
}

onWillSpringBackWhenDismiss: {
    springBackAction: SpringBackAction => {
        // No springBack is registered, so sliding down the half-modal page has no rebound behavior
    }
}
```