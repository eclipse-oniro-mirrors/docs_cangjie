# ohos.request

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The request component primarily provides applications with fundamental capabilities for uploading/downloading files and background transfer proxying.

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Permission List

ohos.permission.INTERNET

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func create(UIAbilityContext, Config)

```cangjie
public func create(context: UIAbilityContext, config: Config): Task
```

**Function:** Creates an upload or download task and queues it.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type                                                                                       | Required | Default | Description                          |
| :-------- | :----------------------------------------------------------------------------------------- | :------- | :------ | :----------------------------------- |
| context   | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes      | -       | Application-based context.           |
| config    | [Config](#class-config)                                                                    | Yes      | -       | Configuration information for upload/download tasks. |

**Return Value:**

| Type                | Description                                                  |
| :------------------ | :----------------------------------------------------------- |
| [Task](#class-task) | Returns a Task object containing the task ID and configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 201          | Permission denied.                                                                                                                    |
  | 13400001     | Invalid file or file system error.                                                                                                    |
  | 13400003     | Task service ability error.                                                                                                           |
  | 21900004     | The application task queue is full.                                                                                                   |
  | 21900005     | Operation with wrong task mode.                                                                                                      |
- IllegalArgumentException:

  | Error Message                | Possible Cause | Handling Steps |
  | :--------------------------- | :------------- | :------------- |
  | The context is invalid.      | todo           | todo           |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let config = Config(
        action = Action.Download,
        url = "https://example.com/file.txt"
    )
    let task = create(context, config)
    Hilog.info(0, "cangjie_ohos_test", "Successfully created task, Task ID: ${task.tid}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getTask(UIAbilityContext, String, ?String)

```cangjie
public func getTask(context: UIAbilityContext, id: String, token!: ?String = None): Task
```

**Function:** Queries a task by its ID.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type                                                                                       | Required | Default | Description                          |
| :-------- | :----------------------------------------------------------------------------------------- | :------- | :------ | :----------------------------------- |
| context   | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes      | -       | Application-based context.           |
| id        | String                                                                                     | Yes      | -       | Task ID.                             |
| token     | ?String                                                                                    | No       | None    | **Named parameter.** Task query token. |

**Return Value:**

| Type                | Description                                                  |
| :------------------ | :----------------------------------------------------------- |
| [Task](#class-task) | Returns a Task object containing the task ID and configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 13499999     | Other error.                                                                                                                          |
  | 13400003     | Task service ability error.                                                                                                           |
  | 21900006     | Task removed or not found.                                                                                                            |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let taskId = "example_task_id"
    let task = getTask(context, taskId)
    Hilog.info(0, "cangjie_ohos_test", "Successfully retrieved task, Task ID: ${task.tid}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

- IllegalArgumentException:

  | Error Message                | Possible Cause | Handling Steps |
  | :--------------------------- | :------------- | :------------- |
  | The context is invalid.      | todo           | todo           |

## func remove(String)

```cangjie
public func remove(id: String): Unit
```

**Function:** Removes a specified task belonging to the caller. If the task is in progress, it will be forcibly stopped.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type   | Required | Default | Description |
| :-------- | :----- | :------- | :------ | :---------- |
| id        | String | Yes      | -       | Task ID.    |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 13400003     | Task service ability error.                                                                                                           |
  | 21900006     | Task removed or not found.                                                                                                            |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let taskId = "example_task_id"
    remove(taskId)
    Hilog.info(0, "cangjie_ohos_test", "Successfully removed task, Task ID: ${taskId}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func search(Filter)

```cangjie
public func search(filter!: Filter = Filter()): Array<String>
```

**Function:** Finds task IDs based on default [Filter](#class-filter) conditions.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type                    | Required | Default    | Description          |
| :-------- | :---------------------- | :------- | :--------- | :------------------- |
| filter    | [Filter](#class-filter) | No       | Filter()   | Filter conditions.   |

**Return Value:**

| Type           | Description                          |
| :------------- | :----------------------------------- |
| Array\<String> | Returns IDs of tasks meeting the conditions. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 13400003     | Task service ability error.                                                                                                           |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let filter = Filter()
    let taskIds = search(filter)
    Hilog.info(0, "cangjie_ohos_test", "Number of tasks found: ${taskIds.length}")
    for (id in taskIds) {
        Hilog.info(0, "cangjie_ohos_test", "Task ID: ${id}")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func show(String)

```cangjie
public func show(id: String): TaskInfo
```

**Function:** Queries detailed information about a task by its ID.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type   | Required | Default | Description |
| :-------- | :----- | :------- | :------ | :---------- |
| id        | String | Yes      | -       | Task ID.    |

**Return Value:**

| Type                        | Description                                      |
| :-------------------------- | :----------------------------------------------- |
| [TaskInfo](#class-taskinfo) | Returns a TaskInfo object with task details.     |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 13400003     | Task service ability error.                                                                                                           |
  | 21900006     | Task removed or not found.                                                                                                            |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let taskId = "example_task_id"
    let taskInfo = show(taskId)
    Hilog.info(0, "cangjie_ohos_test", "Task information: ${taskInfo.toString()}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func touch(String, String)

```cangjie
public func touch(id: String, token: String): TaskInfo
```

**Function:** Queries detailed information about a task by its ID and token.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22

**Parameters:**

| Parameter | Type   | Required | Default | Description          |
| :-------- | :----- | :------- | :------ | :------------------- |
| id        | String | Yes      | -       | Task ID.             |
| token     | String | Yes      | -       | Task query token.    |

**Return Value:**

| Type                        | Description                                      |
| :-------------------------- | :----------------------------------------------- |
| [TaskInfo](#class-taskinfo) | Returns a TaskInfo object with task details.     |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message                                                                                                                          |
  | :----------- | :------------------------------------------------------------------------------------------------------------------------------------ |
  | 13400003     | Task service ability error.                                                                                                           |
  | 21900006     | Task removed or not found.                                                                                                            |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    try {
        let taskId = "example_task_id"
        let token = "example_token"
        let taskInfo = touch(taskId, token)
        Hilog.info(0, "cangjie_ohos_test", "Task information: ${taskInfo.toString()}")
    } catch (e: Exception) {
        Hilog.info(0, "cangjie_ohos_test", "Failed to query task information: ${e.toString()}")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
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
        headers!: HashMap<String, String> = HashMap<String, String>(), data!: ?ConfigData = None,  saveas!: String = "./",
        network!: Network = Network.AnyType, metered!: Bool = false, roaming!: Bool = true, retry!: Bool = true,
        redirect!: Bool = true, index!: UInt32 = 0, begins!: Int64 = 0, ends!: Int64 = -1, gauge!: Bool = false,
        precise!: Bool = false, token!: String = "", priority!: UInt32 = 0,extras!: HashMap<String, String> = HashMap<String, String>()
    )
}
```

**Function:** Configuration information for upload/download tasks.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Initial Version:** 22### var action

```cangjie
public var action: Action
```

**Function:** Task operation option, where UPLOAD indicates an upload task and DOWNLOAD indicates a download task.

**Type:** [Action](#enum-action)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var begins

```cangjie
public var begins: Int64
```

**Function:** File starting point, typically used for resumable transfers. Default value is 0 (inclusive range). For downloads, it sets the starting position for reading from the server (via HTTP "Range" header). For uploads, it specifies the starting read position at upload initiation.

**Type:** Int64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var data

```cangjie
public var data:?ConfigData
```

**Function:** For downloads, `data` is of string type (typically JSON; objects will be converted to JSON text), defaulting to empty. For uploads, `data` is an array of form items (Array\<FormItem>), defaulting to empty.

**Type:** ?[ConfigData](#enum-configdata)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var description

```cangjie
public var description: String
```

**Function:** Detailed information about the task, with a maximum length of 1024 characters. Default value is an empty string.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var ends

```cangjie
public var ends: Int64
```

**Function:** File ending point, typically used for resumable transfers. Default value is -1 (inclusive range). For downloads, it sets the ending position for reading from the server (via HTTP "Range" header). For uploads, it specifies the ending read position during upload.

**Type:** Int64

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**Function:** Additional configuration features, defaulting to empty.

**Type:** HashMap\<String,String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var gauge

```cangjie
public var gauge: Bool
```

**Function:** Progress notification policy for background tasks (applies only to background tasks). Default is false.  
- `false`: Notifications only upon completion or failure.  
- `true`: Notifications for every progress update, completion, or failure.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var headers

```cangjie
public var headers: HashMap<String, String>
```

**Function:** HTTP headers to include with the task.  
- For uploads, default Content-Type is "multipart/form-data".  
- For downloads, default Content-Type is "application/json".

**Type:** HashMap

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var index

```cangjie
public var index: UInt32
```

**Function:** Task path index, typically used for resumable transfers. Default is 0.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var metered

```cangjie
public var metered: Bool
```

**Function:** Whether to allow operation on metered networks. Default is false.  
- `true`: Allowed  
- `false`: Not allowed

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var method

```cangjie
public var method:?String
```

**Function:** HTTP method for upload/download (case-insensitive): GET, POST, or PUT.  
- Uploads default to PUT.  
- Downloads default to GET.

**Type:** ?String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var mode

```cangjie
public var mode: Mode
```

**Function:** Task mode, defaulting to background task.

**Type:** [Mode](#enum-mode)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var network

```cangjie
public var network: Network
```

**Function:** Network options, currently supporting WIFI and CELLULAR. Default is ANY (WIFI or CELLULAR).

**Type:** [Network](#enum-network)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var overwrite

```cangjie
public var overwrite: Bool
```

**Function:** Behavior when download path already exists. Default is false.  
- `true`: Overwrite existing file.  
- `false`: Download fails.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var precise

```cangjie
public var precise: Bool
```

**Function:** If true, task fails when file size cannot be determined during upload/download. If false, task continues with file size set to -1. Default is false.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var priority

```cangjie
public var priority: UInt32
```

**Function:** Task priority. Lower numbers indicate higher priority for tasks with the same mode. Default is 0.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var redirect

```cangjie
public var redirect: Bool
```

**Function:** Whether to allow redirects. Default is true.  
- `true`: Allowed  
- `false`: Not allowed

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var retry

```cangjie
public var retry: Bool
```

**Function:** Whether to enable automatic retry for background tasks (applies only to background tasks). Default is true.  
- `true`: Enabled  
- `false`: Disabled

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var roaming

```cangjie
public var roaming: Bool
```

**Function:** Whether to allow operation on roaming networks. Default is true.  
- `true`: Allowed  
- `false`: Not allowed

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var saveas

```cangjie
public var saveas:String
```

**Function:** Path to save downloaded files, including:  
- Relative paths (under caller's cache directory), e.g., `"./xxx/yyy/zzz.html"`, `"xxx/yyy/zzz.html"`.  
- `internal://` protocol paths (only under `internal://cache/` and subpaths), e.g., `"internal://cache/path/to/file.txt"`.  
- Application sandbox paths (only under `base` and subdirectories), e.g., `"/data/storage/el1/base/path/to/file.txt"`.  
- `file://` protocol paths (must match app package name, only under `base` and subdirectories), e.g., `"file://com.example.test/data/storage/el2/base/file.txt"`.  
Defaults to relative path (caller's current cache directory).

**Type:** ?String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var title

```cangjie
public var title:?String
```

**Function:** Task title, with a maximum length of 256 characters. Defaults to lowercase "upload" or "download" (matching `action`).

**Type:** ?String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var token

```cangjie
public var token: ?String
```

**Function:** When a task is created with a token, this token is required for normal queries; otherwise, the task cannot be retrieved. Minimum length is 8 bytes; maximum is 2048 bytes. Default is empty.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var url

```cangjie
public var url: String
```

**Function:** Resource URL, with a maximum length of 2048 characters.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

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

**Function:** Creates a Config object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter    | Type                            | Required | Default Value              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| :----------- | :------------------------------ | :------- | :------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action       | [Action](#enum-action)          | Yes      | -                          | **Named parameter.** Task operation option.<br>- `UPLOAD`: Upload task.<br>- `DOWNLOAD`: Download task.                                                                                                                                                                                                                                                                                                                                                                                                         |
| url          | String                          | Yes      | -                          | **Named parameter.** Resource URL, with a maximum length of 2048 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| title        | ?String                         | No       | None                       | **Named parameter.** Task title, with a maximum length of 256 characters. Defaults to lowercase "upload" or "download" (matching `action`).                                                                                                                                                                                                                                                                                                                                                                   |
| description  | String                          | No       | ""                         | **Named parameter.** Detailed task information, with a maximum length of 1024 characters. Default is empty string.                                                                                                                                                                                                                                                                                                                                                                                            |
| mode         | [Mode](#enum-mode)              | No       | Mode.Background            | **Named parameter.** Task mode, defaulting to background task.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| overwrite    | Bool                            | No       | false                      | **Named parameter.** Behavior when download path already exists.<br>- `true`: Overwrite existing file.<br>- `false`: Download fails.                                                                                                                                                                                                                                                                                                                                                                           |
| method       | ?String                         | No       | None                       | **Named parameter.** HTTP method for upload/download (case-insensitive): GET, POST, or PUT.<br>- Uploads default to PUT.<br>- Downloads default to GET.                                                                                                                                                                                                                                                                                                                                                         |
| headers      | HashMap\<String,String>         | No       | HashMap<String,String>()   | **Named parameter.** HTTP headers to include with the task.<br>- For uploads, default Content-Type is "multipart/form-data".<br>- For downloads, default Content-Type is "application/json".                                                                                                                                                                                                                                                                                                                    |
| data         | ?[ConfigData](#enum-configdata) | No       | None                       | **Named parameter.**<br>- For downloads: String type (typically JSON; objects converted to JSON text), defaulting to empty.<br>- For uploads: Array of form items (Array\<FormItem>), defaulting to empty.                                                                                                                                                                                                                                                                                                     |
| saveas       | ?String                         | No       | "./"                       | **Named parameter.** Path to save downloaded files:<br>- Relative paths (under caller's cache directory), e.g., `"./xxx/yyy/zzz.html"`, `"xxx/yyy/zzz.html"`.<br>- `internal://` protocol paths (only under `internal://cache/` and subpaths), e.g., `"internal://cache/path/to/file.txt"`.<br>- Application sandbox paths (only under `base` and subdirectories), e.g., `"/data/storage/el1/base/path/to/file.txt"`.<br>- `file://` protocol paths (must match app package name, only under `base` and subdirectories), e.g., `"file://com.example.test/data/storage/el2/base/file.txt"`.<br>Defaults to relative path (caller's current cache directory). |
| network      | [Network](#enum-network)        | No       | Network.AnyType            | **Named parameter.** Network options, supporting WIFI and CELLULAR. Default is ANY (WIFI or CELLULAR).                                                                                                                                                                                                                                                                                                                                                                                                         |
| metered      | Bool                            | No       | false                      | **Named parameter.** Whether to allow operation on metered networks.<br>- `true`: Allowed<br>- `false`: Not allowed                                                                                                                                                                                                                                                                                                                                                                                           |
| roaming      | Bool                            | No       | true                       | **Named parameter.** Whether to allow operation on roaming networks.<br>- `true`: Allowed<br>- `false`: Not allowed                                                                                                                                                                                                                                                                                                                                                                                             |
| retry        | Bool                            | No       | true                       | **Named parameter.** Whether to enable automatic retry for background tasks (applies only to background tasks).<br>- `true`: Enabled<br>- `false`: Disabled                                                                                                                                                                                                                                                                                                                                                     |
| redirect     | Bool                            | No       | true                       | **Named parameter.** Whether to allow redirects.<br>- `true`: Allowed<br>- `false`: Not allowed                                                                                                                                                                                                                                                                                                                                                                                                                |
| index        | UInt32                          | No       | 0                          | **Named parameter.** Task path index, typically used for resumable transfers. Default is 0.                                                                                                                                                                                                                                                                                                                                                                                                                     |
| begins       | Int64                           | No       | 0                          | **Named parameter.** File starting point for resumable transfers (inclusive range). Default is 0.<br>- For downloads: Starting position for reading from server (HTTP "Range" header).<br>- For uploads: Starting read position at upload initiation.                                                                                                                                                                                                                                                            |
| ends         | Int64                           | No       | -1                         | **Named parameter.** File ending point for resumable transfers (inclusive range). Default is -1.<br>- For downloads: Ending position for reading from server (HTTP "Range" header).<br>- For uploads: Ending read position during upload.                                                                                                                                                                                                                                                                       |
| gauge        | Bool                            | No       | false                      | **Named parameter.** Progress notification policy for background tasks (applies only to background tasks).<br>- `false`: Notifications only upon completion or failure.<br>- `true`: Notifications for every progress update, completion, or failure.                                                                                                                                                                                                                                                           |
| precise      | Bool                            | No       | false                      | **Named parameter.**<br>- If `true`, task fails when file size cannot be determined during upload/download.<br>- If `false`, task continues with file size set to -1.<br>Default is `false`.                                                                                                                                                                                                                                                                                                                  |
| token        | ?String                         | No       | None                       | **Named parameter.** When a task is created with a token, this token is required for normal queries; otherwise, the task cannot be retrieved. Minimum length is 8 bytes; maximum is 2048 bytes. Default is empty.                                                                                                                                                                                                                                                                                               |
| priority     | UInt32                          | No       | 0                          | **Named parameter.** Task priority. Lower numbers indicate higher priority for tasks with the same mode. Default is 0.                                                                                                                                                                                                                                                                                                                                                                                         |
| extras       | HashMap\<String,String>         | No       | HashMap\<String, String>() | **Named parameter.** Additional configuration features, defaulting to empty.                                                                                                                                                                                                                                                                                                                                                                                                                                    |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let config = Config(
        action = Action.Download,
        url = "https://example.com/file.txt",
        title = "Sample Download Task",
        description = "This is a sample download task",
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
    Hilog.info(0, "cangjie_ohos_test", "Successfully created configuration object")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class FileSpec

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

**Function:** File information for form items.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**Function:** Additional content of file information.

**Type:** HashMap\<String,String>

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var filename

```cangjie
public var filename:?String
```

**Function:** Filename, default value obtained from path.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var mimeType

```cangjie
public var mimeType:?String
```

**Function:** File's mimetype obtained from filename.

**Type:** ?String

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var path

```cangjie
public var path:String
```

**Function:** File path.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### init(String, ?String, ?String, HashMap\<String,String>)

```cangjie
public init(
    path: String,
    mimeType!: ?String = None,
    filename!: ?String = None,
    extras!: HashMap<String, String> = HashMap<String, String>()
)
```

**Function:** Creates a FileSpec object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                    | Required | Default Value               | Description                                                                                                                                             |
| :-------- | :---------------------- | :------- | :-------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| path      | String                  | Yes      | -                           | **Named parameter.** File path:<br>- Relative path under the caller's cache folder.<br>- Public user files like "file://media/Photo/path/to/file.img". Only supports foreground tasks. |
| mimeType  | ?String                 | No       | None                        | **Named parameter.** File's mimetype obtained from filename.                                                                                             |
| filename  | ?String                 | No       | None                        | **Named parameter.** Filename, default value obtained from path.                                                                                        |
| extras    | HashMap\<String,String> | No       | HashMap<String,String>()    | **Named parameter.** Additional content of file information.                                                                                            |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let fileSpec = FileSpec(
        path = "./example.txt",
        mimeType = "text/plain",
        filename = "example.txt"
    )
    Hilog.info(0, "cangjie_ohos_test", "Successfully created file specification object")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
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

**Function:** Defines network options. When network conditions don't meet settings, pending tasks will wait for execution, while executing tasks will fail or pause.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### AnyType

```cangjie
AnyType
```

**Function:** Indicates no restriction on network type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### WIFI	

```cangjie
WIFI	
```

**Function:** Indicates wireless network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### CELLULAR		

```cangjie
CELLULAR	
```

**Function:** Indicates cellular data network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

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

**Function:** Filter conditions.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var action

```cangjie
public var action:?Action
```

**Function:** Task operation option. UPLOAD indicates upload task. DOWNLOAD indicates download task.

**Type:** ?[Action](#enum-action)

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var after

```cangjie
public var after:?Int64
```

**Function:** Start Unix timestamp (milliseconds), default value is call time minus 24 hours.

**Type:** ?Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var before

```cangjie
public var before:?Int64
```

**Function:** End Unix timestamp (milliseconds), default is call time.

**Type:** ?Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var mode

```cangjie
public var mode:?Mode
```

**Function:** Task mode. FOREGROUND indicates foreground task. BACKGROUND indicates background task. If unspecified, queries all tasks.

**Type:** ?[Mode](#enum-mode)

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var state

```cangjie
public var state:?State
```

**Function:** Specifies task state.

**Type:** ?[State](#enum-state)

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### init(?Int64, ?Int64, ?State, ?Action, ?Mode)

```cangjie
public init(before!: ?Int64 = None, after!: ?Int64 = None, state!: ?State = None,
    action!: ?Action = None, mode!: ?Mode = None
)
```

**Function:** Creates a Filter object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                    | Required | Default Value | Description                                                                                                                                             |
| :-------- | :---------------------- | :------- | :------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| before    | ?Int64                  | No       | None          | **Named parameter.** End Unix timestamp (milliseconds), default is call time.                                                                           |
| after     | ?Int64                  | No       | None          | **Named parameter.** Start Unix timestamp (milliseconds), default value is call time minus 24 hours.                                                    |
| state     | ?[State](#enum-state)   | No       | None          | **Named parameter.** Specifies task state.                                                                                                              |
| action    | ?[Action](#enum-action) | No       | None          | **Named parameter.** Task operation option.<br>-UPLOAD indicates upload task.<br>-DOWNLOAD indicates download task.                                     |
| mode      | ?[Mode](#enum-mode)     | No       | None          | **Named parameter.** Task mode.<br>-FOREGROUND indicates foreground task.<br>-BACKGROUND indicates background task.<br>-If unspecified, queries all tasks. |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let filter = Filter(
        before = None,
        after = None,
        state = State.Running,
        action = Action.Download,
        mode = Mode.Background
    )
    Hilog.info(0, "cangjie_ohos_test", "Successfully created filter object")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
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

**Function:** Configuration information for upload/download tasks.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var name

```cangjie
public var name: String
```

**Function:** Form parameter name.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var value

```cangjie
public var value: FormItemValue
```

**Function:** Form parameter value.

**Type:** [FormItemValue](#enum-formitemvalue)

**Access:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### init(String, FormItemValue)

```cangjie
public init(name: String, value: FormItemValue)
```

**Function:** Creates a FormItem object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                                 | Required | Default Value | Description                     |
| :-------- | :----------------------------------- | :------- | :------------ | :------------------------------- |
| name      | String                               | Yes      | -             | **Named parameter.** Form parameter name. |
| value     | [FormItemValue](#enum-formitemvalue) | Yes      | -             | **Named parameter.** Form parameter value. |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let formItem = FormItem(
        name = "exampleField",
        value = FormItemValue.StringItem("exampleValue")
    )
    Hilog.info(0, "cangjie_ohos_test", "Successfully created form item object")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class HttpResponse

```cangjie
public class HttpResponse {
    public let version: String
    public let statusCode: Int32
    public let reason: String
    public let headers: HashMap<String, Array<String>>
}
```

**Function:** Data structure for task response headers.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let headers

```cangjie
public let headers: HashMap<String, Array<String>>
```

**Function:** HTTP response headers.

**Type:** HashMap\<String,Array\<String>>

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let reason

```cangjie
public let reason: String
```

**Function:** HTTP response reason phrase.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let statusCode

```cangjie
public let statusCode: Int32
```

**Function:** HTTP response status code.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let version

```cangjie
public let version: String
```

**Function:** HTTP version.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

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

**Function:** Data structure for task progress.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**Function:** Additional interaction content, such as headers and body from server responses.

**Type:** HashMap\<String,String>

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let index

```cangjie
public let index: UInt32
```

**Function:** Index of the currently processed file in the task.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let processed

```cangjie
public let processed: Int64
```

**Function:** Size of processed data for the current file in the task, in bytes.

**Type:** Int64

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let sizes

```cangjie
public let sizes: Array<Int64>
```

**Function:** File sizes in the task, in bytes.

**Type:** Array\<Int64>

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let state

```cangjie
public let state: State
```

**Function:** Current state of the task.

**Type:** [State](#enum-state)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

## class Task

```cangjie
public class Task {
    public let tid: String
    public var config: Config

    public init(tid: String, config: Config)
}
```

**Function:** Upload or download task. Requires obtaining a Task object via create() before use.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### var config

```cangjie
public var config: Config
```

**Function:** Configuration information for the task.

**Type:** [Config](#class-config)

**Access:** Read-write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let tid

```cangjie
public let tid: String
```

**Function:** Unique task ID automatically generated by the system.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### init(String, Config)

```cangjie
public init(tid: String, config: Config)
```

**Function:** Creates a Task object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                    | Required | Default | Description                                      |
| :-------- | :---------------------- | :------- | :------ | :----------------------------------------------- |
| tid       | String                  | Yes      | -       | Unique task ID automatically generated by system |
| config    | [Config](#class-config) | Yes      | -       | Configuration information for the task           |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let taskId = "example_task_id"
    let config = Config(
        action = Action.Download,
        url = "https://example.com/file.txt"
    )
    let task = Task(taskId, config)
    Hilog.info(0, "cangjie_ohos_test", "Task initialized successfully, Task ID: ${task.tid}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(EventCallbackType, ?CallbackObject)

```cangjie
public func off(event: EventCallbackType, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from task events.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                                                                               | Required | Default | Description                                                                                                                                                                                                               |
| :-------- | :--------------------------------------------------------------------------------- | :------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| event     | [EventCallbackType](#enum-eventcallbacktype)                                       | Yes      | -       | Event type to unsubscribe from:<br>- 'progress': Task progress<br>- 'completed': Task completion<br>- 'failed': Task failure<br>- 'pause': Task pause<br>- 'resume': Task resume<br>- 'remove': Task removal<br>- 'response': Task response |
| callback  | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No       | None    | **Named parameter.** Callback function to unsubscribe. If omitted, unsubscribes all callbacks of the specified type.                                                                                                     |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let taskId = "example_task_id"
    let config = Config(
        action = Action.Download,
        url = "https://example.com/file.txt"
    )
    let task = Task(taskId, config)

    // First subscribe to event
    task.on(EventCallbackType.Progress, (progress) => {
        Hilog.info(0, "cangjie_ohos_test", "Download progress: ${progress.progress}%")
    })

    // Then unsubscribe
    task.off(EventCallbackType.Progress)
    Hilog.info(0, "cangjie_ohos_test", "Successfully unsubscribed from progress events")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func on(EventCallbackType, Callback1Argument\<HttpResponse>)

```cangjie
public func on(event: EventCallbackType, callback: Callback1Argument<HttpResponse>): Unit
```

**Function:** Subscribes to task response headers.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                                                                                                   | Required | Default | Description                                                                                     |
| :-------- | :----------------------------------------------------------------------------------------------------- | :------- | :------ | :---------------------------------------------------------------------------------------------- |
| event     | [EventCallbackType](#enum-eventcallbacktype)                                                           | Yes      | -       | Event type to subscribe to:<br>- 'response': Task response                                      |
| callback  | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HttpResponse> | Yes      | -       | Callback triggered when event occurs, returning the response header data structure.             |

**Exceptions:**

- BusinessException: Error codes below, see [Universal Error Codes](../cj-errorcode-universal.md)

  | Error Code | Error Message                  |
  | :--------- | :----------------------------- |
  | 401        | Parameter verification failed.  |

### func on(EventCallbackType, Callback1Argument\<Progress>)

```cangjie
public func on(event: EventCallbackType, callback: Callback1Argument<Progress>): Unit
```

**Function:** Subscribes to task events.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parameters:**

| Parameter | Type                                                                                                                  | Required | Default | Description                                                                                                                                                                     |
| :-------- | :-------------------------------------------------------------------------------------------------------------------- | :------- | :------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| event     | [EventCallbackType](#enum-eventcallbacktype)                                                                          | Yes      | -       | Event type to subscribe to:<br>- 'progress': Task progress<br>- 'completed': Task completion<br>- 'failed': Task failure<br>- 'pause': Task pause<br>- 'resume': Task resume<br>- 'remove': Task removal |
| callback  | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[Progress](#class-progress)> | Yes      | -       | Callback triggered when event occurs, returning the task information data structure.                                                                                            |

**Exceptions:**

- BusinessException: Error codes below, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code | Error Message                  |
  | :--------- | :----------------------------- |
  | 401        | Parameter verification failed. |

### func pause()

```cangjie
public func pause(): Unit
```

**Function:** Pauses a task (can pause waiting/running/retrying background tasks).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Exceptions:**

- BusinessException: Error codes below, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code | Error Message                         |
  | :--------- | :----------------------------------- |
  | 13400003   | Task service ability error.          |
  | 21900005   | Operation with wrong task mode.      |
  | 21900007   | Operation with wrong task state.     |

### func resume()

```cangjie
public func resume(): Unit
```

**Function:** Restarts a paused background task.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Exceptions:**

- BusinessException: Error codes below, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code | Error Message                         |
  | :--------- | :----------------------------------- |
  | 201        | Permission denied.                    |
  | 13400003   | Task service ability error.          |
  | 21900005   | Operation with wrong task mode.      |
  | 21900007   | Operation with wrong task state.     |

### func start()

```cangjie
public func start(): Unit
```

**Function:** Starts a task (cannot restart initialized tasks). Can resume failed/stopped download tasks from last progress.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Exceptions:**

- BusinessException: Error codes below, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code | Error Message                         |
  | :--------- | :----------------------------------- |
  | 201        | Permission denied.                    |
  | 13400003   | Task service ability error.          |
  | 21900007   | Operation with wrong task state.     |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let config = Config(
        action = Action.Download,
        url = "https://example.com/file.txt"
    )
    let task = create(context, config)

    task.start()
    Hilog.info(0, "cangjie_ohos_test", "Task started successfully")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func stop()

```cangjie
public func stop(): Unit
```

**Function:** Stops a task (can stop running/waiting/retrying tasks).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Exceptions:**

- BusinessException: Error codes below, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code | Error Message                         |
  | :--------- | :----------------------------------- |
  | 13400003   | Task service ability error.          |
  | 21900007   | Operation with wrong task state.     |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.abilityContext
    let config = Config(
        action = Action.Download,
        url = "https://example.com/largefile.zip"
    )
    let task = create(context, config)

    task.start()
    task.stop()
    Hilog.info(0, "cangjie_ohos_test", "Task stopped successfully")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class TaskInfo

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

**Function:** Data structure for task information query results, providing both regular and system queries with different field visibility scopes.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let action

```cangjie
public let action: Action
```

**Function:** Task operation options. UPLOAD indicates an upload task. DOWNLOAD indicates a download task.

**Type:** [Action](#enum-action)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let ctime

```cangjie
public let ctime: UInt64
```

**Function:** Unix timestamp (milliseconds) when the task was created, generated by the current device's system.

**Type:** UInt64

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let data

```cangjie
public let data: ConfigData
```

**Function:** Task value.

**Type:** [ConfigData](#enum-configdata)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let description

```cangjie
public let description: String
```

**Function:** Task description.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**Function:** Additional parts of the task.

**Type:** HashMap\<String,String>

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let faults

```cangjie
public let faults: Faults
```

**Function:** Failure reasons for the task. OTHERS indicates other faults. DISCONNECT indicates network disconnection. TIMEOUT indicates task timeout. PROTOCOL indicates protocol error. FSIO indicates file system I/O error.

**Type:** [Faults](#enum-faults)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let gauge

```cangjie
public let gauge: Bool
```

**Function:** Progress notification policy for background tasks.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let mimeType

```cangjie
public let mimeType: String
```

**Function:** MIME type in task configuration.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let mode

```cangjie
public let mode: Mode
```

**Function:** Specifies task mode. FOREGROUND indicates foreground task. BACKGROUND indicates background task.

**Type:** [Mode](#enum-mode)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let mtime

```cangjie
public let mtime: UInt64
```

**Function:** Unix timestamp (milliseconds) when task status changed, generated by the current device's system.

**Type:** UInt64

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let priority

```cangjie
public let priority: UInt32
```

**Function:** Priority in task configuration. Foreground tasks have higher priority than background tasks. For tasks in the same mode, lower numbers indicate higher priority.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let progress

```cangjie
public let progress: Progress
```

**Function:** Progress of task execution.

**Type:** [Progress](#class-progress)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let reason

```cangjie
public let reason: String
```

**Function:** Reason for waiting/failed/stopped/paused tasks.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let retry

```cangjie
public let retry: Bool
```

**Function:** Retry switch for tasks, only applicable to background tasks.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let saveas

```cangjie
public let saveas: String
```

**Function:** Path to save downloaded files.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let tid

```cangjie
public let tid: String
```

**Function:** Task ID.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let title

```cangjie
public let title: String
```

**Function:** Task title.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let tries

```cangjie
public let tries: UInt32
```

**Function:** Number of attempts for the task.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### let url

```cangjie
public let url: String
```

**Function:** Task URL.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

## enum Action

```cangjie
public enum Action <: Equatable<Action> & ToString {
    | Download
    | Upload
    | ...
}
```

**Function:** Defines operation options.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- Equatable\<Action>
- ToString

### Download

```cangjie
Download
```

**Function:** Indicates a download task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Upload

```cangjie
Upload
```

**Function:** Indicates an upload task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func !=(Action)

```cangjie
public operator func !=(other: Action): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type                   | Required | Default | Description            |
| :-------- | :--------------------- | :------- | :------ | :---------------------- |
| other     | [Action](#enum-action) | Yes      | -       | Another enum value.     |

**Return Value:**

| Type | Description                                      |
| :--- | :----------------------------------------------- |
| Bool | Returns true if enum values differ, else false. |

### func ==(Action)

```cangjie
public operator func ==(other: Action): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type                   | Required | Default | Description            |
| :-------- | :--------------------- | :------- | :------ | :---------------------- |
| other     | [Action](#enum-action) | Yes      | -       | Another enum value.     |

**Return Value:**

| Type | Description                                    |
| :--- | :--------------------------------------------- |
| Bool | Returns true if enum values match, else false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**

| Type   | Description                          |
| :----- | :----------------------------------- |
| String | String representation of the enum.  |## enum BroadcastEvent

```cangjie
public enum BroadcastEvent <: ToString {
    | Complete
    | ...
}
```

**Function:** Defines custom system events. Users can obtain this event through the public event interface. Upload/download SAs with the 'ohos.permission.SEND_TASK_COMPLETE_EVENT' permission can intercept other event senders by configuring the metadata-referenced secondary configuration file. Uses the CommonEventData type to transmit public event-related data. The member content differs from the description in [CommonEventData Introduction](./cj-apis-common_event_manager.md), where CommonEventData.code represents the task status (currently 0x40 COMPLETE or 0x41 FAILED), and CommonEventData.data represents the task's taskId.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- ToString

### Complete

```cangjie
Complete
```

**Function:** Indicates a task completion event.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Return Value:**


| Type   | Description                   |
| :----- | :--------------------- |
| String | String representation of the current enumeration. |

## enum ConfigData

```cangjie
public enum ConfigData {
    | StringValue(String)
    | FormItems(Array<FormItem>)
    | ...
}
```

**Function:** Enumeration type for upload/download task data configuration.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### FormItems(Array\<FormItem>)

```cangjie
FormItems(Array<FormItem>)
```

**Function:** Indicates that during upload, the data is an array of form items Array&lt;FormItem&gt;, empty by default.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** During download, the data is of string type (typically JSON, where objects will be converted to JSON text), empty by default.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

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

**Function:** Subscription event types.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- Equatable\<EventCallbackType>
- Hashable
- ToString

### Completed

```cangjie
Completed
```

**Function:** Indicates a task completion event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Failed

```cangjie
Failed
```

**Function:** Indicates a task failure event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Pause

```cangjie
Pause
```

**Function:** Indicates a task pause event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Progress

```cangjie
Progress
```

**Function:** Indicates a task progress event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Remove

```cangjie
Remove
```

**Function:** Indicates a task removal event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Response

```cangjie
Response
```

**Function:** Indicates a task response reception event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Resume

```cangjie
Resume
```

**Function:** Indicates a task resume event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func !=(EventCallbackType)

```cangjie
public operator func !=(other: EventCallbackType): Bool
```

**Function:** Determines whether two enumeration values are unequal.

**Parameters:**


| Parameter | Type                                         | Required | Default | Description     |
| :----- | :------------------------------------------- | :--- | :----- | :------- |
| other  | [EventCallbackType](#enum-eventcallbacktype) | Yes   | -      | Callback event |

**Return Value:**


| Type | Description                                      |
| :--- | :---------------------------------------- |
| Bool | Returns true if the two enumeration values are unequal, otherwise false. |

### func ==(EventCallbackType)

```cangjie
public operator func ==(other: EventCallbackType): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**


| Parameter | Type                                         | Required | Default | Description     |
| :----- | :------------------------------------------- | :--- | :----- | :------- |
| other  | [EventCallbackType](#enum-eventcallbacktype) | Yes   | -      | Callback event |

**Return Value:**


| Type | Description                                    |
| :--- | :-------------------------------------- |
| Bool | Returns true if the two enumeration values are equal, otherwise false. |

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Gets the hash value of the callback event.

**Return Value:**


| Type  | Description                   |
| :---- | :--------------------- |
| Int64 | Hash value representation of the callback event. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**Return Value:**


| Type   | Description                   |
| :----- | :--------------------- |
| String | String representation of the current enumeration. |

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

**Function:** Defines reasons for task failures.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- ToString

### Disconnected

```cangjie
Disconnected
```

**Function:** Indicates network disconnection.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Fsio

```cangjie
Fsio
```

**Function:** Indicates file system I/O errors, such as open/lookup/read/write/close operations.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Others

```cangjie
Others
```

**Function:** Indicates other faults.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Protocol

```cangjie
Protocol
```

**Function:** Indicates protocol errors, e.g., server internal errors (500), unprocessable data ranges (416), etc.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Timeout

```cangjie
Timeout
```

**Function:** Indicates task timeout.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**Return Value:**


| Type   | Description                   |
| :----- | :--------------------- |
| String | String representation of the current enumeration. |

## enum FormItemValue

```cangjie
public enum FormItemValue {
    | StringItem(String)
    | FileItem(FileSpec)
    | FileItemArray(Array<FileSpec>)
    | ...
}
```

**Function:** Enumeration type for file information in form items.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### FileItem(FileSpec)

```cangjie
FileItem(FileSpec)
```

**Function:** Indicates file information.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### FileItemArray(Array\<FileSpec>)

```cangjie
FileItemArray(Array<FileSpec>)
```

**Function:** Indicates multiple file information entries.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### StringItem(String)

```cangjie
StringItem(String)
```

**Function:** Indicates file path.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22## enum Mode

```cangjie
public enum Mode <: Equatable<Mode> & ToString{
    | Background
    | Foreground
    | ...
}
```

**Function:** Defines mode options. Frontend tasks fail/pause when the app switches to background for a period; background tasks remain unaffected.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- Equatable\<Mode>
- ToString

### Background

```cangjie
Background
```

**Function:** Represents a background task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Foreground

```cangjie
Foreground
```

**Function:** Represents a foreground task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func !=(Mode)

```cangjie
public operator func !=(other: Mode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**


| Parameter | Type               | Required | Default | Description     |
| :-------- | :----------------- | :------- | :------ | :-------------- |
| other     | [Mode](#enum-mode) | Yes      | -       | Mode state      |

**Return Value:**


| Type | Description                                      |
| :--- | :---------------------------------------------- |
| Bool | Returns true if enum values differ, else false. |

### func ==(Mode)

```cangjie
public operator func ==(other: Mode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**


| Parameter | Type               | Required | Default | Description     |
| :-------- | :----------------- | :------- | :------ | :-------------- |
| other     | [Mode](#enum-mode) | Yes      | -       | Mode state      |

**Return Value:**


| Type | Description                                    |
| :--- | :-------------------------------------------- |
| Bool | Returns true if enum values match, else false. |

## enum Network

```cangjie
public enum Network <: Equatable<Network> & ToString {
    | AnyType
    | Wifi
    | Cellular
    | ...
}
```

**Function:** Defines network options. When network conditions are unmet, queued tasks await execution while active tasks fail/pause.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- Equatable\<Network>
- ToString

### AnyType

```cangjie
AnyType
```

**Function:** Represents unrestricted network type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Cellular

```cangjie
Cellular
```

**Function:** Represents cellular data network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Wifi

```cangjie
Wifi
```

**Function:** Represents wireless network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func !=(Network)

```cangjie
public operator func !=(other: Network): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**


| Parameter | Type                     | Required | Default | Description     |
| :-------- | :----------------------- | :------- | :------ | :-------------- |
| other     | [Network](#enum-network) | Yes      | -       | Network state   |

**Return Value:**


| Type | Description                                      |
| :--- | :---------------------------------------------- |
| Bool | Returns true if enum values differ, else false. |

### func ==(Network)

```cangjie
public operator func ==(other: Network): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**


| Parameter | Type                     | Required | Default | Description     |
| :-------- | :----------------------- | :------- | :------ | :-------------- |
| other     | [Network](#enum-network) | Yes      | -       | Network state   |

**Return Value:**


| Type | Description                                    |
| :--- | :-------------------------------------------- |
| Bool | Returns true if enum values match, else false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**


| Type   | Description                       |
| :----- | :------------------------------- |
| String | String representation of the enum. |

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

**Function:** Defines the current state of a task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

**Parent Types:**

- ToString

### Completed

```cangjie
Completed
```

**Function:** Indicates task completion.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Failed

```cangjie
Failed
```

**Function:** Indicates task failure.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Initialized

```cangjie
Initialized
```

**Function:** Creates an initialized task via configuration (Config).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Paused

```cangjie
Paused
```

**Function:** Indicates a paused task, typically to be resumed later.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Removed

```cangjie
Removed
```

**Function:** Indicates task removal.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Retrying

```cangjie
Retrying
```

**Function:** Indicates a task that failed at least once and is currently reprocessing.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Running

```cangjie
Running
```

**Function:** Indicates an actively processing task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Stopped

```cangjie
Stopped
```

**Function:** Indicates task termination.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### Waiting

```cangjie
Waiting
```

**Function:** Indicates a task awaiting execution due to insufficient resources or network state mismatch.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 22

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**


| Type   | Description                       |
| :----- | :------------------------------- |
| String | String representation of the enum. |