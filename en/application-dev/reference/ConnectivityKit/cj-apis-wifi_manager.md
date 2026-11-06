# ohos.wifi_manager (WLAN)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module primarily provides WLAN basic functions, P2P (peer-to-peer) capabilities, and WLAN notification services, enabling applications to interconnect with other devices via WLAN.

## Import Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.GET_WIFI_INFO

ohos.permission.SET_WIFI_INFO

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration is needed in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md).

## func getScanInfoList()

```cangjie
public func getScanInfoList(): Array<WifiScanInfo>
```

**Description:** Obtains scan results.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[WifiScanInfo](#class-wifiscaninfo)> | Returns the list of scanned hotspots. If the application has requested the ohos.permission.GET_WIFI_PEERS_MAC permission (only system applications can request this), the bssid in the returned results will be the actual device address; otherwise, it will be a randomized device address. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let scanInfoList = getScanInfoList()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func isWifiActive()

```cangjie
public func isWifiActive(): Bool
```

**Description:** Checks whether WLAN is enabled.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: enabled, false: disabled. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let isWifiActive = isWifiActive()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func off(WifiCallbackType, ?CallbackObject)

```cangjie
public func off(eventType: WifiCallbackType, callback!: ?CallbackObject = None): Unit
```

**Description:** Unregisters WLAN state change events.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [WifiCallbackType](#enum-wificallbacktype) | Yes | - | Callback event. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** State change callback function. If no callback parameter is provided, all callback functions associated with the event will be unregistered. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    class WifiCallback <: Callback1Argument<Int32> {
        public func invoke(err: ?BusinessException, arg: Int32) {
            Hilog.info(0, "test", "invoke success", "")
        }
    }

    let callback = WifiCallback()
    // Register event
    on(WifiScanStateChange, callback)
    // Unregister event
    off(WifiScanStateChange, callback: callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func on(WifiCallbackType, Callback1Argument\<Int32>)

```cangjie
public func on(eventType: WifiCallbackType, callback: Callback1Argument<Int32>): Unit
```

**Description:** Registers WLAN state change events.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [WifiCallbackType](#enum-wificallbacktype) | Yes | - | Callback event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Int32> | Yes | - | State change callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    class WifiCallback <: Callback1Argument<Int32> {
        public func invoke(err: ?BusinessException, arg: Int32) {
            Hilog.info(0, "test", "invoke success", "")
        }
    }

    let callback = WifiCallback()
    // Register event
    on(WifiScanStateChange, callback)
    // Unregister event
    off(WifiScanStateChange, callback: callback)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func p2pCancelConnect()

```cangjie
public func p2pCancelConnect(): Unit
```

**Description:** Cancels a P2P connection during the connection process.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    p2pCancelConnect()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func p2pConnect(WifiP2PConfig)

```cangjie
public func p2pConnect(config: WifiP2PConfig): Unit
```

**Description:** Initiates a P2P connection.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| config | [WifiP2PConfig](#class-wifip2pconfig) | Yes | - | Connection configuration information. If DeviceAddressType is not specified, it defaults to the randomized device address type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let config = WifiP2PConfig("xx:xx:xx:xx", -2, "", "", GroupOwnerBand.GoBandAuto)
    p2pConnect(config)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func startDiscoverDevices()

```cangjie
public func startDiscoverDevices(): Unit
```

**Description:** Starts device discovery.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    startDiscoverDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func stopDiscoverDevices()

```cangjie
public func stopDiscoverDevices(): Unit
```

**Description:** Stops device discovery.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    stopDiscoverDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class WifiInfoElem

```cangjie
public class WifiInfoElem {
    public var eid: UInt32
    public var content: Array<UInt8>
}
```

**Functionality:** WLAN hotspot information.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var content

```cangjie
public var content: Array<UInt8>
```

**Functionality:** Element content.

**Type:** Array\<UInt8>

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var eid

```cangjie
public var eid: UInt32
```

**Functionality:** Element ID.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

## class WifiP2PConfig

```cangjie
public class WifiP2PConfig {
    public var deviceAddress: String
    public var netId: Int32
    public var passphrase: String
    public var groupName: String
    public var goBand: GroupOwnerBand
    public var deviceAddressType: DeviceAddressType
    public init(
        deviceAddress: String,
        netId: Int32,
        passphrase: String,
        groupName: String,
        goBand: GroupOwnerBand,
        deviceAddressType!: DeviceAddressType = RandomDeviceAddress
    )
}
```

**Functionality:** Represents P2P configuration information.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var deviceAddress

```cangjie
public var deviceAddress: String
```

**Functionality:** Device address.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var deviceAddressType

```cangjie
public var deviceAddressType: DeviceAddressType
```

**Functionality:** Device address type.

**Type:** [DeviceAddressType](#enum-deviceaddresstype)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var goBand

```cangjie
public var goBand: GroupOwnerBand
```

**Functionality:** Group bandwidth.

**Type:** [GroupOwnerBand](#enum-groupownerband)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var groupName

```cangjie
public var groupName: String
```

**Functionality:** Group name.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var netId

```cangjie
public var netId: Int32
```

**Functionality:** Network ID. When creating a group, -1 indicates creating a temporary group, and -2 indicates creating a permanent group.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### var passphrase

```cangjie
public var passphrase: String
```

**Functionality:** Group passphrase.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

### init(String, Int32, String, String, GroupOwnerBand, DeviceAddressType)

```cangjie
public init(
    deviceAddress: String,
    netId: Int32,
    passphrase: String,
    groupName: String,
    goBand: GroupOwnerBand,
    deviceAddressType!: DeviceAddressType = RandomDeviceAddress
)
```

**Functionality:** Constructs a WifiP2PConfig instance.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceAddress | String | Yes | - | Device address. |
| netId | Int32 | Yes | - | Network ID. When creating a group, -1 indicates creating a temporary group, and -2 indicates creating a permanent group. |
| passphrase | String | Yes | - | Group passphrase. |
| groupName | String | Yes | - | Group name. |
| goBand | [GroupOwnerBand](#enum-groupownerband) | Yes | - | Group bandwidth. |
| deviceAddressType | [DeviceAddressType](#enum-deviceaddresstype) | No | RandomDeviceAddress | **Named parameter.** Device address type. > |

## class WifiScanInfo

```cangjie
public class WifiScanInfo {
    public var ssid: String
    public var bssid: String
    public var bssidType: DeviceAddressType
    public var capabilities: String
    public var securityType: WifiSecurityType
    public var rssi: Int32
    public var band: Int32
    public var frequency: Int32
    public var channelWidth: Int32
    public var centerFrequency0: Int32
    public var centerFrequency1: Int32
    public var infoElems: Array<WifiInfoElem>
    public var timestamp: Int64
    public var supportedWifiCategory: WifiCategory
    public var isHiLinkNetwork: Bool
}
```

**Functionality:** WLAN hotspot information.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var band

```cangjie
public var band: Int32
```

**Functionality:** The frequency band of the WLAN access point, where 1: 2.4GHz; 2: 5GHz.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var bssid

```cangjie
public var bssid: String
```

**Functionality:** The BSSID of the hotspot, e.g., 00:11:22:33:44:55.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var bssidType

```cangjie
public var bssidType: DeviceAddressType
```

**Functionality:** The BSSID type of the hotspot.

**Type:** [DeviceAddressType](#enum-deviceaddresstype)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var capabilities

```cangjie
public var capabilities: String
```

**Functionality:** Hotspot capabilities.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var centerFrequency0

```cangjie
public var centerFrequency0: Int32
```

**Functionality:** The center frequency of the hotspot.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var centerFrequency1

```cangjie
public var centerFrequency1: Int32
```

**Functionality:** The center frequency of the hotspot. If the hotspot uses two non-overlapping WLAN channels, two center frequencies are returned, represented by centerFrequency0 and centerFrequency1 respectively.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var channelWidth

```cangjie
public var channelWidth: Int32
```

**Functionality:** The bandwidth of the WLAN access point.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var frequency

```cangjie
public var frequency: Int32
```

**Functionality:** The frequency of the WLAN access point.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var infoElems

```cangjie
public var infoElems: Array<WifiInfoElem>
```

**Functionality:** Information elements.

**Type:** Array\<[WifiInfoElem](#class-wifiinfoelem)>

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var isHiLinkNetwork

```cangjie
public var isHiLinkNetwork: Bool
```

**Functionality:** Whether the hotspot supports HiLink, true: supported, &nbsp;false: not supported.

**Type:** Bool

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var rssi

```cangjie
public var rssi: Int32
```

**Functionality:** The signal strength (dBm) of the hotspot.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var securityType

```cangjie
public var securityType: WifiSecurityType
```

**Functionality:** WLAN encryption type.

**Type:** [WifiSecurityType](#enum-wifisecuritytype)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var ssid

```cangjie
public var ssid: String
```

**Functionality:** The SSID of the hotspot, with a maximum length of 32 bytes, encoded in UTF-8.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var supportedWifiCategory

```cangjie
public var supportedWifiCategory: WifiCategory
```

**Functionality:** The highest WiFi category supported by the hotspot.

**Type:** [WifiCategory](#enum-wificategory)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**Functionality:** Timestamp.

**Type:** Int64

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 22## enum DeviceAddressType

```cangjie
public enum DeviceAddressType <: Equatable<DeviceAddressType> & ToString {
    | RandomDeviceAddress
    | RealDeviceAddress
    | ...
}
```

**Description:** WiFi device address (MAC/BSSID) type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parent Types:**

- Equatable\<DeviceAddressType>
- ToString

### RandomDeviceAddress

```cangjie
RandomDeviceAddress
```

**Description:** Random device address.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### RealDeviceAddress

```cangjie
RealDeviceAddress
```

**Description:** Real device address.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### func !=(DeviceAddressType)

```cangjie
public operator func !=(other: DeviceAddressType): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DeviceAddressType](#enum-deviceaddresstype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(DeviceAddressType)

```cangjie
public operator func ==(other: DeviceAddressType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DeviceAddressType](#enum-deviceaddresstype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum GroupOwnerBand

```cangjie
public enum GroupOwnerBand <: Equatable<GroupOwnerBand> & ToString {
    | GoBandAuto
    | GoBand2GHz
    | GoBand5GHz
    | ...
}
```

**Description:** Represents group bandwidth.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Parent Types:**

- Equatable\<GroupOwnerBand>
- ToString

### GoBand2GHz

```cangjie
GoBand2GHz
```

**Description:** 2.4GHz.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

### GoBand5GHz

```cangjie
GoBand5GHz
```

**Description:** 5GHz.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

### GoBandAuto

```cangjie
GoBandAuto
```

**Description:** Auto mode.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

### func !=(GroupOwnerBand)

```cangjie
public operator func !=(other: GroupOwnerBand): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GroupOwnerBand](#enum-groupownerband) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(GroupOwnerBand)

```cangjie
public operator func ==(other: GroupOwnerBand): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [GroupOwnerBand](#enum-groupownerband) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum WifiCallbackType

```cangjie
public enum WifiCallbackType <: Equatable<WifiCallbackType> & Hashable & ToString {
    | WifiScanStateChange
    | ...
}
```

**Description:** WLAN callback trigger event type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Parent Types:**

- Equatable\<WifiCallbackType>
- Hashable
- ToString

### WifiScanStateChange

```cangjie
WifiScanStateChange
```

**Description:** Registers the WLAN state change event type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

### func !=(WifiCallbackType)

```cangjie
public operator func !=(other: WifiCallbackType): Bool
```

**Description:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WifiCallbackType](#enum-wificallbacktype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(WifiCallbackType)

```cangjie
public operator func ==(other: WifiCallbackType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WifiCallbackType](#enum-wificallbacktype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Description:** Gets the hash value of the input data.

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The hash value of the data. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum WifiCategory

```cangjie
public enum WifiCategory <: Equatable<WifiCategory> & ToString {
    | Default
    | Wifi6
    | Wifi6Plus
    | ...
}
```

**Description:** Represents the highest WiFi category supported by the hotspot.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Parent Types:**

- Equatable\<WifiCategory>
- ToString

### Default

```cangjie
Default
```

**Description:** Default. WiFi categories below WiFi 6.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

### Wifi6

```cangjie
Wifi6
```

**Description:** WiFi 6.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

### Wifi6Plus

```cangjie
Wifi6Plus
```

**Description:** WiFi 6+.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

### func !=(WifiCategory)

```cangjie
public operator func !=(other: WifiCategory): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WifiCategory](#enum-wificategory) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(WifiCategory)

```cangjie
public operator func ==(other: WifiCategory): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WifiCategory](#enum-wificategory) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |## enum WifiSecurityType

```cangjie
public enum WifiSecurityType <: Equatable<WifiSecurityType> & ToString {
    | WifiSecTypeInvalid
    | WifiSecTypeOpen
    | WifiSecTypeWep
    | WifiSecTypePsk
    | WifiSecTypeSae
    | WifiSecTypeEap
    | WifiSecTypeEapSuiteB
    | WifiSecTypeOwe
    | WifiSecTypeWapiCert
    | WifiSecTypeWapiPsk
    | ...
}
```

**Function:** Represents encryption types.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parent Types:**

- Equatable\<WifiSecurityType>
- ToString

### WifiSecTypeEap

```cangjie
WifiSecTypeEap
```

**Function:** EAP encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeEapSuiteB

```cangjie
WifiSecTypeEapSuiteB
```

**Function:** Suite-B 192-bit encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeInvalid

```cangjie
WifiSecTypeInvalid
```

**Function:** Invalid encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeOpen

```cangjie
WifiSecTypeOpen
```

**Function:** Open encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeOwe

```cangjie
WifiSecTypeOwe
```

**Function:** Opportunistic Wireless Encryption (OWE) type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypePsk

```cangjie
WifiSecTypePsk
```

**Function:** Pre-shared key (PSK) encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeSae

```cangjie
WifiSecTypeSae
```

**Function:** Simultaneous Authentication of Equals (SAE) encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWapiCert

```cangjie
WifiSecTypeWapiCert
```

**Function:** WAPI-Cert encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWapiPsk

```cangjie
WifiSecTypeWapiPsk
```

**Function:** WAPI-PSK encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWep

```cangjie
WifiSecTypeWep
```

**Function:** Wired Equivalent Privacy (WEP) encryption type. This encryption type is not supported by candidate network configurations.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### func !=(WifiSecurityType)

```cangjie
public operator func !=(other: WifiSecurityType): Bool
```

**Function:** Determines whether two enumeration values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[WifiSecurityType](#enum-wifisecuritytype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are unequal, otherwise returns false.|

### func ==(WifiSecurityType)

```cangjie
public operator func ==(other: WifiSecurityType): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[WifiSecurityType](#enum-wifisecuritytype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|Description of the enumeration.|