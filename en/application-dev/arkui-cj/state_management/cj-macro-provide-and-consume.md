# @Provide and @Consume Macros: Two-Way Synchronization with Descendant Components

`@Provide` and `@Consume` are used for two-way data synchronization with descendant components, applicable in scenarios where state data needs to be passed across multiple levels. Unlike the parent-child component parameter passing mechanism mentioned earlier, `@Provide` and `@Consume` eliminate the constraints of parameter passing, enabling cross-level data transfer.

The variable decorated with `@Provide` resides in the ancestor component and can be understood as a state variable "provided" to descendant components. The variable decorated with `@Consume` resides in the descendant component and "consumes (binds)" the state variable provided by the ancestor component.

`@Provide` / `@Consume` enables two-way synchronization across component hierarchies. Before reading the documentation for `@Provide` and `@Consume`, developers are advised to have a basic understanding of UI paradigm syntax and custom components. It is recommended to review the following beforehand: [Basic Syntax Overview](../paradigm/cj-basic-syntax-overview.md), [Declarative UI Description](../paradigm/cj-declarative-ui-description.md), [Custom Components - Creating Custom Components](../paradigm/cj-create-custom-components.md).

## Overview

State variables decorated with \@Provide / \@Consume have the following characteristics:

- The state variable decorated with \@Provide is automatically available to all descendant components, meaning the variable is "provided" to its descendants. This demonstrates the convenience of \@Provide, as developers do not need to pass variables multiple times between components.

- Descendants use \@Consume to access the variable provided by \@Provide, establishing two-way data synchronization between \@Provide and \@Consume. Unlike \@State / \@Link, the former can be passed across multi-level parent-child components.

- \@Provide and \@Consume can be bound using the same variable name or alias, but their types must match. Otherwise, implicit type conversion may occur, leading to abnormal application behavior.

```cangjie
// Binding via the same variable name
@Provide
var age: Int64 = 0;
@Consume
var age: Int64;

// Binding via the same variable alias
@Provide["a"]
var id: Float64 = 0.0;
@Consume["a"]
var age: Float64;
```

When \@Provide and \@Consume are bound using the same variable name or alias, the variable decorated with \@Provide has a one-to-many relationship with the variable(s) decorated with \@Consume. If multiple \@Provide-decorated variables with the same name or alias are declared within the same custom component (including its child components), the \@Consume-decorated variable will match the nearest \@Provide-decorated variable by searching upward.

Additionally, if an alias is declared in the \@Provide annotation, the \@Consume variable must be bound using the corresponding alias. The \@Provide variable cannot be found by variable name alone.

## Macro Description

The rules for `@State` also apply to `@Provide`. The difference is that `@Provide` also serves as a synchronization source for multi-level descendants.

|\@Provide|Description|
|:---|:---|
|Macro Parameter|Alias: A constant string, optional. If an alias is specified, the variable is bound via the alias; if not, it is bound via the variable name.|
|Synchronization Type|Two-way synchronization. Data synchronization occurs from the \@Provide variable to all \@Consume variables and vice versa. The two-way synchronization behavior is the same as the combination of \@State and \@Link.|
|Allowed Variable Types|Cangjie built-in types include basic data types (except Nothing) and custom types, as well as arrays of these types. Function types and DateTime types are supported. The types of \@Provide and \@Consume variables must match. For supported types, refer to "Observing Changes."|
|Initial Value of Decorated Variable|The type must be specified, and the initial value must be provided.|
|\@Provide Supports Duplicate Names|Duplicate names are allowed. \@Consume will match the nearest \@Provide by searching upward.|

