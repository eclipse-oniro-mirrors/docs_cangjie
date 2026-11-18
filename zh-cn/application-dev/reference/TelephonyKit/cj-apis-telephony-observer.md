# ohos.telephony.observer（电话服务状态监听）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

电话服务状态监听模块提供通话状态、网络状态、信号信息、SIM卡状态等变化的订阅与取消订阅能力。

## 导入模块

```cangjie
import kit.TelephonyKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## 订阅与取消订阅

- 本模块从26.1.0版本开始支持，设备需具备 `SystemCapability.Telephony.StateRegistry` 系统能力。通话订阅需要 `ohos.permission.MANAGE_CALL_FOR_DEVICES`，网络状态订阅需要 `ohos.permission.GET_NETWORK_INFO`；信号、SIM状态和SIM账户变化订阅不需要额外申请这两项权限。通话权限受系统管控，应用需使用符合授权要求的签名和配置。
- 省略 `options` 或传入 `None` 时，通话接口监听整体通话状态，其他四类接口监听卡槽0。`ObserverOptions()` 的 `slotId` 默认为0，因此通话接口显式传入 `ObserverOptions()` 与省略 `options` 的监听范围不同。可用卡槽取决于设备能力。
- 状态通过回调通知。应保留订阅时使用的回调对象，在不再需要监听时将同一对象传给 `offXxx(callback: callbackObject)`；省略参数或传入 `None` 时取消当前进程内该事件的全部监听。不同事件分别管理。
- 订阅成功返回不表示本次已收到回调。通话和SIM状态首次建立对应系统订阅时会请求当前缓存状态，实际通知依赖系统数据；网络、信号和账户也可能因正常系统变化主动通知，不要求先有人工操作。相同事件和卡槽已有订阅时，追加回调不会重新请求初始状态。
- 修改 `ObserverOptions.slotId` 不会迁移已经注册的监听，只影响后续使用该对象发起的订阅。修改回调结果对象的属性只改变当前对象，不会修改设备通话或SIM状态。
- `offXxx` 不承诺等待所有已经开始的回调执行结束。示例将开始监听和停止监听分为独立函数：在业务需要时调用 `startXxxObserver`，页面销毁或不再需要监听时调用 `stopXxxObserver`，不要在订阅后立即取消并期待收到状态变化。

## func offCallStateChange(?Callback1Argument\<CallStateInfo>)

```cangjie
public func offCallStateChange(callback!: ?Callback1Argument<CallStateInfo> = None): Unit
```

**功能：** 取消订阅通话状态变化事件。

**需要权限：** ohos.permission.MANAGE_CALL_FOR_DEVICES

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<[CallStateInfo](#class-callstateinfo)> | 否 | None | **命名参数。** 传入订阅时的同一个回调对象，只取消该对象的监听；省略或传入None时取消该事件的全部监听。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8800001 | Invalid parameter value. |
  | 8800002 | Service connection failed. |
  | 8800003 | System internal error. |
  | 8800999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.offCallStateChange
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func stopAllCallStateChangeObservers(): Unit {
    try {
        offCallStateChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func offIccAccountInfoChange(?Callback0Argument)

```cangjie
public func offIccAccountInfoChange(callback!: ?Callback0Argument = None): Unit
```

**功能：** 取消订阅ICC账户信息变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback0Argument | 否 | None | **命名参数。** 传入订阅时的同一个回调对象，只取消该对象的监听；省略或传入None时取消该事件的全部监听。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.offIccAccountInfoChange
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func stopAllIccAccountInfoChangeObservers(): Unit {
    try {
        offIccAccountInfoChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func offNetworkStateChange(?Callback1Argument\<NetworkState>)

```cangjie
public func offNetworkStateChange(callback!: ?Callback1Argument<NetworkState> = None): Unit
```

**功能：** 取消订阅网络状态变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<NetworkState> | 否 | None | **命名参数。** 传入订阅时的同一个回调对象，只取消该对象的监听；省略或传入None时取消该事件的全部监听。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.offNetworkStateChange
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func stopAllNetworkStateChangeObservers(): Unit {
    try {
        offNetworkStateChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func offSignalInfoChange(?Callback1Argument\<Array\<SignalInformation>>)

```cangjie
public func offSignalInfoChange(callback!: ?Callback1Argument<Array<SignalInformation>> = None): Unit
```

**功能：** 取消订阅信号信息变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<Array\<SignalInformation>> | 否 | None | **命名参数。** 传入订阅时的同一个回调对象，只取消该对象的监听；省略或传入None时取消该事件的全部监听。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.offSignalInfoChange
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func stopAllSignalInfoChangeObservers(): Unit {
    try {
        offSignalInfoChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func offSimStateChange(?Callback1Argument\<Array\<SimStateData>>)

```cangjie
public func offSimStateChange(callback!: ?Callback1Argument<Array<SimStateData>> = None): Unit
```

**功能：** 取消订阅SIM卡状态变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<Array\<[SimStateData](#class-simstatedata)>> | 否 | None | **命名参数。** 传入订阅时的同一个回调对象，只取消该对象的监听；省略或传入None时取消该事件的全部监听。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.offSimStateChange
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

func stopAllSimStateChangeObservers(): Unit {
    try {
        offSimStateChange()
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func onCallStateChange(Callback1Argument\<CallStateInfo>, ?ObserverOptions)

```cangjie
public func onCallStateChange(callback: Callback1Argument<CallStateInfo>, options!: ?ObserverOptions = None): Unit
```

**功能：** 订阅通话状态变化事件。状态变化通过回调异步通知。

**需要权限：** ohos.permission.MANAGE_CALL_FOR_DEVICES

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<[CallStateInfo](#class-callstateinfo)> | 是 | - | 接收通话状态和底层提供的号码；号码可能为空字符串。 |
| options | ?[ObserverOptions](#class-observeroptions) | 否 | None | **命名参数。** 订阅选项；None表示监听整体通话状态。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8800001 | Invalid parameter value. |
  | 8800002 | Service connection failed. |
  | 8800003 | System internal error. |
  | 8800999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.*
import kit.CangjieKit.{BusinessException, Callback1Argument}
import kit.PerformanceAnalysisKit.Hilog

class CallStateCallback <: Callback1Argument<CallStateInfo> {
    init() {}

    public func invoke(error: ?BusinessException, value: CallStateInfo): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
            return
        }
        Hilog.info(0, "ObserverExample", "Call state: ${value.state.toString()}", [])
    }
}

let callStateCallback = CallStateCallback()

func startCallStateChangeObserver(): Unit {
    try {
        onCallStateChange(callStateCallback, options: ObserverOptions(slotId: 0))
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func stopCallStateChangeObserver(): Unit {
    try {
        offCallStateChange(callback: callStateCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func onIccAccountInfoChange(Callback0Argument, ?ObserverOptions)

```cangjie
public func onIccAccountInfoChange(callback: Callback0Argument, options!: ?ObserverOptions = None): Unit
```

**功能：** 订阅ICC账户信息变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback0Argument | 是 | - | 接收SIM账户变化通知，不携带账户明细。 |
| options | ?[ObserverOptions](#class-observeroptions) | 否 | None | **命名参数。** 订阅选项；None表示监听卡槽0。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.*
import kit.CangjieKit.{BusinessException, Callback0Argument}
import kit.PerformanceAnalysisKit.Hilog

class IccAccountCallback <: Callback0Argument {
    init() {}

    public func invoke(error: ?BusinessException): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
            return
        }
        Hilog.info(0, "ObserverExample", "SIM account information changed", [])
    }
}

let iccAccountCallback = IccAccountCallback()

func startIccAccountInfoChangeObserver(): Unit {
    try {
        onIccAccountInfoChange(iccAccountCallback, options: ObserverOptions(slotId: 0))
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func stopIccAccountInfoChangeObserver(): Unit {
    try {
        offIccAccountInfoChange(callback: iccAccountCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func onNetworkStateChange(Callback1Argument\<NetworkState>, ?ObserverOptions)

```cangjie
public func onNetworkStateChange(callback: Callback1Argument<NetworkState>, options!: ?ObserverOptions = None): Unit
```

**功能：** 订阅网络状态变化事件。

**需要权限：** ohos.permission.GET_NETWORK_INFO

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<NetworkState> | 是 | - | 用于接收状态变化的回调对象。 |
| options | ?[ObserverOptions](#class-observeroptions) | 否 | None | **命名参数。** 订阅选项；None表示监听卡槽0。 |

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

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.*
import kit.CangjieKit.{BusinessException, Callback1Argument}
import kit.PerformanceAnalysisKit.Hilog

class NetworkStateCallback <: Callback1Argument<NetworkState> {
    init() {}

    public func invoke(error: ?BusinessException, value: NetworkState): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
            return
        }
        Hilog.info(0, "ObserverExample", "Registration: ${value.regState.toString()}, roaming: ${value.isRoaming}", [])
    }
}

let networkStateCallback = NetworkStateCallback()

func startNetworkStateChangeObserver(): Unit {
    try {
        onNetworkStateChange(networkStateCallback, options: ObserverOptions(slotId: 0))
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func stopNetworkStateChangeObserver(): Unit {
    try {
        offNetworkStateChange(callback: networkStateCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func onSignalInfoChange(Callback1Argument\<Array\<SignalInformation>>, ?ObserverOptions)

```cangjie
public func onSignalInfoChange(callback: Callback1Argument<Array<SignalInformation>>, options!: ?ObserverOptions = None): Unit
```

**功能：** 订阅信号信息变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<Array\<SignalInformation>> | 是 | - | 接收信号信息数组，数组允许为空。 |
| options | ?[ObserverOptions](#class-observeroptions) | 否 | None | **命名参数。** 订阅选项；None表示监听卡槽0。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.*
import kit.CangjieKit.{BusinessException, Callback1Argument}
import kit.PerformanceAnalysisKit.Hilog

class SignalInfoCallback <: Callback1Argument<Array<SignalInformation>> {
    init() {}

    public func invoke(error: ?BusinessException, value: Array<SignalInformation>): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
            return
        }
        Hilog.info(0, "ObserverExample", "Signal count: ${value.size}", [])
        for (item in value) {
            Hilog.info(0, "ObserverExample",
                "Type: ${item.signalType.toString()}, level: ${item.signalLevel}, dBm: ${item.dBm}", [])
        }
    }
}

let signalInfoCallback = SignalInfoCallback()

func startSignalInfoChangeObserver(): Unit {
    try {
        onSignalInfoChange(signalInfoCallback, options: ObserverOptions(slotId: 0))
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func stopSignalInfoChangeObserver(): Unit {
    try {
        offSignalInfoChange(callback: signalInfoCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## func onSimStateChange(Callback1Argument\<Array\<SimStateData>>, ?ObserverOptions)

```cangjie
public func onSimStateChange(callback: Callback1Argument<Array<SimStateData>>, options!: ?ObserverOptions = None): Unit
```

**功能：** 订阅SIM卡状态变化事件。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<Array\<[SimStateData](#class-simstatedata)>> | 是 | - | 接收SIM状态数组；当前实现每条通知包含一个元素，应用应遍历处理。 |
| options | ?[ObserverOptions](#class-observeroptions) | 否 | None | **命名参数。** 订阅选项；None表示监听卡槽0。 |

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[电话子系统错误码](./cj-errorcode-telephony.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**示例：**

<!--compile-->

```cangjie
// index.cj

