# ohos.file.fs (File Management)

This module provides basic file operation APIs, offering fundamental file handling capabilities including file basic management, directory management, file information statistics, and stream-based file read/write operations.

## Import Module

```cangjie
import kit.CoreFileKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.
- To obtain the current application sandbox path, use UIAbilityContext.[filesDir](../AbilityKit/cj-apis-app-ability-ui_ability.md#prop-filesdir).

For details about the example project and configuration template, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie示例代码说明).

## class ConflictFiles

```cangjie
public class ConflictFiles {
    public var srcFile: String
    public var destFile: String
}
```

**Function:** Conflict file information, supporting copyDir and moveDir interfaces.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var destFile

```cangjie
public var destFile: String
```

**Function:** Target conflict file path.

**Type:** String

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var srcFile

```cangjie
public var srcFile: String
```

**Function:** Source conflict file path.

**Type:** String

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

## class File

```cangjie
public class File {}
```

**Function:** File object opened via the open interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop fd

```cangjie
public prop fd: Int32
```

**Function:** Opened file descriptor.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop name

```cangjie
public prop name: String
```

**Function:** File name.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop path

```cangjie
public prop path: String
```

**Function:** File path.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### func getParent()

```cangjie
public func getParent(): String
```

**Function:** Get the parent directory path of the file corresponding to the File object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|Returns the parent directory path.|

**Exceptions:**

- BusinessException: Corresponding error codes as shown below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900005 | I/O error |
  | 13900042 | Unknown error |
  | 14300002 | Invalid URI |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with correct file path. Refer to usage instructions for obtaining file path
    let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    Hilog.info(0, "", "The parent path is: " + file.getParent())
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func tryLock(Bool)

```cangjie
public func tryLock(exclusive!: Bool = false): Unit
```

**Function:** Apply non-blocking shared or exclusive lock to a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|exclusive|Bool|No|false|**Named parameter.** Whether to apply an exclusive lock, default false.|

**Exceptions:**

- BusinessException: Corresponding error codes as shown below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900008 | Bad file descriptor |
  | 13900020 | Invalid argument |
  | 13900034 | Operation would block |
  | 13900042 | Unknown error |
  | 13900043 | No record locks available |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with correct file path. Refer to usage instructions for obtaining file path
    let file = FileIo.open(filePath, mode:(OpenMode.READ_WRITE | OpenMode.CREATE))
    file.tryLock(exclusive: true)
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func unlock()

```cangjie
public func unlock(): Unit
```

**Function:** Unlock a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes as shown below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900008 | Bad file descriptor |
  | 13900020 | Invalid argument |
  | 13900034 | Operation would block |
  | 13900042 | Unknown error |
  | 13900043 | No record locks available |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    file.tryLock(exclusive: true)
    file.unlock()
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class FileIo

```cangjie
public class FileIo {}
```

**Function:** Provides basic file operation capabilities.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static func access(String, AccessModeType, AccessFlagType)

```cangjie
public static func access(path: String, mode!: AccessModeType = AccessModeType.Exist,
    flag!: AccessFlagType = AccessFlagType.Local): Bool
```

**Function:** Check if a file exists or verify operation permissions. Failed read, write, or read-write permission checks will throw error code 13900012 (Permission denied).

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|path|String|Yes|-|Application sandbox path of the file or directory.|
|mode|[AccessModeType](#enum-accessmodetype)|No|AccessModeType.Exist|Permission to verify for the file or directory.|
|flag|[AccessFlagType](#enum-accessflagtype)|No|AccessFlagType.Local|Location to verify for the file or directory.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the file exists locally with verified permissions; returns false if the file doesn't exist or is on cloud or other distributed devices.|

**Exceptions:**

- BusinessException: Corresponding error codes as shown below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900020 | Invalid argument |
  | 13900023 | Text file busy |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException

let pathDir = "path/to/file"
let filePath = pathDir + "/test.txt"
try {
    let res = FileIo.access(filePath, mode: AccessModeType.Write, flag: AccessFlagType.Local)
    if (res) {
        Hilog.info(0, "test", "file exists", "")
    } else {
        Hilog.info(0, "test", "file not exists", "")
    }
} catch (e: BusinessException) {
    Hilog.error(0, "test", "access failed with error message: ${e.message}, error code: ${e.code}", "")
}
```

### static func close(Int32)

```cangjie
public static func close(file: Int32): Unit
```

**Function:** Close a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|file|Int32|Yes|-|Opened File object. After closing, the file object becomes meaningless and cannot be used for read/write operations.|

**Exceptions:**

