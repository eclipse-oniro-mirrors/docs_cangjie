# ohos.zlib（Zip模块）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

本模块基于zlib库开发，提供文件压缩和解压缩能力。采用DEFLATE算法，支持zlib、deflate和gzip格式的数据处理。

## 导入模块

```cangjie
import kit.BasicServicesKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../../reference/cj-development-intro.md#仓颉示例代码说明)。

## func compressFile(String, String, Options, AsyncCallback\<Unit>)

```cangjie
public func compressFile(inFile: String, outFile: String, options: Options, callback: AsyncCallback<Unit>): Unit
```

**功能：** 压缩文件。使用callback异步回调。

> **说明：**
>
> 为了避免路径穿越，inFile和outFile传入的参数不允许包含“../”，否则会返回900001、900002错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| inFile | String | 是 | - | 指定压缩的文件夹路径或者文件路径，路径必须为沙箱路径，沙箱路径可以通过context获取。待压缩的文件夹不可为空，否则使用decompressFile对压缩后的文件解压时会报错。 |
| outFile | String | 是 | - | 指定的压缩结果的文件路径。路径必须为沙箱路径，沙箱路径可以通过context获取。并发执行多个压缩任务时，各任务的outFile不能相同，否则可能导致压缩失败或输出文件损坏。 |
| options | [Options](#class-options) | 是 | - | 压缩的配置参数。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | - | 异步获取压缩结果之后的回调。成功时返回None，失败时返回具体错误码。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
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

**功能：** 压缩指定的多个文件。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| inFiles | Array\<String> | 是 | - | 指定压缩的文件夹路径或者文件路径，路径必须为沙箱路径，沙箱路径可以通过context获取。待压缩的文件夹不可为空，否则使用decompressFile对压缩后的文件解压时会报错。 |
| outFile | String | 是 | - | 指定的压缩结果的文件路径。路径必须为沙箱路径，沙箱路径可以通过context获取。多线程并发执行多个压缩任务时，各任务的outFile不能相同，否则可能导致压缩失败或输出文件损坏。 |
| options | [Options](#class-options) | 是 | - | 压缩的配置参数。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | - | 异步获取压缩结果之后的回调。成功时返回None，失败时返回具体错误码。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
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

**功能：** 创建校验对象。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[Checksum](#class-checksum)> | 是 | 回调，返回创建的校验对象。 |

**示例：**

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

**功能：** 创建GZip对象。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[GZip](#class-gzip)> | 是 | 回调，返回创建的GZip对象。 |

**示例：**

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

**功能：** 创建压缩解压缩对象实例。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[Zip](#class-zip)> | 是 | 回调，返回创建的Zip对象实例。 |

**示例：**

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

**功能：** 解压文件。使用callback异步回调。

> **说明：**
>
> - 为了避免路径穿越，inFile和outFile传入的参数不允许包含“../”，否则会返回900001、900002错误码。
> - 传入的压缩包内部文件或者文件夹名称不能包含“../”，否则会返回900003错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| inFile | String | 是 | - | 指定的待解压缩文件的文件路径，文件后缀需要以.zip结尾。路径必须为沙箱路径，沙箱路径可以通过context获取。如果待解压的.zip文件中包含中文的文件名或目录名，需使用UTF-8进行编码，避免解压时文件名或目录名出现中文乱码。 |
| outFile | String | 是 | - | 指定的解压后的文件夹路径，文件夹目录路径需要在系统中存在，不存在则会解压失败。路径必须为沙箱路径，沙箱路径可以通过context获取。如果待解压的文件或文件夹在解压后的路径下已经存在，则会直接覆盖同名文件或同名文件夹中的同名文件。多线程同时解压文件时，outFile不能相同，否则会导致解压数据相互覆盖或文件损坏。 |
| options | [Options](#class-options) | 是 | - | 解压的配置参数。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | - | 异步获取解压结果之后的回调。成功时返回None，失败时返回具体错误码。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
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

**功能：** 解压文件。使用callback异步回调。

> **说明：**
>
> - 为了避免路径穿越，inFile和outFile传入的参数不允许包含“../”，否则会返回900001、900002错误码。
> - 传入的压缩包内部文件或者文件夹名称不能包含“../”，否则会返回900003错误码。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| inFile | String | 是 | 指定的待解压缩文件的文件路径，文件后缀需要以.zip结尾。路径必须为沙箱路径，沙箱路径可以通过context获取。如果待解压的.zip文件中包含中文的文件名或目录名，需使用UTF-8进行编码，避免解压时文件名或目录名出现中文乱码。 |
| outFile | String | 是 | 指定的解压后的文件夹路径，文件夹目录路径需要在系统中存在，不存在则会解压失败。路径必须为沙箱路径，沙箱路径可以通过context获取。如果待解压的文件或文件夹在解压后的路径下已经存在，则会直接覆盖同名文件或同名文件夹中的同名文件。多线程同时解压文件时，outFile不能相同，否则会导致解压数据相互覆盖或文件损坏。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | 异步获取解压结果之后的回调。成功时返回None，失败时返回具体错误码。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900002 | The input destination file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
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

**功能：** 获取压缩文件的原始大小。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| compressedFile | String | 是 | 指定的压缩文件的文件路径，只支持zip格式压缩文件。路径必须为沙箱路径，沙箱路径可以通过context获取。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int64> | 是 | 回调，返回压缩文件的原始大小，单位：字节。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 900001 | The input source file is invalid. |
  | 900003 | The input source file is not in ZIP format or is damaged. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
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

**功能：** 校验对象，用于计算和验证数据校验和。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### func crc32(UInt64, ArrayBuffer, AsyncCallback\<UInt64>)

```cangjie
public func crc32(crc: UInt64, buf: ArrayBuffer, callback: AsyncCallback<UInt64>): Unit
```

**功能：** 更新CRC-32校验和。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| crc | UInt64 | 是 | CRC-32校验和的初始值。 |
| buf | ArrayBuffer | 是 | 计算校验和数据缓冲区。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<UInt64> | 是 | 回调，返回更新后的CRC-32校验和。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充待计算校验和的12字节数据
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

**功能：** GZip对象，提供gzip文件读写相关接口。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### func gzclose(AsyncCallback\<ReturnStatus>)

```cangjie
public func gzclose(callback: AsyncCallback<ReturnStatus>): Unit
```

**功能：** 清除文件的所有挂起输出，如有必要，关闭文件和释放（解）压缩状态。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800006 | Memory allocation failed. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzcloseDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzclose")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzclose/test.gz"
    // 步骤2：关闭文件并释放状态，流程结束（实际开发中需在上一回调完成后发起下一步）
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤1：以写模式打开文件，打开成功后关闭
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

**功能：** 将gzFile与文件描述符fd相关联，打开文件，用于进行读取并解压缩，或者压缩并写入。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| fd | Int32 | 是 | 文件描述符。通常情况下，通过系统调用open或其他方法获得。 |
| mode | String | 是 | 用于指定访问模式。详情与[gzopen](#func-gzopenstring-string-asynccallbackunit)一致。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | 回调，无返回结果。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800002 | No such file or access mode error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzdopenDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzdopen")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    // 步骤2：关闭文件（实际开发中需在上一回调完成后发起下一步）
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤1：将gzFile与文件描述符fd关联，成功后关闭文件
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
    // 打开文件获取文件描述符fd，然后将gzFile与fd关联
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

**功能：** 检查gzip压缩文件的读取位置是否已到达文件的末尾。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32> | 是 | 回调，如果在读取时设置了文件的文件结束指示符，则返回1。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzeofDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzeof")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzeof/test.gz"
    // 填充16字节的待写入数据
    let writeBufferWithData = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        writeBufferWithData[i] = UInt8(i)
    }
    let readBufferWithData = ArrayBuffer(20, repeat: 0)
    // 步骤8：读取结束后关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤7：检查读取位置是否到达文件末尾
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
    // 步骤6：读取文件内容
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
    // 步骤5：以读模式重新打开文件
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
    // 步骤4：写入完成后关闭文件
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
    // 步骤3：将数据压缩写入文件
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
    // 步骤1：以写模式打开文件，写入数据后读取并检查文件末尾
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

**功能：** 从文件中读取字节并将其解压缩到buf中，直到读取换行符并将其传输到buf，或遇到文件结束条件。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| buf | ArrayBuffer | 是 | 存储读取的行数据。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<String> | 是 | 回调，返回以null结尾的字符串。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzgetsDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzgets")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzgets/test.gz"
    let bufferWithData = ArrayBuffer(16, repeat: 0)
    // 步骤6：读取结束后关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤5：读取一行内容
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
    // 步骤4：以读模式重新打开文件
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
    // 步骤3：写入完成后关闭文件
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
    // 步骤2：将字符串压缩写入文件
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
    // 步骤1：以写模式打开文件，写入字符串后读取
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

**功能：** 打开位于指定路径的gzip(.gz)文件，用于进行读取并解压缩，或者压缩并写入。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| path | String | 是 | 需要打开的文件路径。路径必须为沙箱路径，沙箱路径可以通过context获取。 |
| mode | String | 是 | 指定文件打开方法。<br>基础模式（必须三选一）：<br>- “r”或“rb”：读取模式，自动检测并解压gzip文件（若非gzip格式则直接读取原始数据）。<br>- “w”或“wb”：写入模式，创建新文件并压缩数据。<br>- “a”或“ab”：追加模式，在现有文件末尾追加新的gzip流（不校验原文件格式）。<br>可选功能参数（可组合使用）：<br>- 压缩级别：0（不压缩）至9（最佳压缩），默认压缩级别为6，需要配合写入模式或者追加模式使用。<br>- 压缩策略：“f”（过滤策略）、“h”（霍夫曼策略）、“R”（游标编码策略）、“F”（固定编码策略），只能选取一种压缩策略。<br>- 透明模式：“T”，写入时不压缩且不生成gzip头（生成普通文件），与压缩策略互斥。<br>- 独占创建：“x”，如果文件存在则打开失败，需要配合写入模式或者追加模式使用。<br>- close-on-exec标志：“e”，设置文件描述符的FD_CLOEXEC属性（依赖系统支持）。<br>模式字符串示例：<br>- “r”：读取模式，读取时以二进制形式读取。<br>- “rb”：读取模式，读取时以二进制形式读取。<br>- “wb6”：写入模式，压缩时以二进制形式写入，压缩级别为6。<br>- “wb9f”：写入模式，压缩时以二进制形式写入，压缩级别为最佳压缩，压缩策略采用过滤策略。<br>- “wbT”：写入模式，不压缩，生成普通文件。<br>- “wbx”：写入模式，压缩时以二进制形式写入，采用独占创建的方式写入文件。<br>- “abx”：追加模式，压缩时以二进制形式追加并写入，采用独占创建的方式写入文件。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | 是 | 回调，无返回结果。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800002 | No such file or access mode error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzopenDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzopen")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzopen/test.gz"
    // 步骤2：关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤1：以写模式打开文件，打开成功后关闭
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

**功能：** 压缩给定的以null结尾的字符串并将其写入文件，不包括终止的null字符。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| str | String | 是 | 要写入的字符串。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32> | 是 | 回调，返回写入的字符数。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzputsDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzputs")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzputs/test.gz"
    // 步骤3：写入完成后关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤2：将字符串压缩写入文件
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
    // 步骤1：以写模式打开文件，写入字符串后关闭
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

**功能：** 从文件中读取未压缩字节并将其解压缩到buf中，读取字节数由buf缓冲区长度决定。使用callback异步回调。注意：此方法只能在gzopen的读模式（“r”或“rb”）下使用。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| buf | ArrayBuffer | 是 | 用于存储读取结果的目标缓冲区。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int64> | 是 | 回调，返回实际读取的未压缩字节数。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzreadDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzread")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzread/test.gz"
    // 填充16字节的待写入数据
    let writeBuffer = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        writeBuffer[i] = UInt8(i)
    }
    let readBuffer = ArrayBuffer(16, repeat: 0)
    // 步骤7：读取结束后关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let finalCloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤6：读取文件内容
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
    // 步骤5：以读模式重新打开文件
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
    // 步骤4：写入完成后关闭文件
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
    // 步骤3：将数据压缩写入文件
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
    // 步骤1：以写模式打开文件，写入数据后读取
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

**功能：** 将buf中len长度的未压缩字节进行压缩并将其写入文件。使用callback异步回调。注意：此方法只能在gzopen的写模式（“w”或“wb”）下使用。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| buf | ArrayBuffer | 是 | 指向要写入数据的缓冲区。 |
| len | Int64 | 是 | 未压缩字节长度，单位：字节。取值范围：[0, min(buf.byteLength, 2147483647))。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int64> | 是 | 回调，返回写入的未压缩字节数。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800009 | Internal structure error. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.CoreFileKit.*
import kit.PerformanceAnalysisKit.Hilog

func gzwriteDemo(gzip: GZip): Unit {
    // 代码中使用的路径需为应用的沙箱路径，如/data/storage/el2/base/temp，也可以通过context获取
    let pathDir = "/data/storage/el2/base/temp"
    // 确保目标目录存在，已存在时可忽略该异常
    try {
        FileIo.mkdir(pathDir + "/gzwrite")
    } catch (e: BusinessException) {
        Hilog.info(0, "test", "directory may already exist")
    }
    let path = pathDir + "/gzwrite/test.gz"
    // 填充16字节的待写入数据
    let bufferWithData = ArrayBuffer(16, repeat: 0)
    for (i in 0..16) {
        bufferWithData[i] = UInt8(i)
    }
    // 步骤3：写入完成后关闭文件，流程结束（实际开发中需在上一回调完成后发起下一步）
    let gzcloseCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "gzclose error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "gzclose success")
        }
    }
    // 步骤2：将数据压缩写入文件
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
    // 步骤1：以写模式打开文件，写入数据后关闭
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

**功能：** 定义用于压缩或解压ZIP文件时使用的选项。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop level

```cangjie
public mut prop level: ?CompressLevel
```

**功能：** 压缩或解压时指定的压缩等级。默认值为CompressLevelDefaultCompression。

**类型：** ?[CompressLevel](#enum-compresslevel)

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop memLevel

```cangjie
public mut prop memLevel: ?MemLevel
```

**功能：** 压缩时指定的使用内存等级。默认值为MemLevelDefault。

**类型：** ?[MemLevel](#enum-memlevel)

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop strategy

```cangjie
public mut prop strategy: ?CompressStrategy
```

**功能：** 压缩时指定的压缩策略。默认值为CompressStrategyDefaultStrategy。

**类型：** ?[CompressStrategy](#enum-compressstrategy)

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### init(?CompressLevel, ?MemLevel, ?CompressStrategy)

```cangjie
public init(
    level!: ?CompressLevel = None,
    memLevel!: ?MemLevel = None,
    strategy!: ?CompressStrategy = None
)
```

**功能：** 创建一个Options对象。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| level | ?[CompressLevel](#enum-compresslevel) | 否 | None | **命名参数。** 压缩或解压时指定的压缩等级。 |
| memLevel | ?[MemLevel](#enum-memlevel) | 否 | None | **命名参数。** 压缩时指定的使用内存等级。 |
| strategy | ?[CompressStrategy](#enum-compressstrategy) | 否 | None | **命名参数。** 压缩时指定的压缩策略。 |

## class Zip

```cangjie
public class Zip
```

**功能：** 压缩解压缩对象实例，提供以zlib、deflate、gzip格式对数据进行压缩与解压的接口。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### func compress(ArrayBuffer, ArrayBuffer, AsyncCallback\<ZipOutputInfo>, ?Int64)

```cangjie
public func compress(dest: ArrayBuffer, source: ArrayBuffer, callback: AsyncCallback<ZipOutputInfo>, sourceLen!: ?Int64 = None): Unit
```

**功能：** 将源缓冲区压缩到目标缓冲区。使用callback异步回调。压缩后的数据可以使用[uncompress](#func-uncompressarraybuffer-arraybuffer-asynccallbackzipoutputinfo-int64)进行解压。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dest | ArrayBuffer | 是 | - | 目标缓冲区。 |
| source | ArrayBuffer | 是 | - | 源数据缓冲区。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ZipOutputInfo](#class-zipoutputinfo)> | 是 | - | 回调，返回结果状态和目标缓冲区的总大小。 |
| sourceLen | ?Int64 | 否 | None | **命名参数。** 源数据长度，单位：字节。取值范围：[0, source.byteLength]。未传入时，默认使用source.byteLength。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充待压缩的数据（UTF-8编码后为31字节）
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

**功能：** 将源缓冲区压缩到目标缓冲区。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dest | ArrayBuffer | 是 | - | 目标缓冲区。 |
| source | ArrayBuffer | 是 | - | 源数据缓冲区。 |
| level | [CompressLevel](#enum-compresslevel) | 是 | - | 压缩等级，参考[CompressLevel枚举定义](#enum-compresslevel)。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ZipOutputInfo](#class-zipoutputinfo)> | 是 | - | 回调，返回结果状态和目标缓冲区的总大小。 |
| sourceLen | ?Int64 | 否 | None | **命名参数。** 源数据长度，单位：字节。取值范围：[0, source.byteLength]。未传入时，默认使用source.byteLength。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充待压缩的数据（UTF-8编码后为31字节）
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

**功能：** 计算返回压缩大小的上限。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| sourceLen | Int32 | 是 | 源数据长度。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32> | 是 | 回调，返回压缩大小的上限。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充12字节数据，源数据长度与数据保持关联
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

**功能：** 压缩数据。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| flush | [CompressFlushMode](#enum-compressflushmode) | 是 | 压缩或解压过程中的数据刷新策略。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func deflateDemo(zip: Zip): Unit {
    // 填充待压缩的12字节数据
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // 步骤3：释放压缩流的动态数据结构（实际开发中需在上一回调完成后发起下一步）
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "deflateEnd success")
        }
    }
    // 步骤2：压缩数据，完成后释放压缩流
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
    // 步骤1：初始化压缩流并压缩数据
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

**功能：** 压缩流的所有动态分配的数据结构都被释放。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func deflateEndDemo(zip: Zip): Unit {
    // 填充待压缩的12字节数据
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // 步骤3：压缩完成后释放压缩流的所有动态分配的数据结构（实际开发中需在上一回调完成后发起下一步）
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "deflateEnd success")
        }
    }
    // 步骤2：压缩数据
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
    // 步骤1：初始化压缩流并压缩数据，压缩完成后释放
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

**功能：** 初始化压缩流并设置压缩级别、压缩方法、窗口大小、内存级别和压缩策略。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| level | [CompressLevel](#enum-compresslevel) | 是 | 压缩等级，参考[CompressLevel枚举定义](#enum-compresslevel)。 |
| method | [CompressMethod](#enum-compressmethod) | 是 | 压缩方法的枚举类型，指定使用DEFLATED压缩方法。 |
| windowBits | Int32 | 是 | 内存窗口大小，根据数据格式限制取值范围。取值如下：zlib格式：[1, 15]；gzip格式：(15, +∞)；raw deflate格式：[-15, -1]。 |
| memLevel | [MemLevel](#enum-memlevel) | 是 | 内存等级，参考[MemLevel枚举定义](#enum-memlevel)。 |
| strategy | [CompressStrategy](#enum-compressstrategy) | 是 | 压缩策略，参考[CompressStrategy枚举定义](#enum-compressstrategy)。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充待压缩的12字节数据
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

**功能：** 获取并返回ZStream流对象实例。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ZStream](#class-zstream)> | 是 | 回调，返回压缩和解压缩数据流管理对象，用于管理压缩和解压缩过程中的数据流。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func getZStreamDemo(zip: Zip): Unit {
    // 填充12字节数据
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let strm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // 步骤2：获取流对象实例（实际开发中需在上一回调完成后发起下一步）
    let getZStreamCallback: AsyncCallback<ZStream> = {
        err: Option<BusinessException>, data: Option<ZStream> => match (err) {
            case Some(e) => Hilog.error(0, "test", "getZStream error: errcode is ${e.code}")
            case _ => match (data) {
                case Some(value) => Hilog.info(0, "test", "getZStream success")
                case _ => Hilog.error(0, "test", "getZStream failed")
            }
        }
    }
    // 步骤1：初始化流后获取流对象实例，需先通过deflateInit2或inflateInit初始化流
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

**功能：** 解压数据。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| flush | [CompressFlushMode](#enum-compressflushmode) | 是 | 压缩或解压过程中的数据刷新策略。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |
  | 17800005 | The input data is incorrect. For example, the data does not conform to the zlib compression format, the compressed data is corrupted, or the data is not compressed. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func inflateDemo(zip: Zip): Unit {
    // 填充待压缩的12字节数据
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    let compressStrm = ZStream(nextIn: arrayBufferIn, availableIn: 12,
        nextOut: arrayBufferOut, availableOut: 100)
    // 解压时输入为压缩后的数据，输出为原始数据
    let decompressStrm = ZStream(nextIn: arrayBufferOut, availableIn: 100,
        nextOut: arrayBufferIn, availableOut: 12)
    // 步骤6：释放解压流的动态数据结构（实际开发中需在上一回调完成后发起下一步）
    let inflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "inflateEnd success")
        }
    }
    // 步骤5：解压数据，完成后释放解压流
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
    // 步骤4：初始化解压流
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
    // 步骤3：释放压缩流
    let deflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "deflateEnd error: errcode is ${e.code}")
            case _ =>
                Hilog.info(0, "test", "deflateEnd success")
                zip.inflateInit(decompressStrm, inflateInitCallback)
        }
    }
    // 步骤2：压缩数据
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
    // 步骤1：初始化压缩流并压缩数据，压缩完成后对压缩数据解压
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

**功能：** 解压流的所有动态分配的数据结构都被释放。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func inflateEndDemo(zip: Zip): Unit {
    // "hello world!"经deflate压缩后的数据（20字节）
    let compressedData: ArrayBuffer = [0x78, 0x9C, 0xCB, 0x48, 0xCD, 0xC9, 0xC9, 0x57, 0x28, 0xCF,
        0x2F, 0xCA, 0x49, 0x51, 0x04, 0x00, 0x1E, 0x89, 0x04, 0x7E]
    // 解压后可还原出原始数据"hello world!"（12字节）
    let decompressedBuffer = ArrayBuffer(12, repeat: 0)
    let strm = ZStream(nextIn: compressedData, availableIn: 20,
        nextOut: decompressedBuffer, availableOut: 12)
    // 步骤3：解压完成后释放解压流的所有动态分配的数据结构（实际开发中需在上一回调完成后发起下一步）
    let inflateEndCallback: AsyncCallback<ReturnStatus> = {
        err: Option<BusinessException>, data: Option<ReturnStatus> => match (err) {
            case Some(e) => Hilog.error(0, "test", "inflateEnd error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "inflateEnd success")
        }
    }
    // 步骤2：解压数据
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
    // 步骤1：初始化解压流并解压数据，解压完成后释放
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

**功能：** 初始化解压缩流。使用callback异步回调。需要先调用此方法初始化解压缩流，然后调用inflate进行解压，最后调用inflateEnd释放资源。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充12字节数据
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

**功能：** 初始化解压缩流并设置指定的windowBits参数。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| strm | [ZStream](#class-zstream) | 是 | zlib压缩解压的数据流管理对象。 |
| windowBits | Int32 | 是 | 内存窗口大小，根据数据格式限制取值范围。取值如下：zlib格式：[1, 15]；gzip格式：(15, +∞)；raw deflate格式：[-15, -1]。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ReturnStatus](#enum-returnstatus)> | 是 | 回调，返回结果状态。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800004 | Compression or decompression stream error, which may be caused by an initialization error in the zlib stream structure or a modified structure. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// 填充12字节数据
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

**功能：** 将压缩后的数据解压缩为原始的未压缩形式。使用callback异步回调。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| dest | ArrayBuffer | 是 | - | 目标缓冲区。 |
| source | ArrayBuffer | 是 | - | 源数据缓冲区。 |
| callback | [AsyncCallback](../../reference/arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[ZipOutputInfo](#class-zipoutputinfo)> | 是 | - | 回调，返回结果状态和目标缓冲区的总大小。 |
| sourceLen | ?Int64 | 否 | None | **命名参数。** 源数据长度，单位：字节。取值范围：[0, source.byteLength]。未传入时，默认使用source.byteLength。 |

**异常：**

- [BusinessException](../../reference/arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../../reference/cj-errorcode-universal.md)和[zlib子系统错误码](./cj-errorcode-zlib.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 17800005 | The input data is incorrect. For example, the data does not conform to the zlib compression format, the compressed data is corrupted, or the data is not compressed. |
  | 17800007 | The input buffer is incorrect, and the output buffer is too small to accommodate the compressed or decompressed data. |

**示例：**

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

func uncompressDemo(zip: Zip): Unit {
    // 填充待压缩的12字节数据
    let arrayBufferIn = "hello world!".toArray()
    let arrayBufferOut = ArrayBuffer(100, repeat: 0)
    // 步骤2：对压缩后的数据解压（实际开发中需在上一回调完成后发起下一步）
    let uncompressCallback: AsyncCallback<ZipOutputInfo> = {
        err: Option<BusinessException>, data: Option<ZipOutputInfo> => match (err) {
            case Some(e) => Hilog.error(0, "test", "uncompress error: errcode is ${e.code}")
            case _ => Hilog.info(0, "test", "uncompress success")
        }
    }
    // 步骤1：压缩数据，压缩完成后在回调中解压
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

**功能：** 压缩和解压缩的返回值信息。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop destLen

```cangjie
public mut prop destLen: Int64
```

**功能：** 目标缓冲区的总长度。

**类型：** Int64

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop status

```cangjie
public mut prop status: ReturnStatus
```

**功能：** 压缩或解压函数执行结果的状态，包含成功状态和各种错误状态。详见[ReturnStatus](#enum-returnstatus)。

**类型：** [ReturnStatus](#enum-returnstatus)

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## class ZStream

```cangjie
public class ZStream
```

**功能：** 处理压缩和解压缩所需的全部信息。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop adler

```cangjie
public mut prop adler: ?UInt64
```

**功能：** 未压缩数据的Adler-32或CRC-32值。

**类型：** ?UInt64

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop availableIn

```cangjie
public mut prop availableIn: ?UInt32
```

**功能：** nextIn可用的字节数。

**类型：** ?UInt32

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop availableOut

```cangjie
public mut prop availableOut: ?UInt32
```

**功能：** nextOut的剩余可用字节数。

**类型：** ?UInt32

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop dataType

```cangjie
public mut prop dataType: ?Int32
```

**功能：** 关于数据类型的最佳猜测：deflate的二进制或文本，或inflate的解码状态。

**类型：** ?Int32

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop nextIn

```cangjie
public mut prop nextIn: ?ArrayBuffer
```

**功能：** 需要压缩的输入字节。

**类型：** ?ArrayBuffer

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop nextOut

```cangjie
public mut prop nextOut: ?ArrayBuffer
```

**功能：** 压缩后的输出字节。

**类型：** ?ArrayBuffer

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop totalIn

```cangjie
public mut prop totalIn: ?UInt64
```

**功能：** 到目前为止读取的输入字节总数。

**类型：** ?UInt64

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### prop totalOut

```cangjie
public mut prop totalOut: ?UInt64
```

**功能：** 到目前为止输出的字节总数。

**类型：** ?UInt64

**读写能力：** 可读可写

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

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

**功能：** 创建一个ZStream对象。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| nextIn | ?ArrayBuffer | 否 | None | **命名参数。** 需要压缩的输入字节。 |
| availableIn | ?UInt32 | 否 | None | **命名参数。** nextIn可用的字节数。 |
| totalIn | ?UInt64 | 否 | None | **命名参数。** 到目前为止读取的输入字节总数。 |
| nextOut | ?ArrayBuffer | 否 | None | **命名参数。** 压缩后的输出字节。 |
| availableOut | ?UInt32 | 否 | None | **命名参数。** nextOut的剩余可用字节数。 |
| totalOut | ?UInt64 | 否 | None | **命名参数。** 到目前为止输出的字节总数。 |
| dataType | ?Int32 | 否 | None | **命名参数。** 关于数据类型的最佳猜测：deflate的二进制或文本，或inflate的解码状态。 |
| adler | ?UInt64 | 否 | None | **命名参数。** 未压缩数据的Adler-32或CRC-32值。 |

## enum CompressFlushMode

```cangjie
public enum CompressFlushMode
```

**功能：** 表示压缩或解压过程中数据刷新模式的枚举。

**扩展：**

- [extend CompressFlushMode <: ToString](#extend-compressflushmode-tostring)
- [extend CompressFlushMode <: Equatable\<CompressFlushMode>](#extend-compressflushmode-equatablecompressflushmode)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Block

```cangjie
Block
```

**功能：** 允许更精确的控制。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Finish

```cangjie
Finish
```

**功能：** 结束压缩或解压缩过程。适用于压缩流程的最后一步，确保所有数据被完整输出。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### FullFlush

```cangjie
FullFlush
```

**功能：** 重置压缩状态。适用于需要完全重置压缩流的场景，如压缩多个独立数据块。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### NoFlush

```cangjie
NoFlush
```

**功能：** 默认值，表示正常操作。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### PartialFlush

```cangjie
PartialFlush
```

**功能：** 在流中生成部分刷新点。适用于需要同步点以便解压流能够恢复的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### SyncFlush

```cangjie
SyncFlush
```

**功能：** 在保持压缩流状态的同时强制输出所有压缩数据。适用于需要实时输出压缩数据的场景，如网络传输。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Trees

```cangjie
Trees
```

**功能：** 实施过程中有特殊目的。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## enum CompressLevel

```cangjie
public enum CompressLevel
```

**功能：** 表示压缩等级的枚举。

**扩展：**

- [extend CompressLevel <: ToString](#extend-compresslevel-tostring)
- [extend CompressLevel <: Equatable\<CompressLevel>](#extend-compresslevel-equatablecompresslevel)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressLevelBestCompression

```cangjie
CompressLevelBestCompression
```

**功能：** 以最高压缩率完成压缩的压缩等级，压缩速度较慢。适合对存储空间敏感的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressLevelBestSpeed

```cangjie
CompressLevelBestSpeed
```

**功能：** 以最快速度完成压缩的压缩等级，压缩率较低。适合对实时性要求高的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressLevelDefaultCompression

```cangjie
CompressLevelDefaultCompression
```

**功能：** 默认压缩等级，在压缩速度和压缩率之间取得平衡。适合大多数场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressLevelNoCompression

```cangjie
CompressLevelNoCompression
```

**功能：** 压缩率为0的压缩等级。适用于不压缩数据的场景，如已压缩的图片或视频文件。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## enum CompressMethod

```cangjie
public enum CompressMethod
```

**功能：** 表示压缩方法的枚举。deflate压缩方法，当前版本仅支持该方法。

**扩展：**

- [extend CompressMethod <: ToString](#extend-compressmethod-tostring)
- [extend CompressMethod <: Equatable\<CompressMethod>](#extend-compressmethod-equatablecompressmethod)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Deflated

```cangjie
Deflated
```

**功能：** 使用DEFLATE算法进行压缩，是zlib库的标准压缩方法。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## enum CompressStrategy

```cangjie
public enum CompressStrategy
```

**功能：** 表示压缩策略的枚举。

**扩展：**

- [extend CompressStrategy <: ToString](#extend-compressstrategy-tostring)
- [extend CompressStrategy <: Equatable\<CompressStrategy>](#extend-compressstrategy-equatablecompressstrategy)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressStrategyDefaultStrategy

```cangjie
CompressStrategyDefaultStrategy
```

**功能：** 常规数据压缩策略，适用于大多数数据类型，提供平衡的压缩性能。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressStrategyFiltered

```cangjie
CompressStrategyFiltered
```

**功能：** 过滤器产生的数据压缩策略。适用于经过预处理或过滤的数据，如delta编码后的数据。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressStrategyFixed

```cangjie
CompressStrategyFixed
```

**功能：** 固定压缩策略。使用固定的霍夫曼编码，适用于需要固定编码输出的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressStrategyHuffmanOnly

```cangjie
CompressStrategyHuffmanOnly
```

**功能：** 霍夫曼编码压缩策略。仅使用霍夫曼编码、不进行字符串匹配，适用于需要快速压缩的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### CompressStrategyRle

```cangjie
CompressStrategyRle
```

**功能：** 游标编码压缩策略。适用于包含大量重复字节的数据，如位图图像。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## enum MemLevel

```cangjie
public enum MemLevel
```

**功能：** 表示压缩时使用的内存等级的枚举。

**扩展：**

- [extend MemLevel <: ToString](#extend-memlevel-tostring)
- [extend MemLevel <: Equatable\<MemLevel>](#extend-memlevel-equatablememlevel)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### MemLevelDefault

```cangjie
MemLevelDefault
```

**功能：** 默认内存等级，在压缩速度和内存占用之间取得平衡。适合大多数场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### MemLevelMax

```cangjie
MemLevelMax
```

**功能：** 压缩时使用的最大内存等级，压缩速度最快但内存占用最高。适合内存充足的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### MemLevelMin

```cangjie
MemLevelMin
```

**功能：** 压缩时使用的最小内存等级，压缩速度最慢但内存占用最低。适合内存受限的场景。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## enum ReturnStatus

```cangjie
public enum ReturnStatus
```

**功能：** 表示压缩和解压缩函数返回状态的枚举，包含成功状态和各种错误状态。

**扩展：**

- [extend ReturnStatus <: ToString](#extend-returnstatus-tostring)
- [extend ReturnStatus <: Equatable\<ReturnStatus>](#extend-returnstatus-equatablereturnstatus)

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### BufError

```cangjie
BufError
```

**功能：** 函数调用失败，表示输入缓冲区不正确。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### DataError

```cangjie
DataError
```

**功能：** 函数调用失败，表示输入数据不正确。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Errno

```cangjie
Errno
```

**功能：** 函数调用失败，表示文件操作错误。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### MemError

```cangjie
MemError
```

**功能：** 函数调用失败，表示内存分配失败。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### NeedDict

```cangjie
NeedDict
```

**功能：** 函数调用成功，表示需要预设字典才能继续解压缩。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### Ok

```cangjie
Ok
```

**功能：** 函数调用成功。该枚举值支持在原子化服务中使用。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### StreamEnd

```cangjie
StreamEnd
```

**功能：** 函数调用成功，表示已处理了整个数据。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

### StreamError

```cangjie
StreamError
```

**功能：** 函数调用失败，表示压缩或解压缩流错误。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

## extend CompressFlushMode <: Equatable\<CompressFlushMode>

```cangjie
extend CompressFlushMode <: Equatable<CompressFlushMode>
```

**功能：** 为 CompressFlushMode 类型扩展 Equatable\<CompressFlushMode> 接口，支持相等比较。

**被扩展类型：**

- [CompressFlushMode](#enum-compressflushmode)

**扩展接口：**

- Equatable\<[CompressFlushMode](#enum-compressflushmode)>

### func ==(CompressFlushMode)

```cangjie
public operator func ==(other: CompressFlushMode): Bool
```

**功能：** 对数据刷新模式进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressFlushMode](#enum-compressflushmode) | 是 | 数据刷新模式。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果数据刷新模式相同返回true，否则返回false。|

### func !=(CompressFlushMode)

```cangjie
public operator func !=(other: CompressFlushMode): Bool
```

**功能：** 对数据刷新模式进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressFlushMode](#enum-compressflushmode) | 是 | 数据刷新模式。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果数据刷新模式不同返回true，否则返回false。|

## extend CompressFlushMode <: ToString

```cangjie
extend CompressFlushMode <: ToString
```

**功能：** 为 CompressFlushMode 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [CompressFlushMode](#enum-compressflushmode)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回数据刷新模式的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 数据刷新模式值对应的字符串。|

## extend CompressLevel <: Equatable\<CompressLevel>

```cangjie
extend CompressLevel <: Equatable<CompressLevel>
```

**功能：** 为 CompressLevel 类型扩展 Equatable\<CompressLevel> 接口，支持相等比较。

**被扩展类型：**

- [CompressLevel](#enum-compresslevel)

**扩展接口：**

- Equatable\<[CompressLevel](#enum-compresslevel)>

### func ==(CompressLevel)

```cangjie
public operator func ==(other: CompressLevel): Bool
```

**功能：** 对压缩等级进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressLevel](#enum-compresslevel) | 是 | 压缩等级。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩等级相同返回true，否则返回false。|

### func !=(CompressLevel)

```cangjie
public operator func !=(other: CompressLevel): Bool
```

**功能：** 对压缩等级进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressLevel](#enum-compresslevel) | 是 | 压缩等级。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩等级不同返回true，否则返回false。|

## extend CompressLevel <: ToString

```cangjie
extend CompressLevel <: ToString
```

**功能：** 为 CompressLevel 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [CompressLevel](#enum-compresslevel)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回压缩等级的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 压缩等级值对应的字符串。|

## extend CompressMethod <: Equatable\<CompressMethod>

```cangjie
extend CompressMethod <: Equatable<CompressMethod>
```

**功能：** 为 CompressMethod 类型扩展 Equatable\<CompressMethod> 接口，支持相等比较。

**被扩展类型：**

- [CompressMethod](#enum-compressmethod)

**扩展接口：**

- Equatable\<[CompressMethod](#enum-compressmethod)>

### func ==(CompressMethod)

```cangjie
public operator func ==(other: CompressMethod): Bool
```

**功能：** 对压缩方法进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressMethod](#enum-compressmethod) | 是 | 压缩方法。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩方法相同返回true，否则返回false。|

### func !=(CompressMethod)

```cangjie
public operator func !=(other: CompressMethod): Bool
```

**功能：** 对压缩方法进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressMethod](#enum-compressmethod) | 是 | 压缩方法。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩方法不同返回true，否则返回false。|

## extend CompressMethod <: ToString

```cangjie
extend CompressMethod <: ToString
```

**功能：** 为 CompressMethod 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [CompressMethod](#enum-compressmethod)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回压缩方法的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 压缩方法值对应的字符串。|

## extend CompressStrategy <: Equatable\<CompressStrategy>

```cangjie
extend CompressStrategy <: Equatable<CompressStrategy>
```

**功能：** 为 CompressStrategy 类型扩展 Equatable\<CompressStrategy> 接口，支持相等比较。

**被扩展类型：**

- [CompressStrategy](#enum-compressstrategy)

**扩展接口：**

- Equatable\<[CompressStrategy](#enum-compressstrategy)>

### func ==(CompressStrategy)

```cangjie
public operator func ==(other: CompressStrategy): Bool
```

**功能：** 对压缩策略进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressStrategy](#enum-compressstrategy) | 是 | 压缩策略。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩策略相同返回true，否则返回false。|

### func !=(CompressStrategy)

```cangjie
public operator func !=(other: CompressStrategy): Bool
```

**功能：** 对压缩策略进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CompressStrategy](#enum-compressstrategy) | 是 | 压缩策略。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果压缩策略不同返回true，否则返回false。|

## extend CompressStrategy <: ToString

```cangjie
extend CompressStrategy <: ToString
```

**功能：** 为 CompressStrategy 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [CompressStrategy](#enum-compressstrategy)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回压缩策略的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 压缩策略值对应的字符串。|

## extend MemLevel <: Equatable\<MemLevel>

```cangjie
extend MemLevel <: Equatable<MemLevel>
```

**功能：** 为 MemLevel 类型扩展 Equatable\<MemLevel> 接口，支持相等比较。

**被扩展类型：**

- [MemLevel](#enum-memlevel)

**扩展接口：**

- Equatable\<[MemLevel](#enum-memlevel)>

### func ==(MemLevel)

```cangjie
public operator func ==(other: MemLevel): Bool
```

**功能：** 对内存等级进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [MemLevel](#enum-memlevel) | 是 | 内存等级。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果内存等级相同返回true，否则返回false。|

### func !=(MemLevel)

```cangjie
public operator func !=(other: MemLevel): Bool
```

**功能：** 对内存等级进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [MemLevel](#enum-memlevel) | 是 | 内存等级。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果内存等级不同返回true，否则返回false。|

## extend MemLevel <: ToString

```cangjie
extend MemLevel <: ToString
```

**功能：** 为 MemLevel 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [MemLevel](#enum-memlevel)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回内存等级的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 内存等级值对应的字符串。|

## extend ReturnStatus <: Equatable\<ReturnStatus>

```cangjie
extend ReturnStatus <: Equatable<ReturnStatus>
```

**功能：** 为 ReturnStatus 类型扩展 Equatable\<ReturnStatus> 接口，支持相等比较。

**被扩展类型：**

- [ReturnStatus](#enum-returnstatus)

**扩展接口：**

- Equatable\<[ReturnStatus](#enum-returnstatus)>

### func ==(ReturnStatus)

```cangjie
public operator func ==(other: ReturnStatus): Bool
```

**功能：** 对结果状态进行判等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [ReturnStatus](#enum-returnstatus) | 是 | 结果状态。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果结果状态相同返回true，否则返回false。|

### func !=(ReturnStatus)

```cangjie
public operator func !=(other: ReturnStatus): Bool
```

**功能：** 对结果状态进行判不等。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [ReturnStatus](#enum-returnstatus) | 是 | 结果状态。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果结果状态不同返回true，否则返回false。|

## extend ReturnStatus <: ToString

```cangjie
extend ReturnStatus <: ToString
```

**功能：** 为 ReturnStatus 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [ReturnStatus](#enum-returnstatus)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回结果状态的字符串表示。

**系统能力：** SystemCapability.BundleManager.Zlib

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 结果状态值对应的字符串。|
