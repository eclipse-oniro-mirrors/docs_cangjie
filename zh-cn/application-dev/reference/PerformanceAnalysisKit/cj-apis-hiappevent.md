# ohos.hiviewdfx.hi_app_event（应用事件打点）

本模块提供了应用事件打点能力，包括应用事件落盘、应用事件订阅、应用事件清理、打点功能配置等功能。

## 导入模块

```cangjie
import kit.PerformanceAnalysisKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class AppEventFilter

```cangjie
public class AppEventFilter {
    public var domain: String
    public var eventTypes: Array<EventType>
    public var names: Array<String>
    public init(domain: String, eventTypes!: Array<EventType> = [], names!: Array<String> = [])
}
```

**功能：** 提供设置Watcher的订阅过滤条件的参数选项。用于在事件观察者中设置事件过滤条件，确保只有满足过滤条件的事件才会被监听处理。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var domain

```cangjie
public var domain: String
```

**功能：** 需要订阅的事件领域。可以是系统事件领域（hiAppEvent.domain.OS）或开发者在使用Write接口时传入的自定义事件信息（AppEventInfo）中的事件领域。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var eventTypes

```cangjie
public var eventTypes: Array<EventType>
```

**功能：** 需要订阅的事件类型集合。

**类型：** Array\<[EventType](#enum-eventtype)>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var names

```cangjie
public var names: Array<String>
```

**功能：** 需要订阅的事件名称集合。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String, Array\<EventType>, Array\<String>)

```cangjie
public init(domain: String, eventTypes!: Array<EventType> = [], names!: Array<String> = [])
```

**功能：** 创建[AppEventFilter](#class-appeventfilter)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|domain|String|是|-|需要订阅的事件领域。|
|eventTypes|Array\<[EventType](#enum-eventtype)>|否|[]|**命名参数。** 需要订阅的事件类型集合。|
|names|Array\<String>|否|[]|**命名参数。** 需要订阅的事件名称集合。|

## class AppEventGroup

```cangjie
public class AppEventGroup {
    public var name: String
    public var appEventInfos: Array<AppEventInfo>
}
```

**功能：** 提供了订阅返回的事件组的参数定义。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var appEventInfos

```cangjie
public var appEventInfos: Array<AppEventInfo>
```

**功能：** 事件对象集合。

**类型：** Array\<[AppEventInfo](#class-appeventinfo)>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 事件名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

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

**功能：** 提供了应用事件信息的参数选项。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var domain

```cangjie
public var domain: String
```

**功能：** 事件领域。事件领域名称支持数字、字母、下划线字符，需要以字母开头且不能以下划线结尾，长度非空且不超过32个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var eventType

```cangjie
public var eventType: EventType
```

**功能：** 事件类型。

**类型：** [EventType](#enum-eventtype)

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 事件名称。首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过48个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var params

```cangjie
public var params: HashMap<String, EventValueType>
```

**功能：** 事件参数对象，每个事件参数包括参数名和参数值，其规格定义如下：

参数名为String类型，首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过32个字符。

参数值支持String、Int32、Float64、Bool、数组类型，String类型参数长度需在8*1024个字符以内；数组类型参数中的元素类型只能全为String、Int32、Float64、Bool中的一种，且元素个数需在100以内。

参数个数需在32个以内。

**类型：** HashMap\<String,[EventValueType](#enum-eventvaluetype)>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String, String, EventType, HashMap\<String,EventValueType>)

```cangjie
public init(domain: String, name: String, event: EventType, params: HashMap<String, EventValueType>)
```

**功能：** 创建[AppEventInfo](#class-appeventinfo)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|domain|String|是|-|事件领域。事件领域名称支持数字、字母、下划线字符，需要以字母开头且不能以下划线结尾，长度非空且不超过32个字符。|
|name|String|是|-|事件名称。首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过48个字符。|
|event|[EventType](#enum-eventtype)|是|-|事件类型。|
|params|HashMap\<String,[EventValueType](#enum-eventvaluetype)>|是|-|事件参数对象，每个事件参数包括参数名和参数值，其规格定义如下：<br>参数名为String类型，首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过32个字符。<br>参数值支持String、Int32、Float64、Bool、数组类型，String类型参数长度需在8*1024个字符以内；数组类型参数中的元素类型只能全为String、Int32、Float64、Bool中的一种，且元素个数需在100以内。<br>参数个数需在32个以内。|

## class AppEventPackage

```cangjie
public class AppEventPackage {
    public var packageId: Int32
    public var row: Int32
    public var size: Int32
    public var data: Array<String>
}
```

**功能：** 提供了订阅返回的应用事件包的参数定义。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var data

```cangjie
public var data: Array<String>
```

**功能：** 事件包的事件信息。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var packageId

```cangjie
public var packageId: Int32
```

**功能：** 事件包ID，从0开始自动递增。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var row

```cangjie
public var row: Int32
```

**功能：** 事件包的事件数量。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var size

```cangjie
public var size: Int32
```

**功能：** 事件包的事件大小，单位为byte。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

## class AppEventPackageHolder

```cangjie
public class AppEventPackageHolder {
    public init(watcherName: String)
}
```

**功能：** 订阅数据持有者类，用于对订阅事件进行处理。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String)

```cangjie
public init(watcherName: String)
```

**功能：** 类构造函数，创建订阅数据持有者实例，通过addWatcher添加事件观察者关联到应用内已添加的观察者对象。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|watcherName|String|是|-|已通过addWatcher添加的事件观察者名称。若未通过addWatcher添加，则默认无数据。|

### func setSize(Int32)

```cangjie
public func setSize(size: Int32): Unit
```

**功能：** 设置每次取出的应用事件包的数据大小阈值。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|size|Int32|是|-|数据大小阈值，单位为byte，取值范围大于等于0，超出范围会抛异常。|

**异常：**

- BusinessException：对应错误码如下表，详见[应用事件打点错误码](./cj-errorcode-hiappevent.md)和[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11104001 | Invalid size value. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

// 添加数据观察者“Watcher1”，订阅监听系统事件
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

**功能：** 根据设置的数据大小阈值来取出订阅事件数据，当订阅事件数据全部被取出时返回None作为标识。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Option\<[AppEventPackage](#class-appeventpackage)>|取出的事件包对象，订阅事件数据被全部取出后会返回None。|

**示例：**

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
```

