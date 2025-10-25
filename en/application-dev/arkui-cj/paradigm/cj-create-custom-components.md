# Creating Custom Components

In ArkUI, all UI-displayed content consists of components. Those provided directly by the framework are called system components, while those defined by developers are called custom components. When developing UI interfaces, it is usually not just about combining system components but also considering factors such as code reusability, separation of business logic from UI, and future version evolution. Therefore, encapsulating the UI and part of the business logic into custom components is an essential capability.

Custom components have the following characteristics:

- **Composable**: Allows developers to combine system components, their properties, and methods.
- **Reusable**: Custom components can be reused by other components and instantiated in different parent components or containers.
- **Data-driven UI updates**: UI refreshes are driven by changes in state variables.

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
                // Changes to the state variable message drive UI updates, changing from "Hello, World!" to "Hello, Cangjie!"
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

To fully understand the above example, it is necessary to grasp the following conceptual definitions of custom components, which will be introduced in later sections.

## Basic Structure of Custom Components

### class

Custom components are implemented based on `class`. The combination of `class` + custom component name + `{...}` forms a custom component, and inheritance relationships are not allowed.

> **Note:**
>
> The custom component name, class name, and function name cannot be the same as system component names.

### @Component

The `@Component` macro can only decorate data structures declared with the `class` keyword. A `class` decorated with `@Component` gains component capabilities and must implement the `build` method to describe the UI. A `class` can only be decorated by one `@Component`.

```cangjie
@Component
class MyComponent {
}
```

**Usage Restrictions:**

A `class` type (custom component) decorated with `@Component` cannot have more than 128 member variables (including ordinary member variables and state variables).

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

A custom component decorated with `@Entry` serves as the entry point for a UI page. In a single UI page, only one custom component can be decorated with `@Entry`. `@Entry` can accept an optional [LocalStorage](../state_management/cj-localstorage.md) parameter.

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
- Local initialization of member variables in custom components is optional for some and mandatory for others. For details on whether local initialization is required or whether member variables need to be initialized by passing parameters from parent components, refer to [State Management](../state_management/cj-state-management-overview.md).

## Parameter Rules for Custom Components

From the examples above, we have learned that custom components can be created in the `build` method. During the creation of custom components, parameters are initialized according to macro rules.

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

The following example demonstrates passing a function from a parent component to a child component and calling it in the child component.

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

## build() Function Rules

All statements declared in the `build()` function are collectively referred to as UI descriptions and must adhere to the following rules:

- For custom components decorated with `@Entry`, the root node under the `build()` function must be unique, necessary, and a container component. `ForEach` is prohibited as the root node.
- For custom components decorated with `@Component`, the root node under the `build()` function must be unique and necessary, and it can be a non-container component. `ForEach` is prohibited as the root node.

     <!-- run -->

  ```cangjie
  package ohos_app_cangjie_entry
  import kit.ArkUI.*
  import ohos.arkui.state_macro_manage.*
  import kit.LocalizationKit.*

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

- Local variable declarations are not allowed. Example of incorrect usage:

  ```cangjie
  func build() {
      let num :Int64 = 0
  }
  ```

- Direct use of `Hilog.info` in UI descriptions is not allowed, but it is permitted within methods or functions. Example of incorrect usage:

  ```cangjie
  func build() {
      // Incorrect: Hilog.info is not allowed
      // Hilog.info(0, "AppLogCj","print debug log" )
  }
  ```

- Creating local scopes is not allowed. Example of incorrect usage:

  ```cangjie
  func build() {
      // Incorrect: Local scopes are not allowed
      {
          // ...
      }
  }
  ```

- Calling methods not decorated with `@Builder` is not allowed. However, the parameters of system components can be the return values of CJ methods.

  ```cangjie
  @Component
  class EntryView{
      func doSomeCalculations(){

      }
      func calcTextValue():String{
          return "Hello World"
      }
      @Builder func doSomeRender(){
          Text("Hello World")
      }
      func build() {
          Column(){
              // Incorrect: Cannot call methods not decorated with @Builder
              this.doSomeCalculations()
              // Correct: Can call
              this.doSomeRender()
              // Correct: Parameters can be return values of CJ methods
              Text(this.calcTextValue())
          }
      }
  }
  ```

- The `match` syntax is not allowed. For conditional logic, use [if](../rendering_control/cj-rendering-control-ifelse.md) instead. Example:

  ```cangjie
  func build(){
      Column(){
          // Incorrect: match syntax is not allowed
          match(expression ){
              case 0 => Text("...")
              case 1 => Text("...")
              case _ => Text("...")
          }
          // Correct: Use if
          if(expression == 1){
              Text("...")
          }else if(expression == 2){
              Button("...")
          }else {
              Text("...")
          }
      }
  }
  ```

- Direct modification of state variables is not allowed. Example of incorrect usage. For detailed analysis, see [@State FAQ: No Direct Modification of State Variables in build](../state_management/cj-macro-state.md#no-direct-modification-of-state-variables-in-build).

  ```cangjie
  @Component
  class EntryView{
      @State var textColor : Color = Color(0xFFFF00)
      @State var columnColor : Color  = Color.Green
      @State var count : Int64 = 1
      func build(){
          Column(){
              // Incorrect: Directly modifying count within the Text component is not allowed
              Text("${this.count++}")
                  .width(50)
                  .height(50)
                  .fontColor(this.textColor)
                  .onClick({etv=> this.columnColor = Color.Red})
              Button("change textColor")
                  .onClick({etv=> this.textColor = Color.PINK})
          }
          .backgroundColor(this.columnColor)
      }
  }
  ```