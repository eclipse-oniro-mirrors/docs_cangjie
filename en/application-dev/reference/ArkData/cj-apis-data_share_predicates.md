# ohos.data.data_share_predicates

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Predicates (data_share_predicates) are filtering conditions used by developers to query data from databases through DataShare, commonly applied in data updates, deletions, and queries.

The interface functions of predicates correspond one-to-one with database filtering conditions. Developers should understand relevant database knowledge before use.

## Import Module

```cangjie
import kit.ArkData.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration is needed in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#Cangjie-Example-Code-Description).

## class DataSharePredicates

```cangjie
public class DataSharePredicates {
    public init()
}
```

**Function:** Provides data sharing predicates for implementing different query methods.

> **Note:**
>
> This class is not thread-safe. If multiple threads operate on instances derived from this class simultaneously in an application, ensure proper locking protection.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

### init()

```cangjie
public init()
```

**Function:** Initialization constructor for DataSharePredicates.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

### func inValues(String, Array\<VBValueType>)

```cangjie
public func inValues(field: String, value: Array<VBValueType>): DataSharePredicates
```

**Function:** Configures the predicate to match fields with values within a specified range.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | Array\<[VBValueType](cj-apis-values_bucket.md#enum-vbvaluetype)> | Yes | - | Values to match, specified as an array of VBValueType. |

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

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.inValues("AGE", [VBValueType.Integer(18), VBValueType.Integer(20)])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func and()

```cangjie
public func and(): DataSharePredicates
```

**Function:** Adds an AND condition to the predicate.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

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

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.equalTo("NAME", VBValueType.StringValue("lisi"))
            .and()
            .equalTo("SALARY", VBValueType.Double(200.5))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func equalTo(String, VBValueType)

```cangjie
public func equalTo(field: String, value: VBValueType): DataSharePredicates
```

**Function:** Configures the predicate to match fields with values equal to the specified value.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| field | String | Yes | - | Column name in the database table. |
| value | [VBValueType](./cj-apis-values_bucket.md#enum-vbvaluetype) | Yes | - | Value to match with the predicate. |

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

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.equalTo("NAME", VBValueType.StringValue("Rose"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func limit(Int32, Int32)

```cangjie
public func limit(total: Int32, offset: Int32): DataSharePredicates
```

**Function:** Configures the predicate to specify the number of results and starting position.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

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
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.equalTo("NAME", VBValueType.StringValue("Rose")).limit(10, 3)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func orderByAsc(String)

```cangjie
public func orderByAsc(field: String): DataSharePredicates
```

**Function:** Configures the predicate to match columns sorted in ascending order by their values.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

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
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.orderByAsc("AGE")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func orderByDesc(String)

```cangjie
public func orderByDesc(field: String): DataSharePredicates
```

**Function:** Configures the predicate to match columns sorted in descending order by their values.

**System Capability:** SystemCapability.DistributedDataManager.DataShare.Core

**Since:** 22

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
| 1 | Instance invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let predicates = DataSharePredicates()
    predicates.orderByDesc("AGE")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```