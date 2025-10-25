# FileUri开发指导

## 简介

FileUri模块提供统一资源标志符（Uniform Resource Identifier，URI）与文件路径之间的相互转换功能。通过该模块，开发者可以将文件路径转换为URI，或将URI转换为文件路径，便于在文件分享等场景中使用。

## 场景介绍

主要场景有：

- 将文件路径转换为URI，用于文件分享等操作。
- 通过URI获取对应的文件路径，用于文件操作。
- 获取URI对应的文件名和目录信息。

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[FileUri 接口](../../application-dev/reference/CoreFileKit/cj-apis-file_fileuri.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| getUriFromPath(path: String) | 静态方法，通过传入的路径生成对应的文件URI |
| FileUri(uriOrPath: String) | 构造函数，通过URI或路径创建FileUri实例 |
| FileUri.path | 获取FileUri对应的路径名 |
| FileUri.name | 获取FileUri对应的文件名 |
| FileUri.toString() | 返回字符串类型的URI |

## 开发示例

在进行文件URI操作前，开发者需要获取文件路径。以从AbilityContext获取应用文件路径为例进行说明。

下面介绍几种常用操作示例。

### 将文件路径转换为URI

以下示例代码演示了如何将文件路径转换为URI。

<!-- compile -->

```cangjie
// index.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// 见获取UIAbility的上下文信息章节
let context = getContext()
// 获取应用文件路径
let filesDir = context.filesDirectory

func pathToUriExample(): Unit {
    // 创建一个测试文件路径
    let filePath = filesDir + "/test.txt"
    
    // 方法1: 使用静态方法getUriFromPath
    let uri1 = FileUri.getUriFromPath(filePath)
    AppLog.info("URI from static method: ${uri1}")
    
    // 方法2: 使用FileUri构造函数然后调用toString()
    let fileUri = FileUri(filePath)
    let uri2 = fileUri.toString()
    AppLog.info("URI from FileUri.toString(): ${uri2}")
    
    // 获取文件名
    let fileName = fileUri.name
    AppLog.info("File name: ${fileName}")
    
    // 获取路径
    let path = fileUri.path
    AppLog.info("Path: ${path}")
}
```

### 通过URI获取文件路径和信息

以下示例代码演示了如何通过URI获取文件路径和相关信息。

<!-- compile -->

```cangjie
// index.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// 见获取UIAbility的上下文信息章节
let context = getContext()
// 获取应用文件路径
let filesDir = context.filesDirectory

func uriToPathExample(): Unit {
    // 假设我们有一个URI
    let filePath = filesDir + "/example.txt"
    let uri = FileUri.getUriFromPath(filePath)
    AppLog.info("Original URI: ${uri}")
    
    // 通过URI创建FileUri实例
    let fileUri = FileUri(uri)
    
    // 获取文件路径
    let path = fileUri.path
    AppLog.info("Path from URI: ${path}")
    
    // 获取文件名
    let fileName = fileUri.name
    AppLog.info("File name from URI: ${fileName}")
    
    // 验证转换是否正确
    if (path == filePath) {
        AppLog.info("Path conversion is correct")
    } else {
        AppLog.warn("Path conversion may have issues")
    }
}
```

### 在文件操作中使用FileUri

以下示例代码演示了如何在文件操作中结合使用FileUri。

<!-- compile -->

```cangjie
// index.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// 见获取UIAbility的上下文信息章节
let context = getContext()
// 获取应用文件路径
let filesDir = context.filesDirectory

func fileOperationWithUriExample(): Unit {
    // 创建一个测试文件
    let filePath = filesDir + "/uri_test.txt"
    
    // 创建文件并写入内容
    let file = FileFs.open(filePath, mode: OpenMode.READ_WRITE.mode | OpenMode.CREATE.mode)
    let content = "This is a test file for FileUri operations."
    let writeLen = FileFs.write(file.fd, content)
    AppLog.info("Written ${writeLen} bytes to file")
    FileFs.close(file)
    
    // 将文件路径转换为URI
    let fileUri = FileUri(filePath)
    let uri = fileUri.toString()
    AppLog.info("File URI: ${uri}")
    
    // 通过URI获取文件名
    let fileName = fileUri.name
    AppLog.info("File name: ${fileName}")
    
    // 重新通过URI获取路径并读取文件
    let recoveredPath = fileUri.path
    let readFile = FileFs.open(recoveredPath, mode: OpenMode.READ_ONLY.mode)
    let buf = Array<Byte>(1024, repeat: 0)
    let readOptions = ReadOptions(
        offset: 0,
        length: UIntNative(1024)
    )
    let readLen = FileFs.read(readFile.fd, buf, options: readOptions)
    let readContent = String.fromUtf8(buf[..readLen])
    AppLog.info("Read content: ${readContent}")
    FileFs.close(readFile)
}
```

### 处理特殊字符路径

以下示例代码演示了如何处理包含中文或特殊字符的路径。

<!-- compile -->

```cangjie
// index.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// 见获取UIAbility的上下文信息章节
let context = getContext()
// 获取应用文件路径
let filesDir = context.filesDirectory

func specialCharacterPathExample(): Unit {
    // 创建包含中文和特殊字符的文件路径
    let specialFilePath = filesDir + "/测试文件@#$%.txt"
    AppLog.info("Original path: ${specialFilePath}")
    
    // 将路径转换为URI，特殊字符会被编码
    let uri = FileUri.getUriFromPath(specialFilePath)
    AppLog.info("Encoded URI: ${uri}")
    
    // 通过URI恢复路径
    let fileUri = FileUri(uri)
    let recoveredPath = fileUri.path
    AppLog.info("Recovered path: ${recoveredPath}")
    
    // 验证路径是否一致
    if (specialFilePath == recoveredPath) {
        AppLog.info("Special character path conversion is correct")
    } else {
        AppLog.warn("Special character path conversion may have issues")
    }
    
    // 获取文件名
    let fileName = fileUri.name
    AppLog.info("File name: ${fileName}")
}
```

## 相关信息

- FileUri支持的URI类型：
  - 应用沙箱URI：file://\<bundleName>/\<sandboxPath>
  - 公共目录文件类URI：file://docs/storage/Users/currentUser/\<publicPath>
  - 公共目录媒体类URI：file://media/\<mediaType>/IMG_DATATIME_ID/\<displayName>