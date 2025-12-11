# Creating Custom Components

In ArkUI, all UI-displayed content consists of components. Those provided directly by the framework are called system components, while those defined by developers are called custom components. When developing UI interfaces, it is usually not just a simple combination of system components but also requires consideration of code reusability, separation of business logic from UI, and future version evolution. Therefore, encapsulating the UI and part of the business logic into custom components is an essential capability.

Custom components have the following characteristics:

- **Composable**: Allows developers to combine system components, their properties, and methods.

- **Reusable**: Custom components can be reused by other components and instantiated in different parent components or containers.

- **Data-Driven UI Updates**: UI refreshes are driven by changes in state variables.

## Basic Usage of Custom Components

The following example demonstrates the basic usage of custom components.

```cangjie
@Component
class HelloComponent {
    @State var message : String = "Hello, World!"
    func build() {
        // The HelloComponent custom component combines the system components Row and Text
        Row(){
            Text(this.message)
                // Changes to the state variable message drive UI updates, refreshing the UI from "Hello, World!" to "Hello, Cangjie!"
                .onClick({etv=>this.message="Hello, Cangjie!"})
        }
    }
}
```

HelloComponent can be created multiple times in the `build()` function of other custom components to achieve reuse.

```cangjie
@Entry
@Component
class EntryView {
    func build() {
        Column(){
            Text("ArkUI message")
            HelloComponent(message: "Hello, World!")
            Divider()
            HelloComponent(message: "Hello, World!")
        }
    }
}
```

To fully understand the above example, the following conceptual definitions of custom components are required, which will be introduced in later sections:

- Basic structure of custom components
- Member functions/variables
- Parameter specifications for custom components
- `build()` function
- Common styles for custom components

## Basic Structure of Custom Components

### class

Custom components are implemented based on `class`. The combination of `class` + custom component name + `{...}` forms a custom component, and inheritance relationships are not allowed.

> **Note:**
>
> The custom component name, class name, and function name cannot be the same as system component names.

### @Component

The `@Component` macro can only decorate data structures declared with the `class` keyword. A `class` decorated with `@Component` gains componentization capabilities and must implement the `build` method to describe the UI. A `class` can only be decorated by one `@Component`.

```cangjie
@Component
class MyComponent {
}
```

**Usage Restrictions:**

The total number of member variables (including ordinary member variables and state variables) in a `class` type (custom component) decorated with `@Component` cannot exceed 128.

### build() Function

The `build()` function is used to define the declarative UI description of a custom component. A custom component must define the `build()` function.

```cangjie
@Component
class MyComponent {
    func build() {
    }
}
```

### @Entry

A custom component decorated with `@Entry` serves as the entry point of a UI page. In a single UI page, only one custom component can be decorated with `@Entry`. `@Entry` can accept an optional [LocalStorage](../state_management/cj-localstorage.md) parameter.

```cangjie
@Entry
@Component
class MyComponent {
}
```

#### EntryOptions

| Name      | Type                                      | Required | Description                          |
|:----------|:------------------------------------------|:---------|:-------------------------------------|
| storage   | [LocalStorage](../state_management/cj-localstorage.md) | No       | Page-level UI state storage.         |

### @Reusable

A custom component decorated with `@Reusable` has reusable capabilities. For details, see [@Reusable Macro: Component Reuse](./cj-macro-reusable.md#usage-scenarios).

```cangjie
@Reusable
@Component
class MyComponent {
}
```

## Member Functions/Variables

In addition to implementing the `build()` function, custom components can also implement other member functions, which are subject to the following constraints:

- Member functions of custom components are private, and it is not recommended to declare them as static functions.

Custom components can include member variables, which are subject to the following constraints:

- Member variables of custom components are private, and it is not recommended to declare them as static variables.

- Some member variables of custom components require local initialization, while others do not. For details on whether local initialization is needed and whether member variables of child components need to be initialized via parameters passed from parent components, see [State Management](../state_management/cj-state-management-overview.md).

## Parameter Specifications for Custom Components

As seen in the previous example, custom components can be created in the `build` method. During the creation of a custom component, parameters are initialized according to macro rules.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Component
class MyComponent {
    private var countDownFrom: Int64 = 0
    private var color: Color = Color.Blue
    func build() {
    }
}

@Entry
@Component
class EntryView {
    private var someColor: Color = Color.Red
    func build() {
        Column(){
            // Create an instance of MyComponent, initializing the member variable countDownFrom to 10 and the member variable color to this.someColor
            MyComponent(countDownFrom: 10 , color: this.someColor)
        }
    }
}
```

The following example code passes a function from the parent component to the child component and calls it in the child component.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var cnt : Int64 = 0
    func submit():UInt{
        this.cnt++
        return 0
    }
    func build() {
        Column(){
            Text("${this.cnt}")
            Child(Childsubmit: this.submit)
        }
    }
}

@Component
class Child {
    let Childsubmit : () -> UInt
    func build() {
        Row(){
            Button("add")
                .width(80)
                .onClick({etv=> this.Childsubmit()})
        }
    }
}
```

## build() Function

All statements declared in the `build()` function are collectively referred to as UI descriptions and must adhere to the following rules:

- For a custom component decorated with `@Entry`, the root node under the `build()` function must be unique, necessary, and a container component. `ForEach` is prohibited as the root node.
- For a custom component decorated with `@Component`, the root node under the `build()` function must be unique and necessary, and it can be a non-container component. `ForEach` is prohibited as the root node.

  <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import kit.LocalizationKit.*
  import ohos.resource.__GenerateResource__

  @Entry
  @Component
  class EntryView{
      func build() {
          // The root node must be unique, necessary, and a container component
          Row(){
              ChildComponent()
          }
      }
  }

  @Component
  class ChildComponent {
      func build() {
          // The root node must be unique and necessary, and can be a non-container component
          Image(@r(app.media.startIcon))
      }
  }
  ```

- Local variable declarations are not allowed. Counterexample:

  ```cangjie
  func build() {
      let num :Int64 = 0
  }
  ```

- Direct use of `Hilog.info` in UI descriptions is not allowed, but it is permitted in methods or functions. Counterexample:

  ```cangjie
  func build() {
      // Counterexample: Hilog.info is not allowed
      Hilog.info(0, "HilogCj","print debug log" )
  }
  ```

- Creating local scopes is not allowed. Counterexample:

  ```cangjie
  func build() {
      // Counterexample: Local scopes are not allowed
      {
          // ...
      }
  }
  ```

- Calling methods not decorated with `@Builder` is not allowed. However, the parameters of system components can be the return values of CJ methods.

  ```cangjie
  @Component
  class EntryView {
      func doSomeCalculations() {

      }
      func calcTextValue():String {
          return "Hello World"
      }
      @Builder func doSomeRender() {
          Text("Hello World")
      }
      func build() {
          Column() {
              // Counterexample: Cannot call methods not decorated with @Builder
              this.doSomeCalculations()
              // Correct: Can call
              this.doSomeRender()
              // Correct: Parameters can be the return values of CJ methods
              Text(this.calcTextValue())
          }
      }
  }
  ```

- The `match` syntax is not allowed. If conditional judgment is needed, use [if](../rendering_control/cj-rendering-control-ifelse.md) instead. Example:

  ```cangjie
  func build() {
      Column() {
          // Counterexample: match syntax is not allowed
          match(expression ) {
              case 0 => Text("...")
              case 1 => Text("...")
              case _ => Text("...")
          }
          // Correct: Use if
          if(expression == 1) {
              Text("...")
          } else if(expression == 2) {
              Button("...")
          } else {
              Text("...")
          }
      }
  }
  ```

- Direct modification of state variables is not allowed. Counterexample. For a detailed analysis, see [@State Common Issues: Modifying State Variables in build Is Not Allowed](../state_management/cj-macro-state.md#modifying-state-variables-in-build-is-not-allowed).

  ```cangjie
  @Component
  class EntryView {
      @State var textColor : Color = Color(0xFFFF00)
      @State var columnColor : Color  = Color.Green
      @State var count : Int64 = 1
      func build() {
          Column() {
              // Directly modifying the value of count in the Text component is not allowed
              Text("${this.count++}")
                  .width(50)
                  .height(50)
                  .fontColor(this.textColor)
                  .onClick({etv=> this.columnColor = Color.Red})
              Button("change textColor")
                  .onClick({etv=> this.textColor = Color.Blue})
          }
          .backgroundColor(this.columnColor)
      }
  }
  ```

## Common Styles for Custom Components

Custom components set common styles via chained calls with ".".

```cangjie
@Component
class ChildComponent {
    func build() {
        Button("Hello World")
    }
}

@Entry
@Component
class MyComponent {
    func build() {
        Row(){
            ChildComponent()
            .width(200)
            .height(300)
            .backgroundColor(Color.Red)
        }
    }
}
```

> **Note:**
>
> When ArkUI sets styles for custom components, it is equivalent to wrapping the `ChildComponent` in an invisible container component. These styles are applied to the container component, not directly to the `Button` component in `ChildComponent`. The rendering result shows that the red background color is not applied directly to the `Button` but to the invisible container component where the `Button` resides.