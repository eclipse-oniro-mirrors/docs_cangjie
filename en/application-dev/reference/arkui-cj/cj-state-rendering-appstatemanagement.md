# Application-Level Variable State Management

The state management module provides capabilities for application data storage, persistent data management, UIAbility data storage, and the environmental state required by applications.

## Importing the Module

```cangjie
import kit.ArkUI.*
```

## class AppStorage

```cangjie
public class AppStorage {}
```

**Functionality:** AppStorage is a global UI state storage for applications, bound to the application process. It is created by the UI framework when the application starts, serving as a centralized storage for application UI state properties. Establishes a one-way property binding with the corresponding propName in AppStorage. If the given propName exists in AppStorage, returns the one-way bound data corresponding to that propName. If the propName does not exist in AppStorage, returns None. Modifications to the one-way bound data will not be synchronized back to AppStorage.

Unlike page-level UI state storage LocalStorage, AppStorage is a global UI state storage at the application level, acting as the "central hub" for the entire application. Persistent data (PersistentStorage) and environment variables (Environment) must go through AppStorage to interact with the UI.

> **Note:**
>
> AppStorage only supports pure Cangjie scenarios and is not suitable for mixed ArkTS and Cangjie development scenarios.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### static func clear()

```cangjie
public static func clear(): Bool
```

**Functionality:** Deletes all properties in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if all properties in AppStorage have no subscribers and are successfully deleted. Otherwise, returns false. |

### static func delete(String)

```cangjie
public static func delete(propName: String): Bool
```

**Functionality:** Deletes the property corresponding to propName in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in AppStorage and has no subscribers, and is successfully deleted. Otherwise, returns false. |

### static func get\<T>(String)

```cangjie
public static func get<T>(propName: String): ?T
```

**Functionality:** Retrieves the property value corresponding to propName in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?T | Returns the value of the corresponding property in AppStorage. Returns None if the property does not exist. |

### static func has(String)

```cangjie
public static func has(propName: String): Bool
```

**Functionality:** Checks whether the property corresponding to propName exists in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in AppStorage. Otherwise, returns false. |

### static func keys()

```cangjie
public static func keys(): EquatableCollection<String>
```

**Functionality:** Retrieves all property keys in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| EquatableCollection\<String> | Returns a collection of all property keys in AppStorage. |

### static func link\<T>(String)

```cangjie
public static func link<T>(propName: String): ?ObservedProperty<T>
```

**Functionality:** Establishes a two-way property binding with the corresponding propName in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the two-way bound data. Returns None if the property does not exist in AppStorage. |

### static func property\<T>(String)

```cangjie
public static func property<T>(propName: String): ?ObservedProperty<T>
```

**Functionality:** Establishes a one-way property binding with the corresponding propName in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the one-way bound data. Returns None if the property does not exist in AppStorage. |

### static func set\<T>(String, T)

```cangjie
public static func set<T>(propName: String, newValue: T): Bool
```

**Functionality:** Sets the property value corresponding to propName in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |
| newValue | T | Yes | - | The new value to set. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in AppStorage and is successfully set. Otherwise, returns false. |

### static func setAndLink\<T>(String, T)

```cangjie
public static func setAndLink<T>(propName: String, defaultValue: T): ObservedProperty<T>
```

**Functionality:** Establishes a two-way property binding with the corresponding propName in AppStorage. If the property does not exist, it is created and initialized.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |
| defaultValue | T | Yes | - | The default value of the property. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the two-way bound data. |

### static func setAndProp\<T>(String, T)

```cangjie
public static func setAndProp<T>(propName: String, defaultValue: T): ObservedProperty<T>
```

**Functionality:** Establishes a one-way property binding with the corresponding propName in AppStorage. If the property does not exist, it is created and initialized.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |
| defaultValue | T | Yes | - | The default value of the property. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the one-way bound data. |

### static func setOrCreate\<T>(String, T)

```cangjie
public static func setOrCreate<T>(propName: String, newValue: T): Unit
```

**Functionality:** Sets the property value corresponding to propName in AppStorage. If the property does not exist, it is created and initialized.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in AppStorage. |
| newValue | T | Yes | - | The new value to set. |

### static func size()

```cangjie
public static func size(): Int64
```

**Functionality:** Retrieves the number of properties in AppStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the number of properties in AppStorage. |

## class Environment

```cangjie
public class Environment {}
```

**Functionality:** Environment is bound to the application process and is created by the UI framework when the application starts, providing a centralized storage for device environment states.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### static func envProp\<T>(String, T)

```cangjie
public static func envProp<T>(key: String, defaultValue: T): Bool
```

**Functionality:** Creates a property synchronized with the device environment state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The key name of the environment property. |
| defaultValue | T | Yes | - | The default value of the property. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property is successfully created. Otherwise, returns false. |

### static func keys()

```cangjie
public static func keys(): Array<String>
```

**Functionality:** Retrieves all environment property keys.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns an array of all environment property keys. |

## class LocalStorage

```cangjie
public class LocalStorage {
    public init()
}
```

**Functionality:** LocalStorage is a page-level UI state storage that interacts with AppStorage through decorators.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### init()

```cangjie
public init()
```

**Functionality:** Constructor for LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

### func aboutToBeDeleted()

```cangjie
public func aboutToBeDeleted(): Bool
```

**Functionality:** Clears all properties in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if all properties in LocalStorage have no subscribers and are successfully deleted. Otherwise, returns false. |

