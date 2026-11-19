# ohos.zlib (Zip)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module is developed based on the zlib library and provides file compression and decompression capabilities. It uses the DEFLATE algorithm and supports data processing in zlib, deflate, and gzip formats.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Notes](../../reference/cj-development-intro.md#cangjie-sample-code-notes).

## func compressFile(String, String, Options, AsyncCallback\<Unit>)

```cangjie
public func compressFile(inFile: String, outFile: String, options: Options, callback: AsyncCallback<Unit>): Unit
```

**Function:** Compresses a file. This API uses an asynchronous callback to return the result.

> **Note:**
>
> To avoid path traversal, the input parameters of **inFile** and **outFile** cannot contain two consecutive periods and a slash (../). Otherwise, error codes 900001 and 900002 are returned.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|inFile|String|Yes|-|Path of the folder or file to compress. The path must be an application sandbox path, which can be obtained from the context. The folder to compress cannot be empty. Otherwise, an error will be reported when decompressFile is used to decompress the folder.|
|outFile|String|Yes|-|Path of the compressed file. The path must be an application sandbox path, which can be obtained from the context. When multiple tasks compress files at the same time, the values of **outFile** must be different. Otherwise, the compression may fail or the output file may be damaged.|
|options|[Options](#class-options)|Yes|-|Compression parameters.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|-|Callback used to return the compression result. If the operation is successful, **None** is returned; otherwise, a specific error code is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
let inFile = "/data/storage/el2/base/temp/filename.xxx"
let outFile = "/data/storage/el2/base/temp/xxx.zip"
let options = Options(
    level: CompressLevel.CompressLevelDefaultCompression,
    memLevel: MemLevel.MemLevelDefault,
    strategy: CompressStrategy.CompressStrategyDefaultStrategy
)
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "compressFile error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "compressFile success")
    }
}

try {
    compressFile(inFile, outFile, options, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "compressFile error: errcode is ${e.code}, message is ${e.message}")
}
```

## func compressFiles(Array\<String>, String, Options, AsyncCallback\<Unit>)

```cangjie
public func compressFiles(inFiles: Array<String>, outFile: String, options: Options, callback: AsyncCallback<Unit>): Unit
```

**Function:** Compresses multiple specified files. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|inFiles|Array\<String>|Yes|-|Paths of the folders or files to compress. The paths must be application sandbox paths, which can be obtained from the context. The folder to compress cannot be empty. Otherwise, an error will be reported when decompressFile is used to decompress the folder.|
|outFile|String|Yes|-|Path of the compressed file. The path must be an application sandbox path, which can be obtained from the context. When multiple threads compress files at the same time, the values of **outFile** must be different. Otherwise, the compression may fail or the output file may be damaged.|
|options|[Options](#class-options)|Yes|-|Compression parameters.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|-|Callback used to return the compression result. If the operation is successful, **None** is returned; otherwise, a specific error code is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
let inFiles = ["/data/storage/el2/base/temp/filename.xxx", "/data/storage/el2/base/temp/xxx"]
let outFile = "/data/storage/el2/base/temp/xxx.zip"
let options = Options(
    level: CompressLevel.CompressLevelDefaultCompression,
    memLevel: MemLevel.MemLevelDefault,
    strategy: CompressStrategy.CompressStrategyDefaultStrategy
)
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "compressFiles error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "compressFiles success")
    }
}

try {
    compressFiles(inFiles, outFile, options, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "compressFiles error: errcode is ${e.code}, message is ${e.message}")
}
```

## func createChecksum(AsyncCallback\<Checksum>)

```cangjie
public func createChecksum(callback: AsyncCallback<Checksum>): Unit
```

**Function:** Creates a checksum object. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[Checksum](#class-checksum)>|Yes|Callback used to return the created checksum object.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<Checksum> = {
    err: Option<BusinessException>, data: Option<Checksum> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createChecksum error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "createChecksum success")
    }
}

createChecksum(callback)
```

## func createGZip(AsyncCallback\<GZip>)

```cangjie
public func createGZip(callback: AsyncCallback<GZip>): Unit
```

**Function:** Creates a **GZip** object. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[GZip](#class-gzip)>|Yes|Callback used to return the created **GZip** object.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "createGZip success")
    }
}

createGZip(callback)
```

## func createZip(AsyncCallback\<Zip>)

```cangjie
public func createZip(callback: AsyncCallback<Zip>): Unit
```

**Function:** Creates a **Zip** instance. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[Zip](#class-zip)>|Yes|Callback used to return the created **Zip** instance.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "createZip success")
    }
}

createZip(callback)
```

## func decompressFile(String, String, Options, AsyncCallback\<Unit>)

```cangjie
public func decompressFile(inFile: String, outFile: String, options: Options, callback: AsyncCallback<Unit>): Unit
```

**Function:** Decompresses a file. This API uses an asynchronous callback to return the result.

> **Note:**
>
> - To avoid path traversal, the input parameters of **inFile** and **outFile** cannot contain two consecutive periods and a slash (../). Otherwise, error codes 900001 and 900002 are returned.
> - The name of the zipped file or zipped folder cannot contain two consecutive periods and a slash (../). Otherwise, the error code 900003 is returned.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|inFile|String|Yes|-|Path of the file to decompress. The file name extension must be .zip. The path must be an application sandbox path, which can be obtained from the context. If the .zip file to be decompressed contains Chinese file names or folder names, use UTF-8 to encode them. Otherwise, garbled characters may be displayed after decompression.|
|outFile|String|Yes|-|Path of the decompressed folder. The path must exist in the system. Otherwise, the decompression fails. The path must be an application sandbox path, which can be obtained from the context. If a file or folder with the same name already exists in the path, they will be overwritten. When multiple threads decompress files at the same time, the values of **outFile** must be different. Otherwise, the decompressed data may overwrite each other or the file may be damaged.|
|options|[Options](#class-options)|Yes|-|Decompression parameters.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|-|Callback used to return the decompression result. If the operation is successful, **None** is returned; otherwise, a specific error code is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
let inFile = "/data/storage/el2/base/temp/xxx.zip"
let outFileDir = "/data/storage/el2/base/temp"
let options = Options(level: CompressLevel.CompressLevelDefaultCompression)
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "decompressFile error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "decompressFile success")
    }
}

try {
    decompressFile(inFile, outFileDir, options, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "decompressFile error: errcode is ${e.code}, message is ${e.message}")
}
```

## func decompressFile(String, String, AsyncCallback\<Unit>)

```cangjie
public func decompressFile(inFile: String, outFile: String, callback: AsyncCallback<Unit>): Unit
```

**Function:** Decompresses a file. This API uses an asynchronous callback to return the result.

> **Note:**
>
> - To avoid path traversal, the input parameters of **inFile** and **outFile** cannot contain two consecutive periods and a slash (../). Otherwise, error codes 900001 and 900002 are returned.
> - The name of the zipped file or zipped folder cannot contain two consecutive periods and a slash (../). Otherwise, the error code 900003 is returned.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|inFile|String|Yes|-|Path of the file to decompress. The file name extension must be .zip. The path must be an application sandbox path, which can be obtained from the context. If the .zip file to be decompressed contains Chinese file names or folder names, use UTF-8 to encode them. Otherwise, garbled characters may be displayed after decompression.|
|outFile|String|Yes|-|Path of the decompressed folder. The path must exist in the system. Otherwise, the decompression fails. The path must be an application sandbox path, which can be obtained from the context. If a file or folder with the same name already exists in the path, they will be overwritten. When multiple threads decompress files at the same time, the values of **outFile** must be different. Otherwise, the decompressed data may overwrite each other or the file may be damaged.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|-|Callback used to return the decompression result. If the operation is successful, **None** is returned; otherwise, a specific error code is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
let inFile = "/data/storage/el2/base/temp/xxx.zip"
let outFileDir = "/data/storage/el2/base/temp"
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "decompressFile error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "decompressFile success")
    }
}

