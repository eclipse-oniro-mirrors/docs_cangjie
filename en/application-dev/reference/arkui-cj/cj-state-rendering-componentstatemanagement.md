# ohos.arkui.state_management

Provides `ObservedArray` and `ObservedArrayList` as array types for state management. When changes occur in these arrays, such as modifying an item's value, deleting or adding an item, it triggers UI updates.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ObservedArrayList

```cangjie
public class ObservedArrayList<T> <: ObservedComplexAbstract {

    public init(initValue: ArrayList<T>)

    public init(initValue: Array<T>)
}
```

**Functionality:** Provides dynamically-sized array functionality with state management support, capable of detecting internal changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Types:**

- [ObservedComplexAbstract](./cj-state-rendering-appstatemanagement.md#class-observedcomplexabstract)
- CollectionEx\<T>

### prop size

```cangjie
public prop size: Int64
```

**Functionality:** The number of elements in this `ObservedArrayList`.

**Type:** Int64

**Read-Write Permission:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### init(ArrayList\<T>)

```cangjie
public init(initValue: ArrayList<T>)
```

**Functionality:** Constructs an `ObservedArrayList` containing all elements from the specified `ArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| initValue | ArrayList\<T> | Yes | - | The `ArrayList` used to initialize the `ObservedArrayList`. |

### init(Array\<T>)

```cangjie
public init(initValue: Array<T>)
```

**Functionality:** Constructs an `ObservedArrayList` containing all elements from the specified `Array`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| initValue | Array\<T> | Yes | - | The `Array` used to initialize the `ObservedArrayList`. |

### func append(T)

```cangjie
public func append(element: T): Unit
```

**Functionality:** Appends the specified element to the end of this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| element | T | Yes | - | The element to be appended. |

### func appendAll(Collection\<T>)

```cangjie
public func appendAll(elements: Collection<T>): Unit
```

**Functionality:** Appends all elements from the specified collection to the end of this `ObservedArrayList`. The function traverses the input collection in iterator order and inserts all elements to the tail of this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| elements | Collection\<T> | Yes | - | The collection of elements to be appended. |

### func clear()

```cangjie
public func clear(): Unit
```

**Functionality:** Removes all elements from this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### func clone()

```cangjie
public func clone(): ObservedArrayList<T>
```

**Functionality:** Returns a shallow copy of this `ObservedArrayList` instance.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [ObservedArrayList](#class-observedarraylist)\<T> | A shallow copy of this `ObservedArrayList` instance. |

### func get()

```cangjie
public func get(): ArrayList<T>
```

**Functionality:** Returns an `ArrayList` containing all elements of this `ObservedArrayList` in proper sequence.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| ArrayList\<T> | The returned `ArrayList`. |

### func insert(Int64, T)

```cangjie
public func insert(index: Int64, element: T): Unit
```

**Functionality:** Inserts the specified element at the specified position in this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The target index for insertion. |
| element | T | Yes | - | The element of type T to be inserted. |

### func insertAll(Int64, Collection\<T>)

```cangjie
public func insertAll(index: Int64, elements: Collection<T>): Unit
```

**Functionality:** Inserts all elements from the specified collection into this `ObservedArrayList` starting from the specified position. The function traverses the input collection in iterator order and inserts all elements at the specified position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The target index for insertion. |
| elements | Collection\<T> | Yes | - | The collection of elements of type T to be inserted. |

### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**Functionality:** Determines whether this `ObservedArrayList` is empty.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the `ObservedArrayList` is empty; otherwise, returns `false`. |

### func prepend(T)

```cangjie
public func prepend(element: T): Unit
```

**Functionality:** Prepends the specified element to the beginning of this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| element | T | Yes | - | The element to be prepended. |

### func prependAll(Collection\<T>)

```cangjie
public func prependAll(elements: Collection<T>): Unit
```

**Functionality:** Prepends all elements from the specified collection to the beginning of this `ObservedArrayList`. The function traverses the input collection in iterator order and inserts all elements at the start position.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| elements | Collection\<T> | Yes | - | The collection of elements to be prepended. |

### func remove(Int64)

```cangjie
public func remove(index: Int64): T
```

**Functionality:** Removes the element at the specified position in this `ObservedArrayList`. Returns the removed element.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The index of the element to be removed. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | The removed element. |

### func remove(Range\<Int64>)

```cangjie
public func remove(range: Range<Int64>): Unit
```

**Functionality:** Removes all elements within the specified range from this `ObservedArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| range | Range\<Int64> | Yes | - | The range of elements to be removed. |

### func removeIf((T) -> Bool)

```cangjie
public func removeIf(predicate: (T) -> Bool): Unit
```

**Functionality:** Removes all elements from this `ObservedArrayList` that satisfy the given lambda expression or function.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| predicate | (T)->Bool | Yes | - | The condition for removal. |

### func set(ArrayList\<T>)

```cangjie
public func set(newValue: ArrayList<T>): Unit
```

**Functionality:** Resets the value of this `ObservedArrayList` using an `ArrayList`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| newValue | ArrayList\<T> | Yes | - | The `ArrayList` used to set the value of the `ObservedArrayList`. |

### func set(Array\<T>)

```cangjie
public func set(newValue: Array<T>): Unit
```

**Functionality:** Resets the value of this `ObservedArrayList` using an `Array`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| newValue | Array\<T> | Yes | - | The `Array` used to set the value of the `ObservedArrayList`. |

### func set(ObservedComplexAbstract)

```cangjie
public func set(newValue: ObservedComplexAbstract): Unit
```

**Functionality:** Resets the value of this `ObservedArrayList` using an `ObservedComplexAbstract`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| newValue | ObservedComplexAbstract | Yes | - | The `ObservedComplexAbstract` data used to set the value of the `ObservedArrayList`. |

### func subscribeInner(Observer)

```cangjie
public func subscribeInner(observer: Observer): Unit
```

**Functionality:** Recursively binds observation to each item in the state-managed array.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| observer | Observer | Yes | - | The observer class to bind. |

### func unsubscribeInner(Observer)

```cangjie
public func unsubscribeInner(observer: Observer): Unit
```

**Functionality:** Recursively unbinds observation from each item in the state-managed array.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| observer | Observer | Yes | - | The observer class to unbind. |

### func \[](int64)

```cangjie
public operator func [](index: Int64): T
```

**Functionality:** Operator overload - get. Returns the value of the element at the specified index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The index for the get operation. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | The value of the element at the specified index. |

### func [](Int64, T)

```cangjie
public operator func [](index: Int64, value!: T): Unit
```

**Functionality:** Operator overload - set. Replaces the element at the specified position in this list with the specified element using the subscript operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The index to set. |
| value | T | Yes | - | **Named parameter.** The value of type T to set. |

### Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var arr: ObservedArrayList<Int64> = ObservedArrayList<Int64>([1, 2])

    func build() {
        Column {
            Text("arr[0] is ${arr[0]}")
            Button("click").onClick { evt =>
                arr[0] = 0
            }
        }
    }
}
```

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var arr: ObservedArrayList<Int64> = ObservedArrayList<Int64>([1, 2])

    func build() {
        Column {
            Text("arr[0] is ${arr[0]}")
            Button("click").onClick { evt =>
                arr[0] = 0
            }
            Button("append").onClick { evt =>
                arr.append(0)
            }
        }
    }
}
```## class ObservedProperty