### func clear()

```cangjie
public func clear(): Bool
```

**Functionality:** Deletes all properties in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if all properties in LocalStorage have no subscribers and are successfully deleted. Otherwise, returns false. |

### func delete(String)

```cangjie
public func delete(propName: String): Bool
```

**Functionality:** Deletes the property corresponding to propName in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in LocalStorage and has no subscribers, and is successfully deleted. Otherwise, returns false. |

### func get\<T>(String)

```cangjie
public func get<T>(propName: String): ?T
```

**Functionality:** Retrieves the property value corresponding to propName in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?T | Returns the value of the corresponding property in LocalStorage. Returns None if the property does not exist. |

### func has(String)

```cangjie
public func has(propName: String): Bool
```

**Functionality:** Checks whether the property corresponding to propName exists in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in LocalStorage. Otherwise, returns false. |

### func keys()

```cangjie
public func keys(): EquatableCollection<String>
```

**Functionality:** Retrieves all property keys in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| EquatableCollection\<String> | Returns a collection of all property keys in LocalStorage. |

### func link\<T>(String)

```cangjie
public func link<T>(propName: String): ?ObservedProperty<T>
```

**Functionality:** Establishes a two-way property binding with the corresponding propName in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the two-way bound data. Returns None if the property does not exist in LocalStorage. |

### func property\<T>(String)

```cangjie
public func property<T>(propName: String): ?ObservedProperty<T>
```

**Functionality:** Establishes a one-way property binding with the corresponding propName in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |

**Return Value:**

| Type | Description |
|:----|:----|
| ?[ObservedProperty](./cj-state-rendering-componentstatemanagement.md#class-observedproperty)\<T> | Returns the one-way bound data. Returns None if the property does not exist in LocalStorage. |

### func set\<T>(String, T)

```cangjie
public func set<T>(propName: String, newValue: T): Bool
```

**Functionality:** Sets the property value corresponding to propName in LocalStorage.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |
| newValue | T | Yes | - | The new value to set. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the property exists in LocalStorage and is successfully set. Otherwise, returns false. |

### func setAndLink\<T>(String, T)

```cangjie
public func setAndLink<T>(propName: String, defaultValue: T): ObservedProperty<T>
```

**Functionality:** Establishes a two-way property binding with the corresponding propName in LocalStorage. If the property does not exist, it is created and initialized.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| propName | String | Yes | - | The property name in LocalStorage. |
| defaultValue | T | Yes | - | The default value of the property. |

**Return Value:**

| Type | Description |
|:## class PersistentStorage

```cangjie
public class PersistentStorage {}
```

**Function:** PersistentStorage is used for persistently storing UI states, typically working in conjunction with AppStorage to persist selected AppStorage properties to files.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### static func deleteProp(String)

```cangjie
public static func deleteProp(key: String): Unit
```

**Function:** Deletes a persisted property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The key name of the property to be deleted. |

### static func keys()

```cangjie
public static func keys(): Array<String>
```

**Function:** Gets the key names of all persisted properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns an array of key names for all persisted properties. |

### static func persistProp\<T>(String, T)

```cangjie
public static func persistProp<T>(key: String, defaultValue: T): Unit
```

**Function:** Persists the specified AppStorage property.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The key name of the property to be persisted. |
| defaultValue | T | Yes | - | The default value of the property. |

### static func persistProps\<T>(Array<(String, T)>)

```cangjie
public static func persistProps<T>(props: Array<(String, T)>): Unit
```

**Function:** Persists multiple AppStorage properties.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| props | Array\<(String, T)> | Yes | - | An array of key-value pairs for properties to be persisted. |

## enum ColorMode

```cangjie
public enum ColorMode <: Equatable<ColorMode> {
    | Light
    | Dark
    | ...
}
```

**Function:** Defines the color mode of the device.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[ColorMode](#enum-colormode)>

### Light

```cangjie
Light
```

**Function:** Light mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Dark

```cangjie
Dark
```

**Function:** Dark mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(ColorMode)

```cangjie
public operator func !=(other: ColorMode): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ColorMode](#enum-colormode) | Yes | - | Another ColorMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if not equal. |

### operator func ==(ColorMode)

```cangjie
public operator func ==(other: ColorMode): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ColorMode](#enum-colormode) | Yes | - | Another ColorMode instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if equal. |

## enum LayoutDirection

```cangjie
public enum LayoutDirection <: Equatable<LayoutDirection> {
    | Ltr
    | Rtl
    | Auto
    | ...
}
```

**Function:** Defines the layout direction of the device.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parent Type:**

- Equatable\<[LayoutDirection](#enum-layoutdirection)>

### Ltr

```cangjie
Ltr
```

**Function:** Left-to-right layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Rtl

```cangjie
Rtl
```

**Function:** Right-to-left layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### Auto

```cangjie
Auto
```

**Function:** Auto layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### operator func !=(LayoutDirection)

```cangjie
public operator func !=(other: LayoutDirection): Bool
```

**Function:** Inequality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LayoutDirection](#enum-layoutdirection) | Yes | - | Another LayoutDirection instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if not equal. |

### operator func ==(LayoutDirection)

```cangjie
public operator func ==(other: LayoutDirection): Bool
```

**Function:** Equality comparison operator.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [LayoutDirection](#enum-layoutdirection) | Yes | - | Another LayoutDirection instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Comparison result, returns true if equal. |