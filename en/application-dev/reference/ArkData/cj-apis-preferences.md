# ohos.data.preferences

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

User Preferences provide applications with Key-Value pair data processing capabilities, supporting lightweight data persistence for applications, along with modification and query operations.

Data is stored in key-value pairs where keys are of string type, and values can be numeric, string, boolean, or arrays of these three types.

## Import Module

```cangjie
import kit.ArkData.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration is needed in the "main_ability.cj" file of the Cangjie template project.
- A valid [dataGroupId](#var-datagroupid) must be obtained from the application market.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## const MAX_KEY_LENGTH

```cangjie
public const MAX_KEY_LENGTH: UInt32 = 1024
```

**Description:** Maximum key length limit of 1024 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

## const MAX_VALUE_LENGTH

```cangjie
public const MAX_VALUE_LENGTH: UInt32 = 16 * 1024 * 1024
```

**Description:** Maximum value length limit of 16 * 1024 * 1024 bytes.

**Type:** UInt32

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

## class PreferencesOptions

```cangjie
public class PreferencesOptions {
    public var name: String
    public var dataGroupId: String
    public var storageType: StorageType
    public init(name: String, dataGroupId!: String = String.empty,
        storageType!: StorageType = StorageType.Xml)
}
```

**Description:** Configuration options for Preferences instances.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### var dataGroupId

```cangjie
public var dataGroupId: String
```

**Description:** Application group ID, which must be obtained from the application market.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### var name

```cangjie
public var name: String
```

**Description:** Name of the Preferences instance.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### var storageType

```cangjie
public var storageType: StorageType
```

**Description:** Storage mode (optional parameter).

**Type:** [StorageType](#enum-storagetype)

**Access:** Read-write

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### init(String, String, StorageType)

```cangjie
public init(name: String, dataGroupId!: String = String.empty,
    storageType!: StorageType = StorageType.Xml)
