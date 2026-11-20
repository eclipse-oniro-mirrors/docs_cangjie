# ohos.pasteboard（剪贴板）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

剪贴板模块提供应用内及跨应用的数据复制、粘贴能力，支持文本、HTML、URI、像素图等数据类型。

## 导入模块

```cangjie
import kit.BasicServicesKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## 权限列表

ohos.permission.READ_PASTEBOARD

## const MIMETYPE_PIXELMAP

```cangjie
public const MIMETYPE_PIXELMAP: String = "pixelMap"
```

**功能：** PixelMap内容的MIME类型。

**类型：** String

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## const MIMETYPE_TEXT_HTML

```cangjie
public const MIMETYPE_TEXT_HTML: String = "text/html"
```

**功能：** HTML内容的MIME类型。

**类型：** String

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## const MIMETYPE_TEXT_PLAIN

```cangjie
public const MIMETYPE_TEXT_PLAIN: String = "text/plain"
```

**功能：** 纯文本内容的MIME类型。

**类型：** String

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## const MIMETYPE_TEXT_URI

```cangjie
public const MIMETYPE_TEXT_URI: String = "text/uri"
```

**功能：** URI内容的MIME类型。

**类型：** String

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## const MIMETYPE_TEXT_WANT

```cangjie
public const MIMETYPE_TEXT_WANT: String = "text/want"
```

**功能：** Want内容的MIME类型。

**类型：** String

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## func createData(String, PasteDataValueType)

```cangjie
public func createData(mimeType: String, value: PasteDataValueType): PasteData
```

**功能：** 根据一个 MIME 类型和对应的值，构建仅含一条 PasteDataRecord 的剪贴板内容对象。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeType | String | 是 | 剪贴板数据对应的MIME类型，可以是常量中已定义的类型，包括 HTML 类型、纯文本类型、URI 类型、PixelMap 类型；也可以是自定义的MIME类型，开发者可自定义此参数值，mimeType长度不能超过1024字节。 |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | 是 | 自定义数据内容。建议根据实际场景选择合适的数据类型，使用过大的数据对象会影响应用复制粘贴性能和内存占用。对于ArrayBuffer类型，建议合理设置数据大小；对于PixelMap类型，建议及时释放不再使用的对象。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [PasteData](#class-pastedata) | 剪贴板内容对象。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    Hilog.info(0, "test", "createData success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

## func createData(HashMap\<String, PasteDataValueType>)

```cangjie
public func createData(data: HashMap<String, PasteDataValueType>): PasteData
```

**功能：** 构建包含多个数据类型的剪贴板内容对象。该对象仅含一条 PasteDataRecord，首个键值对的键为默认数据类型。HashMap 的遍历顺序不应作为业务依赖。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| data | HashMap\<String, [PasteDataValueType](#enum-pastedatavaluetype)> | 是 | Record的key为剪贴板数据对应的MIME类型。可以是常量中已定义的类型，包括 HTML 类型、纯文本类型、URI 类型、PixelMap 类型。也可以是自定义的MIME类型，可自定义此参数值，mimeType长度不能超过1024字节。 Record的value为key中指定MIME类型对应的数据。 Record中的首个key-value指定的MIME类型，会作为该 PasteDataRecord 的默认 MIME 类型，非默认类型的数据在粘贴时只能使用[getData](#func-getdataasynccallbackpastedata)接口读取。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [PasteData](#class-pastedata) | 剪贴板内容对象。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog
import std.collection.HashMap

try {
    let map = HashMap<String, PasteDataValueType>()
    map.add("text/plain", PasteDataValueType.StringValue("hello"))
    let data = createData(map)
    Hilog.info(0, "test", "createData success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

## func createRecord(String, PasteDataValueType)

```cangjie
public func createRecord(mimeType: String, value: PasteDataValueType): PasteDataRecord
```

**功能：** 创建一条指定类型的数据内容条目，将数据内容封装为PasteDataRecord对象。 调用此方法后，系统将根据MIME类型封装数据内容，返回可添加到PasteData中的条目对象。参数mimeType长度不能超过1024字节，value类型需与mimeType对应（如mimeType为"text/plain"，则value类型必须为StringValue），参数不能为空。

- 创建的条目通常需要通过[addRecord](#func-addrecordstring-pastedatavaluetype)方法添加到[PasteData](#class-pastedata)对象中才能生效。

- 典型使用流程：先通过[createData](#func-createdatahashmapstring-pastedatavaluetype)创建PasteData对象，再使用createRecord创建条目，最后通过addRecord添加条目。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeType | String | 是 | 剪贴板数据对应的MIME类型，可以是常量中已定义的类型，包括 HTML 类型、纯文本类型、URI 类型、PixelMap 类型；也可以是自定义的MIME类型，开发者可自定义此参数值，mimeType长度不能超过1024字节。 |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | 是 | 指定类型对应的数据内容。建议根据实际场景选择合适的数据类型，避免使用过大的数据对象以免影响剪贴板性能和内存占用。对于ArrayBuffer类型，建议合理设置数据大小；对于PixelMap类型，建议及时释放不再使用的对象。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [PasteDataRecord](#class-pastedatarecord) | 一条新建的指定类型的数据内容条目。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let record = createRecord("text/plain", PasteDataValueType.StringValue("hello"))
    Hilog.info(0, "test", "createRecord success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

## func getSystemPasteboard()

```cangjie
public func getSystemPasteboard(): SystemPasteboard
```

**功能：** 获取系统剪贴板服务入口对象。返回的对象可用于读取、写入、查询和清空剪贴板。每次调用可返回不同的包装对象，所有包装对象均操作同一个系统剪贴板服务。调用前剪贴板系统服务需要正常运行。在进行任何剪贴板读写操作前，都需要先调用此方法获取系统剪贴板对象。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [SystemPasteboard](#class-systempasteboard) | 系统剪贴板对象。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
Hilog.info(0, "test", "getSystemPasteboard success")
```

