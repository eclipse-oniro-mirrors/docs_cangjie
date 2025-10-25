# ohos.data.preferences

用户首选项为应用提供Key-Value键值型的数据处理能力，支持应用持久化轻量级数据，并对其修改和查询。

数据存储形式为键值对，键的类型为字符串型，值的存储数据类型包括数字型、字符型、布尔型以及这3种类型的数组类型。

## 导入模块

```cangjie
import kit.ArkData.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。
- 正确的[dataGroupId](#var-datagroupid)需要向应用市场获取。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## const MAX_KEY_LENGTH

```cangjie
public const MAX_KEY_LENGTH: UInt32 = 1024
```

**功能：** Key的最大长度限制为1024个字节。

**类型：** UInt32

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

## const MAX_VALUE_LENGTH

```cangjie
public const MAX_VALUE_LENGTH: UInt32 = 16 * 1024 * 1024
```

**功能：** Value的最大长度限制为16 * 1024 * 1024个字节。

**类型：** UInt32

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

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

**功能：** Preferences实例配置选项。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### var dataGroupId

```cangjie
public var dataGroupId: String
```

**功能：** 应用组ID，需要向应用市场获取。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** Preferences实例的名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### var storageType

```cangjie
public var storageType: StorageType
```

**功能：** 存储模式，为可选参数。

**类型：** [StorageType](#enum-storagetype)

**读写能力：** 可读写

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### init(String, String, StorageType)

```cangjie
public init(name: String, dataGroupId!: String = String.empty,
    storageType!: StorageType = StorageType.Xml)
```

**功能：** 用于创建Options实例的构造函数。默认在本应用沙箱目录下创建Preferences实例。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|Preferences实例的名称。|
|dataGroupId|String|否|String.empty|应用组ID，需要向应用市场获取。|
|storageType|[StorageType](#enum-storagetype)|否|StorageType.Xml|存储模式，为可选参数。|

## class Preferences

```cangjie
public class Preferences {}
```

**功能：** 首选项类，提供获取和修改存储数据的接口。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### static func deletePreferences(UIAbilityContext, String)

```cangjie
public static func deletePreferences(context: UIAbilityContext, name: String): Unit
```

**功能：** 从缓存中移出指定的Preferences实例，若Preferences实例有对应的持久化文件，则同时删除其持久化文件。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|name|String|是|-|Preferences实例的名称。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |
| 15500010 | Failed to delete the user preferences persistence file. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*

// 获取 Preferences 实例
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore")  // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例
    Preferences.deletePreferences(Global.abilityContext, "myStore")
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "delete Preferences failed")
}
```

### static func deletePreferences(UIAbilityContext, Options)

```cangjie
public static func deletePreferences(context: UIAbilityContext, options: Options): Unit
```

**功能：** 从缓存中移出指定的Preferences实例，若Preferences实例有对应的持久化文件，则同时删除其持久化文件。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|options|[Options](#class-options)|是|-|与Preferences实例相关的配置选项。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 801 | Capability not supported. |
| 15500010 | Failed to delete the user preferences persistence file. |
| 15501001 | The operations is supported in stage mode only. |
| 15501002 | Invalid dataGroupId. |

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*

// 获取 Preferences 实例
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore")  // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例
    Preferences.deletePreferences(Global.abilityContext, "myStore")
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "delete Preferences failed")
}
```

### static func getPreferences(UIAbilityContext, String)

```cangjie
public static func getPreferences(context: UIAbilityContext, name: String): Preferences
```

**功能：** 从缓存中移出指定的Preferences实例。

应用首次调用[getPreferences](#static-func-getpreferencesuiabilitycontext-string)接口获取某个Preferences实例后，该实例会被会被缓存起来，后续再次[getPreferences](#static-func-getpreferencesuiabilitycontext-string)时不会再次从持久化文件中读取，直接从缓存中获取Preferences实例。调用此接口移出缓存中的实例之后，再次getPreferences将会重新读取持久化文件，生成新的Preferences实例。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|name|String|是|-|Preferences实例的名称。|

**返回值：**

|类型|说明|
|:----|:----|
|[Preferences](#class-preferences)|Preferences实例。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例的缓存
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### static func getPreferences(UIAbilityContext, Options)

```cangjie
public static func getPreferences(context: UIAbilityContext, options: Options): Preferences
```

**功能：** 从缓存中移出指定的Preferences实例。

应用首次调用[getPreferences](#static-func-getpreferencesuiabilitycontext-options)接口获取某个Preferences实例后，该实例会被会被缓存起来，后续再次[getPreferences](#static-func-getpreferencesuiabilitycontext-options)时不会再次从持久化文件中读取，直接从缓存中获取Preferences实例。调用此接口移出缓存中的实例之后，再次getPreferences将会重新读取持久化文件，生成新的Preferences实例。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|options|[Options](#class-options)|是|-|Preferences实例的名称。|

**返回值：**

|类型|说明|
|:----|:----|
|[Preferences](#class-preferences)|Preferences实例。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例的缓存
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### static func removePreferencesFromCache(UIAbilityContext, String)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, name: String): Unit
```

