# ohos.hiviewdfx.hi_app_event (Application Event Logging)

This module provides capabilities for application event logging, including event persistence, event subscription, event cleanup, and logging configuration.

## Importing the Module

```cangjie
import kit.PerformanceAnalysisKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.

For details about the example projects and configuration templates mentioned above, refer to [Cangjie Sample Code Description](../cj-development-intro.md#cangjie-sample-code-instructions).

## class AppEventFilter

```cangjie
public class AppEventFilter {
    public var domain: String
    public var eventTypes: Array<EventType>
    public var names: Array<String>
    public init(domain: String, eventTypes!: Array<EventType> = [], names!: Array<String> = [])
}
```

**Description:** Provides parameter options for setting subscription filter conditions in Watchers. Used to configure event filtering conditions in event observers, ensuring only events meeting the filter conditions are processed.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var domain

```cangjie
public var domain: String
```

**Description:** The event domain to subscribe to. Can be either system event domains (hiAppEvent.domain.OS) or custom event domains specified in the AppEventInfo when using the Write interface.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var eventTypes

```cangjie
public var eventTypes: Array<EventType>
```

**Description:** The collection of event types to subscribe to.

**Type:** Array\<[EventType](#enum-eventtype)>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var names

```cangjie
public var names: Array<String>
```

**Description:** The collection of event names to subscribe to.

**Type:** Array\<String>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String, Array\<EventType>, Array\<String>)

```cangjie
public init(domain: String, eventTypes!: Array<EventType> = [], names!: Array<String> = [])
```

**Description:** Creates an [AppEventFilter](#class-appeventfilter) instance.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | String | Yes | - | The event domain to subscribe to. |
| eventTypes | Array\<[EventType](#enum-eventtype)> | No | [] | **Named parameter.** The collection of event types to subscribe to. |
| names | Array\<String> | No | [] | **Named parameter.** The collection of event names to subscribe to. |

## class AppEventGroup

```cangjie
public class AppEventGroup {
    public var name: String
    public var appEventInfos: Array<AppEventInfo>
}
```

**Description:** Provides parameter definitions for subscribed event groups.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var appEventInfos

```cangjie
public var appEventInfos: Array<AppEventInfo>
```

**Description:** The collection of event objects.

**Type:** Array\<[AppEventInfo](#class-appeventinfo)>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** The event name.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

## class AppEventInfo

```cangjie
public class AppEventInfo {
    public var domain: String
    public var name: String
    public var eventType: EventType
    public var params: HashMap<String, EventValueType>
    public init(domain: String, name: String, event: EventType, params: HashMap<String, EventValueType>)
}
```

**Description:** Provides parameter options for application event information.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var domain

```cangjie
public var domain: String
```

**Description:** The event domain. Domain names support digits, letters, and underscores, must start with a letter and cannot end with an underscore, with a non-empty length not exceeding 32 characters.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var eventType

```cangjie
public var eventType: EventType
```

**Description:** The event type.

**Type:** [EventType](#enum-eventtype)

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** The event name. The first character must be a letter or $, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter, with a non-empty length not exceeding 48 characters.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var params

```cangjie
public var params: HashMap<String, EventValueType>
```

**Description:** The event parameter object, where each parameter includes a name and value, with specifications as follows:

Parameter names are of String type, must start with a letter or $, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter, with a non-empty length not exceeding 32 characters.

Parameter values support String, Int32, Float64, Bool, and array types. String parameters must be within 8*1024 characters; array parameters must contain elements of only one type (String, Int32, Float64, or Bool), with no more than 100 elements.

The number of parameters must not exceed 32.

**Type:** HashMap\<String,[EventValueType](#enum-eventvaluetype)>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String, String, EventType, HashMap\<String,EventValueType>)

```cangjie
public init(domain: String, name: String, event: EventType, params: HashMap<String, EventValueType>)
```

**Description:** Creates an [AppEventInfo](#class-appeventinfo) instance.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | String | Yes | - | The event domain. Domain names support digits, letters, and underscores, must start with a letter and cannot end with an underscore, with a non-empty length not exceeding 32 characters. |
| name | String | Yes | - | The event name. The first character must be a letter or $, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter, with a non-empty length not exceeding 48 characters. |
| event | [EventType](#enum-eventtype) | Yes | - | The event type. |
| params | HashMap\<String,[EventValueType](#enum-eventvaluetype)> | Yes | - | The event parameter object, where each parameter includes a name and value, with specifications as follows:<br>Parameter names are of String type, must start with a letter or $, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter, with a non-empty length not exceeding 32 characters.<br>Parameter values support String, Int32, Float64, Bool, and array types. String parameters must be within 8*1024 characters; array parameters must contain elements of only one type (String, Int32, Float64, or Bool), with no more than 100 elements.<br>The number of parameters must not exceed 32. |

## class AppEventPackage

```cangjie
public class AppEventPackage {
    public var packageId: Int32
    public var row: Int32
    public var size: Int32
    public var data: Array<String>
}
```

**Description:** Provides parameter definitions for subscribed application event packages.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var data

```cangjie
public var data: Array<String>
```

**Description:** The event information in the package.

**Type:** Array\<String>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var packageId

```cangjie
public var packageId: Int32
```

**Description:** The event package ID, auto-incremented starting from 0.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var row

```cangjie
public var row: Int32
```

**Description:** The number of events in the package.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var size

```cangjie
public var size: Int32
```

**Description:** The size of the event package in bytes.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

## class AppEventPackageHolder

```cangjie
public class AppEventPackageHolder {
    public init(watcherName: String)
}
```

**Description:** A subscription data holder class used for processing subscribed events.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String)

```cangjie
public init(watcherName: String)
```

**Description:** Class constructor that creates a subscription data holder instance, associating it with an existing watcher object added via addWatcher.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| watcherName | String | Yes | - | The name of the watcher added via addWatcher. If not added via addWatcher, no data will be available by default. |

### func setSize(Int32)

```cangjie
public func setSize(size: Int32): Unit
```

**Description:** Sets the data size threshold for each retrieved application event package.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | Int32 | Yes | - | The data size threshold in bytes, must be ≥ 0. Out-of-range values will throw an exception. |

**Exceptions:**

- BusinessException: Error codes as shown below. Refer to [Application Event Logging Error Codes](./cj-errorcode-hiappevent.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11104001 | Invalid size value. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

// Add data watcher "Watcher1" to subscribe to system events
HiAppEvent.addWatcher(Watcher(
    "Watcher1",
    appEventFilters: [
        AppEventFilter(

        )
    ]
))

let holder = AppEventPackageHolder("watcher2")
holder.setSize(100)
```

