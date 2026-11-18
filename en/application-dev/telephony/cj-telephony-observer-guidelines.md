# Observing Telephony State Changes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

Applications can use ohos.telephony.observer to subscribe to changes in call state, network state, signal information, SIM card state, and SIM account information, and unsubscribe when notifications are no longer needed. Changes are delivered through callbacks.

For one-time network queries, see [Obtaining Cellular Network Information](cj-telephony-network-guidelines.md). For SIM card type and state enums, see [Using SIM Card Type and State Enums](cj-telephony-sim-guidelines.md).

## Constraints

- The observation APIs are available since 26.1.0 and require `SystemCapability.Telephony.StateRegistry`.
- Network state subscriptions require `ohos.permission.GET_NETWORK_INFO`, and call state subscriptions require `ohos.permission.MANAGE_CALL_FOR_DEVICES`. Signal, SIM state, and SIM account change subscriptions do not require these two permissions. The call permission is system-controlled and requires an authorized signing configuration.
- If options is omitted or None, the call API observes the overall call state, while the other four event APIs default to slot 0. ObserverOptions() explicitly defaults slotId to 0; for call observation, this differs from omitting options. Available slots depend on the device.
- A successful subscription return does not mean that a callback has arrived. The first underlying call or SIM state subscription requests the cached state; delivery depends on system data. Adding a callback to an existing subscription for the same event and slot does not request another initial state.
- Retain the callback object used for subscription and pass the same object to the off API when notifications are no longer needed. Omitting callback or passing None removes all listeners for that event in the current process. A callback already in progress is not guaranteed to stop immediately.
- Changing ObserverOptions.slotId does not move an existing subscription; it affects subsequent subscriptions. Updating a callback result object does not change the device state.

## APIs

For complete signatures, parameters, and error codes, see [ohos.telephony.observer](../reference/TelephonyKit/cj-apis-telephony-observer.md).

| Subscribe / Unsubscribe | Notification | Permission for subscription |
| :--- | :--- | :--- |
| [onNetworkStateChange / offNetworkStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onnetworkstatechangecallback1argumentnetworkstate-observeroptions) | NetworkState fields such as registration state, operator names, and radio technology. | ohos.permission.GET_NETWORK_INFO |
| [onSignalInfoChange / offSignalInfoChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsignalinfochangecallback1argumentarraysignalinformation-observeroptions) | An array of SignalInformation, possibly empty. Items contain signalType, signalLevel, and dBm. | None |
| [onCallStateChange / offCallStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-oncallstatechangecallback1argumentcallstateinfo-observeroptions) | Call state and the number supplied by the system; the number may be empty. | ohos.permission.MANAGE_CALL_FOR_DEVICES |
| [onIccAccountInfoChange / offIccAccountInfoChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-oniccaccountinfochangecallback0argument-observeroptions) | A notification that SIM account information changed, without account details. | None |
| [onSimStateChange / offSimStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsimstatechangecallback1argumentarraysimstatedata-observeroptions) | An array of SimStateData containing the card type, SIM state, and lock reason. | None |

## Development Steps

1. The network state example requires GET_NETWORK_INFO to be declared in module.json5. Add the following property to the module node, or merge the permission into its existing requestPermissions array. For details, see [Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

   ```json
   {
     "requestPermissions": [
       { "name": "ohos.permission.GET_NETWORK_INFO" }
     ]
   }
   ```

2. Choose an available slot; the examples use slot 0. Implement Callback1Argument for notifications carrying data and Callback0Argument for SIM account changes, and retain the callback object. Observer data callbacks receive an actual data object, whereas radio AsyncCallback receives an optional result. Their parameter types differ.
3. Call the corresponding on API to subscribe. When the page is destroyed or notifications are no longer needed, call the matching off API with the original callback object. Do not immediately unsubscribe after subscribing.
4. Network, signal, and account notifications can occur during normal device operation without manual actions. Fields available in query and observation results may differ; placeholder-value limitations of a query API do not automatically apply to observer callbacks.

## Sample Code

### Network State and Signal Changes

Call startNetworkStateChangeObserver and startSignalInfoChangeObserver separately to begin, and inspect the callback results with Hilog. Call the matching stop functions when notifications are no longer needed. For complete call and SIM account change examples, follow the API reference links in the table above.

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

### SIM State Changes

To receive the SIM state of a real device, use [onSimStateChange](../reference/TelephonyKit/cj-apis-telephony-observer.md#func-onsimstatechangecallback1argumentarraysimstatedata-observeroptions) from the observer module. It is available since 26.1.0, requires `SystemCapability.Telephony.StateRegistry`, and requires no additional permission.

The callback receives `Array<SimStateData>`. Each notification currently contains one item, but applications should iterate over the array. cardType indicates the card type, state the SIM state, and reason the [LockReason](../reference/TelephonyKit/cj-apis-telephony-observer.md#enum-lockreason). For SimStateLocked, use reason to identify PIN, PUK, or another lock. Do not initiate unlocking based only on reason when the SIM is not locked. SIM state and SIM account changes are different events.

Call startSimStateChangeObserver to begin; the example explicitly uses slot 0. The first underlying subscription requests the cached state, but the on function returning does not mean the state has arrived. Display a pending state using SimStateUnknown until the first notification. Call stopSimStateChangeObserver when no longer needed, using the same retained callback object. Omitting callback from offSimStateChange removes all listeners for this event in the current process.

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