## class PasteData

```cangjie
public class PasteData {}
```

**功能：** 剪贴板内容对象。剪贴板内容包含一个或者多个内容条目（[PasteDataRecord](#class-pastedatarecord)）以及属性描述对象（[PasteDataProperty](#class-pastedataproperty)）。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### func addRecord(PasteDataRecord)

```cangjie
public func addRecord(record: PasteDataRecord): Unit
```

**功能：** 向当前剪贴板内容中添加一条条目，同时也会将条目类型添加到[PasteDataProperty](#class-pastedataproperty)的mimeTypes中。入参均不能为空，否则添加失败。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| record | [PasteDataRecord](#class-pastedatarecord) | 是 | 待添加的条目，设置后会将该条目添加到剪贴板内容中，同时更新mimeTypes属性列表。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.addRecord(createRecord("text/plain", PasteDataValueType.StringValue("hello")))
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func addRecord(String, PasteDataValueType)

```cangjie
public func addRecord(mimeType: String, value: PasteDataValueType): Unit
```

**功能：** 向当前剪贴板内容中添加一条条目，同时也会将条目类型添加到[PasteDataProperty](#class-pastedataproperty)的mimeTypes中。入参均不能为空，否则添加失败。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeType | String | 是 | 数据的MIME类型，取值范围：长度不超过1024字节。超出范围时抛出错误码 401 的 BusinessException。 |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | 是 | 数据内容，设置后更新剪贴板内容的属性信息，包括时间戳、数据类型、粘贴范围等。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.addRecord("text/plain", PasteDataValueType.StringValue("hello"))
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getMimeTypes()

```cangjie
public func getMimeTypes(): Array<String>
```

**功能：** 获取剪贴板中[PasteDataProperty](#class-pastedataproperty)的mimeTypes列表，未设置时返回空数组。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| Array\<String> | 剪贴板内容条目的数据类型，非重复的类型列表。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getMimeTypes()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getPrimaryHtml()

```cangjie
public func getPrimaryHtml(): String
```

**功能：** 获取首个 HTML 类型的内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | HTML 内容。剪贴板内容对象中没有 HTML 内容时，返回空字符串。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getPrimaryHtml()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getPrimaryMimeType()

```cangjie
public func getPrimaryMimeType(): String
```

**功能：** 获取剪贴板内容中首个条目的数据类型。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | 首个条目的数据类型。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getPrimaryMimeType()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getPrimaryPixelMap()

```cangjie
public func getPrimaryPixelMap(): PixelMap
```

**功能：** 获取首个 PixelMap 类型的内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| PixelMap | PixelMap 内容。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.ImageKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let colors = Array<UInt8>(16, repeat: 0xff)
    let pixelMap = createPixelMap(colors,
        InitializationOptions(Size(2, 2), editable: true, pixelFormat: PixelMapFormat.Rgba8888))
    let data = createData(MIMETYPE_PIXELMAP, PasteDataValueType.PixelMapValue(pixelMap))
    let primary = data.getPrimaryPixelMap()
    Hilog.info(0, "test", "PixelMap width: ${primary.getImageInfo().size.width}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getPrimaryText()

```cangjie
public func getPrimaryText(): String
```

**功能：** 获取首个纯文本类型的内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | 纯文本内容。剪贴板内容对象中没有纯文本内容时，返回空字符串。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getPrimaryText()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getPrimaryUri()

```cangjie
public func getPrimaryUri(): String
```

**功能：** 获取首个 URI 类型的内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | URI 内容。剪贴板内容对象中没有 URI 内容时，返回空字符串。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getPrimaryUri()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getProperty()

```cangjie
public func getProperty(): PasteDataProperty
```

**功能：** 获取剪贴板内容的属性描述对象。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [PasteDataProperty](#class-pastedataproperty) | 剪贴板内容属性。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getProperty()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getRecord(Int32)

```cangjie
public func getRecord(index: Int32): PasteDataRecord
```

**功能：** 获取剪贴板内容中指定下标的条目。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| index | Int32 | 是 | 指定条目的下标。有效取值范围：[0, getRecordCount()-1]，超出范围会触发错误码12900001。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [PasteDataRecord](#class-pastedatarecord) | 指定下标的条目。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getRecord(0)
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getRecordCount()

```cangjie
public func getRecordCount(): UIntNative
```

**功能：** 获取剪贴板内容中条目的个数。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| UIntNative | 条目的个数。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getRecordCount()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getTag()

```cangjie
public func getTag(): String
```

**功能：** 获取剪贴板内容中用户自定义的标签内容，如果没有设置用户自定义的标签内容将返回空。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | 返回用户自定义的标签内容，如果没有设置用户自定义的标签内容，将返回空。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.getTag()
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func hasType(String)

```cangjie
public func hasType(mimeType: String): Bool
```

**功能：** 检查剪贴板内容中是否有指定的MIME数据类型。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeType | String | 是 | 待查询的数据类型。可以是常量中已定义的类型，包括 HTML 类型、纯文本类型、URI 类型、PixelMap 类型；也可以是自定义的MIME类型，数据类型的字符串长度不能超过1024字节。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| Bool | 有指定的数据类型返回true。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.hasType("text/plain")
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func removeRecord(Int32)

```cangjie
public func removeRecord(index: Int32): Unit
```

**功能：** 移除剪贴板内容中指定下标的条目。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| index | Int32 | 是 | 指定的下标。有效取值范围：[0, getRecordCount()-1]，超出范围会触发错误码12900001。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.removeRecord(0)
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func replaceRecord(Int32, PasteDataRecord)

```cangjie
public func replaceRecord(index: Int32, record: PasteDataRecord): Unit
```

**功能：** 替换剪贴板内容中指定下标的条目。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| index | Int32 | 是 | 指定的下标。有效取值范围：[0, getRecordCount()-1]，超出范围会触发错误码12900001。 |
| record | [PasteDataRecord](#class-pastedatarecord) | 是 | 被替换后的条目数据内容，设置后会替换指定下标位置的原始条目。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.replaceRecord(0, createRecord("text/plain", PasteDataValueType.StringValue("new")))
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func setProperty(PasteDataProperty)

```cangjie
public func setProperty(pasteDataProperty: PasteDataProperty): Unit
```

**功能：** 设置剪贴板内容的属性。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| pasteDataProperty | [PasteDataProperty](#class-pastedataproperty) | 是 | 属性描述对象，设置后更新剪贴板内容的属性信息，包括时间戳、数据类型、粘贴范围等。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
    let result = data.setProperty(PasteDataProperty(["text/plain"], "tag", 0, false, ShareOption.Inapp))
    Hilog.info(0, "test", "success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

## class PasteDataProperty

```cangjie
public class PasteDataProperty {
    public init(mimeTypes: Array<String>, tag: String, timestamp: Int64, localOnly: Bool, shareOption: ShareOption)
}
```

**功能：** 定义剪贴板中所有内容条目的属性，包含时间戳、数据类型、粘贴范围以及一些附加数据等，该属性必须通过[setProperty](#func-setpropertypastedataproperty)方法，才能设置到剪贴板中。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop localOnly

```cangjie
public mut prop localOnly: Bool
```

**功能：** 配置剪贴板内容是否为“仅在本地”，true表示仅在本地有效，false表示允许跨设备传输。默认值为false。其值会被shareOption属性覆盖，推荐使用[ShareOption](#enum-shareoption)属性。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop mimeTypes

```cangjie
public prop mimeTypes: Array<String>
```

**功能：** 剪贴板内容条目的数据类型，非重复的类型列表。

**类型：** Array\<String>

**读写能力：** 只读

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop shareOption

```cangjie
public mut prop shareOption: ShareOption
```

**功能：** 指示剪贴板数据可以粘贴到的范围，默认值为 ShareOption.Localdevice。与localOnly属性互斥，设置shareOption会影响localOnly的实际值。

**类型：** [ShareOption](#enum-shareoption)

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop tag

```cangjie
public mut prop tag: String
```

**功能：** 用户自定义标签，默认为空。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop timestamp

```cangjie
public prop timestamp: Int64
```

**功能：** 剪贴板数据的写入时间戳（单位：已开机时间的ns数）。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### init(Array\<String>, String, Int64, Bool, ShareOption)

```cangjie
public init(mimeTypes: Array<String>, tag: String, timestamp: Int64, localOnly: Bool, shareOption: ShareOption)
```

**功能：** PasteDataProperty的构造函数。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeTypes | Array\<String> | 是 | 剪贴板内容条目的数据类型，非重复的类型列表。 |
| tag | String | 是 | 用户自定义标签，默认为空。 |
| timestamp | Int64 | 是 | 剪贴板数据的写入时间戳（单位：已开机时间的ns数）。 |
| localOnly | Bool | 是 | 配置剪贴板内容是否为“仅在本地”，true表示仅在本地有效，false表示允许跨设备传输。默认值为false。其值会被shareOption属性覆盖，推荐使用[ShareOption](#enum-shareoption)属性。 |
| shareOption | [ShareOption](#enum-shareoption) | 是 | 指示剪贴板数据可以粘贴到的范围，默认值为 ShareOption.Localdevice。与localOnly属性互斥，设置shareOption会影响localOnly的实际值。 |

## class PasteDataRecord

```cangjie
public class PasteDataRecord {}
```

**功能：** 对于剪贴板中内容记录的抽象定义，称之为条目。剪贴板内容部分由一个或者多个条目构成，例如一条文本内容、一份HTML、一个URI或者一个 PixelMap。不支持在创建PasteDataRecord之后，修改PasteDataRecord的默认数据类型的值，应在创建PasteDataRecord时指定正确的默认数据类型的值。可变属性可写，但修改不会生效。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop htmlText

```cangjie
public mut prop htmlText: String
```

**功能：** HTML内容，需符合标准HTML格式。对此属性的修改无效。该属性可写，但修改不会生效。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop mimeType

```cangjie
public mut prop mimeType: String
```

**功能：** 默认数据类型。对此属性的修改无效。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop pixelMap

```cangjie
public mut prop pixelMap: PixelMap
```

**功能：** PixelMap内容。对此属性的修改无效。该属性可写，但修改不会生效。

**类型：** PixelMap

**读写能力：** 只读

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop plainText

```cangjie
public mut prop plainText: String
```

**功能：** 纯文本内容。对此属性的修改无效。该属性可写，但修改不会生效。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### prop uri

```cangjie
public mut prop uri: String
```

**功能：** URI内容，需符合标准URI格式。对此属性的修改无效。该属性可写，但修改不会生效。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## class SystemPasteboard

```cangjie
public class SystemPasteboard {}
```

**功能：** 在调用SystemPasteboard的接口前，需要先通过[getSystemPasteboard](#func-getsystempasteboard)获取系统剪贴板。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### func clearData(AsyncCallback\<Unit>)

```cangjie
public func clearData(callback: AsyncCallback<Unit>): Unit
```

**功能：** 清空系统剪贴板内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | 回调函数。当成功清空时，err为None；否则为错误对象。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, _: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "clearData failed. Code: ${e.code}")
        case None => Hilog.info(0, "test", "clearData success")
    }
}
try {
    board.clearData(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getData(AsyncCallback\<PasteData>)

```cangjie
public func getData(callback: AsyncCallback<PasteData>): Unit
```

**功能：** 从系统剪贴板获取 PasteData。

应用使用自定义控件访问剪贴板内容需申请访问剪贴板权限。应用使用粘贴控件访问剪贴板内容，无需申请权限。

**需要权限：** ohos.permission.READ_PASTEBOARD

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[PasteData](#class-pastedata)> | 是 | 回调函数。当获取系统剪贴板中的 PasteData成功时，err为None，data为获取到的数据；否则err为错误对象。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，以下错误码的详细介绍请参见[通用错误码说明文档](../cj-errorcode-universal.md)和[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 27787277 | Another copy or paste operation is in progress. |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let callback: AsyncCallback<PasteData> = {
    err: Option<BusinessException>, data: Option<PasteData> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getData failed. Code: ${e.code}")
        case None => Hilog.info(0, "test", "getData success")
    }
}
try {
    board.getData(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func getDataSource()

```cangjie
public func getDataSource(): String
```

**功能：** 获取剪贴板数据的来源应用名称。适用于安全审计、数据追踪或向用户提示数据来源等场景。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | 数据来源的应用名称。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 12900005 | Excessive processing time for internal data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let result = board.getDataSource()
Hilog.info(0, "test", "result: ${result}")
```

### func hasData(AsyncCallback\<Bool>)

```cangjie
public func hasData(callback: AsyncCallback<Bool>): Unit
```

**功能：** 判断系统剪贴板中是否有内容。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Bool> | 是 | 回调函数，用于接收剪贴板是否有内容的判断结果。返回true表示系统剪贴板中有内容，返回false表示系统剪贴板中没有内容。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let callback: AsyncCallback<Bool> = {
    err: Option<BusinessException>, has: Option<Bool> => match (err) {
        case Some(e) => Hilog.error(0, "test", "hasData failed. Code: ${e.code}")
        case None => Hilog.info(0, "test", "hasData success")
    }
}
try {
    board.hasData(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

### func hasDataType(String)

```cangjie
public func hasDataType(mimeType: String): Bool
```

**功能：** 检查剪贴板内容中是否有指定类型的数据。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| mimeType | String | 是 | 数据类型，设置后用于检查剪贴板内容中是否存在该类型的特定数据。其长度不能超过1024字节，超出范围时抛出错误码 401 的 BusinessException。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| Bool | 检查剪贴板内容中是否有指定类型的数据。剪贴板内容中有指定类型的数据返回true；剪贴板内容中没有指定类型的数据返回false。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)和[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 401 | The parameter check failed. |
  | 12900005 | Excessive processing time for internal data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let result = board.hasDataType("text/plain")
Hilog.info(0, "test", "result: ${result}")
```

### func isRemoteData()

```cangjie
public func isRemoteData(): Bool
```

**功能：** 判断剪贴板中的数据是否来自其他设备。由于数据跨端传输耗时较大，如果剪贴板数据在远端设备上，不建议在UI线程执行检查剪贴板数据中是否包含自定义数据类型，或读取剪贴板数据。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| Bool | 判断剪贴板中的数据是否来自其他设备。剪贴板数据来自其他设备返回true；剪贴板数据来自本设备返回false。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 12900005 | Excessive processing time for internal data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let result = board.isRemoteData()
Hilog.info(0, "test", "result: ${result}")
```

### func setData(PasteData, AsyncCallback\<Unit>)

```cangjie
public func setData(data: PasteData, callback: AsyncCallback<Unit>): Unit
```

**功能：** 向系统剪贴板写入 PasteData。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| data | [PasteData](#class-pastedata) | 是 | 待写入系统剪贴板的 PasteData。文本数据长度受剪贴板服务约束。 |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | 回调函数。当设置系统剪贴板中的 PasteData成功时，err为None，否则为错误对象。 |

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[剪贴板错误码](./cj-errorcode-pasteboard.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 27787277 | Another copy or paste operation is in progress. |
  | 27787278 | Replication is prohibited. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let board = getSystemPasteboard()
let data = createData("text/plain", PasteDataValueType.StringValue("hello"))
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, _: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "setData failed. Code: ${e.code}")
        case None => Hilog.info(0, "test", "setData success")
    }
}
try {
    board.setData(data, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}")
}
```

## enum PasteDataValueType

```cangjie
public enum PasteDataValueType {
    | ArrayBufferValue(ArrayBuffer)
    | PixelMapValue(PixelMap)
    | StringValue(String)
    | ...
}
```

**功能：** 剪贴板数据类型枚举。

**扩展：**

- [extend PasteDataValueType \<: ToString](#extend-pastedatavaluetype--tostring)
- [extend PasteDataValueType \<: Equatable\<PasteDataValueType>](#extend-pastedatavaluetype--equatablepastedatavaluetype)

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### ArrayBufferValue(ArrayBuffer)

```cangjie
ArrayBufferValue(ArrayBuffer)
```

**功能：** 数组缓冲区类型的剪贴板数据。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### PixelMapValue(PixelMap)

```cangjie
PixelMapValue(PixelMap)
```

**功能：** 像素图类型的剪贴板数据。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### StringValue(String)

```cangjie
StringValue(String)
```

**功能：** 字符串类型的剪贴板数据。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## enum ShareOption

```cangjie
public enum ShareOption {
    | Inapp
    | Localdevice
    | ...
}
```

**功能：** 可粘贴数据的范围类型枚举。

**扩展：**

- [extend ShareOption \<: ToString](#extend-shareoption--tostring)
- [extend ShareOption \<: Equatable\<ShareOption>](#extend-shareoption--equatableshareoption)

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### Inapp

```cangjie
Inapp
```

**功能：** 表示仅允许同应用内粘贴。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

### Localdevice

```cangjie
Localdevice
```

**功能：** 表示仅允许在本设备的应用间粘贴。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

## extend PasteDataValueType \<: Equatable\<PasteDataValueType>

```cangjie
extend PasteDataValueType <: Equatable<PasteDataValueType>
```

**功能：** 为 PasteDataValueType 类型扩展 Equatable\<PasteDataValueType> 接口，支持相等比较。

**被扩展类型：**

- [PasteDataValueType](#enum-pastedatavaluetype)

**扩展接口：**

- Equatable\<[PasteDataValueType](#enum-pastedatavaluetype)>

### func ==(PasteDataValueType)

```cangjie
public operator func ==(other: PasteDataValueType): Bool
```

**功能：** 判断两个 PasteDataValueType 是否相等。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [PasteDataValueType](#enum-pastedatavaluetype) | 是 | 需要比较的PasteDataValueType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 PasteDataValueType 相等则返回 true，否则返回 false。|

### func !=(PasteDataValueType)

```cangjie
public operator func !=(other: PasteDataValueType): Bool
```

**功能：** 判断两个 PasteDataValueType 是否不相等。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [PasteDataValueType](#enum-pastedatavaluetype) | 是 | 需要比较的PasteDataValueType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 PasteDataValueType 不相等则返回 true，否则返回 false。|

## extend PasteDataValueType \<: ToString

```cangjie
extend PasteDataValueType <: ToString
```

**功能：** 为 PasteDataValueType 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [PasteDataValueType](#enum-pastedatavaluetype)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend ShareOption \<: Equatable\<ShareOption>

```cangjie
extend ShareOption <: Equatable<ShareOption>
```

**功能：** 为 ShareOption 类型扩展 Equatable\<ShareOption> 接口，支持相等比较。

**被扩展类型：**

- [ShareOption](#enum-shareoption)

**扩展接口：**

- Equatable\<[ShareOption](#enum-shareoption)>

### func ==(ShareOption)

```cangjie
public operator func ==(other: ShareOption): Bool
```

**功能：** 判断两个 ShareOption 是否相等。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [ShareOption](#enum-shareoption) | 是 | 需要比较的ShareOption对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 ShareOption 相等则返回 true，否则返回 false。|

### func !=(ShareOption)

```cangjie
public operator func !=(other: ShareOption): Bool
```

**功能：** 判断两个 ShareOption 是否不相等。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [ShareOption](#enum-shareoption) | 是 | 需要比较的ShareOption对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 ShareOption 不相等则返回 true，否则返回 false。|

## extend ShareOption \<: ToString

```cangjie
extend ShareOption <: ToString
```

**功能：** 为 ShareOption 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [ShareOption](#enum-shareoption)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.MiscServices.Pasteboard

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|
