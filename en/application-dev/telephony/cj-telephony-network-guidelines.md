# Obtaining Cellular Network Information

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Overview

Applications can query the registered network country code, network registration state, automatic or manual network selection mode, primary slot ID, radio access technology, and device NR support. These are one-time queries; the returned objects do not update automatically when device state changes.

## Basic Concepts

| Name | Description |
| :--- | :--- |
| Slot ID | A zero-based slot index. For example, 0 is slot 1 and 1 is slot 2. Available slots depend on the device configuration; do not assume every device has two slots. |
| Primary slot | The slot configured as primary by the system, queried with getPrimarySlotId. The getNetworkState overload without a slot parameter always queries slot 0. |
| NetworkState | Network information such as operator names, registration state, access technology, and roaming status. |
| NetworkSelectionMode | Unknown, automatic, or manual network selection. The query API does not change this mode. |
| NetworkRadioTech | Radio access technologies for the CS (circuit switched) and PS (packet switched) domains. |
| NR | New Radio, a 5G radio access technology. Device NR support and a current 5G connection are different facts. |

## Constraints

- These APIs are available since 26.1.0 and require SystemCapability.Telephony.CoreService.
- getNetworkState and getRadioTechSync require ohos.permission.GET_NETWORK_INFO.
- The country code can be empty when no network is registered, and is also empty for an invalid slot. getRadioTechSync returns RadioTechnologyUnknown for both domains when the slot is invalid or a query fails. Unknown does not identify a specific error.
- The current getNetworkState implementation returns NsaStateNotSupport for nsaState and false for isCaActive. These properties cannot be used to determine the actual NSA or carrier aggregation state.
- Updating returned object properties only changes the local object, not the device network configuration. Results depend on the SIM card, network coverage, and device capability.

## APIs

For complete signatures, parameters, and error codes, see [ohos.telephony.radio](../reference/TelephonyKit/cj-apis-telephony-radio.md).

| API | Description |
| :--- | :--- |
| getISOCountryCodeForNetworkSync(Int32) | Synchronously obtains the ISO country code of the network registered by the specified slot. |
| getNetworkSelectionMode(Int32, AsyncCallback\<NetworkSelectionMode>) | Asynchronously obtains the selection mode of the specified slot. |
| getNetworkState(Int32, AsyncCallback\<NetworkState>) | Asynchronously obtains the network state of the specified slot. |
| getNetworkState(AsyncCallback\<NetworkState>) | Asynchronously obtains the network state of slot 0. |
| getPrimarySlotId(AsyncCallback\<Int32>) | Asynchronously obtains the primary slot ID. |
| getRadioTechSync(Int32) | Synchronously obtains the CS and PS radio access technologies of the specified slot. |
| isNRSupported() | Checks whether the device supports NR. |

## Development Steps

1. Declare GET_NETWORK_INFO in the module.json5 file. This permission is granted by the system. See [Declaring Permissions](../security/AccessToken/cj-declare-permissions.md). Add the following property to the module node, or merge the permission into its existing requestPermissions array.

   ```json
   "requestPermissions": [
     {
       "name": "ohos.permission.GET_NETWORK_INFO"
     }
   ]
   ```

2. Import TelephonyKit and the callback, exception, and logging types. Select a slot available on the device; the examples use slot 0.
3. Read synchronous return values directly. For asynchronous queries, handle error when it is Some, or read data when error is None and data is Some. Do not read an asynchronous result immediately after submitting the query.
4. Add the following functions to a Cangjie project and call the ones needed by your application. queryNetworkState queries a specified slot, while queryDefaultNetworkState queries slot 0. To query the primary card, call getNetworkState(value, callback) inside the successful getPrimarySlotId callback.

## Sample Code

```cangjie
import kit.TelephonyKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

func queryCountryCode(): Unit {
    let code = getISOCountryCodeForNetworkSync(0)
    if (code.isEmpty()) {
        Hilog.info(0, "TelephonyExample", "No network country code is available", [])
    } else {
        Hilog.info(0, "TelephonyExample", "ISO country code: ${code}", [])
    }
}

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

func queryNrCapability(): Unit {
    let supported = isNRSupported()
    Hilog.info(0, "TelephonyExample", "NR supported: ${supported}", [])
}
```

The example logs results with Hilog. Asynchronous query errors are delivered to the callback; the outer try/catch does not replace callback error handling. Queries run independently and can complete in any order.
