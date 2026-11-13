# ohos.telephony.radio（网络搜索）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

无线网络模块提供网络状态、选网模式、无线接入技术等信息的查询能力。

## 导入模块

```cangjie
import kit.TelephonyKit.*
```

## 使用说明

示例使用的接口均从26.1.0版本开始支持。将示例中的导入和函数定义添加到仓颉工程，在业务代码中调用对应的示例函数。

异步接口的 `AsyncCallback<T>` 包含两个参数：错误信息 `Option<BusinessException>` 和结果 `Option<T>`。查询成功时，错误信息为 `None`、结果为 `Some(value)`；查询失败时，错误信息为 `Some(error)`、结果为 `None`。应在回调中处理查询错误，调用处的 `try/catch` 不能代替回调错误处理。

示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func getISOCountryCodeForNetworkSync(Int32)

```cangjie
public func getISOCountryCodeForNetworkSync(slotId: Int32): String
```

**功能：** 获取注册网络所在国家的ISO国家码。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| slotId | Int32 | 是 | 卡槽ID。 - 0：卡槽1。 - 1：卡槽2。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| String | 返回注册网络所在国家的ISO国家码，例如CN(中国)。如果设备没有注册任何网络，接口返回空字符串。 |

卡槽ID无效时返回空字符串。空字符串表示当前没有可用的网络国家码，不能据此区分未注册网络、无效卡槽等具体原因。

**示例：**

```cangjie
import kit.TelephonyKit.getISOCountryCodeForNetworkSync
import kit.PerformanceAnalysisKit.Hilog

func queryCountryCode(): Unit {
    let code = getISOCountryCodeForNetworkSync(0)
    if (code.isEmpty()) {
        Hilog.info(0, "TelephonyExample", "No network country code is available", [])
    } else {
        Hilog.info(0, "TelephonyExample", "ISO country code: ${code}", [])
    }
}
```

## func getNetworkSelectionMode(Int32, AsyncCallback\<NetworkSelectionMode>)

```cangjie
public func getNetworkSelectionMode(slotId: Int32, callback: AsyncCallback<NetworkSelectionMode>): Unit
```

