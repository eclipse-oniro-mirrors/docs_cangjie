# @Watch Macro: State Variable Change Notification

@Watch is applied to monitor state variables. If developers need to track whether a state variable's value has changed, they can use @Watch to set up a callback function for that state variable.

@Watch provides the capability to monitor state variables, but it can only detect observable changes.

Before reading this document, developers are advised to have a basic understanding of state management observation capabilities. It is recommended to first read: [@State](./cj-macro-state.md).

## Overview

@Watch is used to monitor changes in state variables. When a state variable changes, the @Watch callback method will be invoked. Internally, the ArkUI framework uses strict equality (==) to determine whether a value has been updated, adhering to strict equality standards. When the strict equality comparison returns false (indicating inequality), the @Watch callback is triggered.

## Macro Description

| @Watch Supplemental Variable Macro | Description |
| :--------------------------------- | :---------- |
| Macro Parameter | Required. Name of the callback method. |
| Macro Order | The order of macros does not affect functionality. Developers can arrange macro order as needed. It is recommended to place [@State](./cj-macro-state.md), [@Prop](./cj-macro-prop.md), [@Link](./cj-macro-link.md), etc., before @Watch macros for consistent style. |
| @Watch Trigger Timing | When using @Watch to monitor state variable changes, the callback is triggered at the exact moment the variable is actually changed and assigned. |

## Observing Changes and Behavior

1. When a state variable change is observed (including changes to corresponding keys in two-way bound [AppStorage](./cj-appstorage.md) and [LocalStorage](./cj-localstorage.md)), the corresponding @Watch callback method will be triggered.
2. @Watch methods are executed synchronously after custom component property updates.
3. If other state variables are modified within an @Watch method, this will also trigger state changes and @Watch execution.
4. During initial initialization, @Watch-decorated methods are not invoked, as initialization is not considered a state variable change. @Watch callbacks are only invoked for subsequent state changes.

## Constraints

- Developers should avoid infinite loops. Loops may occur if the same state variable is directly or indirectly modified within an @Watch callback. To prevent loops, it is recommended not to modify the currently decorated state variable within the @Watch callback.
- Developers should consider performance. Property value update functions delay component re-rendering (see behavior above), so callback functions should only perform quick computations.
- Asynchronous operations are not recommended in @Watch functions, as @Watch is designed for rapid calculations. Asynchronous behavior may cause performance issues with re-rendering speed.
- @Watch parameters are mandatory and must be the name of a declared method; otherwise, a compilation error will occur.

  ```cangjie
  @State @Watch[] var count : Int64 = 10
  @State @Watch["onChanged"] var count : Int64 = 10
  // Correct usage
  @State @Watch[onChanged] var count: Int64 = 0
  func onChanged(){
      Hilog.info(0, "xxx", "xxx")
  }
  ```

- Parameters within @Watch must be the name of a declared method; otherwise, a compilation error will occur.

  ```cangjie
  // Incorrect usage: No corresponding function name, compilation error
  @State @Watch[change] var count: Int64 = 0
  func onChanged(){
      Hilog.info(0, "xxx", "xxx")
  }

  // Correct usage
  @State @Watch[change] var count: Int64 = 0
  func change(){
      Hilog.info(0, "xxx", "xxx")
  }
  ```

- Regular variables cannot be decorated with @Watch; otherwise, a compilation error will occur.

  ```cangjie
  // Incorrect usage
  @Watch[change] var count: Int64 = 0
  func change(){
      Hilog.info(0, "xxx", "xxx")
  }

  // Correct usage
  @State @Watch[change] var count: Int64 = 0
  func change(){
      Hilog.info(0, "xxx", "xxx")
  }
  ```

## Usage Scenarios

### @Watch and Custom Component Updates

The following example demonstrates the steps for component updates and @Watch handling. `count` is decorated with @State in `CountModifier` and with @Link in `TotalView`.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Component
class TotalView {
  @Link @Watch[onCountUpdated] var count: Int64 = 0
  @State var total: Int64 = 0
  // @Watch callback
  func onCountUpdated(): Unit {
    this.total += this.count
  }
  func build() {
    Text("Total: ${this.total}")
  }
}