## class AppEventReportConfig

```cangjie
public class AppEventReportConfig {
    public var domain: String
    public var name: String
    public var isRealTime: Bool
    public init(domain!: String = "", name!: String = "", isRealTime!: Bool = false)
}
```

**功能：** 数据处理者可以上报事件的描述配置。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var domain

```cangjie
public var domain: String
```

**功能：** 事件领域。事件领域名称支持数字、字母、下划线字符，需要以字母开头且不能以下划线结尾，长度非空且不超过32个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var isRealTime

```cangjie
public var isRealTime: Bool
```

**功能：** 是否实时上报事件。配置值为true表示实时上报事件，false表示不实时上报事件。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 事件名称。首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过48个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String, String, Bool)

```cangjie
public init(domain!: String = "", name!: String = "", isRealTime!: Bool = false)
```

**功能：** 创建[AppEventReportConfig](#class-appeventreportconfig)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|domain|String|否|""|**命名参数。** 事件领域。事件领域名称支持数字、字母、下划线字符，需要以字母开头且不能以下划线结尾，长度非空且不超过32个字符。|
|name|String|否|""|**命名参数。** 事件名称。首字符必须为字母字符或$字符，中间字符必须为数字字符、字母字符或下划线字符，结尾字符必须为数字字符或字母字符，长度非空且不超过48个字符。|
|isRealTime|Bool|否|false|**命名参数。** 是否实时上报事件。配置值为true表示实时上报事件，false表示不实时上报事件。|

## class ConfigOption

```cangjie
public class ConfigOption {
    public var disable: Bool
    public var maxStorage: String
    public init(disable!: Bool = false, maxStorage!: String = "10M")
}
```

**功能：** 提供了对应用事件打点功能的配置选项。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var disable

```cangjie
public var disable: Bool
```

**功能：** 打点功能开关，默认值为false。true：关闭打点功能，false：不关闭打点功能。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var maxStorage

```cangjie
public var maxStorage: String
```

**功能：** 打点数据存放目录的配额大小，默认值为“10M”。

在目录大小超出配额后，下次打点会触发对目录的清理操作：按从旧到新的顺序逐个删除打点数据文件，直到目录大小不超出配额时结束。

配额值字符串规格如下：

- 配额值字符串只由数字字符和大小单位字符（单位字符支持[b\|k\|kb\|m\|mb\|g\|gb\|t\|tb]，不区分大小写）构成。
- 配额值字符串必须以数字开头，后面可以选择不传单位字符（默认使用byte作为单位），或者以单位字符结尾。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(Bool, String)

```cangjie
public init(disable!: Bool = false, maxStorage!: String = "10M")
```

**功能：** 创建[ConfigOption](#class-configoption)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|disable|Bool|否|false|打点功能开关|
|maxStorage|String|否|"10M"|打点数据存放目录的配额大小|

## class Domain

```cangjie
public class Domain {
    public static const OS = "OS"
}
```

**功能：** 提供了所有预定义事件的领域名称常量。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const OS

```cangjie
public static const OS = "OS"
```

**功能：** 系统领域。

**类型：** String

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

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

**功能：** 提供了所有预定义事件的事件名称常量。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const APP_CRASH

```cangjie
public static const APP_CRASH = "APP_CRASH"
```

**功能：** 应用崩溃事件。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const APP_FREEZE

```cangjie
public static const APP_FREEZE = "APP_FREEZE"
```

**功能：** 应用卡死事件。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const DISTRIBUTED_SERVICE_START

```cangjie
public static const DISTRIBUTED_SERVICE_START = "hiappevent.distributed_service_start"
```

**功能：** 分布式服务启动事件。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const USER_LOGIN

```cangjie
public static const USER_LOGIN = "hiappevent.user_login"
```

**功能：** 用户登录事件。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const USER_LOGOUT

```cangjie
public static const USER_LOGOUT = "hiappevent.user_logout"
```

**功能：** 用户登出事件。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

## class HiAppEvent

```cangjie
public class HiAppEvent {}
```

**功能：** 该类提供了应用事件打点能力。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static func addProcessor(Processor)

```cangjie
public static func addProcessor(processor: Processor): Int64
```

**功能：** 开发者可添加数据处理者，该数据处理者用于提供事件上云功能，数据处理者的实现可预置在设备中，开发者可根据数据处理者的约束设置属性。

Processor的配置信息需要由数据处理者提供，目前设备内暂未预置可供交互的数据处理者，因此当前事件上云功能不可用。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|processor|[Processor](#class-processor)|是|-|上报事件的数据处理者。|

**返回值：**

|类型|说明|
|:----|:----|
|Int64|所添加上报事件数据处理者的ID。添加失败返回-1，添加成功返回大于0的值。|

**示例：**

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

**功能：** 添加应用事件观察者方法，可用于订阅应用事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|watcher|[Watcher](#class-watcher)|是|-|应用事件观察者。|

**返回值：**

|类型|说明|
|:----|:----|
|Option\<[AppEventPackageHolder](#class-appeventpackage)>|订阅数据持有者，订阅失败时返回None。|

**异常：**

- BusinessException：对应错误码如下表，详见[应用事件打点错误码](./cj-errorcode-hiappevent.md)和[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11102001 | Invalid watcher name. |
  | 11102002 | Invalid filtering event domain. |
  | 11102003 | Invalid row value. |
  | 11102004 | Invalid size value. |
  | 11102005 | Invalid timeout value. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import kit.PerformanceAnalysisKit.Hilog

func f1(){
    // 如果观察者传入了回调的相关参数，则可以选择在自动触发的回调函数中对订阅事件进行处理
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
    // 如果观察者未传入回调的相关参数，则可以选择使用返回的holder对象手动去处理订阅事件
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
    // 观察者可以在实时回调函数onReceive中处理订阅事件
    var condition = TriggerCondition(row: 1, size: 100)
    let watcher= Watcher("watcher", triggerCondition: condition,
             onTrigger: {row, size, holder =>
                Hilog.info(0, "AppLogCj", "HiAppEvent onTrigger: curRow=${row}, curSize=${size}")},
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
```

### static func clearData()

```cangjie
public static func clearData(): Unit
```

**功能：** 应用事件打点数据清理方法，将应用存储在本地的打点数据进行清除。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**示例：**

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

**功能：** 应用事件打点配置方法，可用于配置打点开关、目录存储配额大小等功能。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|config|[ConfigOption](#class-configoption)|是|-|应用事件打点配置项对象。|

**示例：**

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

**功能：** 获取之前通过[setUserId](#static-func-setuseridstring-string)接口设置的value值。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|用户ID的key。只能包含大小写字母、数字、下划线和$，不能以数字开头，长度不超过256。|

**返回值：**

|类型|说明|
|:----|:----|
|String|用户ID的值。没有查到返回空字符串。|

**示例：**

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

**功能：** 获取之前通过[setUserProperty](#static-func-setuserpropertystring-string)接口设置的value值。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|用户属性的key。只能包含大小写字母、数字、下划线和$，不能以数字开头，长度不超过256。|

**返回值：**

|类型|说明|
|:----|:----|
|String|用户属性的值。没有查到返回空字符串。|

**示例：**

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

**功能：** 删除上报事件的数据处理者。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|id|Int64|是|-|上报事件数据处理者ID。值大于0。|

**示例：**

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

**功能：** 移除应用事件观察者方法，可用于取消订阅应用事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|watcher|[Watcher](#class-watcher)|是|-|应用事件观察者。|

**异常：**

- BusinessException：对应错误码如下表，详见[应用事件打点错误码](./cj-errorcode-hiappevent.md)和[通用错误码](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 11102001 | Invalid watcher name. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*

// 定义一个应用事件观察者
let watcher= Watcher("watcher1")
// 添加一个应用事件观察者来订阅事件
HiAppEvent.addWatcher(watcher)
// 移除该应用事件观察者以取消订阅事件
HiAppEvent.removeWatcher(watcher)
```

### static func setUserId(String, String)

```cangjie
public static func setUserId(name: String, value: String): Unit
```

**功能：** 设置用户ID。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|用户ID的key。只能包含大小写字母、数字、下划线和$，不能以数字开头，长度非空且不超过256个字符。|
|value|String|是|-|用户ID的值。长度不超过256，当值为null或空字符串时，则清除用户ID。|

### static func setUserProperty(String, String)

```cangjie
public static func setUserProperty(name: String, value: String): Unit
```

**功能：** 设置用户属性。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|用户属性的key。只能包含大小写字母、数字、下划线和$，不能以数字开头，长度非空且不超过256个字符。|
|value|String|是|-|用户属性的值。长度不超过1024，当值为null或空字符串时，则清除用户属性。|

### static func write(AppEventInfo)

```cangjie
public static func write(info: AppEventInfo): Unit
```

**功能：** 应用事件打点方法，将事件写入到当天的事件文件中，可接收[AppEventInfo](#class-appeventinfo)类型的事件对象。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|info|[AppEventInfo](#class-appeventinfo)|是|-|应用事件对象。|

## class Param

```cangjie
public class Param {
    public static const USER_ID = "user_id"
    public static const DISTRIBUTED_SERVICE_NAME = "ds_name"
    public static const DISTRIBUTED_SERVICE_INSTANCE_ID = "ds_instance_id"
}
```

**功能：** 提供了所有预定义参数的参数名称常量。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const DISTRIBUTED_SERVICE_INSTANCE_ID

```cangjie
public static const DISTRIBUTED_SERVICE_INSTANCE_ID = "ds_instance_id"
```

**功能：** 分布式服务实例ID。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const DISTRIBUTED_SERVICE_NAME

```cangjie
public static const DISTRIBUTED_SERVICE_NAME = "ds_name"
```

**功能：** 分布式服务名称。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### static const USER_ID

```cangjie
public static const USER_ID = "user_id"
```

**功能：** 用户自定义ID。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

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

**功能：** 可以上报事件的数据处理者对象。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var appId

```cangjie
public var appId: String
```

**功能：** 应用id，默认为空字符串。传入字符串长度不能超过8KB，超过时会被置为默认值。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var batchReport

```cangjie
public var batchReport: Int32
```

**功能：** 事件上报阈值，当事件条数达到阈值时上报事件。传入数值必须大于0且小于1000，不在数值范围内会被置为默认值0，不进行上报。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var debugMode

```cangjie
public var debugMode: Bool
```

**功能：** 是否开启debug模式，默认值为false。配置值为true表示开启debug模式，false表示不开启debug模式。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var eventConfigs

```cangjie
public var eventConfigs: Array<AppEventReportConfig>
```

**功能：** 数据处理者可以上报的事件数组。

**类型：** Array\<[AppEventReportConfig](#class-appeventreportconfig)>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 数据处理者的名称。名称只能包含大小写字母、数字、下划线和$，不能以数字开头，长度非空且不超过256个字符。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var onBackgroundReport

```cangjie
public var onBackgroundReport: Bool
```

**功能：** 当应用程序进入后台时是否上报事件，默认值为false。配置值为true表示上报事件，false表示不上报事件。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var onStartReport

```cangjie
public var onStartReport: Bool
```

**功能：** 数据处理者在启动时是否上报事件，默认值为false。配置值为true表示上报事件，false表示不上报事件。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var periodReport

```cangjie
public var periodReport: Int32
```

**功能：** 事件定时上报时间周期，单位为秒。传入数值必须大于或等于0，小于0时会被置为默认值0，不进行定时上报。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var routeInfo

```cangjie
public var routeInfo: String
```

**功能：** 服务器位置信息，默认为空字符串。传入字符串长度不能超过8KB，超过时会被置为默认值。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var userIds

```cangjie
public var userIds: Array<String>
```

**功能：** 数据处理者可以上报的用户ID的name数组。name对应[setUserId](#static-func-setuseridstring-string)接口的name参数。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var userProperties

```cangjie
public var userProperties: Array<String>
```

**功能：** 数据处理者可以上报的用户属性的name数组。name对应[setUserProperty](#static-func-setuserpropertystring-string)接口的name参数。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String, Bool, String, String, Bool, Bool, Int32, Int32, Array\<String>, Array\<String>, Array\<AppEventReportConfig>)

```cangjie
public init(name: String, debugMode!: Bool = false, routeInfo!: String = "", appId!: String = "",
    onStartReport!: Bool = false, onBackgroundReport!: Bool = false, periodReport!: Int32 = 0,
    batchReport!: Int32 = 0, userIds!: Array<String> = [], userProperties!: Array<String> = [],
    eventConfigs!: Array<AppEventReportConfig> = [])
```

**功能：** 创建[Processor](#class-processor)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|数据处理者的名称。名称只能包含大小写字母、数字、下划线和$，不能以数字开头，长度非空且不超过256个字符。|
|debugMode|Bool|否|false|**命名参数。** 是否开启debug模式，默认值为false。配置值为true表示开启debug模式，false表示不开启debug模式。|
|routeInfo|String|否|""|**命名参数。** 服务器位置信息，默认为空字符串。传入字符串长度不能超过8KB，超过时会被置为默认值。|
|appId|String|否|""|**命名参数。** 应用id，默认为空字符串。传入字符串长度不能超过8KB，超过时会被置为默认值。|
|onStartReport|Bool|否|false|**命名参数。** 数据处理者在启动时是否上报事件，默认值为false。配置值为true表示上报事件，false表示不上报事件。|
|onBackgroundReport|Bool|否|false|**命名参数。** 当应用程序进入后台时是否上报事件，默认值为false。配置值为true表示上报事件，false表示不上报事件。|
|periodReport|Int32|否|0|**命名参数。** 事件定时上报时间周期，单位为秒。传入数值必须大于或等于0，小于0时会被置为默认值0，不进行定时上报。|
|batchReport|Int32|否|0|**命名参数。** 事件上报阈值，当事件条数达到阈值时上报事件。传入数值必须大于0且小于1000，不在数值范围内会被置为默认值0，不进行上报。|
|userIds|Array\<String>|否|[]|**命名参数。** 数据处理者可以上报的用户ID的name数组。name对应[setUserId](#static-func-setuseridstring-string)接口的name参数。|
|userProperties|Array\<String>|否|[]|**命名参数。** 数据处理者可以上报的用户属性的name数组。name对应[setUserProperty](#static-func-setuserpropertystring-string)接口的name参数。|
|eventConfigs|Array\<[AppEventReportConfig](#class-appeventreportconfig)>|否|[]|**命名参数。** 数据处理者可以上报的事件数组。|

## class TriggerCondition

```cangjie
public class TriggerCondition {
    public var row: Int32
    public var size: Int32
    public var timeOut: Int32
    public init(row!: Int32 = 0, size!: Int32 = 0, timeOut!: Int32 = 0)
}
```

**功能：** 提供了回调触发条件的参数选项，只要满足任一条件就会触发订阅回调。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var row

```cangjie
public var row: Int32
```

**功能：** 满足触发回调的事件总数量，正整数。默认值0，不触发回调。传入负值时，会被置为默认值。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var size

```cangjie
public var size: Int32
```

**功能：** 满足触发回调的事件总大小，正整数，单位为byte。默认值0，不触发回调。传入负值时，会被置为默认值。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var timeOut

```cangjie
public var timeOut: Int32
```

**功能：** 满足触发回调的超时时长，正整数，单位为30s。默认值0，不触发回调。传入负值时，会被置为默认值。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(Int32, Int32, Int32)

```cangjie
public init(row!: Int32 = 0, size!: Int32 = 0, timeOut!: Int32 = 0)
```

**功能：** 创建[TriggerCondition](#class-triggercondition)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|row|Int32|否|0|**命名参数。** 满足触发回调的事件总数量，正整数。默认值0，不触发回调。传入负值时，会被置为默认值。|
|size|Int32|否|0|**命名参数。** 满足触发回调的事件总大小，正整数，单位为byte。默认值0，不触发回调。传入负值时，会被置为默认值。|
|timeOut|Int32|否|0|**命名参数。** 满足触发回调的超时时长，正整数，单位为30s。默认值0，不触发回调。传入负值时，会被置为默认值。|

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

**功能：** 提供了应用事件观察者的参数选项。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var appEventFilters

```cangjie
public var appEventFilters: Array<AppEventFilter>
```

**功能：** 订阅过滤条件，在需要对订阅事件进行过滤时传入。

**类型：** Array\<[AppEventFilter](#class-appeventfilter)>

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 观察者名称，用于唯一标识观察者。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var onReceive

```cangjie
public var onReceive: Option <(String, Array<AppEventGroup>) -> Unit>
```

**功能：** 订阅实时回调函数，与回调函数onTrigger同时存在时，只触发此回调。回调函数的第一个参数表示回调事件的领域名称，回调函数的第二个参数表示回调事件集合。

**类型：** [AppEventGroup](#class-appeventgroup)->Unit

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var onTrigger

```cangjie
public var onTrigger: Option <(Int32, Int32, AppEventPackageHolder) -> Unit>
```

**功能：** 订阅回调函数，需要与回调触发条件triggerCondition一同传入才会生效。回调函数的第一个参数表示在本次回调触发时的订阅事件总数量。回调函数的第二个参数表示在本次回调触发时的订阅事件总大小，单位为byte。回调函数的第三个参数表示订阅数据持有者对象，可以通过其对订阅事件进行处理。

**类型：** (Int32,Int32,[AppEventPackageHolder](#class-appeventpackageholder))->Unit

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### var triggerCondition

```cangjie
public var triggerCondition: TriggerCondition
```

**功能：** 订阅回调触发条件，需要与回调函数onTrigger一同传入才会生效。

**类型：** [TriggerCondition](#class-triggercondition)

**读写能力：** 可读写

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### init(String, TriggerCondition, Array\<AppEventFilter>, Option\<(Int32,Int32,AppEventPackageHolder) -> Unit>, Option\<(String,Array\<AppEventGroup>) -> Unit>)

```cangjie
public init(name: String, triggerCondition!: TriggerCondition = TriggerCondition(),
    appEventFilters!: Array<AppEventFilter> = [],
    onTrigger!: Option<(Int32, Int32, AppEventPackageHolder) -> Unit> = None,
    onReceive!: Option<(String, Array<AppEventGroup>) -> Unit> = None)
```

**功能：** 创建[Watcher](#class-watcher)实例。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|观察者名称，用于唯一标识观察者。|
|triggerCondition|[TriggerCondition](#class-triggercondition)|否|TriggerCondition()|**命名参数。** 订阅回调触发条件，需要与回调函数onTrigger一同传入才会生效。|
|appEventFilters|Array\<[AppEventFilter](#class-appeventfilter)>|否|[]|**命名参数。** 订阅过滤条件，在需要对订阅事件进行过滤时传入。|
|onTrigger|Option\<(Int32,Int32,[AppEventPackageHolder](#class-appeventpackageholder))->Unit>|否|None|**命名参数。** 订阅回调函数，需要与回调触发条件triggerCondition一同传入才会生效，函数入参说明如下：<br>curRow：在本次回调触发时的订阅事件总数量； <br>curSize：在本次回调触发时的订阅事件总大小，单位为byte；<br/>holder：订阅数据持有者对象，可以通过其对订阅事件进行处理。|
|onReceive|Option\<(String,Array\<[AppEventGroup](#class-appeventgroup)>)->Unit>|否|None|**命名参数。** 订阅实时回调函数，与回调函数onTrigger同时存在时，只触发此回调，函数入参说明如下：<br>domain：回调事件的领域名称；<br>appEventGroups：回调事件集合。|

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

**功能：** 事件类型枚举。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### Behavior

```cangjie
Behavior
```

**功能：** 行为类型事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### Fault

```cangjie
Fault
```

**功能：** 故障类型事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### Security

```cangjie
Security
```

**功能：** 安全类型事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### Statistic

```cangjie
Statistic
```

**功能：** 统计类型事件。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### func getValue()

```cangjie
public func getValue(): UInt32
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|获取枚举的值。|

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

**功能：** 事件参数值数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**父类型：**

- ToString

### ArrBool(Array\<Bool>)

```cangjie
ArrBool(Array<Bool>)
```

**功能：** Bool类型数组数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### ArrFloat64(Array\<Float64>)

```cangjie
ArrFloat64(Array<Float64>)
```

**功能：** Float64类型数组数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### ArrInt32(Array\<Int32>)

```cangjie
ArrInt32(Array<Int32>)
```

**功能：** Int32类型数组数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### ArrInt64(Array\<Int64>)

```cangjie
ArrInt64(Array<Int64>)
```

**功能：** Int64类型数组数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### ArrString(Array\<String>)

```cangjie
ArrString(Array<String>)
```

**功能：** 字符串数组数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### BoolValue(Bool)

```cangjie
BoolValue(Bool)
```

**功能：** 布尔类型数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### FloatValue(Float64)

```cangjie
FloatValue(Float64)
```

**功能：** Float64类型数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### Int64Value(Int64)

```cangjie
Int64Value(Int64)
```

**功能：** Int64类型数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### IntValue(Int32)

```cangjie
IntValue(Int32)
```

**功能：** Int32类型数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### StringValue(String)

```cangjie
StringValue(String)
```

**功能：** 字符串类型数据。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回数据的字符串表示。

**系统能力：** SystemCapability.HiviewDFX.HiAppEvent

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|数据的字符串表示。|
