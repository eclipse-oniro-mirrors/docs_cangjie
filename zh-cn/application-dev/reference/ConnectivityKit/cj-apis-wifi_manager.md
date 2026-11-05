# ohos.wifi_manager（WLAN）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

wifi_manager模块主要提供WLAN基础功能、P2P（peer-to-peer）功能和WLAN消息通知的相应服务，让应用可以通过WLAN和其余设备互联互通。

## 导入模块

```cangjie
import kit.ConnectivityKit.*
```

## 权限列表

ohos.permission.GET_WIFI_INFO

ohos.permission.SET_WIFI_INFO

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func createGroup(WifiP2pConfig)

```cangjie
public func createGroup(config: WifiP2pConfig): Unit
```

**功能：** 创建群组。创建群组后，可调用removeGroup移除已创建的群组。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|config|[WifiP2pConfig](#class-wifip2pconfig)|是|-|群组配置信息。如果DeviceAddressType未指定值，则DeviceAddressType默认为随机设备地址类型。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 获取P2P本端设备信息，结果通过回调函数异步返回。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[WifiP2pDevice](#class-wifip2pdevice)\>|是|-|回调函数。当操作成功时，err为0，data表示本端设备信息。如果err为非0，表示处理出现错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 获取P2P对端设备列表信息。结果通过回调函数异步返回。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Array\<[WifiP2pDevice](#class-wifip2pdevice)\>\>|是|-|回调函数。当操作成功时，err为0，data表示对端设备列表信息。如果err为非0，表示处理出现错误。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 获取P2P当前组信息。结果通过回调函数异步返回。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[WifiP2pGroupInfo](#class-wifip2pgroupinfo)\>|是|-|回调函数。当操作成功时，err为0，data表示当前组信息。如果err为非0，表示处理出现错误。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限，则返回结果中的deviceAddress为真实设备地址，否则为随机设备地址。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |

**示例：**

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

**功能：** 获取P2P连接信息。结果通过回调函数异步返回。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[WifiP2pLinkedInfo](#class-wifip2plinkedinfo)\>|是|-|回调函数。当操作成功时，err为0，data表示P2P连接信息。如果err为非0，表示处理出现错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 获取国家码信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|国家码。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2401000 | Operation failed. |

**示例：**

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

**功能：** 获取IPV6信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|[Ipv6Info](#class-ipv6info)|Ipv6信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 获取IPV4信息。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|[IpInfo](#class-ipinfo)|IP信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 获取Wi-Fi连接信息，使用同步方式返回结果。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|[WifiLinkedInfo](#class-wifilinkedinfo)|表示Wi-Fi连接信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 应用使用该接口连接到自己添加的候选网络，支持设置自定义参数。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|settings|[ConnectSettings](#class-connectsettings)|是|-|连接Wi-Fi设置信息。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit\>|是|-|回调函数，用于返回候选网络连接的结果。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |
  | 2501005 | The user does not respond. |
  | 2501006 | The user refused the action. |
  | 2501007 | Parameter validation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let settings = ConnectSettings(0) // 0 为候选网络 ID
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

**功能：** 获取候选网络配置。

- 候选网络是指曾经连接过或者手动添加的网络配置。
- 该接口返回当前应用添加的所有已保存但当前未连接的Wi-Fi候选网络配置。
- 用于展示可连接的网络列表。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Array\<[WifiDeviceConfig](#class-wifideviceconfig)\>|候选网络配置数组。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 添加候选网络配置，结果通过回调函数异步返回。

- 将指定的Wi-Fi设备配置添加为候选网络，添加后的网络在没有连接记录的情况下无法触发自动回连，可以通过connectToCandidateConfig或connectToCandidateConfigWithUserAction方法实现候选网络连接，页面确认连接成功后，可实现自动回连。
- 候选网络属于应用维度添加的网络配置，和系统网络配置是相互隔离的，在系统Wi-Fi页面不可见。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|config|[WifiDeviceConfig](#class-wifideviceconfig)|是|-|Wi-Fi配置信息。如果bssidType未指定值，则bssidType默认为随机设备地址类型。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32\>|是|-|回调函数。error为0时：操作成功，data为添加的网络配置ID，如果data值为-1，表示添加失败。 error为非0值时：操作出现错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 获取扫描结果。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Array\<[WifiScanInfo](#class-wifiscaninfo)>|返回扫描到的热点列表。如果应用申请了ohos.permission.GET_WIFI_PEERS_MAC权限（仅系统应用可申请），则返回结果中的bssid为真实设备地址，否则为随机设备地址。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 判断当前频段是否支持。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|bandType|[WifiBandType](#enum-wifibandtype)|是|-|Wifi 频段类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true:支持， false:不支持。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 判断设备是否支持指定的Wi-Fi特性。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|featureId|Int64|是|-|特性ID值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true:支持， false:不支持。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2401000 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let featureId: Int64 = 0x0008 // 0x0008 表示 Wifi-Direct 特性
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

**功能：** 查询Wi-Fi是否已连接。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true:已连接， false:未连接。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 查询Wi-Fi信号强度。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|rssi|Int32|是|-|热点的信号强度(dBm)。|
|band|Int32|是|-|Wi-Fi接入点的频段，1表示2.4GHz；2表示5GHz。|

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|信号强度，取值范围为[0, 4]。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let level = getSignalLevel(-60, 2) // rssi 为 -60dBm，band 为 2 表示 5GHz
Hilog.info(0, "test", "signal level: ${level}")
```

## func isWifiActive()

```cangjie
public func isWifiActive(): Bool
```

**功能：** 查询WLAN是否已使能。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true:已使能，false:未使能。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 取消注册WLAN状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|eventType|[WifiCallbackType](#enum-wificallbacktype)|是|-|回调事件。|
|callback|?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject)|否|None| **命名参数。** 状态改变回调函数。如果callback没有传入参数，将取消注册该事件关联的所有回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.*

class WifiCallback <: Callback1Argument<Int32> {
    public func invoke(err: ?BusinessException, arg: Int32) {
        Hilog.info(0, "test", "invoke success", "")
    }
}

try {
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

**功能：** 注册WLAN状态改变事件。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|eventType|[WifiCallbackType](#enum-wificallbacktype)|是|-|回调事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Int32>|是|-|状态改变回调函数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.*

class WifiCallback <: Callback1Argument<Int32> {
    public func invoke(err: ?BusinessException, arg: Int32) {
        Hilog.info(0, "test", "invoke success", "")
    }
}

try {
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

**功能：** 在P2P连接过程中，取消P2P连接。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

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

## func p2pConnect(WifiP2pConfig)

```cangjie
public func p2pConnect(config: WifiP2pConfig): Unit
```

**功能：** 执行P2P连接。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|config|[WifiP2pConfig](#class-wifip2pconfig)|是|-|连接配置信息。如果DeviceAddressType未指定值，则DeviceAddressType默认为随机设备地址类型。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let config = WifiP2pConfig("xx:xx:xx:xx", -2, "", "", GroupOwnerBand.GoBandAuto)
    p2pConnect(config)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func removeGroup()

```cangjie
public func removeGroup(): Unit
```

**功能：** 移除群组。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2801001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 移除指定的候选网络配置，结果通过回调函数异步返回。

- 从系统中删除指定网络ID的Wi-Fi候选配置，清理不再需要的Wi-Fi候选配置，释放系统资源。
- 只能移除通过addCandidateConfig添加的候选配置，移除后该候选网络将不再被系统自动连接。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|networkId|Int32|是|-|网络配置ID。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit\>|是|-|回调函数。当操作成功时，error为0。如果error为非0，表示处理出现错误。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

let networkId = 0 // 候选网络 ID，可由 addCandidateConfig 的回调获取
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

**功能：** 开始发现设备。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

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

**功能：** 启动Wi-Fi扫描。

- 应用程序在前台运行时，两分钟内最多可扫描四次。
- 在后台运行时，三十分钟内最多可扫描一次。
- 通过on('wifiScanStateChange')订阅扫描状态变更事件，监听扫描完成通知。

**需要权限：** ohos.permission.SET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2501000 | Operation failed. |

**示例：**

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

**功能：** 停止发现设备。

**需要权限：** ohos.permission.GET_WIFI_INFO

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[WIFI错误码](./cj-errorcode-wifi-manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2801000 | Operation failed. |
  | 2501001 | Wi-Fi STA disabled. |

**示例：**

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
```

## class WifiDeviceConfig

```cangjie
public class WifiDeviceConfig {
    public mut prop ssid: String
    public mut prop bssid: ?String
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

**功能：** Wi-Fi配置信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** 构造WifiDeviceConfig实例。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|ssid|String|是|-|热点的SSID，最大长度为32字节，编码格式为UTF-8。|
|preSharedKey|String|是|-|热点的密钥，最大长度为64字节。 当securityType为WifiSecTypeOpen时该字段需为空串，其余加密类型不能为空串。 当securityType为WifiSecTypeWep时，该字段长度只允许为5、10、13、26、16和32字节其中之一，并且当字段长度为偶数时，该字段必须为纯十六进制数字构成。 当securityType为WifiSecTypeSae时，该字段最小长度为1字节。 当securityType为WifiSecTypePsk时，该字段最小长度为8字节。|
|securityType|[WifiSecurityType](#enum-wifisecuritytype)|是|-|加密类型。|
|bssid|?String|否|None|**命名参数。** 热点的BSSID，例如：00:11:22:33:44:55。|
|bssidType|?[DeviceAddressType](#enum-deviceaddresstype)|否|None|**命名参数。** 热点的BSSID类型。|
|isHiddenSsid|?Bool|否|None|**命名参数。** 是否是隐藏网络。true表示是隐藏网络，false表示不是隐藏网络。|
|eapConfig|?[WifiEapConfig](#class-wifieapconfig)|否|None|**命名参数。** 可扩展身份验证协议配置。只有securityType为WifiSecTypeEap时需要填写。|
|wapiConfig|?[WifiWapiConfig](#class-wifiwapiconfig)|否|None|**命名参数。** WAPI身份验证协议配置。只有securityType为WifiSecTypeWapiCert或WifiSecTypeWapiPsk时需要填写。|

### prop ssid

```cangjie
public mut prop ssid: String
```

**功能：** 热点的SSID，最大长度为32字节，编码格式为UTF-8。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop bssid

```cangjie
public mut prop bssid: ?String
```

**功能：** 热点的BSSID，例如：00:11:22:33:44:55。

**类型：** ?String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop preSharedKey

```cangjie
public mut prop preSharedKey: String
```

**功能：** 热点的密钥，最大长度为64字节。 当securityType为WifiSecTypeOpen时该字段需为空串，其余加密类型不能为空串。 当securityType为WifiSecTypeWep时，该字段长度只允许为5、10、13、26、16和32字节其中之一，并且当字段长度为偶数时，该字段必须为纯十六进制数字构成。 当securityType为WifiSecTypeSae时，该字段最小长度为1字节。 当securityType为WifiSecTypePsk时，该字段最小长度为8字节。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop isHiddenSsid

```cangjie
public mut prop isHiddenSsid: ?Bool
```

**功能：** 是否是隐藏网络。true表示是隐藏网络，false表示不是隐藏网络。

**类型：** ?Bool

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop securityType

```cangjie
public mut prop securityType: WifiSecurityType
```

**功能：** 加密类型。

**类型：** [WifiSecurityType](#enum-wifisecuritytype)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop eapConfig

```cangjie
public mut prop eapConfig: ?WifiEapConfig
```

**功能：** 可扩展身份验证协议配置。只有securityType为WifiSecTypeEap时需要填写。

**类型：** ?[WifiEapConfig](#class-wifieapconfig)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop wapiConfig

```cangjie
public mut prop wapiConfig: ?WifiWapiConfig
```

**功能：** WAPI身份验证协议配置。只有securityType为WifiSecTypeWapiCert或WifiSecTypeWapiPsk时需要填写。

**类型：** ?[WifiWapiConfig](#class-wifiwapiconfig)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** 可扩展身份验证协议配置信息。

- WifiEapConfig是一个用于配置Wi-Fi网络EAP身份验证的类型。
- 包含EAP身份验证方式、第二阶段身份验证方式、身份信息、密码、证书等配置项。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** 构造WifiEapConfig实例。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|eapMethod|[EapMethod](#enum-eapmethod)|是|-|EAP身份验证方式。|
|phase2Method|[Phase2Method](#enum-phase2method)|是|-|第二阶段身份验证方式。只有eapMethod为EapPeap或EapTtls时需要填写。|
|identity|String|是|-|身份信息。当eapMethod为EapPeap、EapTls或EapPwd时，该字段不能为空串。|
|anonymousIdentity|String|是|-|匿名身份。暂未使用。|
|password|String|是|-|密码。当eapMethod为EapPeap或EapPwd时，该字段不能为空串，最大长度为128字节。|
|caCertAlias|String|是|-|CA证书别名。|
|caPath|String|是|-|CA证书路径。|
|clientCertAlias|String|是|-|客户端证书别名。|
|certEntry|Array\<UInt8\>|是|-|CA证书内容。当eapMethod为EapTls时，如果该字段为空，则clientCertAlias不能为空。|
|certPassword|String|是|-|CA证书密码，最大长度为128字节。|
|altSubjectMatch|String|是|-|替代主题匹配。|
|domainSuffixMatch|String|是|-|域后缀匹配。|
|realm|String|是|-|通行证凭证的领域。|
|plmn|String|是|-|公共陆地移动网的直通凭证提供商。|
|eapSubId|Int32|是|-|SIM卡的子ID。|

### prop eapMethod

```cangjie
public mut prop eapMethod: EapMethod
```

**功能：** EAP身份验证方式。

**类型：** [EapMethod](#enum-eapmethod)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop phase2Method

```cangjie
public mut prop phase2Method: Phase2Method
```

**功能：** 第二阶段身份验证方式。只有eapMethod为EapPeap或EapTtls时需要填写。

**类型：** [Phase2Method](#enum-phase2method)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop identity

```cangjie
public mut prop identity: String
```

**功能：** 身份信息。当eapMethod为EapPeap、EapTls或EapPwd时，该字段不能为空串。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop anonymousIdentity

```cangjie
public mut prop anonymousIdentity: String
```

**功能：** 匿名身份。暂未使用。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop password

```cangjie
public mut prop password: String
```

**功能：** 密码。当eapMethod为EapPeap或EapPwd时，该字段不能为空串，最大长度为128字节。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop caCertAlias

```cangjie
public mut prop caCertAlias: String
```

**功能：** CA证书别名。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop caPath

```cangjie
public mut prop caPath: String
```

**功能：** CA证书路径。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop clientCertAlias

```cangjie
public mut prop clientCertAlias: String
```

**功能：** 客户端证书别名。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop certEntry

```cangjie
public mut prop certEntry: Array<UInt8>
```

**功能：** CA证书内容。当eapMethod为EapTls时，如果该字段为空，则clientCertAlias不能为空。

**类型：** Array\<UInt8\>

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop certPassword

```cangjie
public mut prop certPassword: String
```

**功能：** CA证书密码，最大长度为128字节。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop altSubjectMatch

```cangjie
public mut prop altSubjectMatch: String
```

**功能：** 替代主题匹配。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop domainSuffixMatch

```cangjie
public mut prop domainSuffixMatch: String
```

**功能：** 域后缀匹配。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop realm

```cangjie
public mut prop realm: String
```

**功能：** 通行证凭证的领域。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop plmn

```cangjie
public mut prop plmn: String
```

**功能：** 公共陆地移动网的直通凭证提供商。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop eapSubId

```cangjie
public mut prop eapSubId: Int32
```

**功能：** SIM卡的子ID。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** Ipv6信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop linkIpv6Address

```cangjie
public mut prop linkIpv6Address: String
```

**功能：** 链路Ipv6地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop globalIpv6Address

```cangjie
public mut prop globalIpv6Address: String
```

**功能：** 全局Ipv6地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop randomGlobalIpv6Address

```cangjie
public mut prop randomGlobalIpv6Address: String
```

**功能：** 随机全局Ipv6地址。 预留字段，暂不支持。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop uniqueIpv6Address

```cangjie
public mut prop uniqueIpv6Address: ?String
```

**功能：** 唯一本地Ipv6地址。

**类型：** ?String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop randomUniqueIpv6Address

```cangjie
public mut prop randomUniqueIpv6Address: ?String
```

**功能：** 随机唯一本地Ipv6地址。

**类型：** ?String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop gateway

```cangjie
public mut prop gateway: String
```

**功能：** 网关。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop netmask

```cangjie
public mut prop netmask: String
```

**功能：** 网络掩码。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop primaryDNS

```cangjie
public mut prop primaryDNS: String
```

**功能：** 主DNS服务器Ipv6地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop secondDNS

```cangjie
public mut prop secondDNS: String
```

**功能：** 备DNS服务器Ipv6地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** IPV4信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop ipAddress

```cangjie
public mut prop ipAddress: UInt32
```

**功能：** IP 地址。返回值为 UInt32 类型，应用可按需转换为点分十进制等常用格式。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop gateway

```cangjie
public mut prop gateway: UInt32
```

**功能：** 网关。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop netmask

```cangjie
public mut prop netmask: UInt32
```

**功能：** 掩码。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop primaryDns

```cangjie
public mut prop primaryDns: UInt32
```

**功能：** 主DNS服务器IP地址。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop secondDns

```cangjie
public mut prop secondDns: UInt32
```

**功能：** 备DNS服务器IP地址。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop serverIp

```cangjie
public mut prop serverIp: UInt32
```

**功能：** DHCP服务端IP地址。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop leaseDuration

```cangjie
public mut prop leaseDuration: UInt32
```

**功能：** IP地址租用时长，单位：秒。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

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

**功能：** 连接Wi-Fi设置信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### init(Int32)

```cangjie
public init(
    networkId: Int32
)
```

**功能：** 构造ConnectSettings实例。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|networkId|Int32|是|-|候选网络配置的ID。|

### prop networkId

```cangjie
public mut prop networkId: Int32
```

**功能：** 候选网络配置的ID。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop withUserAction

```cangjie
public mut prop withUserAction: ?Bool
```

**功能：** 连接时是否提示用户进行信任确认。true 表示提示用户确认，false 表示不提示用户确认，默认值为 false。

**类型：** ?Bool

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop userActionTimeout

```cangjie
public mut prop userActionTimeout: ?Int32
```

**功能：** 等待用户确认的时间，单位为秒，取值范围为 1 到 30，默认值为 10。

**类型：** ?Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop addNetworkToSystem

```cangjie
public mut prop addNetworkToSystem: ?Bool
```

**功能：** 是否将建议网络添加到系统网络中。true 表示添加到系统网络，false 表示保持为建议网络，默认值为 false。

**类型：** ?Bool

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

## class WifiInfoElement

```cangjie
public class WifiInfoElement {
    public var eid: UInt32
    public var content: Array<UInt8>
}
```

**功能：** WLAN热点信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var content

```cangjie
public var content: Array<UInt8>
```

**功能：** 元素内容。

**类型：** Array\<UInt8>

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var eid

```cangjie
public var eid: UInt32
```

**功能：** 元素ID。

**类型：** UInt32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

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

**功能：** 提供Wi-Fi连接的相关信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop ssid

```cangjie
public mut prop ssid: String
```

**功能：** 热点的SSID（Service Set Identifier，服务集标识符），用于获取当前设备已连接的Wi-Fi热点的公开名称（即无线网络的名称），编码格式为UTF-8。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop bssid

```cangjie
public mut prop bssid: String
```

**功能：** 热点的BSSID（Basic Service Set Identifier，基本服务集标识符）即无线网络的MAC地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop rssi

```cangjie
public mut prop rssi: Int32
```

**功能：** 热点的信号强度(dBm)。 RSSI（Received Signal Strength Indicator，接收信号强度指示），其标准取值范围为-127dBm至0dBm。在正常使用场景下，常见有效范围为-100dBm（弱信号）至-30dBm（强信号），接近0dBm表示信号极强。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop band

```cangjie
public mut prop band: Int32
```

**功能：** Wi-Fi接入点的频段，1表示2.4GHz；2表示5GHz。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop frequency

```cangjie
public mut prop frequency: Int32
```

**功能：** Wi-Fi接入点的频率。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

## class WifiP2pConfig

```cangjie
public class WifiP2pConfig {
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

**功能：** 表示P2P配置信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var deviceAddress

```cangjie
public var deviceAddress: String
```

**功能：** 设备地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var deviceAddressType

```cangjie
public var deviceAddressType: DeviceAddressType
```

**功能：** 设备地址类型。

**类型：** [DeviceAddressType](#enum-deviceaddresstype)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var goBand

```cangjie
public var goBand: GroupOwnerBand
```

**功能：** 群组带宽。

**类型：** [GroupOwnerBand](#enum-groupownerband)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var groupName

```cangjie
public var groupName: String
```

**功能：** 群组名称。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var netId

```cangjie
public var netId: Int32
```

**功能：** 网络ID。创建群组时-1表示创建临时组，-2表示创建永久组。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### var passphrase

```cangjie
public var passphrase: String
```

**功能：** 群组密钥。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

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

**功能：** 构造WifiP2PConfig实例。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|deviceAddress|String|是|-|设备地址。|
|netId|Int32|是|-|网络ID。创建群组时-1表示创建临时组，-2表示创建永久组。|
|passphrase|String|是|-|群组密钥。|
|groupName|String|是|-|群组名称。|
|goBand|[GroupOwnerBand](#enum-groupownerband)|是|-|群组带宽。|
|deviceAddressType|[DeviceAddressType](#enum-deviceaddresstype)|否|RandomDeviceAddress| **命名参数。** 设备地址类型。|

## class WifiP2pLinkedInfo

```cangjie
public class WifiP2pLinkedInfo {
    public mut prop connectState: P2pConnectState
    public mut prop isGroupOwner: Bool
    public mut prop groupOwnerAddr: String
}
```

**功能：** 提供Wi-Fi连接的相关信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop connectState

```cangjie
public mut prop connectState: P2pConnectState
```

**功能：** P2P连接状态。

**类型：** [P2pConnectState](#enum-p2pconnectstate)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop isGroupOwner

```cangjie
public mut prop isGroupOwner: Bool
```

**功能：** true表示是群主，false表示不是群主。

**类型：** Bool

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop groupOwnerAddr

```cangjie
public mut prop groupOwnerAddr: String
```

**功能：** 群组IP地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

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

**功能：** 表示P2P群组相关信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop isP2pGo

```cangjie
public mut prop isP2pGo: Bool
```

**功能：** 是否是群主。true表示是群主，false表示不是群主。

**类型：** Bool

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop ownerInfo

```cangjie
public mut prop ownerInfo: WifiP2pDevice
```

**功能：** 群组的设备信息。

**类型：** [WifiP2pDevice](#class-wifip2pdevice)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop passphrase

```cangjie
public mut prop passphrase: String
```

**功能：** 群组密钥。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop interfaceName

```cangjie
public mut prop interfaceName: String
```

**功能：** P2P 群组使用的网卡接口名，例如 wlan0。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop groupName

```cangjie
public mut prop groupName: String
```

**功能：** 群组名称。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop networkId

```cangjie
public mut prop networkId: Int32
```

**功能：** 网络ID。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop frequency

```cangjie
public mut prop frequency: Int32
```

**功能：** 群组的频率。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop clientDevices

```cangjie
public mut prop clientDevices: Array<WifiP2pDevice>
```

**功能：** 接入的设备列表信息。

**类型：** Array\<[WifiP2pDevice](#class-wifip2pdevice)\>

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop goIpAddress

```cangjie
public mut prop goIpAddress: String
```

**功能：** 群组IP地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

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

**功能：** 表示P2P设备信息。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

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

**功能：** 构造WifiP2pDevice实例。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|deviceName|String|是|-|设备名称。|
|deviceAddress|String|是|-|设备MAC地址。|
|primaryDeviceType|String|是|-|主设备类型。|
|deviceStatus|[P2pDeviceStatus](#enum-p2pdevicestatus)|是|-|设备状态。|
|groupCapabilities|Int32|是|-|群组能力。|
|deviceAddressType|?[DeviceAddressType](#enum-deviceaddresstype)|否|None|**命名参数。** 设备MAC地址类型。|

### prop deviceName

```cangjie
public mut prop deviceName: String
```

**功能：** 设备名称。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop deviceAddress

```cangjie
public mut prop deviceAddress: String
```

**功能：** 设备MAC地址。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop deviceAddressType

```cangjie
public mut prop deviceAddressType: ?DeviceAddressType
```

**功能：** 设备MAC地址类型。

**类型：** ?[DeviceAddressType](#enum-deviceaddresstype)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop primaryDeviceType

```cangjie
public mut prop primaryDeviceType: String
```

**功能：** 主设备类型。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop deviceStatus

```cangjie
public mut prop deviceStatus: P2pDeviceStatus
```

**功能：** 设备状态。

**类型：** [P2pDeviceStatus](#enum-p2pdevicestatus)

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### prop groupCapabilities

```cangjie
public mut prop groupCapabilities: Int32
```

**功能：** 群组能力。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

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
    public var infoElems: Array<WifiInfoElement>
    public var timestamp: Int64
    public var supportedWifiCategory: WifiCategory
    public var isHiLinkNetwork: Bool
}
```

**功能：** WLAN热点信息。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var band

```cangjie
public var band: Int32
```

**功能：**  WLAN接入点的频段，1:2.4GHZ；2:5GHZ。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var bssid

```cangjie
public var bssid: String
```

**功能：** 热点的BSSID，例如：00:11:22:33:44:55。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var bssidType

```cangjie
public var bssidType: DeviceAddressType
```

**功能：** 热点的BSSID类型。

**类型：** [DeviceAddressType](#enum-deviceaddresstype)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var capabilities

```cangjie
public var capabilities: String
```

**功能：** 热点能力。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var centerFrequency0

```cangjie
public var centerFrequency0: Int32
```

**功能：** 热点的中心频率。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var centerFrequency1

```cangjie
public var centerFrequency1: Int32
```

**功能：** 热点的中心频率。如果热点使用两个不重叠的WLAN信道，则返回两个中心频率，分别用centerFrequency0和centerFrequency1表示。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var channelWidth

```cangjie
public var channelWidth: Int32
```

**功能：** WLAN接入点的带宽。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var frequency

```cangjie
public var frequency: Int32
```

**功能：** WLAN接入点的频率。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var infoElems

```cangjie
public var infoElems: Array<WifiInfoElement>
```

**功能：** 信息元素。

**类型：** Array\<[WifiInfoElement](#class-wifiinfoelement)>

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var isHiLinkNetwork

```cangjie
public var isHiLinkNetwork: Bool
```

**功能：** 热点是否支持hiLink，true:支持，&nbsp;false:不支持。

**类型：** Bool

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var rssi

```cangjie
public var rssi: Int32
```

**功能：** 热点的信号强度(dBm)。

**类型：** Int32

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var securityType

```cangjie
public var securityType: WifiSecurityType
```

**功能：** WLAN加密类型。

**类型：** [WifiSecurityType](#enum-wifisecuritytype)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var ssid

```cangjie
public var ssid: String
```

**功能：** 热点的SSID，最大长度为32字节，编码格式为UTF-8。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var supportedWifiCategory

```cangjie
public var supportedWifiCategory: WifiCategory
```

**功能：** 热点支持的最高wifi级别。

**类型：** [WifiCategory](#enum-wificategory)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**功能：** 时间戳。

**类型：** Int64

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

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

**功能：** WAPI(Wireless LAN Authentication and Privacy Infrastructure) 身份验证协议配置。

当用户通过WAPI身份验证协议连接无线网时，可通过以下方式配置参数或者证书进行连接。
- 方式一：通过配置证书进行连接。WifiDeviceConfig中关键字段的配置如下：
- preSharedKey无需传参；
- securityType设置为WifiSecTypeWapiCert；
- 在wapiConfig中：
- wapiAsCert传递AS证书的文本内容。
- wapiUserCert传递用户证书的文本内容。
- 方式二：通过配置preSharedKey进行连接。WifiDeviceConfig中关键字段的配置如下：
- preSharedKey传参为路由器上设置的密码；
- securityType设置为WifiSecTypeWapiPsk。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### init(WapiPskType, String, String)

```cangjie
public init(
    wapiPskType: WapiPskType,
    wapiAsCert: String,
    wapiUserCert: String
)
```

**功能：** 构造WifiWapiConfig实例。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|wapiPskType|[WapiPskType](#enum-wapipsktype)|是|-|加密类型。|
|wapiAsCert|String|是|-|AS证书(Authentication Server Certificate，身份验证服务器证书)。|
|wapiUserCert|String|是|-|用户证书。|

### prop wapiPskType

```cangjie
public mut prop wapiPskType: WapiPskType
```

**功能：** 加密类型。

**类型：** [WapiPskType](#enum-wapipsktype)

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop wapiAsCert

```cangjie
public mut prop wapiAsCert: String
```

**功能：** AS证书(Authentication Server Certificate，身份验证服务器证书)。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### prop wapiUserCert

```cangjie
public mut prop wapiUserCert: String
```

**功能：** 用户证书。

**类型：** String

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

## enum DeviceAddressType

```cangjie
public enum DeviceAddressType <: Equatable<DeviceAddressType> & ToString {
    | RandomDeviceAddress
    | RealDeviceAddress
    | ...
}
```

**功能：** wifi 设备地址（mac/bssid）类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**父类型：**

- Equatable\<[DeviceAddressType](#enum-deviceaddresstype)>
- ToString

### RandomDeviceAddress

```cangjie
RandomDeviceAddress
```

**功能：** 随机设备地址。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### RealDeviceAddress

```cangjie
RealDeviceAddress
```

**功能：** 真实设备地址。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### func !=(DeviceAddressType)

```cangjie
public operator func !=(other: DeviceAddressType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DeviceAddressType](#enum-deviceaddresstype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(DeviceAddressType)

```cangjie
public operator func ==(other: DeviceAddressType): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[DeviceAddressType](#enum-deviceaddresstype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 表示EAP身份验证方式的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapNone

```cangjie
EapNone
```

**功能：** 不指定。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapPeap

```cangjie
EapPeap
```

**功能：** PEAP类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapTls

```cangjie
EapTls
```

**功能：** TLS类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapTtls

```cangjie
EapTtls
```

**功能：** TTLS类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapPwd

```cangjie
EapPwd
```

**功能：** PWD类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapSim

```cangjie
EapSim
```

**功能：** SIM类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapAka

```cangjie
EapAka
```

**功能：** AKA类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapAkaPrime

```cangjie
EapAkaPrime
```

**功能：** AKA Prime类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### EapUnauthTls

```cangjie
EapUnauthTls
```

**功能：** UNAUTH TLS类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### func !=(EapMethod)

```cangjie
public operator func !=(other: EapMethod): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[EapMethod](#enum-eapmethod)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(EapMethod)

```cangjie
public operator func ==(other: EapMethod): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[EapMethod](#enum-eapmethod)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum GroupOwnerBand

```cangjie
public enum GroupOwnerBand <: Equatable<GroupOwnerBand> & ToString {
    | GoBandAuto
    | GoBand2GHz
    | GoBand5GHz
    | ...
}
```

**功能：** 表示群组带宽。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**父类型：**

- Equatable\<[GroupOwnerBand](#enum-groupownerband)>
- ToString

### GoBand2GHz

```cangjie
GoBand2GHz
```

**功能：** 2.4GHZ。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### GoBand5GHz

```cangjie
GoBand5GHz
```

**功能：** 5GHZ。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### GoBandAuto

```cangjie
GoBandAuto
```

**功能：** 自动模式。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

### func !=(GroupOwnerBand)

```cangjie
public operator func !=(other: GroupOwnerBand): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[GroupOwnerBand](#enum-groupownerband)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(GroupOwnerBand)

```cangjie
public operator func ==(other: GroupOwnerBand): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[GroupOwnerBand](#enum-groupownerband)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 表示设备状态的枚举。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Connected

```cangjie
Connected
```

**功能：** 连接状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Invited

```cangjie
Invited
```

**功能：** 邀请状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Failed

```cangjie
Failed
```

**功能：** 失败状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Available

```cangjie
Available
```

**功能：** 可用状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Unavailable

```cangjie
Unavailable
```

**功能：** 不可用状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### func !=(P2pDeviceStatus)

```cangjie
public operator func !=(other: P2pDeviceStatus): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[P2pDeviceStatus](#enum-p2pdevicestatus)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(P2pDeviceStatus)

```cangjie
public operator func ==(other: P2pDeviceStatus): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[P2pDeviceStatus](#enum-p2pdevicestatus)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum P2pConnectState

```cangjie
public enum P2pConnectState <: Equatable<P2pConnectState> & ToString {
    | Disconnected
    | Connected
}
```

**功能：** 表示P2P连接状态的枚举。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Disconnected

```cangjie
Disconnected
```

**功能：** 断开状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### Connected

```cangjie
Connected
```

**功能：** 连接状态。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

### func !=(P2pConnectState)

```cangjie
public operator func !=(other: P2pConnectState): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[P2pConnectState](#enum-p2pconnectstate)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(P2pConnectState)

```cangjie
public operator func ==(other: P2pConnectState): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[P2pConnectState](#enum-p2pconnectstate)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.P2P

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 表示WIFI频段类型的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### WifiBandNone

```cangjie
WifiBandNone
```

**功能：** 无效频段类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### WifiBand2g

```cangjie
WifiBand2g
```

**功能：** 2.4G频段类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### WifiBand5g

```cangjie
WifiBand5g
```

**功能：** 5G频段类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### WifiBand6g

```cangjie
WifiBand6g
```

**功能：** 6G频段类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### WifiBand60g

```cangjie
WifiBand60g
```

**功能：** 60G频段类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### func !=(WifiBandType)

```cangjie
public operator func !=(other: WifiBandType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiBandType](#enum-wifibandtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(WifiBandType)

```cangjie
public operator func ==(other: WifiBandType): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiBandType](#enum-wifibandtype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum WapiPskType

```cangjie
public enum WapiPskType <: Equatable<WapiPskType> & ToString {
    | WapiPskAscii
    | WapiPskHex
}
```

**功能：** WAPI身份验证方式的枚举。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

### WapiPskAscii

```cangjie
WapiPskAscii
```

**功能：** ASCII类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

### WapiPskHex

```cangjie
WapiPskHex
```

**功能：** HEX类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

### func !=(WapiPskType)

```cangjie
public operator func !=(other: WapiPskType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WapiPskType](#enum-wapipsktype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(WapiPskType)

```cangjie
public operator func ==(other: WapiPskType): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WapiPskType](#enum-wapipsktype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 表示第二阶段身份验证方式的枚举。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2None

```cangjie
Phase2None
```

**功能：** 不指定。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Pap

```cangjie
Phase2Pap
```

**功能：** PAP类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Mschap

```cangjie
Phase2Mschap
```

**功能：** MSCHAP类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Mschapv2

```cangjie
Phase2Mschapv2
```

**功能：** MSCHAPV2类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Gtc

```cangjie
Phase2Gtc
```

**功能：** GTC类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Sim

```cangjie
Phase2Sim
```

**功能：** SIM类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2Aka

```cangjie
Phase2Aka
```

**功能：** AKA类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### Phase2AkaPrime

```cangjie
Phase2AkaPrime
```

**功能：** AKA Prime类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

### func !=(Phase2Method)

```cangjie
public operator func !=(other: Phase2Method): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Phase2Method](#enum-phase2method)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(Phase2Method)

```cangjie
public operator func ==(other: Phase2Method): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Phase2Method](#enum-phase2method)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum WifiCallbackType

```cangjie
public enum WifiCallbackType <: Equatable<WifiCallbackType> & Hashable & ToString {
    | WifiScanStateChange
    | ...
}
```

**功能：** WLAN回调触发事件类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**父类型：**

- Equatable\<[WifiCallbackType](#enum-wificallbacktype)>
- Hashable
- ToString

### WifiScanStateChange

```cangjie
WifiScanStateChange
```

**功能：** 注册WLAN状态改变事件类型。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### func !=(WifiCallbackType)

```cangjie
public operator func !=(other: WifiCallbackType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiCallbackType](#enum-wificallbacktype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(WifiCallbackType)

```cangjie
public operator func ==(other: WifiCallbackType): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiCallbackType](#enum-wificallbacktype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**功能：** 获取输入数据的哈希值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Int64|数据的哈希值。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

## enum WifiCategory

```cangjie
public enum WifiCategory <: Equatable<WifiCategory> & ToString {
    | Default
    | Wifi6
    | Wifi6Plus
    | ...
}
```

**功能：** 表示热点支持的最高wifi类别。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**父类型：**

- Equatable\<[WifiCategory](#enum-wificategory)>
- ToString

### Default

```cangjie
Default
```

**功能：** Default。Wifi6以下的wifi类别。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### Wifi6

```cangjie
Wifi6
```

**功能：** Wifi6。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### Wifi6Plus

```cangjie
Wifi6Plus
```

**功能：** Wifi6+。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

### func !=(WifiCategory)

```cangjie
public operator func !=(other: WifiCategory): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiCategory](#enum-wificategory)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(WifiCategory)

```cangjie
public operator func ==(other: WifiCategory): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiCategory](#enum-wificategory)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.STA

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|

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

**功能：** 表示加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**父类型：**

- Equatable\<[WifiSecurityType](#enum-wifisecuritytype)>
- ToString

### WifiSecTypeEap

```cangjie
WifiSecTypeEap
```

**功能：** EAP加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeEapSuiteB

```cangjie
WifiSecTypeEapSuiteB
```

**功能：** Suite-B 192位加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeInvalid

```cangjie
WifiSecTypeInvalid
```

**功能：** 无效加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeOpen

```cangjie
WifiSecTypeOpen
```

**功能：** 开放加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeOwe

```cangjie
WifiSecTypeOwe
```

**功能：** 机会性无线加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypePsk

```cangjie
WifiSecTypePsk
```

**功能：** Pre-shared key (PSK)加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeSae

```cangjie
WifiSecTypeSae
```

**功能：** Simultaneous Authentication of Equals (SAE)加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeWapiCert

```cangjie
WifiSecTypeWapiCert
```

**功能：** WAPI-Cert加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeWapiPsk

```cangjie
WifiSecTypeWapiPsk
```

**功能：** WAPI-PSK加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### WifiSecTypeWep

```cangjie
WifiSecTypeWep
```

**功能：** Wired Equivalent Privacy (WEP)加密类型。候选网络配置不支持该加密类型。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

### func !=(WifiSecurityType)

```cangjie
public operator func !=(other: WifiSecurityType): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiSecurityType](#enum-wifisecuritytype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(WifiSecurityType)

```cangjie
public operator func ==(other: WifiSecurityType): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[WifiSecurityType](#enum-wifisecuritytype)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Communication.WiFi.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|枚举的说明。|
