# ohos.data.relational_store

A Relational Database (RDB) is a database that manages data based on the relational model. The relational database provides a complete mechanism for managing local databases based on the SQLite component, offering a series of interfaces for operations such as insert, delete, update, and query. It can also directly execute user-input SQL statements to meet complex scenario requirements. Worker threads are not supported.

Basic data types supported on the Cangjie side: Int64, Float64, String, binary data, Bool. To ensure successful data insertion and reading, it is recommended that a single piece of data does not exceed 2MB. If the size exceeds this limit, insertion may succeed but reading will fail.

This module provides the following common functionalities related to relational databases:

- [RdbPredicates](#class-rdbpredicates): Terms used in the database to represent the properties, characteristics of data entities, or relationships between data entities, mainly used to define database operation conditions.
- [RdbStore](#class-rdbstore): An interface that provides methods for managing relational databases (RDB).
- [ResultSet](#class-resultset): The result set returned after users call the relational database query interface.

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

For the above example projects and configuration templates, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func deleteRdbStore(UIAbilityContext, String)

```cangjie
public func deleteRdbStore(context: UIAbilityContext, name: String): Unit
```

**Function:** Deletes the database using the specified database file configuration. After successful deletion, it is recommended to set the database object to None. If a custom path is configured in [StoreConfig](#class-storeconfig) when creating the database, calling this interface to delete the database will be ineffective, and the [deleteRdbStore(UIAbilityContext, StoreConfig)](#func-deleterdbstoreuiabilitycontext-storeconfig) interface must be used for deletion.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The application context. |
| name | String | Yes | - | The database name. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800010 | Failed to open or delete the database by an invalid database path. |
  | 14801001 | The operation is supported in the stage model only. |
  | 14801002 | Invalid data group ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Requires obtaining the Context application context. Refer to the usage instructions above.
    deleteRdbStore(Global.getStageContext(), "RdbTest.db")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func deleteRdbStore(UIAbilityContext, StoreConfig)

```cangjie
public func deleteRdbStore(context: UIAbilityContext, config: StoreConfig): Unit
```

**Function:** Deletes the database using the specified database file configuration. After successful deletion, it is recommended to set the database object to None. If the database file is in the public sandbox directory, this interface must be used to delete the database. If multiple processes are operating on the same database, it is recommended to send a database deletion notification to other processes to make them aware and handle it. If a custom path is configured in [StoreConfig](#class-storeconfig) when creating the database, this interface must be called for deletion.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The application context. |
| config | [StoreConfig](#class-storeconfig) | Yes | - | The database configuration related to this RDB store. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800010 | Failed to open or delete the database by an invalid database path. |
  | 14801001 | The operation is supported in the stage model only. |
  | 14801002 | Invalid data group ID. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Requires obtaining the Context application context. Refer to the usage instructions above.
    deleteRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getRdbStore(UIAbilityContext, StoreConfig)

```cangjie
public func getRdbStore(context: UIAbilityContext, config: StoreConfig): RdbStore
```

**Function:** Obtains a related RdbStore to operate the relational database. Users can configure the parameters of the RdbStore according to their needs and then call the RdbStore interface to perform related data operations.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The application context. |
| config | [StoreConfig](#class-storeconfig) | Yes | - | The database configuration related to this RDB store. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbStore](#class-rdbstore) | Returns the RdbStore object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Requires obtaining the Context application context. Refer to the usage instructions above.
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

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

**Initial Version:** 22

### var createTime

```cangjie
public var createTime: String
```

**Function:** The time when the asset was created.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var modifyTime

```cangjie
public var modifyTime: String
```

**Function:** The last time the asset was modified.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var name

```cangjie
public var name: String
```

**Function:** The name of the asset.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var path

```cangjie
public var path: String
```

**Function:** The path of the asset in the application sandbox.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var size

```cangjie
public var size: String
```

**Function:** The size of the space occupied by the asset.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var status

```cangjie
public var status: AssetStatus
```

**Function:** The status of the asset, with a default value of ASSET_NORMAL.

**Type:** [AssetStatus](#enum-assetstatus)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var uri

```cangjie
public var uri: String
```

**Function:** The URI of the asset, which is the absolute path in the system.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### init(String, String, String, String, String, String, AssetStatus)

```cangjie
public init(name: String, uri: String, path: String, createTime: String, modifyTime: String, size: String,
    status!: AssetStatus = AssetStatus.AssetNormal)
```

**Function:** Constructs an Asset.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the asset. |
| uri | String | Yes | - | The URI of the asset, which is the absolute path in the system. |
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

**Initial Version:** 22

### var cryptoPageSize

```cangjie
public var cryptoPageSize: UInt32
```

**Function:** An integer type specifying the page size used for database encryption and decryption.

**Type:** UInt32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var encryptionAlgo

```cangjie
public var encryptionAlgo: EncryptionAlgo
```

**Function:** Specifies the encryption algorithm used for database encryption and decryption.

**Type:** [EncryptionAlgo](#enum-encryptionalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var encryptionKey

```cangjie
public var encryptionKey: Array<UInt8>
```

**Function:** Specifies the key used for database encryption and decryption.

**Type:** Array\<UInt8>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var hmacAlgo

```cangjie
public var hmacAlgo: HmacAlgo
```

**Function:** Specifies the HMAC algorithm used for database encryption and decryption.

**Type:** [HmacAlgo](#enum-hmacalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var iterationCount

```cangjie
public var iterationCount: Int32
```

**Function:** An integer type specifying the iteration count for the PBKDF2 algorithm, with a default value of 10000.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### var kdfAlgo

```cangjie
public var kdfAlgo:?KdfAlgo
```

**Function:** Specifies the PBKDF2 algorithm used for database encryption and decryption.

**Type:** ?[KdfAlgo](#enum-kdfalgo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### init(Array\<UInt8>, Int32, EncryptionAlgo, HmacAlgo, ?KdfAlgo, UInt32)

```cangjie
public init(encryptionKey: Array<UInt8>, iterationCount!: Int32 = 10000,
    encryptionAlgo!: EncryptionAlgo = EncryptionAlgo.Aes256Gcm,
    hmacAlgo!: HmacAlgo = HmacAlgo.Sha256, kdfAlgo!: ?KdfAlgo = None,
    cryptoPageSize!: UInt32 = 1024)
```

**Function:** Constructor of the CryptoParam class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| encryptionKey | Array\<UInt8> | Yes | - | Specifies the key used for database encryption/decryption.<br>If an empty key is passed, the database will generate and store the key, and use the generated key to open the database file.<br>After use, the user must zeroize all key content. |
| iterationCount | Int32 | No | 10000 | An integer specifying the iteration count for the PBKDF2 algorithm in the database. The default value is 10000.<br>The iteration count must be a positive integer; non-integer values will be rounded down.<br>If this parameter is not specified or set to zero, the default value of 10000 will be used, along with the default encryption algorithm AES_256_GCM. |
| encryptionAlgo | [EncryptionAlgo](#enum-encryptionalgo) | No | EncryptionAlgo.Aes256Gcm | Specifies the encryption algorithm used for database encryption/decryption. If not specified, the default value is AES_256_GCM. |
| hmacAlgo | [HmacAlgo](#enum-hmacalgo) | No | HmacAlgo.Sha256 | Specifies the HMAC algorithm used for database encryption/decryption. If not specified, the default value is SHA256. |
| kdfAlgo | ?[KdfAlgo](#enum-kdfalgo) | No | None | Specifies the PBKDF2 algorithm used for database encryption/decryption. If not specified, the default algorithm is the same as the HMAC algorithm. |

## class RdbPredicates

```cangjie
public class RdbPredicates {

    public init(name: String)
}
```

**Description:** Represents predicates for a relational database (RDB). This class determines whether the value of a conditional expression in the RDB is true or false. This type is not thread-safe. If instances derived from this class are operated by multiple threads simultaneously in the application, ensure proper locking protection.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### init(String)

```cangjie
public init(name: String)
```

**Description:** Constructor for the RdbPredicates class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description          |
| :--------| :----- | :-------- | :------ | :------------------- |
| name     | String | Yes       | -       | Name of the database table. |

### func inValues(String, Array\<RelationalStoreValueType>)

```cangjie
public func inValues(field: String, value: Array<RelationalStoreValueType>): RdbPredicates
```

**Description:** Configures the predicate to match fields in the specified column `field` of the data table where the value falls within the given range.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type                                      | Mandatory | Default | Description                          |
| :-------- | :---------------------------------------- | :-------- | :------ | :----------------------------------- |
| field     | String                                    | Yes       | -       | Column name in the database table.   |
| value     | Array\<[RelationalStoreValueType](#enum-relationalstorevaluetype)> | Yes       | -       | Values to match, specified as an array of RelationalStoreValueType. |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Values in the "NAME" column of the data table that are within ["Lisa", "Rose"]
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.inValues("NAME", [RelationalStoreValueType.StringValue("Lisa"), RelationalStoreValueType.StringValue("Rose")])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func and()

```cangjie
public func and(): RdbPredicates
```

**Description:** Adds an AND condition to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RdbPredicates with the AND condition. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields where the value in the "NAME" column is "Lisa" AND the value in the "SALARY" column is "200.5"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
        .and()
        .equalTo("SALARY", RelationalStoreValueType.Double(200.5))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func beginWrap()

```cangjie
public func beginWrap(): RdbPredicates
```

**Description:** Adds a left parenthesis to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RdbPredicates with the left parenthesis. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
        .beginWrap()
        .equalTo("AGE", RelationalStoreValueType.Integer(18))
        .or()
        .equalTo("SALARY", RelationalStoreValueType.Double(200.5))
        .endWrap()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func beginsWith(String, String)

```cangjie
public func beginsWith(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields in the specified column `field` of the data table where the value starts with `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                          |
| :-------- | :----- | :-------- | :------ | :----------------------------------- |
| field     | String | Yes       | -       | Column name in the database table.   |
| value     | String | Yes       | -       | Value to match with the predicate.   |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "NAME" column that start with "Li", such as "Lisa"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.beginsWith("NAME", "Li")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func between(String, RelationalStoreValueType, RelationalStoreValueType)

```cangjie
public func between(field: String, low: RelationalStoreValueType, high: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures the predicate to match fields in the specified column `field` of the data table where the value falls within the given range (inclusive of boundaries).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type                                      | Mandatory | Default | Description                          |
| :-------- | :---------------------------------------- | :-------- | :------ | :----------------------------------- |
| field     | String                                    | Yes       | -       | Column name in the database table.   |
| low       | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes       | -       | Minimum value to match with the predicate. |
| high      | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes       | -       | Maximum value to match with the predicate. |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "AGE" column that are greater than or equal to 10 and less than or equal to 50
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.between("AGE", RelationalStoreValueType.Integer(10), RelationalStoreValueType.Integer(50))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func contains(String, String)

```cangjie
public func contains(field: String, value: String): RdbPredicates
```

**Description:** Configures the predicate to match fields in the specified column `field` of the data table where the value contains `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                          |
| :-------- | :----- | :-------- | :------ | :----------------------------------- |
| field     | String | Yes       | -       | Column name in the database table.   |
| value     | String | Yes       | -       | Value to match with the predicate.   |

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "NAME" column that contain "os", such as "Rose"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.contains("NAME", "os")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func distinct()

```cangjie
public func distinct(): RdbPredicates
```

**Description:** Configures the predicate to filter duplicate records and retain only one of them.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate that can filter duplicate records. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Rose"))
        .distinct()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func endWrap()

```cangjie
public func endWrap(): RdbPredicates
```

**Description:** Adds a right parenthesis to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type                      | Description                              |
| :------------------------ | :--------------------------------------- |
| [RdbPredicates](#class-rdbpredicates) | Returns the RdbPredicates with the right parenthesis. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
        .beginWrap()
        .equalTo("AGE", RelationalStoreValueType.Integer(18))
        .or()
        .equalTo("SALARY", RelationalStoreValueType.Double(200.5))
        .endWrap()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func endsWith(String, String)

```cangjie
public func endsWith(field: String, value: String): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table that end with `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | String | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "NAME" column ending with "se", such as "Rose"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.endsWith("NAME", "se")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func equalTo(String, RelationalStoreValueType)

```cangjie
public func equalTo(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table where the value equals `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "NAME" column where the value equals "Lisa"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func glob(String, String)

```cangjie
public func glob(field: String, value: String): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table where the value matches `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | String | Yes | - | The value to match against the predicate.<br>Supports wildcards: `*` matches 0, 1, or multiple digits or characters; `?` matches exactly 1 digit or character. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "NAME" column of type string where the value matches "?h*g"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.glob("NAME", "?h*g")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func greaterThan(String, RelationalStoreValueType)

```cangjie
public func greaterThan(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table where the value is greater than `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "AGE" column where the value is greater than 18
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.greaterThan("AGE", RelationalStoreValueType.Integer(18))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func greaterThanOrEqualTo(String, RelationalStoreValueType)

```cangjie
public func greaterThanOrEqualTo(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table where the value is greater than or equal to `value`.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches fields in the "AGE" column where the value is greater than or equal to 18
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.greaterThanOrEqualTo("AGE", RelationalStoreValueType.Integer(18))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func groupBy(Array\<String>)

```cangjie
public func groupBy(fields: Array<String>): RdbPredicates
```

**Description:** Configures a predicate to group query results by the specified columns.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fields | Array\<String> | Yes | - | The column names to group by. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate for grouping query columns. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.groupBy(["AGE", "NAME"])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func inAllDevices()

```cangjie
public func inAllDevices(): RdbPredicates
```

**Description:** Connects to all remote devices in the network when synchronizing a distributed database.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.inAllDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isNotNull(String)

```cangjie
public func isNotNull(field: String): RdbPredicates
```

**Description:** Configures a predicate to match fields in the specified column `field` of a data table where the value is not null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.isNotNull("NAME")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isNull(String)

```cangjie
public func isNull(field: String): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table is null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.isNull("NAME")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func lessThan(String, RelationalStoreValueType)

```cangjie
public func lessThan(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table is less than the given value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "AGE" column that are less than 20
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.lessThan("AGE", RelationalStoreValueType.Integer(20))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func lessThanOrEqualTo(String, RelationalStoreValueType)

```cangjie
public func lessThanOrEqualTo(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table is less than or equal to the given value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "AGE" column that are less than or equal to 20
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.lessThanOrEqualTo("AGE", RelationalStoreValueType.Integer(20))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func like(String, String)

```cangjie
public func like(field: String, value: String): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table is similar to the given value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | String | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "NAME" column similar to "os", such as "Rose"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.like("NAME", "%os%")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func limitAs(Int32)

```cangjie
public func limitAs(value: Int32): RdbPredicates
```

**Description:** Sets a predicate to limit the maximum number of data records returned.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Int32 | Yes | - | The maximum number of data records. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate that can be used to set the maximum number of data records. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Rose"))
        .limitAs(3)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func notBetween(String, RelationalStoreValueType, RelationalStoreValueType)

```cangjie
public func notBetween(field: String, low: RelationalStoreValueType, high: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table falls outside the given range (excluding the range boundaries).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| low | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The minimum value to match against the predicate. |
| high | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The maximum value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "AGE" column that are less than 10 or greater than 50
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.notBetween("AGE", RelationalStoreValueType.Integer(10), RelationalStoreValueType.Integer(50))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func notEqualTo(String, RelationalStoreValueType)

```cangjie
public func notEqualTo(field: String, value: RelationalStoreValueType): RdbPredicates
```

**Description:** Configures a predicate to match fields where the value in the specified column of the data table is not equal to the given value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | [RelationalStoreValueType](#enum-relationalstorevaluetype) | Yes | - | The value to match against the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "NAME" column that are not equal to "Lisa"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.notEqualTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func notInValues(String, Array\<RelationalStoreValueType>)

```cangjie
public func notInValues(field: String, value: Array<RelationalStoreValueType>): RdbPredicates
```

**Description:** RelationalStoreValueType

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |
| value | Array\<[RelationalStoreValueType](#enum-relationalstorevaluetype)> | Yes | - | The values to match against the predicate, specified as an array of RelationalStoreValueType. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "NAME" column that are not in ["Lisa", "Rose"]
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.notInValues("NAME", [RelationalStoreValueType.StringValue("Lisa"), RelationalStoreValueType.StringValue("Rose")])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func offsetAs(Int32)

```cangjie
public func offsetAs(rowOffset: Int32): RdbPredicates
```

**Description:** Configures a predicate to specify the starting position of the returned results. This method must be used together with [limitAs](#func-limitasint32).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| rowOffset | Int32 | Yes | - | The starting position of the returned results, which must be a positive integer. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate with the specified starting position for the returned results. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Rose"))
        .offsetAs(3)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func or()

```cangjie
public func or(): RdbPredicates
```

**Description:** Adds an OR condition to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the RDB predicate with the OR condition. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Matches values in the "NAME" column that are equal to "Lisa" OR "Rose"
    let predicates = RdbPredicates("EMPLOYEE")
    predicates
        .equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
        .or()
        .equalTo("NAME", RelationalStoreValueType.StringValue("Rose"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func orderByAsc(String)

```cangjie
public func orderByAsc(field: String): RdbPredicates
```

**Description:** Configures a predicate to sort the values in the specified column of the data table in ascending order.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | Returns the predicate matching the specified field. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.orderByAsc("NAME")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func orderByDesc(String)

```cangjie
public func orderByDesc(field: String): RdbPredicates
```

**Function:** Configures the predicate to sort the column values in the specified field of the data table in descending order.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | The column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RdbPredicates](#class-rdbpredicates) | The column name in the database table. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.orderByDesc("AGE")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class RdbStore

```cangjie
public class RdbStore {}
```

**Description:** Provides interfaces for managing relational database (RDB) methods.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### func backup(String)

```cangjie
public func backup(destName: String): Unit
```

**Description:** Backs up the database with a specified name.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| destName | String | Yes | - | Specifies the backup filename for the database. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    rdbStore.backup("dbBackup.db")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func batchInsert(String, Array\<ValuesBucket>)

```cangjie
public func batchInsert(table: String, values: Array<ValuesBucket>): Int64
```

**Description:** Inserts a set of data into the specified table.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| table | String | Yes | - | Specifies the target table name. |
| values | Array\<[ValuesBucket](#type-valuesbucket)> | Yes | - | Represents the set of data to be inserted into the table. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the number of inserted data items if the operation is successful; otherwise, returns -1. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var values1 = HashMap<String, RelationalStoreValueType>()
    values1.add("ID", RelationalStoreValueType.Integer(1))
    values1.add("NAME", RelationalStoreValueType.StringValue("Lisa"))
    values1.add("AGE", RelationalStoreValueType.Integer(18))
    values1.add("SALARY", RelationalStoreValueType.Double(100.5))
    var values2 = HashMap<String, RelationalStoreValueType>()
    values2.add("ID", RelationalStoreValueType.Integer(2))
    values2.add("NAME", RelationalStoreValueType.StringValue("Jack"))
    values2.add("AGE", RelationalStoreValueType.Integer(19))
    values2.add("SALARY", RelationalStoreValueType.Double(101.5))
    var values3 = HashMap<String, RelationalStoreValueType>()
    values3.add("ID", RelationalStoreValueType.Integer(3))
    values3.add("NAME", RelationalStoreValueType.StringValue("Tom"))
    values3.add("AGE", RelationalStoreValueType.Integer(20))
    values3.add("SALARY", RelationalStoreValueType.Double(102.5))
    let valueBuckets: Array<Map<String, RelationalStoreValueType>>= [values1, values2, values3]
    rdbStore.batchInsert("EMPLOYEE", valueBuckets)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func beginTransaction()

```cangjie
public func beginTransaction(): Unit
```

**Description:** Starts a transaction before executing SQL statements. This interface does not support multi-process or multi-thread usage.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    var values = HashMap<String, RelationalStoreValueType>()
    rdbStore.beginTransaction()
    values.add("ID", RelationalStoreValueType.Integer(2))
    values.add("NAME", RelationalStoreValueType.StringValue("Sun"))
    rdbStore.insert("THING", values)
    rdbStore.commit()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func commit()

```cangjie
public func commit(): Unit
```

**Description:** Commits the executed SQL statements. This interface does not support multi-process or multi-thread usage.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    rdbStore.executeSql("CREATE TABLE THING(ID int NOT NULL, NAME varchar(255) NOT NULL, PRIMARY KEY (Id))")
    rdbStore.beginTransaction()
    var values = HashMap<String, RelationalStoreValueType>()
    values.add("ID", RelationalStoreValueType.Integer(2))
    values.add("NAME", RelationalStoreValueType.StringValue("Sun"))
    rdbStore.insert("THING", values)
    rdbStore.commit()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func delete(RdbPredicates)

```cangjie
public func delete(predicates: RdbPredicates): Int64
```

**Description:** Deletes data from the database based on the conditions specified by the RdbPredicates instance.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| predicates | [RdbPredicates](#class-rdbpredicates) | Yes | - | Specifies the deletion conditions through an RdbPredicates instance. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Number of affected rows. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.equalTo("NAME", RelationalStoreValueType.StringValue("Lisa"))
    rdbStore.delete(predicates)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func emit(String)

```cangjie
public func emit(event: String): Unit
```

**Description:** Notifies the inter-process or intra-process listeners registered via [on](#func-onstring-bool-callback0argument).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | String | Yes | - | Name of the event to notify subscribers. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800050 | Failed to obtain the subscription service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.*
import ohos.callback_invoke.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added to dependency definitions
    class TestCallback <: Callback0Argument {
        public init() {}
        public open func invoke(err: ?BusinessException): Unit {
            Hilog.info(0, "test", "Call invoke.", "")
        }
    }

### func executeSql(String, Array\<RelationalStoreValueType>)

```cangjie
public func executeSql(sql: String, bindArgs!: Array<RelationalStoreValueType> = []): Unit
```

**Function:** Executes an SQL statement with specified parameters but does not return a value.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sql | String | Yes | - | Specifies the SQL statement to execute. |
| bindArgs | Array\<[RelationalStoreValueType](#enum-relationalstorevaluetype)> | No | [] | Values of parameters in the SQL statement. These values correspond to placeholders in the SQL statement. If the SQL statement is complete, this parameter can be omitted. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    rdbStore.executeSql("DELETE FROM EMPLOYEE WHERE ID = ?", bindArgs: [RelationalStoreValueType.Integer(3)])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func insert(String, ValuesBucket, ConflictResolution)

```cangjie
public func insert(table: String, values: ValuesBucket,
    conflict!: ConflictResolution = ConflictResolution.OnConflictNone): Int64
```

**Function:** Inserts a row of data into the specified table.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| table | String | Yes | - | Name of the target table. |
| values | [ValuesBucket](#type-valuesbucket) | Yes | - | Represents the row of data to be inserted into the table. |
| conflict | [ConflictResolution](#enum-conflictresolution) | No | ConflictResolution.OnConflictNone | Specifies the conflict resolution method. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the row ID if the operation is successful; otherwise, returns -1. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    rdbStore.executeSql(
        "CREATE TABLE EMPLOYEE(ID int NOT NULL, NAME varchar(255) NOT NULL, AGE int, SALARY float NOT NULL, CODES Bit NOT NULL, PRIMARY KEY (Id))"
    )
    var values = HashMap<String, RelationalStoreValueType>()
    values.add("ID", RelationalStoreValueType.Integer(1))
    values.add("NAME", RelationalStoreValueType.StringValue("Lisa"))
    values.add("AGE", RelationalStoreValueType.Integer(18))
    values.add("SALARY", RelationalStoreValueType.Double(100.5))
    values.add("CODES", RelationalStoreValueType.Boolean(true))
    rdbStore.insert("EMPLOYEE", values, conflict: OnConflictReplace)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(String, Bool, ?Callback0Argument)

```cangjie
public func off(event: String, interProcess: Bool, observer!: ?Callback0Argument = None): Unit
```

**Function:** Unsubscribes from data change event notifications.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | String | Yes | - | Name of the event to unsubscribe from. |
| interProcess | Bool | Yes | - | Specifies whether to unsubscribe from inter-process or intra-process events. true: inter-process. false: intra-process. |
| observer | ?[Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | No | None | Specifies the callback object to unsubscribe. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800050 | Failed to obtain the subscription service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.*
import ohos.callback_invoke.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added to dependency definitions.
    class TestCallback <: Callback0Argument {
        public init() {}
        public open func invoke(): Unit {
            Hilog.info(0, "test", "Call invoke.", "")
        }
    }

    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(), StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let testCallback = TestCallback()
    rdbStore.on("PRINT", false, testCallback)
    rdbStore.off("PRINT", false, observer: testCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(String, Bool, Callback0Argument)

```cangjie
public func on(event: String, interProcess: Bool, observer: Callback0Argument): Unit
```

**Function:** Subscribes to intra-process or inter-process event notifications for the database. The callback is invoked when the [emit](#func-emitstring) interface is called.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | String | Yes | - | Name of the event to subscribe to. |
| interProcess | Bool | Yes | - | Specifies whether to subscribe to inter-process or intra-process events.<br/> true: inter-process.<br/> false: intra-process. |
| observer | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800050 | Failed to obtain the subscription service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import kit.PerformanceAnalysisKit.*
import ohos.callback_invoke.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added to dependency definitions.
    class TestCallback <: Callback0Argument {
        public init() {}
        public open func invoke(): Unit {
            Hilog.info(0, "test", "Call invoke.", "")
        }
    }

    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let testCallback = TestCallback()
    rdbStore.on("PRINT", false, testCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func query(RdbPredicates, Array\<String>)

```cangjie
public func query(predicates: RdbPredicates, columns!: Array<String> = []): ResultSet
```

**Function:** Queries data in the database based on specified conditions.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| predicates | [RdbPredicates](#class-rdbpredicates) | Yes | - | RdbPredicates instance object specifying the query conditions. |
| columns | Array\<String> | No | [] | Specifies the columns to query. If empty, all columns are queried. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ResultSet](#class-resultset) | ResultSet object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.equalTo("NAME", RelationalStoreValueType.StringValue("Rose"))
    let columns = ["ID", "NAME", "AGE", "SALARY", "CODES"]
    let resultSet = rdbStore.query(predicates, columns: columns)
    resultSet.goToNextRow()
    let id = resultSet.getLong(resultSet.getColumnIndex("ID"))
    let name = resultSet.getString(resultSet.getColumnIndex("NAME"))
    let age = resultSet.getLong(resultSet.getColumnIndex("AGE"))
    let salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func querySql(String, Array\<RelationalStoreValueType>)

```cangjie
public func querySql(sql: String, bindArgs!: Array<RelationalStoreValueType> = []): ResultSet
```

**Function:** Queries data in the database based on a specified SQL statement.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sql | String | Yes | - | Specifies the SQL statement to execute. |
| bindArgs | Array\<[RelationalStoreValueType](#enum-relationalstorevaluetype)> | No | [] | **Named parameters.** Values of parameters in the SQL statement. These values correspond to placeholders in the SQL statement. If the SQL statement is complete, this parameter can be omitted. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ResultSet](#class-resultset) | Returns a ResultSet object if the operation is successful. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800014 | The RdbStore or ResultSet is already closed. |
  | 14800015 | The database does not respond. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToNextRow()
    let id = resultSet.getLong(resultSet.getColumnIndex("ID"))
    let name = resultSet.getString(resultSet.getColumnIndex("NAME"))
    let age = resultSet.getLong(resultSet.getColumnIndex("AGE"))
    let salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func restore(String)

```cangjie
public func restore(srcName: String): Unit
```

**Function:** Restores the database from a specified backup file.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| srcName | String | Yes | - | Specifies the name of the database backup file. |

**Exceptions:**

- BusinessException: The corresponding error codes are shown in the following table. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Application Context needs to be obtained. For details, see the usage instructions in this document.
    rdbStore.restore("dbBackup.db")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func rollBack()

```cangjie
public func rollBack(): Unit
```

**Function:** Rolls back executed SQL statements. This interface does not support multi-process or multi-thread usage.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Exceptions:**

- BusinessException: The corresponding error codes are shown in the following table. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Application Context needs to be obtained. For details, see the usage instructions in this document.
    let predicates = RdbPredicates("THING")
    var values = HashMap<String, RelationalStoreValueType>()
    try {
        rdbStore.beginTransaction()
        values.add("ID", RelationalStoreValueType.Integer(3))
        values.add("NAME", RelationalStoreValueType.StringValue("Tom"))
        rdbStore.insert("THING", values)
        values.add("ID", RelationalStoreValueType.Integer(4))
        values.add("NAME", RelationalStoreValueType.StringValue("Wind"))
        rdbStore.insert("THING", values)
        rdbStore.commit()
    } catch (e: Exception) {
        rdbStore.rollBack()
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func update(ValuesBucket, RdbPredicates, ConflictResolution)

```cangjie
public func update(values: ValuesBucket, predicates: RdbPredicates,
    conflict!: ConflictResolution = ConflictResolution.OnConflictNone): Int64
```

**Function:** Updates data in the database based on the specified RdbPredicates instance.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| values | [ValuesBucket](#type-valuesbucket) | Yes | - | Indicates the data rows to be updated in the database. Key-value pairs are associated with column names in the database table. |
| predicates | [RdbPredicates](#class-rdbpredicates) | Yes | - | Specifies the update conditions through an RdbPredicates instance. |
| conflict | [ConflictResolution](#enum-conflictresolution) | No | ConflictResolution.OnConflictNone | Specifies the conflict resolution strategy. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the number of affected rows. |

**Exceptions:**

- BusinessException: The corresponding error codes are shown in the following table. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import std.collection.HashMap
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Application Context needs to be obtained. For details, see the usage instructions in this document.
    let predicates = RdbPredicates("EMPLOYEE")
    predicates.equalTo("NAME", RelationalStoreValueType.StringValue("TOM"))
    var values = HashMap<String, RelationalStoreValueType>()
    values.add("NAME", RelationalStoreValueType.StringValue("TOM"))
    values.add("AGE", RelationalStoreValueType.Integer(88))
    values.add("SALARY", RelationalStoreValueType.Double(9999.513))
    rdbStore.update(values, predicates, conflict: OnConflictReplace)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class ResultSet

```cangjie
public class ResultSet {}
```

**Description:** Provides access methods for database result sets generated through queries. A result set refers to the collection of results returned after a user invokes a relational database query interface, offering various flexible data access methods for users to retrieve data items.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop columnCount

```cangjie
public prop columnCount: Int32
```

**Description:** Gets the number of columns in the result set.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop columnNames

```cangjie
public prop columnNames: Array<String>
```

**Description:** Gets the names of all columns in the result set.

**Type:** Array\<String>

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop isAtFirstRow

```cangjie
public prop isAtFirstRow: Bool
```

**Description:** Checks whether the result set is positioned at the first row.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop isAtLastRow

```cangjie
public prop isAtLastRow: Bool
```

**Description:** Checks whether the result set is positioned at the last row.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop isClosed

```cangjie
public prop isClosed: Bool
```

**Description:** Checks whether the current result set is closed.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop isEnded

```cangjie
public prop isEnded: Bool
```

**Description:** Checks whether the result set is positioned after the last row.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop isStarted

```cangjie
public prop isStarted: Bool
```

**Description:** Checks whether the cursor has moved.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop rowCount

```cangjie
public prop rowCount: Int32
```

**Description:** Gets the number of rows in the result set.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### prop rowIndex

```cangjie
public prop rowIndex: Int32
```

**Description:** Gets the index of the current row in the result set.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Description:** Closes the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800012 | ResultSet is empty or pointer index is out of bounds. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAsset(Int32)

```cangjie
public func getAsset(columnIndex: Int32): Asset
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | The specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [Asset](#class-asset) | Returns the value of the specified column as an Asset. |

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let doc = resultSet.getAsset(resultSet.getColumnIndex("DOC"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAssets(Int32)

```cangjie
public func getAssets(columnIndex: Int32): Assets
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | The specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Assets | Returns the value of the specified column as an Array\<[Asset](#class-asset)>. |

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let docs = resultSet.getAssets(resultSet.getColumnIndex("DOCS"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getBlob(Int32)

```cangjie
public func getBlob(columnIndex: Int32): Array<UInt8>
```

**Description:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | The specified column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt8> | Returns the value of the specified column as a byte array. |

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
         StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context required. See usage instructions for details.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let codes = resultSet.getBlob(resultSet.getColumnIndex("CODES"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getColumnIndex(String)

```cangjie
public func getColumnIndex(columnName: String): Int32
```

**Function:** Gets the column index based on the specified column name.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnName | String | Yes | - | The name of the specified column in the result set. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the index of the specified column. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let id = resultSet.getLong(resultSet.getColumnIndex("ID"))
    let name = resultSet.getString(resultSet.getColumnIndex("NAME"))
    let age = resultSet.getLong(resultSet.getColumnIndex("AGE"))
    let salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getColumnName(Int32)

```cangjie
public func getColumnName(columnIndex: Int32): String
```

**Function:** Gets the column name based on the specified column index.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | The index of the specified column in the result set. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the name of the specified column. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14800000 | Inner error. |
  | 14800011 | Failed to open the database because it is corrupted. |
  | 14800013 | Resultset is empty or column index is out of bounds. |
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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let id = resultSet.getColumnName(0)
    let name = resultSet.getColumnName(1)
    let age = resultSet.getColumnName(2)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getDouble(Int32)

```cangjie
public func getDouble(columnIndex: Int32): Float64
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DDistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | The index of the specified column, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | Returns the value of the specified column as Float64. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getLong(Int32)

```cangjie
public func getLong(columnIndex: Int32): Int64
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | The index of the specified column, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the value of the specified column as Int64. <br>This interface supports data in the range of Number.MIN_SAFE_INTEGER ~ Number.MAX_SAFE_INTEGER. If the data exceeds this range, it is recommended to use [getDouble](#func-getdoubleint32). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let age = resultSet.getLong(resultSet.getColumnIndex("AGE"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getRow()

```cangjie
public func getRow(): ValuesBucket
```

**Function:** Gets the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ValuesBucket](#type-valuesbucket) | Returns the value of the specified row. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let value = resultSet.getRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getString(Int32)

```cangjie
public func getString(columnIndex: Int32): String
```

**Function:** Gets the value of the specified column in the current row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| columnIndex | Int32 | Yes | - | The index of the specified column, starting from 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the value of the specified column as a string. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Requires obtaining the Context application context, refer to the usage instructions in this document
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let name = resultSet.getString(resultSet.getColumnIndex("NAME"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goTo(Int32)

```cangjie
public func goTo(offset: Int32): Bool
```

**Function:** Moves the result set forward or backward to the specified row relative to its current position.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| offset | Int32 | Yes | - | The offset relative to the current position. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context is required. For details, see the usage instructions.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goTo(1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goToFirstRow()

```cangjie
public func goToFirstRow(): Bool
```

**Function:** Moves the result set to the first row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context is required. For details, see the usage instructions.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToFirstRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goToLastRow()

```cangjie
public func goToLastRow(): Bool
```

**Function:** Moves the result set to the last row.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context is required. For details, see the usage instructions.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToLastRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goToNextRow()

```cangjie
public func goToNextRow(): Bool
```

**Function:** Moves to the next row in the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToNextRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goToPreviousRow()

```cangjie
public func goToPreviousRow(): Bool
```

**Function:** Moves to the previous row in the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToPreviousRow()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func goToRow(Int32)

```cangjie
public func goToRow(position: Int32): Bool
```

**Function:** Moves to the specified row in the result set.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| position | Int32 | Yes | - | Specifies the target position to move to. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the result set is successfully moved; otherwise returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // Context application context needs to be obtained. For details, see the usage instructions in this document.
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    resultSet.goToRow(5)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isColumnNull(Int32)

```cangjie
public func isColumnNull(columnIndex: Int32): Bool
```

**Function:** Checks whether the value of the specified column in the current row is null.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| columnIndex | Int32 | Yes | - | Specifies the column index, starting from 0. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the value of the specified column in the current row is null; otherwise returns false. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Relational Database Error Codes](./cj-errorcode-data-rdb.md).

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

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var rdbStore: RdbStore = getRdbStore(Global.getStageContext(),
        StoreConfig(RelationalStoreSecurityLevel.S1, name: "RdbTest.db")) // 需获取Context应用上下文，详见本文使用说明
    let resultSet = rdbStore.querySql("SELECT * FROM EMPLOYEE WHERE NAME = 'Peter'")
    let isColumnNull = resultSet.isColumnNull(resultSet.getColumnIndex("CODES"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class StoreConfig

```cangjie
public class StoreConfig {
    public var name: String
    public var securityLevel: RelationalStoreSecurityLevel
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

    public init(securityLevel: RelationalStoreSecurityLevel, name!: String = "",
        encrypt!: Bool = false, dataGroupId!: String = "",
        customDir!: String = "", rootDir!: String = "",
        autoCleanDirtyData!: Bool = true, allowRebuild!: Bool = false,
        isReadOnly!: Bool = false, pluginLibs!: Array<String> = Array<String>(),
        cryptoParam!: CryptoParam, vector!: Bool = false,
        tokenizer!: Tokenizer = Tokenizer.NoneTokenizer, persist!: Bool = true,
        enableSemanticIndex!: Bool = false)
}
```

**Description:** Manages relational database configurations.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var allowRebuild

```cangjie
public var allowRebuild: Bool
```

**Description:** Specifies whether the database supports automatic deletion and recreation of empty tables when exceptions occur. Default is false (no deletion).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var autoCleanDirtyData

```cangjie
public var autoCleanDirtyData: Bool
```

**Description:** Specifies whether to automatically clean data deleted from the cloud and synced to the local device. true means automatic cleaning, false means manual cleaning (default is true). For cloud-device collaborative databases, when cloud-deleted data is synced to the device, this parameter determines whether the device automatically cleans it. Manual cleaning can be performed via the cleanDirtyData interface.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### var cryptoParam

```cangjie
public var cryptoParam: CryptoParam
```

**Description:** Specifies user-defined encryption parameters.

**Type:** [CryptoParam](#class-cryptoparam)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var customDir

```cangjie
public var customDir: String
```

**Description:** Custom path for the database.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var dataGroupId

```cangjie
public var dataGroupId: String
```

**Description:** Application group ID, which must be obtained from the application market.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var enableSemanticIndex

```cangjie
public var enableSemanticIndex: Bool
```

**Description:** Specifies whether to enable semantic indexing for the database. true enables semantic indexing, false disables it (default is false).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var encrypt

```cangjie
public var encrypt: Bool
```

**Description:** Specifies whether the database is encrypted. Default is false (not encrypted). true: encrypted. false: not encrypted.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var isReadOnly

```cangjie
public var isReadOnly: Bool
```

**Description:** Specifies whether the database is read-only. Default is false (read-write).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var name

```cangjie
public var name: String
```

**Description:** Database filename.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var persist

```cangjie
public var persist: Bool
```

**Description:** Specifies whether the database requires persistence. true means persistent, false means in-memory database (default is true).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var pluginLibs

```cangjie
public var pluginLibs: Array<String>
```

**Description:** An array of dynamic library names containing capabilities such as FTS (Full-Text Search).

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var rootDir

```cangjie
public var rootDir: String
```

**Description:** Specifies the root directory path for the database.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var securityLevel

```cangjie
public var securityLevel: RelationalStoreSecurityLevel
```

**Description:** Sets the security level of the database.

**Type:** [RelationalStoreSecurityLevel](#enum-relationalstoresecuritylevel)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var tokenizer

```cangjie
public var tokenizer: Tokenizer
```

**Description:** Specifies which tokenizer to use in FTS scenarios.

**Type:** [Tokenizer](#enum-tokenizer)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### var vector

```cangjie
public var vector: Bool
```

**Description:** Specifies whether the database is a vector database. true means vector database, false means relational database (default is false).

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### init(RelationalStoreSecurityLevel, String, Bool, String, String, String, Bool, Bool, Bool, Array\<String>, CryptoParam, Bool, Tokenizer, Bool, Bool)

```cangjie
public init(securityLevel: RelationalStoreSecurityLevel, name!: String = "",
    encrypt!: Bool = false, dataGroupId!: String = "",
    customDir!: String = "", rootDir!: String = "",
    autoCleanDirtyData!: Bool = true, allowRebuild!: Bool = false,
    isReadOnly!: Bool = false, pluginLibs!: Array<String> = Array<String>(),
    cryptoParam = CryptoParam([]), vector!: Bool = false,
    tokenizer!: Tokenizer = Tokenizer.NoneTokenizer, persist!: Bool = true,
    enableSemanticIndex!: Bool = false)
```

**Description:** Constructor for the StoreConfig class.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| securityLevel | [RelationalStoreSecurityLevel](#enum-relationalstoresecuritylevel) | Yes | - | Sets the security level of the database.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| name | String | No | "" | Database filename.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| encrypt | Bool | No | false | **Named parameter.** Specifies whether the database is encrypted. Default is false (not encrypted).<br/> true: encrypted.<br/> false: not encrypted.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| dataGroupId | String | No | "" | **Named parameter.** Application group ID, which must be obtained from the application market.<br/>**Model Constraint:** This property is only available in Stage model.<br/>Specifies creating an RdbStore instance in the sandbox path corresponding to this dataGroupId. If this parameter is not provided, the RdbStore instance is created in the default application sandbox directory.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| customDir | String | No | "" | Custom path for the database.<br/>**Usage Constraint:** The database path size is limited to 128 bytes. Exceeding this limit will cause the database to fail to open and return an error.<br/>The database will be created in the following directory structure: context.databaseDir + "/rdb/" + customDir, where context.databaseDir is the application sandbox path, "/rdb/" indicates a relational database, and customDir is the custom path. If this parameter is not provided, the RdbStore instance is created in the default application sandbox directory.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| rootDir | String | No | "" | Specifies the root directory path for the database.<br/>From API version 18, this optional parameter is supported. The database will be opened or deleted from the following directory: rootDir + "/" + customDir. Databases opened with this parameter are in read-only mode; write operations will return error code 801. When opening or deleting a database with this parameter, ensure the database file exists in the specified path and has read permissions; otherwise, error code 14800010 will be returned.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| autoCleanDirtyData | Bool | No | true | **Named parameter.** Specifies whether to automatically clean data deleted from the cloud and synced to the local device. true means automatic cleaning, false means manual cleaning (default is true).<br/>For cloud-device collaborative databases, when cloud-deleted data is synced to the device, this parameter determines whether the device automatically cleans it. Manual cleaning can be performed via the cleanDirtyData interface.<br/>**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client |
| allowRebuild | Bool | No | false | Specifies whether the database supports automatic deletion and recreation of empty tables when exceptions occur. Default is false (no deletion).<br/>true: automatic deletion.<br/>false: no automatic deletion.<br/>From API version 12, this optional parameter is supported.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| isReadOnly | Bool | No | false | Specifies whether the database is read-only. Default is false (read-write).<br/>true: only allows reading data; write operations will return error code 801.<br/>false: allows read-write operations.<br/>From API version 12, this optional parameter is supported.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| pluginLibs | Array\<String> | No | Array<String>() | An array of dynamic library names containing capabilities such as FTS (Full-Text Search).<br/>**Usage Constraints:**<br/>1. The number of dynamic library names is limited to 16. Exceeding this limit will cause the database to fail to open and return an error.<br/>2. Dynamic libraries must be located in the application sandbox path or system path. If a dynamic library cannot be loaded, the database will fail to open and return an error.<br/>3. Dynamic library names must be full paths for SQLite to load them.<br/>Example: [context.bundleCodeDir + "/libs/arm64/" + libtokenizer.so], where context.bundleCodeDir is the application sandbox path, "/libs/arm64/" is the subdirectory, and libtokenizer.so is the dynamic library filename. If this parameter is not provided, no dynamic libraries are loaded by default.<br/>4. Dynamic libraries must include all dependencies to avoid runtime failures due to missing dependencies.<br/>For example, in an NDK project, building libtokenizer.so with default compilation parameters makes it dependent on the C++ standard library. When loading this library, due to namespace inconsistencies with the compilation environment, it may link to the wrong libc++_shared.so, causing the __emutls_get_address symbol to be missing. To resolve this, statically link the C++ standard library during compilation. For details, refer to the NDK Project Build Overview.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| cryptoParam | [CryptoParam](#class-cryptoparam) | No | CryptoParam([]) | **Named parameter.** Specifies user-defined encryption parameters.<br/>If this parameter is not provided, default encryption parameters are used (see CryptoParam default values).<br/>This configuration only takes effect when the encrypt option is set to true.<br/>From API version 14, this optional parameter is supported.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| vector | Bool | No | false | Specifies whether the database is a vector database. true means vector database, false means relational database (default is false).<br/>Vector databases are suitable for storing and processing high-dimensional vector data, while relational databases are for structured data.<br/>When using a vector database, ensure all opened RdbStore and ResultSet instances are successfully closed before calling deleteRdbStore.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| tokenizer | [Tokenizer](#enum-tokenizer) | No | Tokenizer.NoneTokenizer | Specifies which tokenizer to use in FTS scenarios.<br/>If this parameter is not provided, FTS will not support Chinese or multilingual tokenization but will still support English tokenization.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| persist | Bool | No | true | Specifies whether the database requires persistence. true means persistent, false means in-memory database (default is true).<br/>In-memory databases do not support encryption, backup, restore, cross-process access, or distributed capabilities. The securityLevel property is ignored.<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |
| enableSemanticIndex | Bool | No | false | Specifies whether to enable semantic indexing for the database. true enables semantic indexing, false disables it (default is false).<br/>**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core |

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

**Description:** Enumerates the statuses of asset attachments.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetAbnormal

```cangjie
AssetAbnormal
```

**Description:** Indicates abnormal asset status.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetDelete

```cangjie
AssetDelete
```

**Description:** Indicates that the asset needs to be deleted from the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetDownloading

```cangjie
AssetDownloading
```

**Description:** Indicates that the asset is being downloaded to the local device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetInsert

```cangjie
AssetInsert
```

**Description:** Indicates that the asset needs to be inserted into the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetNormal

```cangjie
AssetNormal
```

**Description:** Indicates normal asset status.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetUpdate

```cangjie
AssetUpdate
```

**Description:** Indicates that the asset needs to be updated in the cloud.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22## enum ChangeType

```cangjie
public enum ChangeType {
    | DataChange
    | AssetChange
    | ...
}
```

**Function:** Describes the type of data change.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### AssetChange

```cangjie
AssetChange
```

**Function:** Indicates that an asset attachment has changed.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### DataChange

```cangjie
DataChange
```

**Function:** Indicates that data has changed.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

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

**Function:** Conflict resolution methods for insert and update interfaces.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictAbort

```cangjie
OnConflictAbort
```

**Function:** When a conflict occurs, aborts the current SQL statement and rolls back any changes made by it, while preserving changes from prior SQL statements in the same transaction and keeping the transaction active.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictFail

```cangjie
OnConflictFail
```

**Function:** When a conflict occurs, aborts the current SQL statement without rolling back its changes or terminating the transaction.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictIgnore

```cangjie
OnConflictIgnore
```

**Function:** When a conflict occurs, skips the row violating constraints and continues processing subsequent rows in the SQL statement.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictNone

```cangjie
OnConflictNone
```

**Function:** When a conflict occurs, takes no action.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictReplace

```cangjie
OnConflictReplace
```

**Function:** When a conflict occurs, deletes pre-existing rows causing constraint violations before inserting or updating the current row, then proceeds with normal execution.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### OnConflictRollback

```cangjie
OnConflictRollback
```

**Function:** When a conflict occurs, aborts the SQL statement and rolls back the current transaction.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

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

**Since:** 22

### DistributedCloud

```cangjie
DistributedCloud
```

**Function:** Indicates a database table distributed between devices and the cloud.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### DistributedDevice

```cangjie
DistributedDevice
```

**Function:** Indicates a database table distributed across different devices.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

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

**Since:** 22

### Aes256Cbc

```cangjie
Aes256Cbc
```

**Function:** AES_256_CBC encryption algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### Aes256Gcm

```cangjie
Aes256Gcm
```

**Function:** AES_256_GCM encryption algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

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

**Function:** Special fields for predicate query conditions.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### CursorField

```cangjie
CursorField
```

**Function:** Field name for cursor lookup.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### DeletedFlagField

```cangjie
DeletedFlagField
```

**Function:** Field populated in result sets during cursor lookup, indicating whether data deleted from the cloud has been cleaned locally. A value of `false` means data is not cleaned, while `true` means cleaned.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### OriginField

```cangjie
OriginField
```

**Function:** Field name specifying data source during cursor lookup.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### OwnerField

```cangjie
OwnerField
```

**Function:** Field populated in result sets when querying shared tables, indicating the initiator of the shared record.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### PrivilegeField

```cangjie
PrivilegeField
```

**Function:** Field populated in result sets when querying shared data permissions, indicating allowed operations for the shared record.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

### SharingResourceField

```cangjie
SharingResourceField
```

**Function:** Field populated in result sets when querying shared data resources, indicating the identifier of the shared resource.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Since:** 22

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

**Since:** 22

### Sha1

```cangjie
Sha1
```

**Function:** HMAC_SHA1 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### Sha256

```cangjie
Sha256
```

**Function:** HMAC_SHA256 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### Sha512

```cangjie
Sha512
```

**Function:** HMAC_SHA512 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

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

**Since:** 22

### KdfSha1

```cangjie
KdfSha1
```

**Function:** PBKDF2_HMAC_SHA1 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### KdfSha256

```cangjie
KdfSha256
```

**Function:** PBKDF2_HMAC_SHA256 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22

### KdfSha512

```cangjie
KdfSha512
```

**Function:** PBKDF2_HMAC_SHA512 algorithm.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Since:** 22## enum Origin

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

**Initial Version:** 22

### Cloud

```cangjie
Cloud
```

**Function:** Represents cloud-synced data.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### Local

```cangjie
Local
```

**Function:** Represents local data.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### Remote

```cangjie
Remote
```

**Function:** Represents peer-to-peer synced data.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

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

**Initial Version:** 22

### SyncBegin

```cangjie
SyncBegin
```

**Function:** Indicates the start of device-cloud synchronization.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### SyncFinish

```cangjie
SyncFinish
```

**Function:** Indicates the completion of device-cloud synchronization.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### SyncInProgress

```cangjie
SyncInProgress
```

**Function:** Indicates that device-cloud synchronization is in progress.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

## enum RelationalStoreSecurityLevel

```cangjie
public enum RelationalStoreSecurityLevel {
    | S1
    | S2
    | S3
    | S4
    | ...
}
```

**Function:** Enumerates database security levels.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### S1

```cangjie
S1
```

**Function:** Indicates a low security level where data leakage would have minor impact. Example: databases containing system data like wallpapers.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### S2

```cangjie
S2
```

**Function:** Indicates a medium security level where data leakage would have significant impact. Example: databases containing user-generated content like audio/video recordings or call logs.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### S3

```cangjie
S3
```

**Function:** Indicates a high security level where data leakage would have major impact. Example: databases containing user health, fitness, or location data.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### S4

```cangjie
S4
```

**Function:** Indicates a critical security level where data leakage would have severe impact. Example: databases containing authentication credentials or financial data.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

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

**Initial Version:** 22

### SubscribeTypeCloud

```cangjie
SubscribeTypeCloud
```

**Function:** Subscribes to cloud data changes.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### SubscribeTypeCloudDetails

```cangjie
SubscribeTypeCloudDetails
```

**Function:** Subscribes to detailed cloud data changes.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### SubscribeTypeRemote

```cangjie
SubscribeTypeRemote
```

**Function:** Subscribes to remote data changes.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

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

**Function:** Specifies database synchronization modes.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### SyncModeCloudFirst

```cangjie
SyncModeCloudFirst
```

**Function:** Synchronizes data from cloud to local device.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### SyncModeNativeFirst

```cangjie
SyncModeNativeFirst
```

**Function:** Synchronizes data from local device to cloud.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

### SyncModePull

```cangjie
SyncModePull
```

**Function:** Pulls data from remote device to local device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### SyncModePush

```cangjie
SyncModePush
```

**Function:** Pushes data from local device to remote device.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### SyncModeTimeFirst

```cangjie
SyncModeTimeFirst
```

**Function:** Synchronizes data from the endpoint with more recent modifications to the endpoint with older modifications.

**System Capability:** SystemCapability.DistributedDataManager.CloudSync.Client

**Initial Version:** 22

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

**Initial Version:** 22

### CustomTokenizer

```cangjie
CustomTokenizer
```

**Function:** Uses a proprietary tokenizer supporting Chinese (Simplified/Traditional), English, and Arabic numerals.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### IcuTokenizer

```cangjie
IcuTokenizer
```

**Function:** Uses ICU tokenizer supporting Chinese and multiple languages.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### NoneTokenizer

```cangjie
NoneTokenizer
```

**Function:** No tokenizer is used.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

## enum RelationalStoreValueType

```cangjie
public enum RelationalStoreValueType {
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

**Function:** Represents allowed data field types. Interface parameter types depend on specific functionality.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### AssetEnum(Asset)

```cangjie
AssetEnum(Asset)
```

**Function:** Indicates value type as attachment [Asset](#type-assets).

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### AssetsEnum(Array\<Asset>)

```cangjie
AssetsEnum(Array<Asset>)
```

**Function:** Indicates value type as attachment array Array\<[Asset](#class-asset)>.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### Boolean(Bool)

```cangjie
Boolean(Bool)
```

**Function:** Indicates boolean value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### Double(Float64)

```cangjie
Double(Float64)
```

**Function:** Indicates floating-point numeric value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### Integer(Int64)

```cangjie
Integer(Int64)
```

**Function:** Indicates integer numeric value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### Null

```cangjie
Null
```

**Function:** Indicates null value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** Indicates string value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22

### Uint8Array(Array\<UInt8>)

```cangjie
Uint8Array(Array<UInt8>)
```

**Function:** Indicates UInt8 array value type.

**System Capability:** SystemCapability.DistributedDataManager.RelationalStore.Core

**Initial Version:** 22## type Assets

```cangjie
public type Assets = Array<Asset>
```

**Function:** [Assets](#type-assets) is a type alias for [Array\<Asset>](#class-asset).

## type ValuesBucket

```cangjie
public type ValuesBucket = Map<String, RelationalStoreValueType>
```

**Function:** [ValuesBucket](#type-valuesbucket) is a type alias for <!-- RP1 -->[Map\<String,RelationalStoreValueType>](https://gitcode.com/Cangjie/cangjie_docs/blob/main/docs/dev-guide/source_zh_cn/generic/generic_class.md)<!-- RP1End -->.