### func takeNext()

```cangjie
public func takeNext(): Option<AppEventPackage>
```

**Description:** Retrieves subscribed event data based on the set size threshold. Returns None when all subscribed event data has been retrieved.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[AppEventPackage](#class-appeventpackage)> | The retrieved event package object. Returns None when all data has been retrieved. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

let holder = AppEventPackageHolder("watcher3")
if (let Some(v) <- holder.takeNext()) {
    let eventPkg = v
    Hilog.info(0, "AppLogCj", "HiAppEvent packageId=${eventPkg.packageId}")
    Hilog.info(0, "AppLogCj", "HiAppEvent row=${eventPkg.row}")
    Hilog.info(0, "AppLogCj", "HiAppEvent size=${eventPkg.size}")
}
```## class AppEventReportConfig

```cangjie
public class AppEventReportConfig {
    public var domain: String
    public var name: String
    public var isRealTime: Bool
    public init(domain!: String = "", name!: String = "", isRealTime!: Bool = false)
}
```

**Function:** Configuration descriptor for event reporting by data processors.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var domain

```cangjie
public var domain: String
```

**Function:** Event domain. The domain name supports digits, letters, and underscores, must start with a letter and cannot end with an underscore. The length must be non-empty and not exceed 32 characters.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var isRealTime

```cangjie
public var isRealTime: Bool
```

**Function:** Whether to report events in real time. A value of `true` indicates real-time reporting, while `false` indicates non-real-time reporting.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var name

```cangjie
public var name: String
```

**Function:** Event name. The first character must be a letter or `$`, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter. The length must be non-empty and not exceed 48 characters.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String, String, Bool)

```cangjie
public init(domain!: String = "", name!: String = "", isRealTime!: Bool = false)
```

**Function:** Creates an instance of [AppEventReportConfig](#class-appeventreportconfig).

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | String | No | "" | **Named parameter.** Event domain. The domain name supports digits, letters, and underscores, must start with a letter and cannot end with an underscore. The length must be non-empty and not exceed 32 characters. |
| name | String | No | "" | **Named parameter.** Event name. The first character must be a letter or `$`, middle characters must be digits, letters, or underscores, and the last character must be a digit or letter. The length must be non-empty and not exceed 48 characters. |
| isRealTime | Bool | No | false | **Named parameter.** Whether to report events in real time. A value of `true` indicates real-time reporting, while `false` indicates non-real-time reporting. |

## class ConfigOption

```cangjie
public class ConfigOption {
    public var disable: Bool
    public var maxStorage: String
    public init(disable!: Bool = false, maxStorage!: String = "10M")
}
```

**Function:** Provides configuration options for application event logging.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var disable

```cangjie
public var disable: Bool
```

**Function:** Event logging switch, default is `false`. `true`: Disables event logging, `false`: Enables event logging.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var maxStorage

```cangjie
public var maxStorage: String
```

**Function:** Quota size for the directory storing event logging data, default is "10M".

When the directory size exceeds the quota, the next logging operation will trigger a cleanup: deleting event data files from oldest to newest until the directory size no longer exceeds the quota.

Quota string specifications:

- The quota string consists of digits and size units (supported units: [b|k|kb|m|mb|g|gb|t|tb], case-insensitive).
- The quota string must start with a digit, followed by an optional unit character (default unit is byte if omitted).

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(Bool, String)

```cangjie
public init(disable!: Bool = false, maxStorage!: String = "10M")
```

**Function:** Creates an instance of [ConfigOption](#class-configoption).

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| disable | Bool | No | false | Event logging switch |
| maxStorage | String | No | "10M" | Quota size for the directory storing event logging data |

## class Domain

```cangjie
public class Domain {
    public static const OS = "OS"
}
```

**Function:** Provides predefined event domain name constants.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const OS

```cangjie
public static const OS = "OS"
```

**Function:** System domain.

**Type:** String

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

## class Event

```cangjie
public class Event {
    public static const USER_LOGIN = "hiappevent.user_login"
    public static const USER_LOGOUT = "hiappevent.user_logout"
    public static const DISTRIBUTED_SERVICE_START = "hiappevent.distributed_service_start"
    public static const APP_CRASH = "APP_CRASH"
    public static const APP_FREEZE = "APP_FREEZE"
}
```

**Function:** Provides predefined event name constants.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const APP_CRASH

```cangjie
public static const APP_CRASH = "APP_CRASH"
```

**Function:** Application crash event.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const APP_FREEZE

```cangjie
public static const APP_FREEZE = "APP_FREEZE"
```

**Function:** Application freeze event.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const DISTRIBUTED_SERVICE_START

```cangjie
public static const DISTRIBUTED_SERVICE_START = "hiappevent.distributed_service_start"
```

**Function:** Distributed service startup event.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const USER_LOGIN

```cangjie
public static const USER_LOGIN = "hiappevent.user_login"
```

**Function:** User login event.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const USER_LOGOUT

```cangjie
public static const USER_LOGOUT = "hiappevent.user_logout"
```

**Function:** User logout event.

**Type:** String

**Read/Write:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

## class HiAppEvent

```cangjie
public class HiAppEvent {}
```

**Function:** This class provides application event logging capabilities.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static func addProcessor(Processor)

```cangjie
public static func addProcessor(processor: Processor): Int64
```

**Function:** Developers can add data processors to enable event cloud reporting. The implementation of data processors can be pre-installed on devices. Developers can set properties based on the constraints of the data processors.

Processor configuration information must be provided by the data processor. Currently, no pre-installed interactive data processors are available on devices, so cloud reporting functionality is currently unavailable.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| processor | [Processor](#class-processor) | Yes | - | Data processor for event reporting. |

**Returns:**

| Type | Description |
|:----|:----|
| Int64 | ID of the added event reporting data processor. Returns -1 on failure, or a value greater than 0 on success. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

var processor : Processor = Processor("test_processor")
let processorId = HiAppEvent.addProcessor(processor)
Hilog.info(0, "AppLogCj", "HiAppEvent::processorId is ${processorId}.")
```

### static func addWatcher(Watcher)

```cangjie
public static func addWatcher(watcher: Watcher): Option<AppEventPackageHolder>
```

**Function:** Adds an application event watcher for subscribing to application events.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| watcher | [Watcher](#class-watcher) | Yes | - | Application event watcher. |

**Returns:**

| Type | Description |
|:----|:----|
| Option\<[AppEventPackageHolder](#class-appeventpackage)> | Holder for subscribed data. Returns `None` on subscription failure. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Application Event Logging Error Codes](./cj-errorcode-hiappevent.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11102001 | Invalid watcher name. |
  | 11102002 | Invalid filtering event domain. |
  | 11102003 | Invalid row value. |
  | 11102004 | Invalid size value. |
  | 11102005 | Invalid timeout value. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

func f1(){
    // If the watcher includes callback parameters, the automatically triggered callback function can be used to process subscribed events
    var condition = TriggerCondition(row: 1)
    var appEventFilter = [AppEventFilter("button")]
    var watcher = Watcher("watcher1", triggerCondition: condition,
        onTrigger:  Some({ row, size, holder =>
            Hilog.info(0, "AppLogCj", "HiAppEvent onTrigger: curRow=${row}, curSize=${size}")
            while (let Some(v) <- holder.takeNext()) {
                let eventPkg = v
                Hilog.info(0, "AppLogCj", "HiAppEvent packageId=${eventPkg.packageId}")
                Hilog.info(0, "AppLogCj", "HiAppEvent row=${eventPkg.row}")
                Hilog.info(0, "AppLogCj", "HiAppEvent size=${eventPkg.size}")
                for (i in 0..eventPkg.data.size) {
                    Hilog.info(0, "AppLogCj", "HiAppEvent info=${eventPkg.data[i]}")
                }
             }
     }))
     HiAppEvent.addWatcher(watcher)
}

func f2(){
    // If the watcher does not include callback parameters, the returned holder object can be used to manually process subscribed events
    let watcher =  Watcher("watcher2")
    let holder = HiAppEvent.addWatcher(watcher)
    if (let Some(v1) <- holder) {
       while (let Some(v2) <- v1.takeNext()) {
            let eventPkg = v2
            Hilog.info(0, "test_hiAppEvent_addWatcher", "HiAppEvent packageId=${eventPkg.packageId}")
            Hilog.info(0, "test_hiAppEvent_addWatcher", "HiAppEvent row=${eventPkg.row}")
            Hilog.info(0, "test_hiAppEvent_addWatcher", "HiAppEvent size=${eventPkg.size}")
            for (i in 0..eventPkg.data.size) {
                Hilog.info(0, "test_hiAppEvent_addWatcher", "HiAppEvent info=${eventPkg.data[i]}")
            }
        }
     }
}

func f3(){
    // The watcher can process subscribed events in the real-time callback function onReceive
    var condition = TriggerCondition(row: 1, size: 100)
    let watcher= Watcher("watcher", triggerCondition: condition,
             onTrigger: {row, size, holder =>
                Hilog.info(0, "AppLogCj", "HiAppEvent onTrigger: curRow=${row}, curSize=${size}"},
             onReceive: {domain, AppEventGroups =>
                Hilog.info(0, "AppLogCj", "domain =${domain}")
                let groupSize = AppEventGroups.size
                for (i in 0..groupSize) {
                    Hilog.info(0, "AppLogCj", "name =${AppEventGroups[i].name}")
                    let appInfosize = AppEventGroups[i].appEventInfos.size
                    for (j in 0..appInfosize) {
                        Hilog.info(0, "AppLogCj", "appEventInfo name=${AppEventGroups[i].appEventInfos[j].name}")
                        Hilog.info(0, "AppLogCj", "appEventInfo domain=${AppEventGroups[i].appEventInfos[j].domain}")
                        Hilog.info(0, "AppLogCj", "appEventInfo event=${AppEventGroups[i].appEventInfos[j].eventType.getValue()}", "")
                        let paSize = AppEventGroups[i].appEventInfos[j].params.size
                        for ((k, v) in AppEventGroups[i].appEventInfos[j].params) {
                            Hilog.info(0x0000, "HiAppEnvent", "key=${k}", "")
                            Hilog.info(0x0000, "HiAppEnvent", "value=${v.toString()}", "")
                        }
                    }
                }
            })
    HiAppEvent.addWatcher(watcher)
}

func test() {
    f1()
    f2()
    f3()
}
```### static func clearData()

```cangjie
public static func clearData(): Unit
```

**Function:** Clears the locally stored application event tracking data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import std.collection.ArrayList
import std.collection.Map

let params = HashMap<String, EventValueType>()
params.add("cangjie", IntValue(1001))
params.add("cangjie2", StringValue("1001"))
var appInfo: AppEventInfo = AppEventInfo("cangjie1", "test_event", EventType.Fault, params)
HiAppEvent.write(appInfo)
HiAppEvent.clearData()
```

### static func configure(ConfigOption)

```cangjie
public static func configure(config: ConfigOption): Unit
```

**Function:** Configures application event tracking, including enabling/disabling tracking and setting storage quota size.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| config | [ConfigOption](#class-configoption) | Yes | - | Configuration object for application event tracking. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

var config : ConfigOption = ConfigOption(maxStorage: "100M", disable: true)
HiAppEvent.configure(config)
Hilog.info(0, "AppLogCj", "HiAppEvent::configure.")
```

### static func getUserId(String)

```cangjie
public static func getUserId(name: String): String
```

**Function:** Retrieves the value previously set via the [setUserId](#static-func-setuseridstring-string) interface.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Key for the user ID. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The value of the user ID. Returns an empty string if not found. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

HiAppEvent.setUserId("test_getUserId_name", "test_getUserId_value")
let userIdName = HiAppEvent.getUserId("test_getUserId_name")
Hilog.info(0, "AppLogCj", "HiAppEvent::test_getUserId is ${userIdName}.")
```

### static func getUserProperty(String)

```cangjie
public static func getUserProperty(name: String): String
```

**Function:** Retrieves the value previously set via the [setUserProperty](#static-func-setuserpropertystring-string) interface.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Key for the user property. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The value of the user property. Returns an empty string if not found. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

HiAppEvent.setUserProperty("test_setUserProperty_name", "test_setUserProperty_value")
let propertyName = HiAppEvent.getUserProperty("test_getUserProperty_name")
Hilog.info(0, "AppLogCj", "HiAppEvent::test_getUserProperty is ${propertyName}.")
```

### static func removeProcessor(Int64)

```cangjie
public static func removeProcessor(id: Int64): Unit
```

**Function:** Removes an event data processor.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | Int64 | Yes | - | ID of the event data processor. Must be greater than 0. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

var processor : Processor = Processor("test_processor")
let processorId = HiAppEvent.addProcessor(processor)
HiAppEvent.removeProcessor(processorId)
Hilog.info(0, "AppLogCj", "HiAppEvent::removeProcessor test over.")
```

### static func removeWatcher(Watcher)

```cangjie
public static func removeWatcher(watcher: Watcher): Unit
```

**Function:** Removes an application event watcher to unsubscribe from events.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| watcher | [Watcher](#class-watcher) | Yes | - | The application event watcher. |

**Exceptions:**

- BusinessException: Error codes as follows, see [Application Event Error Codes](./cj-errorcode-hiappevent.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11102001 | Invalid watcher name. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

// Define an application event watcher
let watcher= Watcher("watcher1")
// Add the watcher to subscribe to events
HiAppEvent.addWatcher(watcher)
// Remove the watcher to unsubscribe from events
HiAppEvent.removeWatcher(watcher)
```

### static func setUserId(String, String)

```cangjie
public static func setUserId(name: String, value: String): Unit
```

**Function:** Sets a user ID.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Key for the user ID. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters. |
| value | String | Yes | - | Value for the user ID. Must not exceed 256 characters. If the value is null or an empty string, the user ID is cleared. |

### static func setUserProperty(String, String)

```cangjie
public static func setUserProperty(name: String, value: String): Unit
```

**Function:** Sets a user property.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Key for the user property. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters. |
| value | String | Yes | - | Value for the user property. Must not exceed 1024 characters. If the value is null or an empty string, the user property is cleared. |

### static func write(AppEventInfo)

```cangjie
public static func write(info: AppEventInfo): Unit
```

**Function:** Writes an event to the daily event file, accepting an [AppEventInfo](#class-appeventinfo) object.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| info | [AppEventInfo](#class-appeventinfo) | Yes | - | The application event object. |

## class Param

```cangjie
public class Param {
    public static const USER_ID = "user_id"
    public static const DISTRIBUTED_SERVICE_NAME = "ds_name"
    public static const DISTRIBUTED_SERVICE_INSTANCE_ID = "ds_instance_id"
}
```

**Function:** Provides constants for predefined parameter names.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const DISTRIBUTED_SERVICE_INSTANCE_ID

```cangjie
public static const DISTRIBUTED_SERVICE_INSTANCE_ID = "ds_instance_id"
```

**Function:** Distributed service instance ID.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const DISTRIBUTED_SERVICE_NAME

```cangjie
public static const DISTRIBUTED_SERVICE_NAME = "ds_name"
```

**Function:** Distributed service name.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### static const USER_ID

```cangjie
public static const USER_ID = "user_id"
```

**Function:** Custom user ID.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

## class Processor

```cangjie
public class Processor {
    public var name: String
    public var debugMode: Bool
    public var routeInfo: String
    public var appId: String
    public var onStartReport: Bool
    public var onBackgroundReport: Bool
    public var periodReport: Int32
    public var batchReport: Int32
    public var userIds: Array<String>
    public var userProperties: Array<String>
    public var eventConfigs: Array<AppEventReportConfig>
    public init(name: String, debugMode!: Bool = false, routeInfo!: String = "", appId!: String = "",
        onStartReport!: Bool = false, onBackgroundReport!: Bool = false, periodReport!: Int32 = 0,
        batchReport!: Int32 = 0, userIds!: Array<String> = [], userProperties!: Array<String> = [],
        eventConfigs!: Array<AppEventReportConfig> = [])
}
```

**Function:** Represents an event data processor that can report events.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var appId

```cangjie
public var appId: String
```

**Function:** Application ID, defaults to an empty string. If the input exceeds 8KB, it will be reset to the default value.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var batchReport

```cangjie
public var batchReport: Int32
```

**Function:** Threshold for event reporting. Events are reported when the count reaches this threshold. Must be greater than 0 and less than 1000. Invalid values will be reset to 0, disabling reporting.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var debugMode

```cangjie
public var debugMode: Bool
```

**Function:** Enables or disables debug mode, defaulting to false. True enables debug mode, false disables it.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var eventConfigs

```cangjie
public var eventConfigs: Array<AppEventReportConfig>
```

**Function:** Array of events that the processor can report.

**Type:** Array\<[AppEventReportConfig](#class-appeventreportconfig)>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var name

```cangjie
public var name: String
```

**Function:** Name of the processor. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var onBackgroundReport

```cangjie
public var onBackgroundReport: Bool
```

**Function:** Determines whether to report events when the application enters the background, defaulting to false. True enables reporting, false disables it.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var onStartReport

```cangjie
public var onStartReport: Bool
```

**Function:** Determines whether to report events when the processor starts, defaulting to false. True enables reporting, false disables it.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var periodReport

```cangjie
public var periodReport: Int32
```

**Function:** Periodic event reporting interval in seconds. Must be greater than or equal to 0. Negative values will be reset to 0, disabling periodic reporting.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var routeInfo

```cangjie
public var routeInfo: String
```

**Function:** Server location information, defaults to an empty string. If the input exceeds 8KB, it will be reset to the default value.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var userIds

```cangjie
public var userIds: Array<String>
```

**Function:** Array of user ID names that the processor can report. Corresponds to the name parameter in [setUserId](#static-func-setuseridstring-string).

**Type:** Array\<String>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var userProperties

```cangjie
public var userProperties: Array<String>
```

**Function:** Array of user property names that the processor can report. Corresponds to the name parameter in [setUserProperty](#static-func-setuserpropertystring-string).

**Type:** Array\<String>

**Access:** Read-write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String, Bool, String, String, Bool, Bool, Int32, Int32, Array\<String>, Array\<String>, Array\<AppEventReportConfig>)

```cangjie
public init(name: String, debugMode!: Bool = false, routeInfo!: String = "", appId!: String = "",
    onStartReport!: Bool = false, onBackgroundReport!: Bool = false, periodReport!: Int32 = 0,
    batchReport!: Int32 = 0, userIds!: Array<String> = [], userProperties!: Array<String> = [],
    eventConfigs!: Array<AppEventReportConfig> = [])
```

**Function:** Creates a [Processor](#class-processor) instance.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the processor. Can only contain letters, numbers, underscores, and $, cannot start with a number, and must not exceed 256 characters. |
| debugMode | Bool | No | false | **Named parameter.** Enables or disables debug mode, defaulting to false. True enables debug mode, false disables it. |
| routeInfo | String | No | "" | **Named parameter.** Server location information, defaults to an empty string. If the input exceeds 8KB, it will be reset to the default value. |
| appId | String | No | "" | **Named parameter.** Application ID, defaults to an empty string. If the input exceeds 8KB, it will be reset to the default value. |
| onStartReport | Bool | No | false | **Named parameter.** Determines whether to report events when the processor starts, defaulting to false. True enables reporting, false disables it. |
| onBackgroundReport | Bool | No | false | **Named parameter.** Determines whether to report events when the application enters the background, defaulting to false. True enables reporting, false disables it. |
| periodReport | Int32 | No | 0 | **Named parameter.** Periodic event reporting interval in seconds. Must be greater than or equal to 0. Negative values will be reset to 0, disabling periodic reporting. |
| batchReport | Int32 | No | 0 | **Named parameter.** Threshold for event reporting. Events are reported when the count reaches this threshold. Must be greater than 0 and less than 1000. Invalid values will be reset to 0, disabling reporting. |
| userIds | Array\<String> | No | [] | **Named parameter.** Array of user ID names that the processor can report. Corresponds to the name parameter in [setUserId](#static-func-setuseridstring-string). |
| userProperties | Array\<String> | No | [] | **Named parameter.** Array of user property names that the processor can report. Corresponds to the name parameter in [setUserProperty](#static-func-setuserpropertystring-string). |
| eventConfigs | Array\<[AppEventReportConfig](#class-appeventreport## class TriggerCondition

```cangjie
public class TriggerCondition {
    public var row: Int32
    public var size: Int32
    public var timeOut: Int32
    public init(row!: Int32 = 0, size!: Int32 = 0, timeOut!: Int32 = 0)
}
```

**Function:** Provides parameter options for callback trigger conditions. The subscription callback will be triggered when any condition is met.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var row

```cangjie
public var row: Int32
```

**Function:** The total number of events required to trigger the callback, a positive integer. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var size

```cangjie
public var size: Int32
```

**Function:** The total size of events required to trigger the callback, a positive integer, in bytes. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var timeOut

```cangjie
public var timeOut: Int32
```

**Function:** The timeout duration required to trigger the callback, a positive integer, in units of 30 seconds. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(Int32, Int32, Int32)

```cangjie
public init(row!: Int32 = 0, size!: Int32 = 0, timeOut!: Int32 = 0)
```

**Function:** Creates a [TriggerCondition](#class-triggercondition) instance.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| row | Int32 | No | 0 | **Named parameter.** The total number of events required to trigger the callback, a positive integer. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value. |
| size | Int32 | No | 0 | **Named parameter.** The total size of events required to trigger the callback, a positive integer, in bytes. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value. |
| timeOut | Int32 | No | 0 | **Named parameter.** The timeout duration required to trigger the callback, a positive integer, in units of 30 seconds. Default value is 0, which means no callback will be triggered. Negative values will be reset to the default value. |

## class Watcher

```cangjie
public class Watcher {
    public var name: String
    public var triggerCondition: TriggerCondition
    public var appEventFilters: Array<AppEventFilter>
    public var onTrigger: Option <(Int32, Int32, AppEventPackageHolder) -> Unit>
    public var onReceive: Option <(String, Array<AppEventGroup>) -> Unit>
    public init(name: String, triggerCondition!: TriggerCondition = TriggerCondition(),
        appEventFilters!: Array<AppEventFilter> = [],
        onTrigger!: Option<(Int32, Int32, AppEventPackageHolder) -> Unit> = None,
        onReceive!: Option<(String, Array<AppEventGroup>) -> Unit> = None)
}
```

**Function:** Provides parameter options for application event watchers.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var appEventFilters

```cangjie
public var appEventFilters: Array<AppEventFilter>
```

**Function:** Subscription filter conditions, used when filtering subscribed events is required.

**Type:** Array\<[AppEventFilter](#class-appeventfilter)>

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var name

```cangjie
public var name: String
```

**Function:** Watcher name, used to uniquely identify the watcher.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var onReceive

```cangjie
public var onReceive: Option <(String, Array<AppEventGroup>) -> Unit>
```

**Function:** Real-time subscription callback function. If both this callback and the `onTrigger` callback exist, only this callback will be triggered. The first parameter of the callback function represents the domain name of the callback event, and the second parameter represents the collection of callback events.

**Type:** [AppEventGroup](#class-appeventgroup)->Unit

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var onTrigger

```cangjie
public var onTrigger: Option <(Int32, Int32, AppEventPackageHolder) -> Unit>
```

**Function:** Subscription callback function, which takes effect only when used together with the callback trigger condition `triggerCondition`. The first parameter of the callback function represents the total number of subscribed events when the callback is triggered. The second parameter represents the total size of subscribed events when the callback is triggered, in bytes. The third parameter represents the subscription data holder object, which can be used to process subscribed events.

**Type:** (Int32,Int32,[AppEventPackageHolder](#class-appeventpackageholder))->Unit

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### var triggerCondition

```cangjie
public var triggerCondition: TriggerCondition
```

**Function:** Subscription callback trigger condition, which takes effect only when used together with the callback function `onTrigger`.

**Type:** [TriggerCondition](#class-triggercondition)

**Access:** Read-Write

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### init(String, TriggerCondition, Array\<AppEventFilter>, Option\<(Int32,Int32,AppEventPackageHolder) -> Unit>, Option\<(String,Array\<AppEventGroup>) -> Unit>)

```cangjie
public init(name: String, triggerCondition!: TriggerCondition = TriggerCondition(),
    appEventFilters!: Array<AppEventFilter> = [],
    onTrigger!: Option<(Int32, Int32, AppEventPackageHolder) -> Unit> = None,
    onReceive!: Option<(String, Array<AppEventGroup>) -> Unit> = None)
```

**Function:** Creates a [Watcher](#class-watcher) instance.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Watcher name, used to uniquely identify the watcher. |
| triggerCondition | [TriggerCondition](#class-triggercondition) | No | TriggerCondition() | **Named parameter.** Subscription callback trigger condition, which takes effect only when used together with the callback function `onTrigger`. |
| appEventFilters | Array\<[AppEventFilter](#class-appeventfilter)> | No | [] | **Named parameter.** Subscription filter conditions, used when filtering subscribed events is required. |
| onTrigger | Option\<(Int32,Int32,[AppEventPackageHolder](#class-appeventpackageholder))->Unit> | No | None | **Named parameter.** Subscription callback function, which takes effect only when used together with the callback trigger condition `triggerCondition`. Function parameters are as follows: <br>curRow: Total number of subscribed events when the callback is triggered; <br>curSize: Total size of subscribed events when the callback is triggered, in bytes;<br/>holder: Subscription data holder object, which can be used to process subscribed events. |
| onReceive | Option\<(String,Array\<[AppEventGroup](#class-appeventgroup)>)->Unit> | No | None | **Named parameter.** Real-time subscription callback function. If both this callback and the `onTrigger` callback exist, only this callback will be triggered. Function parameters are as follows: <br>domain: Domain name of the callback event; <br>appEventGroups: Collection of callback events. |

## enum EventType

```cangjie
public enum EventType {
    | Fault
    | Statistic
    | Security
    | Behavior
    | ...
}
```

**Function:** Event type enumeration.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### Behavior

```cangjie
Behavior
```

**Function:** Behavior type event.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### Fault

```cangjie
Fault
```

**Function:** Fault type event.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### Security

```cangjie
Security
```

**Function:** Security type event.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### Statistic

```cangjie
Statistic
```

**Function:** Statistical type event.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### func getValue()

```cangjie
public func getValue(): UInt32
```

**Function:** Gets the value of the enumeration.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Gets the value of the enumeration. |

## enum EventValueType

```cangjie
public enum EventValueType <: ToString {
    | IntValue(Int32)
    | FloatValue(Float64)
    | StringValue(String)
    | BoolValue(Bool)
    | ArrString(Array<String>)
    | ArrInt32(Array<Int32>)
    | ArrBool(Array<Bool>)
    | ArrFloat64(Array<Float64>)
    | Int64Value(Int64)
    | ArrInt64(Array<Int64>)
    | ...
}
```

**Function:** Event parameter value data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Parent Type:**

- ToString

### ArrBool(Array\<Bool>)

```cangjie
ArrBool(Array<Bool>)
```

**Function:** Bool type array data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### ArrFloat64(Array\<Float64>)

```cangjie
ArrFloat64(Array<Float64>)
```

**Function:** Float64 type array data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### ArrInt32(Array\<Int32>)

```cangjie
ArrInt32(Array<Int32>)
```

**Function:** Int32 type array data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### ArrInt64(Array\<Int64>)

```cangjie
ArrInt64(Array<Int64>)
```

**Function:** Int64 type array data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### ArrString(Array\<String>)

```cangjie
ArrString(Array<String>)
```

**Function:** String array data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**Function:** Boolean type data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### FloatValue(Float64)

```cangjie
FloatValue(Float64)
```

**Function:** Float64 type data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**Function:** Int64 type data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### IntValue(Int32)

```cangjie
IntValue(Int32)
```

**Function:** Int32 type data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### StringValue(String)

```cangjie
StringValue(String)
```

**Function:** String type data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the data.

**System Capability:** SystemCapability.HiviewDFX.HiAppEvent

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the data.|