|\@Consume|Description|
|:---|:---|
|Macro Parameter|Alias: A constant string, optional. If an alias is provided, there must be an \@Provide variable with the same alias for a successful match. If no alias is provided, the variable name and type must match.|
|Synchronization Type|Two-way: From the \@Provide variable (see \@Provide) to all \@Consume variables and vice versa. The two-way synchronization behavior is the same as the combination of \@State and \@Link.|
|Allowed Variable Types|Cangjie built-in types include basic data types (except Nothing) and custom types, as well as arrays of these types. Function types and DateTime types are supported. The types of \@Provide and \@Consume variables must match. For supported types, refer to "Observing Changes."|
|Initial Value of Decorated Variable|The type must be specified, but no initial value is allowed.|

## Variable Passing/Access Rules

|\@Provide Passing/Access|Description|
|:---|:---|
|Initialization and Update from Parent Component|Optional. Allows initialization of the child component's \@Provide with regular variables (assigning regular variables to \@Provide only initializes the value; changes to regular variables do not trigger UI updates; only state variables can trigger UI updates), \@State, \@Link, \@Prop, \@Provide, \@Consume, \@Publish, \@StorageLink, \@StorageProp, \@LocalStorageLink, and \@LocalStorageProp-decorated variables.|
|Used to Initialize Child Components|Allowed. Can be used to initialize \@State, \@Link, \@Prop, and \@Provide.|
|Synchronization with Parent Component|No.|
|Synchronization with Descendant Components|Two-way synchronization with \@Consume.|
|Access Outside Component|Private. Can only be accessed within the component.|

|\@Consume Passing/Access|Description|
|:---|:---|
|Initialization and Update from Parent Component|Prohibited. Initialized from \@Provide using the same variable name or alias.|
|Used to Initialize Child Components|Allowed. Can be used to initialize \@State, \@Link, \@Prop, and \@Provide.|
|Synchronization with Ancestor Component|Two-way synchronization with \@Provide.|
|Access Outside Component|Private. The visibility of the decorated variable follows the `private` modifier.|

## Observing Changes and Behavior

### Observing Changes

- When the decorated data type is integer, float, boolean, character, or string, numerical changes can be observed.

- When the decorated object is a tuple, array, or range, updates to the array elements can be observed.

- When the decorated object is DateTime, the overall assignment of DateTime can be observed. Additionally, DateTime properties can be updated by calling its functions: `addDays(Int64)`, `addHours(Int64)`, `addMinutes(Int64)`, `addMonths(Int64)`, `addNanoseconds(Int64)`, `addSeconds(Int64)`, `addWeeks(Int64)`, and `addYears(Int64)`.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.time.*

// Parent component
@Entry
@Component
class EntryView{

    @Provide
    var selectedDate: DateTime = DateTime.of(year:2021,month:8,dayOfMonth:8)

    public func build(){
        Column(){
            Button("parent increase the day by 1")
                .margin(10)
                .onClick{
                    => this.selectedDate = this.selectedDate.addDays(1)
                }
            Button("parent update the new date")
                .margin(10)
                .onClick{
                    => this.selectedDate = DateTime.of(year:2023,month:7,dayOfMonth:7)
                }
            DatePicker(
                start: DateTime.of(year:1970,month:1,dayOfMonth:1),
                end: DateTime.of(year:2100,month:1,dayOfMonth:1),
                selected: this.selectedDate
            )
           Child()
        }
    }
}

@Component
class Child{

    @Consume
    var selectedDate: DateTime;

