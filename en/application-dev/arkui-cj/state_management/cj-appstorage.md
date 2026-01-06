# AppStorage: Application-wide UI State Storage

AppStorage is an application-wide UI state storage that is bound to the application process. It is created by the UI framework when the application starts, providing a centralized storage for the UI state properties of the application.

Unlike AppStorage, LocalStorage is page-level and typically used for data sharing within a page. AppStorage, on the other hand, is application-level global state sharing and serves as the "hub" of the entire application. [PersistentStorage](./cj-persiststorage.md) and [Environment](./cj-environment.md) variables interact with the UI through AppStorage.

> **Note:**
>
> AppStorage only supports pure Cangjie scenarios and is not suitable for mixed development scenarios involving ArkTS and Cangjie.

This document focuses on the usage scenarios of AppStorage and related macros: @StorageProp and @StorageLink.

AppStorage is designed to provide developers with broader cross-ability basic data sharing, unlike macros such as @State, which can only be passed along the component tree. Before reading this document, developers are advised to have a macro-level understanding of AppStorage's role in the state management framework. It is recommended to read [State Management Overview](cj-state-management-overview.md) in advance.

AppStorage also provides API interfaces, allowing developers to manually trigger additions, deletions, modifications, and queries of AppStorage keys outside custom components. It is recommended to read the [AppStorage API Documentation](../../reference/arkui-cj/cj-state-rendering-appstatemanagement.md#class-appstorage) in conjunction with this document.

## Overview

AppStorage is a singleton created when the application starts. Its purpose is to provide centralized storage for application state data, which is accessible at the application level. AppStorage retains its properties during the application's runtime. Properties are accessed via unique key string values.

AppStorage can synchronize with UI components and can be accessed in application business logic.

Properties in AppStorage can be bidirectionally synchronized. Data can exist locally or on remote devices, with different functionalities for local and remote devices, such as data persistence (see [PersistentStorage](./cj-persiststorage.md)). This data is implemented in business logic, decoupled from the UI. To use this data in the UI, [@StorageProp](#storageprop) and [@StorageLink](#storagelink) are required.

## @StorageProp

As mentioned earlier, to establish a connection between AppStorage and custom components, the @StorageProp and @StorageLink macros are used. Decorating variables within a component with @StorageProp(key)/@StorageLink(key) links them to AppStorage properties, where `key` identifies the AppStorage property.

When a custom component initializes, the variables decorated with @StorageProp(key)/@StorageLink(key) are initialized using the corresponding key's property value in AppStorage. Due to differences in application logic, it cannot be guaranteed that the corresponding property has been stored in AppStorage before component initialization. Therefore, local initialization of these variables is necessary.

@StorageProp(key) establishes one-way data synchronization with the corresponding property in AppStorage. If the property associated with the given key in AppStorage changes, the change will be synchronized to @StorageProp, overwriting local modifications.

### Macro Usage Rules

| @StorageProp Variable Macro | Description |
|:---|:---|
| Macro Parameter | `key`: Constant string, required (the string must be quoted). |
| Allowed Variable Types | Class, String, integer, float, Bool, enum types, and arrays of these types.<br>Supports Datetime, Map, and Set types. For nested types, see [Observing Changes and Behavior](#observing-changes-and-behavior).<br>The type must be specified and should match the corresponding property type in LocalStorage to avoid implicit type conversion, which may cause application behavior anomalies.<br>Any type is not supported. |
| Synchronization Type | One-way synchronization: From the AppStorage property to the component's state variable. Once the given property in AppStorage changes, it will overwrite local modifications. |
| Initial Value of Decorated Variable | Must be specified. If the property does not exist in AppStorage, this initial value will initialize the property and store it in AppStorage. |

### Variable Passing/Access Rules

| Passing/Access | Description |
|:---|:---|
| Initialization and Update from Parent Node | Prohibited. @StorageProp does not support initialization from parent nodes. It can only be initialized by the corresponding key in AppStorage. If the key does not exist, the local default value will be used. |
| Initializing Child Nodes | Supported. Can be used to initialize [@State](./cj-macro-state.md), [@Link](./cj-macro-link.md), [@Prop](./cj-macro-prop.md), and [@Provide](./cj-macro-provide-and-consume.md). |
| Access Outside Component | No. |

**@StorageProp Initialization Rule Diagram**

![StorageProp](figures/StorageProp.png)

### Observing Changes and Behavior

#### Observing Changes

- When the decorated data type is Bool, String, integer, or float, numerical changes can be observed.
- When the decorated data type is a class, object assignment and property changes can be observed (see [Using AppStorage and LocalStorage from UI](#using-appstorage-and-localstorage-from-ui)).
- When the decorated object is an Array, changes such as adding, deleting, or updating array elements can be observed.
- When the decorated object is a Datetime, overall assignment of Datetime can be observed. Additionally, Datetime properties can be updated by calling its methods: `addYears`, `addMonths`, `addWeeks`, `addMinutes`, `addSeconds`, and `addNanoseconds`. See [Decorating Datetime Type Variables](#decorating-datetime-type-variables).
- When the decorated variable is a Map, overall assignment of Map can be observed. Additionally, Map values can be updated by calling its methods: `add`, `clear`, and `remove`. See [Decorating Map Type Variables](#decorating-map-type-variables).
- When the decorated variable is a Set, overall assignment of Set can be observed. Additionally, Set values can be updated by calling its methods: `add`, `clear`, and `remove`. See [Decorating Set Type Variables](#decorating-set-type-variables).

#### Framework Behavior

- Variables decorated with @StorageProp are immutable.
- When the data decorated with @StorageProp(key) is a state variable, it will trigger re-rendering of the associated custom component.
- When the property corresponding to the key in AppStorage changes, it will synchronize with all data decorated with @StorageProp(key), overwriting local modifications.

## @StorageLink

@StorageLink(key) establishes bidirectional data synchronization with the corresponding property in AppStorage:

1. Local modifications are written back to AppStorage.
2. Changes in AppStorage are synchronized to all properties bound to the corresponding key, including one-way (@StorageProp and one-way binding variables created via Prop), two-way (@StorageLink and two-way binding variables created via Link), and other instances (e.g., PersistentStorage).

### Macro Usage Rules

| @StorageLink Variable Macro | Description |
|:---|:---|
| Macro Parameter | `key`: Constant string, required (the string must be quoted). |
| Allowed Variable Types | Class, String, integer, float, Bool, enum types, and arrays of these types.<br>Supports Datetime, Map, and Set types. For nested types, see [Observing Changes and Behavior](#observing-changes-and-behavior).<br>The type must be specified and should match the corresponding property type in LocalStorage to avoid implicit type conversion, which may cause application behavior anomalies.<br>Any type is not supported. |
| Synchronization Type | Two-way synchronization: From AppStorage property to custom component, and from custom component to AppStorage property. |
| Initial Value of Decorated Variable | Must be specified. If the property does not exist in AppStorage, this initial value will initialize the property and store it in AppStorage. |

### Variable Passing/Access Rules

| Passing/Access | Description |
|:---|:---|
| Initialization and Update from Parent Node | Prohibited. |
| Initializing Child Nodes | Supported. Can be used to initialize regular variables, @State, @Link, @Prop, and @Provide. |
| Access Outside Component | No. |

**@StorageLink Initialization Rule Diagram**

![StorageLink](figures/StorageLink.png)

### Observing Changes and Behavior

#### Observing Changes

- When the decorated data type is Bool, String, integer, or float, numerical changes can be observed.
- When the decorated data type is a class, object assignment and property changes can be observed (see [Using AppStorage and LocalStorage from UI](#using-appstorage-and-localstorage-from-ui)).
- When the decorated object is an Array, changes such as adding, deleting, or updating array elements can be observed.
- When the decorated object is a Datetime, overall assignment of Datetime can be observed. Additionally, Datetime properties can be updated by calling its methods: `addYears`, `addMonths`, `addWeeks`, `addMinutes`, `addSeconds`, and `addNanoseconds`. See [Decorating Datetime Type Variables](#decorating-datetime-type-variables).
- When the decorated variable is a Map, overall assignment of Map can be observed. Additionally, Map values can be updated by calling its methods: `add`, `clear`, and `remove`. See [Decorating Map Type Variables](#decorating-map-type-variables).
- When the decorated variable is a Set, overall assignment of Set can be observed. Additionally, Set values can be updated by calling its methods: `add`, `clear`, and `remove`. See [Decorating Set Type Variables](#decorating-set-type-variables).

#### Framework Behavior

1. When a change in the value decorated with @StorageLink(key) is observed, the modification is synchronized back to the corresponding property in AppStorage.
2. Once the data corresponding to the key in AppStorage changes, all data bound to this key (including two-way @StorageLink and one-way @StorageProp) will be synchronized.
3. If the data decorated with @StorageLink(key) is a state variable, its changes will not only be synchronized back to AppStorage but will also trigger re-rendering of the associated custom component.

## Limitations

1. The parameters of @StorageProp/@StorageLink must be of string type; otherwise, a compilation error will occur.

    ```cangjie
    let storage = AppStorage.setOrCreate("PropA", 47)
    let temp = AppStorage.get<Int64>("PropA").getOrThrow() // 47

    // Incorrect usage, compilation error
    @StorageProp[] let storageProp: Int64 = 1
    @StorageLink[] var storageLink: Int64 = 2

    // Correct usage
    @StorageProp["PropA"] let storageProp: Int64 = 1
    @StorageLink["PropA"] var storageLink: Int64 = 2
    ```

2. @StorageProp and @StorageLink do not support decorating Func-type variables. The framework will throw a runtime error.

3. When using AppStorage with [PersistentStorage](./cj-persiststorage.md) and [Environment](./cj-environment.md), note the following:

    a. After creating a property in AppStorage, calling `PersistentStorage.persistProp()` will use the existing value in AppStorage and overwrite the same-named property in PersistentStorage. Therefore, it is recommended to use the opposite calling order. For an example of incorrect usage, see [Accessing AppStorage Properties Before PersistentStorage](./cj-persiststorage.md#accessing-appstorage-properties-before-persistentstorage).

    b. If a property already exists in AppStorage, calling `Environment.envProp()` to create a same-named property will fail. Since AppStorage already has the property, the environment variable will not be written to AppStorage. Therefore, avoid using environment variable names for AppStorage properties.

4. Changes to variables decorated with state macros trigger UI re-rendering. If the variable is not intended for UI updates but for message passing, using an emitter is recommended. See [Avoid Using @StorageLink's Two-Way Sync for Event Notification](#avoid-using-storagelinks-two-way-sync-for-event-notification).

5. AppStorage is shared within the same process.

## Usage Scenarios

### Using AppStorage and LocalStorage from Application Logic

AppStorage is a singleton, and all its APIs are static, similar to the non-static methods in LocalStorage.

```cangjie
let temp1 = AppStorage.setOrCreate<Int64>("PropA", 47)

let storage =  LocalStorage()
let temp2 = storage.setOrCreate("PropA", 17)
let propA = AppStorage.get<Int64>("PropA")                  // propA in AppStorage == 47, propA in LocalStorage == 17
let link1 = AppStorage.link<Int64>("PropA").getOrThrow()    // link1.get() == 47
let link2 = AppStorage.link<Int64>("PropA").getOrThrow()    // link2.get() == 47

let value1 = link1.set(48) // Two-way sync: link1.get() == link2.get() == prop.get() == 48
let value2 = link1.set(49) // Two-way sync: link1.get() == link2.get() == prop.get() == 49

let value3 = storage.get<Int64>("PropA") // == 17
let value4 = storage.set<Int64>("PropA", 101)
let value5 = storage.get<Int64>("PropA") // == 101

let value6 = AppStorage.get<Int64>("PropA") // == 49
let value7 = link1.get() // == 49
let value8 = link2.get() // == 49
```

### Using AppStorage and LocalStorage from UI

The @StorageLink macro works with AppStorage, similar to how @LocalStorageLink works with LocalStorage. This macro creates two-way data synchronization with properties in AppStorage.

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

class Data{
    var code : Int64
    init(code: Int64){
        this.code = code
    }
}
let temp1 = AppStorage.setOrCreate("PropA", 47)
let temp2 = AppStorage.setOrCreate("PropB", Data(50))

let storage =  LocalStorage()
let res1 = storage.setOrCreate("LinkA", 47)
let res2 = storage.setOrCreate("LinkB", Data(50))

@Entry[storage]
@Component
class EntryView{
    @StorageLink["PropA"] var storageLink : Int64 = 1
    @LocalStorageLink["LinkA"] var localStorageLink : Int64 = 1
    @StorageLink["PropB"] var storageLinkObject : Data = Data(1)
    @LocalStorageLink["LinkB"] var localStorageLinkObject : Data = Data(1)

    func build() {
        Column(){
            Text("From AppStorage ${this.storageLink}")
                .onClick({evt => this.storageLink += 1;})
            Text("From LocalStorage ${this.localStorageLink}")
                .onClick({evt => this.localStorageLink += 1;})
            Text("From AppStorage ${this.storageLinkObject.code}")
                .onClick({evt =>
                    var temp = this.storageLinkObject
                    temp.code += 1
                    this.storageLinkObject = temp;
                    })
            Text("From LocalStorage ${this.localStorageLinkObject.code}")
                .onClick({evt =>
                    var temp = this.localStorageLinkObject
                    temp.code += 1
                    this.localStorageLinkObject = temp;
                    })
        }
    }
}
```

### Avoid Using @StorageLink's Two-Way Sync for Event Notification

It is not recommended to use @StorageLink and AppStorage's two-way synchronization mechanism for event notification because AppStorage variables may be bound to components across multiple pages, but event notifications may not need to reach all these components. Additionally, when these @StorageLink-decorated variables are used in the UI, they trigger UI refreshes, causing unnecessary performance overhead.

In the example code, the click event in `TapImage` modifies the `tapIndex` property in AppStorage. Due to the two-way synchronization of @StorageLink, the change is synchronized back to AppStorage, so all custom components bound to `tapIndex` in AppStorage will detect the change. Using `@Watch` to monitor `tapIndex` changes, the state variable `tapColor` is modified to trigger a UI refresh (note that `tapIndex` is not directly bound to the UI, so its changes do not directly trigger UI refreshes).

To use this mechanism for event notification, ensure that AppStorage variables are not directly bound to the UI and control the complexity of the `@Watch` function (a lengthy `@Watch` function can impact UI refresh efficiency).

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.resource_manager.AppResource
import kit.BasicServicesKit.agent.State
import kit.PerformanceAnalysisKit.Hilog
import ohos.resource.__GenerateResource__

class ViewData {
    var title: String
    var uri  : AppResource
    var color : Color = Color.Black

    init(title: String,uri  : AppResource){
        this.title = title
        this.uri   = uri
    }
}

@Entry
@Component
class EntryView{
    // "app.media.startIcon" is for illustration only. Replace it with your own resource, or imageSource creation will fail.
    let dataList : Array<ViewData> = [ViewData("flower",@r(app.media.startIcon)),ViewData("OMG",@r(app.media.image))]
    var gridScroller: Scroller = Scroller()

    func build() {
        Column(){
            Grid(scroller: this.gridScroller){
                ForEach(this.dataList, itemGeneratorFunc: {item : ViewData , idx : Int64 =>
                        GridItem(){
                            TapImage(index: idx,uri: item.uri)
                        }
                            .aspectRatio(1.0)
                        })
            }
        }
    }
}

@Component
class TapImage {
    @StorageLink["PropA"] @Watch[onTapIndexChange] var tapIndex : Int64 = -1
    @State var tapColor : Color = Color.Black
    var index: Int64
    var uri: AppResource

    func onTapIndexChange(){
        if(this.tapIndex >= 0 && this.index == this.tapIndex){
            Hilog.info(0, "tapindex", "${this.tapIndex}, index: ${this.index},red")
            this.tapColor = Color.Red
        }else{
            Hilog.info(0, "tapindex", "${this.tapIndex}, index: ${this.index},black")
            this.tapColorIn the following example, the `memberSet` decorated with `@StorageLink` is of type `Set<Int64>`. Clicking the Button to change the value of `memberSet` will trigger a view refresh.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import std.collection.HashSet
import std.collection.Set

@Entry
@Component
class EntryView {
    @StorageLink["set"] var message: Set<Int64> = HashSet<Int64>([0, 1, 2, 3, 4])
    func build() {
        Row() {
            Column() {
                ForEach(
                    this.message.toArray(),
                    itemGeneratorFunc: {
                        item: Int64, _: Int64 => Text("${item}")
                            .fontSize(30)
                    }
                )
                Button("init set").onClick({evt =>
                        var temp = this.message
                        temp = HashSet<Int64>([0, 1, 2, 3, 4])
                        this.message = temp
                    })
                Button("add new one").onClick({evt =>
                        var temp = this.message
                        temp.add(5)
                        this.message = temp
                    })
                Button("clear").onClick({evt =>
                        var temp = this.message
                        temp.clear()
                        this.message = temp
                    })
                Button("remove the first one").onClick({evt =>
                        var temp = this.message
                        temp.remove(0)
                        this.message = temp
                    })
            }
                .width(100.percent)
        }
        .height(100.percent)
    }
}
```