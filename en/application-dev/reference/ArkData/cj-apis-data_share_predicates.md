# ohos.data.data_share_predicates

Predicates (data_share_predicates) are filtering conditions used by developers to query data in databases through DataShare, commonly applied in data updates, deletions, and queries.

The interface functions of predicates correspond one-to-one with database filtering conditions. Developers should understand relevant database knowledge before use.

## Import Module

```cangjie
import kit.ArkData.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the above sample project and configuration template, see [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class DataSharePredicates

```cangjie
public class DataSharePredicates {
    public init()
}
```

**Function:** Provides data sharing predicates for implementing different query methods.

> **Note:**
>
> This class is not thread-safe. If there are multiple threads in the application simultaneously operating instances derived from this class, ensure proper locking protection.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### init()

```cangjie
public init()
```

**Function:** Initialization constructor for DataSharePredicates.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

### func inValues(String, Array\<ValueType>)

```cangjie
public func inValues(field: String, value: Array<ValueType>): DataSharePredicates
```

**Function:** Configures the predicate to match fields with values within the specified range. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | Array\<[ValueType](cj-apis-preferences.md#enum-valuetype)> | Yes | - | Values to match, specified as a ValueType array. |

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*
import ohos.data.values_bucket.ValueType as VBValueType

let predicates = DataSharePredicates()
predicates.inValues("AGE", [VBValueType.Integer(18), VBValueType.Integer(20)])
```

### func and()

```cangjie
public func and(): DataSharePredicates
```

**Function:** Adds an AND condition to the predicate. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*
import ohos.data.values_bucket.ValueType as VBValueType

let predicates = DataSharePredicates()
predicates.equalTo("NAME", VBValueType.StringValue("lisi"))
        .and()
        .equalTo("SALARY", VBValueType.Double(200.5))
```

### func equalTo(String, ValueType)

```cangjie
public func equalTo(field: String, value: ValueType): DataSharePredicates
```

**Function:** Configures the predicate to match fields with values equal to the specified value. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | [ValueType](cj-apis-preferences.md#enum-valuetype) | Yes | - | Value to match with the predicate. |

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*
import ohos.data.values_bucket.ValueType as VBValueType

let predicates = DataSharePredicates()
predicates.equalTo("NAME", VBValueType.StringValue("Rose"))
```

### func limit(Int32, Int32)

```cangjie
public func limit(total: Int32, offset: Int32): DataSharePredicates
```

**Function:** Configures the predicate to specify the number of results and starting position. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| total | Int32 | Yes | - | Specifies the number of results. |
| offset | Int32 | Yes | - | Indicates the starting position. |

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*
import ohos.data.values_bucket.ValueType as VBValueType

let predicates = DataSharePredicates()
predicates.equalTo("NAME", VBValueType.StringValue("Rose")).limit(10, 3)
```

### func orderByAsc(String)

```cangjie
public func orderByAsc(field: String): DataSharePredicates
```

**Function:** Configures the predicate to match columns sorted in ascending order by their values. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*

let predicates = DataSharePredicates()
predicates.orderByAsc("AGE")
```

### func orderByDesc(String)

```cangjie
public func orderByDesc(field: String): DataSharePredicates
```

**Function:** Configures the predicate to match columns sorted in descending order by their values. Currently, only RDB and KVDB(schema) support this predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |

**Return Value:**

| Type | Description |
|:----|:----|
| [DataSharePredicates](#class-datasharepredicates) | Returns the predicate matching the specified field. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below.

| Error Code ID | Error Message |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*

let predicates = DataSharePredicates()
predicates.orderByDesc("AGE")
```