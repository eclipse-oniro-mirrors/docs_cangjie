# ohos.data.preferences

User Preferences provide applications with Key-Value data processing capabilities, supporting lightweight persistent data storage, modification, and query operations.

Data is stored in key-value pairs where keys are of string type, and values can be numeric, string, boolean, or arrays of these three types.

## Import Module

```cangjie
import kit.ArkData.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.
- A valid [dataGroupId](#var-datagroupid) must be obtained from the application market.

For details about the sample project and configuration template, see [Cangjie Sample Code Guide](../cj-development-intro.md#Cangjie-Sample-Code-Guide).

## const MAX_KEY_LENGTH

```cangjie
public const MAX_KEY_LENGTH: UInt32 = 1024
```

**Description:** Maximum key length limit of 1024 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

## const MAX_VALUE_LENGTH

```cangjie
public const MAX_VALUE_LENGTH: UInt32 = 16 * 1024 * 1024
```

**Description:** Maximum value length limit of 16 * 1024 * 1024 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

## class Options

```cangjie
public class Options {
    public var name: String
    public var dataGroupId: String
    public var storageType: StorageType
    public init(name: String, dataGroupId!: String = String.empty,
        storageType!: StorageType = StorageType.Xml)
}
```

**Description:** Configuration options for Preferences instances.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### var dataGroupId

```cangjie
public var dataGroupId: String
```

**Description:** Application group ID, which must be obtained from the application market.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** Name of the Preferences instance.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### var storageType

```cangjie
public var storageType: StorageType
```

**Description:** Storage mode (optional parameter).

**Type:** [StorageType](#enum-storagetype)

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### init(String, String, StorageType)

```cangjie
public init(name: String, dataGroupId!: String = String.empty,
    storageType!: StorageType = StorageType.Xml)
```

**Description:** Constructor for creating Options instances. By default, creates a Preferences instance in the application sandbox directory.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| name | String | Yes | - | Name of the Preferences instance. |
| dataGroupId | String | No | String.empty | Application group ID (must be obtained from the application market). |
| storageType | [StorageType](#enum-storagetype) | No | StorageType.Xml | Storage mode (optional parameter). |

## class Preferences

```cangjie
public class Preferences {}
```

**Description:** Preferences class providing interfaces for accessing and modifying stored data.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### static func deletePreferences(UIAbilityContext, String)

```cangjie
public static func deletePreferences(context: UIAbilityContext, name: String): Unit
```

**Description:** Removes the specified Preferences instance from cache. If the instance has an associated persistent file, the file is also deleted.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Exceptions:**

- BusinessException: Error codes as follows:

| Error Code | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are missing; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Internal error. |
| 15500010 | Failed to delete the user preferences persistence file. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*

// Get Preferences instance
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore")  // Context required; see usage instructions
try {
    // Delete Preferences instance
    Preferences.deletePreferences(Global.abilityContext, "myStore")
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "delete Preferences failed")
}
```

### static func deletePreferences(UIAbilityContext, Options)

```cangjie
public static func deletePreferences(context: UIAbilityContext, options: Options): Unit
```

**Description:** Removes the specified Preferences instance from cache. If the instance has an associated persistent file, the file is also deleted.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [Options](#class-options) | Yes | - | Configuration options for the Preferences instance. |

**Exceptions:**

- BusinessException: Error codes as follows:

| Error Code | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are missing; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 801 | Capability not supported. |
| 15500010 | Failed to delete the user preferences persistence file. |
| 15501001 | The operation is supported in stage mode only. |
| 15501002 | Invalid dataGroupId. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*

// Get Preferences instance
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore")  // Context required; see usage instructions
try {
    // Delete Preferences instance
    Preferences.deletePreferences(Global.abilityContext, "myStore")
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "delete Preferences failed")
}
```

### static func getPreferences(UIAbilityContext, String)

```cangjie
public static func getPreferences(context: UIAbilityContext, name: String): Preferences
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-string) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-string) will retrieve the instance directly from cache instead of reading the persistence file. After calling this interface to remove the instance from cache, the next getPreferences call will re-read the persistence file and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Returns:**

