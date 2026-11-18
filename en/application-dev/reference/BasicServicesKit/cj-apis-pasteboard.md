# ohos.pasteboard (Pasteboard)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The Pasteboard module provides in-application and cross-application data copy and paste capabilities, and supports data types such as text, HTML, URI, and PixelMap.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of the sample code contains a "// index.cj" comment, the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample needs to obtain the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it must be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-notes).

## Permissions

ohos.permission.READ_PASTEBOARD

## const MIMETYPE_PIXELMAP

```cangjie
public const MIMETYPE_PIXELMAP: String = "pixelMap"
```

**Description:** MIME type of the PixelMap content.

**Type:** String

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Since:** 26.1.0

## const MIMETYPE_TEXT_HTML

```cangjie
public const MIMETYPE_TEXT_HTML: String = "text/html"
```

**Description:** MIME type of the HTML content.

**Type:** String

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Since:** 26.1.0

## const MIMETYPE_TEXT_PLAIN

```cangjie
public const MIMETYPE_TEXT_PLAIN: String = "text/plain"
```

**Description:** MIME type of the plain text content.

**Type:** String

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Since:** 26.1.0

## const MIMETYPE_TEXT_URI

```cangjie
public const MIMETYPE_TEXT_URI: String = "text/uri"
```

**Description:** MIME type of the URI content.

**Type:** String

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Since:** 26.1.0

## const MIMETYPE_TEXT_WANT

```cangjie
public const MIMETYPE_TEXT_WANT: String = "text/want"
```

**Description:** MIME type of the Want content.

**Type:** String

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Since:** 26.1.0

## func createData(String, PasteDataValueType)

```cangjie
public func createData(mimeType: String, value: PasteDataValueType): PasteData
```