    public func build(){
        Column(){
            Button("child increase the day by 1")
                .onClick{
                    => this.selectedDate = this.selectedDate.addDays(1)
                }
            Button("child update the new date")
                .margin(10)
                .onClick{
                    => this.selectedDate = DateTime.of(year:2023,month:9,dayOfMonth:9)
                }
            DatePicker(
                start: DateTime.of(year:1970,month:1,dayOfMonth:1),
                end: DateTime.of(year:2100,month:1,dayOfMonth:1),
                selected: this.selectedDate
            )
        }
    }
}
```

![img1](figures/provide_1_datepicker.gif)

- When the decorated variable is a HashMap, the overall assignment of HashMap can be observed. Additionally, HashMap values can be updated by calling its interfaces: `set()`, `clear()`, and `remove()`.

- When the decorated variable is a HashSet, the overall assignment of HashSet can be observed. Additionally, HashSet values can be updated by calling its interfaces: `add()`, `clear()`, and `remove()`.

- Function-type variables can be decorated, and changes in their output values can be observed.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

public func returnAdd(a: Int64, b:Int64): Int64{
    return a+b
}

public func returnMinus(a: Int64, b:Int64): Int64{
    return a-b
}

@Entry
@Component
class EntryView{

    @Provide["calc"]
    var Func1: (Int64, Int64) -> Int64 = returnAdd

    @Provide
    var isAdd : Bool = true

    func build(){
        Column{
            Text("Parent")
            Text(
                if(isAdd == true){
                    "1+1 = ${Func1(1,1)}"
                }else{
                    "1-1 = ${Func1(1,1)}"}
            )
            Button(
                if(isAdd == true){
                    "Switch to minus"
                }else{
                    "Switch to add"
                }
            ).onClick{ evt =>
                if(isAdd == true){ Func1 = returnMinus }
                else{ Func1 = returnAdd }
                isAdd = !isAdd
            }
            Divider()
            Child()
        }
    }
}

@Component
class Child{
    @Consume["calc"]
    var Func2: (Int64, Int64) -> Int64

    @Consume
    var isAdd: Bool

    func build(){
        Column{
            Text("Child")
            Text(
                if(isAdd == true){
                    "1+1 = ${Func2(1,1)}"
                }else{
                    "1-1 = ${Func2(1,1)}"}
            )
            Button(
                if(isAdd == true){
                    "Switch to minus"
                }else{
                    "Switch to add"
                }
            ).onClick{ evt =>
                if(isAdd == true){ Func2 = returnMinus }
                else{ Func2 = returnAdd }
                isAdd = !isAdd
            }
        }
    }
}
```

![img2](figures/provide_2_decorFunc.gif)

### Framework Behavior

1. Initial Rendering:
   a. The variable decorated with \@Provide calls `addProvideVar` in the component's constructor, storing the state variable's key and value in a map to prepare for \@Consume state variables in descendant components. It also registers the state variable and saves the custom component it belongs to.
   b. If a descendant component uses an \@Consume variable, it calls `initializeConsume` in its constructor to retrieve the state variable from the map. If not found, a runtime error is thrown. After finding the matching \@Provide variable, it registers the state variable and saves the custom component it belongs to.

2. When \@Provide / \@Consume-decorated data changes:
   a. When the state variable is used, the `get` function in `prop` is triggered, which calls the `get` function in `ObservedProperty`, thereby calling `recordDependentUpdate` to record the component IDs related to the state variable. This prepares for component updates when the state variable changes.
   b. When the state variable is modified, the `set` function in `prop` is triggered, calling the `set` function in `ObservedProperty`. The `set` function triggers the state variable's `notifyChanges` function, which calls the `onStateUpdate` function of the component bound to the state variable. The component IDs needing updates are assigned to `dirtDescendantElementIds`, and `markNeedUpdate` is called to update the UI. The UI update invokes `CustomView`'s `rerender` function, followed by `updateDirtyElements`, which retrieves and executes the update function for each component based on its ID.
   c. After rendering, the state variable continues executing the `set` function, updating each state variable bound in `subProps_` by calling their `set` functions. This repeats step 2 to render other components, achieving minimal rendering.

## Constraints

1. The key parameter for \@Provide / \@Consume must be a string literal; otherwise, a compilation error will occur.

    **Counterexample:**

    ```cangjie
    let change: Int64 = 10;
    @Provide[change]
    var message: String = "Hello"

    let change: String = "10"
    @Provide[change]
    var message: String = "Hello"
    ```

    **Correct Example:**

    ```cangjie
    @Provide["10"]
    var message: String = "Hello"
    ```