@Entry
@Component
class EntryView {
  @State var count: Int64 = 0
  func build() {
    Column() {
      Button("add to basket")
        .onClick{ e =>
          this.count++
        }
      TotalView(count: this.count)
    }
  }
}
```

Processing steps:

1. The `Button.onClick` event in the `EntryView` custom component increments `count`.
2. Due to the @State `count` variable change, the @Link in the child component `TotalView` is updated, and its @Watch("onCountUpdated") method is invoked, updating the `total` variable in `TotalView`.
3. The `Text` component in `TotalView` is re-rendered.

### Combining @Watch with @Link

The following example illustrates how to observe an @Link variable in a child component.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList
import std.random.*

@Component
class BasketViewer{
    @Link @Watch[onBasketUpdated] var shopBasket : ArrayList<Float64>
    @State var totalPurchase: Float64 = 0.0
    func updateTotal(): Float64 {
        var total : Float64 = 0.0
        for(i in shopBasket){
            total += i
        }
        if (total >= 100.0) {
            total = 0.9 * total
        }
        return total
    }
    // @Watch callback
    func onBasketUpdated(){
        this.totalPurchase = this.updateTotal()
    }
    func build() {
        Column(){
            ForEach(this.shopBasket,itemGeneratorFunc:
                { item: Float64, index : Int64 =>
                    Text("${index}")
                    Text("Price：${item} €")
                    }
                )
            Text("Total: ${this.totalPurchase} €")
        }
    }
}

@Entry
@Component
class EntryView {
    @State var shopBasket : ArrayList<Float64> =  ArrayList<Float64>([0.0])
    let m : Random = Random()
    func build() {
        Column(){
            Button("Add to basket")
                .onClick{ etv =>
                    var temp = this.shopBasket.clone()
                    temp.add(100.0 * m.nextFloat64())
                    this.shopBasket = temp }
            BasketViewer(shopBasket : shopBasket)
        }
    }
}
```

Processing steps:

1. The `Button.onClick` in `BasketModifier` adds an entry to `BasketModifier shopBasket`.
2. The @Link-decorated `BasketViewer shopBasket` value changes.
3. The state management framework invokes the @Watch function `BasketViewer onBasketUpdated` to update the `BasketViewer TotalPurchase` value.
4. The change in @Link `shopBasket` adds a new array item, causing the `ForEach` component to execute its item Builder and render a new Item. The @State `totalPurchase` change also triggers re-rendering of the corresponding `Text` component. Re-rendering occurs asynchronously.

### Using changedPropertyName for Different Logic Handling

The following example demonstrates how to use `changedPropertyName` in an @Watch function for different logic handling.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView{
    @State @Watch[countUpdated] var apple: Int64 = 0
    @State @Watch[countUpdated] var cabbage: Int64 = 0
    @State var propName :String = "test"
    @State var fruit : Int64 = 0
    func countUpdated(){
        if (this.propName=="apple") {
            this.fruit = this.apple
        }
    }
    func build(){
        Column(){
            Text("Number of apples: ${this.apple.toString()}")
                .fontSize(30)
            Text("Number of cabbages: ${this.cabbage.toString()}")
                .fontSize(30)
            Text("Total number of fruits: ${this.fruit.toString()}")
                .fontSize(30)
            Button("Add apples")
                .onClick{etv=> this.apple++
                    this.propName = "apple"}
            Button("Add cabbages")
                .onClick{etv=> this.cabbage++
                    this.propName = "cabbages"}

        }
    }
}
```

Processing steps:

1. When `Button("Add apples")` is clicked, the value of `apple` changes.
2. The state management framework invokes the @Watch function `countUpdated`. The changed state variable name is `apple`, satisfying the `if` condition, so `fruit` is updated.
3. The `Text` components bound to `apple` and `fruit` state variables are re-rendered.
4. When `Button("Add cabbages")` is clicked, the value of `cabbage` changes.
5. The state management framework invokes the @Watch function `countUpdated`. The changed state variable name is `cabbage`, which does not satisfy the `if` condition, so `fruit` remains unchanged.
6. The `Text` component bound to the `cabbage` state variable is re-rendered.