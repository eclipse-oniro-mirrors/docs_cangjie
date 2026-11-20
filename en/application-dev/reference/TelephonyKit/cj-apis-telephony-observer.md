# ohos.telephony.observer (Telephony Status Observer)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The telephony status observer module provides the capability to subscribe to and unsubscribe from changes in call state, network state, signal information, SIM card state, and more.

## Import Module

```cangjie
import kit.TelephonyKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Sample Code Notes](../cj-development-intro.md#cangjie-sample-code-notes).

## Subscribing and Unsubscribing

- This module is available since 26.1.0 and requires `SystemCapability.Telephony.StateRegistry`. Call state subscriptions require `ohos.permission.MANAGE_CALL_FOR_DEVICES`, and network state subscriptions require `ohos.permission.GET_NETWORK_INFO`. Signal, SIM state, and SIM account change subscriptions do not require these two permissions. The call permission is system-controlled; the application must use a signing configuration that is authorized to request it.
- If `options` is omitted or `None`, the call API observes the overall call state; the other four event APIs observe slot 0. `ObserverOptions()` defaults `slotId` to 0, so explicitly passing this object to the call API differs from omitting `options`. Available slots depend on the device.
- State changes are delivered through callbacks. Retain the callback object used for subscription and pass the same object to `offXxx(callback: callbackObject)` when observation is no longer needed. Omitting the argument or passing `None` removes all listeners for that event in the current process. Different event types are managed separately.
- A successful subscription return does not mean that a callback has arrived. The first underlying call or SIM state subscription requests the cached state; delivery depends on the system data. Network, signal, and account notifications can also occur during normal operation without a manual action. Adding a callback to an existing subscription for the same event and slot does not request another initial state.
- Changing `ObserverOptions.slotId` does not move an existing subscription; it affects subsequent subscriptions using that object. Changing properties of a callback result changes only that object, not the device call or SIM state.
- `offXxx` does not guarantee that all callbacks already in progress have finished. Examples separate starting and stopping observation: call `startXxxObserver` when needed and `stopXxxObserver` when the page is destroyed or observation is no longer required. Do not immediately unsubscribe after subscribing and expect to observe a change.

## func offCallStateChange(?Callback1Argument\<CallStateInfo>)

```cangjie
public func offCallStateChange(callback!: ?Callback1Argument<CallStateInfo> = None): Unit
```

**Description:** Unsubscribes from call state change events.

**Permission Required:** ohos.permission.MANAGE_CALL_FOR_DEVICES

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<[CallStateInfo](#class-callstateinfo)> | No | None | **Named parameter.** Pass the same callback object used for subscription to remove only its listeners. Omit the argument or pass None to remove all listeners for this event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8800001 | Invalid parameter value. |
  | 8800002 | Service connection failed. |
  | 8800003 | System internal error. |
  | 8800999 | Unknown error. |

**Example:**

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

**Description:** Unsubscribes from ICC account information change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback0Argument | No | None | **Named parameter.** Pass the same callback object used for subscription to remove only its listeners. Omit the argument or pass None to remove all listeners for this event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Unsubscribes from network state change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<NetworkState> | No | None | **Named parameter.** Pass the same callback object used for subscription to remove only its listeners. Omit the argument or pass None to remove all listeners for this event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Unsubscribes from signal information change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<Array\<SignalInformation>> | No | None | **Named parameter.** Pass the same callback object used for subscription to remove only its listeners. Omit the argument or pass None to remove all listeners for this event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Unsubscribes from SIM card state change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | ?Callback1Argument\<Array\<[SimStateData](#class-simstatedata)>> | No | None | **Named parameter.** Pass the same callback object used for subscription to remove only its listeners. Omit the argument or pass None to remove all listeners for this event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Subscribes to call state change events. State changes are delivered asynchronously through the callback.

**Permission Required:** ohos.permission.MANAGE_CALL_FOR_DEVICES

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<[CallStateInfo](#class-callstateinfo)> | Yes | - | Receives the call state and the number supplied by the system; the number may be empty. |
| options | ?[ObserverOptions](#class-observeroptions) | No | None | **Named parameter.** Subscription options; None observes the overall call state. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8800001 | Invalid parameter value. |
  | 8800002 | Service connection failed. |
  | 8800003 | System internal error. |
  | 8800999 | Unknown error. |

**Example:**

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

**Description:** Subscribes to ICC account information change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback0Argument | Yes | - | Receives a SIM account change notification without account details. |
| options | ?[ObserverOptions](#class-observeroptions) | No | None | **Named parameter.** Subscription options; None observes slot 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Subscribes to network state change events.

**Permission Required:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<NetworkState> | Yes | - | Callback object used to receive state changes. |
| options | ?[ObserverOptions](#class-observeroptions) | No | None | **Named parameter.** Subscription options; None observes slot 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Subscribes to signal information change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<Array\<SignalInformation>> | Yes | - | Receives an array of signal information; the array may be empty. |
| options | ?[ObserverOptions](#class-observeroptions) | No | None | **Named parameter.** Subscription options; None observes slot 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Subscribes to SIM card state change events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | Callback1Argument\<Array\<[SimStateData](#class-simstatedata)>> | Yes | - | Receives an array of SIM state information. Each notification currently contains one item; iterate over the array. |
| options | ?[ObserverOptions](#class-observeroptions) | No | None | **Named parameter.** Subscription options; None observes slot 0. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

Instances are supplied by state callbacks; this class has no public constructor.

**Description:** Call state information.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop number

```cangjie
public mut prop number: String
```

**Description:** Phone number supplied by the system according to authorization and underlying data. It may be empty. Examples do not log the phone number.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop state

```cangjie
public mut prop state: CallState
```

**Description:** Call state.

**Type:** CallState

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

## class ObserverOptions

```cangjie
public class ObserverOptions {
    public init(slotId!: ?Int32 = None)
}
```

**Description:** Optional parameters for subscribing to telephony-related events.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop slotId

```cangjie
public mut prop slotId: Int32
```

**Description:** Slot ID. 0 indicates slot 1 and 1 indicates slot 2. Available slots depend on the device. The default is 0.

**Type:** Int32

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### init(?Int32)

```cangjie
public init(slotId!: ?Int32 = None)
```

**Description:** Constructor of ObserverOptions.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| slotId | ?Int32 | No | None | **Named parameter.** Slot ID. None is converted to 0 by the constructor. |

## class SimStateData

```cangjie
public class SimStateData {}
```

Instances are supplied by state callbacks; this class has no public constructor.

**Description:** SIM card type and state.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop cardType

```cangjie
public mut prop cardType: CardType
```

**Description:** SIM card type. See [CardType](cj-apis-telephony-sim.md#enum-cardtype).

**Type:** CardType

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop reason

```cangjie
public mut prop reason: LockReason
```

**Description:** SIM card lock type. Use this property with SimStateLocked to determine the lock reason; do not initiate unlocking based only on reason in other states.

**Type:** [LockReason](#enum-lockreason)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### prop state

```cangjie
public mut prop state: SimState
```

**Description:** SIM card state.

**Type:** SimState

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

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

**Description:** SIM card lock type. Use this property with SimStateLocked to determine the lock reason; do not initiate unlocking based only on reason in other states.

**Extended Types:**

- [extend LockReason <: ToString](#extend-lockreason--tostring)
- [extend LockReason <: Equatable\<LockReason>](#extend-lockreason--equatablelockreason)

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimNone

```cangjie
SimNone
```

**Description:** No lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPcPin

```cangjie
SimPcPin
```

**Description:** Organization PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPcPuk

```cangjie
SimPcPuk
```

**Description:** Organization PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPin

```cangjie
SimPin
```

**Description:** PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPnPin

```cangjie
SimPnPin
```

**Description:** Network PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPnPuk

```cangjie
SimPnPuk
```

**Description:** Network PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPpPin

```cangjie
SimPpPin
```

**Description:** Service provider PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPpPuk

```cangjie
SimPpPuk
```

**Description:** Service provider PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPuPin

```cangjie
SimPuPin
```

**Description:** Subnetwork PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPuPuk

```cangjie
SimPuPuk
```

**Description:** Subnetwork PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimPuk

```cangjie
SimPuk
```

**Description:** PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimSimPin

```cangjie
SimSimPin
```

**Description:** SIM PIN lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

### SimSimPuk

```cangjie
SimSimPuk
```

**Description:** SIM PUK lock.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

## extend LockReason <: Equatable\<LockReason>

```cangjie
extend LockReason <: Equatable<LockReason>
```

**Description:** Extends the LockReason type with the Equatable\<LockReason> interface to support equality comparison.

**Extended Type:**

- [LockReason](#enum-lockreason)

**Extended Interfaces:**

- Equatable\<[LockReason](#enum-lockreason)>

### func ==(LockReason)

```cangjie
public operator func ==(other: LockReason): Bool
```

**Description:** Checks whether two LockReason values are equal.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [LockReason](#enum-lockreason) | Yes | - | The LockReason object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two LockReason values are equal; otherwise, returns false. |

### func !=(LockReason)

```cangjie
public operator func !=(other: LockReason): Bool
```

**Description:** Checks whether two LockReason values are not equal.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [LockReason](#enum-lockreason) | Yes | - | The LockReason object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two LockReason values are not equal; otherwise, returns false. |

## extend LockReason <: ToString

```cangjie
extend LockReason <: ToString
```

**Description:** Extends the LockReason type with the ToString interface to support string conversion.

**Extended Type:**

- [LockReason](#enum-lockreason)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.StateRegistry

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |
