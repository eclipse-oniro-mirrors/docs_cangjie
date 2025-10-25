# Declarative UI Description

The Cangjie programming language uses a declarative approach to compose and extend components for describing application UIs, while also providing basic property, event, and child component configuration methods to help developers implement application interaction logic.

## Building Components

Based on different component construction methods, creating components includes both parameterized and non-parameterized approaches.

### Without Parameters

If a component's interface definition doesn't include mandatory construction parameters, then the "()" after the component doesn't need any configuration. For example, the Divider component doesn't include construction parameters.

<!-- run-->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column() {
            Text("item 1")
            Divider()
            Text("item 2")
        }
    }
}
```

### With Parameters

If a component's interface definition includes construction parameters, then the "()" after the component needs to configure corresponding parameters.

- The mandatory src parameter for the Image component.

  ```cangjie
  Image("https://xyz/test.jpg")
  ```

- The optional content parameter for the Text component.

  ```cangjie
  // string-type parameter
  Text("test")
  // @r form to reference application resources, applicable for multilingual scenarios
  Text(@r(app.string.title_value))
  // parameterless form
  Text() {}
  ```

- Variables or expressions can also be used for parameter assignment, where the result type returned by the expression must meet the parameter type requirements.

  For example, setting variables or expressions to construct parameters for Image and Text components.

  ```cangjie
  Image(this.imagePath)
  Image("https://" + this.imageUrl)
  Text("count: ${this.count}")
  ```

## Configuring Properties

Property methods are configured using "." chained calls to style system components and other properties. It's recommended to write each property method on a separate line.

- Configuring the font size for a Text component.

  ```cangjie
  Text("test")
    .fontSize(12)
  ```

- Configuring multiple properties for a component.

  ```cangjie
  Image("test.jpg")
    .alt("error.jpg")
    .width(100)
    .height(100)
  ```

- In addition to passing constant parameters directly, variables or expressions can also be passed.

  ```cangjie
  Text("hello")
    .fontSize(this.size)
  Image("test.jpg")
    .width(if(this.count % 2 == 0) {100} else {200})
    .height(this.offset + 100)
  ```

- For system components, the Cangjie programming language also predefines some enumeration types for their properties, which developers can call. Enumeration types can be passed as parameters but must meet the parameter type requirements.

  For example, the color and font style of a Text component can be configured as follows.

  ```cangjie
  Text("hello")
    .fontSize(20)
    .fontColor(Color.Red)
    .fontWeight(FontWeight.Bold)
  ```

## Configuring Events

Event methods are configured using "." chained calls for events supported by system components. It's recommended to write each event method on a separate line.

- Using arrow functions to configure component event methods.

  ```cangjie
  Button("Click me")
  .onClick({ =>
    this.myText = "Cangjie"
  })
  ```

- Using arrow function expressions to configure component event methods, requiring the use of "{ => ...}" to ensure the function is bound to the component while complying with Cangjie programming language syntax specifications.

  ```cangjie
  Button("add counter")
    .onClick({ =>
      this.counter += 2
    })
  ```

- Using declared Lambda expressions that can be called directly.

  ```cangjie
  var fn: () -> Unit = {=>}
  protected func aboutToAppear() {
      fn = { =>
          this.counter++
      }
  }
  ...
  Button("add counter")
    .onClick(fn)
  ```

> **Note:**
>
> The 'this' inside arrow functions is lexically scoped and determined by the context. Anonymous functions may have ambiguous 'this' references, which are not allowed in the Cangjie programming language.

## Configuring Child Components

If a component supports child component configuration, then child component UI descriptions need to be added within the trailing closure "{...}". Components like Column, Row, Stack, Grid, and List are all container components.

Here's a simple example of configuring child components for a Column component.

```cangjie
Column() {
  Text("Hello")
    .fontSize(100)
  Divider()
  Text(this.myText)
    .fontSize(100)
    .fontColor(Color.Red)
}
```

Container components all support child component configuration, enabling relatively complex multi-level nesting.

```cangjie
Column() {
  Row() {
    Image("test1.jpg")
      .width(100)
      .height(100)
    Button("click +1")
      .onClick({ =>
        Hilog.info(0, "cangjie", +1 clicked!");
      })
  }
}
```