# ohos.data.distributed_kv_store

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The distributed key-value database provides applications with distributed collaboration capabilities across different devices. By calling various interfaces of the distributed key-value database, applications can save data to the database and perform operations such as addition, deletion, modification, query, and synchronization on the data.

This module offers the following common functionalities related to distributed key-value databases:

- [KVManager](#class-kvmanager): A distributed key-value database management instance used to obtain database-related information.
- [KVStoreResultSet](#class-kvstoreresultset): Provides methods for obtaining database result sets, including querying and moving data read positions.
- [Query](#class-query): Uses predicates to represent database queries, providing methods to create Query instances, query data in the database, and add predicates.
- [SingleKVStore](#class-singlekvstore): A single-version distributed key-value database that does not distinguish between data ownership by devices. Modifications to the same key by different devices will overwrite each other. It provides methods for querying and synchronizing data.
- [DeviceKVStore](#class-devicekvstore): A device collaboration database that inherits from [SingleKVStore](#class-singlekvstore). It distinguishes data by device dimension, avoiding conflicts, and supports methods for querying and synchronizing data by device dimension.

## Import Module

```cangjie
import kit.ArkData.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

## Usage Instructions

API example code usage instructions:

- If the first line of the example code has a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class Constants

```cangjie
public class Constants {
    public static let MAX_KEY_LENGTH: Int32 = 1024
    public static let MAX_VALUE_LENGTH: Int32 = 4194303
    public static let MAX_KEY_LENGTH_DEVICE: Int32 = 896
    public static let MAX_STORE_ID_LENGTH: Int32 = 128
    public static let MAX_QUERY_LENGTH: Int32 = 512000
    public static let MAX_BATCH_SIZE: Int32 = 128
}
```

**Function:** Constants for the distributed key-value database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_BATCH_SIZE

```cangjie
public static let MAX_BATCH_SIZE: Int32 = 128
```

**Function:** The maximum number of batch operations.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_KEY_LENGTH

```cangjie
public static let MAX_KEY_LENGTH: Int32 = 1024
```

**Function:** The maximum allowed length of a key in the database, in bytes. If there are duplicate symbols, it is recommended to use the alias: KV_MAX_KEY_LENGTH.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_KEY_LENGTH_DEVICE

```cangjie
public static let MAX_KEY_LENGTH_DEVICE: Int32 = 896
```

**Function:** The maximum allowed length of a key in the device collaboration database, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_QUERY_LENGTH

```cangjie
public static let MAX_QUERY_LENGTH: Int32 = 512000
```

**Function:** The maximum query length, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_STORE_ID_LENGTH

```cangjie
public static let MAX_STORE_ID_LENGTH: Int32 = 128
```

**Function:** The maximum allowed length of a database identifier, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### static let MAX_VALUE_LENGTH

```cangjie
public static let MAX_VALUE_LENGTH: Int32 = 4194303
```

**Function:** The maximum allowed length of a value in the database, in bytes. It is recommended to use the alias: KV_MAX_VALUE_LENGTH.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

## class DeviceKVStore

```cangjie
public class DeviceKVStore <: SingleKVStore {}
```

**Function:** A device collaboration database that inherits from SingleKVStore, providing methods for querying and synchronizing data.

The device collaboration database distinguishes data by device dimension. Each device can only write and modify its own data, while data from other devices is read-only and cannot be modified.

For example, the device collaboration database can be used to implement photo sharing between devices, allowing users to view photos from other devices but not modify or delete them.

Before calling methods of DeviceKVStore, a DeviceKVStore instance must be created.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

**Parent Type:**

- [SingleKVStore](#class-singlekvstore)

### func get(String)

```cangjie
public func get(key: String): KVValueType
```

**Function:** Gets the value of the specified key for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| key | String | Yes | - | The key of the data to query. It cannot be empty and its length must not exceed [MAX_KEY_LENGTH_DEVICE](#static-let-max_key_length_device). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [KVValueType](#enum-kvvaluetype) | Returns the queried value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100004 | Not found. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.get("key")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEntries(String)

```cangjie
public func getEntries(keyPrefix: String): Array<Entry>
```

**Function:** Gets a list of key-value pairs matching the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| keyPrefix | String | Yes | - | The key prefix to match. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<[Entry](#class-entry)> | Returns a list of key-value pairs matching the specified prefix. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.getEntries("key")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getEntries(Query)

```cangjie
public func getEntries(query: Query): Array<Entry>
```

**Function:** Gets a list of key-value pairs matching the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| query | [Query](#class-query) | Yes | - | The key prefix to match. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<[Entry](#class-entry)> | Returns a list of key-value pairs matching the specified Query object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.getEntries(Query())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getResultSet(String)

```cangjie
public func getResultSet(keyPrefix: String): KVStoreResultSet
```

**Function:** Gets a KVStoreResultSet object matching the specified Query object for the current device.The maximum number of open result sets is 8.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| keyPrefix | String | Yes | - | The key prefix to match. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [KVStoreResultSet](#class-kvstoreresultset) | Gets a KVStoreResultSet object matching the specified Query object for the current device. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100001 | Over max limits. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.getResultSet("key")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getResultSet(Query)

```cangjie
public func getResultSet(query: Query): KVStoreResultSet
```

**Function:** Gets a KVStoreResultSet object matching the specified Query object for the current device.The maximum number of open result sets is 8.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| query | [Query](#class-query) | Yes | - | The query object. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [KVStoreResultSet](#class-kvstoreresultset) | Gets a KVStoreResultSet object matching the specified Query object for the current device. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100001 | Over max limits. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.getResultSet(Query())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getResultSize(Query)

```cangjie
public func getResultSize(query: Query): Int32
```

**Function:** Gets the number of results matching the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| query | [Query](#class-query) | Yes | - | The query object. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Gets the number of results matching the specified Query object for the current device. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let manager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // The Context application context needs to be obtained. For details, refer to the usage instructions in this document.
    let store = (manager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    store.getResultSize(Query())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class DistributedKVStore

```cangjie
public class DistributedKVStore {}
```

**Function:** Used to create the KVManager class.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### static func createKVManager(KVManagerConfig)

```cangjie
public static func createKVManager(config: KVManagerConfig): KVManager
```

**Function:** Creates a KVManager object instance for managing database objects.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| config | [KVManagerConfig](#class-kvmanagerconfig) | Yes | - | Provides configuration information for the KVManager instance, including the caller's package name and user information. |

**Return Value:**

| Type | Description |
|:----|:----|
| [KVManager](#class-kvmanager) | Returns the created KVManager object instance. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "com.example.myapplication")) // Context application context needs to be obtained, see usage instructions in this document
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Entry

```cangjie
public class Entry {
    public var key: String
    public var value: KVValueType

    public init(key: String, value: KVValueType)
}
```

**Function:** Key-value pairs stored in the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var key

```cangjie
public var key: String
```

**Function:** Key value.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var value

```cangjie
public var value: KVValueType
```

**Function:** Value object.

**Type:** [KVValueType](#enum-kvvaluetype)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### init(String, KVValueType)

```cangjie
public init(key: String, value: KVValueType)
```

**Function:** Constructor used to create an Entry instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key value. |
| value | [KVValueType](#enum-kvvaluetype) | Yes | - | Value object. |

## class FieldNode

```cangjie
public class FieldNode {
    public var nullable: Bool
    public var default: String
    public var type_: Int32

    public init(name: String, nullable: Bool, default: String, type_: Int32)
}
```

**Function:** Represents a node of a Schema instance, providing methods to define values stored in the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var default

```cangjie
public var default: String
```

**Function:** Represents the default value of the FieldNode.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var nodeType

```cangjie
public var nodeType: Int32
```

**Function:** Represents the data type corresponding to the specified node.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var nullable

```cangjie
public var nullable: Bool
```

**Function:** Indicates whether the database field can be null.

**Type:** Bool

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### init(String, Bool, String, Int32)

```cangjie
public init(name: String, nullable: Bool, default: String, nodeType: Int32)
```

**Function:** Creates a FieldNode instance with values.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Value of the FieldNode. |
| nullable | Bool | Yes | - | Indicates whether the database field can be null. true means this node data can be null, false means this node data cannot be null. |
| default | String | Yes | - | Represents the default value of the FieldNode. |
| nodeType | Int32 | Yes | - | Represents the data type corresponding to the specified node, taking the enumeration value corresponding to KVValueType. BYTE_ARRAY is not supported yet; using this type will cause getKVStore to fail. |

## class KVManager

```cangjie
public class KVManager {}
```

**Function:** Distributed key-value database management instance, used to obtain information related to distributed key-value databases. Before calling methods of KVManager, you need to first build a KVManager instance via [createKVManager](#static-func-createkvmanagerkvmanagerconfig).

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### func closeKVStore(String, String)

```cangjie
public func closeKVStore(appId: String, storeId: String): Unit
```

**Function:** Closes the specified distributed key-value database by the value of storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the called database. |
| storeId | String | Yes | - | Unique identifier of the database to be closed, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are as follows. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error.Possible causes:1.Mandatory parameters are left unspecified;<br>2.Parameter verification failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "com.example.myapplication")) // Context application context needs to be obtained, see usage instructions in this document
    kvManager.closeKVStore("com.example.myapplication", "myStore")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func deleteKVStore(String, String)

```cangjie
public func deleteKVStore(appId: String, storeId: String): Unit
```

**Function:** Deletes the specified distributed key-value database by the value of storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the called database. |
| storeId | String | Yes | - | Unique identifier of the database to be deleted, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are as follows. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100004 | Not found. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "com.example.myapplication")) // Context application context needs to be obtained, see usage instructions in this document
    kvManager.deleteKVStore("com.example.myapplication", "myStore")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAllKVStoreId(String)

```cangjie
public func getAllKVStoreId(appId: String): Array<String>
```

**Function:** Gets the storeId of all created distributed key-value databases that have not been deleted by calling the [deleteKVStore](#func-deletekvstorestring-string) method.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the called database. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns the storeId of all created distributed key-value databases. |

**Exceptions:**

- BusinessException: Corresponding error codes are as follows. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error.Possible causes:1.Mandatory parameters are left unspecified;<br>2.Parameter verification failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "com.example.myapplication")) // Context application context needs to be obtained, see usage instructions in this document
    kvManager.getAllKVStoreId("com.example.myapplication")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getKVStore\<T>(String, KVOptions) where T \<: SingleKVStore

```cangjie
public func getKVStore<T>(storeId: String, options: KVOptions): T where T <: SingleKVStore
```

**Function:** Creates and obtains a distributed key-value database by specifying Options and storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| storeId | String | Yes | - | Unique identifier of the database, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |
| options | [KVOptions](#class-kvoptions) | Yes | - | Configuration information for creating a distributed key-value instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | KVStore object. Single-version distributed key-value database, which does not distinguish data by device and provides methods for querying and synchronizing data. |

**Exceptions:**

- BusinessException: Corresponding error codes are as follows. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100002 | Open existed database with changed options. |
  | 15100003 | Database corrupted. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported yet. | todo | todo |

  **Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "com.example.myapplication")) // Context application context needs to be obtained, see usage instructions in this document
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let kvStore = kvManager.getKVStore("myStoreId", opt)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class KVManagerConfig

```cangjie
public class KVManagerConfig {
    public var context: BaseContext
    public var bundleName: String

    public init(context: BaseContext, bundleName: String)
}
```

**Description:** Provides configuration information for KVManager instances, including the caller's package name and application context.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var bundleName

```cangjie
public var bundleName: String
```

**Description:** The package name of the caller.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var context

```cangjie
public var context: BaseContext
```

**Description:** The application context.

**Type:** [BaseContext](../AbilityKit/cj-apis-app-ability.md#class-basecontext)

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### init(BaseContext, String)

```cangjie
public init(context: BaseContext, bundleName: String)
```

**Description:** Constructor for creating a KVManagerConfig instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [BaseContext](../AbilityKit/cj-apis-app-ability.md#class-basecontext) | Yes | - | The application context. |
| bundleName | String | Yes | - | The package name of the caller. |

## class KVStoreResultSet

```cangjie
public class KVStoreResultSet {}
```

**Description:** Provides methods for obtaining database result sets, including querying and moving data reading positions. The maximum number of open result sets is 8.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### func getCount()

```cangjie
public func getCount(): Int32
```

**Description:** Gets the total number of rows in the result set.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the total number of rows of data. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context needs to be obtained. See usage instructions for details.
    let store = (kvManager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
    store.put("key", KVValueType.StringValue("value"))
    var resultSet = store.getResultSet("key")
    resultSet.getCount()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class KVOptions

```cangjie
public class KVOptions {
    public var createIfMissing: Bool
    public var encrypt: Bool
    public var backup: Bool
    public var autoSync: Bool
    public var securityLevel: KVSecurityLevel
    public var schema:?Schema

    public init(securityLevel: KVSecurityLevel, createIfMissing!: Bool = true, encrypt!: Bool = false,
        backup!: Bool = true, autoSync!: Bool = false, schema!: ?Schema = None)
}
```

**Description:** Provides configuration information for creating a database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var autoSync

```cangjie
public var autoSync: Bool
```

**Description:** Sets whether the database file is automatically synchronized. The default is false, meaning manual synchronization.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var backup

```cangjie
public var backup: Bool
```

**Description:** Sets whether the database file is backed up. The default is true, meaning backup is enabled.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var createIfMissing

```cangjie
public var createIfMissing: Bool
```

**Description:** Sets whether to create a database if the database file does not exist. The default is true, meaning creation is enabled.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var encrypt

```cangjie
public var encrypt: Bool
```

**Description:** Sets whether the database file is encrypted. The default is false, meaning encryption is disabled.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### var schema

```cangjie
public var schema:?Schema
```

**Description:** Schema()|Sets the definition of values stored in the database. The default is undefined, meaning no Schema is used.

**Type:** ?[Schema](#class-schema)

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var securityLevel

```cangjie
public var securityLevel: KVSecurityLevel
```

**Description:** Sets the security level of the database.

**Type:** [KVSecurityLevel](#enum-kvsecuritylevel)

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### init(KVSecurityLevel, Bool, Bool, Bool, Bool, ?Schema)

```cangjie
public init(securityLevel: KVSecurityLevel, createIfMissing!: Bool = true, encrypt!: Bool = false,
    backup!: Bool = true, autoSync!: Bool = false, schema!: ?Schema = None)
```

**Description:** Constructor for creating a KVOptions instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| securityLevel | [KVSecurityLevel](#enum-kvsecuritylevel) | Yes | - | Sets the security level of the database.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| createIfMissing | Bool | No | true | Sets whether to create a database if the database file does not exist. The default is true, meaning creation is enabled.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| encrypt | Bool | No | false | Sets whether the database file is encrypted. The default is false, meaning encryption is disabled.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| backup | Bool | No | true | Sets whether the database file is backed up. The default is true, meaning backup is enabled. <br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| autoSync | Bool | No | false | Sets whether the database file is automatically synchronized. The default is false, meaning manual synchronization.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core<br>**Required Permission:** ohos.permission.DISTRIBUTED_DATASYNC |
| schema | ?[Schema](#class-schema) | No | None | Sets the definition of values stored in the database. The default is undefined, meaning no Schema is used.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore |

## class Query

```cangjie
public class Query {

    public init()
}
```

**Description:** Uses predicates to represent database queries, providing methods to create Query instances, query data in the database, and add predicates. The maximum number of predicates in a Query object is 256.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### init()

```cangjie
public init()
```

**Description:** Constructor for creating a Query instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

## class Schema

```cangjie
public class Schema {
    public var root: FieldNode
    public var indexes: Array<String>
    public var mode: Int32
    public var skip: Int32

    public init(root: FieldNode, indexes: Array<String>, mode: Int32, skip: Int32)
}
```

**Description:** Represents a database schema. Schema objects can be created when creating or opening a database and placed in [KVOptions](#class-kvoptions).

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var indexes

```cangjie
public var indexes: Array<String>
```

**Description:** Represents an array of JSON-type strings.

**Type:** Array\<String>

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var mode

```cangjie
public var mode: Int32
```

**Description:** Represents the mode of the Schema.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var root

```cangjie
public var root: FieldNode
```

**Description:** Represents the JSON root object.

**Type:** [FieldNode](#class-fieldnode)

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### var skip

```cangjie
public var skip: Int32
```

**Description:** The skip size of the Schema.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

### init(FieldNode, Array\<String>, Int32, Int32)

```cangjie
public init(root: FieldNode, indexes: Array<String>, mode: Int32, skip: Int32)
```

**Description:** Represents a database schema. Schema objects can be created when creating or opening a database and placed in [KVOptions](#class-kvoptions).

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| root | [FieldNode](#class-fieldnode) | Yes | - | Represents the JSON root object. |
| indexes | Array\<String> | Yes | - | Represents an array of JSON-type strings. |
| mode | Int32 | Yes | - | Represents the mode of the Schema. |
| skip | Int32 | Yes | - | The skip size of the Schema. |

## class SingleKVStore

```cangjie
public open class SingleKVStore {}
```

**Description:** SingleKVStore database instance, providing methods to add data, delete data, subscribe to data changes, and subscribe to data synchronization completion.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22### func backup(String)

```cangjie
public open func backup(file: String): Unit
```

**Function:** Backs up the database with the specified name.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| file | String | Yes | - | Specified name for backing up the database. Cannot be empty and length must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.backup("myBackupfile")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func commit()

```cangjie
public open func commit(): Unit
```

**Function:** Commits a transaction in the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.commit()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func delete(String)

```cangjie
public open func delete(key: String): Unit
```

**Function:** Deletes data with the specified key from the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key of the data to be deleted. Cannot be empty and length must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.delete("myKey")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func deleteBatch(Array\<String>)

```cangjie
public open func deleteBatch(keys: Array<String>): Unit
```

**Function:** Batch deletes key-value pairs from the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keys | Array\<String> | Yes | - | Key-value pairs to be batch deleted. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let deviceKVStore = (kvManager.getKVStore("myStoreId", opt) as DeviceKVStore).getOrThrow()
    deviceKVStore.deleteBatch(["myBackupfile", "BK002"])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func enableSync(Bool)

```cangjie
public open func enableSync(enabled: Bool): Unit
```

**Function:** Sets whether to enable synchronization.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| enabled | Bool | Yes | - | Whether to enable synchronization. `true` enables synchronization; `false` disables it. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.ArrayList
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.enableSync(true)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func get(String)

```cangjie
public open func get(key: String): KVValueType
```

**Function:** Gets the value of the specified key.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key of the data to be queried. Cannot be empty and length must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Return Value:**

| Type | Description |
|:----|:----|
| [KVValueType](#enum-kvvaluetype) | Returns the queried value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100004 | Not found. |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

let kvManager = DistributedKVStore.createKVManager(KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
let kvStore = (kvManager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
try {
    let value = kvStore.get("myKey")
    match (value) {
        case StringValue(v) => Hilog.info(0, "test", "The obtained value is a String: ${v}", "")
        case Integer(v) => Hilog.info(0, "test", "The obtained value is a Int32: ${v}", "")
        case Double(v) => Hilog.info(0, "test", "The obtained value is a Float64: ${v}", "")
        case _ => Hilog.info(0, "test", "The obtained value is of another type.", "")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "get failed.", "")
}
```

### func put(String, KVValueType)

```cangjie
public open func put(key: String, value: KVValueType): Unit
```

**Function:** Adds a key-value pair of the specified type to the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key of the data to be added. Cannot be empty and length must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |
| value | [KVValueType](#enum-kvvaluetype) | Yes | - | Value of the data to be added. Supports Array\<UInt8>, String, Int32, Bool, Float32, Float64. The length of Array\<UInt8> and String must not exceed [MAX_VALUE_LENGTH](#static-let-max_value_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

let kvManager = DistributedKVStore.createKVManager(
    KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
let kvStore = (kvManager.getKVStore("test", KVOptions(KVSecurityLevel.S1)) as DeviceKVStore).getOrThrow()
try {
    kvStore.put("myKey", StringValue("myValue"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "put failed.", "")
}
```

### func putBatch(Array\<Entry>)

```cangjie
public open func putBatch(entries: Array<Entry>): Unit
```

**Function:** Batch inserts key-value pairs into the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| entries | Array\<[Entry](#class-entry)> | Yes | - | Key-value pairs to be batch inserted. The maximum data volume allowed in a single entries object is 512M. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(
        KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    let entries = ArrayList<Entry>()
    for (i in 0..10) {
        let entry = Entry("batch_test_string_key${i}", StringValue("batch_test_string_value"))
        entries.add(entry)
    }
    singleKVStore.putBatch(entries.toArray())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func restore(String)

```cangjie
public open func restore(file: String): Unit
```

**Function:** Restores the database from the specified database file.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| file | String | Yes | - | Specified database file name. Cannot be empty and length must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(
        KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.restore("myBackupfile")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func rollback()

```cangjie
public open func rollback(): Unit
```

**Function:** Rolls back a transaction in the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100005 | Database or result set already closed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let kvManager = DistributedKVStore.createKVManager(
        KVManagerConfig(Global.getStageContext(), "test_kvstore")) // Context application context required. See usage instructions for details.
    let opt = KVOptions(
        KVSecurityLevel.S4,
        createIfMissing: true,
        encrypt: false,
        backup: true,
        autoSync: false,
    )
    let singleKVStore = kvManager.getKVStore("myStoreId", opt)
    singleKVStore.rollback()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setSyncParam(UInt32)

```cangjie
public open func setSyncParam(defaultAllowedDelayMs: UInt32): Unit
```

**Function:** Sets the default allowed delay for database synchronization.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Initial Version:** 22

**## enum KVSecurityLevel

```cangjie
public enum KVSecurityLevel {
    | S1
    | S2
    | S3
    | S4
    | ...
}
```

**Function:** Enumeration for database security levels.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### S1

```cangjie
S1
```

**Function:** Indicates the database security level is low. Data leakage, tampering, destruction, or loss may cause limited adverse impacts on individuals or organizations. Examples include gender, nationality, user application records, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### S2

```cangjie
S2
```

**Function:** Indicates the database security level is medium. Data leakage, tampering, destruction, or loss may cause significant adverse impacts on individuals or organizations. Examples include detailed personal communication addresses, names/nicknames, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### S3

```cangjie
S3
```

**Function:** Indicates the database security level is high. Data leakage, tampering, destruction, or loss may cause severe adverse impacts on individuals or organizations. Examples include real-time precise location information, movement trajectories, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### S4

```cangjie
S4
```

**Function:** Indicates the database security level is critical, covering special data types defined by industry laws and regulations that involve the most private aspects of individuals. Data leakage, tampering, destruction, or loss may cause major adverse impacts. Examples include political views, religion, philosophical beliefs, trade union membership, genetic data, biometric information, health and sexual life status, sexual orientation, device authentication credentials, personal credit card/financial information, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

## enum KVValueType

```cangjie
public enum KVValueType {
    | StringValue(String)
    | Integer(Int32)
    | Float(Float32)
    | ByteArray(Array<Byte>)
    | Boolean(Bool)
    | Double(Float64)
    | ...
}
```

**Function:** Enumeration for data types.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### Boolean(Bool)

```cangjie
Boolean(Bool)
```

**Function:** Indicates the value type is boolean.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### ByteArray(Array\<Byte>)

```cangjie
ByteArray(Array<Byte>)
```

**Function:** Indicates the value type is byte array.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### Double(Float64)

```cangjie
Double(Float64)
```

**Function:** Indicates the value type is Float64 floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### Float(Float32)

```cangjie
Float(Float32)
```

**Function:** Indicates the value type is Float32 floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### Integer(Int32)

```cangjie
Integer(Int32)
```

**Function:** Indicates the value type is Int32 integer.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** Indicates the value type is string.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 22