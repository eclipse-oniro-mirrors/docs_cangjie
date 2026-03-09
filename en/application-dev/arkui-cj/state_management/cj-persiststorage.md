# PersistentStorage: Persisting UI State

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The first two sections introduced LocalStorage and AppStorage, which are runtime memory solutions. However, a common requirement in application development is to preserve selected results even after the application exits and restarts. This is where PersistentStorage comes into play.

PersistentStorage is an optional singleton object in an application. Its purpose is to persistently store selected AppStorage properties, ensuring these properties retain their values from when the application was last closed upon subsequent restarts.

While PersistentStorage provides the capability to persist state variables, it's important to note that both persistence and UI read-back functionalities depend on AppStorage. Before reading this documentation, we recommend reviewing: [AppStorage](./cj-appstorage.md) and [PersistentStorage API Documentation](../../reference/arkui-cj/cj-state-rendering-appstatemanagement.md#class-persistentstorage).

## Overview

PersistentStorage retains selected AppStorage properties on the device's disk. Applications use APIs to determine which AppStorage properties should be persisted via PersistentStorage. The UI and business logic do not directly access properties in PersistentStorage—all property access is performed through AppStorage, where changes are automatically synchronized to PersistentStorage.

A two-way synchronization is established between PersistentStorage and AppStorage properties. Application development typically accesses PersistentStorage through AppStorage. Additionally, there are interfaces available for managing persisted properties, but business logic always retrieves and sets properties through AppStorage.

## Constraints

PersistentStorage supports the following types and values:

- Simple types: Bool, String, integer, floating-point, etc.
- Objects that can be reconstructed using JSON.stringify() and JSON.parse(), though member methods within objects are not persisted.

PersistentStorage does NOT support:

- Nested objects (object arrays, object properties containing objects, etc.). The framework currently cannot detect changes in nested objects (including arrays) within AppStorage, preventing write-back to PersistentStorage.

Persistence operations are relatively slow, so applications should avoid:

- Persisting large datasets
- Persisting frequently changing variables

PersistentStorage works best with data smaller than 2KB. Avoid persisting large amounts of data because disk write operations are synchronous, and bulk local read-write operations execute on the UI thread, potentially impacting rendering performance. For large-scale data storage needs, we recommend using database APIs.

## Usage Scenarios

### Accessing PersistentStorage-Initialized Properties from AppStorage

1. Initialize PersistentStorage:

```cangjie
PersistentStorage.persistProp("aProp",47)
```

2. Retrieve the corresponding property from AppStorage:

```cangjie
AppStorage.get<Int64>("aProp")
```

&nbsp;&nbsp;Or define within a component:

```cangjie
@StorageLink["aProp"] var aProp : Int64 = 48
```

Complete code example:

 <!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    let temp = PersistentStorage.persistProp("aProp",47)
    @State var message : String = "Hello World"
    @StorageLink["aProp"] var aProp : Int64 = 48
    func build() {
        Row(){
            Column(){
                Text("${this.aProp}")
                    .onClick{
                        etv=> this.aProp += 1
                    }
            }
        }
    }
}
```

- First launch after fresh installation:
  a. persistProp initializes PersistentStorage by first checking if "aProp" exists in the local PersistentStorage file—it doesn't exist for first-time installations.
  b. Next checks if "aProp" exists in AppStorage—still absent.
  c. Creates a number-type property named "aProp" in AppStorage with the default value 47.
  d. PersistentStorage writes property "aProp" with value 47 to disk. Subsequent changes to "aProp" in AppStorage will be persisted.
  e. The @StorageLink("aProp") aProp state variable in the EntryView component establishes two-way binding with "aProp" in AppStorage. During creation, it successfully finds "aProp" in AppStorage and uses its value 47.

**Figure 1** PersistProp Initialization Rules

![PersistProp](figures/PersistProp.png)

- After click event:
  a. The @StorageLink("aProp") aProp state variable changes, triggering Text component refresh.
  b. @StorageLink variables maintain two-way sync with AppStorage, so changes propagate back to AppStorage.
  c. Changes to "aProp" in AppStorage synchronize to all bound variables (none in this example).
  d. Since "aProp" is persisted, AppStorage changes trigger PersistentStorage to write updates to disk.

- Subsequent application launches:
  a. PersistentStorage.persistProp("aProp", 47) first queries the "aProp" property in PersistentStorage local files—successful.
  b. Writes the queried value to AppStorage.
  c. In the EntryView component, the value of the @StorageLink decorated aProp property is the value written by PersistentStorage to AppStorage, that is, the value stored when the application was closed last time.

### Accessing AppStorage Properties Before PersistentStorage

This example demonstrates an anti-pattern. Accessing AppStorage properties via interface calls before invoking PersistentStorage.persistProp or persistProps is incorrect, as this sequence loses property values from the previous application run:

```cangjie
let aProp = AppStorage.setOrCreate("aProp", 47)
let temp = PersistentStorage.persistProp("aProp", 48)
```

During non-first runs:
- AppStorage.setOrCreate("aProp", 47) executes first: creates "aProp" in AppStorage as number type with default value 47. Being a persisted property, it writes back to PersistentStorage, overwriting previous values.
- PersistentStorage.persistProp("aProp", 48) then finds "aProp" with the newly written value 47.

### Accessing AppStorage Properties After PersistentStorage

Developers should first determine whether to overwrite values previously saved in PersistentStorage. If overwriting is needed, then call AppStorage interfaces for modification; otherwise, refrain from calling them.

```cangjie
let temp = PersistentStorage.persistProp("aProp", 48)
if(AppStorage.get<Int64>("aProp").getOrThrow() > 50){
    AppStorage.setOrCreate("aProp", 47)
}
```

This example reads PersistentStorage data first, then checks if "aProp" exceeds 50. If true, it uses AppStorage interfaces to set the value to 47.