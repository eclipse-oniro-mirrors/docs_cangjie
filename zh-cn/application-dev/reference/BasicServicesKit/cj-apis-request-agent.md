# ohos.request

request部件主要给应用提供上传下载文件、后台传输代理的基础能力。

## 导入模块

```cangjie
import kit.BasicServicesKit.*
```

## 权限列表

ohos.permission.INTERNET

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func create(UIAbilityContext, Config)

```cangjie

public func create(context: UIAbilityContext, config: Config): Task
```

**功能：** 创建要上传或下载的任务，并将其排入队列。每个应用最多支持创建10个未完成的任务。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名  | 类型                                                                                       | 必填 | 默认值 | 说明                       |
| :------ | :----------------------------------------------------------------------------------------- | :--- | :----- | :------------------------- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | 是   | -      | 基于应用程序的上下文。     |
| config  | [Config](#class-config)                                                                    | 是   | -      | <上传/下载任务的配置信息。 |

**返回值：**


| 类型                | 说明                                               |
| :------------------ | :------------------------------------------------- |
| [Task](#class-task) | 返回一个Task对象，里面包括任务id和任务的配置信息。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)与[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息                                                                                                                          |
  | :------- | :-------------------------------------------------------------------------------------------------------------------------------- |
  | 201      | Permission denied.                                                                                                                |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. 3. Parameter verification failed. |
  | 13400001 | Invalid file or file system error.                                                                                                |
  | 13400003 | Task service ability error.                                                                                                       |
  | 21900004 | the application task queue is full.                                                                                               |
  | 21900005 | Operation with wrong task mode.                                                                                                   |
- IllegalArgumentException：

  | 错误信息                | 可能原因 | 处理步骤 |
  | :---------------------- | :------- | :------- |
  | The context is invalid. | todo     | todo     |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleCreate(): Unit {
    try {
        let context = Global.abilityContext
        let config = Config(
            action = Action.Download,
            url = "https://example.com/file.txt"
        )
        let task = create(context, config)
        Hilog.info(0, "cangjie_ohos_test", "成功创建任务，任务ID: ${task.tid}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "创建任务失败: ${e.toString()}")
    }
}
```

## func getTask(UIAbilityContext, String, ?String)

```cangjie

public func getTask(context: UIAbilityContext, id: String, token!: ?String = None): Task
```

**功能：** 根据任务id查询任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名  | 类型                                                                                       | 必填 | 默认值 | 说明                           |
| :------ | :----------------------------------------------------------------------------------------- | :--- | :----- | :----------------------------- |
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | 是   | -      | 基于应用程序的上下文。         |
| id      | String                                                                                     | 是   | -      | 任务id。                       |
| token   | ?String                                                                                    | 否   | None   | **命名参数。** 任务查询token。 |

**返回值：**


| 类型                | 说明                                               |
| :------------------ | :------------------------------------------------- |
| [Task](#class-task) | 返回一个Task对象，里面包括任务id和任务的配置信息。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)与[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息                                                                                                                          |
  | :------- | :-------------------------------------------------------------------------------------------------------------------------------- |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. 3. Parameter verification failed. |
  | 13400003 | Task service ability error.                                                                                                       |
  | 21900006 | Task removed or not found.                                                                                                        |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleGetTask(): Unit {
    try {
        let context = Global.abilityContext
        let taskId = "example_task_id"
        let task = getTask(context, taskId)
        Hilog.info(0, "cangjie_ohos_test", "成功获取任务，任务ID: ${task.tid}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "获取任务失败: ${e.toString()}")
    }
}
```

- IllegalArgumentException：

  | 错误信息                | 可能原因 | 处理步骤 |
  | :---------------------- | :------- | :------- |
  | The context is invalid. | todo     | todo     |

## func remove(String)

```cangjie

public func remove(id: String): Unit
```

**功能：**  移除属于调用方的指定任务。如果正在处理中，该任务将被迫停止。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型   | 必填 | 默认值 | 说明     |
| :----- | :----- | :--- | :----- | :------- |
| id     | String | 是   | -      | 任务id。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                                                                                        |
  | :------- | :---------------------------------------------------------------------------------------------- |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error.                                                                     |
  | 21900006 | Task removed or not found.                                                                      |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleRemove(): Unit {
    try {
        let taskId = "example_task_id"
        remove(taskId)
        Hilog.info(0, "cangjie_ohos_test", "成功移除任务，任务ID: ${taskId}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "移除任务失败: ${e.toString()}")
    }
}
```

## func search(Filter)

```cangjie

public func search(filter!: Filter = Filter()): Array<String>
```

**功能：** 根据默认[Filter](#class-filter)过滤条件查找任务id。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型                    | 必填 | 默认值   | 说明       |
| :----- | :---------------------- | :--- | :------- | :--------- |
| filter | [Filter](#class-filter) | 否   | Filter() | 过滤条件。 |

**返回值：**


| 类型           | 说明                 |
| :------------- | :------------------- |
| Array\<String> | 返回满足条件任务id。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)与[通用错误码说明文档](../cj-errorcode-universal.md)

  | 错误码ID | 错误信息                                                                                        |
  | :------- | :---------------------------------------------------------------------------------------------- |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error.                                                                     |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleSearch(): Unit {
    try {
        let filter = Filter()
        let taskIds = search(filter)
        Hilog.info(0, "cangjie_ohos_test", "搜索到任务数量: ${taskIds.length}")
        for (id in taskIds) {
            Hilog.info(0, "cangjie_ohos_test", "任务ID: ${id}")
        }
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "搜索任务失败: ${e.toString()}")
    }
}
```

## func show(String)

```cangjie

public func show(id: String): TaskInfo
```

**功能：** 根据任务id查询任务的详细信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型   | 必填 | 默认值 | 说明     |
| :----- | :----- | :--- | :----- | :------- |
| id     | String | 是   | -      | 任务id。 |

**返回值：**


| 类型                        | 说明                             |
| :-------------------------- | :------------------------------- |
| [TaskInfo](#class-taskinfo) | 返回任务详细信息的TaskInfo对象。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)与[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息                                                                                        |
  | :------- | :---------------------------------------------------------------------------------------------- |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error.                                                                     |
  | 21900006 | Task removed or not found.                                                                      |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleShow(): Unit {
    try {
        let taskId = "example_task_id"
        let taskInfo = show(taskId)
        Hilog.info(0, "cangjie_ohos_test", "任务信息: ${taskInfo.toString()}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "查询任务信息失败: ${e.toString()}")
    }
}
```

## func touch(String, String)

```cangjie

public func touch(id: String, token: String): TaskInfo
```

**功能：** 根据任务id和token查询任务的详细信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型   | 必填 | 默认值 | 说明            |
| :----- | :----- | :--- | :----- | :-------------- |
| id     | String | 是   | -      | 任务id。        |
| token  | String | 是   | -      | 任务查询token。 |

**返回值：**


| 类型                        | 说明                             |
| :-------------------------- | :------------------------------- |
| [TaskInfo](#class-taskinfo) | 返回任务详细信息的TaskInfo对象。 |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)与[通用错误码说明文档](../cj-errorcode-universal.md)

  | 错误码ID | 错误信息                                                                                        |
  | :------- | :---------------------------------------------------------------------------------------------- |
  | 401      | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error.                                                                     |
  | 21900006 | Task removed or not found.                                                                      |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleTouch(): Unit {
    try {
        let taskId = "example_task_id"
        let token = "example_token"
        let taskInfo = touch(taskId, token)
        Hilog.info(0, "cangjie_ohos_test", "任务信息: ${taskInfo.toString()}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "查询任务信息失败: ${e.toString()}")
    }
}
```

## class Config

```cangjie
public class Config {
    public var action: Action
    public var url: String
    public var title:?String
    public var description: String
    public var mode: Mode
    public var overwrite: Bool
    public var method:?String
    public var headers: HashMap<String, String>
    public var data:?ConfigData
    public var saveas:String
    public var network: Network
    public var metered: Bool
    public var roaming: Bool
    public var retry: Bool
    public var redirect: Bool
    public var index: UInt32
    public var begins: Int64
    public var ends: Int64
    public var gauge: Bool
    public var precise: Bool
    public var token: ?String
    public var priority: UInt32
    public var extras: HashMap<String, String>

    public init(action: Action, url: String, title!: ?String = None, description!: String = "",
        mode!: Mode = Mode.Background, overwrite!: Bool = false, method!: ?String = None,
        headers!: HashMap<String, String> = HashMap<String, String>(), data!: ?ConfigData = None, saveas!: ?String = None,
        network!: Network = Network.AnyType, metered!: Bool = false, roaming!: Bool = true, retry!: Bool = true,
        redirect!: Bool = true, index!: UInt32 = 0, begins!: Int64 = 0, ends!: Int64 = -1, gauge!: Bool = false,
        precise!: Bool = false, token!: String = "", priority!: UInt32 = 0,extras!: HashMap<String, String> = HashMap<String, String>()
    )
}
```

**功能：** 上传/下载任务的配置信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var action

```cangjie
public var action: Action
```

**功能：** 任务操作选项，UPLOAD表示上传任务，DOWNLOAD表示下载任务。

**类型：** [Action](#enum-action)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var begins

```cangjie
public var begins: Int64
```

**功能：** 文件起点，通常用于断点续传。默认值为0，取值为闭区间。下载时，请求读取服务器开始下载文件时的起点位置（http协议中设置"Range"选项）。上传时，在上传开始时读取。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var data

```cangjie
public var data:?ConfigData
```

**功能：** 下载时，data为字符串类型，通常使用json(object将被转换为json文本)，默认为空。上传时，data是表单项数组Array\<FormItem>，默认为空。

**类型：** ?[ConfigData](#enum-configdata)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var description

```cangjie
public var description: String
```

**功能：** 任务的详细信息，其最大长度为1024个字符，默认值为空字符串。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var ends

```cangjie
public var ends: Int64
```

**功能：** 文件终点，通常用于断点续传。默认值为-1，取值为闭区间。下载时，请求读取服务器开始下载文件时的结束位置（http协议中设置"Range"选项）。上传时，在上传时结束读取。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**功能：** 配置的附加功能，默认为空。

**类型：** HashMap\<String,String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var gauge

```cangjie
public var gauge: Bool
```

**功能：** 后台任务的过程进度通知策略，仅应用于后台任务，默认值为false。false：代表仅完成或失败的通知。true：发出每个进度已完成或失败的通知。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var headers

```cangjie
public var headers: HashMap<String, String>
```

**功能：** 添加要包含在任务中的HTTP协议标志头。对于上传请求，默认的Content-Type为"multipart/form-data"。对于下载请求，默认的Content-Type为"application/json"。

**类型：** HashMap

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var index

```cangjie
public var index: UInt32
```

**功能：** 任务的路径索引，通常用于任务断点续传，默认为0。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var metered

```cangjie
public var metered: Bool
```

**功能：** 是否允许在按流量计费的网络中工作，默认为false。true：是。false：否。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var method

```cangjie
public var method:?String
```

**功能：** 上传或下载的HTTP标准方法，包括GET、POST和PUT，不区分大小写。上传时，使用PUT或POST，默认值为PUT。下载时，使用GET或POST，默认值为GET。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var mode

```cangjie
public var mode: Mode
```

**功能：** 任务模式, 默认为后台任务。

**类型：** [Mode](#enum-mode)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var network

```cangjie
public var network: Network
```

**功能：** 网络选项，当前支持无线网络WIFI和蜂窝数据网络CELLULAR，默认为ANY（WIFI或CELLULAR）。

**类型：** [Network](#enum-network)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var overwrite

```cangjie
public var overwrite: Bool
```

**功能：** 下载过程中路径已存在时的解决方案选择，默认为false。true：覆盖已存在的文件。false：下载失败。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var precise

```cangjie
public var precise: Bool
```

**功能：** 如果设置为true，在上传/下载无法获取文件大小时任务失败。如果设置为false，将文件大小设置为-1时任务继续。默认值为false。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var priority

```cangjie
public var priority: UInt32
```

**功能：** 任务的优先级。任务模式相同的情况下，该配置项的数字越小优先级越高，默认值为0。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var redirect

```cangjie
public var redirect: Bool
```

**功能：** 是否允许重定向，默认为true。true：是。false：否。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var retry

```cangjie
public var retry: Bool
```

**功能：** 是否为后台任务启用自动重试，仅应用于后台任务，默认为true。true：是。false：否。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var roaming

```cangjie
public var roaming: Bool
```

**功能：** 是否允许在漫游网络中工作，默认为true。true：是。false：否。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var saveas

```cangjie
public var saveas:String
```

**功能：** 保存下载文件的路径，包括如下几种：
-相对路径，位于调用方的缓存路径下，如"./xxx/yyy/zzz.html"、"xxx/yyy/zzz.html"。
-internal协议路径，仅支持"internal://cache/"及其子路径，如"internal://cache/path/to/file.txt"。-应用沙箱目录，只支持到base及其子目录下，如"/data/storage/el1/base/path/to/file.txt"。
-file协议路径，必须匹配应用包名，只支持到base及其子目录下，如"file://com.example.test/data/storage/el2/base/file.txt"。
默认为相对路径，即下载至调用方当前缓存路径下。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var title

```cangjie
public var title:?String
```

**功能：** 任务标题，其最大长度为256个字符，默认值为小写的upload或download，与上面的action保持一致。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var token

```cangjie
public var token: ?String
```

**功能：** 当创建了一个带有token的任务后，token则为正常查询期间必须提供的，否则将无法通过查询进行检索。其最小长度为8个字节，最大长度为2048个字节。默认为空。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var url

```cangjie
public var url: String
```

**功能：** 资源地址，其最大长度为2048个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### init(Action, String, ?String, String, Mode, Bool, ?String, HashMap\<String,String>, ?ConfigData, String, Network, Bool, Bool, Bool, Bool, UInt32, Int64, Int64, Bool, Bool, ?String, UInt32, HashMap\<String,String>)

```cangjie

public init(action: Action, url: String, title!: ?String = None, description!: String = "",
    mode!: Mode = Mode.Background, overwrite!: Bool = false, method!: ?String = None,
    headers!: HashMap<String, String> = HashMap<String, String>(), data!: ?ConfigData = None, saveas!: ?String = "./",
    network!: Network = Network.AnyType, metered!: Bool = false, roaming!: Bool = true, retry!: Bool = true,
    redirect!: Bool = true, index!: UInt32 = 0, begins!: Int64 = 0, ends!: Int64 = -1, gauge!: Bool = false,
    precise!: Bool = false, token!: ?String = None, priority!: UInt32 = 0,extras!: HashMap<String, String> = HashMap<String, String>()
)
```

**功能：** 创建Config对象。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名      | 类型                            | 必填 | 默认值                     | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :---------- | :------------------------------ | :--- | :------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action      | [Action](#enum-action)          | 是   | -                          | **命名参数。** 任务操作选项。<br>- UPLOAD表示上传任务。<br>- DOWNLOAD表示下载任务。                                                                                                                                                                                                                                                                                                                                                                                                                            |
| url         | String                          | 是   | -                          | **命名参数。** 资源地址，其最大长度为2048个字符。                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| title       | ?String                         | 否   | None                       | **命名参数。** 任务标题，其最大长度为256个字符，默认值为小写的upload 或download，与上面的action 保持一致。                                                                                                                                                                                                                                                                                                                                                                                                     |
| description | String                          | 否   | ""                         | **命名参数。** 任务的详细信息，其最大长度为1024个字符，默认值为空字符串。                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| mode        | [Mode](#enum-mode)              | 否   | Mode.Background            | **命名参数。** 任务模式, 默认为后台任务。                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| overwrite   | Bool                            | 否   | false                      | **命名参数。** 下载过程中路径已存在时的解决方案选择，默认为false。<br>- true，覆盖已存在的文件。<br>- false，下载失败。                                                                                                                                                                                                                                                                                                                                                                                        |
| method      | ?String                         | 否   | None                       | **命名参数。** 上传或下载的HTTP标准方法，包括GET、POST和PUT，不区分大小写。<br>-上传时，使用PUT或POST，默认值为PUT。<br>-下载时，使用GET或POST，默认值为GET。                                                                                                                                                                                                                                                                                                                                                  |
| headers     | HashMap\<String,String>         | 否   | HashMap<String,String>()   | **命名参数。** 添加要包含在任务中的HTTP协议标志头。<br>-对于上传请求，默认的Content-Type为"multipart/form-data"。<br>-对于下载请求，默认的Content-Type为"application/json"。                                                                                                                                                                                                                                                                                                                                   |
| data        | ?[ConfigData](#enum-configdata) | 否   | None                       | **命名参数。** -下载时，data为字符串类型，通常使用json(object将被转换为json文本)，默认为空。<br>-上传时，data是表单项数组Array&lt;FormItem&gt;，默认为空。                                                                                                                                                                                                                                                                                                                                                     |
| saveas      | ?String                         | 否   | "./"                       | **命名参数。** 保存下载文件的路径，包括如下几种：<br>-相对路径，位于调用方的缓存路径下，如"./xxx/yyy/zzz.html"、"xxx/yyy/zzz.html"。<br>-internal协议路径，仅支持"internal://cache/"及其子路径，如"internal://cache/path/to/file.txt"。<br>-应用沙箱目录，只支持到base及其子目录下，如"/data/storage/el1/base/path/to/file.txt"。<br>-file协议路径，必须匹配应用包名，只支持到base及其子目录下，如"file://com.example.test/data/storage/el2/base/file.txt"。<br>默认为相对路径，即下载至调用方当前缓存路径下。 |
| network     | [Network](#enum-network)        | 否   | Network.AnyType            | **命名参数。** 网络选项，当前支持无线网络WIFI和蜂窝数据网络CELLULAR，默认为ANY（WIFI或CELLULAR）。                                                                                                                                                                                                                                                                                                                                                                                                             |
| metered     | Bool                            | 否   | false                      | **命名参数。** 是否允许在按流量计费的网络中工作，默认为false。<br>-true：是<br>-false：否                                                                                                                                                                                                                                                                                                                                                                                                                      |
| roaming     | Bool                            | 否   | true                       | **命名参数。** 是否允许在漫游网络中工作，默认为true。<br>-true：是<br>-false：否                                                                                                                                                                                                                                                                                                                                                                                                                               |
| retry       | Bool                            | 否   | true                       | **命名参数。** 是否为后台任务启用自动重试，仅应用于后台任务，默认为true。<br>-true：是<br>-false：否                                                                                                                                                                                                                                                                                                                                                                                                           |
| redirect    | Bool                            | 否   | true                       | **命名参数。** 是否允许重定向，默认为true。<br>-true：是<br>-false：否                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| index       | UInt32                          | 否   | 0                          | **命名参数。** 任务的路径索引，通常用于任务断点续传，默认为0。                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| begins      | Int64                           | 否   | 0                          | **命名参数。** 文件起点，通常用于断点续传。默认值为0，取值为闭区间。<br>-下载时，请求读取服务器开始下载文件时的起点位置（http协议中设置"Range"选项）。<br>-上传时，在上传开始时读取。                                                                                                                                                                                                                                                                                                                          |
| ends        | Int64                           | 否   | - 1                        | **命名参数。** 文件终点，通常用于断点续传。默认值为-1，取值为闭区间。<br>-下载时，请求读取服务器开始下载文件时的结束位置（http协议中设置"Range"选项）。<br>-上传时，在上传时结束读取。                                                                                                                                                                                                                                                                                                                         |
| gauge       | Bool                            | 否   | false                      | **命名参数。** 后台任务的过程进度通知策略，仅应用于后台任务，默认值为false。<br>-false：代表仅完成或失败的通知。<br>-true：发出每个进度已完成或失败的通知。                                                                                                                                                                                                                                                                                                                                                    |
| precise     | Bool                            | 否   | false                      | **命名参数。** -如果设置为true，在上传/下载无法获取文件大小时任务失败。<br>-如果设置为false，将文件大小设置为-1时任务继续。<br>默认值为false。                                                                                                                                                                                                                                                                                                                                                                 |
| token       | ?String                         | 否   | None                       | **命名参数。** 当创建了一个带有token的任务后，token则为正常查询期间必须提供的，否则将无法通过查询进行检索。其最小为8个字节，最大为2048个字节。默认为空。                                                                                                                                                                                                                                                                                                                                                       |
| priority    | UInt32                          | 否   | 0                          | **命名参数。** 任务的优先级。任务模式相同的情况下，该配置项的数字越小优先级越高，默认值为0。                                                                                                                                                                                                                                                                                                                                                                                                                   |
| extras      | HashMap\<String,String>         | 否   | HashMap\<String, String>() | **命名参数。** 配置的附加功能，默认为空。                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleConfigInit(): Unit {
    try {
        let config = Config(
            action = Action.Download,
            url = "https://example.com/file.txt",
            title = "示例下载任务",
            description = "这是一个示例下载任务",
            mode = Mode.Background,
            overwrite = true,
            network = Network.Wifi,
            metered = false,
            roaming = true,
            retry = true,
            redirect = true,
            gauge = false,
            precise = false,
            priority = 0
        )
        Hilog.info(0, "cangjie_ohos_test", "成功创建配置对象")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "创建配置对象失败: ${e.toString()}")
    }
}
```

## class FileSpec

```cangjie
public class FileSpec {
    public var path: String
    public var mimeType:?String
    public var filename:?String
    public var extras: HashMap<String, String>

    public init(
        path: String,
        mimeType!: ?String = None,
        filename!: ?String = None,
        extras!: HashMap<String, String> = HashMap<String, String>()
    )
}
```

**功能：** 表单项的文件信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**功能：** 文件信息的附加内容。

**类型：** HashMap\<String,String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var filename

```cangjie
public var filename:?String
```

**功能：** 文件名，默认值通过路径获取。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var mimeType

```cangjie
public var mimeType:?String
```

**功能：** 文件的mimetype通过文件名获取。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var path

```

```

## enum Network

```cangjie
public enum Network <: Equatable<Network> & ToString {
    | AnyType
    | Wifi
    | Cellular
    | ...
}
```

## enum Mode

```cangjie
public enum Mode <: Equatable<Mode> & ToString {
    | Background
    | Foreground

    public func toString(): String
}
```

**功能：** 任务模式。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 21

### func toString()

```cangjie
public func toString(): String
```

```cangjie
public var path: String
```

**功能：** 文件路径：位于调用方的缓存文件夹下的相对路径或用户公共文件，如"file://media/Photo/path/to/file.img"。
仅支持前端任务。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### init(String, ?String, ?String, HashMap\<String,String>)

```cangjie

public init(
    path: String,
    mimeType!: ?String = None,
    filename!: ?String = None,
    extras!: HashMap<String, String> = HashMap<String, String>()
)
```

**功能：** 创建FileSpec对象。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名   | 类型                    | 必填 | 默认值                   | 说明                                                                                                                                             |
| :------- | :---------------------- | :--- | :----------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| path     | String                  | 是   | -                        | **命名参数。** 文件路径：<br>- 位于调用方的缓存文件夹下的相对路径。<br>- 用户公共文件，如"file://media/Photo/path/to/file.img"。仅支持前端任务。 |
| mimeType | ?String                 | 否   | None                     | **命名参数。** 文件的mimetype通过文件名获取。                                                                                                    |
| filename | ?String                 | 否   | None                     | **命名参数。** 文件名，默认值通过路径获取。                                                                                                      |
| extras   | HashMap\<String,String> | 否   | HashMap<String,String>() | **命名参数。** 文件信息的附加内容。                                                                                                              |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleFileSpecInit(): Unit {
    try {
        let fileSpec = FileSpec(
            path = "./example.txt",
            mimeType = "text/plain",
            filename = "example.txt"
        )
        Hilog.info(0, "cangjie_ohos_test", "成功创建文件规范对象")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "创建文件规范对象失败: ${e.toString()}")
    }
}
```

## class Filter

```cangjie
public class Filter {
    public var before:?Int64
    public var after:?Int64
    public var state:?State
    public var action:?Action
    public var mode:?Mode

    public init(before!: ?Int64 = None, after!: ?Int64 = None, state!: ?State = None,
        action!: ?Action = None, mode!: ?Mode = None
    )
}
```

**功能：** 过滤条件。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var action

```cangjie
public var action:?Action
```

**功能：** 任务操作选项。UPLOAD表示上传任务。DOWNLOAD表示下载任务。

**类型：** ?[Action](#enum-action)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var after

```cangjie
public var after:?Int64
```

**功能：** 开始的Unix时间戳（毫秒），默认值为调用时刻减24小时。

**类型：** ?Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var before

```cangjie
public var before:?Int64
```

**功能：** 结束的Unix时间戳（毫秒），默认为调用时刻。

**类型：** ?Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var mode

```cangjie
public var mode:?Mode
```

**功能：** 任务模式。FOREGROUND表示前端任务。BACKGROUND表示后台任务。如果未填写，则查询所有任务。

**类型：** ?[Mode](#enum-mode)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var state

```cangjie
public var state:?State
```

**功能：** 指定任务的状态。

**类型：** ?[State](#enum-state)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### init(?Int64, ?Int64, ?State, ?Action, ?Mode)

```cangjie

public init(before!: ?Int64 = None, after!: ?Int64 = None, state!: ?State = None,
    action!: ?Action = None, mode!: ?Mode = None
)
```

**功能：** 创建Filter对象。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型                    | 必填 | 默认值 | 说明                                                                                                                 |
| :----- | :---------------------- | :--- | :----- | :------------------------------------------------------------------------------------------------------------------- |
| before | ?Int64                  | 否   | None   | **命名参数。** 结束的Unix时间戳（毫秒），默认为调用时刻。                                                            |
| after  | ?Int64                  | 否   | None   | **命名参数。** 开始的Unix时间戳（毫秒），默认值为调用时刻减24小时。                                                  |
| state  | ?[State](#enum-state)   | 否   | None   | **命名参数。** 指定任务的状态。                                                                                      |
| action | ?[Action](#enum-action) | 否   | None   | **命名参数。** 任务操作选项。<br>-UPLOAD表示上传任务。<br>-DOWNLOAD表示下载任务。                                    |
| mode   | ?[Mode](#enum-mode)     | 否   | None   | **命名参数。** 任务模式。<br>-FOREGROUND表示前端任务。<br>-BACKGROUND表示后台任务。<br>-如果未填写，则查询所有任务。 |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleFilterInit(): Unit {
    try {
        let filter = Filter(
            before = None,
            after = None,
            state = State.Running,
            action = Action.Download,
            mode = Mode.Background
        )
        Hilog.info(0, "cangjie_ohos_test", "成功创建过滤器对象")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "创建过滤器对象失败: ${e.toString()}")
    }
}
```

## class FormItem

```cangjie
public class FormItem {
    public var name: String
    public var value: FormItemValue

    public init(name: String, value: FormItemValue)
}
```

**功能：** 上传/下载任务的配置信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 表单参数名。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var value

```cangjie
public var value: FormItemValue
```

**功能：** 表单参数值。

**类型：** [FormItemValue](#enum-formitemvalue)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### init(String, FormItemValue)

```cangjie

public init(name: String, value: FormItemValue)
```

**功能：** 创建FormItem对象。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型                                 | 必填 | 默认值 | 说明                        |
| :----- | :----------------------------------- | :--- | :----- | :-------------------------- |
| name   | String                               | 是   | -      | **命名参数。** 表单参数名。 |
| value  | [FormItemValue](#enum-formitemvalue) | 是   | -      | **命名参数。** 表单参数值。 |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleFormItemInit(): Unit {
    try {
        let formItem = FormItem(
            name = "exampleField",
            value = FormItemValue.StringItem("exampleValue")
        )
        Hilog.info(0, "cangjie_ohos_test", "成功创建表单项对象")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "创建表单项对象失败: ${e.toString()}")
    }
}
```

## class HttpResponse

```cangjie
public class HttpResponse {
    public let version: String
    public let statusCode: Int32
    public let reason: String
    public let headers: HashMap<String, Array<String>>
}
```

**功能：** 任务响应头的数据结构。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let headers

```cangjie
public let headers: HashMap<String, Array<String>>
```

**功能：** Http响应头部。

**类型：** HashMap\<String,Array\<String>>

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let reason

```cangjie
public let reason: String
```

**功能：** Http响应原因。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let statusCode

```cangjie
public let statusCode: Int32
```

**功能：** Http响应状态码。

**类型：** Int32

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let version

```cangjie
public let version: String
```

**功能：** Http版本。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

## class Progress

```cangjie
public class Progress {
    public let state: State
    public let index: UInt32
    public let processed: Int64
    public let sizes: Array<Int64>
    public let extras: HashMap<String, String>
}
```

**功能：** 任务进度的数据结构。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**功能：** 交互的额外内容，例如来自服务器的响应的header和body。

**类型：** HashMap\<String,String>

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let index

```cangjie
public let index: UInt32
```

**功能：** 任务中当前正在处理的文件索引。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let processed

```cangjie
public let processed: Int64
```

**功能：** 任务中当前文件的已处理数据大小，单位为B。

**类型：** Int64

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let sizes

```cangjie
public let sizes: Array<Int64>
```

**功能：** 任务中文件的大小，单位为B。

**类型：** Array\<Int64>

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let state

```cangjie
public let state: State
```

**功能：** 任务当前的状态。

**类型：** [State](#enum-state)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

## class Task

```cangjie
public class Task {
    public let tid: String
    public var config: Config

    public init(tid: String, config: Config)
}
```

**功能：** 上传或下载任务。使用该方法前需要先获取Task对象，通过create获取。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### var config

```cangjie
public var config: Config
```

**功能：** 任务的配置信息。

**类型：** [Config](#class-config)

**读写能力：** 可读写

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let tid

```cangjie
public let tid: String
```

**功能：** 任务id，在系统上是唯一的，由系统自动生成。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### init(String, Config)

```cangjie

public init(tid: String, config: Config)
```

**功能：** 创建Task对象。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名 | 类型                    | 必填 | 默认值 | 说明                                       |
| :----- | :---------------------- | :--- | :----- | :----------------------------------------- |
| tid    | String                  | 是   | -      | 任务id，在系统上是唯一的，由系统自动生成。 |
| config | [Config](#class-config) | 是   | -      | 任务的配置信息。                           |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleTaskInit(): Unit {
    try {
        let context = Global.abilityContext
        let taskId = "example_task_id"
        let config = Config(
            action = Action.Download,
            url = "https://example.com/file.txt"
        )
        let task = Task(taskId, config)
        Hilog.info(0, "cangjie_ohos_test", "成功初始化任务，任务ID: ${task.tid}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "初始化任务失败: ${e.toString()}")
    }
}
```

### func off(EventCallbackType, ?CallbackObject)

```cangjie

public func off(event: EventCallbackType, callback!: ?CallbackObject = None): Unit
```

**功能：** 取消订阅任务事件。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名   | 类型                                                                               | 必填 | 默认值 | 说明                                                                                                                                                                                                                                                                               |
| :------- | :--------------------------------------------------------------------------------- | :--- | :----- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| event    | [EventCallbackType](#enum-eventcallbacktype)                                       | 是   | -      | 订阅的事件类型。<br>- 取值为'progress'，表示任务进度。<br>- 取值为'completed'，表示任务完成。<br>- 取值为'failed'，表示任务失败。<br>- 取值为'pause'，表示任务暂停。<br>- 取值为'resume'，表示任务恢复。<br>- 取值为'remove'，表示任务删除。<br>- 取值为'response'，表示任务响应。 |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | 否   | None   | **命名参数。** 需要取消订阅的回调函数。若无此参数，则取消订阅当前类型的所有回调函数。                                                                                                                                                                                              |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleTaskOff(): Unit {
    try {
        let context = Global.abilityContext
        let taskId = "example_task_id"
        let config = Config(
            action = Action.Download,
            url = "https://example.com/file.txt"
        )
        let task = Task(taskId, config)

        // 先订阅事件
        task.on(EventCallbackType.Progress, (progress) => {
            Hilog.info(0, "cangjie_ohos_test", "下载进度: ${progress.progress}%")
        })

        // 取消订阅事件
        task.off(EventCallbackType.Progress)
        Hilog.info(0, "cangjie_ohos_test", "成功取消订阅进度事件")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "取消订阅事件失败: ${e.toString()}")
    }
}
```

### func on(EventCallbackType, Callback1Argument<HttpResponse>)

```cangjie

public func on(event: EventCallbackType, callback: Callback1Argument<HttpResponse>): Unit
```

**功能：** 订阅任务响应头。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名   | 类型                                                                                                   | 必填 | 默认值 | 说明                                                       |
| :------- | :----------------------------------------------------------------------------------------------------- | :--- | :----- | :--------------------------------------------------------- |
| event    | [EventCallbackType](#enum-eventcallbacktype)                                                           | 是   | -      | 订阅的事件类型。<br>- 取值为'response'，表示任务响应。     |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HttpResponse> | 是   | -      | 发生相关的事件时触发该回调方法，返回任务响应头的数据结构。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)

  | 错误码ID | 错误信息                       |
  | :------- | :----------------------------- |
  | 401      | Parameter verification failed. |

### func on(EventCallbackType, Callback1Argument\<Progress>)

```cangjie

public func on(event: EventCallbackType, callback: Callback1Argument<Progress>): Unit
```

**功能：** 订阅任务的事件。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**参数：**


| 参数名   | 类型                                                                                                                  | 必填 | 默认值 | 说明                                                                                                                                                                                                                                         |
| :------- | :-------------------------------------------------------------------------------------------------------------------- | :--- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| event    | [EventCallbackType](#enum-eventcallbacktype)                                                                          | 是   | -      | 订阅的事件类型。<br>- 取值为'progress'，表示任务进度。<br>- 取值为'completed'，表示任务完成。<br>- 取值为'failed'，表示任务失败。<br>- 取值为'pause'，表示任务暂停。<br>- 取值为'resume'，表示任务恢复。<br>- 取值为'remove'，表示任务删除。 |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[Progress](#class-progress)> | 是   | -      | 发生相关的事件时触发该回调方法，返回任务信息的数据结构。                                                                                                                                                                                     |

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                       |
  | :------- | :----------------------------- |
  | 401      | Parameter verification failed. |

### func pause()

```cangjie

public func pause(): Unit
```

**功能：** 暂停任务，可以暂停正在等待/正在运行/正在重试的后台任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                         |
  | :------- | :------------------------------- |
  | 13400003 | Task service ability error.      |
  | 21900005 | Operation with wrong task mode.  |
  | 21900007 | Operation with wrong task state. |

### func resume()

```cangjie

public func resume(): Unit
```

**功能：** 重新启动任务，可以恢复暂停的后台任务。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                         |
  | :------- | :------------------------------- |
  | 201      | Permission denied.               |
  | 13400003 | Task service ability error.      |
  | 21900005 | Operation with wrong task mode.  |
  | 21900007 | Operation with wrong task state. |

### func start()

```cangjie

public func start(): Unit
```

**功能：** 启动任务，无法启动已初始化的任务。可以启动一个已失败或已停止的下载任务，从上次的进度开始续传。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                         |
  | :------- | :------------------------------- |
  | 201      | Permission denied.               |
  | 13400003 | Task service ability error.      |
  | 21900007 | Operation with wrong task state. |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleTaskStart(): Unit {
    try {
        let context = Global.abilityContext
        let config = Config(
            action = Action.Download,
            url = "https://example.com/file.txt"
        )
        let task = create(context, config)

        task.start()
        Hilog.info(0, "cangjie_ohos_test", "成功启动任务")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "启动任务失败: ${e.toString()}")
    }
}
```

### func stop()

```cangjie

public func stop(): Unit
```

**功能：** 停止任务，可以停止正在运行/正在等待/正在重试的任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[上传下载错误码](./cj-errorcode-request.md)。

  | 错误码ID | 错误信息                         |
  | :------- | :------------------------------- |
  | 13400003 | Task service ability error.      |
  | 21900007 | Operation with wrong task state. |

**示例：**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog

func exampleTaskStop(): Unit {
    try {
        let context = Global.abilityContext
        let config = Config(
            action = Action.Download,
            url = "https://example.com/largefile.zip"
        )
        let task = create(context, config)

        task.start()
        task.stop()
        Hilog.info(0, "cangjie_ohos_test", "成功停止任务")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "停止任务失败: ${e.toString()}")
    }
}
```

## class TaskInfo

```cangjie
public class TaskInfo {
    public let saveas: String
    public let url: String
    public let data: ConfigData
    public let tid: String
    public let title: String
    public let description: String
    public let action: Action
    public let mode: Mode
    public let priority: UInt32
    public let mimeType: String
    public let progress: Progress
    public let gauge: Bool
    public let ctime: UInt64
    public let mtime: UInt64
    public let retry: Bool
    public let tries: UInt32
    public let faults: Faults
    public let reason: String
    public let extras: HashMap<String, String>
}
```

**功能：** 查询结果的任务信息数据结构，提供普通查询和系统查询，两种字段的可见范围不同。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let action

```cangjie
public let action: Action
```

**功能：** 任务操作选项。UPLOAD表示上传任务。DOWNLOAD表示下载任务。

**类型：** [Action](#enum-action)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let ctime

```cangjie
public let ctime: UInt64
```

**功能：** 创建任务的Unix时间戳（毫秒），由当前设备的系统生成。

**类型：** UInt64

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let data

```cangjie
public let data: ConfigData
```

**功能：** 任务值。

**类型：** [ConfigData](#enum-configdata)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let description

```cangjie
public let description: String
```

**功能：** 任务描述。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**功能：** 任务的额外部分。

**类型：** HashMap\<String,String>

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let faults

```cangjie
public let faults: Faults
```

**功能：** 任务的失败原因。OTHERS表示其他故障。DISCONNECT表示网络断开连接。TIMEOUT表示任务超时。PROTOCOL表示协议错误。FSIO表示文件系统io错误。

**类型：** [Faults](#enum-faults)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let gauge

```cangjie
public let gauge: Bool
```

**功能：** 后台任务的进度通知策略。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let mimeType

```cangjie
public let mimeType: String
```

**功能：** 任务配置中的mimetype。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let mode

```cangjie
public let mode: Mode
```

**功能：** 指定任务模式。FOREGROUND表示前端任务。BACKGROUND表示后台任务。

**类型：** [Mode](#enum-mode)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let mtime

```cangjie
public let mtime: UInt64
```

**功能：** 任务状态改变时的Unix时间戳（毫秒），由当前设备的系统生成。

**类型：** UInt64

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let priority

```cangjie
public let priority: UInt32
```

**功能：** 任务配置中的优先级。前端任务的优先级比后台任务高。相同模式的任务，数字越小优先级越高。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let progress

```cangjie
public let progress: Progress
```

**功能：** 任务的过程进度。

**类型：** [Progress](#class-progress)

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let reason

```cangjie
public let reason: String
```

**功能：** 等待/失败/停止/暂停任务的原因。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let retry

```cangjie
public let retry: Bool
```

**功能：** 任务的重试开关，仅应用于后台任务。

**类型：** Bool

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let saveas

```cangjie
public let saveas: String
```

**功能：** 保存下载文件的路径。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let tid

```cangjie
public let tid: String
```

**功能：** 任务id。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let title

```cangjie
public let title: String
```

**功能：** 任务标题。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let tries

```cangjie
public let tries: UInt32
```

**功能：** 任务的尝试次数。

**类型：** UInt32

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### let url

```cangjie
public let url: String
```

**功能：** 任务的url。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

## enum Action

```cangjie
public enum Action <: Equatable<Action> & ToString {
    | Download
    | Upload
    | ...
}
```

**功能：** 定义操作选项。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- Equatable\<Action>
- ToString

### Download

```cangjie
Download
```

**功能：** 表示下载任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Upload

```cangjie
Upload
```

**功能：** 表示上传任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func !=(Action)

```cangjie
public operator func !=(other: Action): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**


| 参数名 | 类型                   | 必填 | 默认值 | 说明           |
| :----- | :--------------------- | :--- | :----- | :------------- |
| other  | [Action](#enum-action) | 是   | -      | 另一个枚举值。 |

**返回值：**


| 类型 | 说明                                      |
| :--- | :---------------------------------------- |
| Bool | 两个枚举值不相等返回true，否则返回false。 |

### func ==(Action)

```cangjie
public operator func ==(other: Action): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**


| 参数名 | 类型                   | 必填 | 默认值 | 说明           |
| :----- | :--------------------- | :--- | :----- | :------------- |
| other  | [Action](#enum-action) | 是   | -      | 另一个枚举值。 |

**返回值：**


| 类型 | 说明                                    |
| :--- | :-------------------------------------- |
| Bool | 两个枚举值相等返回true，否则返回false。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                   |
| :----- | :--------------------- |
| String | 当前枚举的字符串表示。 |

## enum BroadcastEvent

```cangjie
public enum BroadcastEvent <: ToString {
    | Complete
    | ...
}
```

**功能：** 定义自定义系统事件。用户可以使用公共事件接口获取该事件。上传下载SA具有'ohos.permission.SEND_TASK_COMPLETE_EVENT' 该权限，用户可以配置事件的metadata 指向的二级配置文件来拦截其他事件发送者。使用CommonEventData 类型传输公共事件相关数据。成员的内容填写和[CommonEventData介绍](./cj-apis-common_event_manager.md) 介绍的有所区别，其中CommonEventData.code 表示任务的状态，目前为0x40 COMPLETE或0x41 FAILED; CommonEventData.data 表示任务的taskId。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- ToString

### Complete

```cangjie
Complete
```

**功能：** 表示任务完成事件。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func toString()

```cangjie

public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**返回值：**


| 类型   | 说明                   |
| :----- | :--------------------- |
| String | 当前枚举的字符串表示。 |

## enum ConfigData

```cangjie
public enum ConfigData {
    | StringValue(String)
    | FormItems(Array<FormItem>)
    | ...
}
```

**功能：** 上传/下载任务的data配置枚举类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### FormItems(Array\<FormItem>)

```cangjie
FormItems(Array<FormItem>)
```

**功能：** 表示上传时，data是表单项数组Array&lt;FormItem&gt;，默认为空。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**功能：** 下载时，data为字符串类型，通常使用json(object将被转换为json文本)，默认为空。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

## enum EventCallbackType

```cangjie
public enum EventCallbackType <: Equatable<EventCallbackType> & Hashable & ToString {
    | Progress
    | Completed
    | Failed
    | Pause
    | Resume
    | Remove
    | Response
    | ...
}
```

**功能：** 订阅事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- Equatable\<EventCallbackType>
- Hashable
- ToString

### Completed

```cangjie
Completed
```

**功能：** 表示任务完成的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Failed

```cangjie
Failed
```

**功能：** 表示任务失败的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Pause

```cangjie
Pause
```

**功能：** 表示任务暂停的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Progress

```cangjie
Progress
```

**功能：** 表示任务进度的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Remove

```cangjie
Remove
```

**功能：** 表示任务移除的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Response

```cangjie
Response
```

**功能：** 表示任务接收到响应的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Resume

```cangjie
Resume
```

**功能：** 表示任务恢复的事件类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func !=(EventCallbackType)

```cangjie
public operator func !=(other: EventCallbackType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**


| 参数名 | 类型                                         | 必填 | 默认值 | 说明     |
| :----- | :------------------------------------------- | :--- | :----- | :------- |
| other  | [EventCallbackType](#enum-eventcallbacktype) | 是   | -      | 回调事件 |

**返回值：**


| 类型 | 说明                                      |
| :--- | :---------------------------------------- |
| Bool | 两个枚举值不相等返回true，否则返回false。 |

### func ==(EventCallbackType)

```cangjie
public operator func ==(other: EventCallbackType): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**


| 参数名 | 类型                                         | 必填 | 默认值 | 说明     |
| :----- | :------------------------------------------- | :--- | :----- | :------- |
| other  | [EventCallbackType](#enum-eventcallbacktype) | 是   | -      | 回调事件 |

**返回值：**


| 类型 | 说明                                    |
| :--- | :-------------------------------------- |
| Bool | 两个枚举值相等返回true，否则返回false。 |

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**功能：** 获取回调事件的哈希值。

**返回值：**


| 类型  | 说明                   |
| :---- | :--------------------- |
| Int64 | 回调事件的哈希值表示。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                   |
| :----- | :--------------------- |
| String | 当前枚举的字符串表示。 |

## enum Faults

```cangjie
public enum Faults <: ToString {
    | Others
    | Disconnected
    | Timeout
    | Protocol
    | Fsio
    | ...
}
```

**功能：** 定义任务失败的原因。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- ToString

### Disconnected

```cangjie
Disconnected
```

**功能：** 表示网络断开连接。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Fsio

```cangjie
Fsio
```

**功能：** 表示文件系统io错误，例如打开/查找/读取/写入/关闭。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Others

```cangjie
Others
```

**功能：** 表示其他故障。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Protocol

```cangjie
Protocol
```

**功能：** 表示协议错误，例如：服务器内部错误（500）、无法处理的数据区间（416）等。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Timeout

```cangjie
Timeout
```

**功能：** 表示任务超时。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                   |
| :----- | :--------------------- |
| String | 当前枚举的字符串表示。 |

## enum FormItemValue

```cangjie
public enum FormItemValue {
    | StringItem(String)
    | FileItem(FileSpec)
    | FileItemArray(Array<FileSpec>)
    | ...
}
```

**功能：** 表单项的文件信息枚举类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### FileItem(FileSpec)

```cangjie
FileItem(FileSpec)
```

**功能：** 表示文件信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### FileItemArray(Array\<FileSpec>)

```cangjie
FileItemArray(Array<FileSpec>)
```

**功能：** 表示多个文件信息。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### StringItem(String)

```cangjie
StringItem(String)
```

**功能：** 表示文件路径。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

## enum Mode

```cangjie
public enum Mode <: Equatable<Mode> & ToString{
    | Background
    | Foreground
    | ...
}
```

**功能：** 定义模式选项。前端任务在应用切换到后台一段时间后失败/暂停；后台任务不受影响。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- Equatable\<Mode>
- ToString

### Background

```cangjie
Background
```

**功能：** 表示后台任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Foreground

```cangjie
Foreground
```

**功能：** 表示前端任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func !=(Mode)

```cangjie
public operator func !=(other: Mode): Bool
```

**功能：** 判断两个枚举值是否不相等。
**参数：**


| 参数名 | 类型               | 必填 | 默认值 | 说明     |
| :----- | :----------------- | :--- | :----- | :------- |
| other  | [Mode](#enum-mode) | 是   | -      | 模式状态 |

**返回值：**


| 类型 | 说明                                      |
| :--- | :---------------------------------------- |
| Bool | 两个枚举值不相等返回true，否则返回false。 |

### func ==(Mode)

```cangjie
public operator func ==(other: Mode): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**


| 参数名 | 类型               | 必填 | 默认值 | 说明     |
| :----- | :----------------- | :--- | :----- | :------- |
| other  | [Mode](#enum-mode) | 是   | -      | 模式状态 |

**返回值：**


| 类型 | 说明                                    |
| :--- | :-------------------------------------- |
| Bool | 两个枚举值相等返回true，否则返回false。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                       |
| :----- | :------------------------- |
| String | 获取当前枚举的字符串表示。 |

## enum Network

```cangjie
public enum Network <: Equatable<Network> & ToString {
    | AnyType
    | Wifi
    | Cellular
    | ...
}
```

**功能：** 定义网络选项。网络不满足设置条件时，未执行的任务等待执行，执行中的任务失败/暂停。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- Equatable\<Network>
- ToString

### AnyType

```cangjie
AnyType
```

**功能：** 表示不限网络类型。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Cellular

```cangjie
Cellular
```

**功能：** 表示蜂窝数据网络。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Wifi

```cangjie
Wifi
```

**功能：** 表示无线网络。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func !=(Network)

```cangjie
public operator func !=(other: Network): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**


| 参数名 | 类型                     | 必填 | 默认值 | 说明     |
| :----- | :----------------------- | :--- | :----- | :------- |
| other  | [Network](#enum-network) | 是   | -      | 网络状态 |

**返回值：**


| 类型 | 说明                                      |
| :--- | :---------------------------------------- |
| Bool | 两个枚举值不相等返回true，否则返回false。 |

### func ==(Network)

```cangjie
public operator func ==(other: Network): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**


| 参数名 | 类型                     | 必填 | 默认值 | 说明     |
| :----- | :----------------------- | :--- | :----- | :------- |
| other  | [Network](#enum-network) | 是   | -      | 网络状态 |

**返回值：**


| 类型 | 说明                                    |
| :--- | :-------------------------------------- |
| Bool | 两个枚举值相等返回true，否则返回false。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                       |
| :----- | :------------------------- |
| String | 获取当前枚举的字符串表示。 |

## enum State

```cangjie
public enum State <: ToString {
    | Initialized
    | Waiting
    | Running
    | Retrying
    | Paused
    | Stopped
    | Completed
    | Failed
    | Removed
    | ...
}
```

**功能：** 定义任务当前的状态。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

**父类型：**

- ToString

### Completed

```cangjie
Completed
```

**功能：** 表示任务完成。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Failed

```cangjie
Failed
```

**功能：** 表示任务失败。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Initialized

```cangjie
Initialized
```

**功能：** 通过配置信息（Config）创建初始化任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Paused

```cangjie
Paused
```

**功能：** 表示任务暂停，通常后续会恢复任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Removed

```cangjie
Removed
```

**功能：** 表示任务移除。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Retrying

```cangjie
Retrying
```

**功能：** 表示任务至少失败一次，现在正在再次处理中。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Running

```cangjie
Running
```

**功能：** 表示正在处理的任务。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Stopped

```cangjie
Stopped
```

**功能：** 表示任务停止。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### Waiting

```cangjie
Waiting
```

**功能：** 表示任务缺少运行或重试的资源与网络状态不匹配。

**系统能力：** SystemCapability.Request.FileTransferAgent

**起始版本：** 22

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**


| 类型   | 说明                       |
| :----- | :------------------------- |
| String | 获取当前枚举的字符串表示。 |
