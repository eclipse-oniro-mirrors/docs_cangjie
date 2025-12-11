# Button

A Button is a button component typically used to respond to user click actions. It comes in various types including capsule buttons, circular buttons, and standard buttons. When used as a container, a Button can incorporate child components to create buttons containing elements such as text and images. For specific usage, please refer to [Button](../reference/arkui-cj/cj-button-picker-button.md).

## Creating a Button

Buttons are created by calling interfaces, which can be done in two forms:

- Creating a button without child components by specifying a label and [ButtonOptions](../reference/arkui-cj/cj-button-picker-button.md#class-buttonoptions). Examples include the `shape` and `stateEffect` properties in ButtonOptions.

  ```cangjie
  init(label: String, options: ButtonOptions)
  ```

  Here, `label` sets the button text, `type` defines the Button type, and the `stateEffect` property determines whether the Button has click feedback.

  ```cangjie
  Button('Ok', ButtonOptions(shape: ButtonType.Normal, stateEffect: true))
      .borderRadius(8)
      .backgroundColor(0x317aff)
      .width(90)
      .height(40)
  ```

  ![Button](figures/Button.png)

- Creating a button with child components using [ButtonOptions](../reference/arkui-cj/cj-button-picker-button.md#class-buttonoptions). Examples include the `shape` and `stateEffect` properties in ButtonOptions.

  ```cangjie
  init(options: ButtonOptions, content: () -> Unit)
  ```

  Only one child component is supported, which can be either a basic component or a container component.

  ```cangjie
  Button(ButtonOptions(shape: ButtonType.Normal, stateEffect: true)){
      Row() {
          Image(@r(app.media.loading)).width(20).height(40).margin(left: 12)
          Text('loading').fontSize(12).fontColor(0xffffff).margin(left: 5, right: 12)
      }.alignItems(VerticalAlign.Center)
  }
  .borderRadius(8)
  .backgroundColor(0x317aff)
  .width(90)
  .height(40)
  ```

  ![Button2](figures/Button2.png)

## Setting Button Types

Buttons have four optional types: Capsule, Circle, Normal, and ROUNDED_RECTANGLE, configured via the `shape` property.

- Capsule Button (default type).

  The corners of this button type are automatically set to half the height, and cannot be reconfigured using the `borderRadius` property.

  ```cangjie
  Button('Disable', ButtonOptions(shape: ButtonType.Capsule, stateEffect: false))
      .backgroundColor(0x317aff)
      .width(90)
      .height(40)
  ```

  ![Button3](figures/Button3.png)

- Circular Button.

  This button type is perfectly round and does not support corner reconfiguration via the `borderRadius` property.

  ```cangjie
  Button('Circle', ButtonOptions(shape: ButtonType.Circle, stateEffect: false))
      .backgroundColor(0x317aff)
      .width(90)
      .height(90)
  ```

  ![Button4](figures/Button4.png)

- Standard Button.

  This button type has default square corners (radius 0) and supports corner customization via the [borderRadius](../reference/arkui-cj/cj-common-types.md#class-borderradiuses) property.

  ```cangjie
  Button('Ok', ButtonOptions(shape: ButtonType.Normal, stateEffect: true))
      .borderRadius(8)
      .backgroundColor(0x317aff)
      .width(90)
      .height(40)
  ```

  ![Button5](figures/Button5.png)

## Customizing Styles

- Setting Border Radius.

  Use universal attributes to customize button styles. For example, configure the border radius via the [borderRadius](../reference/arkui-cj/cj-common-types.md#class-borderradiuses) property.

  ```cangjie
  Button('circle border', ButtonOptions(shape: ButtonType.Normal))
      .borderRadius(20)
      .height(40)
  ```

  ![Button6](figures/Button6.png)

- Setting Text Styles.

  Apply text styles to customize the button's text display.

  ```cangjie
  Button('font style', ButtonOptions(shape: ButtonType.Normal))
      .fontSize(20)
      .fontColor(0xffffc0cb)
  ```

  ![Button7](figures/Button7.png)

- Setting Background Color.

  Use the [backgroundColor](../reference/arkui-cj/cj-universal-attribute-background.md#func-backgroundcolorresourcecolor) property to define the button's background color.

  ```cangjie
  Button('background color').backgroundColor(0xF55A42)
  ```

  ![Button8](figures/Button8.png)

- Creating Functional Buttons.

  Create a button for delete operations.

  ```cangjie
  Button(ButtonOptions(shape: ButtonType.Circle, stateEffect: true)) {
      Image(@r(app.media.ic_public_delete_filled))
        .width(30)
        .height(30)
  }
  .width(55)
  .height(55)
  .margin(left:20)
  .backgroundColor(0xF55A42)
  ```

  ![Button9](figures/Button9.png)

## Adding Events

Button components are typically used to trigger actions. You can bind the [onClick](../reference/arkui-cj/cj-universal-event-click.md#func-onclickclickevent---unit) event to define custom behaviors upon click.

```cangjie
  Button('Ok', ButtonOptions(shape: ButtonType.Normal, stateEffect: true))
      .onClick({ evt =>
      Hilog.info(0, '', 'Button onClick')
  })
```

## Usage Examples

- Form Submission.

  On user login/registration pages, use buttons for login or registration actions.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*

  @Entry
  @Component
  class EntryView {
      func build() {
          Column() {
              TextInput(placeholder: 'input your username')
                .margin(top: 20)
              TextInput(placeholder: 'input your password')
                .margin(top: 20)
              Button('Register')
                .width(300)
                .margin(top: 20)
                .onClick({ evt =>
                    // Action to perform
                    })
          }
          .padding(20)
      }
  }
  ```

  ![Button10](figures/Button10.png)

- Floating Button.

  In scrollable interfaces, maintain a floating button that stays visible during scrolling.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import kit.LocalizationKit.AppResource
  import ohos.resource.__GenerateResource__

  @Entry
  @Component
  class EntryView {
      private var arr: Array<Int64> = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
      func build() {
          Stack() {
              List(space: 20, initialIndex: 0) {
                  ForEach(
                      this.arr,
                      itemGeneratorFunc: {
                          item: Int64, _: Int64 => ListItem() {
                              Text("${item}")
                                  .width(100.percent)
                                  .height(100)
                                  .fontSize(16)
                                  .textAlign(TextAlign.Center)
                                  .borderRadius(10)
                                  .backgroundColor(0xFFFFFF)
                          }
                      }
                  )
              }.width(90.percent)

              Button() {
                  Image(@r(app.media.startIcon))
                      .width(50)
                      .height(50)
              }
              .shape(ButtonType.Circle)
              .width(60)
              .height(60)
              .position(x: 80.percent, y: 600)
              .shadow(radius: 10.0)
              .onClick ({
                  evt =>
                  // Action to perform
              })
          }
          .width(100.percent)
          .height(100.percent)
          .backgroundColor(0xDCDCDC)
          .padding(top: 5)
      }
  }
  ```

  ![floating_button](figures/floating_button.gif)