| Type | Description |
| :---- | :---- |
| [Preferences](#class-preferences) | Preferences instance. |

**Exceptions:**

- BusinessException: Error codes as follows:

| Error Code | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are missing; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Internal error. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context required; see usage instructions
try {
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### static func getPreferences(UIAbilityContext, Options)

```cangjie
public static func getPreferences(context: UIAbilityContext, options: Options): Preferences
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-options) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-options) will retrieve the instance directly from cache instead of reading the persistence file. After calling this interface to remove the instance from cache, the next getPreferences call will re-read the persistence file and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [Options](#class-options) | Yes | - | Name of the Preferences instance. |

**Returns:**

| Type | Description |
| :---- | :---- |
| [Preferences](#class-preferences) | Preferences instance. |

**Exceptions:**

- BusinessException: Error codes as follows:

| Error Code | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are missing; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Internal error. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context required; see usage instructions
try {
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### static func removePreferencesFromCache(UIAbilityContext, String)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, name: String): Unit
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-string) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-string) will retrieve the instance directly from cache instead of reading the persistence file. After calling this interface to remove the instance from cache, the next getPreferences call will re-read the persistence file and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Exceptions:**

- BusinessException: Error codes as follows:

| Error Code | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are missing; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Internal error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context required; see usage instructions
try {
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```### static func removePreferencesFromCache(UIAbilityContext, Options)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, options: Options): Unit
```

**Function:** Removes the specified Preferences instance from the cache.

When an application first calls the [getPreferences](#static-func-getpreferencesuiabilitycontext-options) interface to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-options) will retrieve the instance directly from the cache without reading from the persistent file again. After calling this interface to remove the instance from the cache, the next getPreferences call will re-read the persistent file and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may lead to data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [Options](#class-options) | Yes | - | Name of the Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 801 | Capability not supported. |
| 15500000 | Inner error. |
| 15501001 | The operation is supported in stage mode only. |
| 15501002 | Invalid dataGroupId. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
try {
    // Remove the Preferences instance from the cache
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### func clear()

```cangjie
public func clear(): Unit
```

**Function:** Clears all data in the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
preferences.put("myKey", PreferencesValueType.StringData("myValue"))
preferences.clear()
```

### func delete(String)

```cangjie
public func delete(key: String): Unit
```

**Function:** Deletes the key-value pair with the given key from the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Name of the key to be deleted. Cannot be empty. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Inner error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*

// Obtain the Preferences instance
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore") // Context application context needs to be obtained; see usage instructions in this document.
preferences.delete("startup")
```

### func flush()

```cangjie
public func flush(): Unit
```

**Function:** Persists the data in the cached Preferences instance to the user preferences persistent file.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
preferences.put("myKey", PreferencesValueType.StringData("myValue"))
preferences.flush()
```

### func get(String, ValueType)

```cangjie
public func get(key: String, defValue: ValueType): ValueType
```

**Function:** Retrieves the value corresponding to the key from the cached Preferences instance. If the key does not exist, returns the default value defValue.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Name of the key to retrieve. |
| defValue | [ValueType](#enum-valuetype) | Yes | - | Default return value. Supports Int64, Float64, String, Bool, Array\<Bool>, Array\<Float64>, Array\<String>. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ValueType](#enum-valuetype) | Returns the value corresponding to the key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
var value = preferences.get("key", PreferencesValueType.Integer(0))
match (value) {
    case PreferencesValueType.Integer(n) => Hilog.info(0, "AppLogCj", "Retrieved value: ${n}")
    case _ => Hilog.info(0, "AppLogCj", "Retrieved value is not Int")
}
```

### func getAll()

```cangjie
public func getAll(): HashMap<String, ValueType>
```

**Function:** Retrieves all key-value data from the cached Preferences instance.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| HashMap\<String, [ValueType](#enum-valuetype)> | HashMap object containing all key-value data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
var values = preferences.getAll()
for ((k, v) in values) {
    match (v) {
        case Integer(n) => Hilog.info(0, "AppLogCj", "Key-value pair: key: ${k} value: ${n}")
        case Double(n) => Hilog.info(0, "AppLogCj", "Key-value pair: key: ${k} value: ${n}")
        case StringData(n) => Hilog.info(0, "AppLogCj", "Key-value pair: key: ${k} value: ${n}")
        case _ => Hilog.info(0, "AppLogCj", "Other value")
    }
}
```

### func has(String)

```cangjie
public func has(key: String): Bool
```

**Function:** Checks whether the cached Preferences instance contains a key-value pair with the given key.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Name of the key to check. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Boolean value. Returns whether the Preferences instance contains a key-value pair with the given key. true indicates existence; false indicates non-existence. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
let hasKey = preferences.has("startup")
if (hasKey) {
    Hilog.info(0, "AppLogCj", "The key 'startup' is contained.")
} else {
    Hilog.info(0, "AppLogCj", "The key 'startup' does not contain.")
}
```

### func off(PreferencesEvent, ?Callback1Argument\<String>)

```cangjie
public func off(event: PreferencesEvent, callback: ?Callback1Argument<String> = None): Unit
```

**Function:** Unsubscribes from data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [PreferencesEvent](#enum-preferencesevent) | Yes | - | Event type, indicating unsubscription from data changes or inter-process data changes. |
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String> | No | None | Callback function to be unsubscribed. If not specified, all callbacks are unsubscribed. <br> String: Type of the changed key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Inner error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.data.preferences.ValueType as PValueType

import kit.PerformanceAnalysisKit.Hilog

// This code can be added to the dependency definition
// Callback function
class Callback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
    }
}

var str = "container"
var a = Preferences.getPreferences(Global.abilityContext, str) // Context application context needs to be obtained; see usage instructions in this document.
var c = Callback()
a.on(PreferencesEvent.PreferencesChange, c)
a.off(PreferencesEvent.PreferencesChange)
a.put("kkk1", PValueType.StringData("vvv1"))
a.flush()
```

### func on(PreferencesEvent, Callback1Argument\<String>)

```cangjie
public func on(event: PreferencesEvent, callback: Callback1Argument<String>): Unit
```

**Function:** Subscribes to data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [PreferencesEvent](#enum-preferencesevent) | Yes | - | Event type. <br> PreferencesChange: Subscribes to data changes. When the value of the subscribed key changes, the callback is triggered after the flush method is executed. <br> PreferencesMultiProcessChange: Subscribes to inter-process data changes. When multiple processes hold the same preferences file, the callback is triggered after the flush method is executed when the value of the subscribed key changes in any process. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String> | Yes | - | Callback function. <br> String: Type of the changed key. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.data.preferences.ValueType as PValueType

import kit.PerformanceAnalysisKit.Hilog

// Callback function
class Callback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
    }
}

var str = "container"
var a = Preferences.getPreferences(Global.abilityContext, str) // Context application context needs to be obtained; see usage instructions in this document.
var c = Callback()
a.on(PreferencesEvent.PreferencesChange, c)
a.put("kkk1", PValueType.StringData("vvv1"))
a.flush()
```

### func put(String, ValueType)

```cangjie
public func put(key: String, value: ValueType): Unit
```

**Function:** Writes data to the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key to be modified. Cannot be empty. |
| value | [ValueType](#enum-valuetype) | Yes | - | New value to store. Supports Int64, Float64, String, Bool, Array\<Bool>, Array\<Float64>, Array\<String>. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

var preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained; see usage instructions in this document.
preferences.put("Monday", PreferencesValueType.StringData("The weather is nice today"))
```## enum PreferencesEvent

```cangjie
public enum PreferencesEvent {
    | PreferencesChange
    | PreferencesMultiProcessChange
}
```

**Description:** Enumeration of event types for Preferences.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### PreferencesChange

```cangjie
PreferencesChange
```

**Description:** Indicates data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### PreferencesMultiProcessChange

```cangjie
PreferencesMultiProcessChange
```

**Description:** Indicates data changes across multiple processes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

## enum StorageType

```cangjie
public enum StorageType {
    | Xml
    | Gskv
}
```

**Description:** Enumeration of storage modes for Preferences.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### Gskv

```cangjie
Gskv
```

**Description:** Indicates GSKV storage mode.

**Features:** Data is stored in GSKV database mode. Operations on data are immediately persisted to disk without requiring the flush interface.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### Xml

```cangjie
Xml
```

**Description:** Indicates XML storage mode, which is the default storage mode for Preferences.

**Features:** Data is stored in XML format. Operations on data occur in memory, requiring the flush interface for disk persistence.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

## enum ValueType

```cangjie
public enum ValueType {
    | Integer(Int64)
    | Double(Float64)
    | StringData(String)
    | BoolData(Bool)
    | BoolArray(Array<Bool>)
    | DoubleArray(Array<Float64>)
    | StringArray(Array<String>)
}
```

**Description:** Represents supported value types.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### BoolArray(Array\<Bool>)

```cangjie
BoolArray(Array<Bool>)
```

**Description:** Indicates an array of boolean values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### BoolData(Bool)

```cangjie
BoolData(Bool)
```

**Description:** Indicates a boolean value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### Double(Float64)

```cangjie
Double(Float64)
```

**Description:** Indicates a 64-bit floating-point value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### DoubleArray(Array\<Float64>)

```cangjie
DoubleArray(Array<Float64>)
```

**Description:** Indicates an array of 64-bit floating-point values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### Integer(Int64)

```cangjie
Integer(Int64)
```

**Description:** Indicates a 64-bit signed integer value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### StringArray(Array\<String>)

```cangjie
StringArray(Array<String>)
```

**Description:** Indicates an array of string values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21

### StringData(String)

```cangjie
StringData(String)
```

**Description:** Indicates a string value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 21