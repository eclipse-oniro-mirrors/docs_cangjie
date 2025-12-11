# RichEditor

RichEditor is a component that supports mixed text-image layout and interactive text editing, typically used for responding to user input operations involving mixed content, such as comment sections that allow both text and images. For specific usage, refer to [RichEditor](../reference/arkui-cj/cj-text-input-richeditor.md).

## Creating a RichEditor Component Without Attribute String Construction

Creating a RichEditor component without attribute string construction is generally used to display simple mixed text-image information, such as contact details, or in scenarios requiring uniform content formatting, such as certain code editors.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var option: RichEditorTextSpanOptions = RichEditorTextSpanOptions()

    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Create a RichEditor component without attribute string construction")
                    })
            }.width(200)
        }.height(200)
    }
}
```

![bushiyongshuxing](figures/bushiyongshuxing.jpg)

## Setting Properties

### Configuring Custom Selection Menu

Use [bindSelectionMenu](../reference/arkui-cj/cj-text-input-richeditor.md#func-bindselectionmenuricheditorspantype-custombuilder-responsetype-selectionmenuoptions) to set a custom selection menu.

The component comes with a default text selection menu that includes copy, cut, and select-all functions. Users can use this property to define custom menus, such as translating English text, bolding fonts, and other rich menu functionalities.

When custom menus are excessively long, it is recommended to nest a Scroll component internally to prevent keyboard obstruction.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.hilog.*
import ohos.arkui.component.CopyOptions as MyCopyOptions
import std.collection.ArrayList
import ohos.resource.*

@Entry
@Component
class EntryView {
    let controller: RichEditorController = RichEditorController()

    @Builder
    func RightClickTextCustomMenu() {
        Menu() {
            MenuItemGroup() {=>
                MenuItem(startIcon: @r(app.media.startIcon), endIcon: @r(app.media.startIcon), content: "Cut", labelInfo: "Ctrl+X" )
                MenuItem(startIcon: @r(app.media.startIcon), endIcon: @r(app.media.startIcon), content: "Copy", labelInfo: "Ctrl+C" )
                MenuItem(startIcon: @r(app.media.startIcon), endIcon: @r(app.media.startIcon), content: "Paste", labelInfo: "Ctrl+V" )
            }
        }.backgroundColor(0XF0F0F0)
    }
    func build() {
        Scroll() {
            Column {
                RichEditor(this.controller)
                .bindSelectionMenu(
                    spanType: RichEditorSpanType.Text,
                    content: bind(this.RightClickTextCustomMenu, this),
                    responseType: ResponseType.LongPress,
                    options: SelectionMenuOptions( onDisappear: {
                            => Hilog.info(0, " ", "Trigger this callback when the custom selection menu closes")
                        },
                        onAppear: {
                            => Hilog.info(0, " ", "Callback triggered when the custom selection menu appears")
                        }
                    )
                )
                .onReady({ =>
                    controller.addTextSpan(content: "This is a piece of text used to display the selected menu.")
                })
            }
        }
    }
}
```

![caidan](figures/menu.jpg)

## Adding Events

### Adding a Callback Triggered After Component Initialization

Use [onReady](../reference/arkui-cj/cj-text-input-richeditor.md#func-onreadyvoidcallback) to add a callback triggered after component initialization.

This callback can effectively display rich content, including text, images, and emojis, after the component initializes. For example, when using the RichEditor component to display news, this callback can trigger fetching mixed text-image data from a server. The retrieved data can then be populated into the component, ensuring the complete news content is quickly rendered on the page after initialization.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var option: RichEditorTextSpanOptions = RichEditorTextSpanOptions()

    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"The onReady callback content is preset text within the component")
                })
            }.width(200)
        }.height(200)
    }
}
```

![chushihua](figures/chushihua.jpg)

### Adding a Callback Triggered When Component Content Is Selected

Use [onSelect](../reference/arkui-cj/cj-text-input-richeditor.md#func-onselectcallbackricheditorselection-unit) to add a callback triggered when component content is selected.

This callback can enhance operational experience after text selection. For example, after selecting text, the callback can trigger a pop-up menu for users to modify text styles. Alternatively, it can analyze and process the selected text to provide input suggestions, improving text editing efficiency and convenience.

The callback can be triggered in two ways:
1. Via left mouse button selection—pressing the left button to select and releasing it to trigger the callback.
2. Via touch selection—using a finger to select and releasing it to trigger the callback.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()
    var option: RichEditorTextSpanOptions = RichEditorTextSpanOptions()

    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Select this text to trigger the onselect callback.")
                    })
                    .onSelect({value1: RichEditorSelection=>
                        this.controller.addTextSpan(content:"1234")
                    }).width(200).height(200)
                Text("View callback content:").fontSize(10).fontColor(Color.Gray).width(200)
                RichEditor(this.controller1)
                    .width(200)
                    .height(200)
            }.width(200)
        }.height(200)
    }
}
```

![callback](figures/callback.gif)

### Adding Callbacks Triggered Before and After Text-Image Changes

