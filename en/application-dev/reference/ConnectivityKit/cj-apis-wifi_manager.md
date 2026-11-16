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

## func createGroup(WifiP2pConfig)

```cangjie
public func createGroup(config: WifiP2pConfig): Unit
```

**Description:** Creates a group. After the group is created, you can call removeGroup to remove the created group.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| config | [WifiP2pConfig](#class-wifip2pconfig) | Yes | - | Group configuration information. If DeviceAddressType is not specified, DeviceAddressType defaults to the random device address type. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let config = WifiP2pConfig("xx:xx:xx:xx:xx:xx", -2, "12345678", "test_group", GroupOwnerBand.GoBandAuto)
try {
    createGroup(config)
    Hilog.info(0, "test", "createGroup success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "createGroup failed, code: ${e.code}")
}
```

## func getP2pLocalDevice(AsyncCallback\<WifiP2pDevice\>)

```cangjie
public func getP2pLocalDevice(callback: AsyncCallback<WifiP2pDevice>): Unit
```

**Description:** Obtains the local P2P device information. The result is returned asynchronously through the callback function.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[WifiP2pDevice](#class-wifip2pdevice)\> | Yes | - | Callback function. When the operation is successful, err is 0 and data indicates the local device information. If err is not 0, an error occurs during processing. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<WifiP2pDevice> = {
    err: Option<BusinessException>, data: Option<WifiP2pDevice> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getP2pLocalDevice failed, code: ${e.code}")
        case None => match (data) {
            case Some(device) =>
                Hilog.info(0, "test", "deviceName: ${device.deviceName}, deviceAddress: ${device.deviceAddress}")
            case None => Hilog.error(0, "test", "local device is null")
        }
    }
}
try {
    getP2pLocalDevice(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getP2pLocalDevice failed, code: ${e.code}")
}
```

## func getP2pPeerDevices(AsyncCallback\<Array\<WifiP2pDevice\>\>)

```cangjie
public func getP2pPeerDevices(callback: AsyncCallback<Array<WifiP2pDevice>>): Unit
```

**Description:** Obtains the list of P2P peer devices. The result is returned asynchronously through the callback function.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Array\<[WifiP2pDevice](#class-wifip2pdevice)\>\> | Yes | - | Callback function. When the operation is successful, err is 0 and data indicates the peer device list information. If err is not 0, an error occurs during processing. If the application has requested the ohos.permission.GET_WIFI_PEERS_MAC permission, deviceAddress in the returned result is the actual device address; otherwise, it is a random device address. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<Array<WifiP2pDevice>> = {
    err: Option<BusinessException>, data: Option<Array<WifiP2pDevice>> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getP2pPeerDevices failed, code: ${e.code}")
        case None => match (data) {
            case Some(devices) =>
                for (device in devices) {
                    Hilog.info(0, "test", "deviceName: ${device.deviceName}, deviceAddress: ${device.deviceAddress}")
                }
            case None => Hilog.error(0, "test", "device list is null")
        }
    }
}
try {
    getP2pPeerDevices(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getP2pPeerDevices failed, code: ${e.code}")
}
```

## func getCurrentGroup(AsyncCallback\<WifiP2pGroupInfo\>)

```cangjie
public func getCurrentGroup(callback: AsyncCallback<WifiP2pGroupInfo>): Unit
```

**Description:** Obtains the information about the current P2P group. The result is returned asynchronously through the callback function.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[WifiP2pGroupInfo](#class-wifip2pgroupinfo)\> | Yes | - | Callback function. When the operation is successful, err is 0 and data indicates the current group information. If err is not 0, an error occurs during processing. If the application has requested the ohos.permission.GET_WIFI_PEERS_MAC permission, deviceAddress in the returned result is the actual device address; otherwise, it is a random device address. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<WifiP2pGroupInfo> = {
    err: Option<BusinessException>, data: Option<WifiP2pGroupInfo> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getCurrentGroup failed, code: ${e.code}")
        case None => match (data) {
            case Some(group) =>
                Hilog.info(0, "test", "groupName: ${group.groupName}, networkId: ${group.networkId}")
            case None => Hilog.error(0, "test", "group info is null")
        }
    }
}
try {
    getCurrentGroup(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getCurrentGroup failed, code: ${e.code}")
}
```

## func getP2pLinkedInfo(AsyncCallback\<WifiP2pLinkedInfo\>)

```cangjie
public func getP2pLinkedInfo(callback: AsyncCallback<WifiP2pLinkedInfo>): Unit
```

**Description:** Obtains the P2P connection information. The result is returned asynchronously through the callback function.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[WifiP2pLinkedInfo](#class-wifip2plinkedinfo)\> | Yes | - | Callback function. When the operation is successful, err is 0 and data indicates the P2P connection information. If err is not 0, an error occurs during processing. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<WifiP2pLinkedInfo> = {
    err: Option<BusinessException>, data: Option<WifiP2pLinkedInfo> => match (err) {
        case Some(e) => Hilog.error(0, "test", "getP2pLinkedInfo failed, code: ${e.code}")
        case None => match (data) {
            case Some(info) =>
                Hilog.info(0, "test", "connectState: ${info.connectState}, isGroupOwner: ${info.isGroupOwner}")
            case None => Hilog.error(0, "test", "p2p linked info is null")
        }
    }
}
try {
    getP2pLinkedInfo(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getP2pLinkedInfo failed, code: ${e.code}")
}
```

## func getCountryCode()

```cangjie
public func getCountryCode(): String
```

**Description:** Obtains the country code information.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | Country code. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2401000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let countryCode = getCountryCode()
    Hilog.info(0, "test", "countryCode: ${countryCode}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getCountryCode failed, code: ${e.code}")
}
```

## func getIpv6Info()

```cangjie
public func getIpv6Info(): Ipv6Info
```

**Description:** Obtains the IPv6 information.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| [Ipv6Info](#class-ipv6info) | IPv6 information. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let ipv6Info = getIpv6Info()
    Hilog.info(0, "test", "linkIpv6Address: ${ipv6Info.linkIpv6Address}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getIpv6Info failed, code: ${e.code}")
}
```

## func getIpInfo()

```cangjie
public func getIpInfo(): IpInfo
```

**Description:** Obtains the IPv4 information.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| [IpInfo](#class-ipinfo) | IP information. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let ipInfo = getIpInfo()
    Hilog.info(0, "test", "ipAddress: ${ipInfo.ipAddress}, gateway: ${ipInfo.gateway}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getIpInfo failed, code: ${e.code}")
}
```

## func getLinkedInfoSync()

```cangjie
public func getLinkedInfoSync(): WifiLinkedInfo
```

**Description:** Obtains Wi-Fi connection information and returns the result synchronously.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| [WifiLinkedInfo](#class-wifilinkedinfo) | Wi-Fi connection information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let linkedInfo = getLinkedInfoSync()
    Hilog.info(0, "test", "ssid: ${linkedInfo.ssid}, rssi: ${linkedInfo.rssi}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getLinkedInfoSync failed, code: ${e.code}")
}
```

## func connectToCandidateConfig(ConnectSettings, AsyncCallback\<Unit\>)

```cangjie
public func connectToCandidateConfig(settings: ConnectSettings, callback: AsyncCallback<Unit>): Unit
```

**Description:** Allows an application to connect to a candidate network added by the application itself, with support for custom parameters.

**Required Permission:** ohos.permission.SET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| settings | [ConnectSettings](#class-connectsettings) | Yes | - | Wi-Fi connection settings. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit\> | Yes | - | Callback function, used to return the result of the candidate network connection. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |
  | 2501005 | The user does not respond. |
  | 2501006 | The user refused the action. |
  | 2501007 | Parameter validation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let settings = ConnectSettings(0) // 0 is the candidate network ID
settings.withUserAction = true
settings.userActionTimeout = 10
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, _: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "connectToCandidateConfig failed, code: ${e.code}")
        case None => Hilog.info(0, "test", "connectToCandidateConfig success")
    }
}
try {
    connectToCandidateConfig(settings, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "connectToCandidateConfig failed, code: ${e.code}")
}
```

## func getCandidateConfigs()

```cangjie
public func getCandidateConfigs(): Array<WifiDeviceConfig>
```

**Description:** Obtains candidate network configurations.

- A candidate network is a network configuration that has been connected before or has been manually added.
- This API returns all saved Wi-Fi candidate network configurations that are added by the current application and are not currently connected.
- It is used to display the list of connectable networks.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[WifiDeviceConfig](#class-wifideviceconfig)\> | Array of candidate network configurations. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let configs = getCandidateConfigs()
    for (config in configs) {
        Hilog.info(0, "test", "ssid: ${config.ssid}")
    }
} catch (e: BusinessException) {
    Hilog.error(0, "test", "getCandidateConfigs failed, code: ${e.code}")
}
```

## func addCandidateConfig(WifiDeviceConfig, AsyncCallback\<Int32\>)

```cangjie
public func addCandidateConfig(config: WifiDeviceConfig, callback: AsyncCallback<Int32>): Unit
```

**Description:** Adds a candidate network configuration. The result is returned asynchronously through a callback function.

- The specified Wi-Fi device configuration is added as a candidate network. After being added, the network cannot trigger automatic reconnection if there is no connection record. You can use connectToCandidateConfig or connectToCandidateConfigWithUserAction to connect to the candidate network. Once the connection is confirmed on the page, automatic reconnection can be implemented.
- Candidate networks are network configurations added at the application level. They are isolated from system network configurations and are invisible on the system Wi-Fi page.

**Required Permission:** ohos.permission.SET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| config | [WifiDeviceConfig](#class-wifideviceconfig) | Yes | - | Wi-Fi configuration information. If bssidType is not specified, bssidType defaults to the random device address type. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32\> | Yes | - | Callback function. When error is 0, the operation is successful and data is the ID of the added network configuration; if the value of data is -1, the addition fails. When error is a non-0 value, an error occurs during the operation. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let config = WifiDeviceConfig("test_ssid", "12345678", WifiSecurityType.WifiSecTypePsk)
let callback: AsyncCallback<Int32> = {
    err: Option<BusinessException>, data: Option<Int32> => match (err) {
        case Some(e) => Hilog.error(0, "test", "addCandidateConfig failed, code: ${e.code}")
        case None => match (data) {
            case Some(networkId) => Hilog.info(0, "test", "networkId: ${networkId}")
            case None => Hilog.error(0, "test", "networkId is null")
        }
    }
}
try {
    addCandidateConfig(config, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "addCandidateConfig failed, code: ${e.code}")
}
```

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

## func isBandTypeSupported(WifiBandType)

```cangjie
public func isBandTypeSupported(bandType: WifiBandType): Bool
```

**Description:** Checks whether the current band type is supported.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| bandType | [WifiBandType](#enum-wifibandtype) | Yes | - | Wi-Fi band type. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: supported, false: not supported. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let supported = isBandTypeSupported(WifiBandType.WifiBand5g)
    Hilog.info(0, "test", "5GHz supported: ${supported}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "isBandTypeSupported failed, code: ${e.code}")
}
```

## func isFeatureSupported(Int64)

```cangjie
public func isFeatureSupported(featureId: Int64): Bool
```

**Description:** Checks whether the device supports the specified Wi-Fi feature.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| featureId | Int64 | Yes | - | Feature ID value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: supported, false: not supported. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2401000 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let featureId: Int64 = 0x0008 // 0x0008 indicates the Wifi-Direct feature
try {
    let supported = isFeatureSupported(featureId)
    Hilog.info(0, "test", "supported: ${supported}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "isFeatureSupported failed, code: ${e.code}")
}
```

## func isConnected()

```cangjie
public func isConnected(): Bool
```

**Description:** Checks whether Wi-Fi is connected.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: connected, false: not connected. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let connected = isConnected()
    Hilog.info(0, "test", "connected: ${connected}")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "isConnected failed, code: ${e.code}")
}
```

## func getSignalLevel(Int32, Int32)

```cangjie
public func getSignalLevel(rssi: Int32, band: Int32): UInt32
```

**Description:** Queries the Wi-Fi signal strength.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rssi | Int32 | Yes | - | Signal strength of the hotspot (dBm). |
| band | Int32 | Yes | - | Band of the Wi-Fi access point. 1 indicates 2.4 GHz; 2 indicates 5 GHz. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Signal strength, in the range [0, 4]. |

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let level = getSignalLevel(-60, 2) // rssi is -60 dBm and band 2 indicates 5 GHz
Hilog.info(0, "test", "signal level: ${level}")
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

## func removeGroup()

```cangjie
public func removeGroup(): Unit
```

**Description:** Removes a group.

**Required Permission:** ohos.permission.GET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    removeGroup()
    Hilog.info(0, "test", "removeGroup success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "removeGroup failed, code: ${e.code}")
}
```

## func removeCandidateConfig(Int32, AsyncCallback\<Unit\>)

```cangjie
public func removeCandidateConfig(networkId: Int32, callback: AsyncCallback<Unit>): Unit
```

**Description:** Removes the specified candidate network configuration, and the result is returned asynchronously through a callback function.

- Deletes the Wi-Fi candidate configuration with the specified network ID from the system, clears Wi-Fi candidate configurations that are no longer needed, and releases system resources.
- Only candidate configurations added by addCandidateConfig can be removed. After removal, the system will no longer automatically connect to this candidate network.

**Required Permission:** ohos.permission.SET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| networkId | Int32 | Yes | - | Network configuration ID. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit\> | Yes | - | Callback function. When the operation is successful, error is 0. If error is not 0, an error occurred during processing. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [WIFI Error Codes](./cj-errorcode-wifi-manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let networkId = 0 // Candidate network ID, which can be obtained from the callback of addCandidateConfig
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, _: Option<Unit> => match (err) {
        case Some(e) => Hilog.error(0, "test", "removeCandidateConfig failed, code: ${e.code}")
        case None => Hilog.info(0, "test", "removeCandidateConfig success")
    }
}
try {
    removeCandidateConfig(networkId, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "removeCandidateConfig failed, code: ${e.code}")
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

## func startScan()

```cangjie
public func startScan(): Unit
```

**Description:** Starts Wi-Fi scanning.

- When the application runs in the foreground, it can scan at most four times within two minutes.
- When it runs in the background, it can scan at most once within thirty minutes.
- Subscribe to scan state change events through on('wifiScanStateChange') to listen for scan completion notifications.

**Required Permission:** ohos.permission.SET_WIFI_INFO

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

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
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    startScan()
    Hilog.info(0, "test", "startScan success")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "startScan failed, code: ${e.code}")
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

## class WifiDeviceConfig

```cangjie
public class WifiDeviceConfig {
    public mut prop ssid: String
    public mut prop bssid: ?String
    public mut prop bssidType: ?DeviceAddressType
    public mut prop preSharedKey: String
    public mut prop isHiddenSsid: ?Bool
    public mut prop securityType: WifiSecurityType
    public mut prop eapConfig: ?WifiEapConfig
    public mut prop wapiConfig: ?WifiWapiConfig
    public init(
        ssid: String,
        preSharedKey: String,
        securityType: WifiSecurityType,
        bssid!: ?String = None,
        bssidType!: ?DeviceAddressType = None,
        isHiddenSsid!: ?Bool = None,
        eapConfig!: ?WifiEapConfig = None,
        wapiConfig!: ?WifiWapiConfig = None
    )
}
```

**Functionality:** Wi-Fi configuration information.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### init(String, String, WifiSecurityType, ?String, ?DeviceAddressType, ?Bool, ?WifiEapConfig, ?WifiWapiConfig)

```cangjie
public init(
    ssid: String,
    preSharedKey: String,
    securityType: WifiSecurityType,
    bssid!: ?String = None,
    bssidType!: ?DeviceAddressType = None,
    isHiddenSsid!: ?Bool = None,
    eapConfig!: ?WifiEapConfig = None,
    wapiConfig!: ?WifiWapiConfig = None
)
```

**Functionality:** Constructs a WifiDeviceConfig instance.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| ssid | String | Yes | - | SSID of the hotspot. The maximum length is 32 bytes, and the encoding format is UTF-8. |
| preSharedKey | String | Yes | - | Key of the hotspot. The maximum length is 64 bytes. When securityType is WifiSecTypeOpen, this field must be an empty string; for other encryption types, it cannot be an empty string. When securityType is WifiSecTypeWep, the length of this field can only be one of 5, 10, 13, 26, 16, and 32 bytes, and when the field length is an even number, the field must consist of pure hexadecimal digits. When securityType is WifiSecTypeSae, the minimum length of this field is 1 byte. When securityType is WifiSecTypePsk, the minimum length of this field is 8 bytes. |
| securityType | [WifiSecurityType](#enum-wifisecuritytype) | Yes | - | Encryption type. |
| bssid | ?String | No | None | **Named parameter.** BSSID of the hotspot, for example, 00:11:22:33:44:55. |
| bssidType | ?[DeviceAddressType](#enum-deviceaddresstype) | No | None | **Named parameter.** BSSID type of the hotspot. |
| isHiddenSsid | ?Bool | No | None | **Named parameter.** Whether the network is hidden. true indicates a hidden network, and false indicates a non-hidden network. |
| eapConfig | ?[WifiEapConfig](#class-wifieapconfig) | No | None | **Named parameter.** Extensible Authentication Protocol configuration. This field is required only when securityType is WifiSecTypeEap. |
| wapiConfig | ?[WifiWapiConfig](#class-wifiwapiconfig) | No | None | **Named parameter.** WAPI authentication protocol configuration. This field is required only when securityType is WifiSecTypeWapiCert or WifiSecTypeWapiPsk. |

### prop ssid

```cangjie
public mut prop ssid: String
```

**Functionality:** SSID of the hotspot. The maximum length is 32 bytes, and the encoding format is UTF-8.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop bssid

```cangjie
public mut prop bssid: ?String
```

**Functionality:** BSSID of the hotspot, for example, 00:11:22:33:44:55.

**Type:** ?String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop bssidType

```cangjie
public mut prop bssidType: ?DeviceAddressType
```

**Functionality:** BSSID type of the hotspot.

**Type:** ?[DeviceAddressType](#enum-deviceaddresstype)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop preSharedKey

```cangjie
public mut prop preSharedKey: String
```

**Functionality:** Key of the hotspot. The maximum length is 64 bytes. When securityType is WifiSecTypeOpen, this field must be an empty string; for other encryption types, it cannot be an empty string. When securityType is WifiSecTypeWep, the length of this field can only be one of 5, 10, 13, 26, 16, and 32 bytes, and when the field length is an even number, the field must consist of pure hexadecimal digits. When securityType is WifiSecTypeSae, the minimum length of this field is 1 byte. When securityType is WifiSecTypePsk, the minimum length of this field is 8 bytes.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop isHiddenSsid

```cangjie
public mut prop isHiddenSsid: ?Bool
```

**Functionality:** Whether the network is hidden. true indicates a hidden network, and false indicates a non-hidden network.

**Type:** ?Bool

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop securityType

```cangjie
public mut prop securityType: WifiSecurityType
```

**Functionality:** Encryption type.

**Type:** [WifiSecurityType](#enum-wifisecuritytype)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop eapConfig

```cangjie
public mut prop eapConfig: ?WifiEapConfig
```

**Functionality:** Extensible Authentication Protocol configuration. This field is required only when securityType is WifiSecTypeEap.

**Type:** ?[WifiEapConfig](#class-wifieapconfig)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop wapiConfig

```cangjie
public mut prop wapiConfig: ?WifiWapiConfig
```

**Functionality:** WAPI authentication protocol configuration. This field is required only when securityType is WifiSecTypeWapiCert or WifiSecTypeWapiPsk.

**Type:** ?[WifiWapiConfig](#class-wifiwapiconfig)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## class WifiEapConfig

```cangjie
public class WifiEapConfig {
    public mut prop eapMethod: EapMethod
    public mut prop phase2Method: Phase2Method
    public mut prop identity: String
    public mut prop anonymousIdentity: String
    public mut prop password: String
    public mut prop caCertAlias: String
    public mut prop caPath: String
    public mut prop clientCertAlias: String
    public mut prop certEntry: Array<UInt8>
    public mut prop certPassword: String
    public mut prop altSubjectMatch: String
    public mut prop domainSuffixMatch: String
    public mut prop realm: String
    public mut prop plmn: String
    public mut prop eapSubId: Int32
    public init(
        eapMethod: EapMethod,
        phase2Method: Phase2Method,
        identity: String,
        anonymousIdentity: String,
        password: String,
        caCertAlias: String,
        caPath: String,
        clientCertAlias: String,
        certEntry: Array<UInt8>,
        certPassword: String,
        altSubjectMatch: String,
        domainSuffixMatch: String,
        realm: String,
        plmn: String,
        eapSubId: Int32
    )
}
```

**Functionality:** Configuration information for the Extensible Authentication Protocol.

- WifiEapConfig is a type used to configure EAP authentication for Wi-Fi networks.
- It contains configuration items such as the EAP authentication method, the phase 2 authentication method, identity information, password, and certificates.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### init(EapMethod, Phase2Method, String, String, String, String, String, String, Array\<UInt8\>, String, String, String, String, String, Int32)

```cangjie
public init(
    eapMethod: EapMethod,
    phase2Method: Phase2Method,
    identity: String,
    anonymousIdentity: String,
    password: String,
    caCertAlias: String,
    caPath: String,
    clientCertAlias: String,
    certEntry: Array<UInt8>,
    certPassword: String,
    altSubjectMatch: String,
    domainSuffixMatch: String,
    realm: String,
    plmn: String,
    eapSubId: Int32
)
```

**Functionality:** Constructs a WifiEapConfig instance.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eapMethod | [EapMethod](#enum-eapmethod) | Yes | - | EAP authentication method. |
| phase2Method | [Phase2Method](#enum-phase2method) | Yes | - | Phase 2 authentication method. This parameter is required only when eapMethod is EapPeap or EapTtls. |
| identity | String | Yes | - | Identity information. When eapMethod is EapPeap, EapTls, or EapPwd, this field cannot be an empty string. |
| anonymousIdentity | String | Yes | - | Anonymous identity. Not used yet. |
| password | String | Yes | - | Password. When eapMethod is EapPeap or EapPwd, this field cannot be an empty string, and the maximum length is 128 bytes. |
| caCertAlias | String | Yes | - | CA certificate alias. |
| caPath | String | Yes | - | CA certificate path. |
| clientCertAlias | String | Yes | - | Client certificate alias. |
| certEntry | Array\<UInt8\> | Yes | - | CA certificate content. When eapMethod is EapTls, if this field is empty, clientCertAlias cannot be empty. |
| certPassword | String | Yes | - | CA certificate password. The maximum length is 128 bytes. |
| altSubjectMatch | String | Yes | - | Alternative subject match. |
| domainSuffixMatch | String | Yes | - | Domain suffix match. |
| realm | String | Yes | - | Realm of the passpoint credential. |
| plmn | String | Yes | - | Passpoint credential provider for the public land mobile network. |
| eapSubId | Int32 | Yes | - | Sub-ID of the SIM card. |

### prop eapMethod

```cangjie
public mut prop eapMethod: EapMethod
```

**Functionality:** EAP authentication method.

**Type:** [EapMethod](#enum-eapmethod)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop phase2Method

```cangjie
public mut prop phase2Method: Phase2Method
```

**Functionality:** Phase 2 authentication method. This parameter is required only when eapMethod is EapPeap or EapTtls.

**Type:** [Phase2Method](#enum-phase2method)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop identity

```cangjie
public mut prop identity: String
```

**Functionality:** Identity information. When eapMethod is EapPeap, EapTls, or EapPwd, this field cannot be an empty string.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop anonymousIdentity

```cangjie
public mut prop anonymousIdentity: String
```

**Functionality:** Anonymous identity. Not used yet.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop password

```cangjie
public mut prop password: String
```

**Functionality:** Password. When eapMethod is EapPeap or EapPwd, this field cannot be an empty string, and the maximum length is 128 bytes.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop caCertAlias

```cangjie
public mut prop caCertAlias: String
```

**Functionality:** CA certificate alias.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop caPath

```cangjie
public mut prop caPath: String
```

**Functionality:** CA certificate path.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop clientCertAlias

```cangjie
public mut prop clientCertAlias: String
```

**Functionality:** Client certificate alias.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop certEntry

```cangjie
public mut prop certEntry: Array<UInt8>
```

**Functionality:** CA certificate content. When eapMethod is EapTls, if this field is empty, clientCertAlias cannot be empty.

**Type:** Array\<UInt8\>

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop certPassword

```cangjie
public mut prop certPassword: String
```

**Functionality:** CA certificate password. The maximum length is 128 bytes.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop altSubjectMatch

```cangjie
public mut prop altSubjectMatch: String
```

**Functionality:** Alternative subject match.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop domainSuffixMatch

```cangjie
public mut prop domainSuffixMatch: String
```

**Functionality:** Domain suffix match.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop realm

```cangjie
public mut prop realm: String
```

**Functionality:** Realm of the passpoint credential.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop plmn

```cangjie
public mut prop plmn: String
```

**Functionality:** Passpoint credential provider for the public land mobile network.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop eapSubId

```cangjie
public mut prop eapSubId: Int32
```

**Functionality:** Sub-ID of the SIM card.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## class Ipv6Info

```cangjie
public class Ipv6Info {
    public mut prop linkIpv6Address: String
    public mut prop globalIpv6Address: String
    public mut prop randomGlobalIpv6Address: String
    public mut prop uniqueIpv6Address: ?String
    public mut prop randomUniqueIpv6Address: ?String
    public mut prop gateway: String
    public mut prop netmask: String
    public mut prop primaryDNS: String
    public mut prop secondDNS: String
}
```

**Functionality:** IPv6 information.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop linkIpv6Address

```cangjie
public mut prop linkIpv6Address: String
```

**Functionality:** Link IPv6 address.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop globalIpv6Address

```cangjie
public mut prop globalIpv6Address: String
```

**Functionality:** Global IPv6 address.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop randomGlobalIpv6Address

```cangjie
public mut prop randomGlobalIpv6Address: String
```

**Functionality:** Random global IPv6 address. Reserved field, not supported yet.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop uniqueIpv6Address

```cangjie
public mut prop uniqueIpv6Address: ?String
```

**Functionality:** Unique local IPv6 address.

**Type:** ?String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop randomUniqueIpv6Address

```cangjie
public mut prop randomUniqueIpv6Address: ?String
```

**Functionality:** Random unique local IPv6 address.

**Type:** ?String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop gateway

```cangjie
public mut prop gateway: String
```

**Functionality:** Gateway.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop netmask

```cangjie
public mut prop netmask: String
```

**Functionality:** Network mask.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop primaryDNS

```cangjie
public mut prop primaryDNS: String
```

**Functionality:** IPv6 address of the primary DNS server.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop secondDNS

```cangjie
public mut prop secondDNS: String
```

**Functionality:** IPv6 address of the secondary DNS server.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## class IpInfo

```cangjie
public class IpInfo {
    public mut prop ipAddress: UInt32
    public mut prop gateway: UInt32
    public mut prop netmask: UInt32
    public mut prop primaryDns: UInt32
    public mut prop secondDns: UInt32
    public mut prop serverIp: UInt32
    public mut prop leaseDuration: UInt32
}
```

**Functionality:** IPv4 information.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop ipAddress

```cangjie
public mut prop ipAddress: UInt32
```

**Functionality:** IP address. The value is of the UInt32 type, and applications can convert it to common formats such as dotted decimal notation as required.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop gateway

```cangjie
public mut prop gateway: UInt32
```

**Functionality:** Gateway.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop netmask

```cangjie
public mut prop netmask: UInt32
```

**Functionality:** Mask.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop primaryDns

```cangjie
public mut prop primaryDns: UInt32
```

**Functionality:** IP address of the primary DNS server.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop secondDns

```cangjie
public mut prop secondDns: UInt32
```

**Functionality:** IP address of the secondary DNS server.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop serverIp

```cangjie
public mut prop serverIp: UInt32
```

**Functionality:** IP address of the DHCP server.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop leaseDuration

```cangjie
public mut prop leaseDuration: UInt32
```

**Functionality:** Lease duration of the IP address, in seconds.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## class ConnectSettings

```cangjie
public class ConnectSettings {
    public mut prop networkId: Int32
    public mut prop withUserAction: ?Bool
    public mut prop userActionTimeout: ?Int32
    public mut prop addNetworkToSystem: ?Bool
    public init(
        networkId: Int32
    )
}
```

**Functionality:** Information about Wi-Fi connection settings.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### init(Int32)

```cangjie
public init(
    networkId: Int32
)
```

**Functionality:** Constructs a ConnectSettings instance.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| networkId | Int32 | Yes | - | ID of the candidate network configuration. |

### prop networkId

```cangjie
public mut prop networkId: Int32
```

**Functionality:** ID of the candidate network configuration.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop withUserAction

```cangjie
public mut prop withUserAction: ?Bool
```

**Functionality:** Whether to prompt the user for trust confirmation during connection. true indicates that the user is prompted for confirmation, false indicates that the user is not prompted for confirmation, and the default value is false.

**Type:** ?Bool

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop userActionTimeout

```cangjie
public mut prop userActionTimeout: ?Int32
```

**Functionality:** Time to wait for user confirmation, in seconds. The value range is 1 to 30, and the default value is 10.

**Type:** ?Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop addNetworkToSystem

```cangjie
public mut prop addNetworkToSystem: ?Bool
```

**Functionality:** Whether to add the suggested network to system networks. true indicates that the network is added to system networks, false indicates that it remains a suggested network, and the default value is false.

**Type:** ?Bool

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## class WifiInfoElement

```cangjie
public class WifiInfoElement {
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

## class WifiLinkedInfo

```cangjie
public class WifiLinkedInfo {
    public mut prop ssid: String
    public mut prop bssid: String
    public mut prop rssi: Int32
    public mut prop band: Int32
    public mut prop frequency: Int32
}
```

**Functionality:** Provides information about the Wi-Fi connection.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop ssid

```cangjie
public mut prop ssid: String
```

**Functionality:** SSID of the hotspot (Service Set Identifier), which is used to obtain the public name (that is, the name of the wireless network) of the Wi-Fi hotspot to which the current device is connected. The encoding format is UTF-8.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop bssid

```cangjie
public mut prop bssid: String
```

**Functionality:** BSSID of the hotspot (Basic Service Set Identifier), that is, the MAC address of the wireless network.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop rssi

```cangjie
public mut prop rssi: Int32
```

**Functionality:** Signal strength of the hotspot (dBm). RSSI (Received Signal Strength Indicator) has a standard value range of -127 dBm to 0 dBm. In normal usage scenarios, the common valid range is -100 dBm (weak signal) to -30 dBm (strong signal), and a value close to 0 dBm indicates an extremely strong signal.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop band

```cangjie
public mut prop band: Int32
```

**Functionality:** Band of the Wi-Fi access point. 1 indicates 2.4 GHz, and 2 indicates 5 GHz.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop frequency

```cangjie
public mut prop frequency: Int32
```

**Functionality:** Frequency of the Wi-Fi access point.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

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

## class WifiP2pLinkedInfo

```cangjie
public class WifiP2pLinkedInfo {
    public mut prop connectState: P2pConnectState
    public mut prop isGroupOwner: Bool
    public mut prop groupOwnerAddr: String
}
```

**Functionality:** Provides information about the Wi-Fi connection.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop connectState

```cangjie
public mut prop connectState: P2pConnectState
```

**Functionality:** P2P connection state.

**Type:** [P2pConnectState](#enum-p2pconnectstate)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop isGroupOwner

```cangjie
public mut prop isGroupOwner: Bool
```

**Functionality:** true indicates that the device is the group owner, and false indicates that it is not.

**Type:** Bool

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop groupOwnerAddr

```cangjie
public mut prop groupOwnerAddr: String
```

**Functionality:** Group IP address.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

## class WifiP2pGroupInfo

```cangjie
public class WifiP2pGroupInfo {
    public mut prop isP2pGo: Bool
    public mut prop ownerInfo: WifiP2pDevice
    public mut prop passphrase: String
    public mut prop interfaceName: String
    public mut prop groupName: String
    public mut prop networkId: Int32
    public mut prop frequency: Int32
    public mut prop clientDevices: Array<WifiP2pDevice>
    public mut prop goIpAddress: String
}
```

**Functionality:** Indicates P2P group information.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop isP2pGo

```cangjie
public mut prop isP2pGo: Bool
```

**Functionality:** Whether the device is the group owner. true means it is the group owner, and false means it is not.

**Type:** Bool

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop ownerInfo

```cangjie
public mut prop ownerInfo: WifiP2pDevice
```

**Functionality:** Device information of the group.

**Type:** [WifiP2pDevice](#class-wifip2pdevice)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop passphrase

```cangjie
public mut prop passphrase: String
```

**Functionality:** Group passphrase.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop interfaceName

```cangjie
public mut prop interfaceName: String
```

**Functionality:** Name of the network interface used by the P2P group, for example, wlan0.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop groupName

```cangjie
public mut prop groupName: String
```

**Functionality:** Group name.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop networkId

```cangjie
public mut prop networkId: Int32
```

**Functionality:** Network ID.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop frequency

```cangjie
public mut prop frequency: Int32
```

**Functionality:** Frequency of the group.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop clientDevices

```cangjie
public mut prop clientDevices: Array<WifiP2pDevice>
```

**Functionality:** Information about the list of connected devices.

**Type:** Array\<[WifiP2pDevice](#class-wifip2pdevice)\>

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop goIpAddress

```cangjie
public mut prop goIpAddress: String
```

**Functionality:** IP address of the group.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

## class WifiP2pDevice

```cangjie
public class WifiP2pDevice {
    public mut prop deviceName: String
    public mut prop deviceAddress: String
    public mut prop deviceAddressType: ?DeviceAddressType
    public mut prop primaryDeviceType: String
    public mut prop deviceStatus: P2pDeviceStatus
    public mut prop groupCapabilities: Int32
    public init(
        deviceName: String,
        deviceAddress: String,
        primaryDeviceType: String,
        deviceStatus: P2pDeviceStatus,
        groupCapabilities: Int32,
        deviceAddressType!: ?DeviceAddressType = None
    )
}
```

**Functionality:** Indicates P2P device information.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### init(String, String, String, P2pDeviceStatus, Int32, ?DeviceAddressType)

```cangjie
public init(
    deviceName: String,
    deviceAddress: String,
    primaryDeviceType: String,
    deviceStatus: P2pDeviceStatus,
    groupCapabilities: Int32,
    deviceAddressType!: ?DeviceAddressType = None
)
```

**Functionality:** Constructs a WifiP2pDevice instance.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceName | String | Yes | - | Device name. |
| deviceAddress | String | Yes | - | Device MAC address. |
| primaryDeviceType | String | Yes | - | Primary device type. |
| deviceStatus | [P2pDeviceStatus](#enum-p2pdevicestatus) | Yes | - | Device status. |
| groupCapabilities | Int32 | Yes | - | Group capabilities. |
| deviceAddressType | ?[DeviceAddressType](#enum-deviceaddresstype) | No | None | **Named parameter.** Device MAC address type. |

### prop deviceName

```cangjie
public mut prop deviceName: String
```

**Functionality:** Device name.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop deviceAddress

```cangjie
public mut prop deviceAddress: String
```

**Functionality:** Device MAC address.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop deviceAddressType

```cangjie
public mut prop deviceAddressType: ?DeviceAddressType
```

**Functionality:** Device MAC address type.

**Type:** ?[DeviceAddressType](#enum-deviceaddresstype)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop primaryDeviceType

```cangjie
public mut prop primaryDeviceType: String
```

**Functionality:** Primary device type.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop deviceStatus

```cangjie
public mut prop deviceStatus: P2pDeviceStatus
```

**Functionality:** Device status.

**Type:** [P2pDeviceStatus](#enum-p2pdevicestatus)

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

### prop groupCapabilities

```cangjie
public mut prop groupCapabilities: Int32
```

**Functionality:** Group capabilities.

**Type:** Int32

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Initial Version:** 26.1.0

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

## class WifiWapiConfig

```cangjie
public class WifiWapiConfig {
    public mut prop wapiPskType: WapiPskType
    public mut prop wapiAsCert: String
    public mut prop wapiUserCert: String
    public init(
        wapiPskType: WapiPskType,
        wapiAsCert: String,
        wapiUserCert: String
    )
}
```

**Functionality:** WAPI (Wireless LAN Authentication and Privacy Infrastructure) authentication protocol configuration.

When a user connects to a wireless network through the WAPI authentication protocol, the parameters or certificates can be configured in the following ways:
- Method 1: Connect by configuring certificates. Configure the key fields in WifiDeviceConfig as follows:
- preSharedKey does not need to be specified;
- Set securityType to WifiSecTypeWapiCert;
- In wapiConfig:
- Pass the text content of the AS certificate to wapiAsCert.
- Pass the text content of the user certificate to wapiUserCert.
- Method 2: Connect by configuring preSharedKey. Configure the key fields in WifiDeviceConfig as follows:
- Pass the password set on the router as preSharedKey;
- Set securityType to WifiSecTypeWapiPsk.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### init(WapiPskType, String, String)

```cangjie
public init(
    wapiPskType: WapiPskType,
    wapiAsCert: String,
    wapiUserCert: String
)
```

**Functionality:** Constructs a WifiWapiConfig instance.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| wapiPskType | [WapiPskType](#enum-wapipsktype) | Yes | - | Encryption type. |
| wapiAsCert | String | Yes | - | AS certificate (Authentication Server Certificate). |
| wapiUserCert | String | Yes | - | User certificate. |

### prop wapiPskType

```cangjie
public mut prop wapiPskType: WapiPskType
```

**Functionality:** Encryption type.

**Type:** [WapiPskType](#enum-wapipsktype)

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop wapiAsCert

```cangjie
public mut prop wapiAsCert: String
```

**Functionality:** AS certificate (Authentication Server Certificate).

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

### prop wapiUserCert

```cangjie
public mut prop wapiUserCert: String
```

**Functionality:** User certificate.

**Type:** String

**System Capability:** SystemCapability.Communication.WiFi.STA

**Initial Version:** 26.1.0

## enum DeviceAddressType

```cangjie
public enum DeviceAddressType <: Equatable<DeviceAddressType> & ToString {
    | RandomDeviceAddress
    | RealDeviceAddress
    | ...
}
```

**Description:** Type of the Wi-Fi device address (MAC/BSSID).

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parent Types:**

- Equatable\<[DeviceAddressType](#enum-deviceaddresstype)>
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

**Description:** Checks whether two enum values are not equal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DeviceAddressType](#enum-deviceaddresstype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal; otherwise, returns false. |

### func ==(DeviceAddressType)

```cangjie
public operator func ==(other: DeviceAddressType): Bool
```

**Description:** Checks whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [DeviceAddressType](#enum-deviceaddresstype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enumeration. |

## enum EapMethod

```cangjie
public enum EapMethod <: Equatable<EapMethod> & ToString {
    | EapNone
    | EapPeap
    | EapTls
    | EapTtls
    | EapPwd
    | EapSim
    | EapAka
    | EapAkaPrime
    | EapUnauthTls
}
```

**Description:** Enumeration of EAP authentication methods.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapNone

```cangjie
EapNone
```

**Description:** Not specified.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapPeap

```cangjie
EapPeap
```

**Description:** PEAP type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapTls

```cangjie
EapTls
```

**Description:** TLS type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapTtls

```cangjie
EapTtls
```

**Description:** TTLS type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapPwd

```cangjie
EapPwd
```

**Description:** PWD type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapSim

```cangjie
EapSim
```

**Description:** SIM type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapAka

```cangjie
EapAka
```

**Description:** AKA type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapAkaPrime

```cangjie
EapAkaPrime
```

**Description:** AKA Prime type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### EapUnauthTls

```cangjie
EapUnauthTls
```

**Description:** UNAUTH TLS type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### func !=(EapMethod)

```cangjie
public operator func !=(other: EapMethod): Bool
```

**Description:** Checks whether two enum values are not equal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [EapMethod](#enum-eapmethod) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal; otherwise, returns false. |

### func ==(EapMethod)

```cangjie
public operator func ==(other: EapMethod): Bool
```

**Description:** Checks whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [EapMethod](#enum-eapmethod) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | Description of the enumeration. |

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

## enum P2pDeviceStatus

```cangjie
public enum P2pDeviceStatus <: Equatable<P2pDeviceStatus> & ToString {
    | Connected
    | Invited
    | Failed
    | Available
    | Unavailable
}
```

**Description:** Represents the device status.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Connected

```cangjie
Connected
```

**Description:** Connected state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Invited

```cangjie
Invited
```

**Description:** Invited state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Failed

```cangjie
Failed
```

**Description:** Failed state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Available

```cangjie
Available
```

**Description:** Available state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Unavailable

```cangjie
Unavailable
```

**Description:** Unavailable state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### func !=(P2pDeviceStatus)

```cangjie
public operator func !=(other: P2pDeviceStatus): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [P2pDeviceStatus](#enum-p2pdevicestatus) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(P2pDeviceStatus)

```cangjie
public operator func ==(other: P2pDeviceStatus): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [P2pDeviceStatus](#enum-p2pdevicestatus) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum P2pConnectState

```cangjie
public enum P2pConnectState <: Equatable<P2pConnectState> & ToString {
    | Disconnected
    | Connected
}
```

**Description:** Represents the P2P connection status.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Disconnected

```cangjie
Disconnected
```

**Description:** Disconnected state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### Connected

```cangjie
Connected
```

**Description:** Connected state.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

### func !=(P2pConnectState)

```cangjie
public operator func !=(other: P2pConnectState): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [P2pConnectState](#enum-p2pconnectstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(P2pConnectState)

```cangjie
public operator func ==(other: P2pConnectState): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [P2pConnectState](#enum-p2pconnectstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.P2P

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum WifiBandType

```cangjie
public enum WifiBandType <: Equatable<WifiBandType> & ToString {
    | WifiBandNone
    | WifiBand2g
    | WifiBand5g
    | WifiBand6g
    | WifiBand60g
}
```

**Description:** Represents the WIFI band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### WifiBandNone

```cangjie
WifiBandNone
```

**Description:** Invalid band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### WifiBand2g

```cangjie
WifiBand2g
```

**Description:** 2.4 GHz band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### WifiBand5g

```cangjie
WifiBand5g
```

**Description:** 5 GHz band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### WifiBand6g

```cangjie
WifiBand6g
```

**Description:** 6 GHz band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### WifiBand60g

```cangjie
WifiBand60g
```

**Description:** 60 GHz band type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### func !=(WifiBandType)

```cangjie
public operator func !=(other: WifiBandType): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WifiBandType](#enum-wifibandtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(WifiBandType)

```cangjie
public operator func ==(other: WifiBandType): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WifiBandType](#enum-wifibandtype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum WapiPskType

```cangjie
public enum WapiPskType <: Equatable<WapiPskType> & ToString {
    | WapiPskAscii
    | WapiPskHex
}
```

**Description:** Enum of WAPI authentication modes.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

### WapiPskAscii

```cangjie
WapiPskAscii
```

**Description:** ASCII type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

### WapiPskHex

```cangjie
WapiPskHex
```

**Description:** HEX type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

### func !=(WapiPskType)

```cangjie
public operator func !=(other: WapiPskType): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WapiPskType](#enum-wapipsktype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(WapiPskType)

```cangjie
public operator func ==(other: WapiPskType): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WapiPskType](#enum-wapipsktype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |

## enum Phase2Method

```cangjie
public enum Phase2Method <: Equatable<Phase2Method> & ToString {
    | Phase2None
    | Phase2Pap
    | Phase2Mschap
    | Phase2Mschapv2
    | Phase2Gtc
    | Phase2Sim
    | Phase2Aka
    | Phase2AkaPrime
}
```

**Description:** Represents the enum of phase 2 authentication methods.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2None

```cangjie
Phase2None
```

**Description:** Not specified.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Pap

```cangjie
Phase2Pap
```

**Description:** PAP type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Mschap

```cangjie
Phase2Mschap
```

**Description:** MSCHAP type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Mschapv2

```cangjie
Phase2Mschapv2
```

**Description:** MSCHAPv2 type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Gtc

```cangjie
Phase2Gtc
```

**Description:** GTC type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Sim

```cangjie
Phase2Sim
```

**Description:** SIM type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2Aka

```cangjie
Phase2Aka
```

**Description:** AKA type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### Phase2AkaPrime

```cangjie
Phase2AkaPrime
```

**Description:** AKA Prime type.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

### func !=(Phase2Method)

```cangjie
public operator func !=(other: Phase2Method): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Phase2Method](#enum-phase2method) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(Phase2Method)

```cangjie
public operator func ==(other: Phase2Method): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Phase2Method](#enum-phase2method) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.STA

**Since:** 26.1.0

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

## enum WifiSecurityType

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

**Description:** Represents the encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parent Types:**

- Equatable\<[WifiSecurityType](#enum-wifisecuritytype)>
- ToString

### WifiSecTypeEap

```cangjie
WifiSecTypeEap
```

**Description:** EAP encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeEapSuiteB

```cangjie
WifiSecTypeEapSuiteB
```

**Description:** Suite-B 192-bit encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeInvalid

```cangjie
WifiSecTypeInvalid
```

**Description:** Invalid encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeOpen

```cangjie
WifiSecTypeOpen
```

**Description:** Open encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeOwe

```cangjie
WifiSecTypeOwe
```

**Description:** Opportunistic Wireless Encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypePsk

```cangjie
WifiSecTypePsk
```

**Description:** Pre-shared key (PSK) encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeSae

```cangjie
WifiSecTypeSae
```

**Description:** Simultaneous Authentication of Equals (SAE) encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWapiCert

```cangjie
WifiSecTypeWapiCert
```

**Description:** WAPI-Cert encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWapiPsk

```cangjie
WifiSecTypeWapiPsk
```

**Description:** WAPI-PSK encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### WifiSecTypeWep

```cangjie
WifiSecTypeWep
```

**Description:** Wired Equivalent Privacy (WEP) encryption type. Candidate network configuration does not support this encryption type.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

### func !=(WifiSecurityType)

```cangjie
public operator func !=(other: WifiSecurityType): Bool
```

**Description:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WifiSecurityType](#enum-wifisecuritytype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise returns `false`. |

### func ==(WifiSecurityType)

```cangjie
public operator func ==(other: WifiSecurityType): Bool
```

**Description:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [WifiSecurityType](#enum-wifisecuritytype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**System Capability:** SystemCapability.Communication.WiFi.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |
