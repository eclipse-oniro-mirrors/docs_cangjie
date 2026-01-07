# State Management at Component Level Variables

Provides `ObservedArray` and `ObservedArrayList` as array types for state management. When changes occur in these arrays, such as modifying an item's value, deleting or adding an item, UI updates will be triggered.

## Import Module

```cangjie
import kit.ArkUI.*
```

## ObservedProperty

A property type used for state management.

## ObservedArrayList

An array list type used for state management.

### class ObservedArrayList\<T>

```cangjie
public class ObservedArrayList<T> <: CollectionEx<T> {
    public init(initValue: ArrayList<T>)
    public init(initValue: Array<T>)
}
```

**Function:** Represents an array list type used for state management.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parent Type:**

- [CollectionEx](./cj-common-types.md#interface-collectionext)\<T>

#### prop size

```cangjie
public prop size: Int64
```

**Function:** Gets the size of the state-managed array list.

**Type:** Int64

**Read-Write Capability:** Read-only

**Initial Version:** 22

#### init(ArrayList\<T>)

```cangjie
public init(initValue: ArrayList<T>)
```

**Function:** Defines an `ObservedArrayList` type array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| initValue | ArrayList\<T> | Yes | - | Initialization value for the state-managed array list type. |

#### init(Array\<T>)

```cangjie
public init(initValue: Array<T>)
```

**Function:** Defines an `ObservedArrayList` type array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| initValue | Array\<T> | Yes | - | Initialization value for the state-managed array list type. |

#### operator func [](Int64)

```cangjie
public operator func [](index: Int64): T
```

**Function:** Gets an element in the array list by index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Element index. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | Element at the specified index position. |

#### operator func [](Int64, T)

```cangjie
public operator func [](index: Int64, value!: T): Unit
```

**Function:** Sets an element in the array list by index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | Element index. |
| value | T | Yes | - | **Named parameter.** The element value to set. |

#### func isEmpty()

```cangjie
public func isEmpty(): Bool
```

**Function:** Checks whether the state-managed array list is empty.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the state-managed array list is empty. |

#### func clone()

```cangjie
public func clone(): ObservedArrayList<T>
```

**Function:** Clones the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ObservedArrayList](#class-observedarraylist)\<T> | Cloned state-managed array list. |

#### func clear()

```cangjie
public func clear(): Unit
```

**Function:** Clears the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

#### func append(T)

```cangjie
public func append(element: T): Unit
```

**Function:** Appends an element to the end of the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| element | T | Yes | - | The element to append. |

#### func appendAll(Collection\<T>)

```cangjie
public func appendAll(elements: Collection<T>): Unit
```

**Function:** Appends multiple elements to the end of the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| elements | Collection\<T> | Yes | - | The collection of elements to append. |

#### func insert(Int64, T)

```cangjie
public func insert(index: Int64, element: T): Unit
```

**Function:** Inserts an element at the specified position in the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The insertion position index. |
| element | T | Yes | - | The element to insert. |

#### func insertAll(Int64, Collection\<T>)

```cangjie
public func insertAll(index: Int64, elements: Collection<T>): Unit
```

**Function:** Inserts multiple elements at the specified position in the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The insertion position index. |
| elements | Collection\<T> | Yes | - | The collection of elements to insert. |

#### func prepend(T)

```cangjie
public func prepend(element: T): Unit
```

**Function:** Prepends an element to the beginning of the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| element | T | Yes | - | The element to prepend. |

#### func prependAll(Collection\<T>)

```cangjie
public func prependAll(elements: Collection<T>): Unit
```

**Function:** Prepends multiple elements to the beginning of the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| elements | Collection\<T> | Yes | - | The collection of elements to prepend. |

#### func remove(Int64)

```cangjie
public func remove(index: Int64): T
```

**Function:** Removes the element at the specified position in the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int64 | Yes | - | The index of the element to remove. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | The removed element. |

#### func remove(Range\<Int64>)

```cangjie
public func remove(range: Range<Int64>): Unit
```

**Function:** Removes elements within the specified range in the state-managed array list.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| range | Range\<Int64> | Yes | - | The range of elements to remove. |

#### func removeIf((T) -> Bool)

```cangjie
public func removeIf(predicate: (T) -> Bool): Unit
```

**Function:** Removes elements from the state-managed array list based on a condition.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| predicate | (T) -> Bool | Yes | - | The removal condition. |

## Example Code

Notes on state updates: Concurrent modifications to state variables in `spawn` expressions are not allowed, as they may lead to concurrency safety issues. When modifying state variables, it is recommended to use the `launch` method provided by the `concurrency` package to execute state updates on the main thread, ensuring concurrency safety. The following example demonstrates how to update variable states in a `spawn` expression:

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
            Button(text).onClick({ evt =>
                changeText({ p: String =>
                    // Use the launch expression to update state variables on the main thread
                    launch {
                        text = p
                    }
                })
            })
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
``````
    }
}
```

![Component State Management](figures/componentstatemanagement.gif)