import kit.TelephonyKit.*
import kit.CangjieKit.{BusinessException, Callback1Argument}
import kit.PerformanceAnalysisKit.Hilog

class SimStateCallback <: Callback1Argument<Array<SimStateData>> {
    init() {}

    public func invoke(error: ?BusinessException, value: Array<SimStateData>): Unit {
        if (let Some(e) <- error) {
            Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
            return
        }
        for (item in value) {
            Hilog.info(0, "ObserverExample",
                "Card: ${item.cardType.toString()}, state: ${item.state.toString()}, reason: ${item.reason.toString()}", [])
        }
    }
}

let simStateCallback = SimStateCallback()

func startSimStateChangeObserver(): Unit {
    try {
        onSimStateChange(simStateCallback, options: ObserverOptions(slotId: 0))
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}

func stopSimStateChangeObserver(): Unit {
    try {
        offSimStateChange(callback: simStateCallback)
    } catch (e: BusinessException) {
        Hilog.error(0, "ObserverExample", "Code: ${e.code}, message: ${e.message}", [])
    }
}
```

## class CallStateInfo

```cangjie
public class CallStateInfo {}
```

该类由状态回调提供，不提供公开构造函数。

**功能：** 通话状态相关信息。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop number

```cangjie
public mut prop number: String
```

**功能：** 电话号码，由系统根据授权及底层上报提供，可能为空字符串。示例不输出明文号码。

**类型：** String

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop state

```cangjie
public mut prop state: CallState
```

**功能：** 通话状态。

**类型：** CallState

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

## class ObserverOptions

```cangjie
public class ObserverOptions {
    public init(slotId!: ?Int32 = None)
}
```

**功能：** 电话相关事件订阅参数可选项。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop slotId

```cangjie
public mut prop slotId: Int32
```

**功能：** 卡槽ID。0表示卡槽1，1表示卡槽2，实际可用卡槽由设备能力决定。默认值为0。

**类型：** Int32

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### init(?Int32)

```cangjie
public init(slotId!: ?Int32 = None)
```

**功能：** ObserverOptions的构造函数。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| slotId | ?Int32 | 否 | None | **命名参数。** 卡槽ID。None在构造时转换为0。 |

## class SimStateData

```cangjie
public class SimStateData {}
```

该类由状态回调提供，不提供公开构造函数。

**功能：** SIM卡类型和状态。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop cardType

```cangjie
public mut prop cardType: CardType
```

**功能：** SIM卡类型，参考[CardType](cj-apis-telephony-sim.md#enum-cardtype)。

**类型：** CardType

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop reason

```cangjie
public mut prop reason: LockReason
```

**功能：** SIM卡锁类型。当state为SimStateLocked时结合该属性判断锁定原因；其他状态下不应仅依据reason执行解锁。

**类型：** [LockReason](#enum-lockreason)

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### prop state

```cangjie
public mut prop state: SimState
```

**功能：** SIM卡状态。

**类型：** SimState

**读写能力：** 读写

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

## enum LockReason

```cangjie
public enum LockReason {
    | SimNone
    | SimPcPin
    | SimPcPuk
    | SimPin
    | SimPnPin
    | SimPnPuk
    | SimPpPin
    | SimPpPuk
    | SimPuPin
    | SimPuPuk
    | SimPuk
    | SimSimPin
    | SimSimPuk
    | ...
}
```

**功能：** SIM卡锁类型。当state为SimStateLocked时结合该属性判断锁定原因；其他状态下不应仅依据reason执行解锁。

**扩展：**

- [extend LockReason <: ToString](#extend-lockreason--tostring)
- [extend LockReason <: Equatable\<LockReason>](#extend-lockreason--equatablelockreason)

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimNone

```cangjie
SimNone
```

**功能：** 无锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPcPin

```cangjie
SimPcPin
```

**功能：** 组织PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPcPuk

```cangjie
SimPcPuk
```

**功能：** 组织PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPin

```cangjie
SimPin
```

**功能：** PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPnPin

```cangjie
SimPnPin
```

**功能：** 网络PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPnPuk

```cangjie
SimPnPuk
```

**功能：** 网络PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPpPin

```cangjie
SimPpPin
```

**功能：** 服务提供商PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPpPuk

```cangjie
SimPpPuk
```

**功能：** 服务提供商PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPuPin

```cangjie
SimPuPin
```

**功能：** 子网PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPuPuk

```cangjie
SimPuPuk
```

**功能：** 子网PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimPuk

```cangjie
SimPuk
```

**功能：** PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimSimPin

```cangjie
SimSimPin
```

**功能：** SIM PIN锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

### SimSimPuk

```cangjie
SimSimPuk
```

**功能：** SIM PUK锁。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

## extend LockReason <: Equatable\<LockReason>

```cangjie
extend LockReason <: Equatable<LockReason>
```

**功能：** 为 LockReason 类型扩展 Equatable\<LockReason> 接口，支持相等比较。

**被扩展类型：**

- [LockReason](#enum-lockreason)

**扩展接口：**

- Equatable\<[LockReason](#enum-lockreason)>

### func ==(LockReason)

```cangjie
public operator func ==(other: LockReason): Bool
```

**功能：** 判断两个 LockReason 是否相等。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [LockReason](#enum-lockreason) | 是 | 需要比较的LockReason对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 LockReason 相等则返回 true，否则返回 false。|

### func !=(LockReason)

```cangjie
public operator func !=(other: LockReason): Bool
```

**功能：** 判断两个 LockReason 是否不相等。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [LockReason](#enum-lockreason) | 是 | 需要比较的LockReason对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 LockReason 不相等则返回 true，否则返回 false。|

## extend LockReason <: ToString

```cangjie
extend LockReason <: ToString
```

**功能：** 为 LockReason 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [LockReason](#enum-lockreason)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.StateRegistry

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|
