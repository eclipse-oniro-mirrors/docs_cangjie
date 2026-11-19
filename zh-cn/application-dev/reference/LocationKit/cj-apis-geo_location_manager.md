# ohos.geo_location_manager（位置服务）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

geo_location_manager模块提供GNSS定位、网络定位（蜂窝基站、WLAN、蓝牙定位技术）等基本功能。

使用位置服务时请打开设备“位置”开关。如果“位置”开关关闭并且代码未设置捕获异常，可能导致应用异常。

> **说明：**
>
> 本模块能力仅支持WGS-84坐标系。

## 导入模块

```cangjie
import kit.LocationKit.*
```

## 申请权限

请参考[申请位置权限开发指导](../../location/cj-location-permission-guidelines.md#开发步骤)

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class ContinuousLocationRequest

```cangjie
public class ContinuousLocationRequest {
    public init(interval: Int32, locationScenario: ScenarioValueType)
}
```

**功能：** 持续定位的请求参数，通过用户活动场景或功耗场景描述持续定位需求。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop interval

```cangjie
public mut prop interval: Int32
```

**功能：** 表示上报位置信息的时间间隔，单位是秒。默认值为1，取值范围为大于等于0。等于0时对位置上报时间间隔无限制。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop locationScenario

```cangjie
public mut prop locationScenario: ScenarioValueType
```

**功能：** 表示定位的场景信息。取值范围见[ScenarioValueType](#enum-scenariovaluetype)的定义。

**类型：** [ScenarioValueType](#enum-scenariovaluetype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### init(Int32, ScenarioValueType)

```cangjie
public init(interval: Int32, locationScenario: ScenarioValueType)
```

**功能：** 构造持续定位请求参数。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|interval|Int32|是|-|表示上报位置信息的时间间隔，单位是秒。|
|locationScenario|[ScenarioValueType](#enum-scenariovaluetype)|是|-|表示定位的场景信息，为用户活动场景或功耗场景。|

## class CountryCode

```cangjie
public class CountryCode {}
```

**功能：** 国家码信息，包含国家码字符串和国家码的来源信息。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop country

```cangjie
public mut prop country: String
```

**功能：** 表示国家码字符串。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop countryCodeType

```cangjie
public mut prop countryCodeType: CountryCodeType
```

**功能：** 表示国家码信息来源。取值范围见[CountryCodeType](#enum-countrycodetype)的定义。

**类型：** [CountryCodeType](#enum-countrycodetype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

## class CurrentLocationRequest

```cangjie
public class CurrentLocationRequest {
    public var priority: LocationRequestPriority
    public var scenario: LocationRequestScenario
    public var maxAccuracy: Float32
    public var timeoutMs: Int32
    public init(priority!: LocationRequestPriority = LocationRequestPriority.FirstFix,
        scenario!: LocationRequestScenario = LocationRequestScenario.Unset, maxAccuracy!: Float32 = 0.0,
        timeoutMs!: Int32 = 5000)
}
```

**功能：** 当前位置信息请求参数。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var maxAccuracy

```cangjie
public var maxAccuracy: Float32
```

**功能：** 应用向系统请求位置信息时要求的精度值，单位为米。该参数仅在精确位置功能场景（即同时授权了ohos.permission.APPROXIMATELY_LOCATION和ohos.permission.LOCATION 权限）下有效，模糊位置功能生效场景（即仅授权了ohos.permission.APPROXIMATELY_LOCATION 权限）下该字段无意义。

该参数生效的情况下，系统会对比GNSS或网络定位服务上报的位置信息与应用的位置信息申请。当位置信息[Location](#class-location)中的精度值（accuracy）小于等于应用要求的精度值（maxAccuracy）时，位置信息会返回给应用；否则系统将丢弃本次收到的位置信息。

当scenario为NAVIGATION/TRAJECTORY_TRACKING/CAR_HAILING或者priority为ACCURACY时建议设置maxAccuracy为大于10的值。

当scenario为DAILY_LIFE_SERVICE/NO_POWER或者priority为LOW_POWER/FIRST_FIX时建议设置maxAccuracy为大于100的值。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var priority

```cangjie
public var priority: LocationRequestPriority
```

**功能：** 表示优先级信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。取值范围见[LocationRequestPriority](#enum-locationrequestpriority)的定义。

**类型：** [LocationRequestPriority](#enum-locationrequestpriority)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var scenario

```cangjie
public var scenario: LocationRequestScenario
```

**功能：** 表示场景信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。取值范围见[LocationRequestScenario](#enum-locationrequestscenario)的定义。

**类型：** [LocationRequestScenario](#enum-locationrequestscenario)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var timeoutMs

```cangjie
public var timeoutMs: Int32
```

**功能：** 表示超时时间，单位是毫秒，最小为1000毫秒。取值范围为大于等于1000。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### init(LocationRequestPriority, LocationRequestScenario, Float32, Int32)

```cangjie
public init(priority!: LocationRequestPriority = LocationRequestPriority.FirstFix,
    scenario!: LocationRequestScenario = LocationRequestScenario.Unset, maxAccuracy!: Float32 = 0.0,
    timeoutMs!: Int32 = 5000)
```

**功能：** 构造CurrentLocationRequest对象。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|priority|[LocationRequestPriority](#enum-locationrequestpriority)|否|LocationRequestPriority.FirstFix|**命名参数。** 表示优先级信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。取值范围见[LocationRequestPriority](#enum-locationrequestpriority)的定义。默认值为LocationRequestPriority.FirstFix。|
|scenario|[LocationRequestScenario](#enum-locationrequestscenario)|否|LocationRequestScenario.Unset|**命名参数。** 表示场景信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。取值范围见[LocationRequestScenario](#enum-locationrequestscenario)的定义。默认值为LocationRequestScenario.Unset。|
|maxAccuracy|Float32|否|0.0|**命名参数。** 应用向系统请求位置信息时要求的精度值，单位为米。默认值为0，表示不限制位置信息的精度，取值范围为大于等于0。|
|timeoutMs|Int32|否|5000|**命名参数。** 表示超时时间，单位是毫秒，最小为1000毫秒。取值范围为大于等于1000。|

## class GeoLocationManager

```cangjie
public class GeoLocationManager {}
```

**功能：** 用于提供位置服务的类。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### static func getCurrentLocation()

```cangjie
public static func getCurrentLocation(): Location
```

**功能：** 获取当前位置。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[Location](#class-location)|返回当前位置信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getCurrentLocation} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |
  | 3301200 | Failed to obtain the geographical location. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let location = GeoLocationManager.getCurrentLocation()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getCurrentLocation(CurrentLocationRequest)

```cangjie
public static func getCurrentLocation(request: CurrentLocationRequest): Location
```

**功能：** 获取当前位置。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|request|[CurrentLocationRequest](#class-currentlocationrequest)|是|-|设置位置请求参数。|

**返回值：**

|类型|说明|
|:----|:----|
|[Location](#class-location)|返回当前位置信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getCurrentLocation} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |
  | 3301200 | Failed to obtain the geographical location. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let location = GeoLocationManager.getCurrentLocation(CurrentLocationRequest())
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getCurrentLocation(SingleLocationRequest)

```cangjie
public static func getCurrentLocation(request: SingleLocationRequest): Location
```

**功能：** 获取当前位置。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|request|[SingleLocationRequest](#class-singlelocationrequest)|是|-|设置位置请求参数。|

**返回值：**

|类型|说明|
|:----|:----|
|[Location](#class-location)|返回当前位置信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getCurrentLocation} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |
  | 3301200 | Failed to obtain the geographical location. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let location = GeoLocationManager.getCurrentLocation(SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 1000))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func isLocationEnabled()

```cangjie
public static func isLocationEnabled(): Bool
```

**功能：** 判断位置服务是否已经开启。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true：位置信息开关已开启。<br/>false：位置信息开关已关闭。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.isLocationEnabled} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let res = GeoLocationManager.isLocationEnabled()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class Location

```cangjie
public class Location {
    public var latitude: Float64
    public var longitude: Float64
    public var altitude: Float64
    public var accuracy: Float64
    public var speed: Float64
    public var timestamp: Int64
    public var direction: Float64
    public var timeSinceBoot: Int64
    public var additions: ?Array<String>
    public var additionsMap: ?Map<String, String>
    public var additionSize: ?Int64
    public var altitudeAccuracy: ?Float64
    public var speedAccuracy: ?Float64
    public var directionAccuracy: ?Float64
    public var uncertaintyOfTimeSinceBoot: ?Int64
    public var sourceType: ?LocationSourceType
}
```

**功能：** 位置信息。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var accuracy

```cangjie
public var accuracy: Float64
```

**功能：** 表示精度信息，单位米。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var additionSize

```cangjie
public var additionSize: ?Int64
```

**功能：** 附加信息数量。取值范围为大于等于0。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var additions

```cangjie
public var additions: ?Array<String>
```

**功能：** 附加信息。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var additionsMap

```cangjie
public var additionsMap: ?Map<String, String>
```

**功能：** 附加信息。具体内容和顺序与additions一致。

**类型：** ?Map\<String, String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var altitude

```cangjie
public var altitude: Float64
```

**功能：** 表示高度信息，单位米。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var altitudeAccuracy

```cangjie
public var altitudeAccuracy: ?Float64
```

**功能：** 表示高度信息的精度，单位米。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var direction

```cangjie
public var direction: Float64
```

**功能：** 表示航向信息。单位是“度”，取值范围为0到360。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var directionAccuracy

```cangjie
public var directionAccuracy: ?Float64
```

**功能：** 表示航向信息的精度。单位是“度”，取值范围为0到360。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var latitude

```cangjie
public var latitude: Float64
```

**功能：** 表示纬度信息，正值表示北纬，负值表示南纬。取值范围为-90到90。仅支持WGS84坐标系。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var longitude

```cangjie
public var longitude: Float64
```

**功能：** 表示经度信息，正值表示东经，负值表示西经。取值范围为-180到180。仅支持WGS84坐标系。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var sourceType

```cangjie
public var sourceType: ?LocationSourceType
```

**功能：** 表示定位结果的来源。

**类型：** [LocationSourceType](#enum-locationsourcetype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var speed

```cangjie
public var speed: Float64
```

**功能：** 表示速度信息，单位米每秒。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var speedAccuracy

```cangjie
public var speedAccuracy: ?Float64
```

**功能：** 表示速度信息的精度，单位米每秒。

**类型：** ?Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var timeSinceBoot

```cangjie
public var timeSinceBoot: Int64
```

**功能：** 表示获取位置成功的时间戳，值表示从本次开机到获取位置成功所经过的时间，单位为纳秒。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**功能：** 表示位置时间戳，UTC格式。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var uncertaintyOfTimeSinceBoot

```cangjie
public var uncertaintyOfTimeSinceBoot: ?Int64
```

**功能：** 表示位置时间戳的不确定度。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

## class LocationCommand

```cangjie
public class LocationCommand {
    public init(scenario: LocationRequestScenario, command: String)
}
```

**功能：** 位置子系统扩展命令参数，包含目标定位场景和命令内容。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop scenario

```cangjie
public mut prop scenario: LocationRequestScenario
```

**功能：** 表示发送命令的定位场景。

**类型：** LocationRequestScenario

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop command

```cangjie
public mut prop command: String
```

**功能：** 表示发送的命令内容，字符串长度不超过100。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### init(LocationRequestScenario, String)

```cangjie
public init(scenario: LocationRequestScenario, command: String)
```

**功能：** 构造位置子系统扩展命令参数。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|scenario|LocationRequestScenario|是|-|表示发送命令的定位场景。|
|command|String|是|-|表示发送的命令内容，字符串长度不超过100。|

## class LocationRequest

```cangjie
public class LocationRequest {
    public init(priority!: ?LocationRequestPriority = None,
        scenario!: ?LocationRequestScenario = None, timeInterval!: ?Int32 = None,
        distanceInterval!: ?Float64 = None, maxAccuracy!: ?Float32 = None)
}
```

**功能：** 持续定位的位置信息请求参数，用于配置定位优先级、场景、上报间隔和精度要求。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop priority

```cangjie
public mut prop priority: ?LocationRequestPriority
```

**功能：** 表示优先级信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。默认值为FirstFix。取值范围见LocationRequestPriority的定义。

**类型：** ?LocationRequestPriority

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop scenario

```cangjie
public mut prop scenario: ?LocationRequestScenario
```

**功能：** 表示场景信息。当scenario取值为Unset时，priority参数生效，否则priority参数不生效；当scenario和priority均取值为Unset时，无法发起定位请求。默认值为Unset。取值范围见LocationRequestScenario的定义。

**类型：** ?LocationRequestScenario

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop timeInterval

```cangjie
public mut prop timeInterval: ?Int32
```

**功能：** 表示上报位置信息的时间间隔，单位为秒，取值范围为大于等于0。默认值为对应定位模式下允许的最小时间间隔：GNSS定位时为1秒，网络定位时为20秒。当设置值小于最小间隔时，以最小时间间隔生效；设置为0时不对时间间隔进行校验，直接上报位置信息。

**类型：** ?Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop distanceInterval

```cangjie
public mut prop distanceInterval: ?Float64
```

**功能：** 表示上报位置信息的距离间隔，单位为米，默认值为0，取值范围为大于等于0。等于0时对位置上报距离间隔无限制。

**类型：** ?Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### prop maxAccuracy

```cangjie
public mut prop maxAccuracy: ?Float32
```

**功能：** 应用向系统请求位置信息时要求的精度值，单位为米，默认值为0，表示不限制位置信息的精度，取值范围为大于等于0。该参数仅在精确位置功能场景（即同时授权了ohos.permission.APPROXIMATELY_LOCATION和ohos.permission.LOCATION权限）下有效，模糊位置功能生效场景（即仅授权了ohos.permission.APPROXIMATELY_LOCATION权限）下该字段无意义。

该参数生效的情况下，系统会对比GNSS或网络定位服务上报的位置信息与应用的位置信息申请。当位置信息中的精度值（accuracy）小于等于应用要求的精度值（maxAccuracy）时，位置信息会返回给应用；否则系统将丢弃本次收到的位置信息。

当scenario为Navigation、TrajectoryTracking、CarHailing或者priority为Accuracy时建议设置maxAccuracy为大于10的值；当scenario为DailyLifeService、NoPower或者priority为LowPower、FirstFix时建议设置maxAccuracy为大于100的值。

**类型：** ?Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### init(?LocationRequestPriority, ?LocationRequestScenario, ?Int32, ?Float64, ?Float32)

```cangjie
public init(priority!: ?LocationRequestPriority = None,
    scenario!: ?LocationRequestScenario = None, timeInterval!: ?Int32 = None,
    distanceInterval!: ?Float64 = None, maxAccuracy!: ?Float32 = None)
```

**功能：** 构造位置信息请求参数。未设置的参数使用系统默认值。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|priority|?LocationRequestPriority|否|None|表示优先级信息，默认值为FirstFix。|
|scenario|?LocationRequestScenario|否|None|表示场景信息，默认值为Unset。|
|timeInterval|?Int32|否|None|表示上报位置信息的时间间隔，单位为秒，默认值为1。|
|distanceInterval|?Float64|否|None|表示上报位置信息的距离间隔，单位为米，默认值为0.0。|
|maxAccuracy|?Float32|否|None|表示精度值，单位为米，默认值为0.0。|

## class SatelliteStatusInfo

```cangjie
public class SatelliteStatusInfo {}
```

**功能：** 卫星状态信息，包含卫星数量、卫星ID、载波噪声密度、高度角、方位角、载波频率、星座类型与附加信息。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop satellitesNumber

```cangjie
public mut prop satellitesNumber: Int32
```

**功能：** 表示卫星数量。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop satelliteIds

```cangjie
public mut prop satelliteIds: Array<Int32>
```

**功能：** 表示卫星ID数组。

**类型：** Array\<Int32\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop carrierToNoiseDensitys

```cangjie
public mut prop carrierToNoiseDensitys: Array<Float64>
```

**功能：** 表示卫星载波噪声密度数组。

**类型：** Array\<Float64\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop altitudes

```cangjie
public mut prop altitudes: Array<Float64>
```

**功能：** 表示卫星高度角数组。

**类型：** Array\<Float64\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop azimuths

```cangjie
public mut prop azimuths: Array<Float64>
```

**功能：** 表示卫星方位角数组。

**类型：** Array\<Float64\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop carrierFrequencies

```cangjie
public mut prop carrierFrequencies: Array<Float64>
```

**功能：** 表示卫星载波频率数组。

**类型：** Array\<Float64\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop satelliteConstellation

```cangjie
public mut prop satelliteConstellation: ?Array<SatelliteConstellationCategory>
```

**功能：** 表示卫星星座类型数组，取值参见[SatelliteConstellationCategory](#enum-satelliteconstellationcategory)。

**类型：** ?Array\<[SatelliteConstellationCategory](#enum-satelliteconstellationcategory)\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### prop satelliteAdditionalInfo

```cangjie
public mut prop satelliteAdditionalInfo: ?Array<Int32>
```

**功能：** 表示卫星附加信息数组。

**类型：** ?Array\<Int32\>

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

## class SingleLocationRequest

```cangjie
public class SingleLocationRequest {
    public var locatingPriority: LocatingPriority
    public var locatingTimeoutMs: Int32
    public init(locatingPriority: LocatingPriority, locatingTimeoutMs: Int32)
}
```

**功能：** 单次定位的请求参数。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var locatingPriority

```cangjie
public var locatingPriority: LocatingPriority
```

**功能：** 表示优先级信息。取值范围见[LocatingPriority](#enum-locatingpriority)的定义。

**类型：** [LocatingPriority](#enum-locatingpriority)

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### var locatingTimeoutMs

```cangjie
public var locatingTimeoutMs: Int32
```

**功能：** 表示超时时间，单位是毫秒，最小为1000毫秒。取值范围为大于等于1000。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### init(LocatingPriority, Int32)

```cangjie
public init(locatingPriority: LocatingPriority, locatingTimeoutMs: Int32)
```

**功能：** 构造SingleLocationRequest对象。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|locatingPriority|[LocatingPriority](#enum-locatingpriority)|是|-|表示优先级信息。取值范围见[LocatingPriority](#enum-locatingpriority)的定义。|
|locatingTimeoutMs|Int32|是|-|表示超时时间，单位是毫秒，最小为1000毫秒。取值范围为大于等于1000。|

## enum CountryCodeType

```cangjie
public enum CountryCodeType {
    | CountryCodeFromLocale
    | CountryCodeFromSim
    | CountryCodeFromLocation
    | CountryCodeFromNetwork
    | ...
}
```

**功能：** 国家码来源类型。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<CountryCodeType\>
- ToString

### CountryCodeFromLocale

```cangjie
CountryCodeFromLocale
```

**功能：** 从全球化模块的语言配置信息中获取到的国家码。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### CountryCodeFromSim

```cangjie
CountryCodeFromSim
```

**功能：** 从SIM卡中获取到的国家码。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### CountryCodeFromLocation

```cangjie
CountryCodeFromLocation
```

**功能：** 基于用户的位置信息，通过逆地理编码查询到的国家码。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### CountryCodeFromNetwork

```cangjie
CountryCodeFromNetwork
```

**功能：** 从蜂窝网络注册信息中获取到的国家码。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将国家码来源类型转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|国家码来源类型的字符串表示。|

### func ==(CountryCodeType)

```cangjie
public operator func ==(other: CountryCodeType): Bool
```

**功能：** 判断两个国家码来源类型是否相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CountryCodeType](#enum-countrycodetype)|是|-|待比较的国家码来源类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(CountryCodeType)

```cangjie
public operator func !=(other: CountryCodeType): Bool
```

**功能：** 判断两个国家码来源类型是否不相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[CountryCodeType](#enum-countrycodetype)|是|-|待比较的国家码来源类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## enum LocatingPriority

```cangjie
public enum LocatingPriority {
    | PriorityAccuracy
    | PriorityLocatingSpeed
    | ...
}
```

**功能：** 单次位置请求中的优先级类型。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### PriorityAccuracy

```cangjie
PriorityAccuracy
```

**功能：** 表示精度优先。

定位精度优先策略会同时使用GNSS定位和网络定位技术，并把一段时间内精度较好的结果返回给应用；这个时间段长度为[SingleLocationRequest](#class-singlelocationrequest).locatingTimeoutMs与“30秒”中的较小者。

对设备的硬件资源消耗较大，功耗较大。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### PriorityLocatingSpeed

```cangjie
PriorityLocatingSpeed
```

**功能：** 表示快速获取位置优先，如果应用希望快速拿到一个位置，可以将优先级设置为该类型。

快速定位优先策略会同时使用GNSS定位和网络定位技术，以便在室内和户外场景下均可以快速获取到位置结果，我们会把最先拿到的定位结果返回给应用。对设备的硬件资源消耗较大，功耗也较大。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

## enum LocationError

```cangjie
public enum LocationError {
    | LocatingFailedDefault
    | LocatingFailedLocationPermissionDenied
    | LocatingFailedBackgroundPermissionDenied
    | LocatingFailedLocationSwitchOff
    | LocatingFailedInternetAccessFailure
    | ...
}
```

**功能：** 持续定位过程中的错误信息。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<LocationError\>
- ToString

### LocatingFailedDefault

```cangjie
LocatingFailedDefault
```

**功能：** 定位失败的默认原因。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### LocatingFailedLocationPermissionDenied

```cangjie
LocatingFailedLocationPermissionDenied
```

**功能：** 表示ohos.permission.APPROXIMATELY_LOCATION权限或ohos.permission.LOCATION权限校验失败导致持续定位失败。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### LocatingFailedBackgroundPermissionDenied

```cangjie
LocatingFailedBackgroundPermissionDenied
```

**功能：** 表示应用在后台时位置权限校验失败导致持续定位失败。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### LocatingFailedLocationSwitchOff

```cangjie
LocatingFailedLocationSwitchOff
```

**功能：** 表示位置信息开关关闭导致持续定位失败。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### LocatingFailedInternetAccessFailure

```cangjie
LocatingFailedInternetAccessFailure
```

**功能：** 表示无法访问网络，导致网络定位失败。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将定位错误信息转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|定位错误信息的字符串表示。|

### func ==(LocationError)

```cangjie
public operator func ==(other: LocationError): Bool
```

**功能：** 判断两个定位错误信息是否相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[LocationError](#enum-locationerror)|是|-|待比较的定位错误信息。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(LocationError)

```cangjie
public operator func !=(other: LocationError): Bool
```

**功能：** 判断两个定位错误信息是否不相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[LocationError](#enum-locationerror)|是|-|待比较的定位错误信息。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## enum LocationRequestPriority

```cangjie
public enum LocationRequestPriority {
    | Unset
    | Accuracy
    | LowPower
    | FirstFix
    | ...
}
```

**功能：** 位置请求中位置信息优先级类型。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Accuracy

```cangjie
Accuracy
```

**功能：** 表示精度优先。

定位精度优先策略主要以GNSS定位技术为主。我们会在GNSS提供稳定位置结果之前使用网络定位技术提供服务。在持续定位过程中，如果超过30秒无法获取GNSS定位结果则使用网络定位技术。对设备的硬件资源消耗较大，功耗较大。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### FirstFix

```cangjie
FirstFix
```

**功能：** 表示快速获取位置优先，如果应用希望快速拿到一个位置，可以将优先级设置为该字段。

快速定位优先策略会同时使用GNSS定位和网络定位技术，以便在室内和户外场景下均可以快速获取到位置结果；当各种定位技术都有提供位置结果时，系统会选择其中精度较好的结果返回给应用。因为对各种定位技术同时使用，对设备的硬件资源消耗较大，功耗也较大。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### LowPower

```cangjie
LowPower
```

**功能：** 表示低功耗优先。

低功耗定位优先策略仅使用网络定位技术，在室内和户外场景均可提供定位服务，因为其依赖周边基站、可见WLAN、蓝牙设备的分布情况，定位结果的精度波动范围较大，推荐在对定位结果精度要求不高的场景下使用该策略，可以有效节省设备功耗。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Unset

```cangjie
Unset
```

**功能：** 表示未设置优先级，表示[LocationRequestPriority](#enum-locationrequestpriority)无效。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

## enum LocationRequestScenario

```cangjie
public enum LocationRequestScenario {
    | Unset
    | Navigation
    | TrajectoryTracking
    | CarHailing
    | DailyLifeService
    | NoPower
    | ...
}
```

**功能：** 位置请求中定位场景类型。

> **说明：**
>
> 当使用NAVIGATION/TRAJECTORY_TRACKING/CAR_HAILING场景进行单次定位或持续定位时，会在GNSS提供稳定位置结果之前使用网络定位技术提供服务；在持续定位时，如果超过30秒无法获取GNSS定位结果则会使用网络定位技术获取位置。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### CarHailing

```cangjie
CarHailing
```

**功能：** 表示打车场景。

适用于用户出行打车时定位当前位置的场景，如网约车类应用。

主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### DailyLifeService

```cangjie
DailyLifeService
```

**功能：** 表示日常服务使用场景。

适用于不需要定位用户精确位置的使用场景，如新闻资讯、网购、点餐类应用。

该场景仅使用网络定位技术提供定位服务，功耗较低。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Navigation

```cangjie
Navigation
```

**功能：** 表示导航场景。

适用于在户外获取设备实时位置的场景，如车载、步行导航。

主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### NoPower

```cangjie
NoPower
```

**功能：** 表示无功耗场景，这种场景下不会主动触发定位，会在其他应用定位时，才给当前应用返回位置。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### TrajectoryTracking

```cangjie
TrajectoryTracking
```

**功能：** 表示运动轨迹记录场景。

适用于记录用户位置轨迹的场景，如运动类应用记录轨迹功能。

主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Unset

```cangjie
Unset
```

**功能：** 表示未设置场景信息。

表示[LocationRequestScenario](#enum-locationrequestscenario)字段无效。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

## enum LocationSourceType

```cangjie
public enum LocationSourceType {
    | Gnss
    | Network
    | Indoor
    | Rtk
    | ...
}
```

**功能：** 定位结果的来源。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Gnss

```cangjie
Gnss
```

**功能：** 表示定位结果来自于GNSS定位技术。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Indoor

```cangjie
Indoor
```

**功能：** 表示定位结果来自于室内高精度定位技术。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Network

```cangjie
Network
```

**功能：** 表示定位结果来自于网络定位技术。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

### Rtk

```cangjie
Rtk
```

**功能：** 表示定位结果来自于室外高精度定位技术。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 22

## enum PowerConsumptionScenario

```cangjie
public enum PowerConsumptionScenario {
    | HighPowerConsumption
    | LowPowerConsumption
    | NoPowerConsumption
    | ...
}
```

**功能：** 位置请求中的功耗场景类型。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<PowerConsumptionScenario\>
- ToString

### HighPowerConsumption

```cangjie
HighPowerConsumption
```

**功能：** 高功耗。以GNSS定位技术为主，在GNSS提供稳定位置结果之前使用网络定位技术提供服务；在持续定位时，如果超过30秒无法获取GNSS定位结果则使用网络定位技术获取位置。对设备的硬件资源消耗较大，功耗较大。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### LowPowerConsumption

```cangjie
LowPowerConsumption
```

**功能：** 低功耗。适用于对用户位置精度要求不高的使用场景，如新闻资讯、网购、点餐类应用。该场景仅使用网络定位技术提供定位服务，功耗较低。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### NoPowerConsumption

```cangjie
NoPowerConsumption
```

**功能：** 无功耗。这种场景下不会主动触发定位，会在其他应用定位时，才给当前应用返回位置。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将功耗场景类型转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|功耗场景类型的字符串表示。|

### func ==(PowerConsumptionScenario)

```cangjie
public operator func ==(other: PowerConsumptionScenario): Bool
```

**功能：** 判断两个功耗场景类型是否相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PowerConsumptionScenario](#enum-powerconsumptionscenario)|是|-|待比较的功耗场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(PowerConsumptionScenario)

```cangjie
public operator func !=(other: PowerConsumptionScenario): Bool
```

**功能：** 判断两个功耗场景类型是否不相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[PowerConsumptionScenario](#enum-powerconsumptionscenario)|是|-|待比较的功耗场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## enum SatelliteConstellationCategory

```cangjie
public enum SatelliteConstellationCategory {
    | ConstellationCategoryUnknown
    | ConstellationCategoryGps
    | ConstellationCategorySbas
    | ConstellationCategoryGlonass
    | ConstellationCategoryQzss
    | ConstellationCategoryBeidou
    | ConstellationCategoryGalileo
    | ConstellationCategoryIrnss
    | ...
}
```

**功能：** 卫星星座类型。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**父类型：**

- Equatable\<SatelliteConstellationCategory\>
- ToString

### ConstellationCategoryUnknown

```cangjie
ConstellationCategoryUnknown
```

**功能：** 未知星座类型。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryGps

```cangjie
ConstellationCategoryGps
```

**功能：** GPS星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategorySbas

```cangjie
ConstellationCategorySbas
```

**功能：** SBAS（星基增强系统）星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryGlonass

```cangjie
ConstellationCategoryGlonass
```

**功能：** GLONASS星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryQzss

```cangjie
ConstellationCategoryQzss
```

**功能：** QZSS（准天顶卫星系统）星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryBeidou

```cangjie
ConstellationCategoryBeidou
```

**功能：** 北斗星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryGalileo

```cangjie
ConstellationCategoryGalileo
```

**功能：** Galileo（伽利略）星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### ConstellationCategoryIrnss

```cangjie
ConstellationCategoryIrnss
```

**功能：** IRNSS（印度区域导航卫星系统）星座。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将卫星星座类型转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|卫星星座类型的字符串表示。|

### func ==(SatelliteConstellationCategory)

```cangjie
public operator func ==(other: SatelliteConstellationCategory): Bool
```

**功能：** 判断两个卫星星座类型是否相等。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SatelliteConstellationCategory](#enum-satelliteconstellationcategory)|是|-|待比较的卫星星座类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(SatelliteConstellationCategory)

```cangjie
public operator func !=(other: SatelliteConstellationCategory): Bool
```

**功能：** 判断两个卫星星座类型是否不相等。

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SatelliteConstellationCategory](#enum-satelliteconstellationcategory)|是|-|待比较的卫星星座类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## enum ScenarioValueType

```cangjie
public enum ScenarioValueType {
    | UserActivityScenarioValue(UserActivityScenario)
    | PowerConsumptionScenarioValue(PowerConsumptionScenario)
}
```

**功能：** 定位场景类型，用作持续定位请求中的场景参数，可选择用户活动场景或功耗场景。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<ScenarioValueType\>
- ToString

### UserActivityScenarioValue(UserActivityScenario)

```cangjie
UserActivityScenarioValue(UserActivityScenario)
```

**功能：** 表示用户活动场景，取值范围见UserActivityScenario的定义。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### PowerConsumptionScenarioValue(PowerConsumptionScenario)

```cangjie
PowerConsumptionScenarioValue(PowerConsumptionScenario)
```

**功能：** 表示功耗场景，取值范围见[PowerConsumptionScenario](#enum-powerconsumptionscenario)的定义。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将定位场景类型转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|定位场景类型的字符串表示。|

### func ==(ScenarioValueType)

```cangjie
public operator func ==(other: ScenarioValueType): Bool
```

**功能：** 判断两个定位场景类型是否相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ScenarioValueType](#enum-scenariovaluetype)|是|-|待比较的定位场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(ScenarioValueType)

```cangjie
public operator func !=(other: ScenarioValueType): Bool
```

**功能：** 判断两个定位场景类型是否不相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ScenarioValueType](#enum-scenariovaluetype)|是|-|待比较的定位场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## enum UserActivityScenario

```cangjie
public enum UserActivityScenario {
    | Navigation
    | Sport
    | Transport
    | DailyLifeService
    | ...
}
```

**功能：** 位置请求中的用户活动场景类型。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**父类型：**

- Equatable\<UserActivityScenario\>
- ToString

### Navigation

```cangjie
Navigation
```

**功能：** 表示导航场景。适用于在户外获取设备实时位置的场景，如车载、步行导航。主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### Sport

```cangjie
Sport
```

**功能：** 表示运动场景。适用于记录用户位置轨迹的场景，如运动类应用记录轨迹功能。主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### Transport

```cangjie
Transport
```

**功能：** 表示出行场景。适用于用户出行场景，如打车、乘坐公共交通等场景。主要使用GNSS定位技术提供定位服务，功耗较高。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### DailyLifeService

```cangjie
DailyLifeService
```

**功能：** 表示日常服务使用场景。适用于不需要定位用户精确位置的使用场景，如新闻资讯、网购、点餐类应用。该场景仅使用网络定位技术提供定位服务，功耗较低。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将用户活动场景类型转换为字符串表示。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|用户活动场景类型的字符串表示。|

### func ==(UserActivityScenario)

```cangjie
public operator func ==(other: UserActivityScenario): Bool
```

**功能：** 判断两个用户活动场景类型是否相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[UserActivityScenario](#enum-useractivityscenario)|是|-|待比较的用户活动场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(UserActivityScenario)

```cangjie
public operator func !=(other: UserActivityScenario): Bool
```

**功能：** 判断两个用户活动场景类型是否不相等。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[UserActivityScenario](#enum-useractivityscenario)|是|-|待比较的用户活动场景类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

## func onLocationChange(LocationRequest, Callback1Argument\<Location>)

```cangjie
public func onLocationChange(request: LocationRequest, callback: Callback1Argument<Location>): Unit
```

**功能：** 开启位置变化订阅，并发起定位请求。使用callback异步回调。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|request|[LocationRequest](#class-locationrequest)|是|-|设置位置请求参数。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\>|是|-|用于接收位置信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = LocationRequest(priority: LocationRequestPriority.FirstFix,
        scenario: LocationRequestScenario.Unset, timeInterval: 1, distanceInterval: 0.0, maxAccuracy: 0.0)
    onLocationChange(request, Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationChange(ContinuousLocationRequest, Callback1Argument\<Location>)

```cangjie
public func onLocationChange(request: ContinuousLocationRequest, callback: Callback1Argument<Location>): Unit
```

**功能：** 开启位置变化订阅，并发起定位请求。使用callback异步回调。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|request|[ContinuousLocationRequest](#class-continuouslocationrequest)|是|-|设置持续定位的请求参数。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\>|是|-|用于接收位置信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = ContinuousLocationRequest(1,
        ScenarioValueType.UserActivityScenarioValue(UserActivityScenario.Navigation))
    onLocationChange(request, Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationChange(?Callback1Argument\<Location>)

```cangjie
public func offLocationChange(callback!: ?Callback1Argument<Location> = None): Unit
```

**功能：** 关闭位置变化订阅，并删除对应的定位请求。传入的callback需要与onLocationChange接口传入的callback保持一致，否则取消订阅失败；不传入callback时取消当前类型的所有订阅。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = LocationRequest(priority: LocationRequestPriority.FirstFix, scenario: LocationRequestScenario.Unset)
    let callback = Callback()
    onLocationChange(request, callback)
    offLocationChange(callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationError(Callback1Argument\<LocationError>)

```cangjie
public func onLocationError(callback: Callback1Argument<LocationError>): Unit
```

**功能：** 订阅持续定位过程中的错误信息。使用callback异步回调。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[LocationError](#enum-locationerror)\>|是|-|用于接收持续定位错误信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationError} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<LocationError> {
    public func invoke(err: ?BusinessException, arg: LocationError): Unit {
        Hilog.info(0, "test", "location error: ${arg.toString()}")
    }
}

try {
    onLocationError(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationError(?Callback1Argument\<LocationError>)

```cangjie
public func offLocationError(callback!: ?Callback1Argument<LocationError> = None): Unit
```

**功能：** 取消订阅持续定位过程中的错误信息。传入的callback需要与onLocationError接口传入的callback保持一致；不传入callback时取消当前类型的所有订阅。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[LocationError](#enum-locationerror)\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationError} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offLocationError()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationEnabledChange(Callback1Argument\<Bool>)

```cangjie
public func onLocationEnabledChange(callback: Callback1Argument<Bool>): Unit
```

**功能：** 订阅位置服务状态变化。使用callback异步回调。回调返回true表示位置信息开关已经开启，返回false表示位置信息开关已经关闭。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Bool\>|是|-|用于接收位置开关状态的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationEnabledChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Bool> {
    public func invoke(err: ?BusinessException, arg: Bool): Unit {
        Hilog.info(0, "test", "location enabled: ${arg}")
    }
}

try {
    onLocationEnabledChange(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationEnabledChange(?Callback1Argument\<Bool>)

```cangjie
public func offLocationEnabledChange(callback!: ?Callback1Argument<Bool> = None): Unit
```

**功能：** 取消订阅位置服务状态变化。传入的callback需要与onLocationEnabledChange接口传入的callback保持一致；不传入callback时取消当前类型的所有订阅。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Bool\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationEnabledChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offLocationEnabledChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onSatelliteStatusChange(Callback1Argument\<SatelliteStatusInfo>)

```cangjie
public func onSatelliteStatusChange(callback: Callback1Argument<SatelliteStatusInfo>): Unit
```

**功能：** 订阅卫星状态变化事件。使用callback异步回调。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[SatelliteStatusInfo](#class-satellitestatusinfo)\>|是|-|用于接收卫星状态信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onSatelliteStatusChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class SatelliteCallback <: Callback1Argument<SatelliteStatusInfo> {
    public func invoke(err: ?BusinessException, arg: SatelliteStatusInfo): Unit {
        Hilog.info(0, "test", "satellites: ${arg.satellitesNumber}, ids: ${arg.satelliteIds.size}")
    }
}

try {
    onSatelliteStatusChange(SatelliteCallback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offSatelliteStatusChange(?Callback1Argument\<SatelliteStatusInfo>)

```cangjie
public func offSatelliteStatusChange(callback!: ?Callback1Argument<SatelliteStatusInfo> = None): Unit
```

**功能：** 取消订阅卫星状态变化事件。传入的callback需要与onSatelliteStatusChange接口传入的callback保持一致；不传入callback时取消当前类型的所有订阅。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[SatelliteStatusInfo](#class-satellitestatusinfo)\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offSatelliteStatusChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offSatelliteStatusChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onNmeaMessage(Callback1Argument\<String>)

```cangjie
public func onNmeaMessage(callback: Callback1Argument<String>): Unit
```

**功能：** 订阅NMEA消息事件。使用callback异步回调。

**需要权限：** ohos.permission.LOCATION、ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<String\>|是|-|用于接收NMEA消息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onNmeaMessage} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class NmeaCallback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "test", "nmea: ${arg}")
    }
}

try {
    onNmeaMessage(NmeaCallback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offNmeaMessage(?Callback1Argument\<String>)

```cangjie
public func offNmeaMessage(callback!: ?Callback1Argument<String> = None): Unit
```

**功能：** 取消订阅NMEA消息事件。传入的callback需要与onNmeaMessage接口传入的callback保持一致；不传入callback时取消当前类型的所有订阅。

**需要权限：** ohos.permission.LOCATION、ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Gnss

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<String\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offNmeaMessage} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offNmeaMessage()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onCountryCodeChange(Callback1Argument\<CountryCode>)

```cangjie
public func onCountryCodeChange(callback: Callback1Argument<CountryCode>): Unit
```

**功能：** 订阅国家码信息变化事件。使用callback异步回调。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[CountryCode](#class-countrycode)\>|是|-|用于接收国家码信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onCountryCodeChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<CountryCode> {
    public func invoke(err: ?BusinessException, arg: CountryCode): Unit {
        Hilog.info(0, "test", "country: ${arg.country}, type: ${arg.countryCodeType.toString()}")
    }
}

try {
    onCountryCodeChange(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offCountryCodeChange(?Callback1Argument\<CountryCode>)

```cangjie
public func offCountryCodeChange(callback!: ?Callback1Argument<CountryCode> = None): Unit
```

**功能：** 取消订阅国家码信息变化事件。传入的callback需要与onCountryCodeChange接口传入的callback保持一致；不传入callback时取消当前类型的所有订阅。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[CountryCode](#class-countrycode)\>|否|None|需要取消订阅的回调函数。不填写时取消所有订阅。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offCountryCodeChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offCountryCodeChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func getLastLocation()

```cangjie
public func getLastLocation(): Location
```

**功能：** 获取上一次位置。

**需要权限：** ohos.permission.APPROXIMATELY_LOCATION

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Location|上一次的位置信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getLastLocation} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |
  | 3301200 | Failed to obtain the geographical location. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let location = getLastLocation()
    Hilog.info(0, "test", "last location: (${location.latitude}, ${location.longitude})")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func sendCommand(LocationCommand, AsyncCallback\<Unit>)

```cangjie
public func sendCommand(command: LocationCommand, callback: AsyncCallback<Unit>): Unit
```

**功能：** 给位置服务子系统的各个部件发送扩展命令。使用callback异步回调。命令发送成功时callback的err为None，否则err包含错误信息。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|command|[LocationCommand](#class-locationcommand)|是|-|指定目标场景和将要发送的命令。|
|callback|AsyncCallback\<Unit\>|是|-|用于返回命令发送结果的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.sendCommand} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let command = LocationCommand(LocationRequestScenario.Navigation, "command_1")
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        } else {
            Hilog.info(0, "test", "sendCommand success")
        }
    }
    sendCommand(command, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func getCountryCode(AsyncCallback\<CountryCode>)

```cangjie
public func getCountryCode(callback: AsyncCallback<CountryCode>): Unit
```

**功能：** 查询当前的国家码。使用callback异步回调。

**系统能力：** SystemCapability.Location.Location.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback\<[CountryCode](#class-countrycode)\>|是|-|用于返回国家码信息的回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[位置服务子系统错误码](./cj-errorcode-geo_location_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getCountryCode} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**示例：**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let callback: AsyncCallback<CountryCode> = {
        err: Option<BusinessException>, data: Option<CountryCode> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        } else if (let Some(countryCode) <- data) {
            Hilog.info(0, "test", "country: ${countryCode.country}")
        }
    }
    getCountryCode(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```
