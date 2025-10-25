# ohos.data.data_share_predicates

谓词（data_share_predicates）是开发者通过DataShare查询数据库中的数据所使用的筛选条件，经常被应用在更新数据、删除数据和查询数据中。

谓词的接口函数与数据库的筛选条件一一对应，开发者在使用前需了解数据库相关知识。

## 导入模块

```cangjie
import kit.ArkData.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class DataSharePredicates

```cangjie
public class DataSharePredicates {
    public init()
}
```

**功能：** 提供用于不同实现不同查询方法的数据共享谓词。

> **说明：**
>
> 该类不是多线程安全的，如果应用中存在多线程同时操作该类派生出的实例，注意加锁保护。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

### init()

```cangjie
public init()
```

**功能：** DataSharePredicates的初始化构造函数。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

### func inValues(String, Array\<ValueType>)

```cangjie
public func inValues(field: String, value: Array<ValueType>): DataSharePredicates
```

**功能：** 用于配置谓词以匹配值在指范围内的字段。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|数据库表中的列名。|
|value|Array\<[ValueType](cj-apis-preferences.md#enum-valuetype)>|是|-|以ValueType数组形式指定的要匹配的值。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**示例：**

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

**功能：** 用于将和条件添加到谓词中。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 1 | Instance invalid. |

**示例：**

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

**功能：** 用于配置谓词以匹配值等于指定值的字段。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|数据库表中的列名。|
|value|[ValueType](cj-apis-preferences.md#enum-valuetype)|是|-|指示要与谓词匹配的值。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**示例：**

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

**功能：** 用于配置谓词以指定结果数和起始位置。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|total|Int32|是|-|指定结果数。|
|offset|Int32|是|-|指示起始位置。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**示例：**

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

**功能：** 用于配置谓词以匹配其值按升序排序的列。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|数据库表中的列名。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**示例：**

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

**功能：** 用于配置谓词以匹配其值按降序排序的列。目前仅RDB及KVDB(schema)支持该谓词。

**系统能力：** SystemCapability.DistributedDataManager.DataShare.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|field|String|是|-|数据库表中的列名。|

**返回值：**

|类型|说明|
|:----|:----|
|[DataSharePredicates](#class-datasharepredicates)|返回与指定字段匹配的谓词。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. |
| 1 | Instance invalid. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ArkData.*

let predicates = DataSharePredicates()
predicates.orderByDesc("AGE")
```
