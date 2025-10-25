# ohos.file.fileuri

该模块提供通过PATH获取文件统一资源标志符（Uniform Resource Identifier，URI），后续可通过使用[ohos.file_fs（文件管理）](cj-apis-file_fs.md)进行相关open、read、write等操作，实现文件分享。

## 导入模块

```cangjie
import kit.CoreFileKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## static func getUriFromPath(String)

```cangjie
public static func getUriFromPath(path: String): String
```

**功能：** 通过传入的路径path生成应用自己的uri(不支持媒体类型uri的获取)。将path转uri时，路径中的中文及非数字字母的特殊字符将会被编译成对应的ASCII码，拼接在uri中。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|path|String|是|-|文件的沙箱路径。|

**返回值：**

|类型|说明|
|:----|:----|
|String|返回文件URI。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | The input parameter is invalid.|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CoreFileKit.*

let uri = getUriFromPath("test.txt")
```

## class FileUri

```cangjie
public class FileUri <: Uri {
    public init(uriOrPath: String)
}
```

**功能：** 提供在分享过程中将uri转分享路径path、应用自己的沙箱路径在分享时生成对应应用自己的uri、获取uri所在目录路径的uri等接口能力，方便应用对文件分享业务中uri的访问。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**父类型：**

- [Uri](#class-uri)

### prop name

```cangjie
public prop name: String
```

**功能：** 获取FileUri对应文件名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

### prop path

```cangjie
public override prop path: String
```

**功能：** 获取FileUri对应路径名。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

### init(String)

```cangjie

public init(uriOrPath: String)
```

**功能：** FileUri的构造函数。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|uriOrPath|String|是|-|URI或路径。URI类型：<br/>-&nbsp; 应用沙箱URI：file://\<bundleName>/\<sandboxPath> <br/>-&nbsp; 公共目录文件类URI：file://docs/storage/Users/currentUser/\<publicPath> <br/>-&nbsp; 公共目录媒体类URI：file://media/\<mediaType>/IMG_DATATIME_ID/\<displayName>|

**异常：**

- BusinessException：对应错误码如下表，详见[文件管理错误码](./cj-errorcode-filemanagement.md)。

  | 错误码ID | 错误信息 |
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

**功能：** 返回字符串类型URI。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|返回字符串类型URI。|

## class Uri

```cangjie
public open class Uri <: ToString {
}
```

**功能：** 提供在分享过程中将uri转分享路径path、应用自己的沙箱路径在分享时生成对应应用自己的uri、获取uri所在目录路径的uri等接口能力，方便应用对文件分享业务中uri的访问。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**父类型：**

- ToString

### prop path

```cangjie
public override prop path: String
```

**功能：** 获取Uri对应路径名。提供给子类，不建议用户直接使用，否则会抛出异常。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The prop is not supported. | 直接使用。 | 使用子类的函数。 |

### func toString()

```cangjie
public open func toString(): String
```

**功能：** 返回字符串类型URI。提供给子类，不建议用户直接使用，否则会抛出异常。

**系统能力：** SystemCapability.FileManagement.AppFileService

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|返回字符串类型URI。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The function is not supported. | 直接使用。 | 使用子类的函数。 |
