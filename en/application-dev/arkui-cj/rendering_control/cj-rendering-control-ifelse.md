# if/else: Conditional Rendering

Cangjie provides the capability for rendering control. Conditional rendering allows displaying UI content corresponding to different application states using `if`, `else`, and `else if` statements.

## Usage Rules

- Supports `if`, `else`, and `else if` statements.

- The conditional expressions following `if` and `else if` can use either state variables or regular variables (state variables: changes in value trigger real-time UI updates; regular variables: changes in value do not trigger real-time UI updates).

- Permitted within container components to build different child components through conditional rendering statements.

- Conditional rendering statements are "transparent" when it comes to parent-child component relationships. When one or more `if` statements exist between parent and child components, the rules regarding child component usage by the parent component must be followed.

- The build function within each branch must adhere to build function rules and create one or more components. Empty build functions that cannot create components will result in syntax errors.

- Certain container components impose restrictions on the types or quantities of child components. When using conditional rendering statements within these components, these restrictions also apply to components created within the conditional rendering statements. For example, the [Grid](../../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-grid.md) container component only supports [GridItem](../../../../en/application-dev/reference/arkui-cj/cj-scroll-swipe-griditem.md) components as children. When using conditional rendering statements within a Grid, only GridItem components are allowed within those statements.

## Update Mechanism

When the state variables used in the conditional expressions following `if` or `else if` change, the conditional rendering statements will update according to the following steps:

1. Evaluate the conditions of `if` and `else if` statements. If the branch conditions remain unchanged, no further steps are required. If branch conditions change, proceed with steps 2 and 3.

2. Remove all previously built child components.

3. Execute the constructor of the new branch and add the resulting components to the parent container of the `if` statement. If no applicable `else` branch exists, nothing will be built.

Conditions may include Cangjie expressions. For expressions within constructors, such expressions must not modify the application state.

## Usage Scenarios

### Conditional Rendering Using `if`

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
  @State var count: Int64 = 0;
  func build() {
    Column() {
      Text("count=${this.count}")

      if (this.count > 0) {
        Text("count is positive")
          .fontColor(Color.Green)
      }

      Button('increase count')
        .onClick({ =>
          this.count++;
        })

      Button('decrease count')
        .onClick({ =>
          this.count--;
        })
    }
  }
}
```

Each branch of an `if` statement contains a build function. Such build functions must create one or more child components. During initial rendering, the `if` statement executes the build function and adds the generated child components to its parent component.

Whenever state variables used in `if` or `else if` conditional statements change, the conditional statements update and re-evaluate the new condition values. If the condition evaluation result changes, indicating a need to build another conditional branch, the ArkUI framework will:

1. Remove all previously rendered components (from earlier branches).

2. Execute the constructor of the new branch and add the generated child components to its parent component.

In the above example, if `count` increases from 0 to 1, the `if` statement updates, and the condition `count > 0` re-evaluates from `false` to `true`. Thus, the constructor for the true branch executes, creating a Text component and adding it to the parent Column component. If `count` later changes to 0, the Text component is removed from the Column component. Since there is no `else` branch, no new constructor is executed.

### `if ... else ...` Statements and Child Component State

The following example demonstrates an `if ... else ...` statement with child components that have `@State` decorated variables.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
internal import ohos.base.*
internal import ohos.arkui.component.*

@Component
public class CounterView {
      @State var counter: Int64 = 0;
      var label: String = 'unknown';
      func build() {
        Column(space: 20) {
          Text("${this.label}")
          Button("counter ${this.counter} +1")
            .onClick({ =>
              this.counter += 1;
            })
        }
        .margin(10)
        .padding(10)
        .border( width: 1 )
      }
}

@Entry
@Component
public class EntryView {
    @State var toggle: Bool = true;
    func build() {
      Column() {
        if (this.toggle) {
          CounterView( label: "CounterView #positive" )
        } else {
          CounterView( label: "CounterView #negative" )
        }
        Button("toggle ${this.toggle}")
          .onClick({ =>
            this.toggle = !this.toggle;
          })
      }
      .width(100.percent)
      .justifyContent(FlexAlign.Center)
    }
}
```