- BusinessException: Corresponding error codes as shown below. For details, refer to [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900025 | No space left on device |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath)
    FileIo.close(file.fd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### static func close(File)

```cangjie
public static func close(file: File): Unit
```

**Function:** Closes a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | [File](#class-file) | Yes | - | The opened File object. After closing, the file object becomes meaningless and can no longer be used for read/write operations. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900025 | No space left on device |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath)
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func copyDir(String, String, Int32)

```cangjie
public static func copyDir(src: String, dest: String, mode!: Int32 = 0): Unit
```

**Function:** Copies a source directory to the target path.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | Application sandbox path of the source directory. |
| dest | String | Yes | - | Application sandbox path of the target directory. |
| mode | Int32 | No | 0 | **Named parameter.** Copy mode. Default mode is 0.<br/>- If mode is 0, exceptions are thrown at the file level. If the target directory contains a folder with the same name as the source directory and there are files with the same name in the conflicting folder, an exception is thrown. Non-conflicting files in the source directory are moved to the target directory, while non-conflicting files in the target directory remain unchanged. Conflict file information is provided in the `data` attribute of the thrown exception (ConfilictFileException) as an `Array<ConflictFiles>`.<br/>- If mode is 1, files are forcibly overwritten at the file level. If the target directory contains a folder with the same name as the source directory and there are files with the same name in the conflicting folder, all conflicting files are forcibly overwritten, while non-conflicting files remain unchanged. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900015 | File exists |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/"
    let destPath = pathDir + "/destDir/"
    FileIo.copyDir(srcPath, destPath, mode: 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func copyFile(String, String, Int32)

```cangjie
public static func copyFile(src: String, dest: String, mode!: Int32 = 0): Unit
```

**Function:** Copies a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | File descriptor of the source file to be copied. |
| dest | String | Yes | - | File descriptor of the target file. |
| mode | Int32 | No | 0 | **Named parameter.** Provides options for overwriting files. Currently, only mode 0 is supported, and it is the default.<br/>0: Completely overwrites the target file, and any non-overwritten parts are truncated. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/test.txt"
    let dstPath = pathDir + "/dstDir/test.txt"
    FileIo.copyFile(srcPath, dstPath, mode: 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func copyFile(String, Int32, Int32)

```cangjie
public static func copyFile(src: String, dest: Int32, mode!: Int32 = 0): Unit
```

**Function:** Copies a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | File descriptor of the source file to be copied. |
| dest | Int32 | Yes | - | File descriptor of the target file. |
| mode | Int32 | No | 0 | **Named parameter.** Provides options for overwriting files. Currently, only mode 0 is supported, and it is the default.<br/>0: Completely overwrites the target file, and any non-overwritten parts are truncated. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/test.txt"
    let dstPath = pathDir + "/dstDir/test.txt"
    let dstFile = FileIo.open(dstPath)
    FileIo.copyFile(srcPath, dstFile.fd, mode: 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func copyFile(Int32, String, Int32)

```cangjie
public static func copyFile(src: Int32, dest: String, mode!: Int32 = 0): Unit
```

**Function:** Copies a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | Int32 | Yes | - | File descriptor of the source file to be copied. |
| dest | String | Yes | - | File descriptor of the target file. |
| mode | Int32 | No | 0 | **Named parameter.** Provides options for overwriting files. Currently, only mode 0 is supported, and it is the default.<br/>0: Completely overwrites the target file, and any non-overwritten parts are truncated. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/test.txt"
    let dstPath = pathDir + "/dstDir/test.txt"
    let srcFile = FileIo.open(srcPath)
    FileIo.copyFile(srcFile.fd, dstPath, mode: 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func copyFile(Int32, Int32, Int32)

```cangjie
public static func copyFile(src: Int32, dest: Int32, mode!: Int32 = 0): Unit
```

**Function:** Copies a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | Int32 | Yes | - | File descriptor of the source file to be copied. |
| dest | Int32 | Yes | - | File descriptor of the target file. |
| mode | Int32 | No | 0 | **Named parameter.** Provides options for overwriting files. Currently, only mode 0 is supported, and it is the default.<br/>0: Completely overwrites the target file, and any non-overwritten parts are truncated. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/test.txt"
    let dstPath = pathDir + "/dstDir/test.txt"
    let srcFile = FileIo.open(srcPath)
    let dstFile = FileIo.open(dstPath)
    FileIo.copyFile(srcFile.fd, dstFile.fd, mode: 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func createRandomAccessFile(String, Int64, RandomAccessFileOptions)

```cangjie
public static func createRandomAccessFile(file: String, mode!: Int64 = OpenMode.READ_ONLY,
    options!: RandomAccessFileOptions = RandomAccessFileOptions()): RandomAccessFile
```

**Function:** Creates a RandomAccessFile object based on a file path or file object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | String | Yes | - | The opened File object. |
| mode | Int64 | No | OpenMode.READ_ONLY | **Named parameter.** Options for creating the RandomAccessFile object (see [OpenMode](#class-openmode)). This parameter takes effect only when a file sandbox path is passed. One of the following options must be specified. The default is read-only creation:<br/>- OpenMode.READ_ONLY(0o0): Creates in read-only mode.<br/>- OpenMode.WRITE_ONLY(0o1): Creates in write-only mode.<br/>- OpenMode.READ_WRITE(0o2): Creates in read-write mode.<br/>Additional functional options can be appended using bitwise OR. By default, no additional options are specified:<br/>- OpenMode.CREATE(0o100): Creates the file if it does not exist.<br/>- OpenMode.TRUNC(0o1000): If the RandomAccessFile object exists and the file has write permissions, its length is truncated to zero.<br/>- OpenMode.APPEND(0o2000): Opens in append mode. Subsequent writes will append to the end of the RandomAccessFile object.<br/>- OpenMode.NONBLOCK(0o4000): If the path points to a FIFO, block special file, or character special file, this open and subsequent I/O operations will be non-blocking.<br/>- OpenMode.DIR(0o200000): Raises an error if the path does not point to a directory. Write permissions cannot be appended.<br/>- OpenMode.NOFOLLOW(0o400000): Raises an error if the path points to a symbolic link.<br/>- OpenMode.SYNC(0o4010000): Creates the RandomAccessFile object in synchronous I/O mode. |
| options | [RandomAccessFileOptions](#class-randomaccessfileoptions) | No | RandomAccessFileOptions() | Supports the following options:<br/>- start: A number indicating the desired starting position for reading the file. Optional; defaults to the current position.<br/>- end: A number indicating the desired ending position for reading the file. Optional; defaults to the end of the file. |

**Return Value:**

| Type | Description |
|:----|:----|
| [RandomAccessFile](#class-randomaccessfile) | Returns the RandomAccessFile object. |

**Exceptions:**

- BusinessException: Corresponding### static func createRandomAccessFile(File, Int64, RandomAccessFileOptions)

```cangjie
public static func createRandomAccessFile(file: File, mode!: Int64 = OpenMode.READ_ONLY,
    options!: RandomAccessFileOptions = RandomAccessFileOptions()): RandomAccessFile
```

**Function:** Creates a RandomAccessFile object based on a file path or File object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | [File](#class-file) | Yes | - | An opened File object. |
| mode | Int64 | No | OpenMode.READ_ONLY | Options for creating the RandomAccessFile object. Only effective when a sandbox file path is provided. Must specify one of the following options (default is read-only creation):<br/>- OpenMode.READ_ONLY(0o0): Create in read-only mode.<br/>- OpenMode.WRITE_ONLY(0o1): Create in write-only mode.<br/>- OpenMode.READ_WRITE(0o2): Create in read-write mode.<br/>Additional functional options can be appended via bitwise OR (default is no extra options):<br/>- OpenMode.CREATE(0o100): Create the file if it does not exist.<br/>- OpenMode.TRUNC(0o1000): Truncate the file length to zero if the RandomAccessFile object exists and has write permissions.<br/>- OpenMode.APPEND(0o2000): Open in append mode; subsequent writes will append to the end of the RandomAccessFile object.<br/>- OpenMode.NONBLOCK(0o4000): Perform non-blocking operations if the path points to a FIFO, block special file, or character special file.<br/>- OpenMode.DIR(0o200000): Error if the path does not point to a directory. Write permissions cannot be appended.<br/>- OpenMode.NOFOLLOW(0o400000): Error if the path points to a symbolic link.<br/>- OpenMode.SYNC(0o4010000): Create the RandomAccessFile object in synchronous I/O mode. |
| options | [RandomAccessFileOptions](#class-randomaccessfileoptions) | No | RandomAccessFileOptions() | Supported options:<br/>- start: number type, indicates the desired starting position for reading the file (optional, defaults to the current position).<br/>- end: number type, indicates the desired ending position for reading the file (optional, defaults to the end of the file). |

**Return Value:**

| Type | Description |
|:----|:----|
| [RandomAccessFile](#class-randomaccessfile) | Returns the RandomAccessFile object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900006 | No such device or address |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900017 | No such device |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900029 | Resource deadlock would occur |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    FileIo.write(file.fd, "hello world")
    FileIo.fdatasync(file.fd)
    let randomAccessFile = FileIo.createRandomAccessFile(file)
    randomAccessFile.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func createStream(String, String)

```cangjie
public static func createStream(path: String, mode: String): Stream
```

**Function:** Creates a file stream based on a file path.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | The application sandbox path of the file. |
| mode | String | Yes | - | - r: Open a read-only file (the file must exist).<br/>- r+: Open a readable and writable file (the file must exist).<br/>- w: Open a write-only file. If the file exists, its length is truncated to zero (i.e., the file content is erased). If the file does not exist, it is created.<br/>- w+: Open a readable and writable file. If the file exists, its length is truncated to zero (i.e., the file content is erased). If the file does not exist, it is created.<br/>- a: Open a write-only file in append mode. If the file does not exist, it is created. If the file exists, data is appended to the end (i.e., the original content is preserved).<br/>- a+: Open a readable and writable file in append mode. If the file does not exist, it is created. If the file exists, data is appended to the end (i.e., the original content is preserved). |

**Return Value:**

| Type | Description |
|:----|:----|
| [Stream](#class-stream) | Returns the file stream result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900006 | No such device or address |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900017 | No such device |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900029 | Resource deadlock would occur |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let stream = FileIo.createStream(filePath, "r+")
    Hilog.info(0, "test", "createStream succeed", "")
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func dup(Int32)

```cangjie
public static func dup(fd: Int32): File
```

**Function:** Converts a file descriptor into a File object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor. |

**Return Value:**

| Type | Description |
|:----|:----|
| [File](#class-file) | The opened File object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900014 | Device or resource busy |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file1 = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    let fd = file1.fd
    let file2 = FileIo.dup(fd)
    Hilog.info(0, "test", "The name of the file2 is ${file2.name}", "")
    FileIo.close(file1)
    FileIo.close(file2)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func fdatasync(Int32)

```cangjie
public static func fdatasync(fd: Int32): Unit
```

**Function:** Synchronizes file data content synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The opened file descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath)
    FileIo.fdatasync(file.fd)
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func fdopenStream(Int32, String)

```cangjie
public static func fdopenStream(fd: Int32, mode: String): Stream
```

**Function:** Opens a file stream synchronously based on a file descriptor.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The opened file descriptor. |
| mode | String | Yes | - | - r: Open a read-only file (the file must exist).<br/>- r+: Open a readable and writable file (the file must exist).<br/>- w: Open a write-only file (if the file exists, its content will be overwritten).<br/>- w+: Open a readable and writable file (if the file exists, its content will be overwritten).<br/>- a: Open a write-only file in append mode (data will be appended to the end of the file, preserving the original content).<br/>- a+: Open a readable and writable file in append mode (data will be appended to the end of the file, preserving the original content). |

**Return Value:**

| Type | Description |
|:----|:----|
| [Stream](#class-stream) | Returns the file stream result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900006 | No such device or address |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900017 | No such device |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900029 | Resource deadlock would occur |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.READ_ONLY | OpenMode.CREATE))
    let stream = FileIo.fdopenStream(file.fd, "r+")
    FileIo.close(file)
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func fsync(Int32)

```cangjie
public static func fsync(fd: Int32): Unit
```

**Function:** Synchronizes file data synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The opened file descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath)
    FileIo.fsync(file.fd)
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### static func listFile(String, ListFileOptions)

```cangjie
public static func listFile(path: String, options!: ListFileOptions = ListFileOptions()): Array<String>
```

**Function:** Synchronously lists all filenames under a directory, supports recursive listing (including subdirectories), and supports file filtering.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the directory. |
| options | [ListFileOptions](#class-listfileoptions) | No | ListFileOptions() | File filtering options. No filtering by default. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns an array of filenames. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900018 | Not a directory |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filter = Filter(suffix: [".png", ".jpg", ".jpeg"], displayName: ["*abc", "efg*"])
    let listFileOptions = ListFileOptions(recursion: false, listNum: 0, filter: filter)
    let filenames = FileIo.listFile(pathDir, options: listFileOptions)
    for (name in filenames) {
        Hilog.info(0, "test", name, "")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func lseek(Int32, Int64, WhenceType)

```cangjie
public static func lseek(fd: Int32, offset: Int64, whence!: WhenceType = SeekSet): Int64
```

**Function:** Adjusts the file offset pointer position.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | File descriptor. |
| offset | Int64 | Yes | - | Relative offset position. |
| whence | [WhenceType](#enum-whencetype) | No | SeekSet | Type of offset pointer relative position. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Current file offset pointer position (relative to the start of the file). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900008 | Bad file descriptor |
  | 13900020 | Invalid argument |
  | 13900026 | Illegal seek |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: OpenMode.CREATE)
    let offset = FileIo.lseek(file.fd, 5, whence: WhenceType.SeekSet)
    Hilog.info(0, "test", "The current offset is at ${offset.toString()}", "")
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func lstat(String)

```cangjie
public static func lstat(path: String): Stat
```

**Function:** Synchronously retrieves symbolic link file information.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the file. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Stat](#class-stat) | Represents detailed file information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/linkToFile"
    let fileStat = FileIo.lstat(filePath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func mkdir(String)

```cangjie
public static func mkdir(path: String): Unit
```

**Function:** Creates a directory.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the directory. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900015 | File exists |
  | 13900018 | Not a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900028 | Too many links |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/testDir1/testDir2/testDir3"
    FileIo.mkdir(dirPath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func mkdir(String, Bool)

```cangjie
public static func mkdir(path: String, recursion: Bool): Unit
```

**Function:** Creates a directory. When `recursion` is set to `true`, multi-level directories can be created.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the directory. |
| recursion | Bool | Yes | - | Whether to create multi-level directories. When `recursion` is `true`, multi-level directories can be created. When `recursion` is `false`, only a single-level directory can be created. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900015 | File exists |
  | 13900018 | Not a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900028 | Too many links |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/testDir1/testDir2/testDir3"
    FileIo.mkdir(dirPath, true)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func mkdtemp(String)

```cangjie
public static func mkdtemp(prefix: String): String
```

**Function:** Synchronously creates a temporary directory.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| prefix | String | Yes | - | Specifies the directory path, which must end with "XXXXXX". The "XXXXXX" at the end of the path will be replaced with random characters to create a unique directory name. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Generated unique directory path. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900015 | File exists |
  | 13900018 | Not a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900028 | Too many links |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let res = FileIo.mkdtemp(pathDir + "/XXXXXX")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func moveDir(String, String, Int32)

```cangjie
public static func moveDir(src: String, dest: String, mode!: Int32 = 0): Unit
```

**Function:** Moves a source directory to the target path.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | Application sandbox path of the source directory. |
| dest | String | Yes | - | Application sandbox path of the target directory. |
| mode | Int32 | No | 0 | Move mode. Default mode is 0.<br/>- Mode 0: Directory-level exception. If the target directory contains a non-empty directory with the same name as the source directory, an exception is thrown.<br/>- Mode 1: File-level exception. If the target directory contains a directory with the same name as the source directory, and there are conflicting files within, an exception is thrown. Non-conflicting files from the source directory are moved to the target directory, and non-conflicting files in the target directory are retained. Conflict file information is provided in the `data` attribute of the thrown exception (ConfilictFileException) as an Array\<ConflictFiles>.<br/>- Mode 2: File-level force overwrite. If the target directory contains a directory with the same name as the source directory, and there are conflicting files within, all conflicting files are forcibly overwritten. Non-conflicting files are retained.<br/>- Mode 3: Directory-level force overwrite. Moves the source directory to the target directory, ensuring the target directory's contents match the source directory exactly. If the target directory contains a directory with the same name as the source directory, all original files in that directory will not be retained. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900016 | Cross-device link |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900028 | Too many links |
  | 13900032 | Directory not empty |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    // move directory from srcPath to destPath
    let srcPath = pathDir + "/srcDir/"
    let destPath = pathDir + "/destDir/"
    FileIo.moveDir(srcPath, destPath, mode: 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### static func moveFile(String, String, Int32)

```cangjie
public static func moveFile(src: String, dest: String, mode!: Int32 = 0): Unit
```

**Function:** Moves the source folder to the target path.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | Application sandbox path of the source folder. |
| dest | String | Yes | - | Application sandbox path of the target folder. |
| mode | Int32 | No | 0 | Move mode. Default mode is 0.<br/>- Mode 0: Throws an exception at folder level. If a non-empty folder with the same name as the source folder exists in the target folder, an exception is thrown.<br/>- Mode 1: Throws an exception at file level. If a folder with the same name as the source folder exists in the target folder and contains files with the same names, an exception is thrown. Non-conflicting files from the source folder are moved to the target folder, while non-conflicting files in the target folder remain unchanged. Conflict file information is provided in the `data` attribute of the thrown exception (ConfilictFileException) as an Array\<ConflictFiles>.<br/>- Mode 2: Force overwrite at file level. If a folder with the same name as the source folder exists in the target folder and contains files with the same names, all conflicting files in the target folder are forcibly overwritten, while non-conflicting files remain unchanged.<br/>- Mode 3: Force overwrite at folder level. Moves the source folder to the target folder, ensuring the contents of the moved folder in the target folder are identical to the source folder. If a folder with the same name as the source folder exists in the target folder, all original files in that folder will not be retained. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900016 | Cross-device link |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900028 | Too many links |
  | 13900032 | Directory not empty |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcPath = pathDir + "/srcDir/"
    let destPath = pathDir + "/destDir/"
    FileIo.moveFile(srcPath, destPath, mode: 0)
    Hilog.info(0, "test", "move file succeed", "")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func open(String, Int64)

```cangjie
public static func open(path: String, mode!: Int64 = OpenMode.READ_ONLY): File
```

**Function:** Opens a file synchronously. Supports opening files using URIs.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path or URI of the file to open. |
| mode | Int64 | No | OpenMode.READ_ONLY | File opening options. Must specify one of the following options, default is read-only:<br/>- OpenMode.READ_ONLY(0o0): Open for reading only.<br/>- OpenMode.WRITE_ONLY(0o1): Open for writing only.<br/>- OpenMode.READ_WRITE(0o2): Open for reading and writing.<br/>Additional options can be appended using bitwise OR, default is no additional options:<br/>- OpenMode.CREATE(0o100): Create the file if it does not exist.<br/>- OpenMode.TRUNC(0o1000): If the file exists and is writable, truncate its length to zero.<br/>- OpenMode.APPEND(0o2000): Open in append mode; subsequent writes will append to the end of the file.<br/>- OpenMode.NONBLOCK(0o4000): If path points to a FIFO, block special file, or character special file, this open and subsequent I/O operations will be non-blocking.<br/>- OpenMode.DIR(0o200000): If path does not point to a directory, an error occurs. Writing is not allowed.<br/>- OpenMode.NOFOLLOW(0o400000): If path points to a symbolic link, an error occurs.<br/>- OpenMode.SYNC(0o4010000): Open the file in synchronous I/O mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| [File](#class-file) | The opened File object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900006 | No such device or address |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900017 | No such device |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900029 | Resource deadlock would occur |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900034 | Operation would block |
  | 13900038 | Value too large for defined data type |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    Hilog.info(0, "test", "open file success, file fd: ${file.fd.toString()}", "")
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func read(Int32, Array\<Byte>, ReadOptions)

```cangjie
public static func read(fd: Int32, buffer: Array<Byte>, options!: ReadOptions = ReadOptions()): Int64
```

**Function:** Reads data from a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor of the opened file. |
| buffer | Array\<Byte> | Yes | - | Buffer to store the read file data. |
| options | [ReadOptions](#class-readoptions) | No | ReadOptions() | Supports the following options:<br/>- offset, Int64 type, indicates the desired position to read from the file. Default is the current position.<br/>- length, UIntNative type, indicates the desired length of data to read. Default is the buffer length. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the actual length of data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900034 | Operation would block |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.READ_WRITE | OpenMode.CREATE))
    let buf = Array<Byte>(4096, repeat: 0)
    FileIo.read(file.fd, buf)
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func readLines(String, Options)

```cangjie
public static func readLines(filePath: String, options!: Options = Options()): ReaderIterator
```

**Function:** Reads file text content line by line synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| filePath | String | Yes | - | Application sandbox path of the file. |
| options | [Options](#class-options) | No | Options() | Optional. Supports the following options:<br/>- encoding, String type, valid when data is of String type, indicates the encoding method of the data. Default is "utf-8", and only "utf-8" is supported. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ReaderIterator](#class-readeriterator) | Returns a file reader iterator. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900012 | Permission denied |
  | 13900015 | File exists |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900022 | Too many open files |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let options: Options = Options(encoding: "utf-8")
    let readerIterator = FileIo.readLines(filePath, options: options)
    var result = readerIterator.next()
    while (!result.done) {
        Hilog.info(0, "test", "content: ${result.value}", "")
        result = readerIterator.next()
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func readText(String, ReadTextOptions)

```cangjie
public static func readText(filePath: String, options!: ReadTextOptions = ReadTextOptions()): String
```

**Function:** Reads file content as text synchronously (i.e., directly reads the text content of the file).

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| filePath | String | Yes | - | Application sandbox path of the file. |
| options | [ReadTextOptions](#class-readtextoptions) | No | ReadTextOptions() | Supports the following options:<br/>- offset, Int64 type, indicates the desired position to read from the file. Optional, default is the starting position.<br/>- length, Int64 type, indicates the desired length of data to read. Optional, default is the file length.<br/>- encoding, String type, valid when data is of String type, indicates the encoding method of the data. Default is "utf-8", and only "utf-8" is supported. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the content read from the file. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let str = FileIo.readText(filePath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func rename(String, String)

```cangjie
public static func rename(oldPath: String, newPath: String): Unit
```

**Function:** Renames a file or folder.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| oldPath | String | Yes | - | Original application sandbox path of the file. |
| newPath | String | Yes | - | New application sandbox path of the file. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900015 | File exists |
  | 13900016 | Cross-device link |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900025 | No space left on device |
  | 13900027 | Read-only file system |
  | 13900028 | Too many links |
  | 13900032 | Directory not empty |
  | 13900033 | Too many symbolic links encountered |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let srcFile = pathDir + "/test.txt"
    let dstFile = pathDir + "/new.txt"
    FileIo.rename(srcFile, dstFile)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### static func rmdir(String)

```cangjie
public static func rmdir(path: String): Unit
```

**Function:** Delete a directory.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the directory. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900018 | Not a directory |
  | 13900020 | Invalid argument |
  | 13900027 | Read-only file system1 |
  | 13900030 | File name too long |
  | 13900032 | Directory not empty |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/testDir"
    FileIo.rmdir(dirPath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func stat(Int32)

```cangjie
public static func stat(file: Int32): Stat
```

**Function:** Obtain detailed file attribute information.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | Int32 | Yes | - | File descriptor fd of the opened file. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Stat](#class-stat) | Represents specific file information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/testDir"
    let file = FileIo.open(dirPath)
    FileIo.stat(file.fd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func stat(String)

```cangjie
public static func stat(file: String): Stat
```

**Function:** Obtain detailed file attribute information.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | String | Yes | - | Application sandbox path of the file. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Stat](#class-stat) | Represents specific file information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900030 | File name too long |
  | 13900031 | Function not implemented |
  | 13900033 | Too many symbolic links encountered |
  | 13900038 | Value too large for defined data type |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/testDir"
    FileIo.stat(dirPath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func truncate(String, Int64)

```cangjie
public static func truncate(file: String, len!: Int64 = 0): Unit
```

**Function:** Truncate a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | String | Yes | - | Application sandbox path of the file. |
| len | Int64 | No | 0 | Length of the file after truncation, in bytes. Default is 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900027 | Read-only file system |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let len: Int64 = 5
    FileIo.truncate(filePath, len: len)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func truncate(Int32, Int64)

```cangjie
public static func truncate(file: Int32, len!: Int64 = 0): Unit
```

**Function:** Truncate a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| file | Int32 | Yes | - | File descriptor fd of the opened file. |
| len | Int64 | No | 0 | Length of the file after truncation, in bytes. Default is 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900023 | Text file busy |
  | 13900024 | File too large |
  | 13900027 | Read-only file system |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let len: Int64 = 5
    let file  = FileIo.open(filePath, mode: OpenMode.READ_WRITE)
    FileIo.truncate(file.fd, len: len)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func unlink(String)

```cangjie
public static func unlink(path: String): Unit
```

**Function:** Delete a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the file. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900011 | Out of memory |
  | 13900012 | Permission denied |
  | 13900013 | Bad address |
  | 13900014 | Device or resource busy |
  | 13900018 | Not a directory |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900027 | Read-only file system |
  | 13900030 | File name too long |
  | 13900033 | Too many symbolic links encountered |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    FileIo.unlink(filePath)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func utimes(String, Float64)

```cangjie
public static func utimes(path: String, mtime: Float64): Unit
```

**Function:** Delete a file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | Application sandbox path of the file. |
| mtime | Float64 | Yes | - | Timestamp to be updated. Milliseconds from January 1, 1970 to the target time. Only supports modifying the file's last access time attribute. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900002 | No such file or directory |
  | 13900012 | Permission denied |
  | 13900020 | Invalid argument |
  | 13900027 | Read-only file system |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import std.time.DateTime
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    FileIo.write(file.fd, "test data")
    FileIo.close(file)
    FileIo.utimes(filePath, Float64(DateTime.UnixEpoch.second))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func write(Int32, Array\<Byte>, WriteOptions)

```cangjie
public static func write(fd: Int32, buffer: Array<Byte>, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Write data to a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | File descriptor of the opened file. |
| buffer | Array\<Byte> | Yes | - | Data to be written to the file, from a string. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | Supports the following options:<br/>- offset, ?Int64 type, indicates the desired position to write in the file. Optional, defaults to the current position.<br/>- length, ?UIntNative type, indicates the desired length of data to write. Optional, defaults to the buffer length.<br/>- encoding, String type, valid when data is of String type, indicates the encoding method of the data, default is "utf-8". Currently only supports "utf-8". |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Actual length written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let str = "hello, world"
    let writeLen = FileIo.write(file.fd, str.toArray())
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func write(Int32, String, WriteOptions)

```cangjie
public static func write(fd: Int32, buffer: String, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Write data to a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | File descriptor of the opened file. |
| buffer | String | Yes | - | Data to be written to the file, from a string. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | Supports the following options:<br/>- offset, ?Int64 type, indicates the desired position to write in the file. Optional, defaults to the current position.<br/>- length, ?UIntNative type, indicates the desired length of data to write. Optional, defaults to the buffer length.<br/>- encoding, String type, valid when data is of String type, indicates the encoding method of the data, default is "utf-8". Currently only supports "utf-8". |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Actual length written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 139000## class Filter

```cangjie
public class Filter {
    public var suffix: Array<String>
    public var displayName: Array<String>
    public var mimeType: Array<String>
    public var fileSizeOver:?Int64
    public var lastModifiedAfter:?Float64
    public var excludeMedia: Bool
    public init(
        suffix!: Array<String> = Array<String>(),
        displayName!: Array<String> = Array<String>(),
        mimeType!: Array<String> = Array<String>(),
        fileSizeOver!: ?Int64 = None,
        lastModifiedAfter!: ?Float64 = None,
        excludeMedia!: Bool = false
    )
}
```

**Function:** File filtering configuration type, used by the listFile interface. Note: mimeType and excludeMedia filtering are currently unsupported.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var displayName

```cangjie
public var displayName: Array<String>
```

**Function:** Fuzzy filename matching with OR relationship between keywords. Currently only supports wildcard *.

**Type:** Array\<String>

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var excludeMedia

```cangjie
public var excludeMedia: Bool
```

**Function:** Whether to exclude files already present in Media. Reserved capability, currently unsupported.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var fileSizeOver

```cangjie
public var fileSizeOver:?Int64
```

**Function:** File size matching - files larger than specified size.

**Type:** ?Int64

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var lastModifiedAfter

```cangjie
public var lastModifiedAfter:?Float64
```

**Function:** File last modified time matching - files modified after specified timestamp.

**Type:** ?Float64

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var mimeType

```cangjie
public var mimeType: Array<String>
```

**Function:** Exact mime type matching with OR relationship between keywords. Reserved capability, currently unsupported.

**Type:** Array\<String>

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var suffix

```cangjie
public var suffix: Array<String>
```

**Function:** Exact file extension matching with OR relationship between keywords.

**Type:** Array\<String>

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Array\<String>, Array\<String>, Array\<String>, ?Int64, ?Float64, Bool)

```cangjie
public init(
    suffix!: Array<String> = Array<String>(),
    displayName!: Array<String> = Array<String>(),
    mimeType!: Array<String> = Array<String>(),
    fileSizeOver!: ?Int64 = None,
    lastModifiedAfter!: ?Float64 = None,
    excludeMedia!: Bool = false
)
```

**Function:** Constructs a Filter object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| suffix | Array\<String> | No | Array\<String>() | Exact file extension matching with OR relationship between keywords. |
| displayName | Array\<String> | No | Array\<String>() | Fuzzy filename matching with OR relationship between keywords. Currently only supports wildcard *. |
| mimeType | Array\<String> | No | Array\<String>() | Exact mime type matching with OR relationship between keywords. Reserved capability, currently unsupported. |
| fileSizeOver | ?Int64 | No | None | File size matching - files larger than specified size. |
| lastModifiedAfter | ?Float64 | No | None | File last modified time matching - files modified after specified timestamp. |
| excludeMedia | Bool | No | false | Whether to exclude files already present in Media. Reserved capability, currently unsupported. |

**Exceptions:**

- BusinessException: Error codes as shown below, see [File Management Error Codes](./cj-errorcode-filemanagement.md) for details.

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900020 | Invalid argument |

## class ListFileOptions

```cangjie
public class ListFileOptions {
    public var recursion: Bool
    public var listNum: Int32
    public var filter: Filter
    public init(
        recursion!: Bool = false,
        listNum!: Int32 = 0,
        filter!: Filter = Filter()
    )
}
```

**Function:** Optional configuration type for use with the listFile interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var filter

```cangjie
public var filter: Filter
```

**Function:** Valid when data is of String type, indicates data encoding method (default "utf-8"). Only "utf-8" is supported.

**Type:** [Filter](#class-filter)

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var listNum

```cangjie
public var listNum: Int32
```

**Function:** Number of filenames to list. When set to 0, lists all files (default is 0).

**Type:** Int32

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var recursion

```cangjie
public var recursion: Bool
```

**Function:** Whether to recursively list filenames in subdirectories. Default is false. When recursion is false, returns filenames and folder names in current directory that meet filtering requirements. When recursion is true, returns relative paths (starting with /) of all files meeting filtering requirements in this directory.

**Type:** Bool

**Read-Write Permission:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Bool, Int32, Filter)

```cangjie
public init(
    recursion!: Bool = false,
    listNum!: Int32 = 0,
    filter!: Filter = Filter()
)
```

**Function:** Constructs a ListFileOptions object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| recursion | Bool | No | false | Whether to recursively list filenames in subdirectories. Default is false. When recursion is false, returns filenames and folder names in current directory that meet filtering requirements. When recursion is true, returns relative paths (starting with /) of all files meeting filtering requirements in this directory. |
| listNum | Int32 | No | 0 | Number of filenames to list. When set to 0, lists all files (default is 0). |
| filter | [Filter](#class-filter) | No | Filter() | File filtering options. Currently only supports extension matching, fuzzy filename query, file size filtering, and last modified time filtering. |

## class OpenMode

```cangjie
public class OpenMode {
    public static const READ_ONLY: Int64 = 0o0
    public static const WRITE_ONLY: Int64 = 0o1
    public static const READ_WRITE: Int64 = 0o2
    public static const CREATE: Int64 = 0o100
    public static const TRUNC: Int64 = 0o1000
    public static const APPEND: Int64 = 0o2000
    public static const NONBLOCK: Int64 = 0o4000
    public static const DIR: Int64 = 0o200000
    public static const NOFOLLOW: Int64 = 0o400000
    public static const SYNC: Int64 = 0o4010000
}
```

**Function:** Constants for flags parameter in open interface. File opening flags.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const APPEND

```cangjie
public static const APPEND: Int64 = 0o2000
```

**Function:** Open in append mode, subsequent writes will append to end of file.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const CREATE

```cangjie
public static const CREATE: Int64 = 0o100
```

**Function:** Create file if it doesn't exist.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const DIR

```cangjie
public static const DIR: Int64 = 0o200000
```

**Function:** Error if path doesn't point to directory.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const NOFOLLOW

```cangjie
public static const NOFOLLOW: Int64 = 0o400000
```

**Function:** Error if path points to symbolic link.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const NONBLOCK

```cangjie
public static const NONBLOCK: Int64 = 0o4000
```

**Function:** If path points to FIFO, block special file or character special file, this open and subsequent I/O operations will be non-blocking.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const READ_ONLY

```cangjie
public static const READ_ONLY: Int64 = 0o0
```

**Function:** Open for reading only.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const READ_WRITE

```cangjie
public static const READ_WRITE: Int64 = 0o2
```

**Function:** Open for reading and writing.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const SYNC

```cangjie
public static const SYNC: Int64 = 0o4010000
```

**Function:** Open file with synchronous I/O.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const TRUNC

```cangjie
public static const TRUNC: Int64 = 0o1000
```

**Function:** If file exists and is opened for writing or reading/writing, truncate its length to zero.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### static const WRITE_ONLY

```cangjie
public static const WRITE_ONLY: Int64 = 0o1
```

**Function:** Open for writing only.

**Type:** Int64

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22## class Options

```cangjie
public open class Options {
    public var encoding: String
    public init(
        encoding!: String = "utf-8"
    )
}
```

**Function:** Optional type, supports the use of readLines interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var encoding

```cangjie
public var encoding: String
```

**Function:** File encoding method. Optional.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(String)

```cangjie
public init(
    encoding!: String = "utf-8"
)
```

**Function:** Constructs an Options object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| encoding | String | No | "utf-8" | Specifies the encoding method for strings. |

## class RandomAccessFile

```cangjie
public class RandomAccessFile {}
```

**Function:** Random access file stream. Before calling methods of RandomAccessFile, you need to first construct a RandomAccessFile instance via the createRandomAccessFile method.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop fd

```cangjie
public prop fd: Int32
```

**Function:** The opened file descriptor.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop filePointer

```cangjie
public prop filePointer: Int64
```

**Function:** The offset pointer of the RandomAccessFile object.

**Type:** Int64

**Access:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Function:** Synchronously closes the RandomAccessFile object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Please replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let randomAccessFile = FileIo.createRandomAccessFile(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    randomAccessFile.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func read(Array\<Byte>, ReadOptions)

```cangjie
public func read(buffer: Array<Byte>, options!: ReadOptions = ReadOptions()): Int64
```

**Function:** Reads data from a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | Array\<Byte> | Yes | - | Buffer for reading the file. |
| options | [ReadOptions](#class-readoptions) | No | ReadOptions() | **Named parameter.** Supports the following options:<br>- length, ?UIntNative type, indicates the expected length of data to read. Optional, defaults to buffer length.<br>- offset, ?Int64 type, indicates the expected position to read from the file. Optional, defaults to current position. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The actual length read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900034 | Operation would block |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Please replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let randomAccessFile = FileIo.createRandomAccessFile(file)
    let length: Int64 = 4096
    let arrayBuffer = Array<Byte>(length, repeat: 0)
    let readLength = randomAccessFile.read(arrayBuffer)
    randomAccessFile.close()
    FileIo.close(file)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setFilePointer(Int64)

```cangjie
public func setFilePointer(filePointer: Int64): Unit
```

**Function:** Sets the file offset pointer.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| filePointer | Int64 | Yes | - | The offset pointer of the RandomAccessFile object. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Please replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let randomAccessFile = FileIo.createRandomAccessFile(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    randomAccessFile.setFilePointer(1)
    randomAccessFile.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func write(String, WriteOptions)

```cangjie
public func write(buffer: String, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Writes data to a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | String | Yes | - | Data to be written to the file. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | **Named parameter.** Supports the following options:<br>- length, ?UIntNative type, indicates the expected length of data to write. Defaults to buffer length.<br>- offset, ?Int64 type, indicates the expected position to write to the file. Optional, defaults to current position.<br>- encoding, String type, valid when data is of String type, indicates the encoding method of the data, defaults to "utf-8". Only "utf-8" is supported. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The actual length written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Please replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let randomAccessFile = FileIo.createRandomAccessFile(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let option = WriteOptions(length: 5, offset: 5)
    let bytesWritten = randomAccessFile.write("hello, world", options: option)
    randomAccessFile.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func write(Array\<Byte>, WriteOptions)

```cangjie
public func write(buffer: Array<Byte>, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Writes data to a file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | Array\<Byte> | Yes | - | Data to be written to the file. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | **Named parameter.** Supports the following options:<br>- length, ?UIntNative type, indicates the expected length of data to write. Defaults to buffer length.<br>- offset, ?Int64 type, indicates the expected position to write to the file. Optional, defaults to current position.<br>- encoding, String type, valid when data is of String type, indicates the encoding method of the data, defaults to "utf-8". Only "utf-8" is supported. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The actual length written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Please replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let randomAccessFile = FileIo.createRandomAccessFile(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    let option = WriteOptions(length: 5, offset: 5)
    let arr: Array<UInt8> = [104, 101, 108, 108, 111, 32, 119, 111, 114, 108, 100]
    let bytesWritten = randomAccessFile.write(arr, options: option)
    randomAccessFile.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class RandomAccessFileOptions

```cangjie
public class RandomAccessFileOptions {
    public var start: Option<Int64>
    public var end: Option<Int64>
    public init(
        start!: Option<Int64> = None,
        end!: Option<Int64> = None
    )
}
```

**Function:** Optional type, supports the use of createRandomAccessFile interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var end

```cangjie
public var end: Option<Int64>
```

**Function:** The expected end position for reading. Optional, defaults to end of file.

**Type:** Option\<Int64>

**Access:** Read-write

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var start

```cangjie
public var start: Option<Int64>
```

**Function:** The expected starting position for reading the file. Optional, defaults to current position.

**Type:** Option\<Int64>

**Access:** Read-write

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Option\<Int64>, Option\<Int64>)

```cangjie
public init(
    start!: Option<Int64> = None,
    end!: Option<Int64> = None
)
```

**Function:** Constructs a RandomAccessFileOptions object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| start | Option\<Int64> | No | None | The expected starting position for reading the file. Optional, defaults to current position. |
| end | Option\<Int64> | No | None | The expected end position for reading. Optional, defaults to end of file. |## class ReaderIterator

```cangjie
public class ReaderIterator {}
```

**Description:** File reading iterator. Before calling methods of ReaderIterator, a ReaderIterator instance must be constructed via the `readLines` method.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### func next()

```cangjie
public func next(): ReaderIteratorResult
```

**Description:** Retrieves the next item from the iterator.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ReaderIteratorResult](#class-readeriteratorresult) | The result returned by the file reading iterator. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900005 | I/O error |
  | 13900037 | No data available |
  | 13900042 | Unknown error |

## class ReaderIteratorResult

```cangjie
public class ReaderIteratorResult {
    public var done: Bool
    public var value: String
}
```

**Description:** The result returned by the file reading iterator, supporting the ReaderIterator interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var done

```cangjie
public var done: Bool
```

**Description:** Indicates whether the iterator has completed iteration.

**Type:** Bool

**Read/Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var value

```cangjie
public var value: String
```

**Description:** The text content of the file read line by line.

**Type:** String

**Read/Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

## class ReadOptions

```cangjie
public open class ReadOptions {
    public var offset: Option<Int64>
    public var length: Option<UIntNative>
    public init(
        offset!: Option<Int64> = None,
        length!: Option<UIntNative> = None
    )
}
```

**Description:** Optional type, supporting the `read` interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parent Type:**

- [ReadOptions](#class-readoptions)

### var length

```cangjie
public var length: Option<UIntNative>
```

**Description:** The expected length of data to read. Defaults to the buffer length.

**Type:** Option\<UIntNative>

**Read/Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var offset

```cangjie
public var offset: Option<Int64>
```

**Description:** The expected file position to read from (based on the current `filePointer` plus the offset). Defaults to reading from the offset pointer (`filePointer`).

**Type:** Option\<Int64>

**Read/Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Option\<Int64>, Option\<UIntNative>)

```cangjie
public init(
    offset!: Option<Int64> = None,
    length!: Option<UIntNative> = None
)
```

**Description:** Constructs a ReadOptions object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| offset | Option\<Int64> | No | None | The expected file position to read from (based on the current `filePointer` plus the offset). Defaults to reading from the offset pointer (`filePointer`). |
| length | Option\<UIntNative> | No | None | The expected length of data to read. Defaults to the buffer length. |

## class ReadTextOptions

```cangjie
public class ReadTextOptions <: ReadOptions {
    public var encoding: String
    public init(
        offset!: Option<Int64> = None,
        length!: Option<UIntNative> = None,
        encoding!: String = "utf-8"
    )
}
```

**Description:** Optional type, supporting the `readText` interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parent Type:**

- [ReadOptions](#class-readoptions)

### var encoding

```cangjie
public var encoding: String
```

**Description:** Valid when the data is of type String, indicating the encoding method of the data. Defaults to "utf-8" and only supports "utf-8".

**Type:** String

**Read/Write Attribute:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Option\<Int64>, Option\<UIntNative>, String)

```cangjie
public init(
    offset!: Option<Int64> = None,
    length!: Option<UIntNative> = None,
    encoding!: String = "utf-8"
)
```

**Description:** Constructs a ReadOptions object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| offset | Option\<Int64> | No | None | The expected file position to read from (based on the current `filePointer` plus the offset). Defaults to reading from the offset pointer (`filePointer`). |
| length | Option\<UIntNative> | No | None | The expected length of data to read. Defaults to the buffer length. |
| encoding | String | No | "utf-8" | Valid when the data is of type String, indicating the encoding method of the data. Defaults to "utf-8" and only supports "utf-8". |

## class Stat

```cangjie
public class Stat {}
```

**Description:** Detailed file information. Before calling methods of Stat, a Stat instance must be constructed via the [FileIo.stat()](#static-func-statstring) method.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop atime

```cangjie
public prop atime: Int64
```

**Description:** The last access time of the file, represented as the number of seconds since 00:00:00 on January 1, 1970.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop ctime

```cangjie
public prop ctime: Int64
```

**Description:** The last time the file status was changed, represented as the number of seconds since 00:00:00 on January 1, 1970.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop gid

```cangjie
public prop gid: Int64
```

**Description:** The group ID of the file owner.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop ino

```cangjie
public prop ino: Int64
```

**Description:** Identifies the file. Typically, different files on the same device have different INOs.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop mode

```cangjie
public prop mode: Int64
```

**Description:** Represents file permissions. The meanings of each bit are as follows.

>**Note:**
>
>The following values are in octal. The returned value is in decimal and should be converted for viewing.<br/>- 0o400: User read. For regular files, the owner can read the file; for directories, the owner can read directory entries.<br/>- 0o200: User write. For regular files, the owner can write to the file; for directories, the owner can create/delete directory entries.<br/>- 0o100: User execute. For regular files, the owner can execute the file; for directories, the owner can search for a given pathname in the directory.<br/>- 0o040: Group read. For regular files, the group can read the file; for directories, the group can read directory entries.<br/>- 0o020: Group write. For regular files, the group can write to the file; for directories, the group can create/delete directory entries.<br/>- 0o010: Group execute. For regular files, the group can execute the file; for directories, the group can search for a given pathname in the directory.<br/>- 0o004: Others read. For regular files, others can read the file; for directories, others can read directory entries.<br/>- 0o002: Others write. For regular files, others can write to the file; for directories, others can create/delete directory entries.<br/>- 0o001: Others execute. For regular files, others can execute the file; for directories, others can search for a given pathname in the directory.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop mtime

```cangjie
public prop mtime: Int64
```

**Description:** The last modification time of the file, represented as the number of seconds since 00:00:00 on January 1, 1970.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop size

```cangjie
public prop size: Int64
```

**Description:** The size of the file in bytes. Only valid for regular files.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### prop uid

```cangjie
public prop uid: Int64
```

**Description:** The user ID of the file owner.

**Type:** Int64

**Read/Write Attribute:** Read-only

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### func isBlockDevice()

```cangjie
public func isBlockDevice(): Bool
```

**Description:** Determines whether the file is a block special file. A block special file can only be accessed in blocks and is accessed with caching.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a block special device. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isBLockDevice = FileIo.stat(filePath).isBlockDevice()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isCharacterDevice()

```cangjie
public func isCharacterDevice(): Bool
```

**Description:** Determines whether the file is a character special file. A character special device can be accessed randomly and is accessed without caching.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a character special device. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isCharacterDevice = FileIo.stat(filePath).isCharacterDevice()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isDirectory()

```cangjie
public func isDirectory(): Bool
```

**Description:** Determines whether the file is a directory.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a directory. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let dirPath = pathDir + "/test"
    let isDirectory = FileIo.stat(dirPath).isDirectory()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isFIFO()

```cangjie
public func isFIFO(): Bool
```

**Description:** Determines whether the file is a named pipe (sometimes referred to as FIFO). Named pipes are typically used for inter-process communication.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a FIFO. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isFIFO = FileIo.stat(filePath).isFIFO()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isFile()

```cangjie
public func isFile(): Bool
```

**Description:** Determines whether the file is a regular file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a regular file. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isFile = FileIo.stat(filePath).isFile()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isSocket()

```cangjie
public func isSocket(): Bool
```

**Description:** Determines whether the file is a socket.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a socket. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isSocket = FileIo.stat(filePath).isSocket()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func isSymbolicLink()

```cangjie
public func isSymbolicLink(): Bool
```

**Description:** Determines whether the file is a symbolic link.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Indicates whether the file is a symbolic link. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining the file path.
    let isSymbolicLink = FileIo.stat(filePath).isSymbolicLink()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class Stream

```cangjie
public class Stream {}
```

**Function:** File stream. Before calling Stream methods, a Stream instance must first be constructed via either the [FileIo.createStream](#static-func-createstreamstring-string) method or [FileIo.fdopenStream](#static-func-fdopenstreamint32-string).

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Function:** Synchronously closes the file stream.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900025 | No space left on device |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let stream = FileIo.createStream(filePath, "r+")
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func flush()

```cangjie
public func flush(): Unit
```

**Function:** Synchronously flushes the file stream.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let stream = FileIo.createStream(filePath, "r+")
    stream.flush()
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func read(Array\<Byte>, ReadOptions)

```cangjie
public func read(buffer: Array<Byte>, options!: ReadOptions = ReadOptions()): Int64
```

**Function:** Reads data from the stream file synchronously.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | Array\<Byte> | Yes | - | Buffer for reading the file. |
| options | [ReadOptions](#class-readoptions) | No | ReadOptions() | **Named parameter.** Supports the following options:<br/>-&nbsp;length, UIntNative type, indicates the expected length of data to read. Optional, defaults to buffer length.<br/>-&nbsp;offset, Int64 type, indicates the expected position to read from the file. Optional, defaults to current position.<br/>|

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Actual length of data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900019 | Is a directory |
  | 13900020 | Invalid argument |
  | 13900034 | Operation would block |
  | 13900042 | Unknown error |
  | 13900044 | Network is unreachable |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let stream = FileIo.createStream(filePath, "r+")
    let buf = Array<Byte>(4096, repeat: 0)
    let num = stream.read(buf)
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func write(String, WriteOptions)

```cangjie
public func write(buffer: String, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Writes data to the stream file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | String | Yes | - | Data to be written to the file. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | **Named parameter.** Supports the following options:<br/>-&nbsp;length, ?UIntNative type, indicates the expected length of data to write. Defaults to buffer length.<br/>-&nbsp;offset, ?Int64 type, indicates the expected position to write to the file. Optional, defaults to current position.<br/>-&nbsp;encoding, String type, effective when data is of String type, indicates the encoding method of the data. Default is "utf-8". Only "utf-8" is supported.|

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Actual length of data written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let stream = FileIo.createStream(filePath, "r+")
    let arr: Array<UInt8> = [104, 101, 108, 108, 111, 32, 119, 111, 114, 108, 100]
    let num = stream.write(arr)
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func write(Array\<Byte>, WriteOptions)

```cangjie
public func write(buffer: Array<Byte>, options!: WriteOptions = WriteOptions()): Int64
```

**Function:** Writes data to the stream file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buffer | Array\<Byte> | Yes | - | Data to be written to the file. |
| options | [WriteOptions](#class-writeoptions) | No | WriteOptions() | **Named parameter.** Supports the following options:<br/>-&nbsp;length, ?UIntNative type, indicates the expected length of data to write. Defaults to buffer length.<br/>-&nbsp;offset, ?Int64 type, indicates the expected position to write to the file. Optional, defaults to current position.<br/>-&nbsp;encoding, String type, effective when data is of String type, indicates the encoding method of the data. Default is "utf-8". Only "utf-8" is supported.|

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Actual length of data written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [File Management Error Codes](./cj-errorcode-filemanagement.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13900001 | Operation not permitted |
  | 13900004 | Interrupted system call |
  | 13900005 | I/O error |
  | 13900008 | Bad file descriptor |
  | 13900010 | Try again |
  | 13900013 | Bad address |
  | 13900020 | Invalid argument |
  | 13900024 | File too large |
  | 13900025 | No space left on device |
  | 13900034 | Operation would block |
  | 13900041 | Quota exceeded |
  | 13900042 | Unknown error |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let pathDir = "path/to/file"
    let filePath = pathDir + "/test.txt"  // Replace with the correct file path. Refer to the usage instructions for obtaining file paths.
    let stream = FileIo.createStream(filePath, "r+")
    let arr: Array<UInt8> = [104, 101, 108, 108, 111, 32, 119, 111, 114, 108, 100]
    let num = stream.write(arr)
    stream.close()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class WriteOptions

```cangjie
public class WriteOptions <: Options {
    public var length: Option<UIntNative>
    public var offset: Option<Int64>
    public init(
        length!: Option<UIntNative> = None,
        offset!: Option<Int64> = None,
        encoding!: String = "utf-8"
    )
}
```

**Function:** Optional type, supports the write interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parent Type:**

- [Options](#class-options)

### var length

```cangjie
public var length: Option<UIntNative>
```

**Function:** Expected length of data to write. Defaults to buffer length.

**Type:** Option\<UIntNative>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### var offset

```cangjie
public var offset: Option<Int64>
```

**Function:** Expected position to write to the file (based on the current filePointer plus offset). Defaults to writing from the offset pointer (filePointer).

**Type:** Option\<Int64>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### init(Option\<UIntNative>, Option\<Int64>, String)

```cangjie
public init(
    length!: Option<UIntNative> = None,
    offset!: Option<Int64> = None,
    encoding!: String = "utf-8"
)
```

**Function:** Constructs a WriteOptions object.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| length | Option\<UIntNative> | No | None | Expected length of data to write. Defaults to buffer length. |
| offset | Option\<Int64> | No | None | Expected position to write to the file (based on the current filePointer plus offset). Defaults to writing from the offset pointer (filePointer). |
| encoding | String | No | "utf-8" | Effective when data is of String type, indicates the encoding method of the data. Default is "utf-8". Only "utf-8" is supported. |

## enum AccessFlagType

```cangjie
public enum AccessFlagType {
    | Local
    | ...
}
```

**Function:** Indicates the file location to be verified.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### Local

```cangjie
Local
```

**Function:** Whether the file is local.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22## enum AccessModeType

```cangjie
public enum AccessModeType {
    | Exist
    | Write
    | Read
    | ReadWrite
    | ...
}
```

**Function:** Specifies the specific permission to be verified. Defaults to checking file existence.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### Exist

```cangjie
Exist
```

**Function:** Checks whether the file exists.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### Read

```cangjie
Read
```

**Function:** Checks whether the file has read permission.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### ReadWrite

```cangjie
ReadWrite
```

**Function:** Checks whether the file has read-write permissions.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### Write

```cangjie
Write
```

**Function:** Checks whether the file has write permission.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

## enum WhenceType

```cangjie
public enum WhenceType {
    | SeekSet
    | SeekCur
    | SeekEnd
    | ...
}
```

**Function:** Specifies the relative position type for file offset pointer, used by the lseek interface.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### SeekCur

```cangjie
SeekCur
```

**Function:** Current position of the file offset pointer.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### SeekEnd

```cangjie
SeekEnd
```

**Function:** End position of the file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22

### SeekSet

```cangjie
SeekSet
```

**Function:** Starting position of the file.

**System Capability:** SystemCapability.FileManagement.File.FileIO

**Since:** 22