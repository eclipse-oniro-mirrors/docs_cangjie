# ohos.telephony.radio (Network Search)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The radio module provides the capability to query network state, network selection mode, radio access technology, and other information.

## Import Module

```cangjie
import kit.TelephonyKit.*
```

## Usage Instructions

The APIs in these examples are available since 26.1.0. Add the imports and function definitions to a Cangjie project, and call the corresponding example function from your application code.

The asynchronous APIs use `AsyncCallback<T>` with two parameters: an error of type `Option<BusinessException>` and a result of type `Option<T>`. On success, the error is `None` and the result is `Some(value)`. On failure, the error is `Some(error)` and the result is `None`. Handle query errors inside the callback; a `try/catch` around the call does not replace callback error handling.

For the project and configuration template, see [Cangjie Sample Code Notes](../cj-development-intro.md#cangjie-sample-code-notes).

## func getISOCountryCodeForNetworkSync(Int32)

```cangjie
public func getISOCountryCodeForNetworkSync(slotId: Int32): String
```

**Description:** Obtains the ISO country code of the country where the registered network is located.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| slotId | Int32 | Yes | - | Slot ID. - 0: Slot 1. - 1: Slot 2. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| String | Returns the ISO country code of the country where the registered network is located, for example, CN (China). If the device is not registered with any network, an empty string is returned. |

An invalid slot ID returns an empty string. An empty string means that no network country code is available; it does not distinguish between an unregistered network, an invalid slot, and other causes.

**Example:**

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

**Description:** Obtains the current network selection mode.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| slotId | Int32 | Yes | - | Slot ID. - 0: Slot 1. - 1: Slot 2. |
| callback | AsyncCallback\<[NetworkSelectionMode](#enum-networkselectionmode)> | Yes | - | Callback function. Returns the current network selection mode. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Obtains the network state of the specified slot.

**Permission Required:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| slotId | Int32 | Yes | - | Slot ID. - 0: Slot 1. - 1: Slot 2. |
| callback | AsyncCallback\<[NetworkState](#class-networkstate)> | Yes | - | Callback function. Returns the current network state. |

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

**Description:** Obtains the network state of slot 0. This overload does not select the primary slot. To query the primary card, obtain its slot ID with getPrimarySlotId and pass it to the overload that accepts slotId.

**Permission Required:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | AsyncCallback\<[NetworkState](#class-networkstate)> | Yes | - | Callback function. Returns the current network state. |

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

**Description:** Obtains the index of the slot where the primary card is located.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| callback | AsyncCallback\<Int32> | Yes | - | Callback function. Returns the index of the slot where the primary card is located. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Service connection failed. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error. |

**Example:**

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

**Description:** Obtains the CS domain and PS domain radio access technologies of the SIM card in the specified slot. The CS domain is the circuit switched domain, and the PS domain is the packet switched domain.

**Permission Required:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| slotId | Int32 | Yes | - | Slot ID. - 0: Slot 1. - 1: Slot 2. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| [NetworkRadioTech](#class-networkradiotech) | Returns the currently connected CS domain and PS domain technologies. The CS domain is the circuit switched domain, and the PS domain is the packet switched domain. |

In the current version, an invalid slot ID or a failed radio technology query returns an object with both csRadioTech and psRadioTech set to RadioTechnologyUnknown, rather than reporting these query failures through a business exception. This value can also indicate an unknown technology and does not identify a specific error. The exception table below retains the error codes specified by the API declaration.

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Telephony Subsystem Error Codes](./cj-errorcode-telephony.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

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

**Description:** Checks whether the current device supports NR (New Radio, a 5G radio access technology). The result describes device capability, not whether the device is currently connected to a 5G network.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
| :--- | :--- |
| Bool | Whether the current device supports NR. - true: Supported. - false: Not supported. |

**Example:**

```cangjie
import kit.TelephonyKit.isNRSupported
import kit.PerformanceAnalysisKit.Hilog

func queryNrCapability(): Unit {
    let supported = isNRSupported()
    Hilog.info(0, "TelephonyExample", "NR supported: ${supported}", [])
}
```

## class NetworkRadioTech

This object is returned by getRadioTechSync. Changing its properties only updates the local object; it does not change the device radio access technology.

```cangjie
public class NetworkRadioTech {}
```

**Description:** Radio access technologies of the PS (packet switched) and CS (circuit switched) domains in the network.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop csRadioTech

```cangjie
public mut prop csRadioTech: RadioTechnology
```

**Description:** CS radio access technology.

**Type:** [RadioTechnology](#enum-radiotechnology)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop psRadioTech

```cangjie
public mut prop psRadioTech: RadioTechnology
```

**Description:** PS radio access technology.

**Type:** [RadioTechnology](#enum-radiotechnology)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## class NetworkState

This object is returned by getNetworkState. Changing its properties only updates the local object; it does not change the device network configuration or registration state.

```cangjie
public class NetworkState {}
```

**Description:** Network registration status.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop cfgTech

```cangjie
public mut prop cfgTech: RadioTechnology
```

**Description:** Radio access technology of the device.

**Type:** [RadioTechnology](#enum-radiotechnology)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop isCaActive

```cangjie
public mut prop isCaActive: Bool
```

**Description:** CA (carrier aggregation) status. - true: CA is activated. - false: CA is not activated. The current getNetworkState implementation returns false for this property, so it cannot be used to determine the actual CA state.

**Type:** Bool

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop isEmergency

```cangjie
public mut prop isEmergency: Bool
```

**Description:** Whether the device can only make emergency calls.

**Type:** Bool

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop isRoaming

```cangjie
public mut prop isRoaming: Bool
```

**Description:** Whether the device is roaming. - true: The device is roaming. - false: The device is not roaming.

**Type:** Bool

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop longOperatorName

```cangjie
public mut prop longOperatorName: String
```

**Description:** Long operator name of the registered network.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop nsaState

```cangjie
public mut prop nsaState: NsaState
```

**Description:** NSA (non-standalone) network registration status of the device. The current getNetworkState implementation returns NsaStateNotSupport for this property, so it cannot be used to determine the actual NSA registration state.

**Type:** [NsaState](#enum-nsastate)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop plmnNumeric

```cangjie
public mut prop plmnNumeric: String
```

**Description:** PLMN (Public Land Mobile Network) code of the registered network.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop regState

```cangjie
public mut prop regState: RegState
```

**Description:** Network registration status of the device.

**Type:** [RegState](#enum-regstate)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop shortOperatorName

```cangjie
public mut prop shortOperatorName: String
```

**Description:** Short operator name of the registered network.

**Type:** String

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## class SignalInformation

This type describes signal strength information. The current module provides neither a public constructor nor a signal strength query function. Changing its properties only updates the local object; it does not change the device signal strength.

```cangjie
public class SignalInformation {}
```

**Description:** Network signal strength information object.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop dBm

```cangjie
public mut prop dBm: Int32
```

**Description:** Network signal strength. The value range is [-140, 140].

**Type:** Int32

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop signalLevel

```cangjie
public mut prop signalLevel: Int32
```

**Description:** Network signal strength level. The value range is [0, 5].

**Type:** Int32

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### prop signalType

```cangjie
public mut prop signalType: NetworkType
```

**Description:** Network signal strength type.

**Type:** [NetworkType](#enum-networktype)

**Read/Write Capability:** Read/Write

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## enum NetworkSelectionMode

```cangjie
public enum NetworkSelectionMode {
    | NetworkSelectionAutomatic
    | NetworkSelectionManual
    | NetworkSelectionUnknown
    | ...
}
```

**Description:** Network selection mode.

**Extended Types:**

- [extend NetworkSelectionMode <: ToString](#extend-networkselectionmode--tostring)
- [extend NetworkSelectionMode <: Equatable\<NetworkSelectionMode>](#extend-networkselectionmode--equatablenetworkselectionmode)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkSelectionAutomatic

```cangjie
NetworkSelectionAutomatic
```

**Description:** Automatic network selection mode.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkSelectionManual

```cangjie
NetworkSelectionManual
```

**Description:** Manual network selection mode.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkSelectionUnknown

```cangjie
NetworkSelectionUnknown
```

**Description:** Unknown network selection mode.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

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

**Description:** Network type.

**Extended Types:**

- [extend NetworkType <: ToString](#extend-networktype--tostring)
- [extend NetworkType <: Equatable\<NetworkType>](#extend-networktype--equatablenetworktype)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeCdma

```cangjie
NetworkTypeCdma
```

**Description:** The network type is CDMA (Code Division Multiple Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeGsm

```cangjie
NetworkTypeGsm
```

**Description:** The network type is GSM (Global System For Mobile Communication).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeLte

```cangjie
NetworkTypeLte
```

**Description:** The network type is LTE (Long Term Evolution).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeNr

```cangjie
NetworkTypeNr
```

**Description:** The network type is NR (New Radio).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeTdscdma

```cangjie
NetworkTypeTdscdma
```

**Description:** The network type is TDSCDMA (TimeDivision-Synchronous Code Division Multiple Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeUnknown

```cangjie
NetworkTypeUnknown
```

**Description:** Unknown network type.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NetworkTypeWcdma

```cangjie
NetworkTypeWcdma
```

**Description:** The network type is WCDMA (Wideband Code Division Multiple Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

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

**Description:** Non-standalone networking state.

**Extended Types:**

- [extend NsaState <: ToString](#extend-nsastate--tostring)
- [extend NsaState <: Equatable\<NsaState>](#extend-nsastate--equatablensastate)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateConnectedDetect

```cangjie
NsaStateConnectedDetect
```

**Description:** The device is connected to an LTE network in an LTE cell that supports NSA and NR coverage detection.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateDualConnected

```cangjie
NsaStateDualConnected
```

**Description:** The device is connected to the LTE + NR network in an LTE cell that supports NSA.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateIdleDetect

```cangjie
NsaStateIdleDetect
```

**Description:** The device is in idle state in an LTE cell that supports NSA and NR coverage detection.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateNoDetect

```cangjie
NsaStateNoDetect
```

**Description:** The device is in idle state in an LTE cell that supports NSA but does not support NR coverage detection.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateNotSupport

```cangjie
NsaStateNotSupport
```

**Description:** The device is in idle or connected state in an LTE cell that does not support NSA.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### NsaStateSaAttached

```cangjie
NsaStateSaAttached
```

**Description:** The device is idle or connected to an NG-RAN (Next Generation Radio Access Network) cell when attached to the 5GC (5G Core Network).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

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

**Description:** Radio access technology.

**Extended Types:**

- [extend RadioTechnology <: ToString](#extend-radiotechnology--tostring)
- [extend RadioTechnology <: Equatable\<RadioTechnology>](#extend-radiotechnology--equatableradiotechnology)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnology1xrtt

```cangjie
RadioTechnology1xrtt
```

**Description:** Radio access technology 1XRTT (Single-Carrier Radio Transmission Technology).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyEhrpd

```cangjie
RadioTechnologyEhrpd
```

**Description:** Radio access technology EHRPD (Evolved High Rate Packet Data).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyEvdo

```cangjie
RadioTechnologyEvdo
```

**Description:** Radio access technology EVDO (Evolution Data Only).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyGsm

```cangjie
RadioTechnologyGsm
```

**Description:** Radio access technology GSM (Global System For Mobile Communication).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyHspa

```cangjie
RadioTechnologyHspa
```

**Description:** Radio access technology HSPA (High Speed Packet Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyHspap

```cangjie
RadioTechnologyHspap
```

**Description:** Radio access technology HSPAP (High Speed Packet Access+).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyIwlan

```cangjie
RadioTechnologyIwlan
```

**Description:** Radio access technology IWLAN (Interworking Wireless LAN).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyLte

```cangjie
RadioTechnologyLte
```

**Description:** Radio access technology LTE (Long Term Evolution).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyLteCa

```cangjie
RadioTechnologyLteCa
```

**Description:** Radio access technology LTE_CA (Long Term Evolution_Carrier Aggregation).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyNr

```cangjie
RadioTechnologyNr
```

**Description:** Radio access technology NR (New Radio).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyTdScdma

```cangjie
RadioTechnologyTdScdma
```

**Description:** Radio access technology TD_SCDMA (TimeDivision-Synchronous Code Division Multiple Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyUnknown

```cangjie
RadioTechnologyUnknown
```

**Description:** Unknown radio access technology (RAT).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RadioTechnologyWcdma

```cangjie
RadioTechnologyWcdma
```

**Description:** Radio access technology WCDMA (Wideband Code Division Multiple Access).

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

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

**Description:** Network registration status.

**Extended Types:**

- [extend RegState <: ToString](#extend-regstate--tostring)
- [extend RegState <: Equatable\<RegState>](#extend-regstate--equatableregstate)

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RegStateEmergencyCallOnly

```cangjie
RegStateEmergencyCallOnly
```

**Description:** The device can use only emergency call services.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RegStateInService

```cangjie
RegStateInService
```

**Description:** The device can use services properly, including data services, SMS, and calls.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RegStateNoService

```cangjie
RegStateNoService
```

**Description:** The device cannot use any service, including data services, SMS, and calls.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

### RegStatePowerOff

```cangjie
RegStatePowerOff
```

**Description:** The cellular radio is disabled and the modem is powered off, so the device cannot communicate with the network.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

## extend NetworkSelectionMode <: Equatable\<NetworkSelectionMode>

```cangjie
extend NetworkSelectionMode <: Equatable<NetworkSelectionMode>
```

**Description:** Extends the NetworkSelectionMode type with the Equatable\<NetworkSelectionMode> interface to support equality comparison.

**Extended Type:**

- [NetworkSelectionMode](#enum-networkselectionmode)

**Extended Interfaces:**

- Equatable\<[NetworkSelectionMode](#enum-networkselectionmode)>

### func ==(NetworkSelectionMode)

```cangjie
public operator func ==(other: NetworkSelectionMode): Bool
```

**Description:** Checks whether two NetworkSelectionMode values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NetworkSelectionMode](#enum-networkselectionmode) | Yes | - | The NetworkSelectionMode object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NetworkSelectionMode values are equal; otherwise, returns false. |

### func !=(NetworkSelectionMode)

```cangjie
public operator func !=(other: NetworkSelectionMode): Bool
```

**Description:** Checks whether two NetworkSelectionMode values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NetworkSelectionMode](#enum-networkselectionmode) | Yes | - | The NetworkSelectionMode object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NetworkSelectionMode values are not equal; otherwise, returns false. |

## extend NetworkSelectionMode <: ToString

```cangjie
extend NetworkSelectionMode <: ToString
```

**Description:** Extends the NetworkSelectionMode type with the ToString interface to support string conversion.

**Extended Type:**

- [NetworkSelectionMode](#enum-networkselectionmode)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## extend NetworkType <: Equatable\<NetworkType>

```cangjie
extend NetworkType <: Equatable<NetworkType>
```

**Description:** Extends the NetworkType type with the Equatable\<NetworkType> interface to support equality comparison.

**Extended Type:**

- [NetworkType](#enum-networktype)

**Extended Interfaces:**

- Equatable\<[NetworkType](#enum-networktype)>

### func ==(NetworkType)

```cangjie
public operator func ==(other: NetworkType): Bool
```

**Description:** Checks whether two NetworkType values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NetworkType](#enum-networktype) | Yes | - | The NetworkType object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NetworkType values are equal; otherwise, returns false. |

### func !=(NetworkType)

```cangjie
public operator func !=(other: NetworkType): Bool
```

**Description:** Checks whether two NetworkType values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NetworkType](#enum-networktype) | Yes | - | The NetworkType object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NetworkType values are not equal; otherwise, returns false. |

## extend NetworkType <: ToString

```cangjie
extend NetworkType <: ToString
```

**Description:** Extends the NetworkType type with the ToString interface to support string conversion.

**Extended Type:**

- [NetworkType](#enum-networktype)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## extend NsaState <: Equatable\<NsaState>

```cangjie
extend NsaState <: Equatable<NsaState>
```

**Description:** Extends the NsaState type with the Equatable\<NsaState> interface to support equality comparison.

**Extended Type:**

- [NsaState](#enum-nsastate)

**Extended Interfaces:**

- Equatable\<[NsaState](#enum-nsastate)>

### func ==(NsaState)

```cangjie
public operator func ==(other: NsaState): Bool
```

**Description:** Checks whether two NsaState values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NsaState](#enum-nsastate) | Yes | - | The NsaState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NsaState values are equal; otherwise, returns false. |

### func !=(NsaState)

```cangjie
public operator func !=(other: NsaState): Bool
```

**Description:** Checks whether two NsaState values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [NsaState](#enum-nsastate) | Yes | - | The NsaState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two NsaState values are not equal; otherwise, returns false. |

## extend NsaState <: ToString

```cangjie
extend NsaState <: ToString
```

**Description:** Extends the NsaState type with the ToString interface to support string conversion.

**Extended Type:**

- [NsaState](#enum-nsastate)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## extend RadioTechnology <: Equatable\<RadioTechnology>

```cangjie
extend RadioTechnology <: Equatable<RadioTechnology>
```

**Description:** Extends the RadioTechnology type with the Equatable\<RadioTechnology> interface to support equality comparison.

**Extended Type:**

- [RadioTechnology](#enum-radiotechnology)

**Extended Interfaces:**

- Equatable\<[RadioTechnology](#enum-radiotechnology)>

### func ==(RadioTechnology)

```cangjie
public operator func ==(other: RadioTechnology): Bool
```

**Description:** Checks whether two RadioTechnology values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [RadioTechnology](#enum-radiotechnology) | Yes | - | The RadioTechnology object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two RadioTechnology values are equal; otherwise, returns false. |

### func !=(RadioTechnology)

```cangjie
public operator func !=(other: RadioTechnology): Bool
```

**Description:** Checks whether two RadioTechnology values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [RadioTechnology](#enum-radiotechnology) | Yes | - | The RadioTechnology object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two RadioTechnology values are not equal; otherwise, returns false. |

## extend RadioTechnology <: ToString

```cangjie
extend RadioTechnology <: ToString
```

**Description:** Extends the RadioTechnology type with the ToString interface to support string conversion.

**Extended Type:**

- [RadioTechnology](#enum-radiotechnology)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |

## extend RegState <: Equatable\<RegState>

```cangjie
extend RegState <: Equatable<RegState>
```

**Description:** Extends the RegState type with the Equatable\<RegState> interface to support equality comparison.

**Extended Type:**

- [RegState](#enum-regstate)

**Extended Interfaces:**

- Equatable\<[RegState](#enum-regstate)>

### func ==(RegState)

```cangjie
public operator func ==(other: RegState): Bool
```

**Description:** Checks whether two RegState values are equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [RegState](#enum-regstate) | Yes | - | The RegState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two RegState values are equal; otherwise, returns false. |

### func !=(RegState)

```cangjie
public operator func !=(other: RegState): Bool
```

**Description:** Checks whether two RegState values are not equal.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [RegState](#enum-regstate) | Yes | - | The RegState object to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two RegState values are not equal; otherwise, returns false. |

## extend RegState <: ToString

```cangjie
extend RegState <: ToString
```

**Description:** Extends the RegState type with the ToString interface to support string conversion.

**Extended Type:**

- [RegState](#enum-regstate)

**Extended Interfaces:**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Telephony.CoreService

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enumeration. |
