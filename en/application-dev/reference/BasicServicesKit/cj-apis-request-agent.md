# ohos.request

The request component primarily provides applications with fundamental capabilities for uploading/downloading files and background transfer proxy.

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Permission List

ohos.permission.INTERNET

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#仓颉示例代码说明).

## func create(UIAbilityContext, Config)

```cangjie
public func create(context: UIAbilityContext, config: Config): Task
```

**Function:** Creates a task to be uploaded or downloaded and enqueues it. Each application supports a maximum of 10 unfinished tasks.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application-based context. |
| config | [Config](#class-config) | Yes | - | Configuration information for upload/download tasks. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Task](#class-task) | Returns a Task object containing the task ID and configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. 3. Parameter verification failed. |
  | 13400001 | Invalid file or file system error. |
  | 13400003 | Task service ability error. |
  | 21900004 | The application task queue is full. |
  | 21900005 | Operation with wrong task mode. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

## func getTask(UIAbilityContext, String, ?String)

```cangjie
public func getTask(context: UIAbilityContext, id: String, token!: ?String = None): Task
```

**Function:** Queries a task by its ID.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application-based context. |
| id | String | Yes | - | Task ID. |
| token | ?String | No | None | **Named parameter.** Task query token. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Task](#class-task) | Returns a Task object containing the task ID and configuration information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. 3. Parameter verification failed. |
  | 13400003 | Task service ability error. |
  | 21900006 | Task removed or not found. |

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | todo | todo |

## func remove(String)

```cangjie
public func remove(id: String): Unit
```

**Function:** Removes a specified task belonging to the caller. If the task is in progress, it will be forcibly stopped.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Task ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error. |
  | 21900006 | Task removed or not found. |

## func search(Filter)

```cangjie
public func search(filter!: Filter = Filter()): Array<String>
```

**Function:** Searches for task IDs based on default [Filter](#class-filter) conditions.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| filter | [Filter](#class-filter) | No | Filter() | Filter conditions. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns task IDs that meet the conditions. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error. |

## func show(String)

```cangjie
public func show(id: String): TaskInfo
```

**Function:** Queries detailed information of a task by its ID.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Task ID. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TaskInfo](#class-taskinfo) | Returns a TaskInfo object containing detailed task information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error. |
  | 21900006 | Task removed or not found. |

## func touch(String, String)

```cangjie
public func touch(id: String, token: String): TaskInfo
```

**Function:** Queries detailed information of a task by its ID and token.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | Task ID. |
| token | String | Yes | - | Task query token. |

**Return Value:**

| Type | Description |
|:----|:----|
| [TaskInfo](#class-taskinfo) | Returns a TaskInfo object containing detailed task information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. Refer to [Upload/Download Error Codes](./cj-errorcode-request.md) and [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Missing mandatory parameters. 2. Incorrect parameter type. |
  | 13400003 | Task service ability error. |
  | 21900006 | Task removed or not found. |

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

**Function:** Configuration information for upload/download tasks.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var action

```cangjie
public var action: Action
```

**Function:** Task operation option. UPLOAD indicates an upload task, DOWNLOAD indicates a download task.

**Type:** [Action](#enum-action)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var begins

```cangjie
public var begins: Int64
```

**Function:** File starting point, typically used for resumable transfers. Default value is 0 (inclusive). For downloads, it specifies the starting position when requesting to read the server file (setting the "Range" option in HTTP protocol). For uploads, it is read at upload start.

**Type:** Int64

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var data

```cangjie
public var data:?ConfigData
```

**Function:** For downloads, data is of string type (typically JSON, where objects will be converted to JSON text), default is empty. For uploads, data is an array of form items Array\<FormItem>, default is empty.

**Type:** ?[ConfigData](#enum-configdata)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var description

```cangjie
public var description: String
```

**Function:** Detailed information about the task, with a maximum length of 1024 characters. Default is an empty string.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var ends

```cangjie
public var ends: Int64
```

**Function:** File ending point, typically used for resumable transfers. Default value is -1 (inclusive). For downloads, it specifies the ending position when requesting to read the server file (setting the "Range" option in HTTP protocol). For uploads, it is read at upload completion.

**Type:** Int64

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**Function:** Additional features of the configuration. Default is empty.

**Type:** HashMap\<String,String>

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21

### var gauge

```cangjie
public var gauge: Bool
```

**Function:** Progress notification strategy for background tasks, applicable only to background tasks. Default is false. false: Only completion or failure notifications. true: Notifications for each progress completion or failure.

**Type:** Bool

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since Version:** 21### var headers

```cangjie
public var headers: HashMap<String, String>
```

**Function:** Adds HTTP protocol headers to be included in the task. For upload requests, the default Content-Type is "multipart/form-data". For download requests, the default Content-Type is "application/json".

**Type:** HashMap

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var index

```cangjie
public var index: UInt32
```

**Function:** The path index of the task, typically used for task resumption. Default is 0.

**Type:** UInt32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var metered

```cangjie
public var metered: Bool
```

**Function:** Whether to allow operation in metered networks. Default is false.  
- true: Yes  
- false: No  

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var method

```cangjie
public var method:?String
```

**Function:** The HTTP standard method for upload or download, including GET, POST, and PUT (case-insensitive).  
- For uploads: Use PUT or POST, default is PUT.  
- For downloads: Use GET or POST, default is GET.  

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var mode

```cangjie
public var mode: Mode
```

**Function:** Task mode, default is background task.

**Type:** [Mode](#enum-mode)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var network

```cangjie
public var network: Network
```

**Function:** Network options, currently supporting WIFI and CELLULAR. Default is ANY (WIFI or CELLULAR).

**Type:** [Network](#enum-network)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var overwrite

```cangjie
public var overwrite: Bool
```

**Function:** Solution for existing paths during download. Default is false.  
- true: Overwrite existing files.  
- false: Download fails.  

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var precise

```cangjie
public var precise: Bool
```

**Function:** If set to true, the task fails when file size cannot be obtained during upload/download. If set to false, the task continues with file size set to -1. Default is false.

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var priority

```cangjie
public var priority: UInt32
```

**Function:** Task priority. For tasks with the same mode, a lower number indicates higher priority. Default is 0.

**Type:** UInt32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var redirect

```cangjie
public var redirect: Bool
```

**Function:** Whether to allow redirection. Default is true.  
- true: Yes  
- false: No  

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var retry

```cangjie
public var retry: Bool
```

**Function:** Whether to enable automatic retry for background tasks (applies only to background tasks). Default is true.  
- true: Yes  
- false: No  

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var roaming

```cangjie
public var roaming: Bool
```

**Function:** Whether to allow operation in roaming networks. Default is true.  
- true: Yes  
- false: No  

**Type:** Bool

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var saveas

```cangjie
public var saveas:String
```

**Function:** Path to save downloaded files, including:  
- Relative path: Located under the caller's cache path, e.g., "./xxx/yyy/zzz.html", "xxx/yyy/zzz.html".  
- Internal protocol path: Only supports "internal://cache/" and its subpaths, e.g., "internal://cache/path/to/file.txt".  
- Application sandbox directory: Only supports base and its subdirectories, e.g., "/data/storage/el1/base/path/to/file.txt".  
- File protocol path: Must match the application package name, only supports base and its subdirectories, e.g., "file://com.example.test/data/storage/el2/base/file.txt".  
Default is a relative path, i.e., downloaded to the caller's current cache path.

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var title

```cangjie
public var title:?String
```

**Function:** Task title, with a maximum length of 256 characters. Default is lowercase "upload" or "download", matching the action above.

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var token

```cangjie
public var token: ?String
```

**Function:** When a task is created with a token, the token must be provided during normal queries; otherwise, retrieval via query will fail. Minimum length is 8 bytes, maximum is 2048 bytes. Default is empty.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var url

```cangjie
public var url: String
```

**Function:** Resource address, with a maximum length of 2048 characters.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### init(Action, String, ?String, String, Mode, Bool, ?String, HashMap\<String,String>, ?ConfigData, String, Network, Bool, Bool, Bool, Bool, UInt32, Int64, Int64, Bool, Bool, ?String, UInt32, HashMap\<String,String>)

```cangjie

public init(action: Action, url: String, title!: ?String = None, description!: String = "",
    mode!: Mode = Mode.Background, overwrite!: Bool = false, method!: ?String = None,
    headers!: HashMap<String, String> = HashMap<String, String>(), data!: ?ConfigData = None, saveas!: ?String = None,
    network!: Network = Network.AnyType, metered!: Bool = false, roaming!: Bool = true, retry!: Bool = true,
    redirect!: Bool = true, index!: UInt32 = 0, begins!: Int64 = 0, ends!: Int64 = -1, gauge!: Bool = false,
    precise!: Bool = false, token!: String = "", priority!: UInt32 = 0,extras!: HashMap<String, String> = HashMap<String, String>()
)
```

**Function:** Creates a Config object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| action | [Action](#enum-action) | Yes | - | **Named parameter.** Task operation option.<br>- UPLOAD: Upload task.<br>- DOWNLOAD: Download task. |
| url | String | Yes | - | **Named parameter.** Resource address, max length 2048 characters. |
| title | ?String | No | None | **Named parameter.** Task title, max length 256 characters. Default is lowercase "upload" or "download", matching the action. |
| description | String | No | "" | **Named parameter.** Task details, max length 1024 characters. Default is empty string. |
| mode | [Mode](#enum-mode) | No | Mode.Background | **Named parameter.** Task mode, default is background task. |
| overwrite | Bool | No | false | **Named parameter.** Solution for existing paths during download.<br>- true: Overwrite existing files.<br>- false: Download fails. |
| method | ?String | No | None | **Named parameter.** HTTP standard method for upload/download (GET, POST, PUT, case-insensitive).<br>- Upload: PUT or POST, default is PUT.<br>- Download: GET or POST, default is GET. |
| headers | HashMap\<String,String> | No | HashMap<String,String>() | **Named parameter.** HTTP headers to include in the task.<br>- Upload: Default Content-Type is "multipart/form-data".<br>- Download: Default Content-Type is "application/json". |
| data | ?[ConfigData](#enum-configdata) | No | None | **Named parameter.**<br>- Download: data is string type (typically JSON; objects are converted to JSON text). Default is empty.<br>- Upload: data is an array of form items Array&lt;FormItem&gt;. Default is empty. |
| saveas | ?String | No | None | **Named parameter.** Path to save downloaded files, including:<br>- Relative path: Under caller's cache path, e.g., "./xxx/yyy/zzz.html".<br>- Internal path: Only "internal://cache/" and subpaths, e.g., "internal://cache/path/to/file.txt".<br>- Sandbox path: Only base and subdirectories, e.g., "/data/storage/el1/base/path/to/file.txt".<br>- File path: Must match package name, e.g., "file://com.example.test/data/storage/el2/base/file.txt".<br>Default is relative path (caller's cache path). |
| network | [Network](#enum-network) | No | Network.AnyType | **Named parameter.** Network options (WIFI or CELLULAR). Default is ANY (WIFI or CELLULAR). |
| metered | Bool | No | false | **Named parameter.** Allow operation in metered networks.<br>- true: Yes<br>- false: No |
| roaming | Bool | No | true | **Named parameter.** Allow operation in roaming networks.<br>- true: Yes<br>- false: No |
| retry | Bool | No | true | **Named parameter.** Enable auto-retry for background tasks.<br>- true: Yes<br>- false: No |
| redirect | Bool | No | true | **Named parameter.** Allow redirection.<br>- true: Yes<br>- false: No |
| index | UInt32 | No | 0 | **Named parameter.** Task path index (for resumption). Default is 0. |
| begins | Int64 | No | 0 | **Named parameter.** File start point (for resumption). Default is 0 (inclusive).<br>- Download: HTTP "Range" header start position.<br>- Upload: Read at upload start. |
| ends | Int64 | No | -1 | **Named parameter.** File end point (for resumption). Default is -1 (inclusive).<br>- Download: HTTP "Range" header end position.<br>- Upload: Read at upload end. |
| gauge | Bool | No | false | **Named parameter.** Background task progress notification policy.<br>- false: Only completion/failure notifications.<br>- true: Notify for every progress update. |
| precise | Bool | No | false | **Named parameter.**<br>- true: Task fails if file size cannot be obtained.<br>- false: Task continues with size -1. |
| token | String | No | "" | **Named parameter.** Required for querying tasks created with a token. Min 8 bytes, max 2048 bytes. Default is empty. |
| priority | UInt32 | No | 0 | **Named parameter.** Task priority (lower number = higher priority). Default is 0. |
| extras | HashMap\<String,String> | No | HashMap\<String, String>() | **Named parameter.** Additional configuration. Default is empty. |

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

**Function:** File information for form items.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var extras

```cangjie
public var extras: HashMap<String, String>
```

**Function:** Additional file information.

**Type:** HashMap\<String,String>

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var filename

```cangjie
public var filename:?String
```

**Function:** Filename, default is derived from the path.

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var mimeType

```cangjie
public var mimeType:?String
```

**Function:** File MIME type, derived from the filename.

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var path

```cangjie
public var path: String
```

**Function:** File path: Relative path under the caller's cache folder or public user files (e.g., "file://media/Photo/path/to/file.img"). Only supports foreground tasks.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

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

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| path | String | Yes | - | **Named parameter.** File path:<br>- Relative path under caller's cache folder.<br>- Public user files (e.g., "file://media/Photo/path/to/file.img"). Only supports foreground tasks. |
| mimeType | ?String | No | None | **Named parameter.** File MIME type, derived from filename. |
| filename | ?String | No | None | **Named parameter.** Filename, default is derived from path. |
| extras | HashMap\<String,String> | No | HashMap<String,String>() | **Named parameter.** Additional file information. |## class Filter

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

**Since:** 21

### var action

```cangjie
public var action:?Action
```

**Function:** Task operation options. UPLOAD indicates upload tasks. DOWNLOAD indicates download tasks.

**Type:** ?[Action](#enum-action)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var after

```cangjie
public var after:?Int64
```

**Function:** Start Unix timestamp (milliseconds), default value is the current time minus 24 hours.

**Type:** ?Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var before

```cangjie
public var before:?Int64
```

**Function:** End Unix timestamp (milliseconds), default value is the current time.

**Type:** ?Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var mode

```cangjie
public var mode:?Mode
```

**Function:** Task mode. FOREGROUND indicates foreground tasks. BACKGROUND indicates background tasks. If not specified, all tasks will be queried.

**Type:** ?[Mode](#enum-mode)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var state

```cangjie
public var state:?State
```

**Function:** Specifies the state of the task.

**Type:** ?[State](#enum-state)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### init(?Int64, ?Int64, ?State, ?Action, ?Mode)

```cangjie

public init(before!: ?Int64 = None, after!: ?Int64 = None, state!: ?State = None,
    action!: ?Action = None, mode!: ?Mode = None
)
```

**Function:** Creates a Filter object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| before | ?Int64 | No | None | **Named parameter.** End Unix timestamp (milliseconds), default value is the current time. |
| after | ?Int64 | No | None | **Named parameter.** Start Unix timestamp (milliseconds), default value is the current time minus 24 hours. |
| state | ?[State](#enum-state) | No | None | **Named parameter.** Specifies the state of the task. |
| action | ?[Action](#enum-action) | No | None | **Named parameter.** Task operation options.<br>- UPLOAD indicates upload tasks.<br>- DOWNLOAD indicates download tasks. |
| mode | ?[Mode](#enum-mode) | No | None | **Named parameter.** Task mode.<br>- FOREGROUND indicates foreground tasks.<br>- BACKGROUND indicates background tasks.<br>- If not specified, all tasks will be queried. |

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

**Since:** 21

### var name

```cangjie
public var name: String
```

**Function:** Form parameter name.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var value

```cangjie
public var value: FormItemValue
```

**Function:** Form parameter value.

**Type:** [FormItemValue](#enum-formitemvalue)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### init(String, FormItemValue)

```cangjie

public init(name: String, value: FormItemValue)
```

**Function:** Creates a FormItem object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | **Named parameter.** Form parameter name. |
| value | [FormItemValue](#enum-formitemvalue) | Yes | - | **Named parameter.** Form parameter value. |

## class HttpResponse

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

**Since:** 21

### let headers

```cangjie
public let headers: HashMap<String, Array<String>>
```

**Function:** HTTP response headers.

**Type:** HashMap\<String,Array\<String>>

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let reason

```cangjie
public let reason: String
```

**Function:** HTTP response reason.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let statusCode

```cangjie
public let statusCode: Int32
```

**Function:** HTTP response status code.

**Type:** Int32

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let version

```cangjie
public let version: String
```

**Function:** HTTP version.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

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

**Since:** 21

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**Function:** Additional content for interaction, such as headers and body from the server's response.

**Type:** HashMap\<String,String>

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let index

```cangjie
public let index: UInt32
```

**Function:** Index of the currently processed file in the task.

**Type:** UInt32

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let processed

```cangjie
public let processed: Int64
```

**Function:** Size of processed data for the current file in the task, in bytes.

**Type:** Int64

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let sizes

```cangjie
public let sizes: Array<Int64>
```

**Function:** Sizes of files in the task, in bytes.

**Type:** Array\<Int64>

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let state

```cangjie
public let state: State
```

**Function:** Current state of the task.

**Type:** [State](#enum-state)

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

## class Task

```cangjie
public class Task {
    public let tid: String
    public var config: Config

    public init(tid: String, config: Config)
}
```

**Function:** Upload or download task. Before using this method, you need to obtain a Task object via create.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### var config

```cangjie
public var config: Config
```

**Function:** Configuration information for the task.

**Type:** [Config](#class-config)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let tid

```cangjie
public let tid: String
```

**Function:** Task ID, which is unique in the system and automatically generated by the system.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### init(String, Config)

```cangjie

public init(tid: String, config: Config)
```

**Function:** Creates a Task object.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| tid | String | Yes | - | Task ID, which is unique in the system and automatically generated by the system. |
| config | [Config](#class-config) | Yes | - | Configuration information for the task. |

### func off(EventCallbackType, ?CallbackObject)

```cangjie

public func off(event: EventCallbackType, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from task events.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [EventCallbackType](#enum-eventcallbacktype) | Yes | - | Event type to unsubscribe from.<br>- 'progress' indicates task progress.<br>- 'completed' indicates task completion.<br>- 'failed' indicates task failure.<br>- 'pause' indicates task pause.<br>- 'resume' indicates task resume.<br>- 'remove' indicates task removal.<br>- 'response' indicates task response. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** Callback function to unsubscribe. If this parameter is not specified, all callback functions of the current type will be unsubscribed. |

### func on(EventCallbackType, Callback1Argument\<HttpResponse>)

```cangjie

public func on(event: EventCallbackType, callback: Callback1Argument<HttpResponse>): Unit
```

**Function:** Subscribes to task response headers.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [EventCallbackType](#enum-eventcallbacktype) | Yes | - | Event type to subscribe to.<br>- 'response' indicates task response. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HttpResponse> | Yes | - | Callback method triggered when the related event occurs, returning the data structure of the task response headers. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Common Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter verification failed. |

### func on(EventCallbackType, Callback1Argument\<Progress>)

```cangjie

public func on(event: EventCallbackType, callback: Callback1Argument<Progress>): Unit
```

**Function:** Subscribes to task events.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [EventCallbackType](#enum-eventcallbacktype) | Yes | - | Event type to subscribe to.<br>- 'progress' indicates task progress.<br>- 'completed' indicates task completion.<br>- 'failed' indicates task failure.<br>- 'pause' indicates task pause.<br>- 'resume' indicates task resume.<br>- 'remove' indicates task removal. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[Progress](#class-progress)> | Yes | - | Callback method triggered when the related event occurs, returning the data structure of the task information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter verification failed. |

### func pause()

```cangjie

public func pause(): Unit
```

**Function:** Pauses the task. Can pause background tasks that are waiting/running/retrying.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13400003 | Task service ability error. |
  | 21900005 | Operation with wrong task mode. |
  | 21900007 | Operation with wrong task state. |

### func resume()

```cangjie

public func resume(): Unit
```

**Function:** Restarts the task. Can resume paused background tasks.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 13400003 | Task service ability error. |
  | 21900005 | Operation with wrong task mode. |
  | 21900007 | Operation with wrong task state. |

### func start()

```cangjie

public func start(): Unit
```

**Function:** Starts the task. Cannot start an already initialized task. Can start a failed or stopped download task, resuming from the last progress.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 13400003 | Task service ability error. |
  | 21900007 | Operation with wrong task state. |

### func stop()

```cangjie

public func stop(): Unit
```

**Function:** Stops the task. Can stop tasks that are running/waiting/retrying.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Upload/Download Error Codes](./cj-errorcode-request.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 13400003 | Task service ability error. |
  | 21900007 | Operation with wrong task state. |## class TaskInfo

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

**Since:** 21

### let action

```cangjie
public let action: Action
```

**Function:** Task operation option. UPLOAD indicates upload task. DOWNLOAD indicates download task.

**Type:** [Action](#enum-action)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let ctime

```cangjie
public let ctime: UInt64
```

**Function:** Unix timestamp (milliseconds) when the task was created, generated by the current device's system.

**Type:** UInt64

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let data

```cangjie
public let data: ConfigData
```

**Function:** Task value.

**Type:** [ConfigData](#enum-configdata)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let description

```cangjie
public let description: String
```

**Function:** Task description.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let extras

```cangjie
public let extras: HashMap<String, String>
```

**Function:** Additional parts of the task.

**Type:** HashMap\<String,String>

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let faults

```cangjie
public let faults: Faults
```

**Function:** Failure reasons for the task. OTHERS indicates other faults. DISCONNECT indicates network disconnection. TIMEOUT indicates task timeout. PROTOCOL indicates protocol error. FSIO indicates file system I/O error.

**Type:** [Faults](#enum-faults)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let gauge

```cangjie
public let gauge: Bool
```

**Function:** Progress notification policy for background tasks.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let mimeType

```cangjie
public let mimeType: String
```

**Function:** MIME type in task configuration.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let mode

```cangjie
public let mode: Mode
```

**Function:** Specifies task mode. FOREGROUND indicates foreground task. BACKGROUND indicates background task.

**Type:** [Mode](#enum-mode)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let mtime

```cangjie
public let mtime: UInt64
```

**Function:** Unix timestamp (milliseconds) when task status changed, generated by the current device's system.

**Type:** UInt64

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let priority

```cangjie
public let priority: UInt32
```

**Function:** Priority in task configuration. Foreground tasks have higher priority than background tasks. For tasks in the same mode, smaller numbers indicate higher priority.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let progress

```cangjie
public let progress: Progress
```

**Function:** Progress status of the task.

**Type:** [Progress](#class-progress)

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let reason

```cangjie
public let reason: String
```

**Function:** Reason for waiting/failed/stopped/paused tasks.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let retry

```cangjie
public let retry: Bool
```

**Function:** Retry switch for tasks, only applicable to background tasks.

**Type:** Bool

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let saveas

```cangjie
public let saveas: String
```

**Function:** Path to save downloaded files.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let tid

```cangjie
public let tid: String
```

**Function:** Task ID.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let title

```cangjie
public let title: String
```

**Function:** Task title.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let tries

```cangjie
public let tries: UInt32
```

**Function:** Number of attempts for the task.

**Type:** UInt32

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### let url

```cangjie
public let url: String
```

**Function:** URL of the task.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

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

**Since:** 21

**Parent Types:**

- Equatable\<Action>
- ToString

### Download

```cangjie
Download
```

**Function:** Indicates download task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Upload

```cangjie
Upload
```

**Function:** Indicates upload task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func !=(Action)

```cangjie
public operator func !=(other: Action): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Action](#enum-action)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise returns false.|

### func ==(Action)

```cangjie
public operator func ==(other: Action): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Action](#enum-action)|Yes|-|Another enum value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enum.|## enum BroadcastEvent

```cangjie
public enum BroadcastEvent <: ToString {
    | Complete
    | ...
}
```

**Function:** Defines custom system events. Users can obtain these events through the public event interface. Upload/download SAs with the 'ohos.permission.SEND_TASK_COMPLETE_EVENT' permission can intercept event senders by configuring the metadata-referenced secondary configuration file. Common event data is transmitted using the CommonEventData type. The content filling of members differs from the [CommonEventData introduction](./cj-apis-common_event_manager.md), where CommonEventData.code represents task status (currently 0x40 COMPLETE or 0x41 FAILED), and CommonEventData.data represents the task's taskId.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parent Types:**

- ToString

### Complete

```cangjie
Complete
```

**Function:** Indicates a task completion event.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enumeration.|

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

**Since:** 21

### FormItems(Array\<FormItem>)

```cangjie
FormItems(Array<FormItem>)
```

**Function:** Indicates that during upload, data is an array of form items Array&lt;FormItem&gt;, empty by default.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** During download, data is of string type (typically JSON, with objects converted to JSON text), empty by default.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### Failed

```cangjie
Failed
```

**Function:** Indicates a task failure event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Pause

```cangjie
Pause
```

**Function:** Indicates a task pause event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Progress

```cangjie
Progress
```

**Function:** Indicates a task progress event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Remove

```cangjie
Remove
```

**Function:** Indicates a task removal event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Response

```cangjie
Response
```

**Function:** Indicates a task response reception event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Resume

```cangjie
Resume
```

**Function:** Indicates a task resume event type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func !=(EventCallbackType)

```cangjie
public operator func !=(other: EventCallbackType): Bool
```

**Function:** Determines whether two enumeration values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[EventCallbackType](#enum-eventcallbacktype)|Yes|-|Callback event|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if unequal, otherwise false.|

### func ==(EventCallbackType)

```cangjie
public operator func ==(other: EventCallbackType): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[EventCallbackType](#enum-eventcallbacktype)|Yes|-|Callback event|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if equal, otherwise false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Gets the hash value of the callback event.

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|Hash value representation of the callback event.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enumeration.|

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

**Since:** 21

**Parent Types:**

- ToString

### Disconnected

```cangjie
Disconnected
```

**Function:** Indicates network disconnection.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Fsio

```cangjie
Fsio
```

**Function:** Indicates file system I/O errors (e.g., open/lookup/read/write/close operations).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Others

```cangjie
Others
```

**Function:** Indicates other faults.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Protocol

```cangjie
Protocol
```

**Function:** Indicates protocol errors (e.g., server internal error 500, unprocessable data range 416).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Timeout

```cangjie
Timeout
```

**Function:** Indicates task timeout.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enumeration.|

## enum FormItemValue

```cangjie
public enum FormItemValue {
    | StringItem(String)
    | FileItem(FileSpec)
    | FileItemArray(Array<FileSpec>)
    | ...
}
```

**Function:** Enumeration type for form item file information.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### FileItem(FileSpec)

```cangjie
FileItem(FileSpec)
```

**Function:** Indicates file information.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### FileItemArray(Array\<FileSpec>)

```cangjie
FileItemArray(Array<FileSpec>)
```

**Function:** Indicates multiple file information entries.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### StringItem(String)

```cangjie
StringItem(String)
```

**Function:** Indicates file path.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21## enum Mode

```cangjie
public enum Mode <: Equatable<Mode> & ToString{
    | Background
    | Foreground
    | ...
}
```

**Function:** Defines mode options. Frontend tasks fail/pause when the app switches to background for a period; background tasks remain unaffected.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parent Types:**

- Equatable\<Mode>
- ToString

### Background

```cangjie
Background
```

**Function:** Represents a background task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Foreground

```cangjie
Foreground
```

**Function:** Represents a foreground task.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func !=(Mode)

```cangjie
public operator func !=(other: Mode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Mode](#enum-mode)|Yes|-|Mode status|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise false.|

### func ==(Mode)

```cangjie
public operator func ==(other: Mode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Mode](#enum-mode)|Yes|-|Mode status|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string representation of the current enum.|

## enum Network

```cangjie
public enum Network <: Equatable<Network> & ToString {
    | AnyType
    | Wifi
    | Cellular
    | ...
}
```

**Function:** Defines network options. When network conditions don't meet the settings, pending tasks wait for execution while executing tasks fail/pause.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

**Parent Types:**

- Equatable\<Network>
- ToString

### AnyType

```cangjie
AnyType
```

**Function:** Represents unrestricted network type.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Cellular

```cangjie
Cellular
```

**Function:** Represents cellular data network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Wifi

```cangjie
Wifi
```

**Function:** Represents wireless network.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func !=(Network)

```cangjie
public operator func !=(other: Network): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Network](#enum-network)|Yes|-|Network status|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are unequal, otherwise false.|

### func ==(Network)

```cangjie
public operator func ==(other: Network): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[Network](#enum-network)|Yes|-|Network status|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string representation of the current enum.|

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

**Since:** 21

**Parent Types:**

- ToString

### Completed

```cangjie
Completed
```

**Function:** Indicates task completion.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Failed

```cangjie
Failed
```

**Function:** Indicates task failure.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Initialized

```cangjie
Initialized
```

**Function:** Creates an initialized task through configuration information (Config).

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Paused

```cangjie
Paused
```

**Function:** Indicates task pause, typically followed by task resumption.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Removed

```cangjie
Removed
```

**Function:** Indicates task removal.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Retrying

```cangjie
Retrying
```

**Function:** Indicates the task has failed at least once and is currently being reprocessed.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Running

```cangjie
Running
```

**Function:** Indicates a task being processed.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Stopped

```cangjie
Stopped
```

**Function:** Indicates task stoppage.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### Waiting

```cangjie
Waiting
```

**Function:** Indicates the task lacks execution resources or the network status doesn't match.

**System Capability:** SystemCapability.Request.FileTransferAgent

**Since:** 21

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enum.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string representation of the current enum.|