2. The variable decorated with \@Consume cannot be initialized locally or via constructor parameters. Initialization of \@Consume variables has no effect. \@Consume can only be initialized by matching the corresponding \@Provide variable via key.

    **Counterexample:**

    ```cangjie
    // Parent component
    @Entry
    @Component
    class EntryView {
        @Provide
        var message: String = "Hello";

        func build() {
            Column() {
                Child()
            }
        }
    }

    @Component
    class Child {
        // Incorrect: Cannot initialize locally
        @Consume
        var msg: String = "Hello";

        func build() {
            Text(this.msg)
        }
    }
    ```

    **Correct Example:**

    ```cangjie
    @Component
    class Child {
        @Consume
        var num: Int64;

        func build() {
            Column() {
                Text("num's value: ${this.num}")
            }
        }
    }

    // Parent component
    @Entry
    @Component
    class EntryView {
        @Provide
        var num: Int64 = 10;

        func build() {
            Column() {
                Text("num's value: ${this.num}")
                Child()
            }
        }
    }
    ```

3. When \@Provide keys (variable names or aliases) are duplicated, \@Consume will bind to the nearest \@Provide-decorated variable by searching upward in the component tree.

    ```cangjie
    // If variable names are duplicated, \@Consume will bind to the last \@Provide-decorated variable.
    // Types must match; otherwise, the framework will throw a runtime error.
    @Provide
    var count: Int32 = 10
    @Provide
    var count: Int64 = 10

    // If aliases are duplicated, \@Consume will bind to the last \@Provide-decorated variable.
    // Similarly, types must match.
    @Provide["a"]
    var count: Int32 = 10
    @Provide["a"]
    var num: Int64 = 10
    ```

4. When initializing an \@Consume variable, if the developer does not define an \@Provide variable with the corresponding key, the framework will throw a runtime error, indicating that initialization failed because no \@Provide variable with the matching key (variable name or alias) could be found.

    **Counterexample:**

    ```cangjie
    @Component
    class Child{
        @Consume
        var num: Int64

        func build(){
            Column(){
                Text("num's value: ${this.num}")
            }
        }
    }

    // Parent component
    @Entry
    @Component
    class EntryView{
        // Incorrect: Missing @Provide
        var num: Int64 = 10;

        func build(){
            Column(){
                Text("num's value: ${this.num}")
                Child()
            }
        }
    }
    ```

    **Correct Example:**

    ```cangjie
    @Component
    class Child{
        @Consume
        var num: Int64

        func build(){
            Column(){
                Text("num's value: ${this.num}")
            }
        }
    }

    // Parent component
    @Entry
    @Component
    class EntryView{
        @Provide
        var num: Int64 = 10;

        func build(){
            Column(){
                Text("num's value: ${this.num}")
                Child()
            }
        }
    }
    ```## Usage Scenarios

The following example demonstrates a two-way state synchronization scenario between parent and child components using `@Provide` and `@Consume`. When clicking the Button within the EntryView and ToDoItem components respectively, changes to the `count` value will be bidirectionally synchronized between EntryView and ToDoItem.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Component
class ToDoItem {

    // The @Consume decorated variable binds to the @Provide decorated variable in its ancestor component EntryView through the same property name
    @Consume
    var count: Int64;

    func build(){
        Column{
            Text("count(${this.count})")
            Button("count(${this.count}), count + 1")
                .onClick{
                   evt => this.count += 1
            }
        }.width(100.percent)
    }
}

@Component
class ToDoList{
    func build(){
        Row(space: 5){
            ToDoItem()
            ToDoItem()
        }
    }
}

@Component
class ToDoDemo{
    func build(){
        Column{
            ToDoList()
        }
    }
}

@Entry
@Component
class EntryView{
    // The @Provide decorated variable count is provided by the entry component EntryView to its descendant components
    @Provide
    var count: Int64 = 0;

