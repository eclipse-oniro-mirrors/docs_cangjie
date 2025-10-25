# ohos.data.distributed_kv_store

The distributed key-value database provides applications with distributed collaboration capabilities for databases across different devices. By calling various interfaces of the distributed key-value database, applications can save data to the distributed key-value database and perform operations such as addition, deletion, modification, query, and synchronization on the data in the distributed key-value database.

This module provides the following common functionalities related to the distributed key-value database:

- [KVManager](#class-kvmanager): A distributed key-value database management instance used to obtain database-related information.
- [KVStoreResultSet](#class-kvstoreresultset): Provides methods for obtaining database result sets, including querying and moving data reading positions.
- [Query](#class-query): Uses predicates to represent database queries, providing methods to create Query instances, query data in the database, and add predicates.
- [SingleKVStore](#class-singlekvstore): A single-version distributed key-value database that does not distinguish data by device. Modifications to the same key by different devices will overwrite each other. It provides methods for querying and synchronizing data.
- [DeviceKVStore](#class-devicekvstore): A device collaboration database that inherits from [SingleKVStore](#class-singlekvstore). It distinguishes data by device dimension, avoiding conflicts, and supports methods for querying and synchronizing data by device dimension.

## Import Module

```cangjie
import kit.ArkData.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

## Usage Guidelines

API sample code usage guidelines:

- If the first line of the sample code has a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

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

**Since:** 21

### static let MAX_BATCH_SIZE

```cangjie
public static let MAX_BATCH_SIZE: Int32 = 128
```

**Function:** Maximum number of batch operations.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### static let MAX_KEY_LENGTH

```cangjie
public static let MAX_KEY_LENGTH: Int32 = 1024
```

**Function:** Maximum allowed length of a key in the database, in bytes. If there are duplicate symbols, it is recommended to use the alias: KV_MAX_KEY_LENGTH.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### static let MAX_KEY_LENGTH_DEVICE

```cangjie
public static let MAX_KEY_LENGTH_DEVICE: Int32 = 896
```

**Function:** Maximum allowed length of a key in the device collaboration database, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### static let MAX_QUERY_LENGTH

```cangjie
public static let MAX_QUERY_LENGTH: Int32 = 512000
```

**Function:** Maximum query length, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### static let MAX_STORE_ID_LENGTH

```cangjie
public static let MAX_STORE_ID_LENGTH: Int32 = 128
```

**Function:** Maximum allowed length of a database identifier, in bytes.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### static let MAX_VALUE_LENGTH

```cangjie
public static let MAX_VALUE_LENGTH: Int32 = 4194303
```

**Function:** Maximum allowed length of a value in the database, in bytes. It is recommended to use the alias: KV_MAX_VALUE_LENGTH.

**Type:** Int32

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

## class DeviceKVStore

```cangjie
public class DeviceKVStore <: SingleKVStore {}
```

**Function:** A device collaboration database that inherits from SingleKVStore, providing methods for querying and synchronizing data.

The device collaboration database distinguishes data by device dimension. Each device can only write and modify its own data. Data from other devices is read-only and cannot be modified.

For example, the device collaboration database can be used to implement image sharing between devices. You can view images from other devices but cannot modify or delete them.

Before calling the methods of DeviceKVStore, you need to first create a DeviceKVStore instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

**Parent Type:**

- [SingleKVStore](#class-singlekvstore)

### func get(String)

```cangjie

public func get(key: String): ValueType
```

**Function:** Gets the value of the specified key for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | The key of the data to query. It cannot be empty and its length must not exceed [MAX_KEY_LENGTH_DEVICE](#static-let-max_key_length_device). |

**Return Value:**

| Type | Description |
|:----|:----|
| [ValueType](#enum-valuetype) | Returns the value obtained from the query. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100003 | Database corrupted. |
  | 15100004 | Not found. |
  | 15100005 | Database or result set already closed. |

### func getEntries(String)

```cangjie

public func getEntries(keyPrefix: String): Array<Entry>
```

**Function:** Gets a list of key-value pairs that match the specified key prefix for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keyPrefix | String | Yes | - | The key prefix to match. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Entry](#class-entry)> | Returns a list of key-value pairs that match the specified prefix. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

### func getEntries(Query)

```cangjie

public func getEntries(query: Query): Array<Entry>
```

**Function:** Gets a list of key-value pairs that match the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| query | [Query](#class-query) | Yes | - | The query object to match. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Entry](#class-entry)> | Returns a list of key-value pairs that match the specified Query object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

### func getResultSet(String)

```cangjie

public func getResultSet(keyPrefix: String): KVStoreResultSet
```

**Function:** Gets a KVStoreResultSet object that matches the specified key prefix for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| keyPrefix | String | Yes | - | The key prefix to match. |

**Return Value:**

| Type | Description |
|:----|:----|
| [KVStoreResultSet](#class-kvstoreresultset) | Returns a KVStoreResultSet object that matches the specified key prefix. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 15100001 | Over max limits. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

### func getResultSet(Query)

```cangjie

public func getResultSet(query: Query): KVStoreResultSet
```

**Function:** Gets a KVStoreResultSet object that matches the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| query | [Query](#class-query) | Yes | - | The query object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [KVStoreResultSet](#class-kvstoreresultset) | Returns a KVStoreResultSet object that matches the specified Query object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 15100001 | Over max limits. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

### func getResultSize(Query)

```cangjie

public func getResultSize(query: Query): Int32
```

**Function:** Gets the number of results that match the specified Query object for the current device.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| query | [Query](#class-query) | Yes | - | The query object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the number of results that match the specified Query object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

## class DistributedKVStore

```cangjie
public class DistributedKVStore {}
```

**Function:** Used to create the KVManager class.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### static func createKVManager(KVManagerConfig)

```cangjie

public static func createKVManager(config: KVManagerConfig): KVManager
```

**Function:** Creates a KVManager object instance for managing database objects.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| config | [KVManagerConfig](#class-kvmanagerconfig) | Yes | - | Provides configuration information for the KVManager instance, including the caller's package name and user information. |

**Return Value:**

| Type | Description |
|:----|:----|
| [KVManager](#class-kvmanager) | Returns the created KVManager object instance. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | The context type is not supported. Only support UIAbilityContext. | todo | todo |## class Entry

```cangjie
public class Entry {
    public var key: String
    public var value: ValueType

    public init(key: String, value: ValueType)
}
```

**Function:** Key-value pair stored in the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var key

```cangjie
public var key: String
```

**Function:** Key value.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var value

```cangjie
public var value: ValueType
```

**Function:** Value object.

**Type:** [ValueType](#enum-valuetype)

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### init(String, ValueType)

```cangjie
public init(key: String, value: ValueType)
```

**Function:** Constructor for creating an Entry instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| key | String | Yes | - | Key value. |
| value | [ValueType](#enum-valuetype) | Yes | - | Value object. |

## class FieldNode

```cangjie
public class FieldNode {
    public var nullable: Bool
    public var default: String
    public var type_: Int32

    public init(name: String, nullable: Bool, default: String, type_: Int32)
}
```

**Function:** Represents a node in a Schema instance, providing methods to define values stored in the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var default

```cangjie
public var default: String
```

**Function:** Default value of the FieldNode.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var nodeType

```cangjie
public var nodeType: Int32
```

**Function:** Data type corresponding to the specified node.

**Type:** Int32

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var nullable

```cangjie
public var nullable: Bool
```

**Function:** Indicates whether the database field can be null.

**Type:** Bool

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### init(String, Bool, String, Int32)

```cangjie
public init(name: String, nullable: Bool, default: String, nodeType: Int32)
```

**Function:** Creates a FieldNode instance with values.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Value of the FieldNode. |
| nullable | Bool | Yes | - | Indicates whether the database field can be null. `true` means the node data can be null, `false` means it cannot. |
| default | String | Yes | - | Default value of the FieldNode. |
| nodeType | Int32 | Yes | - | Data type corresponding to the specified node, which takes the enumeration value of ValueType. BYTE_ARRAY is not supported yet; using this type will cause getKVStore to fail. |

## class KVManager

```cangjie
public class KVManager {}
```

**Function:** Distributed key-value database management instance, used to obtain information about distributed key-value databases. Before calling KVManager methods, you need to first create a KVManager instance via [createKVManager](#static-func-createkvmanagerkvmanagerconfig).

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### func closeKVStore(String, String)

```cangjie
public func closeKVStore(appId: String, storeId: String): Unit
```

**Function:** Closes the specified distributed key-value database based on the storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the database caller. |
| storeId | String | Yes | - | Unique identifier of the database to be closed, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Parameter verification failed. |

### func deleteKVStore(String, String)

```cangjie
public func deleteKVStore(appId: String, storeId: String): Unit
```

**Function:** Deletes the specified distributed key-value database based on the storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the database caller. |
| storeId | String | Yes | - | Unique identifier of the database to be deleted, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Parameter verification failed. |
  | 15100004 | Not found. |

### func getAllKVStoreId(String)

```cangjie
public func getAllKVStoreId(appId: String): Array<String>
```

**Function:** Retrieves the storeIds of all created distributed key-value databases that have not been deleted via [deleteKVStore](#func-deletekvstorestring-string).

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| appId | String | Yes | - | Package name of the database caller. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns the storeIds of all created distributed key-value databases. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Parameter verification failed. |

### func getKVStore\<T>(String, Options) where T \<: SingleKVStore

```cangjie
public func getKVStore<T>(storeId: String, options: Options): T where T <: SingleKVStore
```

**Function:** Creates and retrieves a distributed key-value database by specifying Options and storeId.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| storeId | String | Yes | - | Unique identifier of the database, with a length not exceeding [MAX_STORE_ID_LENGTH](#static-let-max_store_id_length). |
| options | [Options](#class-options) | Yes | - | Configuration information for creating a distributed key-value instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| T | KVStore object. A single-version distributed key-value database that does not distinguish between data sources, providing methods for querying and synchronizing data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Database Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100002 | Open an existing database with changed options. |
  | 15100003 | Database corrupted. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported yet. | todo | todo |

## class KVManagerConfig

```cangjie
public class KVManagerConfig {
    public var context: BaseContext
    public var bundleName: String

    public init(context: BaseContext, bundleName: String)
}
```

**Function:** Provides configuration information for the KVManager instance, including the caller's package name and application context.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var bundleName

```cangjie
public var bundleName: String
```

**Function:** Caller's package name.

**Type:** String

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var context

```cangjie
public var context: BaseContext
```

**Function:** Application context.

**Type:** [BaseContext](../AbilityKit/cj-apis-app-ability.md#class-basecontext)

**Read-Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### init(BaseContext, String)

```cangjie
public init(context: BaseContext, bundleName: String)
```

**Function:** Constructor for creating a KVManagerConfig instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [BaseContext](../AbilityKit/cj-apis-app-ability.md#class-basecontext) | Yes | - | Application context. |
| bundleName | String | Yes | - | Caller's package name. |

## class KVStoreResultSet

```cangjie
public class KVStoreResultSet {}
```

**Function:** Provides methods for obtaining database result sets, including querying and moving data read positions. The maximum number of open result sets is 8.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### func getCount()

```cangjie
public func getCount(): Int32
```

**Function:** Retrieves the total number of rows in the result set.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the total number of rows of data. |## class Options

```cangjie
public class Options {
    public var createIfMissing: Bool
    public var encrypt: Bool
    public var backup: Bool
    public var autoSync: Bool
    public var securityLevel: SecurityLevel
    public var schema:?Schema

    public init(securityLevel: SecurityLevel, createIfMissing!: Bool = true, encrypt!: Bool = false,
        backup!: Bool = true, autoSync!: Bool = false, schema!: ?Schema = None)
}
```

**Description:** Provides configuration information for database creation.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var autoSync

```cangjie
public var autoSync: Bool
```

**Description:** Sets whether database files are automatically synchronized. Default is false (manual synchronization).

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var backup

```cangjie
public var backup: Bool
```

**Description:** Sets whether database files are backed up. Default is true (backup enabled).

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var createIfMissing

```cangjie
public var createIfMissing: Bool
```

**Description:** Determines whether to create a database if the file doesn't exist. Default is true (create if missing).

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var encrypt

```cangjie
public var encrypt: Bool
```

**Description:** Sets whether database files are encrypted. Default is false (no encryption).

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### var schema

```cangjie
public var schema:?Schema
```

**Description:** Schema()|Defines the structure of values stored in the database. Default is undefined (no Schema used).

**Type:** ?[Schema](#class-schema)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var securityLevel

```cangjie
public var securityLevel: SecurityLevel
```

**Description:** Sets the security level of the database.

**Type:** [SecurityLevel](#enum-securitylevel)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### init(SecurityLevel, Bool, Bool, Bool, Bool, ?Schema)

```cangjie
public init(securityLevel: SecurityLevel, createIfMissing!: Bool = true, encrypt!: Bool = false,
    backup!: Bool = true, autoSync!: Bool = false, schema!: ?Schema = None)
```

**Description:** Constructor for creating a KVOptions instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| securityLevel | [SecurityLevel](#enum-securitylevel) | Yes | - | Sets the security level of the database.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| createIfMissing | Bool | No | true | Determines whether to create a database if the file doesn't exist. Default is true.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| encrypt | Bool | No | false | Sets whether database files are encrypted. Default is false.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| backup | Bool | No | true | Sets whether database files are backed up. Default is true.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core |
| autoSync | Bool | No | false | Sets whether database files are automatically synchronized. Default is false.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core<br>**Required Permission:** ohos.permission.DISTRIBUTED_DATASYNC |
| schema | ?[Schema](#class-schema) | No | None | Defines the structure of values stored in the database. Default is undefined.<br>**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore |

## class Query

```cangjie
public class Query {
    public init()
}
```

**Description:** Represents database queries using predicates, providing methods to create Query instances, query data, and add predicates. A Query object can contain up to 256 predicates.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### init()

```cangjie
public init()
```

**Description:** Constructor for creating a Query instance.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

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

**Description:** Represents database schemas. Schema objects can be created and placed in [KVOptions](#class-options) when creating or opening a database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var indexes

```cangjie
public var indexes: Array<String>
```

**Description:** Represents an array of JSON-type strings.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var mode

```cangjie
public var mode: Int32
```

**Description:** Represents the mode of the Schema.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var root

```cangjie
public var root: FieldNode
```

**Description:** Represents the root object of JSON.

**Type:** [FieldNode](#class-fieldnode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### var skip

```cangjie
public var skip: Int32
```

**Description:** The skip size of the Schema.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

### init(FieldNode, Array\<String>, Int32, Int32)

```cangjie
public init(root: FieldNode, indexes: Array<String>, mode: Int32, skip: Int32)
```

**Description:** Represents database schemas. Schema objects can be created and placed in [KVOptions](#class-options) when creating or opening a database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.DistributedKVStore

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| root | [FieldNode](#class-fieldnode) | Yes | - | Represents the root object of JSON. |
| indexes | Array\<String> | Yes | - | Represents an array of JSON-type strings. |
| mode | Int32 | Yes | - | Represents the mode of the Schema. |
| skip | Int32 | Yes | - | The skip size of the Schema. |

## class SingleKVStore

```cangjie
public open class SingleKVStore {}
```

**Description:** SingleKVStore database instance, providing methods to add, delete, and subscribe to data changes, as well as subscribe to data synchronization completion.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### func backup(String)

```cangjie
public open func backup(file: String): Unit
```

**Description:** Backs up the database with the specified name.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| file | String | Yes | - | The specified name for the backup file. Cannot be empty and must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Parameter verification failed. |
  | 15100005 | Database or result set already closed. |

### func commit()

```cangjie
public open func commit(): Unit
```

**Description:** Commits a transaction in the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 15100005 | Database or result set already closed. |

### func delete(String)

```cangjie
public open func delete(key: String): Unit
```

**Description:** Deletes data with the specified key from the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| key | String | Yes | - | The key of the data to be deleted. Cannot be empty and must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func deleteBatch(Array\<String>)

```cangjie
public open func deleteBatch(keys: Array<String>): Unit
```

**Description:** Batch deletes key-value pairs from the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| keys | Array\<String> | Yes | - | The keys of the key-value pairs to be batch deleted. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func enableSync(Bool)

```cangjie
public open func enableSync(enabled: Bool): Unit
```

**Description:** Sets whether synchronization is enabled.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| enabled | Bool | Yes | - | Determines whether synchronization is enabled. true enables synchronization, false disables it. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types. |

### func get(String)

```cangjie
public open func get(key: String): ValueType
```

**Description:** Retrieves the value associated with the specified key.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| key | String | Yes | - | The key of the data to be queried. Cannot be empty and must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ValueType](#enum-valuetype) | Returns the queried value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md) and [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100003 | Database corrupted. |
  | 15100004 | Not found. |
  | 15100005 | Database or result set already closed. |

### func put(String, ValueType)

```cangjie
public open func put(key: String, value: ValueType): Unit
```

**Description:** Adds a key-value pair of the specified type to the database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| key | String | Yes | - | The key of the data to be added. Cannot be empty and must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |
| value | [ValueType](#enum-valuetype) | Yes | - | The value of the data to be added. Supports Array\<UInt8>, String, Int32, Bool, Float32, Float64. The length of Array\<UInt8> and String must not exceed [MAX_VALUE_LENGTH](#static-let-max_value_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func putBatch(Array\<Entry>)

```cangjie
public open func putBatch(entries: Array<Entry>): Unit
```

**Description:** Batch inserts key-value pairs into the SingleKVStore database.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| entries | Array\<[Entry](#class-entry)> | Yes | - | The key-value pairs to be batch inserted. The maximum data size for an entries object is 512M. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are unspecified; 2. Incorrect parameter types. |
  | 15100003 | Database corrupted. |
  | 15100005 | Database or result set already closed. |

### func restore(String)

```cangjie
public open func restore(file: String): Unit
```

**Description:** Restores the database from the specified database file.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| file | String | Yes | - | The specified database file name. Cannot be empty and must not exceed [MAX_KEY_LENGTH](#static-let-max_key_length). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. See [Distributed Key-Value Store Error Codes](./cj-errorcode-distributed_kv_store.md) and## enum SecurityLevel

```cangjie
public enum SecurityLevel {
    | S1
    | S2
    | S3
    | S4
    | ...
}
```

**Function:** Enumeration of database security levels.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### S1

```cangjie
S1
```

**Function:** Indicates the database security level is low. Data leakage, tampering, destruction, or loss may cause limited adverse impacts on individuals or organizations. Examples include gender, nationality, user application records, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### S2

```cangjie
S2
```

**Function:** Indicates the database security level is medium. Data leakage, tampering, destruction, or loss may cause serious adverse impacts on individuals or organizations. Examples include detailed personal communication addresses, names/nicknames, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### S3

```cangjie
S3
```

**Function:** Indicates the database security level is high. Data leakage, tampering, destruction, or loss may cause severe adverse impacts on individuals or organizations. Examples include real-time precise location information, movement trajectories, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### S4

```cangjie
S4
```

**Function:** Indicates the database security level is critical, covering special data types defined by industry laws and regulations that involve the most private information of individuals. Any leakage, tampering, destruction, or loss may cause significant adverse impacts on individuals or organizations. Examples include political views, religion, philosophical beliefs, trade union membership, genetic data, biometric information, health and sexual life status, sexual orientation, device authentication credentials, personal credit card/financial information, etc.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

## enum ValueType

```cangjie
public enum ValueType {
    | StringValue(String)
    | Integer(Int32)
    | Float(Float32)
    | ByteArray(Array<Byte>)
    | Boolean(Bool)
    | Double(Float64)
    | ...
}
```

**Function:** Enumeration of data types.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### Boolean(Bool)

```cangjie
Boolean(Bool)
```

**Function:** Indicates the value type is boolean.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### ByteArray(Array\<Byte>)

```cangjie
ByteArray(Array<Byte>)
```

**Function:** Indicates the value type is byte array.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### Double(Float64)

```cangjie
Double(Float64)
```

**Function:** Indicates the value type is Float64 floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### Float(Float32)

```cangjie
Float(Float32)
```

**Function:** Indicates the value type is Float32 floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### Integer(Int32)

```cangjie
Integer(Int32)
```

**Function:** Indicates the value type is Int32 integer.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** Indicates the value type is string.

**System Capability:** SystemCapability.DistributedDataManager.KVStore.Core

**Since:** 21