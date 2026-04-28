# Page-Level Dialog

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

By default, dialogs are set to global level, where the dialog node acts as a child node of the page root node, with a display level higher than all routing/navigation pages in the application. When routing transitions occur within the page, if the application does not actively call the close method to dismiss the dialog, the dialog will not automatically close and will continue to display on the next navigated page.

If developers want the dialog to disappear with the previous routing page after routing transitions, and continue to display normally when returning from routing, this can be achieved through page-level dialogs.

> **Note:**
> - Page-level capability only takes effect when the dialog is in non-sub-window mode. That is, the showInSubWindow parameter is not set or set to false.
> - Page-level dialogs are typically used in combination with navigation routing capabilities. You can refer to [Overview of Component Navigation and Page Routing](cj-navigation-introduction.md) to understand related terminology.
> - The usage of page-level dialogs involves adding relevant property capabilities in the current dialog's input parameters. Before using, you can learn about basic dialog usage methods through the [dialog Popup Overview](cj-dialog-base-overview.md).

## Setting Parameters

Set the [levelMode](../reference/arkui-cj/cj-apis-uicontext-promptaction.md#enum-levelmode) property in the dialog's options input parameter, with a value of LevelMode.Embedded to enable page-level dialog capability.

When the dialog appears, it automatically obtains the currently displayed Page and mounts the dialog node under this page. At this point, the dialog's display level is higher than all Navigation pages under this Page.

```cangjie
this.getUIContext().getPromptAction().openCustomDialog(
    CustomDialogOptions(
        builder: bind(this.CustomDialogBuilder, this)
        levelMode: LevelMode.Embedded, // Enable page-level dialog
        // ···
    )
)
```

## Interaction Description

Page-level dialogs still follow the interaction strategies specified by some dialogs in certain interaction logic:

Swipe gesture first dismisses the dialog. When returning to the previous page through a swipe gesture, if a dialog exists on the page, the dialog will be dismissed first and this gesture behavior will end. If you want to return to the previous page, you need to trigger the swipe gesture again.

Clicking the dialog mask layer will dismiss the dialog by default, while clicking areas outside the mask layer will not.

## Complete Example

The following example demonstrates a page-level dialog based on Router routing mode.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var message: String = 'Hello World'
    @State var customDialogId: Int32 = 0
    
    @Builder
    func customDialogBuilder() {
        Column() {
            Text('Custom dialog Message').fontSize(20).height(100)
            Row() {
                Button('Next').onClick({ evt => 
                    // Route transition inside the dialog
                    this.getUIContext().getRouter().pushUrl(url: 'Next')
                })
                Blank().width(50)
                Button('Close').onClick({ evt =>
                    this.getUIContext().getPromptAction().closeCustomDialog(customDialogId)
                })
            }
        }.padding(20)
    }

    func build() {
        NavDestination() {
            Row() {
                Column() {
                    Text(this.message).id('test_text')
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick({ evt =>
                        this.getUIContext().getPromptAction().openCustomDialog(
                            CustomDialogConfig(
                                builder: bind(this.customDialogBuilder, this),
                                levelMode: LevelMode.Embedded, // Enable page-level dialog
                            ),
                            { id =>
                                customDialogId = id
                            }
                        )    
                    })
                }
                .width(100.percent)
            }
            .height(100.percent)
        }
    }
}
```

```cangjie
// Next.cj

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class Next {
    @State var message: String = 'Back'

    func build() {
        Row() {
            Column() {
                Button(this.message)
                .fontSize(20)
                .fontWeight(FontWeight.Bold)
                .onClick({ evt =>
                    this.getUIContext().getRouter().back()
                })
            }
            .width(100.percent)
        }
        .height(100.percent)
    }
}
```

![image](figures/dialog-levelmode.gif)