```

**Description:** Constructor for creating PreferencesOptions instances. By default, creates a Preferences instance in the application sandbox directory.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the Preferences instance. |
| dataGroupId | String | No | String.empty | Application group ID, which must be obtained from the application market. |
| storageType | [StorageType](#enum-storagetype) | No | StorageType.Xml | Storage mode (optional parameter). |

## class Preferences

```cangjie
public class Preferences {}
```

**Description:** Preferences class providing interfaces for accessing and modifying stored data.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### static func deletePreferences(UIAbilityContext, String)

```cangjie
public static func deletePreferences(context: UIAbilityContext, name: String): Unit
```

**Description:** Removes the specified Preferences instance from cache. If the Preferences instance has a corresponding persistent file, the file is also deleted.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |
| 15500010 | Failed to delete the user preferences persistence file. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Get Preferences instance
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), "myStore")  // Application context required; see usage instructions above
    // Delete Preferences instance
    Preferences.deletePreferences(Global.getAbilityContext(), "myStore")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func deletePreferences(UIAbilityContext, PreferencesOptions)

```cangjie
public static func deletePreferences(context: UIAbilityContext, options: PreferencesOptions): Unit
```

**Description:** Removes the specified Preferences instance from cache. If the Preferences instance has a corresponding persistent file, the file is also deleted.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [PreferencesOptions](#class-preferencesoptions) | Yes | - | Configuration options related to the Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 801 | Capability not supported. |
| 15500000 | Inner error. |
| 15500010 | Failed to delete the user preferences persistence file. |
| 15501001 | The operations is supported in stage mode only. |
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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Get Preferences instance
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), "myStore")  // Application context required; see usage instructions above
    // Delete Preferences instance
    Preferences.deletePreferences(Global.getAbilityContext(), "myStore")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getPreferences(UIAbilityContext, String)

```cangjie
public static func getPreferences(context: UIAbilityContext, name: String): Preferences
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-string) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-string) will retrieve the instance directly from cache rather than reading from the persistent file. After calling this interface to remove the instance from cache, the next getPreferences call will read the persistent file again and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Preferences](#class-preferences) | Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Application context required; see usage instructions above
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getPreferences(UIAbilityContext, PreferencesOptions)

```cangjie
public static func getPreferences(context: UIAbilityContext, options: PreferencesOptions): Preferences
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-preferencesoptions) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-preferencesoptions) will retrieve the instance directly from cache rather than reading from the persistent file. After calling this interface to remove the instance from cache, the next getPreferences call will read the persistent file again and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [PreferencesOptions](#class-preferencesoptions) | Yes | - | Name of the Preferences instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Preferences](#class-preferences) | Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 801 | Capability not supported. |
| 15500000 | Inner error. |
| 15501001 | The operations is supported in stage mode only. |
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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Application context required; see usage instructions above
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func removePreferencesFromCache(UIAbilityContext, String)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, name: String): Unit
```

**Description:** Removes the specified Preferences instance from cache.

When an application first calls [getPreferences](#static-func-getpreferencesuiabilitycontext-string) to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-string) will retrieve the instance directly from cache rather than reading from the persistent file. After calling this interface to remove the instance from cache, the next getPreferences call will read the persistent file again and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may cause data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | String | Yes | - | Name of the Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Application context required; see usage instructions above
    // Remove Preferences instance from cache
    Preferences.removePreferencesFromCache(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### static func removePreferencesFromCache(UIAbilityContext, PreferencesOptions)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, options: PreferencesOptions): Unit
```

**Function:** Removes the specified Preferences instance from the cache.

When an application first calls the [getPreferences](#static-func-getpreferencesuiabilitycontext-preferencesoptions) interface to obtain a Preferences instance, the instance is cached. Subsequent calls to [getPreferences](#static-func-getpreferencesuiabilitycontext-preferencesoptions) will retrieve the instance directly from the cache without reading from the persistent file again. After calling this interface to remove the instance from the cache, the next getPreferences call will re-read the persistent file and generate a new Preferences instance.

After calling this interface, it is not recommended to continue using the old Preferences instance for data operations, as this may lead to data consistency issues.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| options | [PreferencesOptions](#class-preferencesoptions) | Yes | - | The name of the Preferences instance. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 801 | Capability not supported. |
| 15500000 | Inner error. |
| 15501001 | The operations is supported in stage mode only. |
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
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    // Remove the Preferences instance from the cache
    Preferences.removePreferencesFromCache(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func clear()

```cangjie
public func clear(): Unit
```

**Function:** Clears all data in the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    preferences.put("myKey", PreferencesValueType.StringData("myValue"))
    preferences.clear()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func delete(String)

```cangjie
public func delete(key: String): Unit
```

**Function:** Deletes the key-value pair with the given key from the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The name of the key to be deleted. Cannot be empty. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Obtain the Preferences instance
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), "myStore") // Context application context needs to be obtained. For details, see the usage instructions in this document.
    preferences.delete("startup")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func flush()

```cangjie
public func flush(): Unit
```

**Function:** Stores the data in the cached Preferences instance into the persistent file of user preferences.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    preferences.put("myKey", PreferencesValueType.StringData("myValue"))
    preferences.flush()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func get(String, PreferencesValueType)

```cangjie
public func get(key: String, defValue: PreferencesValueType): PreferencesValueType
```

**Function:** Retrieves the value corresponding to the key from the cached Preferences instance. If the key does not exist, returns the default value defValue.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The name of the key to be retrieved. |
| defValue | [PreferencesValueType](#enum-preferencesvaluetype) | Yes | - | The default return value. Supports Int64, Float64, String, Bool, Array\<Bool>, Array\<Float64>, Array\<String>. |

**Return Value:**

| Type | Description |
|:----|:----|
| [PreferencesValueType](#enum-preferencesvaluetype) | The value corresponding to the key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var value = preferences.get("key", PreferencesValueType.Integer(0))
    match (value) {
        case PreferencesValueType.Integer(n) => Hilog.info(0, "AppLogCj", "Retrieved value: ${n}")
        case _ => Hilog.info(0, "AppLogCj", "Retrieved value is not an Int")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAll()

```cangjie
public func getAll(): HashMap<String, PreferencesValueType>
```

**Function:** Retrieves all key-value data from the cached Preferences instance.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| HashMap\<String, [PreferencesValueType](#enum-preferencesvaluetype)> | A HashMap object containing all key-value data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var values = preferences.getAll()
    for ((k, v) in values) {
        match (v) {
            case PreferencesValueType.Integer(n) => Hilog.info(0, "AppLogCj", "Retrieved key-value pair: key: ${k} value: ${n}")
            case PreferencesValueType.Double(n) => Hilog.info(0, "AppLogCj", "Retrieved key-value pair: key: ${k} value: ${n}")
            case PreferencesValueType.StringData(n) => Hilog.info(0, "AppLogCj", "Retrieved key-value pair: key: ${k} value: ${n}")
            case _ => Hilog.info(0, "AppLogCj", "Other value")
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func has(String)

```cangjie
public func has(key: String): Bool
```

**Function:** Checks whether the cached Preferences instance contains a key-value pair with the given key.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The name of the key to be checked. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | A Boolean value. Returns whether the Preferences instance contains a key-value pair with the given key. true indicates existence; false indicates non-existence. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let preferences = Preferences.getPreferences(Global.getAbilityContext(), PreferencesOptions("mystore", dataGroupId:"myGroupID")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let hasKey = preferences.has("startup")
    if (hasKey) {
        Hilog.info(0, "AppLogCj", "The key 'startup' is contained.")
    } else {
        Hilog.info(0, "AppLogCj", "The key 'startup' does not exist.")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(PreferencesEvent, ?Callback1Argument\<String>)

```cangjie
public func off(event :PreferencesEvent, callback!: ?Callback1Argument<String> = None): Unit
```

**Function:** Unsubscribes from data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [PreferencesEvent](#enum-preferencesevent) | Yes | - | Event type, indicating unsubscription from data changes or inter-process data changes. |
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String> | No | None | The callback function to be unsubscribed. If not specified, all callbacks are unsubscribed.<br> String: The type of the changed key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    // This code can be added to the dependency definition
    // Callback function
    class Callback <: Callback1Argument<String> {
        public func invoke(err: ?BusinessException, arg: String): Unit {
            Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
        }
    }

    var str = "container"
    var a = Preferences.getPreferences(Global.getAbilityContext(), str) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var c = Callback()
    a.on(PreferencesEvent.PreferencesChange, c)
    a.off(PreferencesEvent.PreferencesChange)
    a.put("kkk1", PreferencesValueType.StringData("vvv1"))
    a.flush()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(PreferencesEvent, Callback1Argument\<String>)

```cangjie
public func on(event :PreferencesEvent, callback: Callback1Argument<String>): Unit
```

**Function:** Subscribes to data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [PreferencesEvent](#enum-preferencesevent) | Yes | - | Event type.<br> When PreferencesChange, it indicates subscription to data changes. After the value of the subscribed key changes, the callback is triggered upon executing the flush method.<br> When PreferencesMultiProcessChange, it indicates subscription to inter-process data changes. When multiple processes hold the same preferences file, the callback is triggered upon executing the flush method after the value of the subscribed key changes in any process. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String> | Yes | - | Callback function.<br>String: The type of the changed key. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |
| 15500019 | Failed to obtain the subscription service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    // Callback function
    class Callback <: Callback1Argument<String> {
        public func invoke(err: ?BusinessException, arg: String): Unit {
            Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
        }
    }

    var str = "container"
    var a = Preferences.getPreferences(Global.getAbilityContext(), str) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var c = Callback()
    a.on(PreferencesEvent.PreferencesChange, c)
    a.put("kkk1", PreferencesValueType.StringData("vvv1"))
    a.flush()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func put(String, PreferencesValueType)

```cangjie
public func put(key: String, value: PreferencesValueType): Unit
```

**Function:** Writes data to the cached Preferences instance. The Preferences instance can be persisted via [flush](#func-flush).

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The key to be modified. Cannot be empty. |
| value | [PreferencesValueType](#enum-preferencesvaluetype) | Yes | - | The new value to be stored. Supports Int64, Float64, String, Bool, Array\<Bool>, Array\<Float64>, Array\<String>. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Preferences Error Codes](./cj-errorcode-preferences.md).

| Error Code ID | Error Message |
| :---- | :--- |
| 15500000 | Inner error. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData## enum PreferencesEvent

```cangjie
public enum PreferencesEvent {
    | PreferencesChange
    | PreferencesMultiProcessChange
}
```

**Description:** Enumeration of Preferences event types.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### PreferencesChange

```cangjie
PreferencesChange
```

**Description:** Indicates data changes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### PreferencesMultiProcessChange

```cangjie
PreferencesMultiProcessChange
```

**Description:** Indicates data changes across multiple processes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

## enum StorageType

```cangjie
public enum StorageType {
    | Xml
    | Gskv
}
```

**Description:** Enumeration of Preferences storage modes.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### Gskv

```cangjie
Gskv
```

**Description:** Represents GSKV storage mode.

**Characteristics:** Data is stored in GSKV database mode. Operations on data are immediately persisted to disk without requiring the flush interface.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### Xml

```cangjie
Xml
```

**Description:** Represents XML storage mode, which is the default storage mode for Preferences.

**Characteristics:** Data is stored in XML format. Operations on data occur in memory, requiring the flush interface for disk persistence.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

## enum PreferencesValueType

```cangjie
public enum PreferencesValueType {
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

**Since:** 22

### BoolArray(Array\<Bool>)

```cangjie
BoolArray(Array<Bool>)
```

**Description:** Represents an array of boolean values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### BoolData(Bool)

```cangjie
BoolData(Bool)
```

**Description:** Represents a boolean value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### Double(Float64)

```cangjie
Double(Float64)
```

**Description:** Represents a 64-bit floating-point value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### DoubleArray(Array\<Float64>)

```cangjie
DoubleArray(Array<Float64>)
```

**Description:** Represents an array of 64-bit floating-point values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### Integer(Int64)

```cangjie
Integer(Int64)
```

**Description:** Represents a 64-bit signed integer value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### StringArray(Array\<String>)

```cangjie
StringArray(Array<String>)
```

**Description:** Represents an array of string values.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22

### StringData(String)

```cangjie
StringData(String)
```

**Description:** Represents a string value.

**System Capability:** SystemCapability.DistributedDataManager.Preferences.Core

**Since:** 22