    func build(){
        Column{
            Button("count(${this.count}), count + 1")
                .onClick{
                   evt => this.count += 1
                }
            ToDoDemo()
        }
    }
}
```

![img3](figures/provide_3_binding.gif)

### Decorating Map Type Variables

In the following example, the `message` variable is of type `HashMap<Int64, String>`. Clicking the Button to modify the `message` value will trigger view updates accordingly.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.HashMap

@Component
class Child {
    @Consume
    var message: HashMap<Int64, String> = HashMap<Int64, String>()

    @Consume
    var arr: Array<(Int64, String)>

    func build(){
        Column(){
            ForEach(arr,
                { item: (Int64, String), idx: Int64 =>
                    Text("key: ${item[0]} value: ${item[1]}").fontSize(30)
                    Divider()
                },
                keyGeneratorFunc: {item: (Int64, String), idx: Int64
                    => "${idx}_${item[0]}" + item[1]
                })
            Button("Consume init map").onClick{
                evt =>
                    this.message = HashMap<Int64, String>([(0,"a"),(1,"b"),(3,"c")])
                    arr = message.toArray()
            }
            Button("Consume set new one").onClick{
                evt =>
                    this.message.add(4,"d")
                    arr = message.toArray()
            }
            Button("Consume clear").onClick{
                evt =>
                    this.message.clear()
                    arr = message.toArray()
            }
            Button("Consume replace the first item").onClick{
                evt =>
                    this.message.add(0,"aa")
                    arr = message.toArray()
            }
            Button("Consume delete the first item").onClick{
                evt =>
                    this.message.remove(0)
                    arr = message.toArray()
            }
        }
    }
}

@Entry
@Component
class EntryView {
    @Provide
    var message: HashMap<Int64, String> = HashMap<Int64, String>([(0,"a"),(1,"b"),(3,"c")])

    @Provide
    var arr: Array<(Int64, String)> = []

    public override func onPageShow(){
        arr = message.toArray()
    }

    func build(){
        Row(){
            Column(){
                Button("Provide init map").onClick{
                    evt =>
                        this.message = HashMap<Int64,String>([(0,"a"),(1,"b"),(3,"c"),(4,"d")])
                        arr = message.toArray()
                }
                Child()
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

![img4](figures/provide_4_map.gif)

### Decorating Set Type Variables

In the following example, the `message` variable is of type `HashSet<Int64>`. Clicking the Button to modify the `message` value will trigger view updates accordingly.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.*

@Component
class Child{
    @Consume
    var message: HashSet<Int64>

    @Consume
    var arr: Array<Int64>

    func build(){
        Column{
            ForEach(arr,{item: Int64, idx: Int64 =>
                Text("${item}").fontSize(30)
                Divider()
            })
            Button("Consume init set").onClick{
                evt =>
                    this.message = HashSet<Int64>([0,1,2,3,4])
                    this.arr = this.message.toArray()
            }
            Button("Consume set new one").onClick{
                evt =>
                    this.message.add(5)
                    this.arr = this.message.toArray()
            }
            Button("Consume clear").onClick{
                evt =>
                    this.message.clear()
                    this.arr = this.message.toArray()
            }
            Button("Consume delete the first one").onClick{
                evt =>
                    this.message.remove(0)
                    this.arr = this.message.toArray()
            }
        }
    }
}

@Entry
@Component
class EntryView{
    public override func onPageShow(){
        arr = message.toArray()
    }

    @Provide
    var message: HashSet<Int64> = HashSet([0,1,2,3,4])

    @Provide
    var arr: Array<Int64> = []

    func build(){
        Row(){
            Column(){
                Button("Provide init Set").onClick{
                    evt =>
                    this.message = HashSet<Int64>([0,1,2,3,4,5])
                    this.arr = this.message.toArray()
                }
                Child()
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

![img5](figures/provide_5_set.gif)