try {
    decompressFile(inFile, outFileDir, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "decompressFile error: errcode is ${e.code}, message is ${e.message}")
}
```

## func getOriginalSize(String, AsyncCallback\<Int64>)

```cangjie
public func getOriginalSize(compressedFile: String, callback: AsyncCallback<Int64>): Unit
```

**Function:** Obtains the original size of a compressed file. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|compressedFile|String|Yes|Specifies the path of the compressed file. Only .zip files are supported. The path must be an application sandbox path, which can be obtained from the context.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int64>|Yes|Callback used to return the original size of the compressed file, in bytes.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
let compressedFile = "/data/storage/el2/base/temp/test.zip"
let callback: AsyncCallback<Int64> = {
    err: Option<BusinessException>, data: Option<Int64> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getOriginalSize error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(size) => Hilog.info(0, "test", "getOriginalSize success, size is ${size}")
            case _ => Hilog.error(0, "test", "getOriginalSize failed")
        }
    }
}

try {
    getOriginalSize(compressedFile, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getOriginalSize error: errcode is ${e.code}, message is ${e.message}")
}
```

## class Checksum

```cangjie
public class Checksum
```

**Function:** Checksum object, used for calculating and verifying data checksums.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### func crc32(UInt64, ArrayBuffer, AsyncCallback\<UInt64>)

```cangjie
public func crc32(crc: UInt64, buf: ArrayBuffer, callback: AsyncCallback<UInt64>): Unit
```

**Function:** Updates a CRC-32 checksum. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|crc|UInt64|Yes|Initial value of the CRC-32 checksum.|
|buf|ArrayBuffer|Yes|Data buffer for calculating the checksum.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<UInt64>|Yes|Callback used to return the updated CRC-32 checksum.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the 12 bytes of data for calculating the checksum.
let str = "hello world!"
let arrayBufferIn = str.toArray()
let crcCallback: AsyncCallback<UInt64> = {
    err: Option<BusinessException>, data: Option<UInt64> => match (err) {
        case Some(e) => Hilog.error(0, "test", "crc32 error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(value) => Hilog.info(0, "test", "crc32 success, checksum is ${value}")
            case _ => Hilog.error(0, "test", "crc32 failed")
        }
    }
}
let createCallback: AsyncCallback<Checksum> = {
    err: Option<BusinessException>, data: Option<Checksum> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createChecksum error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(checksum) => checksum.crc32(0, arrayBufferIn, crcCallback)
            case _ => Hilog.error(0, "test", "createChecksum failed")
        }
    }
}

