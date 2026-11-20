# 电话服务状态监听

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 场景介绍

应用可以通过ohos.telephony.observer订阅通话、网络、信号、SIM卡状态和SIM账户信息的变化，并在不再需要通知时取消订阅。状态变化通过回调通知应用。

一次性查询网络信息见[获取蜂窝网络信息](cj-telephony-network-guidelines.md)，SIM卡类型和状态枚举见[使用SIM卡类型和状态枚举](cj-telephony-sim-guidelines.md)。

## 约束与限制

- 本文监听接口从26.1.0版本开始支持，设备需具备 `SystemCapability.Telephony.StateRegistry` 系统能力。
- 网络状态订阅需要 `ohos.permission.GET_NETWORK_INFO`，通话状态订阅需要 `ohos.permission.MANAGE_CALL_FOR_DEVICES`；信号、SIM状态和SIM账户信息变化订阅无需申请这两个权限。通话权限受系统管控，需使用符合授权要求的签名和配置。
- 省略options或传入None时，通话接口监听整体通话状态，其余四类事件默认监听卡槽0。显式传入ObserverOptions()时，slotId默认为0；这与通话接口省略options的含义不同。可用卡槽取决于设备。
- 订阅成功返回不代表回调已经到达。首次建立对应的通话或SIM状态订阅时会请求当前缓存状态，实际通知取决于系统数据；向已有的同事件、同卡槽订阅增加回调，不会再次请求首次状态。
- 保留订阅时使用的回调对象，并在不再需要通知时，将同一个对象传给off接口。省略callback或传入None会取消当前进程该事件的全部监听。已经开始执行的回调不保证立即结束。
- 修改ObserverOptions.slotId不会迁移已有监听，只影响后续订阅。修改回调结果对象也不会改变设备状态。

## 接口说明

完整接口、参数和错误码见[ohos.telephony.observer](../reference/TelephonyKit/cj-apis-telephony-observer.md)。

| 订阅 / 取消订阅 | 通知内容 | 订阅所需权限 |
| :--- | :--- | :--- |
| [onNetworkStateChange / offNetworkStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onnetworkstatechangecallback1argumentnetworkstate-observeroptions) | 网络注册状态、运营商名称、接入技术等NetworkState字段。 | ohos.permission.GET_NETWORK_INFO |
| [onSignalInfoChange / offSignalInfoChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsignalinfochangecallback1argumentarraysignalinformation-observeroptions) | SignalInformation数组，可为空；非空时可读取signalType、signalLevel和dBm。 | 无 |
| [onCallStateChange / offCallStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-oncallstatechangecallback1argumentcallstateinfo-observeroptions) | 通话状态和系统提供的号码；号码可能为空。 | ohos.permission.MANAGE_CALL_FOR_DEVICES |
| [onIccAccountInfoChange / offIccAccountInfoChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-oniccaccountinfochangecallback0argument-observeroptions) | SIM账户信息发生变化的通知，不带账户明细。 | 无 |
| [onSimStateChange / offSimStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsimstatechangecallback1argumentarraysimstatedata-observeroptions) | SimStateData数组，包含卡类型、SIM状态和锁定原因。 | 无 |

## 开发步骤

1. 网络状态监听示例需要在module.json5中声明GET_NETWORK_INFO权限。以下内容放入module节点；已有requestPermissions时，将权限项合并到原数组。权限声明方式见[声明权限](../security/AccessToken/cj-declare-permissions.md)。

   ```json
   {
     "requestPermissions": [
       { "name": "ohos.permission.GET_NETWORK_INFO" }
     ]
   }
   ```

2. 选择实际可用卡槽，下面的示例指定卡槽0。带数据的通知实现Callback1Argument，SIM账户变化通知实现Callback0Argument，并保留回调对象。Observer的数据回调接收实际数据对象，radio的AsyncCallback接收可选结果，二者参数类型不同。
3. 调用相应on接口开始订阅。在页面销毁或不再需要通知时，调用对应off接口并传入原回调对象，避免订阅后立即注销。
4. 网络、信号和账户通知可能在设备正常运行时主动上报，不需要人工操作才能触发。查询结果与观察结果的可用字段可能不同，不能将查询接口的占位值限制直接套用到监听回调。

## 示例代码

### 网络状态与信号变化

分别调用startNetworkStateChangeObserver和startSignalInfoChangeObserver开始监听，通过Hilog查看回调结果；不再需要通知时，分别调用对应stop函数。通话和SIM账户变化的完整示例见上表中的API参考链接。

<!--compile-->

```cangjie
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

### SIM卡状态变化

要接收真实设备的SIM状态，使用observer模块的[onSimStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsimstatechangecallback1argumentarraysimstatedata-observeroptions)。它从26.1.0开始支持，需要 `SystemCapability.Telephony.StateRegistry` 系统能力，不需要额外申请权限。

回调参数为 `Array<SimStateData>`。当前每条通知包含一个元素，应用仍应遍历数组：`cardType` 表示卡类型，`state` 表示状态，`reason` 表示[LockReason](../reference/TelephonyKit/cj-apis-telephony-observer.md#enum-lockreason)锁类型。当state为SimStateLocked时结合reason提示PIN、PUK等锁定原因；未锁定时，不应仅依据reason执行解锁。SIM状态通知与SIM账户变化通知是不同事件。

开始时调用startSimStateChangeObserver，示例明确订阅卡槽0。首次建立对应系统订阅时会请求当前缓存状态，但不能把on函数返回当成状态已经到达；首次通知前可按SimStateUnknown展示“正在获取”。不再需要监听时，调用stopSimStateChangeObserver，使用订阅时保留的同一个对象取消。省略offSimStateChange的callback参数会取消当前进程该事件的全部监听。

<!--compile-->

```cangjie
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