The CounterView (labeled 'CounterView #positive') child component is created during initial rendering. This child component carries a state variable named `counter`. When the `CounterView.counter` state variable is modified, the CounterView (labeled 'CounterView #positive') child component re-renders while preserving the state variable value. When the `MainView.toggle` state variable changes to `false`, the `if` statement within the MainView parent component updates, subsequently removing the CounterView (labeled 'CounterView #positive') child component. Simultaneously, a new CounterView (labeled 'CounterView #negative') instance is created, with its own `counter` state variable initialized to 0.

> **Note:**
>
> CounterView (labeled 'CounterView #positive') and CounterView (labeled 'CounterView #negative') are two distinct instances of the same custom component. Changes to `if` branches do not update existing child components or preserve their state.

The following example demonstrates modifications needed to preserve the `counter` value when conditions change.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
internal import ohos.base.*
internal import ohos.arkui.component.*

@Component
class CounterView {
    @Link var counter: Int64;
    var label: String = 'unknown';

    func build() {
      Column( 20 ) {
        Text("${this.label}")
          .fontSize(20)
        Button("counter ${this.counter} +1")
          .onClick({ =>
            this.counter += 1;
          })
      }
      .margin(10)
      .padding(10)
      .border(width:1)
    }
}

@Entry
@Component
public class EntryView {
    @State var toggle: Bool = true;
    @State var counter: Int64 = 0;
    func build() {
      Column() {
        if (this.toggle) {
          CounterView( counter: counter, label: 'CounterView #positive' )
        } else {
          CounterView( counter: counter, label: 'CounterView #negative' )
        }
        Button("toggle ${this.toggle}")
          .onClick({ =>
            this.toggle = !this.toggle;
          })
      }
      .width(100.percent)
      .justifyContent(FlexAlign.Center)
    }
}
```

Here, the `@State counter` variable is owned by the parent component. Thus, when CounterView component instances are deleted, this variable is not destroyed. The CounterView component references the state via the `@Link` decorator. The state must be moved from the child to its parent (or parent's parent) to avoid losing state when conditional content or repeated content is destroyed.

### Nested `if` Statements

Nested conditional statements do not affect the relevant rules of parent components.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
internal import ohos.base.*
internal import ohos.arkui.component.*
@Entry
@Component
public class EntryView {
    @State var toggle: Bool = false;
    @State var toggleColor: Bool = false;
    func build() {
      Column( 20 ) {
        Text('Before')
          .fontSize(15)
        if (this.toggle) {
          Text('Top True, positive 1 top')
            .backgroundColor(Color.Green).fontSize(20)
          // Inner if statement
          if (this.toggleColor) {
            Text('Top True, Nested True, positive COLOR  Nested ')
              .backgroundColor(Color.Green).fontSize(15)
          } else {
            Text('Top True, Nested False, Negative COLOR  Nested ')
              .backgroundColor(Color.Blue).fontSize(15)
          }
        } else {
          Text('Top false, negative top level').fontSize(20)
            .backgroundColor(Color.Red)
          if (this.toggleColor) {
            Text('positive COLOR  Nested ')
              .backgroundColor(Color.Green).fontSize(15)
          } else {
            Text('Negative COLOR  Nested ')
              .backgroundColor(Color.Blue).fontSize(15)
          }
        }
        Text('After')
          .fontSize(15)
        Button('Toggle Outer')
          .onClick({ =>
            this.toggle = !this.toggle;
          })
        Button('Toggle Inner')
          .onClick({ =>
            this.toggleColor = !this.toggleColor;
          })
      }
      .width(100.percent)
      .justifyContent(FlexAlign.Center)
    }
}
```