**Description:** Builds a pasteboard content object that contains only one PasteDataRecord based on a MIME type and its value.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeType | String | Yes | - | MIME type of the pasteboard data. It can be a type defined in constants, including the HTML, plain text, URI, and PixelMap types; or a custom MIME type. Developers can customize this parameter value. The length of mimeType cannot exceed 1024 bytes. |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | Yes | - | Custom data content. Select an appropriate data type based on the actual scenario. An excessively large data object affects the copy and paste performance and memory usage of the application. For the ArrayBuffer type, set a proper data size. For the PixelMap type, release objects that are no longer used in a timely manner. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| [PasteData](#class-pastedata) | Pasteboard content object. |

**Example:**

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

**Description:** Builds a pasteboard content object containing multiple data types. The object contains only one PasteDataRecord, and the key of the first key-value pair is the default data type. Do not rely on the traversal order of HashMap.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| data | HashMap\<String, [PasteDataValueType](#enum-pastedatavaluetype)> | Yes | - | The key in the Record is the MIME type of the pasteboard data. It can be a type defined in constants, including the HTML, plain text, URI, and PixelMap types. It can also be a custom MIME type; this parameter value can be customized, and the length of mimeType cannot exceed 1024 bytes. The value in the Record is the data corresponding to the MIME type specified by the key. The MIME type specified by the first key-value pair in the Record is used as the default MIME type of the PasteDataRecord in the pasteboard content object. Data of non-default types can only be read through the [getData](#func-getdataasynccallbackpastedata) API during paste. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| [PasteData](#class-pastedata) | Pasteboard content object. |

**Example:**

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

**Description:** Creates a data content entry of a specified type and encapsulates the data content as a PasteDataRecord object. After this method is called, the system encapsulates the data content based on the MIME type and returns an entry object that can be added to PasteData. The length of the mimeType parameter cannot exceed 1024 bytes, and the value type must correspond to mimeType (for example, if mimeType is "text/plain", the value type must be StringValue). The parameters cannot be empty.

- The created entry usually takes effect only after it is added to the [PasteData](#class-pastedata) object through the [addRecord](#func-addrecordstring-pastedatavaluetype) method.

- Typical usage process: first create a PasteData object through [createData](#func-createdatahashmapstring-pastedatavaluetype), then create an entry using createRecord, and finally add the entry through addRecord.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeType | String | Yes | - | MIME type of the pasteboard data. It can be a type defined in constants, including the HTML, plain text, URI, and PixelMap types; or a custom MIME type. Developers can customize this parameter value. The length of mimeType cannot exceed 1024 bytes. |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | Yes | - | Data content corresponding to the specified type. Select an appropriate data type based on the actual scenario, and avoid excessively large data objects that affect the pasteboard performance and memory usage. For the ArrayBuffer type, set a proper data size. For the PixelMap type, release objects that are no longer used in a timely manner. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| [PasteDataRecord](#class-pastedatarecord) | A newly created data content entry of the specified type. |

**Example:**

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

**Description:** Obtains an entry object for the system pasteboard service. The returned object can be used to read, write, query, and clear the pasteboard. Each call may return a different wrapper object, but all wrapper objects operate on the same system pasteboard service. The pasteboard system service must be running properly before the call. Before any pasteboard read or write operation, call this method to obtain the system pasteboard object.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| [SystemPasteboard](#class-systempasteboard) | System pasteboard object. |

**Example:**

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

**Description:** Pasteboard content object. The pasteboard content includes one or more content entries ([PasteDataRecord](#class-pastedatarecord)) and a property description object ([PasteDataProperty](#class-pastedataproperty)).

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### func addRecord(PasteDataRecord)

```cangjie
public func addRecord(record: PasteDataRecord): Unit
```

**Description:** Adds an entry to the current pasteboard content and also adds the entry type to mimeTypes of [PasteDataProperty](#class-pastedataproperty). The input parameters cannot be empty; otherwise, the addition fails.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| record | [PasteDataRecord](#class-pastedatarecord) | Yes | - | Entry to be added. After it is set, the entry is added to the pasteboard content and the mimeTypes property list is updated. |

**Example:**

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

**Description:** Adds an entry to the current pasteboard content and also adds the entry type to mimeTypes of [PasteDataProperty](#class-pastedataproperty). The input parameters cannot be empty; otherwise, the addition fails.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeType | String | Yes | - | MIME type of the data. Value range: no more than 1024 bytes. If the value is out of range, a BusinessException with error code 401 is thrown. |
| value | [PasteDataValueType](#enum-pastedatavaluetype) | Yes | - | Data content. After it is set, the property information of the pasteboard content is updated, including the timestamp, data type, and paste range. |

**Example:**

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

**Description:** Obtains the mimeTypes list of [PasteDataProperty](#class-pastedataproperty) in the pasteboard. If no MIME types are set, an empty array is returned.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| Array\<String> | Data types of the pasteboard content entries. The list does not contain duplicate types. |

**Example:**

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

**Description:** Obtains the first HTML content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | HTML content. If the pasteboard content object does not contain HTML content, an empty string is returned. |

**Example:**

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

**Description:** Obtains the data type of the first entry in the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | Data type of the first entry. |

**Example:**

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

**Description:** Obtains the first PixelMap content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| PixelMap | PixelMap content. |

**Example:**

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

**Description:** Obtains the first plain text content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | Plain text content. If the pasteboard content object does not contain plain text content, an empty string is returned. |

**Example:**

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

**Description:** Obtains the first URI content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | URI content. If the pasteboard content object does not contain URI content, an empty string is returned. |

**Example:**

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

**Description:** Obtains the property description object of the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| [PasteDataProperty](#class-pastedataproperty) | Pasteboard content properties. |

**Example:**

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

**Description:** Obtains the entry at the specified index in the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| index | Int32 | Yes | - | Index of the specified entry. Valid value range: [0, getRecordCount()-1]. If the value is out of range, error code 12900001 is triggered. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| [PasteDataRecord](#class-pastedatarecord) | Entry at the specified index. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**Example:**

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

**Description:** Obtains the number of entries in the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| UIntNative | Number of entries. |

**Example:**

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

**Description:** Obtains the user-defined tag content in the pasteboard content. If no user-defined tag content is set, an empty value is returned.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | User-defined tag content. If no user-defined tag content is set, an empty value is returned. |

**Example:**

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

**Description:** Checks whether the pasteboard content contains the specified MIME data type.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeType | String | Yes | - | Data type to be queried. It can be a type defined in constants, including the HTML, plain text, URI, and PixelMap types; or a custom MIME type. The length of the data type string cannot exceed 1024 bytes. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| Bool | Returns true if the specified data type exists. |

**Example:**

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

**Description:** Removes the entry at the specified index from the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| index | Int32 | Yes | - | Specified index. Valid value range: [0, getRecordCount()-1]. If the value is out of range, error code 12900001 is triggered. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**Example:**

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

**Description:** Replaces the entry at the specified index in the pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| index | Int32 | Yes | - | Specified index. Valid value range: [0, getRecordCount()-1]. If the value is out of range, error code 12900001 is triggered. |
| record | [PasteDataRecord](#class-pastedatarecord) | Yes | - | Entry data content after replacement. After it is set, the original entry at the specified index is replaced. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 12900001 | The index is out of range. |

**Example:**

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

**Description:** Sets the pasteboard content properties.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| pasteDataProperty | [PasteDataProperty](#class-pastedataproperty) | Yes | - | Property description object. After it is set, the property information of the pasteboard content is updated, including the timestamp, data type, and paste range. |

**Example:**

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

**Description:** Defines the properties of all content entries in the pasteboard, including the timestamp, data type, paste range, and additional data. These properties can be set to the pasteboard only through the [setProperty](#func-setpropertypastedataproperty) method.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop localOnly

```cangjie
public mut prop localOnly: Bool
```

**Description:** Configures whether the pasteboard content is "local only". true indicates that the content is valid only locally, and false indicates that cross-device transmission is allowed. The default value is false. This value is overwritten by the shareOption property. You are advised to use the [ShareOption](#enum-shareoption) property.

**Type:** Bool

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop mimeTypes

```cangjie
public prop mimeTypes: Array<String>
```

**Description:** Data types of the pasteboard content entries. The list does not contain duplicate types.

**Type:** Array\<String>

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop shareOption

```cangjie
public mut prop shareOption: ShareOption
```

**Description:** Indicates the range to which the pasteboard data can be pasted. The default value is ShareOption.Localdevice. This property is mutually exclusive with the localOnly property. Setting shareOption affects the actual value of localOnly.

**Type:** [ShareOption](#enum-shareoption)

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop tag

```cangjie
public mut prop tag: String
```

**Description:** User-defined tag. The default value is empty.

**Type:** String

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop timestamp

```cangjie
public prop timestamp: Int64
```

**Description:** Timestamp when the pasteboard data is written (unit: number of ns since boot).

**Type:** Int64

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### init(Array\<String>, String, Int64, Bool, ShareOption)

```cangjie
public init(mimeTypes: Array<String>, tag: String, timestamp: Int64, localOnly: Bool, shareOption: ShareOption)
```

**Description:** Constructor of PasteDataProperty.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeTypes | Array\<String> | Yes | - | Data types of the pasteboard content entries. The list does not contain duplicate types. |
| tag | String | Yes | - | User-defined tag. The default value is empty. |
| timestamp | Int64 | Yes | - | Timestamp when the pasteboard data is written (unit: number of ns since boot). |
| localOnly | Bool | Yes | - | Configures whether the pasteboard content is "local only". true indicates that the content is valid only locally, and false indicates that cross-device transmission is allowed. The default value is false. This value is overwritten by the shareOption property. You are advised to use the [ShareOption](#enum-shareoption) property. |
| shareOption | [ShareOption](#enum-shareoption) | Yes | - | Indicates the range to which the pasteboard data can be pasted. The default value is ShareOption.Localdevice. This property is mutually exclusive with the localOnly property. Setting shareOption affects the actual value of localOnly. |

## class PasteDataRecord

```cangjie
public class PasteDataRecord {}
```

**Description:** Abstract definition of a content record in the pasteboard, called an entry. The pasteboard content consists of one or more entries, such as a text content, an HTML content, a URI, or a PixelMap. After a PasteDataRecord is created, the value of its default data type cannot be modified. Specify the correct default data type when creating the PasteDataRecord. Mutable properties can be written, but modifications do not take effect.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop htmlText

```cangjie
public mut prop htmlText: String
```

**Description:** HTML content, which must comply with the standard HTML format. Modifications to this property do not take effect. The property can be written, but modifications do not take effect.

**Type:** String

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop mimeType

```cangjie
public mut prop mimeType: String
```

**Description:** Default data type. Modifications to this property do not take effect.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop pixelMap

```cangjie
public mut prop pixelMap: PixelMap
```

**Description:** PixelMap content. Modifications to this property do not take effect. The property can be written, but modifications do not take effect.

**Type:** PixelMap

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop plainText

```cangjie
public mut prop plainText: String
```

**Description:** Plain text content. Modifications to this property do not take effect. The property can be written, but modifications do not take effect.

**Type:** String

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### prop uri

```cangjie
public mut prop uri: String
```

**Description:** URI content, which must comply with the standard URI format. Modifications to this property do not take effect. The property can be written, but modifications do not take effect.

**Type:** String

**Read/Write Capability:** Read-write

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

## class SystemPasteboard

```cangjie
public class SystemPasteboard {}
```

**Description:** Before calling APIs of SystemPasteboard, obtain the system pasteboard through [getSystemPasteboard](#func-getsystempasteboard) first.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### func clearData(AsyncCallback\<Unit>)

```cangjie
public func clearData(callback: AsyncCallback<Unit>): Unit
```

**Description:** Clears the system pasteboard content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | Yes | - | Callback function. When the content is cleared successfully, err is None; otherwise, err is an error object. |

**Example:**

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

**Description:** Obtains PasteData from the system pasteboard.

To access pasteboard content using a custom control, an application must request the pasteboard access permission. To access pasteboard content using a paste control, an application does not need to request the permission.

**Permission Required:** ohos.permission.READ_PASTEBOARD

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[PasteData](#class-pastedata)> | Yes | - | Callback function. When the PasteData in the system pasteboard is obtained successfully, err is None and data is the obtained data; otherwise, err is an error object. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details about the error codes, see the [Universal Error Code Documentation](../cj-errorcode-universal.md) and [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 27787277 | Another copy or paste operation is in progress. |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |

**Example:**

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

**Description:** Obtains the name of the application from which the pasteboard data comes. This API applies to scenarios such as security audit, data tracking, and prompting the data source to users.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | Name of the application from which the data comes. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 12900005 | Excessive processing time for internal data. |

**Example:**

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

**Description:** Checks whether the system pasteboard contains content.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Bool> | Yes | - | Callback function used to receive the check result of whether the pasteboard contains content. true indicates that the system pasteboard contains content, and false indicates that the system pasteboard does not contain content. |

**Example:**

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

**Description:** Checks whether the pasteboard content contains data of the specified type.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| mimeType | String | Yes | - | Data type. After it is set, it is used to check whether the pasteboard content contains specific data of this type. The length cannot exceed 1024 bytes. If the value is out of range, a BusinessException with error code 401 is thrown. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| Bool | Checks whether the pasteboard content contains data of the specified type. Returns true if the pasteboard content contains data of the specified type; returns false if the pasteboard content does not contain data of the specified type. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | The parameter check failed. |
  | 12900005 | Excessive processing time for internal data. |

**Example:**

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

**Description:** Checks whether the data in the pasteboard comes from another device. Because cross-device data transmission takes a long time, if the pasteboard data is on a remote device, do not check whether the pasteboard data contains a custom data type or read the pasteboard data on the UI thread.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| Bool | Checks whether the data in the pasteboard comes from another device. Returns true if the pasteboard data comes from another device; returns false if the pasteboard data comes from the local device. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 12900005 | Excessive processing time for internal data. |

**Example:**

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

**Description:** Writes PasteData to the system pasteboard.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| data | [PasteData](#class-pastedata) | Yes | - | PasteData to be written to the system pasteboard. The text data length is subject to the constraints of the pasteboard service. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | Yes | - | Callback function. When the PasteData in the system pasteboard is set successfully, err is None; otherwise, err is an error object. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The corresponding error codes are listed in the following table. For details, see [Pasteboard Error Codes](./cj-errorcode-pasteboard.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 27787277 | Another copy or paste operation is in progress. |
  | 27787278 | Replication is prohibited. |

**Example:**

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

**Description:** Pasteboard data type enumeration.

**Extensions:**

- [extend PasteDataValueType \<: ToString](#extend-pastedatavaluetype--tostring)
- [extend PasteDataValueType \<: Equatable\<PasteDataValueType>](#extend-pastedatavaluetype--equatablepastedatavaluetype)

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### ArrayBufferValue(ArrayBuffer)

```cangjie
ArrayBufferValue(ArrayBuffer)
```

**Description:** Pasteboard data of the array buffer type.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### PixelMapValue(PixelMap)

```cangjie
PixelMapValue(PixelMap)
```

**Description:** Pasteboard data of the pixel map type.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### StringValue(String)

```cangjie
StringValue(String)
```

**Description:** Pasteboard data of the string type.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

## enum ShareOption

```cangjie
public enum ShareOption {
    | Inapp
    | Localdevice
    | ...
}
```

**Description:** Range type enumeration for pasteable data.

**Extensions:**

- [extend ShareOption \<: ToString](#extend-shareoption--tostring)
- [extend ShareOption \<: Equatable\<ShareOption>](#extend-shareoption--equatableshareoption)

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### Inapp

```cangjie
Inapp
```

**Description:** Indicates that pasting is allowed only within the same application.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

### Localdevice

```cangjie
Localdevice
```

**Description:** Indicates that data can be pasted only between applications on the local device.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

## extend PasteDataValueType \<: Equatable\<PasteDataValueType>

```cangjie
extend PasteDataValueType <: Equatable<PasteDataValueType>
```

**Description:** Extends the Equatable\<PasteDataValueType> interface for the PasteDataValueType type to support equality comparison.

**Extended Type:**

- [PasteDataValueType](#enum-pastedatavaluetype)

**Extended Interfaces:**

- Equatable\<[PasteDataValueType](#enum-pastedatavaluetype)>

### func ==(PasteDataValueType)

```cangjie
public operator func ==(other: PasteDataValueType): Bool
```

**Description:** Checks whether two PasteDataValueType values are equal.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [PasteDataValueType](#enum-pastedatavaluetype) | Yes | - | PasteDataValueType object to be compared. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two PasteDataValueType values are equal; otherwise, returns false. |

### func !=(PasteDataValueType)

```cangjie
public operator func !=(other: PasteDataValueType): Bool
```

**Description:** Checks whether two PasteDataValueType values are not equal.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [PasteDataValueType](#enum-pastedatavaluetype) | Yes | - | PasteDataValueType object to be compared. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two PasteDataValueType values are not equal; otherwise, returns false. |

## extend PasteDataValueType \<: ToString

```cangjie
extend PasteDataValueType <: ToString
```

**Description:** Extends the ToString interface for the PasteDataValueType type to support string conversion.

**Extended Type:**

- [PasteDataValueType](#enum-pastedatavaluetype)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enumeration. |

## extend ShareOption \<: Equatable\<ShareOption>

```cangjie
extend ShareOption <: Equatable<ShareOption>
```

**Description:** Extends the Equatable\<ShareOption> interface for the ShareOption type to support equality comparison.

**Extended Type:**

- [ShareOption](#enum-shareoption)

**Extended Interfaces:**

- Equatable\<[ShareOption](#enum-shareoption)>

### func ==(ShareOption)

```cangjie
public operator func ==(other: ShareOption): Bool
```

**Description:** Checks whether two ShareOption values are equal.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [ShareOption](#enum-shareoption) | Yes | - | ShareOption object to be compared. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two ShareOption values are equal; otherwise, returns false. |

### func !=(ShareOption)

```cangjie
public operator func !=(other: ShareOption): Bool
```

**Description:** Checks whether two ShareOption values are not equal.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [ShareOption](#enum-shareoption) | Yes | - | ShareOption object to be compared. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two ShareOption values are not equal; otherwise, returns false. |

## extend ShareOption \<: ToString

```cangjie
extend ShareOption <: ToString
```

**Description:** Extends the ToString interface for the ShareOption type to support string conversion.

**Extended Type:**

- [ShareOption](#enum-shareoption)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.MiscServices.Pasteboard

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enumeration. |
