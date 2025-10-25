# @Builder Macro: Custom Builder Functions

The Cangjie UI provides a lightweight mechanism for UI element reuse through @Builder, where the internal UI structure is fixed and only data is exchanged with the caller. Developers can abstract reusable UI elements into a method and invoke it within the build method.

For simplicity, we refer to functions decorated with @Builder as "custom builder functions."

Before reading this document, it is recommended to review: [Basic Syntax Overview](./cj-basic-syntax-overview.md), [Declarative UI Description](./cj-declarative-ui-description.md), [Custom Components - Creating Custom Components](./cj-create-custom-components.md).

## Macro Usage Instructions

The @Builder macro can be used in two ways: as a private custom builder function defined within a custom component or as a global custom builder function defined globally.

### Private Custom Builder Function

Definition syntax:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @Builder
    func showTextBuilder() {
        Text("Hello World")
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
    }

    @Builder
    func showTextValueBuilder(param: String) {
        Text(param)
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
    }

    func build() {
        Column {
            // No parameters
            this.showTextBuilder()
            // With parameters
            this.showTextValueBuilder("Hello @Builder")
        }
    }
}
```

Usage method:

```cangjie
this.showTextBuilder()
```

- Allows defining one or more @Builder methods within a custom component, which are considered private, special-type member functions of the component.

- Private custom builder functions can be invoked within the custom component, the build method, and other custom builder functions.

- Within the custom function body, `this` refers to the current component, and the component's state variables can be accessed within the custom builder function. It is recommended to access the component's state variables via `this` rather than through parameter passing.

### Global Custom Builder Function

Definition syntax:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Builder
func showTextBuilder() {
    Text("Hello World")
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
}

@Entry
@Component
class EntryView {

    func build() {
        Column {
            showTextBuilder()
        }
    }
}
```

Usage method:

```cangjie
showTextBuilder()
```

- If component state changes are not involved, it is recommended to use global custom builder methods.

- Global custom builder functions can be invoked within the build method and other custom builder functions.

## Parameter Passing Rules

Custom builder functions support two parameter passing methods: [pass-by-value](#pass-by-value-parameters) and [pass-by-reference](#pass-by-reference-parameters). Both must adhere to the following rules:

- The parameter type must match the declared parameter type.

- Within a function decorated with @Builder, modifying parameter values is not allowed.

- UI syntax within @Builder follows [UI Syntax Rules](./cj-create-custom-components.md).

- Pass-by-reference occurs only when a single parameter is passed and the parameter requires direct object literal input. All other passing methods are pass-by-value.

### Pass-by-Value Parameters

By default, functions decorated with @Builder use pass-by-value. When passing state variables as parameters, changes to the state variables do not trigger UI refreshes within the @Builder method. Therefore, when using state variables, [pass-by-reference](#pass-by-reference-parameters) is recommended.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Builder
func overBuilder(paramA1: String) {
    Row {
        Text("UseStateVarByValue: ${paramA1}")
    }
}

@Entry
@Component
class EntryView {
    @State var label: String = "Hello"

    func build() {
        Column {
            overBuilder(label)
        }
    }
}
```

### Pass-by-Reference Parameters

When passing parameters by reference, the parameters can be state variables, and changes to the state variables will trigger UI refreshes within the @Builder method.

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Observed
class Tmp {
    @Publish
    var paramA1: String = ""

}

@Builder
func overBuilder(params: Tmp) {
    Row {
        Text("UseStateVarByReference: ${params.paramA1}")
    }
}

@Entry
@Component
class EntryView {
    @State var tmp: Tmp = Tmp(paramA1: "Hello")

    func build() {
        Column {
            // When invoking the overBuilder component in the parent component,
            // pass the parameter to the overBuilder component by reference.
            overBuilder(tmp)
            Button("Click me")
            .onClick({
                _ =>
                // After clicking "Click me," the UI text changes to "ArkUI."
                this.tmp.paramA1 = "ArkUI"
            })
        }
    }
}
```

## Constraints

Dynamic UI rendering is triggered only when parameters are passed by reference in @Builder. Refer to [Pass-by-Reference Parameters](#pass-by-reference-parameters).

## Usage Scenarios

### Using Custom Builder Functions Within Custom Components

Create a private @Builder method and invoke it within a Column using `this.builder()`. Use the `aboutToAppear` lifecycle function and button click events to modify the content of `builder_value`, enabling dynamic UI rendering.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var builder_value: String = "Hello"

    @Builder
    func builder() {
        Column {
            Text(this.builder_value)
            .fontSize(30)
            .fontWeight(FontWeight.Bold)
        }
    }

    protected override func aboutToAppear() {
        this.builder_value = "Hello World"
    }

    func build() {
        Row {
            Column {
                Text(this.builder_value)
                .fontSize(30)
                .fontWeight(FontWeight.Bold)

                this.builder()
                Button("Click to change builder_value content")
                .onClick{
                    e =>
                    this.builder_value = "builder_value was clicked"
                }
            }
        }
    }
}
```

### Using Global Custom Builder Functions

Create a global @Builder method and invoke it within a Column using `overBuilder()`. Pass parameters in the form of object literals. Changes to values, whether simple or complex, will trigger UI refreshes.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.ArrayList

@Observed
class ChildTmp {
    @Publish
    var val: Int64 = 1
}

@Observed
class Tmp {
    @Publish
    var tmp_value: ChildTmp = ChildTmp()
    @Publish
    var str_value: String = "Hello"
    @Publish
    var num_value: Int64 = 0
    @Publish
    var arrayTmp_value: ObservedArrayList<ChildTmp> = ObservedArrayList<ChildTmp>()
}

@Builder
func overBuilder(param: Tmp) {
    Column {
        Text("str_value: ${param.str_value}")
        Text("num_value: ${param.num_value}")
        Text("tmp_value: ${param.tmp_value.val}")
        ForEach(
            param.arrayTmp_value,
            itemGeneratorFunc: {
                item: ChildTmp, idx: Int64 => Text("arrayTmp_value: ${item.val}")
            }
        )
    }
}

@Entry
@Component
class EntryView {
    @State
    var objParam: Tmp = Tmp()

    func build() {
        Column {
            Text("Render UI by invoking @Builder").fontSize(20)
            overBuilder(this.objParam)

            Line()
                .width(100.percent)
                .height(10)
                .backgroundColor(0x000000)
                .margin(10)

            Button("Click to change parameter values").onClick(
                {
                    _ =>
                    this.objParam.str_value = "Hello World"
                    this.objParam.num_value = 1
                    this.objParam.tmp_value.val = 8
                    let child_value: ChildTmp = ChildTmp(val: 2)
                    this.objParam.arrayTmp_value.append(child_value)
                }
            )
        }
    }
}
```

### Modifying Macro-Decorated Variables to Trigger UI Refresh

In this scenario, @Builder is only used to display the Text component and does not participate in dynamic UI refresh functionality. Changes to the Text component's value are triggered by the macro's feature of listening for value changes, not by @Builder's capability.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Observed
class Tmp {
    @Publish var str_value: String = "Hello"
}

@Entry
@Component
class EntryView {
    @State var objParam: Tmp = Tmp()
    @State var label: String = "World"

    @Builder
    func privateBuilder() {
        Column {
            Text("wrapBuilder str_value: ${this.objParam.str_value}")
            Text("wrapBuilder num: ${this.label}")
        }
    }

    func build() {
        Column {
            Text("Render UI by invoking @Builder")
            .fontSize(20)
            this.privateBuilder()
            Line()
            .width(100.percent)
            .height(10)
            .backgroundColor(0x000000)
            .margin(10)

            Button("Click to change parameter values")
            .onClick({
                _ =>
                this.objParam.str_value = "str_value: Hello World"
                this.label = "label Hello World"
            })
        }

    }
}
```

### Passing customBuilder Types Using Global and Local @Builder

When a parameter type is `customBuilder`, a defined @Builder function can be passed in because `customBuilder` is essentially a Function or Unit type, and @Builder is also a Function type. In this scenario, passing @Builder achieves specific effects.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Builder
func myBuilder2() {
    Column {
        Text("Global Builder")
    }
    .width(100.percent)
    .height(100.percent)
    .align(Alignment.Center)
}

@Entry
@Component
class EntryView {
    @State var isShow: Bool = false
    @State var isShow2: Bool = false

    @Builder
    func myBuilder() {
        Column {
            Text("Local Builder")
        }
        .width(100.percent)
        .height(100.percent)
        .align(Alignment.Center)
    }

    func build() {
        Column {
            Button("Local Builder")
            .onClick{
              e => this.isShow = true
            }
            .fontSize(20)
            .margin(10)
            .bindSheet(this.isShow, myBuilder, options: SheetOptions(onDisappear: {=> this.isShow = false}) )

            Button("Global Builder")
            .onClick{
              e => this.isShow2 = true
            }
            .fontSize(20)
            .margin(10)
            .bindSheet(this.isShow2, myBuilder2, options: SheetOptions(onDisappear: {=> this.isShow2 = false}) )
        }
        .justifyContent(FlexAlign.Center)
        .backgroundColor(Color.White)
        .width(100.percent)
        .height(100.percent)
    }
}
```### Multi-layer @Builder Method Nesting Usage

Calling custom components or other @Builder methods within an @Builder method enables scenarios of multiple @Builder nestings. To achieve dynamic UI refresh functionality for the innermost @Builder, it is essential to ensure that each layer of @Builder invocation uses pass-by-reference.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Observed
class Tmp {
    @Publish var paramA1: String = ""
}

@Builder
func parentBuilder(params: Tmp) {
    Row {
        Text("parentBuilder: ${params.paramA1}")
    }
    childBuilder(params)
}

@Builder
func childBuilder(params: Tmp) {

    Row {
        Text("childBuilder: ${params.paramA1}")
    }
    grandsonBuilder(params)
}

@Builder
func grandsonBuilder(params: Tmp) {

    Row {
        Text("grandsonBuilder: ${params.paramA1}")
    }
}

@Entry
@Component
class EntryView {
    @State var tmp: Tmp = Tmp(paramA1: "Hello")

    func build() {
        Column {
            parentBuilder(this.tmp)
            Text(this.tmp.paramA1)
            Button("Click me")
            .onClick({
                _ =>
                this.tmp.paramA1 = "ArkUI"
            })
        }
    }
}
```