createChecksum(createCallback)
```

## class GZip

```cangjie
public class GZip
```

**Function:** **GZip** object, which provides APIs for reading and writing gzip files.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### func gzclose(AsyncCallback\<ReturnStatus>)

```cangjie
public func gzclose(callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Clears all pending output of the file. Closes the file and releases the decompression or compression state if necessary. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800006 | Memory allocation failed. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzcloseDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzclose")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzclose/test.gz"
    // Step 2: Close the file and release the state, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 1: Open the file in write mode, and close it after the file is successfully opened.
    let gzopenCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => 
                Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ => 
                Hilog.info(0, "test", "gzopen success")
                try {
                    gzip.gzclose(gzcloseCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
            }
        }
    }
    try {
        gzip.gzopen(path, "wb", gzopenCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzcloseDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzdopen(Int32, String, AsyncCallback\<Unit>)

```cangjie
public func gzdopen(fd: Int32, mode: String, callback: AsyncCallback<Unit>): Unit
```

**Function:** Associates gzip file with the file descriptor (fd) and opens the file for reading and decompressing, or compressing and writing. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|fd|Int32|Yes|File descriptor. Generally, the value is obtained by calling the **open** method or other methods.|
|mode|String|Yes|Specifies the access mode. For details, see the description of [gzopen](#func-gzopenstring-string-asynccallbackunit).|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|Callback used to return the result. No value is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800002 | No such file or access mode error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzdopenDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzdopen")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    // Step 2: Close the file. (In actual development, initiate the next step after the previous callback is complete.)
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 1: Associate the gzFile with the file descriptor fd, and close the file after the association is successful.
    let gzdopenCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzdopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzdopen success")
                try {
                    gzip.gzclose(gzcloseCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Open the file to obtain the file descriptor fd, and then associate the gzFile with fd.
    try {
        let file = FileIo.open(pathDir + "/gzdopen/test.gz", mode: OpenMode.READ_WRITE | OpenMode.CREATE)
        try {
            gzip.gzdopen(file.fd, "wb", gzdopenCallback)
        } catch (e: BusinessException) {
            Hilog.error(0, "test", "gzdopen error: errcode is ${e.code}, message is ${e.message}")
        }
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "open error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzdopenDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzeof(AsyncCallback\<Int32>)

```cangjie
public func gzeof(callback: AsyncCallback<Int32>): Unit
```

**Function:** Checks whether the position from which data is read has reached the end of the gzip file. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|Callback used to return the result. If the end-of-file indicator is set while reading, **1** is returned.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzeofDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzeof")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzeof/test.gz"
    // Fill in the 16 bytes of data to be written.
    let writeBufferWithData = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        writeBufferWithData[i] = UInt8(i)
    }
    let readBufferWithData = ArrayBuffer(20, repeat: 0)
    // Step 8: Close the file after reading ends, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 7: Check whether the read position reaches the end of the file.
    let gzeofCallback: AsyncCallback<Int32> = {
        err: Option<BusinessException>, data: Option<Int32> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzeof error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzeof success, eof is ${value}")
                    try {
                        gzip.gzclose(finalCloseCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzeof failed")
            }
        }
    }
    // Step 6: Read the file content.
    let gzreadCallback: AsyncCallback<Int64> = {
        err: Option<BusinessException>, data: Option<Int64> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzread error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) => 
                    Hilog.info(0, "test", "gzread success, read is ${value}")
                    gzip.gzeof(gzeofCallback)
                case _ => Hilog.error(0, "test", "gzread failed")
            }
        }
    }
    // Step 5: Reopen the file in read mode.
    let openReadCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen read mode success")
                try {
                    gzip.gzread(readBufferWithData, gzreadCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzread error: errcode is ${e.code}, message is ${e.message}")
                }          
        }
    }
    // Step 4: Close the file after writing is complete.
    let closeWriteCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzclose success")
                try {
                    gzip.gzopen(path, "rb", openReadCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
                }

        }
    }
    // Step 3: Compress the data and write it to the file.
    let gzwriteCallback: AsyncCallback<Int64> = {
        err: Option<BusinessException>, data: Option<Int64> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) => 
                    Hilog.info(0, "test", "gzwrite success, written is ${value}")
                    try {
                        gzip.gzclose(closeWriteCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzwrite failed")
            }
        }
    }
    // Step 1: Open the file in write mode, write data, read the data, and check the end of the file.
    let openWriteCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen write mode success")
                try {
                    gzip.gzwrite(writeBufferWithData, 16, gzwriteCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", openWriteCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzeofDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzgets(ArrayBuffer, AsyncCallback\<String>)

```cangjie
public func gzgets(buf: ArrayBuffer, callback: AsyncCallback<String>): Unit
```

**Function:** Reads bytes from a compressed file and decompresses them into **buf** until a newline character is read and transferred to **buf**, or an end-of-file condition is encountered. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|buf|ArrayBuffer|Yes|Stores the read row data.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<String>|Yes|Callback used to return a null-terminated string.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzgetsDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzgets")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzgets/test.gz"
    let bufferWithData = ArrayBuffer(16, repeat: 0)
    // Step 6: Close the file after reading ends, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 5: Read one line of content.
    let gzgetsCallback: AsyncCallback<String> = {
        err: Option<BusinessException>, data: Option<String> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzgets error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzgets success, content is ${value}")
                    try {
                        gzip.gzclose(finalCloseCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzgets failed")
            }
        }
    }
    // Step 4: Reopen the file in read mode.
    let openReadCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen read mode success")
                try {
                    gzip.gzgets(bufferWithData, gzgetsCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzgets error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 3: Close the file after writing is complete.
    let closeWriteCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzclose success")
                try {
                    gzip.gzopen(path, "rb", openReadCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 2: Compress the string and write it to the file.
    let gzputsCallback: AsyncCallback<Int32> = {
        err: Option<BusinessException>, data: Option<Int32> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzputs error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzputs success, written is ${value}")
                    try {
                        gzip.gzclose(closeWriteCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzputs failed")
            }
        }
    }
    // Step 1: Open the file in write mode, write the string, and then read it.
    let openWriteCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen write mode success")
                try {
                    gzip.gzputs("hello", gzputsCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzputs error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", openWriteCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzgetsDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzopen(String, String, AsyncCallback\<Unit>)

```cangjie
public func gzopen(path: String, mode: String, callback: AsyncCallback<Unit>): Unit
```

**Function:** Opens the .gz file in the specified path for reading and decompressing, or compressing and writing. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|path|String|Yes|Path of the file to open. The path must be an application sandbox path, which can be obtained from the context.|
|mode|String|Yes|Specifies a mode for opening a file.<br>Basic modes (one of the following must be selected):<br>- **"r"** or **"rb"**: read mode. The system automatically detects and decompresses the gzip file. If the file is not in gzip format, the original data is directly read.<br>- **"w"** or **"wb"**: write mode. The system creates a new file and compresses data.<br>- **"a"** or **"ab"**: append mode. The system appends a new gzip stream to the end of the existing file without verifying the format of the original file.<br>Optional function parameters (can be used together):<br>- Compression level: **0** (no compression) to **9** (maximum compression). The default compression level is **6**. This parameter must be used together with the write or append mode.<br>- Compression strategy: **"f"** (filtering strategy), **"h"** (Huffman coding strategy), **"R"** (RLE compression strategy), or **"F"** (fixed encoding strategy). You can only select one of the strategies.<br>- Transparent mode: **"T"**. In this mode, data is not compressed and no gzip header is generated during writing (a common file is generated). This parameter is mutually exclusive with the compression strategy parameter.<br>- Exclusive creation: **"x"**. The file fails to be opened if it already exists. This parameter must be used together with the write or append mode.<br>- Close-on-exec flag: **"e"**. This parameter is used to set the **FD_CLOEXEC** property of the file descriptor (system-dependent).<br>Examples:<br>- **"r"**: read mode. Data is read in binary format.<br>- **"rb"**: read mode. Data is read in binary format.<br>- **"wb6"**: write mode. Data is written in binary format with the compression level of 6.<br>- **"wb9f"**: write mode. Data is written in binary format with the maximum compression level and filtering strategy.<br>- **"wbT"**: write mode. Data is not compressed and a common file is generated.<br>- **"wbx"**: write mode. Data is written to the exclusively created file in binary format.<br>- **"abx"**: append mode. Data is appended and written to the exclusively created file in binary format.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit>|Yes|Callback used to return the result. No value is returned.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800002 | No such file or access mode error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzopenDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzopen")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzopen/test.gz"
    // Step 2: Close the file, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 1: Open the file in write mode, and close it after the file is successfully opened.
    let gzopenCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen success")
                try {
                    gzip.gzclose(gzcloseCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", gzopenCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzopenDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzputs(String, AsyncCallback\<Int32>)

```cangjie
public func gzputs(str: String, callback: AsyncCallback<Int32>): Unit
```

**Function:** Compresses the given null-terminated strings and writes them to the file, excluding the null operator. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|str|String|Yes|String to write.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|Callback used to return the number of characters written.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzputsDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzputs")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzputs/test.gz"
    // Step 3: Close the file after writing is complete, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 2: Compress the string and write it to the file.
    let gzputsCallback: AsyncCallback<Int32> = {
        err: Option<BusinessException>, data: Option<Int32> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzputs error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzputs success, written is ${value}")
                    try {
                        gzip.gzclose(gzcloseCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzputs failed")
            }
        }
    }
    // Step 1: Open the file in write mode, and close the file after the string is written.
    let gzopenCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen success")
                try {
                    gzip.gzputs("hello", gzputsCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzputs error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", gzopenCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzputsDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzread(ArrayBuffer, AsyncCallback\<Int64>)

```cangjie
public func gzread(buf: ArrayBuffer, callback: AsyncCallback<Int64>): Unit
```

**Function:** Reads uncompressed bytes from a file and decompresses them into **buf**. The number of bytes read is determined by the length of the **buf** buffer. This API uses an asynchronous callback to return the result. Note: This method can only be used in the read mode ("r" or "rb") of **gzopen**.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|buf|ArrayBuffer|Yes|Target buffer for storing the read result.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int64>|Yes|Callback used to return the number of uncompressed bytes actually read.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzreadDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzread")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzread/test.gz"
    // Fill in the 16 bytes of data to be written.
    let writeBuffer = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        writeBuffer[i] = UInt8(i)
    }
    let readBuffer = ArrayBuffer(16, repeat: 0)
    // Step 7: Close the file after reading ends, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 6: Read the file content.
    let gzreadCallback: AsyncCallback<Int64> = {
        err: Option<BusinessException>, data: Option<Int64> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzread error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzread success, read is ${value}")
                    try {
                        gzip.gzclose(finalCloseCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzread failed")
            }
        }
    }
    // Step 5: Reopen the file in read mode.
    let openReadCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen read mode success")
                try {
                    gzip.gzread(readBuffer, gzreadCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzread error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 4: Close the file after writing is complete.
    let closeWriteCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzclose success")
                try {
                    gzip.gzopen(path, "rb", openReadCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 3: Compress the data and write it to the file.
    let gzwriteCallback: AsyncCallback<Int64> = {
        err: Option<BusinessException>, data: Option<Int64> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) => 
                    Hilog.info(0, "test", "gzwrite success, written is ${value}")
                    try {
                        gzip.gzclose(closeWriteCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzwrite failed")
            }
        }
    }
    // Step 1: Open the file in write mode, and read the data after writing.
    let openWriteCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen write mode success")
                try {
                    gzip.gzwrite(writeBuffer, 16, gzwriteCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", openWriteCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzreadDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

### func gzwrite(ArrayBuffer, Int64, AsyncCallback\<Int64>)

```cangjie
public func gzwrite(buf: ArrayBuffer, len: Int64, callback: AsyncCallback<Int64>): Unit
```

**Function:** Compresses the uncompressed bytes of the declared length in the buffer and writes them to the file. This API uses an asynchronous callback to return the result. Note: This method can only be used in the write mode ("w" or "wb") of **gzopen**.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|buf|ArrayBuffer|Yes|Data buffer pointed by an object to be written.|
|len|Int64|Yes|Length of uncompressed bytes, in bytes. Value range: [0, min(buf.byteLength, 2147483647)).|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int64>|Yes|Callback used to return the number of uncompressed bytes written.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzwriteDemo(gzip: GZip): Unit {
    // The path used in the code must be an application sandbox path, such as /data/storage/el2/base/temp. It can also be obtained from the context.
    let pathDir = "/data/storage/el2/base/temp"
    // Ensure that the target directory exists. Ignore this exception if the directory already exists.
    try {
        FileIo.mkdir(pathDir + "/gzwrite")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzwrite/test.gz"
    // Fill in the 16 bytes of data to be written.
    let bufferWithData = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        bufferWithData[i] = UInt8(i)
    }
    // Step 3: Close the file after writing is complete, and the process ends. (In actual development, initiate the next step after the previous callback is complete.)
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // Step 2: Compress the data and write it to the file.
    let gzwriteCallback: AsyncCallback<Int64> = {
        err: Option<BusinessException>, data: Option<Int64> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) =>
                    Hilog.info(0, "test", "gzwrite success, written is ${value}")
                    try {
                        gzip.gzclose(gzcloseCallback)
                    } catch (e: BusinessException) {
                        Hilog.error(0, "test", "gzclose error: errcode is ${e.code}, message is ${e.message}")
                    }
                case _ => Hilog.error(0, "test", "gzwrite failed")
            }
        }
    }
    // Step 1: Open the file in write mode, and close the file after data writing.
    let gzopenCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzopen error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "gzopen success")
                try {
                    gzip.gzwrite(bufferWithData, 16, gzwriteCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "gzwrite error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        gzip.gzopen(path, "wb", gzopenCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "gzopen error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<GZip> = {
    err: Option<BusinessException>, data: Option<GZip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createGZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(gzip) => gzwriteDemo(gzip)
            case _ => Hilog.error(0, "test", "createGZip failed")
        }
    }
}

createGZip(createCallback)
```

## class Options

```cangjie
public class Options
```

**Function:** Defines options used to compress or decompress a ZIP file.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop level

```cangjie
public mut prop level: ?CompressLevel
```

**Function:** Compression level specified for compression or decompression. The default value is **CompressLevelDefaultCompression**.

**Type:** ?[CompressLevel](#enum-compresslevel)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop memLevel

```cangjie
public mut prop memLevel: ?MemLevel
```

**Function:** Memory level specified for compression. The default value is **MemLevelDefault**.

**Type:** ?[MemLevel](#enum-memlevel)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop strategy

```cangjie
public mut prop strategy: ?CompressStrategy
```

**Function:** Compression strategy specified for compression. The default value is **CompressStrategyDefaultStrategy**.

**Type:** ?[CompressStrategy](#enum-compressstrategy)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### init(?CompressLevel, ?MemLevel, ?CompressStrategy)

```cangjie
public init(
    level!: ?CompressLevel = None,
    memLevel!: ?MemLevel = None,
    strategy!: ?CompressStrategy = None
)
```

**Function:** A constructor used to create an **Options** object.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|level|?[CompressLevel](#enum-compresslevel)|No|None|**Named parameter.** Compression level specified for compression or decompression.|
|memLevel|?[MemLevel](#enum-memlevel)|No|None|**Named parameter.** Memory level specified for compression.|
|strategy|?[CompressStrategy](#enum-compressstrategy)|No|None|**Named parameter.** Compression strategy specified for compression.|

## class ZStream

```cangjie
public class ZStream
```

**Function:** Processes all the information required for compression and decompression.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop adler

```cangjie
public mut prop adler: ?UInt64
```

**Function:** Adler-32 or CRC-32 value of uncompressed data.

**Type:** ?UInt64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop availableIn

```cangjie
public mut prop availableIn: ?UInt32
```

**Function:** Number of bytes available for **nextIn**.

**Type:** ?UInt32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop availableOut

```cangjie
public mut prop availableOut: ?UInt32
```

**Function:** Number of remaining bytes available for **nextOut**.

**Type:** ?UInt32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop dataType

```cangjie
public mut prop dataType: ?Int32
```

**Function:** Binary or text of **deflate**, or decoding state of **inflate**.

**Type:** ?Int32

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop nextIn

```cangjie
public mut prop nextIn: ?ArrayBuffer
```

**Function:** Input bytes to be compressed.

**Type:** ?ArrayBuffer

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop nextOut

```cangjie
public mut prop nextOut: ?ArrayBuffer
```

**Function:** Output bytes after compression.

**Type:** ?ArrayBuffer

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop totalIn

```cangjie
public mut prop totalIn: ?UInt64
```

**Function:** Total number of input bytes read so far.

**Type:** ?UInt64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop totalOut

```cangjie
public mut prop totalOut: ?UInt64
```

**Function:** Total number of output bytes.

**Type:** ?UInt64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### init(?ArrayBuffer, ?UInt32, ?UInt64, ?ArrayBuffer, ?UInt32, ?UInt64, ?Int32, ?UInt64)

```cangjie
public init(
    nextIn!: ?ArrayBuffer = None,
    availableIn!: ?UInt32 = None,
    totalIn!: ?UInt64 = None,
    nextOut!: ?ArrayBuffer = None,
    availableOut!: ?UInt32 = None,
    totalOut!: ?UInt64 = None,
    dataType!: ?Int32 = None,
    adler!: ?UInt64 = None
)
```

**Function:** A constructor used to create a **ZStream** object.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|nextIn|?ArrayBuffer|No|None|**Named parameter.** Input bytes to be compressed.|
|availableIn|?UInt32|No|None|**Named parameter.** Number of bytes available for **nextIn**.|
|totalIn|?UInt64|No|None|**Named parameter.** Total number of input bytes read so far.|
|nextOut|?ArrayBuffer|No|None|**Named parameter.** Output bytes after compression.|
|availableOut|?UInt32|No|None|**Named parameter.** Number of remaining bytes available for **nextOut**.|
|totalOut|?UInt64|No|None|**Named parameter.** Total number of output bytes.|
|dataType|?Int32|No|None|**Named parameter.** Binary or text of **deflate**, or decoding state of **inflate**.|
|adler|?UInt64|No|None|**Named parameter.** Adler-32 or CRC-32 value of uncompressed data.|

## class Zip

```cangjie
public class Zip
```

**Function:** Defines the **Zip** instance. It provides APIs to zip or unzip data in Zlib, Deflate, or Gzip format.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### func compress(ArrayBuffer, ArrayBuffer, AsyncCallback\<ZipOutputInfo>, ?Int64)

```cangjie
public func compress(dest: ArrayBuffer, source: ArrayBuffer, callback: AsyncCallback<ZipOutputInfo>, sourceLen!: ?Int64 = None): Unit
```

**Function:** Compresses the source buffer into the destination buffer. This API uses an asynchronous callback to return the result. The compressed data can be decompressed by using [uncompress](#func-uncompressarraybuffer-arraybuffer-asynccallbackzipoutputinfo-int64).

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|dest|ArrayBuffer|Yes|-|Destination buffer.|
|source|ArrayBuffer|Yes|-|Source buffer.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ZipOutputInfo](#class-zipoutputinfo)>|Yes|-|Callback used to return the result status and the total size of the destination buffer.|
|sourceLen|?Int64|No|None|**Named parameter.** Length of the source data, in bytes. Value range: [0, source.byteLength]. If this parameter is not specified, source.byteLength is used by default.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the data to be compressed (31 bytes after UTF-8 encoding).
let arrayBufferIn = "hello world! 你好，世界！".toArray()
let arrayBufferOut = ArrayBuffer(100, repeat: 0)
let compressCallback: AsyncCallback<ZipOutputInfo> = {
    err: Option<BusinessException>, data: Option<ZipOutputInfo> => match (err) {
        case Some(e) => Hilog.error(0, "test", "compress error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "compress success")
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) =>
                try {
                    zip.compress(arrayBufferOut, arrayBufferIn, compressCallback, sourceLen: Some(20))
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "compress error: errcode is ${e.code}, message is ${e.message}")
                }  
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func compress2(ArrayBuffer, ArrayBuffer, CompressLevel, AsyncCallback\<ZipOutputInfo>, ?Int64)

```cangjie
public func compress2(dest: ArrayBuffer, source: ArrayBuffer, level: CompressLevel, callback: AsyncCallback<ZipOutputInfo>, sourceLen!: ?Int64 = None): Unit
```

**Function:** Compresses the source buffer into the destination buffer. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|dest|ArrayBuffer|Yes|-|Destination buffer.|
|source|ArrayBuffer|Yes|-|Source buffer.|
|level|[CompressLevel](#enum-compresslevel)|Yes|-|Compression level. For details, see the [CompressLevel](#enum-compresslevel) enumeration definition.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ZipOutputInfo](#class-zipoutputinfo)>|Yes|-|Callback used to return the result status and the total size of the destination buffer.|
|sourceLen|?Int64|No|None|**Named parameter.** Length of the source data, in bytes. Value range: [0, source.byteLength]. If this parameter is not specified, source.byteLength is used by default.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the data to be compressed (31 bytes after UTF-8 encoding).
let arrayBufferIn = "hello world! 你好，世界！".toArray()
let arrayBufferOut = ArrayBuffer(100, repeat: 0)
let compress2Callback: AsyncCallback<ZipOutputInfo> = {
    err: Option<BusinessException>, data: Option<ZipOutputInfo> => match (err) {
        case Some(e) => Hilog.error(0, "test", "compress2 error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "compress2 success")
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) =>
                try {
                    zip.compress2(arrayBufferOut, arrayBufferIn, CompressLevel.CompressLevelBestSpeed,
                        compress2Callback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "compress2 error: errcode is ${e.code}, message is ${e.message}")   
                }
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func compressBound(Int32, AsyncCallback\<Int32>)

```cangjie
public func compressBound(sourceLen: Int32, callback: AsyncCallback<Int32>): Unit
```

**Function:** Calculates the maximum size of the compressed data to be returned. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|sourceLen|Int32|Yes|Length of the source data.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|Callback used to return the maximum size of the compressed data.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the 12 bytes of data, and associate the source length with the data.
let str = "hello world!"
let arrayBufferIn = str.toArray()
let compressBoundCallback: AsyncCallback<Int32> = {
    err: Option<BusinessException>, data: Option<Int32> => match (err) {
        case Some(e) => Hilog.error(0, "test", "compressBound error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(value) => Hilog.info(0, "test", "compressBound success, bound is ${value}")
            case _ => Hilog.error(0, "test", "compressBound failed")
        }
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => zip.compressBound(Int32(str.size), compressBoundCallback)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func deflate(ZStream, CompressFlushMode, AsyncCallback\<ReturnStatus>)

```cangjie
public func deflate(strm: ZStream, flush: CompressFlushMode, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Deflates data. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|flush|[CompressFlushMode](#enum-compressflushmode)|Yes|Data flush mode during compression or decompression.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func deflateDemo(zip: Zip): Unit {
    // Fill in the 12 bytes of data to be compressed.
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // Step 3: Release the dynamically allocated data structures of the compression stream. (In actual development, initiate the next step after the previous callback is complete.)
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "deflateEnd success")
        }
    }
    // Step 2: Compress the data, and release the compression stream after compression is complete.
    let deflateCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflate error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflate success")
                try {
                    zip.deflateEnd(strm, deflateEndCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 1: Initialize the compression stream and compress the data.
    let deflateInit2Callback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflateInit2 success")
                try {
                    zip.deflate(strm, CompressFlushMode.Finish, deflateCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflate error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        zip.deflateInit2(strm, CompressLevel.CompressLevelBestSpeed, CompressMethod.Deflated, 15,
            MemLevel.MemLevelDefault, CompressStrategy.CompressStrategyDefaultStrategy, deflateInit2Callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => deflateDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func deflateEnd(ZStream, AsyncCallback\<ReturnStatus>)

```cangjie
public func deflateEnd(strm: ZStream, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Releases all dynamically allocated data structs of a compression stream. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func deflateEndDemo(zip: Zip): Unit {
    // Fill in the 12 bytes of data to be compressed.
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // Step 3: Release all dynamically allocated data structures of the compression stream after compression is complete. (In actual development, initiate the next step after the previous callback is complete.)
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "deflateEnd success")
        }
    }
    // Step 2: Compress the data.
    let deflateCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflate error: errcode is ${e.code}")
            case _ => {
                Hilog.info(0, "test", "deflate success")
                try {
                    zip.deflateEnd(strm, deflateEndCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}, message is ${e.message}")
                }
            }
        }
    }
    // Step 1: Initialize the compression stream and compress the data, and release the compression stream after compression is complete.
    let deflateInit2Callback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}")
            case _ => {
                Hilog.info(0, "test", "deflateInit2 success")
                try {
                    zip.deflate(strm, CompressFlushMode.Finish, deflateCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflate error: errcode is ${e.code}, message is ${e.message}")
                }
            }
        }
    }
    try {
        zip.deflateInit2(strm, CompressLevel.CompressLevelBestSpeed, CompressMethod.Deflated, 15,
            MemLevel.MemLevelDefault, CompressStrategy.CompressStrategyDefaultStrategy, deflateInit2Callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => deflateEndDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func deflateInit2(ZStream, CompressLevel, CompressMethod, Int32, MemLevel, CompressStrategy, AsyncCallback\<ReturnStatus>)

```cangjie
public func deflateInit2(strm: ZStream, level: CompressLevel, method: CompressMethod, windowBits: Int32, memLevel: MemLevel, strategy: CompressStrategy, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Initializes a compression stream with the specified compression level, compression method, window size, memory level, and compression strategy. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|level|[CompressLevel](#enum-compresslevel)|Yes|Compression level. For details, see the [CompressLevel](#enum-compresslevel) enumeration definition.|
|method|[CompressMethod](#enum-compressmethod)|Yes|Enumeration type of the compression method, which specifies the DEFLATED compression method.|
|windowBits|Int32|Yes|Memory window size. The value is restricted in certain range based on the data formats. The options are as follows:<br>Zlib: [1, 15]<br>Gzip: (15, +∞)<br>Raw Deflate: [-15, -1]|
|memLevel|[MemLevel](#enum-memlevel)|Yes|Memory level. For details, see the [MemLevel](#enum-memlevel) enumeration definition.|
|strategy|[CompressStrategy](#enum-compressstrategy)|Yes|Compression strategy. For details, see the [CompressStrategy](#enum-compressstrategy) enumeration definition.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the 12 bytes of data to be compressed.
let arrayBufferIn = "hello world!".toArray()
let arrayBufferOut = ArrayBuffer(100, repeat: 0)
let deflateInit2Callback: AsyncCallback<ReturnStatus> = {
    err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
        case Some(e) => Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "deflateInit2 success")
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) =>
                let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
                    nextOut: arrayBufferOut, availableOut: 100)
                try {
                    zip.deflateInit2(strm, CompressLevel.CompressLevelBestSpeed, CompressMethod.Deflated, 28,
                        MemLevel.MemLevelDefault, CompressStrategy.CompressStrategyDefaultStrategy,
                        deflateInit2Callback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}, message is ${e.message}")
                }
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func getZStream(AsyncCallback\<ZStream>)

```cangjie
public func getZStream(callback: AsyncCallback<ZStream>): Unit
```

**Function:** Obtains this stream. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ZStream](#class-zstream)>|Yes|Callback used to return the **ZStream** object, which manages the data streams during compression and decompression.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func getZStreamDemo(zip: Zip): Unit {
    // Fill in the 12 bytes of data.
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // Step 2: Obtain the stream object instance. (In actual development, initiate the next step after the previous callback is complete.)
    let getZStreamCallback: AsyncCallback<ZStream> = {
        err: Option<BusinessException>, data: Option<ZStream> => match (err) {
            case Some(e) => Hilog.error(0, "test", "getZStream error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) => Hilog.info(0, "test", "getZStream success")
                case _ => Hilog.error(0, "test", "getZStream failed")
            }
        }
    }
    // Step 1: Initialize the stream and then obtain the stream object instance. The stream must be initialized by deflateInit2 or inflateInit first.
    let inflateInitCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateInit error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "inflateInit success")
                zip.getZStream(getZStreamCallback)
        }
    }
    zip.inflateInit(strm, inflateInitCallback)
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => getZStreamDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func inflate(ZStream, CompressFlushMode, AsyncCallback\<ReturnStatus>)

```cangjie
public func inflate(strm: ZStream, flush: CompressFlushMode, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Inflates data. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|flush|[CompressFlushMode](#enum-compressflushmode)|Yes|Data flush mode during compression or decompression.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800005 | The input data is incorrect. For example, the data does not conform to the zlib compression format, the compressed data is corrupted, or the data is not compressed. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func inflateDemo(zip: Zip): Unit {
    // Fill in the 12 bytes of data to be compressed.
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let compressStrm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // For decompression, the input is the compressed data and the output is the original data.
    let decompressStrm = ZStream(nextIn: arrayBufferOut, availableIn: 100,
        nextOut: arrayBufferIn, availableOut: 12)
    // Step 6: Release the dynamically allocated data structures of the decompression stream. (In actual development, initiate the next step after the previous callback is complete.)
    let inflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "inflateEnd success")
        }
    }
    // Step 5: Decompress the data, and release the decompression stream after decompression is complete.
    let inflateCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflate error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "inflate success")
                try {
                    zip.inflateEnd(decompressStrm, inflateEndCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 4: Initialize the decompression stream.
    let inflateInitCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateInit error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "inflateInit success")
                try {
                    zip.inflate(decompressStrm, CompressFlushMode.NoFlush, inflateCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "inflate error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 3: Release the compression stream.
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflateEnd success")
                zip.inflateInit(decompressStrm, inflateInitCallback)
        }
    }
    // Step 2: Compress the data.
    let deflateCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflate error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflate success")
                try {
                    zip.deflateEnd(compressStrm, deflateEndCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    // Step 1: Initialize the compression stream and compress the data, and decompress the compressed data after compression is complete.
    let deflateInit2Callback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflateInit2 success")
                try {
                    zip.deflate(compressStrm, CompressFlushMode.Finish, deflateCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "deflate error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        zip.deflateInit2(compressStrm, CompressLevel.CompressLevelBestSpeed, CompressMethod.Deflated, 15,
            MemLevel.MemLevelDefault, CompressStrategy.CompressStrategyDefaultStrategy, deflateInit2Callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "deflateInit2 error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => inflateDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func inflateEnd(ZStream, AsyncCallback\<ReturnStatus>)

```cangjie
public func inflateEnd(strm: ZStream, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Releases all dynamically allocated data structs of a decompression stream. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func inflateEndDemo(zip: Zip): Unit {
    // Data compressed from "hello world!" using deflate (20 bytes).
    let compressedData: ArrayBuffer = [0x78, 0x9C, 0xCB, 0x48, 0xCD, 0xC9, 0xC9, 0x57, 0x28, 0xCF,
        0x2F, 0xCA, 0x49, 0x51, 0x04, 0x00, 0x1E, 0x89, 0x04, 0x7E]
    // The original data "hello world!" can be restored after decompression (12 bytes).
    let decompressedBuffer = ArrayBuffer(12, repeat: 0)
    let strm = ZStream(nextIn: compressedData, availableIn: 20,
        nextOut: decompressedBuffer, availableOut: 12)
    // Step 3: Release the dynamically allocated data structures of the decompression stream after decompression is complete. (In actual development, initiate the next step after the previous callback is complete.)
    let inflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "inflateEnd success")
        }
    }
    // Step 2: Decompress the data.
    let inflateCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflate error: errcode is ${e.code}")
            case _ => {
                Hilog.info(0, "test", "inflate success")
                try {
                    zip.inflateEnd(strm, inflateEndCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}, message is ${e.message}")
                }
            }
        }
    }
    // Step 1: Initialize the decompression stream and decompress the data, and release the decompression stream after decompression is complete.
    let inflateInitCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateInit error: errcode is ${e.code}")
            case _ => {
                Hilog.info(0, "test", "inflateInit success")
                try {
                    zip.inflate(strm, CompressFlushMode.NoFlush, inflateCallback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "inflate error: errcode is ${e.code}, message is ${e.message}")
                }
            }
        }
    }
    zip.inflateInit(strm, inflateInitCallback)
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => inflateEndDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func inflateInit(ZStream, AsyncCallback\<ReturnStatus>)

```cangjie
public func inflateInit(strm: ZStream, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Initializes a decompression stream. This API uses an asynchronous callback to return the result. Call this API to initialize the decompression stream before calling **inflate** to decompress data, and call **inflateEnd** to release resources.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the 12 bytes of data.
let arrayBufferIn = "hello world!".toArray()
let arrayBufferOut = ArrayBuffer(100, repeat: 0)
let inflateInitCallback: AsyncCallback<ReturnStatus> = {
    err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
        case Some(e) => Hilog.error(0, "test", "inflateInit error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "inflateInit success")
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) =>
                let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
                    nextOut: arrayBufferOut, availableOut: 100)
                zip.inflateInit(strm, inflateInitCallback)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func inflateInit2(ZStream, Int32, AsyncCallback\<ReturnStatus>)

```cangjie
public func inflateInit2(strm: ZStream, windowBits: Int32, callback: AsyncCallback<ReturnStatus>): Unit
```

**Function:** Initializes a decompression stream with the specified **windowBits**. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|strm|[ZStream](#class-zstream)|Yes|Data stream management object for zlib compression and decompression.|
|windowBits|Int32|Yes|Memory window size. The value is restricted in certain range based on the data formats. The options are as follows:<br>Zlib: [1, 15]<br>Gzip: (15, +∞)<br>Raw Deflate: [-15, -1]|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ReturnStatus](#enum-returnstatus)>|Yes|Callback used to return the result status.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Fill in the 12 bytes of data.
let arrayBufferIn = "hello world!".toArray()
let arrayBufferOut = ArrayBuffer(100, repeat: 0)
let inflateInit2Callback: AsyncCallback<ReturnStatus> = {
    err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
        case Some(e) => Hilog.error(0, "test", "inflateInit2 error: errcode is ${e.code}")
        case _ => Hilog.info(0, "test", "inflateInit2 success")
    }
}
let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) =>
                let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
                    nextOut: arrayBufferOut, availableOut: 100)
                try {
                    zip.inflateInit2(strm, 28, inflateInit2Callback)
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "inflateInit2 error: errcode is ${e.code}, message is ${e.message}")
                }
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

### func uncompress(ArrayBuffer, ArrayBuffer, AsyncCallback\<ZipOutputInfo>, ?Int64)

```cangjie
public func uncompress(dest: ArrayBuffer, source: ArrayBuffer, callback: AsyncCallback<ZipOutputInfo>, sourceLen!: ?Int64 = None): Unit
```

**Function:** Decompresses the compressed data into the raw data. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|dest|ArrayBuffer|Yes|-|Destination buffer.|
|source|ArrayBuffer|Yes|-|Source buffer.|
|callback|[AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallback)\<[ZipOutputInfo](#class-zipoutputinfo)>|Yes|-|Callback used to return the result status and the total size of the destination buffer.|
|sourceLen|?Int64|No|None|**Named parameter.** Length of the source data, in bytes. Value range: [0, source.byteLength]. If this parameter is not specified, source.byteLength is used by default.|

**Error Codes:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../../reference/cj-errorcode-universal.md) and [zlib Error Codes](./cj-errorcode-zlib.md).

  | Error Code ID| Error Message |
  | :--- | :--- |
  | 17800005 | The input data is incorrect. For example, the data does not conform to the zlib compression format, the compressed data is corrupted, or the data is not compressed. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**Example:**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func uncompressDemo(zip: Zip): Unit {
    // Fill in the 12 bytes of data to be compressed.
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    // Step 2: Decompress the compressed data. (In actual development, initiate the next step after the previous callback is complete.)
    let uncompressCallback: AsyncCallback<ZipOutputInfo> = {
        err: Option<BusinessException>, data: Option<ZipOutputInfo> => match (err) {
            case Some(e) => Hilog.error(0, "test", "uncompress error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "uncompress success")
        }
    }
    // Step 1: Compress the data, and decompress it in the callback after compression is complete.
    let compressCallback: AsyncCallback<ZipOutputInfo> = {
        err: Option<BusinessException>, data: Option<ZipOutputInfo> => match (err) {
            case Some(e) => Hilog.error(0, "test", "compress error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "compress success")
                try {
                    zip.uncompress(arrayBufferIn, arrayBufferOut, uncompressCallback, sourceLen: Some(20))
                } catch (e: BusinessException) {
                    Hilog.error(0, "test", "uncompress error: errcode is ${e.code}, message is ${e.message}")
                }
        }
    }
    try {
        zip.compress(arrayBufferOut, arrayBufferIn, compressCallback, sourceLen: Some(12))
    } catch (e: BusinessException) {
        Hilog.error(0, "test", "compress error: errcode is ${e.code}, message is ${e.message}")
    }
}

let createCallback: AsyncCallback<Zip> = {
    err: Option<BusinessException>, data: Option<Zip> => match (err) {
        case Some(e) => Hilog.error(0, "test", "createZip error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(zip) => uncompressDemo(zip)
            case _ => Hilog.error(0, "test", "createZip failed")
        }
    }
}

createZip(createCallback)
```

## class ZipOutputInfo

```cangjie
public class ZipOutputInfo
```

**Function:** Compression and decompression return value information.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop destLen

```cangjie
public mut prop destLen: Int64
```

**Function:** Total length of the destination buffer.

**Type:** Int64

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### prop status

```cangjie
public mut prop status: ReturnStatus
```

**Function:** Result status of the compression or decompression function, including the success status and various error statuses. For details, see [ReturnStatus](#enum-returnstatus).

**Type:** [ReturnStatus](#enum-returnstatus)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum CompressFlushMode

```cangjie
public enum CompressFlushMode
```

**Function:** Represents the data flush mode during compression or decompression.

**Extensions:**

- [extend CompressFlushMode <: ToString](#extend-compressflushmode-tostring)
- [extend CompressFlushMode <: Equatable<CompressFlushMode>](#extend-compressflushmode-equatablecompressflushmode)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Block

```cangjie
Block
```

**Function:** Allows more precise control.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Finish

```cangjie
Finish
```

**Function:** Ends the compression or decompression process. Suitable for the last step of the compression process to ensure that all data is completely output.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### FullFlush

```cangjie
FullFlush
```

**Function:** Resets the compression state. Suitable for scenarios where the compression stream needs to be completely reset, such as compressing multiple independent data blocks.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### NoFlush

```cangjie
NoFlush
```

**Function:** Default value, indicating a normal operation.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### PartialFlush

```cangjie
PartialFlush
```

**Function:** Generates some refresh points in the stream. Suitable for scenarios requiring sync points so that the decompression stream can be restored.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### SyncFlush

```cangjie
SyncFlush
```

**Function:** Forcibly outputs all compressed data while maintaining the compression stream state. Suitable for scenarios requiring real-time compressed data output, such as network transmission.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Trees

```cangjie
Trees
```

**Function:** Implements special purposes.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum CompressLevel

```cangjie
public enum CompressLevel
```

**Function:** Represents compression levels.

**Extensions:**

- [extend CompressLevel <: ToString](#extend-compresslevel-tostring)
- [extend CompressLevel <: Equatable<CompressLevel>](#extend-compresslevel-equatablecompresslevel)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressLevelBestCompression

```cangjie
CompressLevelBestCompression
```

**Function:** Compression level 9 that gives the best compression, at a slower speed. Suitable for scenarios sensitive to storage space.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressLevelBestSpeed

```cangjie
CompressLevelBestSpeed
```

**Function:** Compression level 1 that gives the best speed, with a lower compression ratio. Suitable for scenarios with high real-time requirements.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressLevelDefaultCompression

```cangjie
CompressLevelDefaultCompression
```

**Function:** Default compression level, which strikes a balance between compression speed and compression ratio. Suitable for most scenarios.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressLevelNoCompression

```cangjie
CompressLevelNoCompression
```

**Function:** Compression level 0 that indicates no compression. Suitable for scenarios where data does not need to be compressed, such as already compressed images or video files.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum CompressMethod

```cangjie
public enum CompressMethod
```

**Function:** Represents compression methods. The deflate compression method; only this method is supported in the current version.

**Extensions:**

- [extend CompressMethod <: ToString](#extend-compressmethod-tostring)
- [extend CompressMethod <: Equatable<CompressMethod>](#extend-compressmethod-equatablecompressmethod)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Deflated

```cangjie
Deflated
```

**Function:** Compresses data using the DEFLATE algorithm, which is the standard compression method of the zlib library.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum CompressStrategy

```cangjie
public enum CompressStrategy
```

**Function:** Represents compression strategies.

**Extensions:**

- [extend CompressStrategy <: ToString](#extend-compressstrategy-tostring)
- [extend CompressStrategy <: Equatable<CompressStrategy>](#extend-compressstrategy-equatablecompressstrategy)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressStrategyDefaultStrategy

```cangjie
CompressStrategyDefaultStrategy
```

**Function:** Default compression strategy, applicable to most data types and providing balanced compression performance.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressStrategyFiltered

```cangjie
CompressStrategyFiltered
```

**Function:** Compression strategy for data generated by filters. Suitable for data that has been preprocessed or filtered, such as delta-encoded data.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressStrategyFixed

```cangjie
CompressStrategyFixed
```

**Function:** Fixed compression strategy. Uses fixed Huffman coding, suitable for scenarios requiring fixed coding output.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressStrategyHuffmanOnly

```cangjie
CompressStrategyHuffmanOnly
```

**Function:** Huffman coding compression strategy. Uses only Huffman coding without string matching, suitable for scenarios requiring fast compression.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### CompressStrategyRle

```cangjie
CompressStrategyRle
```

**Function:** RLE compression strategy. Suitable for data containing a large number of repeated bytes, such as bitmap images.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum MemLevel

```cangjie
public enum MemLevel
```

**Function:** Represents memory levels used during compression.

**Extensions:**

- [extend MemLevel <: ToString](#extend-memlevel-tostring)
- [extend MemLevel <: Equatable<MemLevel>](#extend-memlevel-equatablememlevel)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### MemLevelDefault

```cangjie
MemLevelDefault
```

**Function:** Default memory used by the **zlib** API during compression, which strikes a balance between compression speed and memory usage. Suitable for most scenarios.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### MemLevelMax

```cangjie
MemLevelMax
```

**Function:** Maximum memory used by the **zlib** API during compression, with the fastest compression speed but the highest memory usage. Suitable for scenarios with sufficient memory.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### MemLevelMin

```cangjie
MemLevelMin
```

**Function:** Minimum memory used by the **zlib** API during compression, with the slowest compression speed but the lowest memory usage. Suitable for memory-constrained scenarios.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## enum ReturnStatus

```cangjie
public enum ReturnStatus
```

**Function:** Represents the return statuses of compression and decompression functions, including success statuses and various error statuses.

**Extensions:**

- [extend ReturnStatus <: ToString](#extend-returnstatus-tostring)
- [extend ReturnStatus <: Equatable<ReturnStatus>](#extend-returnstatus-equatablereturnstatus)

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### BufError

```cangjie
BufError
```

**Function:** The API fails to be called, indicating that the input buffer is incorrect.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### DataError

```cangjie
DataError
```

**Function:** The API fails to be called, indicating that the input data is incorrect.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Errno

```cangjie
Errno
```

**Function:** The API fails to be called, indicating that the file operation is incorrect.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### MemError

```cangjie
MemError
```

**Function:** The API fails to be called, indicating that the memory allocation fails.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### NeedDict

```cangjie
NeedDict
```

**Function:** The API is successfully called, indicating that a preset dictionary is required to continue decompression.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### Ok

```cangjie
Ok
```

**Function:** The API is successfully called. This enum value can be used in atomic services.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### StreamEnd

```cangjie
StreamEnd
```

**Function:** The API is successfully called, indicating that the entire data has been processed.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

### StreamError

```cangjie
StreamError
```

**Function:** The API fails to be called, indicating that the compression or decompression stream is incorrect.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

## extend CompressFlushMode <: Equatable<CompressFlushMode>

```cangjie
extend CompressFlushMode <: Equatable<CompressFlushMode>
```

**Function:** Implements the Equatable\<CompressFlushMode> interface for the CompressFlushMode type, enabling equality comparison.

**Extended Type:**

- [CompressFlushMode](#enum-compressflushmode)

**Extended Interfaces:**

- Equatable\<[CompressFlushMode](#enum-compressflushmode)>

### func ==(CompressFlushMode)

```cangjie
public operator func ==(other: CompressFlushMode): Bool
```

**Function:** Performs equality comparison on data flush modes.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressFlushMode](#enum-compressflushmode)|Yes|Data flush mode.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the data flush modes are the same; returns false otherwise.|

### func !=(CompressFlushMode)

```cangjie
public operator func !=(other: CompressFlushMode): Bool
```

**Function:** Performs inequality comparison on data flush modes.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressFlushMode](#enum-compressflushmode)|Yes|Data flush mode.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the data flush modes are different; returns false otherwise.|

## extend CompressFlushMode <: ToString

```cangjie
extend CompressFlushMode <: ToString
```

**Function:** Implements the ToString interface for the CompressFlushMode type, enabling string conversion.

**Extended Type:**

- [CompressFlushMode](#enum-compressflushmode)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the data flush mode.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the data flush mode value.|

## extend CompressLevel <: Equatable<CompressLevel>

```cangjie
extend CompressLevel <: Equatable<CompressLevel>
```

**Function:** Implements the Equatable\<CompressLevel> interface for the CompressLevel type, enabling equality comparison.

**Extended Type:**

- [CompressLevel](#enum-compresslevel)

**Extended Interfaces:**

- Equatable\<[CompressLevel](#enum-compresslevel)>

### func ==(CompressLevel)

```cangjie
public operator func ==(other: CompressLevel): Bool
```

**Function:** Performs equality comparison on compression levels.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressLevel](#enum-compresslevel)|Yes|Compression level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression levels are the same; returns false otherwise.|

### func !=(CompressLevel)

```cangjie
public operator func !=(other: CompressLevel): Bool
```

**Function:** Performs inequality comparison on compression levels.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressLevel](#enum-compresslevel)|Yes|Compression level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression levels are different; returns false otherwise.|

## extend CompressLevel <: ToString

```cangjie
extend CompressLevel <: ToString
```

**Function:** Implements the ToString interface for the CompressLevel type, enabling string conversion.

**Extended Type:**

- [CompressLevel](#enum-compresslevel)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the compression level.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the compression level value.|

## extend CompressMethod <: Equatable<CompressMethod>

```cangjie
extend CompressMethod <: Equatable<CompressMethod>
```

**Function:** Implements the Equatable\<CompressMethod> interface for the CompressMethod type, enabling equality comparison.

**Extended Type:**

- [CompressMethod](#enum-compressmethod)

**Extended Interfaces:**

- Equatable\<[CompressMethod](#enum-compressmethod)>

### func ==(CompressMethod)

```cangjie
public operator func ==(other: CompressMethod): Bool
```

**Function:** Performs equality comparison on compression methods.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressMethod](#enum-compressmethod)|Yes|Compression method.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression methods are the same; returns false otherwise.|

### func !=(CompressMethod)

```cangjie
public operator func !=(other: CompressMethod): Bool
```

**Function:** Performs inequality comparison on compression methods.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressMethod](#enum-compressmethod)|Yes|Compression method.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression methods are different; returns false otherwise.|

## extend CompressMethod <: ToString

```cangjie
extend CompressMethod <: ToString
```

**Function:** Implements the ToString interface for the CompressMethod type, enabling string conversion.

**Extended Type:**

- [CompressMethod](#enum-compressmethod)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the compression method.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the compression method value.|

## extend CompressStrategy <: Equatable<CompressStrategy>

```cangjie
extend CompressStrategy <: Equatable<CompressStrategy>
```

**Function:** Implements the Equatable\<CompressStrategy> interface for the CompressStrategy type, enabling equality comparison.

**Extended Type:**

- [CompressStrategy](#enum-compressstrategy)

**Extended Interfaces:**

- Equatable\<[CompressStrategy](#enum-compressstrategy)>

### func ==(CompressStrategy)

```cangjie
public operator func ==(other: CompressStrategy): Bool
```

**Function:** Performs equality comparison on compression strategies.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressStrategy](#enum-compressstrategy)|Yes|Compression strategy.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression strategies are the same; returns false otherwise.|

### func !=(CompressStrategy)

```cangjie
public operator func !=(other: CompressStrategy): Bool
```

**Function:** Performs inequality comparison on compression strategies.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[CompressStrategy](#enum-compressstrategy)|Yes|Compression strategy.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the compression strategies are different; returns false otherwise.|

## extend CompressStrategy <: ToString

```cangjie
extend CompressStrategy <: ToString
```

**Function:** Implements the ToString interface for the CompressStrategy type, enabling string conversion.

**Extended Type:**

- [CompressStrategy](#enum-compressstrategy)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the compression strategy.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the compression strategy value.|

## extend MemLevel <: Equatable<MemLevel>

```cangjie
extend MemLevel <: Equatable<MemLevel>
```

**Function:** Implements the Equatable\<MemLevel> interface for the MemLevel type, enabling equality comparison.

**Extended Type:**

- [MemLevel](#enum-memlevel)

**Extended Interfaces:**

- Equatable\<[MemLevel](#enum-memlevel)>

### func ==(MemLevel)

```cangjie
public operator func ==(other: MemLevel): Bool
```

**Function:** Performs equality comparison on memory levels.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[MemLevel](#enum-memlevel)|Yes|Memory level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the memory levels are the same; returns false otherwise.|

### func !=(MemLevel)

```cangjie
public operator func !=(other: MemLevel): Bool
```

**Function:** Performs inequality comparison on memory levels.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[MemLevel](#enum-memlevel)|Yes|Memory level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the memory levels are different; returns false otherwise.|

## extend MemLevel <: ToString

```cangjie
extend MemLevel <: ToString
```

**Function:** Implements the ToString interface for the MemLevel type, enabling string conversion.

**Extended Type:**

- [MemLevel](#enum-memlevel)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the memory level.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the memory level value.|

## extend ReturnStatus <: Equatable<ReturnStatus>

```cangjie
extend ReturnStatus <: Equatable<ReturnStatus>
```

**Function:** Implements the Equatable\<ReturnStatus> interface for the ReturnStatus type, enabling equality comparison.

**Extended Type:**

- [ReturnStatus](#enum-returnstatus)

**Extended Interfaces:**

- Equatable\<[ReturnStatus](#enum-returnstatus)>

### func ==(ReturnStatus)

```cangjie
public operator func ==(other: ReturnStatus): Bool
```

**Function:** Performs equality comparison on result statuses.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[ReturnStatus](#enum-returnstatus)|Yes|Result status.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the result statuses are the same; returns false otherwise.|

### func !=(ReturnStatus)

```cangjie
public operator func !=(other: ReturnStatus): Bool
```

**Function:** Performs inequality comparison on result statuses.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Parameters:**

|Parameter|Type|Required|Description|
|:---|:---|:---|:---|
|other|[ReturnStatus](#enum-returnstatus)|Yes|Result status.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if the result statuses are different; returns false otherwise.|

## extend ReturnStatus <: ToString

```cangjie
extend ReturnStatus <: ToString
```

**Function:** Implements the ToString interface for the ReturnStatus type, enabling string conversion.

**Extended Type:**

- [ReturnStatus](#enum-returnstatus)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the result status.

**System Capability:** SystemCapability.BundleManager.Zlib

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the result status value.|
