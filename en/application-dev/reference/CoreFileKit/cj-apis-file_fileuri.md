# ohos.file.fileuri

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides the capability to obtain a Uniform Resource Identifier (URI) from a PATH, enabling subsequent file operations such as open, read, and write through [ohos.file_fs (File Management)](cj-apis-file_fs.md), thereby facilitating file sharing.

## Importing the Module

```cangjie
import kit.CoreFileKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of the example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details on the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie-Example-Code-Instructions).

## static func getUriFromPath(String)

```cangjie
public static func getUriFromPath(path: String): String
```

**Function:** Generates the application's own URI from the provided path (does not support obtaining media-type URIs). When converting a path to a URI, Chinese characters and non-alphanumeric special characters in the path will be encoded into corresponding ASCII codes and concatenated into the URI.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | The sandbox path of the file. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the file URI. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | The input parameter is invalid. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let uri = getUriFromPath("test.txt")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class FileUri

```cangjie
public class FileUri <: Uri {
    public init(uriOrPath: String)
}
```

**Function:** Provides interfaces for converting a URI to a shared path during sharing, generating the application's own URI from its sandbox path during sharing, and obtaining the URI of the directory path where the URI resides, facilitating URI access in file sharing operations.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Parent Type:**

- [Uri](#class-uri)

### prop name

```cangjie
public prop name: String
```

**Function:** Gets the filename corresponding to the FileUri.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

### prop path

```cangjie
public override prop path: String
```

**Function:** Gets the pathname corresponding to the FileUri.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

### init(String)

```cangjie

public init(uriOrPath: String)
```

**Function:** Constructor for FileUri.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| uriOrPath | String | Yes | - | URI or path. URI types: <br/>- Application sandbox URI: file://\<bundleName>/\<sandboxPath> <br/>- Public directory file URI: file://docs/storage/Users/currentUser/\<publicPath> <br/>- Public directory media URI: file://media/\<mediaType>/IMG_DATATIME_ID/\<displayName> |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900005 | I/O error |
  | 13900011 | Out of memory |
  | 13900020 | Invalid argument |
  | 13900042 | Unknown error |
  | 14300002 | Invalid uri |

### func toString()

```cangjie

public override func toString(): String
```

**Function:** Returns the URI as a string.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the URI as a string. |

## class Uri

```cangjie
public open class Uri <: ToString {
}
```

**Function:** Provides interfaces for converting a URI to a shared path during sharing, generating the application's own URI from its sandbox path during sharing, and obtaining the URI of the directory path where the URI resides, facilitating URI access in file sharing operations.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Parent Type:**

- ToString

### prop path

```cangjie
public override prop path: String
```

**Function:** Gets the pathname corresponding to the Uri. Intended for use by subclasses; direct use by users is not recommended and may throw an exception.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The prop is not supported. | Direct use. | Use the functions of the subclass. |

### func toString()

```cangjie
public open func toString(): String
```

**Function:** Returns the URI as a string. Intended for use by subclasses; direct use by users is not recommended and may throw an exception.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the URI as a string. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The function is not supported. | Direct use. | Use the functions of the subclass. |