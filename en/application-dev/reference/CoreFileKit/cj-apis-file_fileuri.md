# ohos.file.fileuri

This module provides the capability to obtain Uniform Resource Identifiers (URIs) from file paths. Subsequent operations such as open, read, and write can be performed using [ohos.file_fs (File Management)](cj-apis-file_fs.md) to enable file sharing.

## Import Module

```cangjie
import kit.CoreFileKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## static func getUriFromPath(String)

```cangjie
public static func getUriFromPath(path: String): String
```

**Function:** Generates an application-specific URI from the provided path (does not support obtaining media-type URIs). When converting a path to a URI, Chinese characters and non-alphanumeric special characters in the path will be encoded into corresponding ASCII codes and concatenated into the URI.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Parameters:**

| Parameter | Type   | Mandatory | Default | Description                     |
| :------- | :----- | :-------- | :------ | :------------------------------ |
| path     | String | Yes       | -       | The sandbox path of the file.   |

**Return Value:**

| Type   | Description           |
| :----- | :-------------------- |
| String | Returns the file URI. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message                   |
  | :----------- | :------------------------------ |
  | 401          | The input parameter is invalid. |

## class FileUri

```cangjie
public class FileUri <: Uri {
    public init(uriOrPath: String)
}
```

**Function:** Provides interfaces for converting URIs to shared paths during sharing, generating application-specific URIs from sandbox paths, and obtaining the URI of the directory path where the URI resides. These capabilities facilitate URI access in file sharing operations.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Parent Type:**

- [Uri](#class-uri)

### prop name

```cangjie
public prop name: String
```

**Function:** Gets the filename corresponding to the FileUri.

**Type:** String

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

### prop path

```cangjie
public override prop path: String
```

**Function:** Gets the pathname corresponding to the FileUri.

**Type:** String

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

### init(String)

```cangjie
public init(uriOrPath: String)
```

**Function:** Constructor for FileUri.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Parameters:**

| Parameter  | Type   | Mandatory | Default | Description                                                                 |
| :-------- | :----- | :-------- | :------ | :-------------------------------------------------------------------------- |
| uriOrPath | String | Yes       | -       | URI or path. URI types:                                                    |
|           |        |           |         | - Application sandbox URI: file://\<bundleName>/\<sandboxPath>             |
|           |        |           |         | - Public directory file URI: file://docs/storage/Users/currentUser/\<publicPath> |
|           |        |           |         | - Public directory media URI: file://media/\<mediaType>/IMG_DATATIME_ID/\<displayName> |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message           |
  | :----------- | :---------------------- |
  | 13900005     | I/O error               |
  | 13900011     | Out of memory           |
  | 13900020     | Invalid argument        |
  | 13900042     | Unknown error           |
  | 14300002     | Invalid uri             |

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the URI as a string.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Return Value:**

| Type   | Description           |
| :----- | :-------------------- |
| String | Returns the URI as a string. |

## class Uri

```cangjie
public open class Uri <: ToString {
}
```

**Function:** Provides interfaces for converting URIs to shared paths during sharing, generating application-specific URIs from sandbox paths, and obtaining the URI of the directory path where the URI resides. These capabilities facilitate URI access in file sharing operations.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Parent Type:**

- ToString

### prop path

```cangjie
public override prop path: String
```

**Function:** Gets the pathname corresponding to the Uri. This is provided for subclasses and is not recommended for direct use by users; otherwise, an exception will be thrown.

**Type:** String

**Read-Write Capability:** Read-only

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Exceptions:**

- IllegalArgumentException:

  | Error Message           | Possible Cause       | Handling Steps                     |
  | :---------------------- | :------------------ | :-------------------------------- |
  | The prop is not supported. | Direct usage.       | Use functions from subclasses.    |

### func toString()

```cangjie
public open func toString(): String
```

**Function:** Returns the URI as a string. This is provided for subclasses and is not recommended for direct use by users; otherwise, an exception will be thrown.

**System Capability:** SystemCapability.FileManagement.AppFileService

**Since:** 21

**Return Value:**

| Type   | Description           |
| :----- | :-------------------- |
| String | Returns the URI as a string. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message           | Possible Cause       | Handling Steps                     |
  | :---------------------- | :------------------ | :-------------------------------- |
  | The function is not supported. | Direct usage.       | Use functions from subclasses.    |