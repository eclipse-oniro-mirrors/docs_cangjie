# Text Input (TextInput/TextArea)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

TextInput and TextArea are input field components, typically used to respond to user input operations such as comment section inputs, chat box inputs, form inputs, etc. They can also be combined with other components to build functional pages, such as login/registration pages. For specific usage, please refer to [TextInput](../reference/arkui-cj/cj-text-input-textinput.md) and [TextArea](../reference/arkui-cj/cj-text-input-textarea.md).

## Creating Input Fields

TextInput is a single-line input field, while TextArea is a multi-line input field. They can be created using the following interfaces.

```cangjie
init(placeholder!: ?ResourceStr = None, text!: ?ResourceStr = None, controller!: ?TextInputController = None)
```

```cangjie
init(placeholder!: ?ResourceStr = None, text!: ?ResourceStr = None,controller!: ?TextAreaController = None)
```

- Single-line input field.

    ```cangjie
    TextInput()
    ```

    ![Text](figures/Text.png)

- Multi-line input field.

    ```cangjie
    TextArea()
    ```

    ![Text1](figures/Text1.png)

- Multi-line input field text will automatically wrap when it exceeds one line.

    ```cangjie
    TextArea(text: "I am TextArea I am TextArea I am TextArea I am TextArea" ).width(300)
    ```

    ![Text2](figures/Text2.png)

## Customizing Styles

- Setting placeholder text when there is no input.

    ```cangjie
    TextInput(placeholder: 'I am placeholder text')
    ```

    ![Text10](figures/Text10.png)

- Setting the current text content of the input field.

    ```cangjie
    TextInput( placeholder: 'I am placeholder text', text: 'I am the current text content' )
    ```

    ![Text11](figures/Text11.png)

- Adding backgroundColor to change the background color of the input field.

    ```cangjie
    TextInput( placeholder: 'I am placeholder text', text: 'I am the current text content' )
    .backgroundColor(0x4D0A59F7)
    ```

    ![Text12](figures/Text12.png)

    More diverse styles can be achieved by combining [Universal Attributes](../reference/arkui-cj/cj-universal-attributes.md#universal-attributes).

## Selection Menu

When text in the input field is selected, a menu containing options like Cut, Copy, and Translate will appear.

TextInput:

```cangjie
TextInput( text: 'This is a piece of text to demonstrate the selection menu')
```

![Text13](figures/Text13.png)

TextArea:

```cangjie
TextArea( text: 'This is a piece of text to demonstrate the selection menu')
```

![Text13](figures/Text13.png)

## Keyboard Avoidance

After the keyboard is raised, keyboard avoidance will only take effect for container components with scrolling capabilities during screen orientation changes. If you want keyboard avoidance to work for container components without scrolling capabilities, it is recommended to nest them within a container component that has scrolling capabilities, such as [Scroll](../reference/arkui-cj/cj-scroll-swipe-scroll.md), [List](../reference/arkui-cj/cj-scroll-swipe-list.md), or [Grid](../reference/arkui-cj/cj-scroll-swipe-grid.md).

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var placeHolderArr: Array<String> = ["1", "2", "3", "4", "5", "6", "7"];
    func build() {
        Scroll() {
            Column {
                ForEach(this.placeHolderArr, itemGeneratorFunc: {placeholder: String, _: Int64 =>
                TextInput( placeholder: 'TextInput ' + placeholder )
                .margin(30)}
                )
            }
        }
        .height(100.percent)
        .width(100.percent)
    }
}
```

![textinputkeyboardavoid](figures/TextInputKeyboardAvoid.gif)

## Common Issues

### How to Set the Minimum Display Lines for TextArea and Enable Adaptive Height

**Problem Description**

Set the initial height of TextArea to control the minimum number of text lines to display. When the input text exceeds the initial height, the TextArea height adapts automatically.

**Solution**

Set minLines, or set height to LengthMetrics.AUTO and use constraintSize to calculate the height yourself.

``` cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let textAreaPadding = 12.0
    let setMaxLines = 3.0
    let changeText = "I am TextArea"
    @State var fullText: String = this.changeText
    @State var originText: String = this.changeText

    func build() {
        Column() {
            TextArea(text: 'constraintSize: ' + this.fullText)
            .fontSize(18)
            .padding(top: this.textAreaPadding, bottom: this.textAreaPadding)
            .width(300)
            .height(LengthMetrics.AUTO)
            .constraintSize(
                // Calculate with padding, set to display at least this.setMaxLines lines of text.
                // If elderly-friendly font scaling is involved, need to listen and adjust height.
                minHeight: (this.textAreaPadding * 2.0 + this.setMaxLines * 21.0)
            )

            Blank(min: 50)
            Button("Input something")
            .onClick({ evt =>
                this.fullText += this.changeText
            })
        }
        .justifyContent(FlexAlign.Center)
        .width(100.percent)
        .padding(top: 30)
    }
}
```
![textAreaAuto](figures/TextArea-auto.gif)