```cangjie
public open class ObservedProperty<T> <: ObservedPropertyAbstract {
    public init(info: String, initValue: T)
}
```

**Function:** Observable property class for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- [ObservedPropertyAbstract](./cj-ui-framework.md#class-observedpropertyabstract)

### init(String, T)

```cangjie
public init(info: String, initValue: T)
```

**Function:** Constructor for the ObservedProperty class.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| info | String | Yes | - | Initialization information for construction. |
| initValue | T | Yes | - | Initial value for construction. |

### func createProp(String)

```cangjie
public func createProp(info: String): ObservedProperty<T>
```

**Function:** Creates and returns a one-way binding copy of the current property. The newly created property remains synchronized with the original property, but modifications to the new property will not affect the original one.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| info | String | Yes | - | Description information for the newly created property. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ObservedProperty](#class-observedproperty)\<T> | A one-way binding copy of the current property. |

### func get()

```cangjie
public func get(): T
```

**Function:** Reads the data of the synchronized property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| T | Data of the synchronized property. |

### func getInner()

```cangjie
public func getInner(): T
```

**Function:** Gets the internal value of the property without triggering state updates.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| T | Internal value of the property. |

### func set(T)

```cangjie
public open func set(newValue: T): Unit
```

**Function:** Sets the data of the synchronized property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| newValue | T | Yes | - | Data to be set. |

### func subscribeEx(Observer)

```cangjie
public func subscribeEx(observer: Observer)
```

**Function:** Adds an observer for property changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| observer | Observer | Yes | - | Observer for property changes. |

### func unsubscribeEx(Observer)

```cangjie
public func unsubscribeEx(observer: Observer)
```

**Function:** Removes an observer for property changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| observer | Observer | Yes | - | Observer to be removed. |

## Example Code

**Note on State Updates:** Concurrent modification of state variables within `spawn` expressions is not allowed, as it may lead to concurrency safety issues. When modifying state variables, it is recommended to use the `launch` method provided by the `concurrency` package to ensure state updates are executed on the main thread for concurrency safety. The following example demonstrates how to update state variables within a `spawn` expression:

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    @State var text: String = "begin"

    func build() {
        Column(space: 30) {
            Button(text).onClick { evt =>
                changeText({ p: String =>
                    // Use the launch expression to update state variables on the main thread
                    launch {
                        text = p
                    }
                })
            }
        }.width(100.percent)
    }

    private func changeText(callback: (String) -> Unit): Unit {
        spawn {
            while (true) {
                callback("blink 0")
                sleep(Duration.millisecond * 100)
                callback("blink 1")
                sleep(Duration.millisecond * 100)
            }
        }
    }
}
```