**功能：** 从缓存中移出指定的Preferences实例。

应用首次调用[getPreferences](#static-func-getpreferencesuiabilitycontext-string)接口获取某个Preferences实例后，该实例会被会被缓存起来，后续再次[getPreferences](#static-func-getpreferencesuiabilitycontext-string)时不会再次从持久化文件中读取，直接从缓存中获取Preferences实例。调用此接口移出缓存中的实例之后，再次getPreferences将会重新读取持久化文件，生成新的Preferences实例。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|name|String|是|-|Preferences实例的名称。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例的缓存
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### static func removePreferencesFromCache(UIAbilityContext, Options)

```cangjie
public static func removePreferencesFromCache(context: UIAbilityContext, options: Options): Unit
```

**功能：** 从缓存中移出指定的Preferences实例。

应用首次调用[getPreferences](#static-func-getpreferencesuiabilitycontext-options)接口获取某个Preferences实例后，该实例会被会被缓存起来，后续再次[getPreferences](#static-func-getpreferencesuiabilitycontext-options)时不会再次从持久化文件中读取，直接从缓存中获取Preferences实例。调用此接口移出缓存中的实例之后，再次getPreferences将会重新读取持久化文件，生成新的Preferences实例。

调用该接口后，不建议再使用旧的Preferences实例进行数据操作，否则会出现数据一致性问题。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|应用上下文。|
|options|[Options](#class-options)|是|-|Preferences实例的名称。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 801 | Capability not supported. |
| 15500000 | Inner error. |
| 15501001 | The operations is supported in stage mode only. |
| 15501002 | Invalid dataGroupId. |

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
| :---- | :--- | :--- |
| The context is invalid. | todo | todo |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
try {
    // 删除 Preferences 实例的缓存
    Preferences.removePreferencesFromCache(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID"))
} catch (e: Exception) {
    Hilog.error(0, "AppLogCj", "Failed to remove cache for preferences")
}
```

### func clear()

```cangjie
public func clear(): Unit
```

**功能：** 清除缓存的Preferences实例中的所有数据，可通过[flush](#func-flush)将Preferences实例持久化。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
preferences.put("myKey", PreferencesValueType.StringData("myValue"))
preferences.clear()
```

### func delete(String)

```cangjie
public func delete(key: String): Unit
```

**功能：** 从缓存的Preferences实例中删除名为给定Key的存储键值对，可通过[flush](#func-flush)将Preferences实例持久化。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|String|是|-|要删除的存储Key名称，不能为空。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*

// 获取 Preferences 实例
let preferences = Preferences.getPreferences(Global.abilityContext, "myStore") // 需获取Context应用上下文，详见本文使用说明
preferences.delete("startup")
```

### func flush()

```cangjie
public func flush(): Unit
```

**功能：** 将缓存的Preferences实例中的数据存储到用户首选项的持久化文件中。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
preferences.put("myKey", PreferencesValueType.StringData("myValue"))
preferences.flush()
```

### func get(String, ValueType)

```cangjie
public func get(key: String, defValue: ValueType): ValueType
```

**功能：** 从缓存的Preferences实例中获取键对应的值，如果该键不存在，返回默认数据defValue。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|String|是|-|要获取的存储Key名称。|
|defValue|[ValueType](#enum-valuetype)|是|-|默认返回值。支持Int64、Float64、String、Bool、 Array\<Bool>、Array\<Float64>、Array\<String>。|

**返回值：**

|类型|说明|
|:----|:----|
|[ValueType](#enum-valuetype)|返回键对应的值。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
var value = preferences.get("key", PreferencesValueType.Integer(0))
match (value) {
    case PreferencesValueType.Integer(n) => Hilog.info(0, "AppLogCj", "获取到的值为${n}")
    case _ => Hilog.info(0, "AppLogCj", "获取到的值并不是 Int")
}
```

### func getAll()

```cangjie
public func getAll(): HashMap<String, ValueType>
```

**功能：** 从缓存的Preferences实例中获取所有键值数据。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|HashMap\<String,[ValueType](#enum-valuetype)>|HashMap对象，返回含有所有键值数据。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Mandatory parameters are left unspecified. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
var values = preferences.getAll()
for ((k, v) in values) {
    match (v) {
        case Integer(n) => Hilog.info(0, "AppLogCj", "获得到的键值对key: ${k} value: ${n}")
        case Double(n) => Hilog.info(0, "AppLogCj", "获得到的键值对key: ${k} value: ${n}")
        case StringData(n) => Hilog.info(0, "AppLogCj", "获得到的键值对key: ${k} value: ${n}")
        case _ => Hilog.info(0, "AppLogCj", "其他值")
    }
}
```

### func has(String)

```cangjie
public func has(key: String): Bool
```

**功能：** 检查缓存的Preferences实例中是否包含名为给定Key的存储键值对。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|String|是|-|要检查的存储key名称。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|Bool值。返回Preferences实例是否包含给定key的存储键值对，true表示存在，false表示不存在。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.base.*

import kit.PerformanceAnalysisKit.Hilog

let preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
let hasKey = preferences.has("startup")
if (hasKey) {
    Hilog.info(0, "AppLogCj", "The key 'startup' is contained.")
} else {
    Hilog.info(0, "AppLogCj", "The key 'startup' dose not contain.")
}
```

### func off(PreferencesEvent, ?Callback1Argument\<String>)

```cangjie
public func off(event :PreferencesEvent, callback!: ?Callback1Argument<String> = None): Unit
```

**功能：** 取消订阅数据变更。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[PreferencesEvent](#enum-preferencesevent)|是|-|事件类型，表示取消订阅数据变更，或表示取消订阅进程间数据变更|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String>|否|None|需要取消的回调函数，不填写则全部取消。<br> String: 发生变化的Key的类型。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.data.preferences.ValueType as PValueType

import kit.PerformanceAnalysisKit.Hilog

// 此处代码可添加在依赖项定义中
// 回调函数
class Callback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
    }
}

var str = "container"
var a = Preferences.getPreferences(Global.abilityContext, str) // 需获取Context应用上下文，详见本文使用说明
var c = Callback()
a.on(PreferencesEvent.PreferencesChange, c)
a.off(PreferencesEvent.PreferencesChange)
a.put("kkk1", PValueType.StringData("vvv1"))
a.flush()
```

### func on(PreferencesEvent, Callback1Argument\<String>)

```cangjie
public func on(event :PreferencesEvent, callback: Callback1Argument<String>): Unit
```

**功能：** 订阅数据变更。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[PreferencesEvent](#enum-preferencesevent)|是|-|事件类型。<br> PreferencesChange 时，表示订阅数据变更，订阅的Key的值发生变更后，在执行flush方法后，触发callback回调。<br> PreferencesMultiProcessChange 时，表示订阅进程间数据变更，多个进程持有同一个首选项文件时，订阅的Key的值在任意一个进程发生变更后，执行flush方法后，触发callback回调。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<String>|是|-|回调函数。<br>String: 发生变化的Key的类型。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
import ohos.data.preferences.ValueType as PValueType

import kit.PerformanceAnalysisKit.Hilog

// 回调函数
class Callback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "AppLogCj", "=========callback========= ${arg.toString()}======================")
    }
}

var str = "container"
var a = Preferences.getPreferences(Global.abilityContext, str) // 需获取Context应用上下文，详见本文使用说明
var c = Callback()
a.on(PreferencesEvent.PreferencesChange, c)
a.put("kkk1", PValueType.StringData("vvv1"))
a.flush()
```

### func put(String, ValueType)

```cangjie
public func put(key: String, value: ValueType): Unit
```

**功能：** 将数据写入缓存的Preferences实例中，可通过[flush](#func-flush)将Preferences实例持久化。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|key|String|是|-|要修改的存储的Key，不能为空。|
|value|[ValueType](#enum-valuetype)|是|-|存储的新值。支持Int64、Float64、String、Bool、 Array\<Bool>、Array\<Float64>、Array\<String>。|

**异常：**

- BusinessException：对应错误码如下表。

| 错误码ID | 错误信息 |
| :---- | :--- |
| 401 | Parameter error. Possible causes:1. Mandatory parameters are left unspecified; 2. Incorrect parameter types;3. Parameter verification failed. |
| 15500000 | Inner error. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.ArkData.*
import ohos.data.preferences.Options as PreferencesOptions
import ohos.data.preferences.ValueType as PreferencesValueType

var preferences = Preferences.getPreferences(Global.abilityContext, PreferencesOptions("mystore", dataGroupId:"myGroupID")) // 需获取Context应用上下文，详见本文使用说明
preferences.put("Monday", PreferencesValueType.StringData("今天天气真好"))
```

## enum PreferencesEvent

```cangjie
public enum PreferencesEvent {
    | PreferencesChange
    | PreferencesMultiProcessChange
}
```

**功能：** Preferences的事件类型枚举。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### PreferencesChange

```cangjie
PreferencesChange
```

**功能：** 表示数据变更。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### PreferencesMultiProcessChange

```cangjie
PreferencesMultiProcessChange
```

**功能：** 表示多进程间的数据变更。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

## enum StorageType

```cangjie
public enum StorageType {
    | Xml
    | Gskv
}
```

**功能：** Preferences的存储模式枚举。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### Gskv

```cangjie
Gskv
```

**功能：** 表示GSKV存储模式。

**特点：** 数据以GSKV数据库模式进行存储。对数据的操作实时落盘，无需调用flush接口对数据进行落盘。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### Xml

```cangjie
Xml
```

**功能：** 表示XML存储模式，这是Preferences的默认存储模式。

**特点：** 数据XML格式进行存储。对数据的操作发生在内存中，需要调用flush接口进行落盘。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

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

**功能：** 表示支持的值类型。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### BoolArray(Array\<Bool>)

```cangjie
BoolArray(Array<Bool>)
```

**功能：** 表示值类型为布尔类型的数组。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### BoolData(Bool)

```cangjie
BoolData(Bool)
```

**功能：** 表示值类型为布尔值。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### Double(Float64)

```cangjie
Double(Float64)
```

**功能：** 表示值类型为64位浮点数类型。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### DoubleArray(Array\<Float64>)

```cangjie
DoubleArray(Array<Float64>)
```

**功能：** 表示值类型为64位浮点数类型的数组。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### Integer(Int64)

```cangjie
Integer(Int64)
```

**功能：** 表示值类型为64位有符号整型类型。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### StringArray(Array\<String>)

```cangjie
StringArray(Array<String>)
```

**功能：** 表示值类型为字符串类型的数组。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22

### StringData(String)

```cangjie
StringData(String)
```

**功能：** 表示值类型为字符串。

**系统能力：** SystemCapability.DistributedDataManager.Preferences.Core

**起始版本：** 22
