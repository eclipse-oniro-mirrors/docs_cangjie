# ohos.data.relational_store

A Relational Database (RDB) is a database that manages data based on the relational model. Built upon the SQLite component, the relational database provides a comprehensive mechanism for managing local databases. It offers a series of interfaces for operations such as insert, delete, update, and query, and can also directly execute user-input SQL statements to meet complex scenario requirements. Worker threads are not supported.

Basic data types supported on the Cangjie side: Int64, Float64, String, binary data, Bool. To ensure successful data insertion and retrieval, it is recommended that a single piece of data does not exceed 2MB. Data exceeding this size may be inserted successfully but fail to be read.

This module provides the following common functionalities related to relational databases:

- [RdbPredicates](#class-rdbpredicates): Terms used in the database to represent the properties, characteristics of data entities, or relationships between data entities, primarily used to define database operation conditions.
- [RdbStore](#class-rdbstore): An interface that provides methods for managing relational databases (RDB).
- [ResultSet](#class-resultset): The result set returned after users call relational database query interfaces.

## Import Module

```cangjie
import kit.ArkData.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

## Usage Guidelines

API example code usage guidelines:

- If the first line of the example code has a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details on the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#仓颉示例代码说明).

## func deleteRdbStore(UIAbilityContext, String)

```cangjie
public func deleteRdbStore(context: UIAbilityContext, name: String): Unit
```

**Function:** Deletes a database using the specified database file configuration. After successful deletion, it is recommended to set the database object to None. If a custom path is configured in [StoreConfig](#class-storeconfig) when creating the database, calling this interface for deletion will be ineffective, and the [deleteRdbStore(UIAbilityContext, StoreConfig)](#func-deleterdbstoreuiabilitycontext-storeconfig) interface must be used instead.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The context of the application. |
| name | String | Yes | - | The name of the database. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800010 | Failed to open or delete the database by an invalid database path. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

## func deleteRdbStore(UIAbilityContext, StoreConfig)

```cangjie
public func deleteRdbStore(context: UIAbilityContext, config: StoreConfig): Unit
```

**Function:** Deletes a database using the specified database file configuration. After successful deletion, it is recommended to set the database object to None. If the database file is in the public sandbox directory, this interface must be used for deletion. When multiple processes operate on the same database, it is recommended to send a database deletion notification to other processes to make them aware and handle it. If a custom path is configured in [StoreConfig](#class-storeconfig) when creating the database, this interface must be called for deletion.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The context of the application. |
| config | [StoreConfig](#class-storeconfig) | Yes | - | The database configuration related to this RDB store. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800010 | Failed to open or delete the database by an invalid database path. |
  | 14801001 | The operation is supported in the stage model only. |
  | 14801002 | Invalid data group ID. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

## func getRdbStore(UIAbilityContext, StoreConfig)

```cangjie
public func getRdbStore(context: UIAbilityContext, config: StoreConfig): RdbStore
```

**Function:** Obtains a related RdbStore to operate the relational database. Users can configure RdbStore parameters according to their needs and then call RdbStore interfaces to perform related data operations.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The context of the application. |
| config | [StoreConfig](#class-storeconfig) | Yes | - | The database configuration related to this RDB store. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbStore](#class-rdbstore) | Returns the RdbStore object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 14800000 | Inner error. |
  | 14800010 | Failed to open or delete the database by an invalid database path. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14801001 | The operation is supported in the stage model only. |
  | 14801002 | Invalid data group ID. |
  | 14800017 | StoreConfig is changed. |
  | 14800020 | The secret key is corrupted or lost. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

## class Asset

```cangjie
public class Asset {
    public var name: String
    public var uri: String
    public var path: String
    public var createTime: String
    public var modifyTime: String
    public var size: String
    public var status: AssetStatus

    public init(name: String, uri: String, path: String, createTime: String, modifyTime: String, size: String,
        status!: AssetStatus = AssetStatus.AssetNormal)
}
```

**Function:** Records information related to asset attachments (files, images, videos, etc.). Related interfaces for asset types do not currently support Datashare.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var createTime

```cangjie
public var createTime: String
```

**Function:** The time when the asset was created.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var modifyTime

```cangjie
public var modifyTime: String
```

**Function:** The last time the asset was modified.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var name

```cangjie
public var name: String
```

**Function:** The name of the asset.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var path

```cangjie
public var path: String
```

**Function:** The path of the asset in the application sandbox.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var size

```cangjie
public var size: String
```

**Function:** The size of the space occupied by the asset.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var status

```cangjie
public var status: AssetStatus
```

**Function:** The status of the asset, with a default value of ASSET_NORMAL.

**Type:** [AssetStatus](#enum-assetstatus)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var uri

```cangjie
public var uri: String
```

**Function:** The URI of the asset, representing its absolute path in the system.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### init(String, String, String, String, String, String, AssetStatus)

```cangjie
public init(name: String, uri: String, path: String, createTime: String, modifyTime: String, size: String,
    status!: AssetStatus = AssetStatus.AssetNormal)
```

**Function:** Constructs an Asset.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the asset. |
| uri | String | Yes | - | The URI of the asset, representing its absolute path in the system. |
| path | String | Yes | - | The path of the asset in the application sandbox. |
| createTime | String | Yes | - | The time when the asset was created. |
| modifyTime | String | Yes | - | The last time the asset was modified. |
| size | String | Yes | - | The size of the space occupied by the asset. |
| status | [AssetStatus](#enum-assetstatus) | No | AssetStatus.AssetNormal | **Named parameter.** The status of the asset, with a default value of ASSET_NORMAL. |

## class CryptoParam

```cangjie
public class CryptoParam {
    public var encryptionKey: Array<UInt8>
    public var iterationCount: Int32
    public var encryptionAlgo: EncryptionAlgo
    public var hmacAlgo: HmacAlgo
    public var kdfAlgo:?KdfAlgo
    public var cryptoPageSize: UInt32

    public init(encryptionKey: Array<UInt8>, iterationCount!: Int32 = 10000,
        encryptionAlgo!: EncryptionAlgo = EncryptionAlgo.Aes256Gcm,
        hmacAlgo!: HmacAlgo = HmacAlgo.Sha256, kdfAlgo!: ?KdfAlgo = None,
        cryptoPageSize!: UInt32 = 1024)
}
```

**Function:** Configuration parameters for database encryption. This configuration is only effective when the encrypt option in StoreConfig is set to true.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var cryptoPageSize

```cangjie
public var cryptoPageSize: UInt32
```

**Function:** An integer type specifying the page size used for database encryption and decryption.

**Type:** UInt32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var encryptionAlgo

```cangjie
public var encryptionAlgo: EncryptionAlgo
```

**Function:** Specifies the encryption algorithm used for database encryption and decryption.

**Type:** [EncryptionAlgo](#enum-encryptionalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var encryptionKey

```cangjie
public var encryptionKey: Array<UInt8>
```

**Function:** Specifies the key used for database encryption and decryption.

**Type:** Array\<UInt8>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var hmacAlgo

```cangjie
public var hmacAlgo: HmacAlgo
```

**Function:** Specifies the HMAC algorithm used for database encryption and decryption.

**Type:** [HmacAlgo](#enum-hmacalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var iterationCount

```cangjie
public var iterationCount: Int32
```

**Function:** An integer type specifying the iteration count for the PBKDF2 algorithm used in the database, with a default value of 10000.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### var kdfAlgo

```cangjie
public var kdfAlgo:?KdfAlgo
```

**Function:** Specifies the PBKDF2 algorithm used for database encryption and decryption.

**Type:** ?[KdfAlgo](#enum-kdfalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

### init(Array\<UInt8>, Int32, EncryptionAlgo, HmacAlgo, ?KdfAlgo, UInt32)

```cangjie
public init(encryptionKey: Array<UInt8>, iterationCount!: Int32 = 10000,
    encryptionAlgo!: EncryptionAlgo = EncryptionAlgo.Aes256Gcm,
    hmacAlgo!: HmacAlgo = HmacAlgo.Sha256, kdfAlgo!: ?KdfAlgo = None,
    cryptoPageSize!: UInt32 = 1024)
```

**Function:** Constructor for the CryptoParam class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| encryptionKey | Array\<UInt8> | Yes | - | Specifies the key used for database encryption and decryption. If an empty key is passed, the database will generate and save the key, and use the generated key to open the database file. After use, the user must set all key contents to zero. |
| iterationCount | Int32 | No | 10000 | An integer type specifying the iteration count for the PBKDF2 algorithm used in the database, with a default value of 10000. The iteration count should be a positive integer; if not, it will be rounded down. If this parameter is not specified or is set to zero, the default value of 10000 will be used, along with the default encryption algorithm AES_256_GCM. |
| encryptionAlgo | [EncryptionAlgo](#enum-encryptionalgo) | No | EncryptionAlgo.Aes256Gcm |## class RdbPredicates

```cangjie
public class RdbPredicates {

    public init(name: String)
}
```

**Description:** Represents predicates for relational databases (RDB). This class determines whether the value of a conditional expression in an RDB is true or false. This type is not thread-safe. If there are multi-thread operations on instances derived from this class in the application, ensure proper locking protection.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### init(String)

```cangjie
public init(name: String)
```

**Description:** Constructor for the RdbPredicates class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description          |
| :--------| :----- | :-------- | :------ | :------------------- |
| name     | String | Yes       | -       | Name of the database table. |

### func inValues(String, Array\<ValueType>)

```cangjie
public func inValues(field: String, value: Array<ValueType>): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table falls within the given range.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type                  | Mandatory | Default | Description                                      |
| :--------| :-------------------- | :-------- | :------ | :----------------------------------------------- |
| field    | String                | Yes       | -       | Column name in the database table.               |
| value    | Array\<[ValueType](#enum-valuetype)> | Yes       | -       | Values to match, specified as an array of RelationalStoreValueType. |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func and()

```cangjie
public func and(): RdbPredicates
```

**Description:** Adds an AND condition to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RDB predicate with the AND condition. |

### func beginWrap()

```cangjie
public func beginWrap(): RdbPredicates
```

**Description:** Adds a left parenthesis to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RDB predicate with the left parenthesis. |

### func beginsWith(String, String)

```cangjie
public func beginsWith(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table starts with `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                                      |
| :--------| :----- | :-------- | :------ | :----------------------------------------------- |
| field    | String | Yes       | -       | Column name in the database table.               |
| value    | String | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func between(String, ValueType, ValueType)

```cangjie
public func between(field: String, low: ValueType, high: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table falls within the given range (inclusive of boundaries).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type                  | Mandatory | Default | Description                                      |
| :--------| :-------------------- | :-------- | :------ | :----------------------------------------------- |
| field    | String                | Yes       | -       | Column name in the database table.               |
| low      | [ValueType](#enum-valuetype) | Yes       | -       | Minimum value to match with the predicate.       |
| high     | [ValueType](#enum-valuetype) | Yes       | -       | Maximum value to match with the predicate.       |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func contains(String, String)

```cangjie
public func contains(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table contains `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                                      |
| :--------| :----- | :-------- | :------ | :----------------------------------------------- |
| field    | String | Yes       | -       | Column name in the database table.               |
| value    | String | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func distinct()

```cangjie
public func distinct(): RdbPredicates
```

**Description:** Configures the predicate to filter duplicate records and retain only one of them.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate for filtering duplicate records. |

### func endWrap()

```cangjie
public func endWrap(): RdbPredicates
```

**Description:** Adds a right parenthesis to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RDB predicate with the right parenthesis. |

### func endsWith(String, String)

```cangjie
public func endsWith(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table ends with `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                                      |
| :--------| :----- | :-------- | :------ | :----------------------------------------------- |
| field    | String | Yes       | -       | Column name in the database table.               |
| value    | String | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func equalTo(String, ValueType)

```cangjie
public func equalTo(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table equals `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type                  | Mandatory | Default | Description                                      |
| :--------| :-------------------- | :-------- | :------ | :----------------------------------------------- |
| field    | String                | Yes       | -       | Column name in the database table.               |
| value    | [ValueType](#enum-valuetype) | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func glob(String, String)

```cangjie
public func glob(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match the specified field where the data field equals `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                                      |
| :--------| :----- | :-------- | :------ | :----------------------------------------------- |
| field    | String | Yes       | -       | Column name in the database table.               |
| value    | String | Yes       | -       | Value to match with the predicate.<br>Wildcards are supported: `*` represents 0, 1, or multiple digits or characters; `?` represents 1 digit or character. |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func greaterThan(String, ValueType)

```cangjie
public func greaterThan(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table is greater than `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type                  | Mandatory | Default | Description                                      |
| :--------| :-------------------- | :-------- | :------ | :----------------------------------------------- |
| field    | String                | Yes       | -       | Column name in the database table.               |
| value    | [ValueType](#enum-valuetype) | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func greaterThanOrEqualTo(String, ValueType)

```cangjie
public func greaterThanOrEqualTo(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the specified column `field` of the data table is greater than or equal to `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type                  | Mandatory | Default | Description                                      |
| :--------| :-------------------- | :-------- | :------ | :----------------------------------------------- |
| field    | String                | Yes       | -       | Column name in the database table.               |
| value    | [ValueType](#enum-valuetype) | Yes       | -       | Value to match with the predicate.               |

**Return Value:**

| Type                  | Description                                  |
| :-------------------- | :------------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :------------ | :------------ |
  | 401           | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |### func groupBy(Array\<String>)

```cangjie

public func groupBy(fields: Array<String>): RdbPredicates
```

**Description:** Configures the predicate to group query results by specified columns.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fields | Array\<String> | Yes | - | Column names on which grouping depends. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate for grouping query columns. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func inAllDevices()

```cangjie

public func inAllDevices(): RdbPredicates
```

**Description:** Connects to all remote devices in the network when synchronizing distributed databases.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

### func isNotNull(String)

```cangjie

public func isNotNull(field: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is not null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func isNull(String)

```cangjie

public func isNull(field: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func lessThan(String, ValueType)

```cangjie

public func lessThan(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is less than `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | [ValueType](#enum-valuetype) | Yes | - | Value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func lessThanOrEqualTo(String, ValueType)

```cangjie

public func lessThanOrEqualTo(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is less than or equal to `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | [ValueType](#enum-valuetype) | Yes | - | Value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func like(String, String)

```cangjie

public func like(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is similar to `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | String | Yes | - | Value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func limitAs(Int32)

```cangjie

public func limitAs(value: Int32): RdbPredicates
```

**Description:** Sets the predicate for the maximum number of data records.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | Maximum number of data records. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate that can be used to set the maximum number of data records. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func notBetween(String, ValueType, ValueType)

```cangjie

public func notBetween(field: String, low: ValueType, high: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table falls outside the given range (excluding the range boundaries).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| low | [ValueType](#enum-valuetype) | Yes | - | Minimum value to match with the predicate. |
| high | [ValueType](#enum-valuetype) | Yes | - | Maximum value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func notEqualTo(String, ValueType)

```cangjie

public func notEqualTo(field: String, value: ValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is not equal to `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | [ValueType](#enum-valuetype) | Yes | - | Value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func notInValues(String, Array\<ValueType>)

```cangjie

public func notInValues(field: String, value: Array<ValueType>): RdbPredicates
```

**Description:** Configures the predicate to match fields where the value in the `field` column of the data table is not in the specified range of `ValueType`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | Array\<[ValueType](#enum-valuetype)> | Yes | - | Values to match with the predicate, specified as an array of `ValueType`. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func offsetAs(Int32)

```cangjie

public func offsetAs(rowOffset: Int32): RdbPredicates
```

**Description:** Configures the predicate to specify the starting position of the returned results. This method must be used together with [limitAs](#func-limitasint32).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| rowOffset | Int32 | Yes | - | Starting position of the returned results, which must be a positive integer. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate with the specified starting position for returned results. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func or()

```cangjie

public func or(): RdbPredicates
```

**Description:** Adds an OR condition to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the Rdb predicate with the OR condition. |

### func orderByAsc(String)

```cangjie

public func orderByAsc(field: String): RdbPredicates
```

**Description:** Configures the predicate to sort the values in the `field` column of the data table in ascending order.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |

### func orderByDesc(String)

```cangjie

public func orderByDesc(field: String): RdbPredicates
```

**Description:** Configures the predicate to sort the values in the `field` column of the data table in descending order.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Column name in the database table. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types. |## class RdbStore

```cangjie
public class RdbStore {}
```

**Description:** Provides interfaces for managing relational databases (RDB).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### func backup(String)

```cangjie
public func backup(destName: String): Unit
```

**Description:** Backs up the database with a specified name.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| destName | String | Yes | - | Specifies the backup file name of the database. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func batchInsert(String, Array\<ValuesBucket>)

```cangjie
public func batchInsert(table: String, values: Array<ValuesBucket>): Int64
```

**Description:** Inserts a set of data into the specified table.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| table | String | Yes | - | Specifies the name of the target table. |
| values | Array\<[ValuesBucket](#type-valuesbucket)> | Yes | - | Represents the set of data to be inserted into the table. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | If the operation is successful, returns the number of inserted data rows; otherwise, returns -1. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func beginTransaction()

```cangjie
public func beginTransaction(): Unit
```

**Description:** Starts a transaction before executing SQL statements. This interface does not support multi-process or multi-thread usage.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. The store must not be nullptr. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func commit()

```cangjie
public func commit(): Unit
```

**Description:** Commits the executed SQL statements. This interface does not support multi-process or multi-thread usage.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. The store must not be nullptr. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func delete(RdbPredicates)

```cangjie
public func delete(predicates: RdbPredicates): Int64
```

**Description:** Deletes data from the database based on the specified RdbPredicates conditions.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| predicates | [RdbPredicates](#class-rdbpredicates) | Yes | - | Specifies the deletion conditions defined by the RdbPredicates instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Number of affected rows. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func emit(String)

```cangjie
public func emit(event: String): Unit
```

**Description:** Notifies the inter-process or intra-process listeners registered via [on](#func-onstring-bool-callback0argument).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | String | Yes | - | Specifies the name of the event to notify. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800050 | Failed to obtain the subscription service. |

### func executeSql(String, Array\<ValueType>)

```cangjie
public func executeSql(sql: String, bindArgs!: Array<ValueType> = []): Unit
```

**Description:** Executes an SQL statement with specified parameters that does not return a value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| sql | String | Yes | - | Specifies the SQL statement to execute. |
| bindArgs | Array\<[ValueType](#enum-valuetype)> | No | [] | Specifies the parameter values for the SQL statement, corresponding to the placeholders in the SQL statement. If the SQL statement is complete, this parameter can be omitted. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 801 | Capability not supported the sql(attach,begin,commit,rollback etc.). |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |
  | 14800047 | The WAL file size exceeds the default limit. |

### func insert(String, ValuesBucket, ConflictResolution)

```cangjie
public func insert(table: String, values: ValuesBucket,
    conflict!: ConflictResolution = ConflictResolution.OnConflictNone): Int64
```

**Description:** Inserts a row of data into the specified table.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| table | String | Yes | - | Specifies the name of the target table. |
| values | [ValuesBucket](#type-valuesbucket) | Yes | - | Represents the row of data to be inserted into the table. |
| conflict | [ConflictResolution](#enum-conflictresolution) | No | ConflictResolution.OnConflictNone | Specifies the conflict resolution strategy. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | If the operation is successful, returns the row ID; otherwise, returns -1. |

**Exceptions:**

- BusinessException: The error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029## class ResultSet

```cangjie
public class ResultSet {}
```

**Description:** Provides methods for accessing database result sets generated by queries. A result set refers to the collection of results returned after a user calls a relational database query interface, offering various flexible data access methods for users to retrieve data items.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop columnCount

```cangjie
public prop columnCount: Int32
```

**Description:** Gets the number of columns in the result set.

**Type:** Int32

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop columnNames

```cangjie
public prop columnNames: Array<String>
```

**Description:** Gets the names of all columns in the result set.

**Type:** Array\<String>

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop isAtFirstRow

```cangjie
public prop isAtFirstRow: Bool
```

**Description:** Checks whether the result set is positioned at the first row.

**Type:** Bool

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop isAtLastRow

```cangjie
public prop isAtLastRow: Bool
```

**Description:** Checks whether the result set is positioned at the last row.

**Type:** Bool

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop isClosed

```cangjie
public prop isClosed: Bool
```

**Description:** Checks whether the current result set is closed.

**Type:** Bool

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop isEnded

```cangjie
public prop isEnded: Bool
```

**Description:** Checks whether the result set is positioned after the last row.

**Type:** Bool

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop isStarted

```cangjie
public prop isStarted: Bool
```

**Description:** Checks whether the cursor has moved.

**Type:** Bool

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop rowCount

```cangjie
public prop rowCount: Int32
```

**Description:** Gets the number of rows in the result set.

**Type:** Int32

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### prop rowIndex

```cangjie
public prop rowIndex: Int32
```

**Description:** Gets the index of the current row in the result set.

**Type:** Int32

**Read-Write Attribute:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### func close()

```cangjie

public func close(): Unit
```

**Description:** Closes the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error.|
  | 14800012 | ResultSet is empty or pointer index is out of bounds.|

### func getAsset(Int32)

```cangjie

public func getAsset(columnIndex: Int32): Asset
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [Asset](#class-asset) | Returns the value of the specified column as an Asset. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
  | 14800000 | Inner error.|
  | 14800011 | Failed to open the database because it is corrupted.|
  | 14800012 | ResultSet is empty or pointer index is out of bounds.|
  | 14800013 | Resultset is empty or column index is out of bounds.|
  | 14800014 | The RdbStore or ResultSet is already closed.|
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist.|
  | 14800022 | SQLite: Callback routine requested an abort.|
  | 14800023 | SQLite: Access permission denied.|
  | 14800024 | SQLite: The database file is locked.|
  | 14800025 | SQLite: A table in the database is locked.|
  | 14800026 | SQLite: The database is out of memory.|
  | 14800027 | SQLite: Attempt to write a readonly database.|
  | 14800028 | SQLite: Some kind of disk I/O error occurred.|
  | 14800029 | SQLite: The database is full.|
  | 14800030 | SQLite: Unable to open the database file.|
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit.|
  | 14800032 | SQLite: Abort due to constraint violation.|
  | 14800033 | SQLite: Data type mismatch.|
  | 14800034 | SQLite: Library used incorrectly.|

### func getAssets(Int32)

```cangjie

public func getAssets(columnIndex: Int32): Assets
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DDistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Assets | Returns the value of the specified column as an Array\<[Asset](#class-asset)>. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
  | 14800000 | Inner error.|
  | 14800011 | Failed to open the database because it is corrupted.|
  | 14800012 | ResultSet is empty or pointer index is out of bounds.|
  | 14800013 | Resultset is empty or column index is out of bounds.|
  | 14800014 | The RdbStore or ResultSet is already closed.|
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist.|
  | 14800022 | SQLite: Callback routine requested an abort.|
  | 14800023 | SQLite: Access permission denied.|
  | 14800024 | SQLite: The database file is locked.|
  | 14800025 | SQLite: A table in the database is locked.|
  | 14800026 | SQLite: The database is out of memory.|
  | 14800027 | SQLite: Attempt to write a readonly database.|
  | 14800028 | SQLite: Some kind of disk I/O error occurred.|
  | 14800029 | SQLite: The database is full.|
  | 14800030 | SQLite: Unable to open the database file.|
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit.|
  | 14800032 | SQLite: Abort due to constraint violation.|
  | 14800033 | SQLite: Data type mismatch.|
  | 14800034 | SQLite: Library used incorrectly.|

### func getBlob(Int32)

```cangjie

public func getBlob(columnIndex: Int32): Array<UInt8>
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt8> | Returns the value of the specified column as a byte array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
  | 14800000 | Inner error.|
  | 14800011 | Failed to open the database because it is corrupted.|
  | 14800012 | ResultSet is empty or pointer index is out of bounds.|
  | 14800013 | Resultset is empty or column index is out of bounds.|
  | 14800014 | The RdbStore or ResultSet is already closed.|
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist.|
  | 14800022 | SQLite: Callback routine requested an abort.|
  | 14800023 | SQLite: Access permission denied.|
  | 14800024 | SQLite: The database file is locked.|
  | 14800025 | SQLite: A table in the database is locked.|
  | 14800026 | SQLite: The database is out of memory.|
  | 14800027 | SQLite: Attempt to write a readonly database.|
  | 14800028 | SQLite: Some kind of disk I/O error occurred.|
  | 14800029 | SQLite: The database is full.|
  | 14800030 | SQLite: Unable to open the database file.|
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit.|
  | 14800032 | SQLite: Abort due to constraint violation.|
  | 14800033 | SQLite: Data type mismatch.|
  | 14800034 | SQLite: Library used incorrectly.|

### func getColumnIndex(String)

```cangjie

public func getColumnIndex(columnName: String): Int32
```

**Description:** Gets the column index based on the specified column name.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnName | String | Yes | - | Specifies the name of the column in the result set. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Returns the index of the specified column. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
  | 14800000 | Inner error.|
  | 14800011 | Failed to open the database because it is corrupted.|
  | 14800013 | Resultset is empty or column index is out of bounds.|
  | 14800014 | The RdbStore or ResultSet is already closed.|
  | 14800019 | The SQL must be a query statement.|
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist.|
  | 14800022 | SQLite: Callback routine requested an abort.|
  | 14800023 | SQLite: Access permission denied.|
  | 14800024 | SQLite: The database file is locked.|
  | 14800025 | SQLite: A table in the database is locked.|
  | 14800026 | SQLite: The database is out of memory.|
  | 14800027 | SQLite: Attempt to write a readonly database.|
  | 14800028 | SQLite: Some kind of disk I/O error occurred.|
  | 14800029 | SQLite: The database is full.|
  | 14800030 | SQLite: Unable to open the database file.|
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit.|
  | 14800032 | SQLite: Abort due to constraint violation.|
  | 14800033 | SQLite: Data type mismatch.|
  | 14800034 | SQLite: Library used incorrectly.|

### func getColumnName(Int32)

```cangjie

public func getColumnName(columnIndex: Int32): String
```

**Description:** Gets the column name based on the specified column index.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | Specifies the index of the column in the result set. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | Returns the name of the specified column. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types.|
  | 14800000 | Inner error.|
  | 14800011 | Failed to open the database because it is corrupted.|
  | 14800013 | Resultset is empty or column index is out of bounds.|
  | 14800014 | The RdbStore or ResultSet is already closed.|
  | 14800019 | The SQL must be a query statement.|
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist.|
  | 14800022 | SQLite: Callback routine requested an abort.|
  | 14800023 | SQLite: Access permission denied.|
  | 14800024 | SQLite: The database file is locked.|
  | 14800025 | SQLite: A table in the database is locked.|
  | 14800026 | SQLite: The database is out of memory.|
  | 14800027 | SQLite: Attempt to write a readonly database.|
  | 14800028 | SQLite: Some kind of disk I/O error occurred.|
  | 14800029 | SQLite: The database is full.|
  | 14800030 | SQLite: Unable to open the database file.|
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit.|
  | 14800032 | SQLite: Abort due to constraint violation.|
  | 14800033 | SQLite: Data type mismatch.|
  | 14800034 | SQLite: Library used incorrectly.|### func getDouble(Int32)

```cangjie

public func getDouble(columnIndex: Int32): Float64
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | Returns the value of the specified column as Float64. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func getLong(Int32)

```cangjie

public func getLong(columnIndex: Int32): Int64
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RRelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the value of the specified column as Int64.<br>This interface supports data range: Number.MIN_SAFE_INTEGER ~ Number.MAX_SAFE_INTEGER. If the value exceeds this range, it is recommended to use [getDouble](#func-getdoubleint32). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func getRow()

```cangjie

public func getRow(): ValuesBucket
```

**Function:** Gets the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [ValuesBucket](#type-valuesbucket) | Returns the value of the specified row. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func getString(Int32)

```cangjie

public func getString(columnIndex: Int32): String
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the value of the specified column as a string. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func goTo(Int32)

```cangjie

public func goTo(offset: Int32): Bool
```

**Function:** Moves the result set forward or backward to the specified row relative to its current position.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| offset | Int32 | Yes | - | Indicates the offset relative to the current position. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

### func goToFirstRow()

```cangjie

public func goToFirstRow(): Bool
```

**Function:** Moves to the first row of the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

### func goToLastRow()

```cangjie

public func goToLastRow(): Bool
```

**Function:** Moves to the last row of the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800019 | The SQL must be a query statement. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |

### func goToNextRow()

```cangjie

public func goToNextRow(): Bool
```

**Function:** Moves to the next row of the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

### func goToPreviousRow()

```cangjie

public func goToPreviousRow(): Bool
```

**Function:** Moves to the previous row of the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

### func goToRow(Int32)

```cangjie

public func goToRow(position: Int32): Bool
```

**Function:** Moves to the specified row of the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| position | Int32 | Yes | - | Specifies the position to move to. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise, returns false. |

### func isColumnNull(Int32)

```cangjie

public func isColumnNull(columnIndex: Int32): Bool
```

**Function:** Checks whether the value of the specified column in the current row is null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | Specified column index, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the value of the specified column in the current row is null; otherwise, returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types. |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800021 | SQLite: Generic error. Possible causes: Insert failed or the updated data does not exist. |
  | 14800022 | SQLite: Callback routine requested an abort. |
  | 14800023 | SQLite: Access permission denied. |
  | 14800024 | SQLite: The database file is locked. |
  | 14800025 | SQLite: A table in the database is locked. |
  | 14800026 | SQLite: The database is out of memory. |
  | 14800027 | SQLite: Attempt to write a readonly database. |
  | 14800028 | SQLite: Some kind of disk I/O error occurred. |
  | 14800029 | SQLite: The database is full. |
  | 14800030 | SQLite: Unable to open the database file. |
  | 14800031 | SQLite: TEXT or BLOB exceeds size limit. |
  | 14800032 | SQLite: Abort due to constraint violation. |
  | 14800033 | SQLite: Data type mismatch. |
  | 14800034 | SQLite: Library used incorrectly. |## class StoreConfig

```cangjie
public class StoreConfig {
    public var name: String
    public var securityLevel: SecurityLevel
    public var encrypt: Bool
    public var dataGroupId: String
    public var customDir: String
    public var rootDir: String
    public var autoCleanDirtyData: Bool
    public var allowRebuild: Bool
    public var isReadOnly: Bool
    public var pluginLibs: Array<String>
    public var cryptoParam: CryptoParam
    public var vector: Bool
    public var tokenizer: Tokenizer
    public var persist: Bool
    public var enableSemanticIndex: Bool

    public init(securityLevel: SecurityLevel, name!: String = "",
        encrypt!: Bool = false, dataGroupId!: String = "",
        customDir!: String = "", rootDir!: String = "",
        autoCleanDirtyData!: Bool = true, allowRebuild!: Bool = false,
        isReadOnly!: Bool = false, pluginLibs!: Array<String> = Array<String>(),
        cryptoParam!: CryptoParam, vector!: Bool = false,
        tokenizer!: Tokenizer = Tokenizer.NoneTokenizer, persist!: Bool = true,
        enableSemanticIndex!: Bool = false)
}
```

**Function:** Manages relational database configurations.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var allowRebuild

```cangjie
public var allowRebuild: Bool
```

**Function:** Specifies whether the database supports automatic deletion and recreation of empty databases/tables upon exceptions. Default is false (no deletion).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var autoCleanDirtyData

```cangjie
public var autoCleanDirtyData: Bool
```

**Function:** Specifies whether to automatically clean data synchronized from the cloud after deletion. true means automatic cleanup, false means manual cleanup (default is true). For cloud-device collaborative databases, this parameter determines whether the device automatically cleans up cloud-deleted data. Manual cleanup can be performed via the cleanDirtyData interface.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### var cryptoParam

```cangjie
public var cryptoParam: CryptoParam
```

**Function:** Specifies user-defined encryption parameters.

**Type:** [CryptoParam](#class-cryptoparam)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var customDir

```cangjie
public var customDir: String
```

**Function:** Custom database directory path.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var dataGroupId

```cangjie
public var dataGroupId: String
```

**Function:** Application group ID, which must be obtained from the application market.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var enableSemanticIndex

```cangjie
public var enableSemanticIndex: Bool
```

**Function:** Specifies whether to enable semantic indexing for the database. true enables it, false disables it (default is false).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var encrypt

```cangjie
public var encrypt: Bool
```

**Function:** Specifies whether the database is encrypted (default is false). true: encrypted. false: unencrypted.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var isReadOnly

```cangjie
public var isReadOnly: Bool
```

**Function:** Specifies whether the database is read-only (default is read-write).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var name

```cangjie
public var name: String
```

**Function:** Database filename.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var persist

```cangjie
public var persist: Bool
```

**Function:** Specifies whether the database requires persistence. true means persistent storage, false means in-memory database (default is true).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var pluginLibs

```cangjie
public var pluginLibs: Array<String>
```

**Function:** An array of dynamic library names containing capabilities like FTS (Full-Text Search).

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var rootDir

```cangjie
public var rootDir: String
```

**Function:** Specifies the root directory path for the database.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var securityLevel

```cangjie
public var securityLevel: SecurityLevel
```

**Function:** Sets the database security level.

**Type:** [SecurityLevel](#enum-securitylevel)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var tokenizer

```cangjie
public var tokenizer: Tokenizer
```

**Function:** Specifies which tokenizer to use in FTS scenarios.

**Type:** [Tokenizer](#enum-tokenizer)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### var vector

```cangjie
public var vector: Bool
```

**Function:** Specifies whether the database is a vector database. true means vector database, false means relational database (default is false).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### init(SecurityLevel, String, Bool, String, String, String, Bool, Bool, Bool, Array\<String>, CryptoParam, Bool, Tokenizer, Bool, Bool)

```cangjie
public init(securityLevel: SecurityLevel, name!: String = "",
    encrypt!: Bool = false, dataGroupId!: String = "",
    customDir!: String = "", rootDir!: String = "",
    autoCleanDirtyData!: Bool = true, allowRebuild!: Bool = false,
    isReadOnly!: Bool = false, pluginLibs!: Array<String> = Array<String>(),
    cryptoParam = CryptoParam([]), vector!: Bool = false,
    tokenizer!: Tokenizer = Tokenizer.NoneTokenizer, persist!: Bool = true,
    enableSemanticIndex!: Bool = false)
```

**Function:** Constructor for the StoreConfig class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| securityLevel | [SecurityLevel](#enum-securitylevel) | Yes | - | Sets the database security level.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| name | String | No | "" | Database filename.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| encrypt | Bool | No | false | **Named parameter.** Specifies whether the database is encrypted (default is false).<br/> true: encrypted.<br/> false: unencrypted.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| dataGroupId | String | No | "" | **Named parameter.** Application group ID, which must be obtained from the application market.<br/>**Model Constraint:** This property is only available in Stage model.<br/>Specifies creating an RdbStore instance in the sandbox path corresponding to this dataGroupId. If not provided, it defaults to the application's sandbox directory.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| customDir | String | No | "" | Custom database directory path.<br/>**Usage Constraint:** The database path size is limited to 128 bytes. Exceeding this limit will cause failure with an error.<br/>The database will be created in the following directory structure: context.databaseDir + "/rdb/" + customDir, where context.databaseDir is the application sandbox path, "/rdb/" indicates a relational database, and customDir is the custom path. If not provided, it defaults to the application's sandbox directory.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| rootDir | String | No | "" | Specifies the root directory path for the database.<br/>From API version 18, this optional parameter is supported. The database will be opened or deleted from: rootDir + "/" + customDir. Databases opened with this parameter are read-only; write operations will return error code 801. Ensure the database file exists and has read permissions, otherwise error code 14800010 will be returned.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| autoCleanDirtyData | Bool | No | true | **Named parameter.** Specifies whether to automatically clean data synchronized from the cloud after deletion (default is true).<br/>For cloud-device collaborative databases, this determines automatic cleanup of cloud-deleted data on the device. Manual cleanup can be done via cleanDirtyData.<br/>**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client |
| allowRebuild | Bool | No | false | Specifies whether the database supports automatic deletion and recreation upon exceptions (default is false).<br/>true: automatic deletion.<br/>false: no automatic deletion.<br/>Supported since API version 12.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| isReadOnly | Bool | No | false | Specifies whether the database is read-only (default is read-write).<br/>true: read-only (write operations return error code 801).<br/>false: read-write.<br/>Supported since API version 12.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| pluginLibs | Array\<String> | No | Array<String>() | Array of dynamic library names containing capabilities like FTS.<br/>**Usage Constraints:**<br/>1. Maximum of 16 library names; exceeding this will cause failure.<br/>2. Libraries must be in the application sandbox or system paths; loading failures will cause errors.<br/>3. Full paths are required for SQLite loading.<br/>Example: [context.bundleCodeDir + "/libs/arm64/" + libtokenizer.so]. If not provided, no libraries are loaded.<br/>4. Libraries must include all dependencies to avoid runtime errors.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| cryptoParam | [CryptoParam](#class-cryptoparam) | No | CryptoParam([]) | **Named parameter.** Specifies user-defined encryption parameters.<br/>If not provided, default encryption parameters are used (see CryptoParam defaults). Only effective when encrypt is true.<br/>Supported since API version 14.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| vector | Bool | No | false | Specifies whether the database is a vector database (default is false).<br/>Vector databases are suitable for high-dimensional vector data, while relational databases are for structured data.<br/>Ensure all RdbStore and ResultSet instances are closed before calling deleteRdbStore for vector databases.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| tokenizer | [Tokenizer](#enum-tokenizer) | No | Tokenizer.NoneTokenizer | Specifies the tokenizer for FTS scenarios.<br/>If not provided, FTS will not support Chinese or multilingual tokenization (English tokenization remains supported).<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| persist | Bool | No | true | Specifies database persistence (default is true).<br/>In-memory databases do not support encryption, backup, restore, cross-process access, or distributed capabilities. securityLevel is ignored.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| enableSemanticIndex | Bool | No | false | Specifies whether to enable semantic indexing (default is false).<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |

## enum AssetStatus

```cangjie
public enum AssetStatus {
    | AssetNormal
    | AssetInsert
    | AssetUpdate
    | AssetDelete
    | AssetAbnormal
    | AssetDownloading
    | ...
}
```

**Function:** Enumerates the status of asset attachments.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetAbnormal

```cangjie
AssetAbnormal
```

**Function:** Indicates abnormal asset status.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetDelete

```cangjie
AssetDelete
```

**Function:** Indicates the asset needs to be deleted from the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetDownloading

```cangjie
AssetDownloading
```

**Function:** Indicates the asset is being downloaded to the local device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetInsert

```cangjie
AssetInsert
```

**Function:** Indicates the asset needs to be inserted into the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetNormal

```cangjie
AssetNormal
```

**Function:** Indicates normal asset status.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetUpdate

```cangjie
AssetUpdate
```

**Function:** Indicates the asset needs to be updated in the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21## enum ChangeType

```cangjie
public enum ChangeType {
    | DataChange
    | AssetChange
    | ...
}
```

**Function:** Describes the type of data change.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetChange

```cangjie
AssetChange
```

**Function:** Indicates that an asset attachment has changed.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### DataChange

```cangjie
DataChange
```

**Function:** Indicates that data has changed.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum ConflictResolution

```cangjie
public enum ConflictResolution {
    | OnConflictNone
    | OnConflictRollback
    | OnConflictAbort
    | OnConflictFail
    | OnConflictIgnore
    | OnConflictReplace
    | ...
}
```

**Function:** Conflict resolution methods for insert and update operations.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictAbort

```cangjie
OnConflictAbort
```

**Function:** When a conflict occurs, aborts the current SQL statement and rolls back any changes made by it, while preserving changes from prior SQL statements in the same transaction and keeping the transaction active.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictFail

```cangjie
OnConflictFail
```

**Function:** When a conflict occurs, aborts the current SQL statement without rolling back its prior changes or terminating the transaction.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictIgnore

```cangjie
OnConflictIgnore
```

**Function:** When a conflict occurs, skips the row that violates constraints and continues processing subsequent rows in the SQL statement.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictNone

```cangjie
OnConflictNone
```

**Function:** When a conflict occurs, takes no action.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictReplace

```cangjie
OnConflictReplace
```

**Function:** When a conflict occurs, deletes pre-existing rows that caused constraint violations before inserting or updating the current row, then continues normal execution.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### OnConflictRollback

```cangjie
OnConflictRollback
```

**Function:** When a conflict occurs, aborts the SQL statement and rolls back the current transaction.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum DistributedType

```cangjie
public enum DistributedType {
    | DistributedDevice
    | DistributedCloud
    | ...
}
```

**Function:** Describes the distributed type of a table.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### DistributedCloud

```cangjie
DistributedCloud
```

**Function:** Indicates a database table distributed between devices and cloud.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### DistributedDevice

```cangjie
DistributedDevice
```

**Function:** Indicates a database table distributed across different devices.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum EncryptionAlgo

```cangjie
public enum EncryptionAlgo {
    | Aes256Gcm
    | Aes256Cbc
    | ...
}
```

**Function:** Enumeration of database encryption algorithms. Use enum names rather than values.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Aes256Cbc

```cangjie
Aes256Cbc
```

**Function:** AES_256_CBC encryption algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Aes256Gcm

```cangjie
Aes256Gcm
```

**Function:** AES_256_GCM encryption algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum Field

```cangjie
public enum Field {
    | CursorField
    | OriginField
    | DeletedFlagField
    | OwnerField
    | PrivilegeField
    | SharingResourceField
    | ...
}
```

**Function:** Special fields used for predicate query conditions.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### CursorField

```cangjie
CursorField
```

**Function:** Field name used for cursor lookup.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### DeletedFlagField

```cangjie
DeletedFlagField
```

**Function:** Field populated in result sets during cursor lookup, indicating whether cloud-deleted data has been cleaned locally. A value of false means data remains, true means cleaned.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### OriginField

```cangjie
OriginField
```

**Function:** Field name specifying data source during cursor lookup.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### OwnerField

```cangjie
OwnerField
```

**Function:** Field populated in shared table result sets, indicating the initiator of the shared record.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### PrivilegeField

```cangjie
PrivilegeField
```

**Function:** Field populated in shared table result sets, indicating permitted operation privileges for the shared record.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### SharingResourceField

```cangjie
SharingResourceField
```

**Function:** Field populated during data sharing lookups, identifying the shared resource marker.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

## enum HmacAlgo

```cangjie
public enum HmacAlgo {
    | Sha1
    | Sha256
    | Sha512
    | ...
}
```

**Function:** Enumeration of database HMAC algorithms.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Sha1

```cangjie
Sha1
```

**Function:** HMAC_SHA1 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Sha256

```cangjie
Sha256
```

**Function:** HMAC_SHA256 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Sha512

```cangjie
Sha512
```

**Function:** HMAC_SHA512 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum KdfAlgo

```cangjie
public enum KdfAlgo {
    | KdfSha1
    | KdfSha256
    | KdfSha512
    | ...
}
```

**Function:** Enumeration of database PBKDF2 algorithms.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### KdfSha1

```cangjie
KdfSha1
```

**Function:** PBKDF2_HMAC_SHA1 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### KdfSha256

```cangjie
KdfSha256
```

**Function:** PBKDF2_HMAC_SHA256 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### KdfSha512

```cangjie
KdfSha512
```

**Function:** PBKDF2_HMAC_SHA512 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21## enum Origin

```cangjie
public enum Origin {
    | Local
    | Cloud
    | Remote
    | ...
}
```

**Function:** Indicates the data source.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### Cloud

```cangjie
Cloud
```

**Function:** Represents data synchronized from the cloud.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### Local

```cangjie
Local
```

**Function:** Represents local data.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### Remote

```cangjie
Remote
```

**Function:** Represents data synchronized between devices.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

## enum Progress

```cangjie
public enum Progress {
    | SyncBegin
    | SyncInProgress
    | SyncFinish
    | ...
}
```

**Function:** Describes the device-cloud synchronization process.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncBegin

```cangjie
SyncBegin
```

**Function:** Indicates the start of the device-cloud synchronization process.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncFinish

```cangjie
SyncFinish
```

**Function:** Indicates the completion of the device-cloud synchronization process.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncInProgress

```cangjie
SyncInProgress
```

**Function:** Indicates that the device-cloud synchronization is in progress.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum SecurityLevel

```cangjie
public enum SecurityLevel {
    | S1
    | S2
    | S3
    | S4
    | ...
}
```

**Function:** Enumerates the security levels of databases.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### S1

```cangjie
S1
```

**Function:** Indicates a low security level for the database, where data leakage would have minor impact. For example, databases containing system data such as wallpapers.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### S2

```cangjie
S2
```

**Function:** Indicates a medium security level for the database, where data leakage would have significant impact. For example, databases containing user-generated data such as audio recordings, videos, or call logs.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### S3

```cangjie
S3
```

**Function:** Indicates a high security level for the database, where data leakage would have major impact. For example, databases containing user activity, health, or location information.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### S4

```cangjie
S4
```

**Function:** Indicates a critical security level for the database, where data leakage would have severe impact. For example, databases containing authentication credentials or financial data.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum SubscribeType

```cangjie
public enum SubscribeType {
    | SubscribeTypeRemote
    | SubscribeTypeCloud
    | SubscribeTypeCloudDetails
    | ...
}
```

**Function:** Describes subscription types.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SubscribeTypeCloud

```cangjie
SubscribeTypeCloud
```

**Function:** Subscribes to cloud data changes.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### SubscribeTypeCloudDetails

```cangjie
SubscribeTypeCloudDetails
```

**Function:** Subscribes to detailed cloud data changes.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### SubscribeTypeRemote

```cangjie
SubscribeTypeRemote
```

**Function:** Subscribes to remote data changes.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum SyncMode

```cangjie
public enum SyncMode {
    | SyncModePush
    | SyncModePull
    | SyncModeTimeFirst
    | SyncModeNativeFirst
    | SyncModeCloudFirst
    | ...
}
```

**Function:** Indicates database synchronization modes.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncModeCloudFirst

```cangjie
SyncModeCloudFirst
```

**Function:** Indicates data synchronization from the cloud to the local device.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### SyncModeNativeFirst

```cangjie
SyncModeNativeFirst
```

**Function:** Indicates data synchronization from the local device to the cloud.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

### SyncModePull

```cangjie
SyncModePull
```

**Function:** Indicates data being pulled from a remote device to the local device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncModePush

```cangjie
SyncModePush
```

**Function:** Indicates data being pushed from the local device to a remote device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### SyncModeTimeFirst

```cangjie
SyncModeTimeFirst
```

**Function:** Indicates data synchronization from the end with the more recent modification time to the end with the older modification time.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 21

## enum Tokenizer

```cangjie
public enum Tokenizer {
    | NoneTokenizer
    | IcuTokenizer
    | CustomTokenizer
    | ...
}
```

**Function:** Enumerates tokenizers used in full-text search (FTS) scenarios.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### CustomTokenizer

```cangjie
CustomTokenizer
```

**Function:** Indicates the use of a custom tokenizer, supporting Chinese (Simplified and Traditional), English, and Arabic numerals.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### IcuTokenizer

```cangjie
IcuTokenizer
```

**Function:** Indicates the use of the ICU tokenizer, supporting Chinese and multiple languages.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### NoneTokenizer

```cangjie
NoneTokenizer
```

**Function:** Indicates no tokenizer is used.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

## enum ValueType

```cangjie
public enum ValueType {
    | Null
    | Integer(Int64)
    | Double(Float64)
    | StringValue(String)
    | Boolean(Bool)
    | Uint8Array(Array<UInt8>)
    | AssetEnum(Asset)
    | AssetsEnum(Array<Asset>)
    | ...
}
```

**Function:** Represents allowed data field types. The specific type of interface parameters depends on their functionality.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetEnum(Asset)

```cangjie
AssetEnum(Asset)
```

**Function:** Indicates the value type is an attachment [Asset](#type-assets).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### AssetsEnum(Array\<Asset>)

```cangjie
AssetsEnum(Array<Asset>)
```

**Function:** Indicates the value type is an array of attachments Array\<[Asset](#class-asset)>.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Boolean(Bool)

```cangjie
Boolean(Bool)
```

**Function:** Indicates the value type is a boolean.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Double(Float64)

```cangjie
Double(Float64)
```

**Function:** Indicates the value type is a floating-point number.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Integer(Int64)

```cangjie
Integer(Int64)
```

**Function:** Indicates the value type is an integer.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Null

```cangjie
Null
```

**Function:** Indicates the value type is null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** Indicates the value type is a string.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21

### Uint8Array(Array\<UInt8>)

```cangjie
Uint8Array(Array<UInt8>)
```

**Function:** Indicates the value type is an array of UInt8.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 21## type Assets

```cangjie
public type Assets = Array<Asset>
```

**Function:** [Assets](#type-assets) is a type alias for [Array\<Asset>](../../../../cj-user-manual/source_en/basic_data_type/array.md#array).

## type ValuesBucket

```cangjie
public type ValuesBucket = Map<String, ValueType>
```

**Function:** [ValuesBucket](#type-valuesbucket) is a type alias for [Map\<String,ValueType>](../../../../cj-user-manual/source_en/generic/generic_class.md#泛型类).