**功能：** 获取当前选网模式。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| slotId | Int32 | 是 | 卡槽ID。 - 0：卡槽1。 - 1：卡槽2。 |
| callback | AsyncCallback\<[NetworkSelectionMode](#enum-networkselectionmode)> | 是 | 回调函数。返回当前选网模式。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

```cangjie
import kit.TelephonyKit.{NetworkSelectionMode, getNetworkSelectionMode}
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func querySelectionMode(): Unit {
    let callback: AsyncCallback<NetworkSelectionMode> = { error: ?BusinessException, data: ?NetworkSelectionMode =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample", "Selection mode: ${value.toString()}", [])
        }
    }
    try {
        getNetworkSelectionMode(0, callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func getNetworkState(Int32, AsyncCallback\<NetworkState>)

```cangjie
public func getNetworkState(slotId: Int32, callback: AsyncCallback<NetworkState>): Unit
```

**功能：** 获取指定卡槽的网络状态。

**需要权限：** ohos.permission.GET_NETWORK_INFO

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| slotId | Int32 | 是 | 卡槽ID。 - 0：卡槽1。 - 1：卡槽2。 |
| callback | AsyncCallback\<[NetworkState](#class-networkstate)> | 是 | 回调函数。返回当前网络状态。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

```cangjie
import kit.TelephonyKit.{NetworkState, RegState, getNetworkState}
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func queryNetworkState(): Unit {
    let callback: AsyncCallback<NetworkState> = { error: ?BusinessException, data: ?NetworkState =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample",
                "Registration: ${value.regState.toString()}, operator: ${value.longOperatorName}", [])
        }
    }
    try {
        getNetworkState(0, callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func getNetworkState(AsyncCallback\<NetworkState>)

```cangjie
public func getNetworkState(callback: AsyncCallback<NetworkState>): Unit
```

**功能：** 获取卡槽0的网络状态。此重载不根据主卡位置选择卡槽；如需查询主卡，应先通过getPrimarySlotId获取主卡卡槽ID，再调用带slotId参数的重载。

**需要权限：** ohos.permission.GET_NETWORK_INFO

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | AsyncCallback\<[NetworkState](#class-networkstate)> | 是 | 回调函数。返回当前网络状态。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

```cangjie
import kit.TelephonyKit.{NetworkState, RegState, getNetworkState}
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func queryDefaultNetworkState(): Unit {
    let callback: AsyncCallback<NetworkState> = { error: ?BusinessException, data: ?NetworkState =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample",
                "Registration: ${value.regState.toString()}, roaming: ${value.isRoaming}", [])
        }
    }
    try {
        getNetworkState(callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func getPrimarySlotId(AsyncCallback\<Int32>)

```cangjie
public func getPrimarySlotId(callback: AsyncCallback<Int32>): Unit
```

**功能：** 获取主卡所在卡槽的索引号。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| callback | AsyncCallback\<Int32> | 是 | 回调函数。返回主卡所在卡槽的索引号。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

```cangjie
import kit.TelephonyKit.{getPrimarySlotId}
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func queryPrimarySlot(): Unit {
    let callback: AsyncCallback<Int32> = { error: ?BusinessException, data: ?Int32 =>
        if (let Some(e) <- error) {
            Hilog.error(0, "TelephonyExample", "Query failed. Code: ${e.code}, message: ${e.message}", [])
        } else if (let Some(value) <- data) {
            Hilog.info(0, "TelephonyExample", "Primary slot ID: ${value}", [])
        }
    }
    try {
        getPrimarySlotId(callback)
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func getRadioTechSync(Int32)

```cangjie
public func getRadioTechSync(slotId: Int32): NetworkRadioTech
```

**功能：** 获取指定卡槽中SIM卡的CS域和PS域无线接入技术。CS域为电路交换域，PS域为分组交换域。

**需要权限：** ohos.permission.GET_NETWORK_INFO

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| slotId | Int32 | 是 | 卡槽ID。 - 0：卡槽1。 - 1：卡槽2。 |

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| [NetworkRadioTech](#class-networkradiotech) | 返回当前接入的CS域和PS域技术。CS域为电路交换域，PS为分组交换域。 |

当前版本中，卡槽ID无效或无线接入技术查询失败时，返回对象的csRadioTech和psRadioTech均为RadioTechnologyUnknown，而不是通过业务异常报告这些查询失败。该值也可能表示当前技术未知，不能据此判断具体错误原因。以下异常表保留接口声明的错误码约定。

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**示例：**

```cangjie
import kit.TelephonyKit.{getRadioTechSync, RadioTechnology}
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func queryRadioTechnology(): Unit {
    try {
        let technology = getRadioTechSync(0)
        if (technology.psRadioTech == RadioTechnology.RadioTechnologyUnknown &&
            technology.csRadioTech == RadioTechnology.RadioTechnologyUnknown) {
            Hilog.info(0, "TelephonyExample", "Radio technology is unknown or unavailable", [])
        } else {
            Hilog.info(0, "TelephonyExample",
                "PS: ${technology.psRadioTech.toString()}, CS: ${technology.csRadioTech.toString()}", [])
        }
    } catch (e: BusinessException) {
        Hilog.error(0, "TelephonyExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func isNRSupported()

```cangjie
public func isNRSupported(): Bool
```

**功能：** 检查当前设备是否支持NR（New Radio，5G无线接入技术）。返回值表示设备能力，不表示当前已连接5G网络。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
| :--- | :--- |
| Bool | 当前设备是否支持NR。- true：支持。 - false：不支持。 |

**示例：**

```cangjie
import kit.TelephonyKit.isNRSupported
import kit.PerformanceAnalysisKit.Hilog

func queryNrCapability(): Unit {
    let supported = isNRSupported()
    Hilog.info(0, "TelephonyExample", "NR supported: ${supported}", [])
}
```

## class NetworkRadioTech

该对象由getRadioTechSync返回。修改属性只改变当前对象，不会改变设备的无线接入技术。

```cangjie
public class NetworkRadioTech {}
```

**功能：** 网络中PS（分组交换域）和CS（电路交换域）的无线接入技术。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop csRadioTech

```cangjie
public mut prop csRadioTech: RadioTechnology
```

**功能：** CS无线接入技术。

**类型：** [RadioTechnology](#enum-radiotechnology)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop psRadioTech

```cangjie
public mut prop psRadioTech: RadioTechnology
```

**功能：** PS无线接入技术。

**类型：** [RadioTechnology](#enum-radiotechnology)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## class NetworkState

该对象由getNetworkState返回。修改属性只改变当前对象，不会修改设备的网络配置或注册状态。

```cangjie
public class NetworkState {}
```

**功能：** 网络注册状态。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop cfgTech

```cangjie
public mut prop cfgTech: RadioTechnology
```

**功能：** 设备的无线接入技术。

**类型：** [RadioTechnology](#enum-radiotechnology)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop isCaActive

```cangjie
public mut prop isCaActive: Bool
```

**功能：** CA（Carrier Aggregation，载波聚合）的状态。- true：CA已激活。- false：CA未激活。当前getNetworkState返回的该属性为false，不能据此判断设备的实际CA状态。

**类型：** Bool

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop isEmergency

```cangjie
public mut prop isEmergency: Bool
```

**功能：** 此设备是否只允许拨打紧急呼叫。

**类型：** Bool

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop isRoaming

```cangjie
public mut prop isRoaming: Bool
```

**功能：** 是否处于漫游状态。 - true：处于漫游状态。 - false：未处于漫游状态。

**类型：** Bool

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop longOperatorName

```cangjie
public mut prop longOperatorName: String
```

**功能：** 注册网络的长运营商名称。

**类型：** String

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop nsaState

```cangjie
public mut prop nsaState: NsaState
```

**功能：** 设备的NSA（非独立组网）网络注册状态。当前getNetworkState返回的该属性为NsaStateNotSupport，不能据此判断设备的实际NSA注册状态。

**类型：** [NsaState](#enum-nsastate)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop plmnNumeric

```cangjie
public mut prop plmnNumeric: String
```

**功能：** 注册网络的PLMN(Public Land Mobile Network，公共陆地移动网络)码。

**类型：** String

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop regState

```cangjie
public mut prop regState: RegState
```

**功能：** 设备的网络注册状态。

**类型：** [RegState](#enum-regstate)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop shortOperatorName

```cangjie
public mut prop shortOperatorName: String
```

**功能：** 注册网络的短运营商名称。

**类型：** String

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## class SignalInformation

该类型描述信号强度信息。当前模块未提供公开构造函数和信号强度查询函数。修改属性只改变当前对象，不会改变设备的信号强度。

```cangjie
public class SignalInformation {}
```

**功能：** 网络信号强度信息对象。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop dBm

```cangjie
public mut prop dBm: Int32
```

**功能：** 网络信号强度，范围为[-140, 140]。

**类型：** Int32

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop signalLevel

```cangjie
public mut prop signalLevel: Int32
```

**功能：** 网络信号强度等级，范围为[0, 5]。

**类型：** Int32

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### prop signalType

```cangjie
public mut prop signalType: NetworkType
```

**功能：** 网络信号强度类型。

**类型：** [NetworkType](#enum-networktype)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum NetworkSelectionMode

```cangjie
public enum NetworkSelectionMode {
    | NetworkSelectionAutomatic
    | NetworkSelectionManual
    | NetworkSelectionUnknown
    | ...
}
```

**功能：** 选网模式。

**扩展：**

- [extend NetworkSelectionMode <: ToString](#extend-networkselectionmode--tostring)
- [extend NetworkSelectionMode <: Equatable\<NetworkSelectionMode>](#extend-networkselectionmode--equatablenetworkselectionmode)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkSelectionAutomatic

```cangjie
NetworkSelectionAutomatic
```

**功能：** 自动选网模式。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkSelectionManual

```cangjie
NetworkSelectionManual
```

**功能：** 手动选网模式。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkSelectionUnknown

```cangjie
NetworkSelectionUnknown
```

**功能：** 未知选网模式。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum NetworkType

```cangjie
public enum NetworkType {
    | NetworkTypeCdma
    | NetworkTypeGsm
    | NetworkTypeLte
    | NetworkTypeNr
    | NetworkTypeTdscdma
    | NetworkTypeUnknown
    | NetworkTypeWcdma
    | ...
}
```

**功能：** 网络类型。

**扩展：**

- [extend NetworkType <: ToString](#extend-networktype--tostring)
- [extend NetworkType <: Equatable\<NetworkType>](#extend-networktype--equatablenetworktype)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeCdma

```cangjie
NetworkTypeCdma
```

**功能：** 网络类型为CDMA(Code Division Multiple Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeGsm

```cangjie
NetworkTypeGsm
```

**功能：** 网络类型为GSM(Global System For Mobile Communication)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeLte

```cangjie
NetworkTypeLte
```

**功能：** 网络类型为LTE(Long Term Evolution)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeNr

```cangjie
NetworkTypeNr
```

**功能：** 网络类型为NR(New Radio)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeTdscdma

```cangjie
NetworkTypeTdscdma
```

**功能：** 网络类型为TDSCDMA(TimeDivision-Synchronous Code Division Multiple Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeUnknown

```cangjie
NetworkTypeUnknown
```

**功能：** 未知网络类型。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NetworkTypeWcdma

```cangjie
NetworkTypeWcdma
```

**功能：** 网络类型为WCDMA(Wideband Code Division Multiple Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum NsaState

```cangjie
public enum NsaState {
    | NsaStateConnectedDetect
    | NsaStateDualConnected
    | NsaStateIdleDetect
    | NsaStateNoDetect
    | NsaStateNotSupport
    | NsaStateSaAttached
    | ...
}
```

**功能：** 非独立组网状态。

**扩展：**

- [extend NsaState <: ToString](#extend-nsastate--tostring)
- [extend NsaState <: Equatable\<NsaState>](#extend-nsastate--equatablensastate)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateConnectedDetect

```cangjie
NsaStateConnectedDetect
```

**功能：** 设备在LTE小区下连接到LTE网络支持NSA和NR覆盖检测。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateDualConnected

```cangjie
NsaStateDualConnected
```

**功能：** 设备在支持NSA的LTE小区下连接到LTE + NR网络。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateIdleDetect

```cangjie
NsaStateIdleDetect
```

**功能：** 支持NSA和NR覆盖检测的LTE小区下设备处于空闲状态。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateNoDetect

```cangjie
NsaStateNoDetect
```

**功能：** 在支持NSA但不支持NR覆盖检测的LTE小区下，设备处于空闲状态。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateNotSupport

```cangjie
NsaStateNotSupport
```

**功能：** 设备在不支持NSA的LTE小区下处于空闲状态或连接状态。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### NsaStateSaAttached

```cangjie
NsaStateSaAttached
```

**功能：** 设备在5GC（5G核心网）附着时在NG-RAN（下一代无线接入网）小区下空闲或连接到NG-RAN小区。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum RadioTechnology

```cangjie
public enum RadioTechnology {
    | RadioTechnology1xrtt
    | RadioTechnologyEhrpd
    | RadioTechnologyEvdo
    | RadioTechnologyGsm
    | RadioTechnologyHspa
    | RadioTechnologyHspap
    | RadioTechnologyIwlan
    | RadioTechnologyLte
    | RadioTechnologyLteCa
    | RadioTechnologyNr
    | RadioTechnologyTdScdma
    | RadioTechnologyUnknown
    | RadioTechnologyWcdma
    | ...
}
```

**功能：** 无线接入技术。

**扩展：**

- [extend RadioTechnology <: ToString](#extend-radiotechnology--tostring)
- [extend RadioTechnology <: Equatable\<RadioTechnology>](#extend-radiotechnology--equatableradiotechnology)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnology1xrtt

```cangjie
RadioTechnology1xrtt
```

**功能：** 无线接入技术1XRTT(Single-Carrier Radio Transmission Technology)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyEhrpd

```cangjie
RadioTechnologyEhrpd
```

**功能：** 无线接入技术EHRPD(Evolved High Rate Packet Data)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyEvdo

```cangjie
RadioTechnologyEvdo
```

**功能：** 无线接入技术EVDO(Evolution Data Only)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyGsm

```cangjie
RadioTechnologyGsm
```

**功能：** 无线接入技术GSM(Global System For Mobile Communication)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyHspa

```cangjie
RadioTechnologyHspa
```

**功能：** 无线接入技术HSPA(High Speed Packet Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyHspap

```cangjie
RadioTechnologyHspap
```

**功能：** 无线接入技术HSPAP(High Speed Packet Access+)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyIwlan

```cangjie
RadioTechnologyIwlan
```

**功能：** 无线接入技术IWLAN(Interworking Wireless LAN)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyLte

```cangjie
RadioTechnologyLte
```

**功能：** 无线接入技术LTE(Long Term Evolution)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyLteCa

```cangjie
RadioTechnologyLteCa
```

**功能：** 无线接入技术LTE_CA(Long Term Evolution_Carrier Aggregation)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyNr

```cangjie
RadioTechnologyNr
```

**功能：** 无线接入技术NR(New Radio)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyTdScdma

```cangjie
RadioTechnologyTdScdma
```

**功能：** 无线接入技术TD_SCDMA(TimeDivision-Synchronous Code Division Multiple Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyUnknown

```cangjie
RadioTechnologyUnknown
```

**功能：** 未知无线接入技术(RAT)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RadioTechnologyWcdma

```cangjie
RadioTechnologyWcdma
```

**功能：** 无线接入技术WCDMA(Wideband Code Division Multiple Access)。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum RegState

```cangjie
public enum RegState {
    | RegStateEmergencyCallOnly
    | RegStateInService
    | RegStateNoService
    | RegStatePowerOff
    | ...
}
```

**功能：** 网络注册状态。

**扩展：**

- [extend RegState <: ToString](#extend-regstate--tostring)
- [extend RegState <: Equatable\<RegState>](#extend-regstate--equatableregstate)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RegStateEmergencyCallOnly

```cangjie
RegStateEmergencyCallOnly
```

**功能：** 设备只能使用紧急呼叫业务。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RegStateInService

```cangjie
RegStateInService
```

**功能：** 设备可以正常使用服务，包括数据业务、短信、通话等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RegStateNoService

```cangjie
RegStateNoService
```

**功能：** 设备不能使用任何服务，包括数据业务、短信、通话等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### RegStatePowerOff

```cangjie
RegStatePowerOff
```

**功能：** 蜂窝无线电已关闭，modem下电，无法和网侧进行通信。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## extend NetworkSelectionMode <: Equatable\<NetworkSelectionMode>

```cangjie
extend NetworkSelectionMode <: Equatable<NetworkSelectionMode>
```

**功能：** 为 NetworkSelectionMode 类型扩展 Equatable\<NetworkSelectionMode> 接口，支持相等比较。

**被扩展类型：**

- [NetworkSelectionMode](#enum-networkselectionmode)

**扩展接口：**

- Equatable\<[NetworkSelectionMode](#enum-networkselectionmode)>

### func ==(NetworkSelectionMode)

```cangjie
public operator func ==(other: NetworkSelectionMode): Bool
```

**功能：** 判断两个 NetworkSelectionMode 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NetworkSelectionMode](#enum-networkselectionmode) | 是 | 需要比较的NetworkSelectionMode对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NetworkSelectionMode 相等则返回 true，否则返回 false。|

### func !=(NetworkSelectionMode)

```cangjie
public operator func !=(other: NetworkSelectionMode): Bool
```

**功能：** 判断两个 NetworkSelectionMode 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NetworkSelectionMode](#enum-networkselectionmode) | 是 | 需要比较的NetworkSelectionMode对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NetworkSelectionMode 不相等则返回 true，否则返回 false。|

## extend NetworkSelectionMode <: ToString

```cangjie
extend NetworkSelectionMode <: ToString
```

**功能：** 为 NetworkSelectionMode 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [NetworkSelectionMode](#enum-networkselectionmode)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend NetworkType <: Equatable\<NetworkType>

```cangjie
extend NetworkType <: Equatable<NetworkType>
```

**功能：** 为 NetworkType 类型扩展 Equatable\<NetworkType> 接口，支持相等比较。

**被扩展类型：**

- [NetworkType](#enum-networktype)

**扩展接口：**

- Equatable\<[NetworkType](#enum-networktype)>

### func ==(NetworkType)

```cangjie
public operator func ==(other: NetworkType): Bool
```

**功能：** 判断两个 NetworkType 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NetworkType](#enum-networktype) | 是 | 需要比较的NetworkType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NetworkType 相等则返回 true，否则返回 false。|

### func !=(NetworkType)

```cangjie
public operator func !=(other: NetworkType): Bool
```

**功能：** 判断两个 NetworkType 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NetworkType](#enum-networktype) | 是 | 需要比较的NetworkType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NetworkType 不相等则返回 true，否则返回 false。|

## extend NetworkType <: ToString

```cangjie
extend NetworkType <: ToString
```

**功能：** 为 NetworkType 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [NetworkType](#enum-networktype)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend NsaState <: Equatable\<NsaState>

```cangjie
extend NsaState <: Equatable<NsaState>
```

**功能：** 为 NsaState 类型扩展 Equatable\<NsaState> 接口，支持相等比较。

**被扩展类型：**

- [NsaState](#enum-nsastate)

**扩展接口：**

- Equatable\<[NsaState](#enum-nsastate)>

### func ==(NsaState)

```cangjie
public operator func ==(other: NsaState): Bool
```

**功能：** 判断两个 NsaState 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NsaState](#enum-nsastate) | 是 | 需要比较的NsaState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NsaState 相等则返回 true，否则返回 false。|

### func !=(NsaState)

```cangjie
public operator func !=(other: NsaState): Bool
```

**功能：** 判断两个 NsaState 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [NsaState](#enum-nsastate) | 是 | 需要比较的NsaState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 NsaState 不相等则返回 true，否则返回 false。|

## extend NsaState <: ToString

```cangjie
extend NsaState <: ToString
```

**功能：** 为 NsaState 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [NsaState](#enum-nsastate)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend RadioTechnology <: Equatable\<RadioTechnology>

```cangjie
extend RadioTechnology <: Equatable<RadioTechnology>
```

**功能：** 为 RadioTechnology 类型扩展 Equatable\<RadioTechnology> 接口，支持相等比较。

**被扩展类型：**

- [RadioTechnology](#enum-radiotechnology)

**扩展接口：**

- Equatable\<[RadioTechnology](#enum-radiotechnology)>

### func ==(RadioTechnology)

```cangjie
public operator func ==(other: RadioTechnology): Bool
```

**功能：** 判断两个 RadioTechnology 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [RadioTechnology](#enum-radiotechnology) | 是 | 需要比较的RadioTechnology对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 RadioTechnology 相等则返回 true，否则返回 false。|

### func !=(RadioTechnology)

```cangjie
public operator func !=(other: RadioTechnology): Bool
```

**功能：** 判断两个 RadioTechnology 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [RadioTechnology](#enum-radiotechnology) | 是 | 需要比较的RadioTechnology对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 RadioTechnology 不相等则返回 true，否则返回 false。|

## extend RadioTechnology <: ToString

```cangjie
extend RadioTechnology <: ToString
```

**功能：** 为 RadioTechnology 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [RadioTechnology](#enum-radiotechnology)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend RegState <: Equatable\<RegState>

```cangjie
extend RegState <: Equatable<RegState>
```

**功能：** 为 RegState 类型扩展 Equatable\<RegState> 接口，支持相等比较。

**被扩展类型：**

- [RegState](#enum-regstate)

**扩展接口：**

- Equatable\<[RegState](#enum-regstate)>

### func ==(RegState)

```cangjie
public operator func ==(other: RegState): Bool
```

**功能：** 判断两个 RegState 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [RegState](#enum-regstate) | 是 | 需要比较的RegState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 RegState 相等则返回 true，否则返回 false。|

### func !=(RegState)

```cangjie
public operator func !=(other: RegState): Bool
```

**功能：** 判断两个 RegState 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [RegState](#enum-regstate) | 是 | 需要比较的RegState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 RegState 不相等则返回 true，否则返回 false。|

## extend RegState <: ToString

```cangjie
extend RegState <: ToString
```

**功能：** 为 RegState 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [RegState](#enum-regstate)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|