Use [onDidChange](../reference/arkui-cj/cj-text-input-richeditor.md#func-ondidchangeondidchangecallback) to add a callback triggered after text-image changes. This callback is suitable for content saving and synchronization. For example, after a user finishes editing content, this callback can automatically save the latest content locally or synchronize it to a server. It is also useful for content state updates and rendering. For instance, in a to-do list application, after a user edits a to-do description in RichEditor format, this callback can update the display style of the to-do item in the list.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()
    var rangeBefore: TextRange = TextRange(10,13)
    var rangeAfter: TextRange = TextRange(15,18)

    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Before text-image changes, trigger callback.\nAfter text-image changes, trigger callback.")
                    })
                    .onDidChange({ rangeBefore: TextRange, rangeAfter: TextRange=>
                        this.controller1.addTextSpan(content:"\nAfter text-image changes, trigger callback:\nrangeBefore:" + "1234" +
                            "\nrangeAfter：" + "2345")
                        }).width(180)
                Text("View callback content:").fontSize(10).fontColor(Color.Gray).width(70)
                RichEditor(this.controller1).width(200).height(500)
            }.width(200).height(200)
        }
    }
}
```

![richeditor-change](figures/richeditor-change.gif)

### Adding Callbacks Triggered Before and After Input Method Input

Before input method input begins, use [aboutToImeInput](../reference/arkui-cj/cj-text-input-richeditor.md#func-abouttoimeinputcallbackricheditorinsertvalue-bool) to trigger a callback. After input method input completes, use [onImeInputComplete](../reference/arkui-cj/cj-text-input-richeditor.md#func-onimeinputcompletecallbackricheditortextspanresult-unit) to trigger a callback.

These callback mechanisms are suitable for intelligent input assistance. For example:
- Before a user starts typing, use the callback to provide word suggestions.
- After a user completes input, use the callback to perform automated error correction or format conversion.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()

    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Before input method input, trigger callback.\nAfter input method input completes, trigger callback.")
                    })
                    .aboutToImeInput({value:   RichEditorInsertValue=>
                        this.controller1.addTextSpan(content:"Before input method input, trigger callback:\n123")
                        return true;
                    })
                    .onImeInputComplete({value: RichEditorTextSpanResult=>
                        this.controller1.addTextSpan(content:"After input method input completes, trigger callback:\n456")
                    }).width(200).height(200)

                Text("View callback content:").fontSize(10).fontColor(Color.Gray).width(200)
                RichEditor(this.controller1).width(200).height(200)
            }.width(200).height(200)
        }
    }
}
```

![shurufa](figures/shurufa.jpg)

### Adding a Callback Triggered Before Pasting Completes

Use [onPaste](../reference/arkui-cj/cj-text-input-richeditor.md#func-onpastepasteeventcallback) to add a callback triggered before pasting completes.

This callback is suitable for content format processing. For example, when a user copies text containing HTML tags, the callback can include code to convert it into a format supported by the RichEditor component, stripping unnecessary tags or retaining only plain text.

Since the component's default paste behavior is limited to plain text and cannot handle image pasting, developers can use this method to implement mixed text-image paste functionality, replacing the component's default paste behavior.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()
    func build() {
        Column() {
            Column() {
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Copy and paste operations on this text will trigger corresponding callbacks.")
                    })
                    .onPaste({value1:PasteEvent=>
                        this.controller1.addTextSpan(content:"Trigger onPaste callback\n")
                    }).width(300).height(70)
                Text("View callback content:").fontSize(10).fontColor(Color.Gray).width(300)
                RichEditor(this.controller1)
                    .width(300).height(70).width(200)
            }.height(200)
        }
    }
}
```

![zhantie](figures/zhantie.jpg)

## Adding Text Content

In addition to directly inputting content within the component, you can also use [addTextSpan](../reference/arkui-cj/cj-text-input-richeditor.md#func-addtextspanresourcestr-richeditortextspanoptions) to add text content.

This interface enables diverse text styling, such as creating mixed-style text.

If the component is in focus with a blinking cursor, after adding text content via addTextSpan, the cursor position updates and blinks to the right of the newly added text.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()

    func build() {
        Column() {
            Button("addTextSpan")
                .width(200)
                .height(300)
                .fontSize(13)
                .onClick({ evt =>
                    this.controller.addTextSpan(content:"Add a new paragraph of text.")
                })
            RichEditor(this.controller)
                .width(200)
                .height(200)
        }.width(100.percent)
    }
}
```

![add](figures/ad.gif)

## Adding Image Content

Use [addImageSpan](../reference/arkui-cj/cj-text-input-richeditor.md#func-addimagespanresourcestr-richeditorimagespanoptions) to add image content.

This interface can be used for content enrichment and visual presentation, such as adding images to news articles or data visualization graphics to documents.

If the component is in focus with a blinking cursor, after adding image content via addImageSpan, the cursor position updates and blinks to the right of the newly added image.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import kit.LocalizationKit.*
import ohos.arkui.state_macro_manage.*
import ohos.resource.*

@Entry
@Component
class EntryView {
    var controller: RichEditorController = RichEditorController()
    var controller1: RichEditorController = RichEditorController()
    func build() {
        Column() {
            Column() {
                Button("addTextSpan")
                    .width(200)
                    .height(300)
                    .fontSize(13)
                    .onClick({ evt =>
                        this.controller.addImageSpan(value: @r(app.media.startIcon),
                        options: RichEditorImageSpanOptions(
                            imageStyle: RichEditorImageSpanStyle(
                                size: (24.vp, 24.vp)
                            )
                        ))
                    })
                RichEditor(this.controller)
                    .onReady({=>
                        this.controller.addTextSpan(content:"Copy and paste operations on this text will trigger corresponding callbacks.")}).width(200).height(200)
            }.width(200).height(300)
        }
    }
}
```

![tupian](figures/tupian.jpg)