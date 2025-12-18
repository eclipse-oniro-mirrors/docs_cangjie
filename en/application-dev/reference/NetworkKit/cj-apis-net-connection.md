# ohos.net.connection (Network Connection Management)

Network connection management provides fundamental capabilities for managing networks, including obtaining the default active data network, retrieving a list of all active data networks, enabling/disabling airplane mode, obtaining network capability information, and more.

For detailed error code descriptions in this section, please refer to [Network Connection Management Error Codes](./cj-errorcode-net-connection.md).

## Import Module

```cangjie
import kit.NetworkKit.*
```

## Permission List

ohos.permission.GET_NETWORK_INFO

ohos.permission.INTERNET

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned example projects and configuration templates, please refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie Example Code Instructions).

## func createNetConnection(?NetSpecifier, UInt32)

```cangjie
public func createNetConnection(netSpecifier!: ?NetSpecifier = None, timeout!: UInt32 = 0): NetConnection
```

**Function:** Creates a NetConnection object. netSpecifier specifies the characteristics of the network to monitor; timeout is the timeout duration (in milliseconds); netSpecifier is a prerequisite for timeout. If neither is specified, it monitors the default network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| netSpecifier | ?[NetSpecifier](#class-netspecifier) | No | None | **Named parameter.** Specifies the characteristics of the network. If None, monitors the default network. |
| timeout | UInt32 | No | 0 | **Named parameter.** Timeout duration for obtaining the network specified by netSpecifier. Only takes effect if netSpecifier is present. Default value is 0. |

**Return Value:**

| Type | Description |
|:----|:----|
| [NetConnection](#class-netconnection) | Handle to the monitored network. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Monitor default network, no parameters needed
    let netConnection = createNetConnection()

    // Monitor cellular network, requires passing relevant network characteristics. timeout parameter not passed means no timeout is used, so timeout is 0
    let netspecifier = NetSpecifier(NetCapabilities([NetBearType.BearerCellular]))
    let netConnectionCellular = createNetConnection(netSpecifier: netspecifier)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getAddressesByName(String)

```cangjie
public func getAddressesByName(host: String): Array<NetAddress>
```

**Function:** Resolves a hostname to obtain all IP addresses using the corresponding network.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| host | String | Yes | - | Hostname to resolve. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[NetAddress](#class-netaddress)> | Returns all IP addresses. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let addresses = getAddressesByName("localhost")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getAllNets()

```cangjie
public func getAllNets(): Array<NetHandle>
```

**Function:** Retrieves a list of all networks currently in a connected state.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[NetHandle](#class-nethandle)> | Returns a list of active data networks. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let netHandles = getAllNets()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getAppNet()

```cangjie
public func getAppNet(): NetHandle
```

**Function:** Binds an app to a specified network. After binding, the app can only access external networks through the specified network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [NetHandle](#class-nethandle) | Returns the data network bound to the app. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let netHandle = getAppNet()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getConnectionProperties(NetHandle)

```cangjie
public func getConnectionProperties(netHandle: NetHandle): ConnectionProperties
```

**Function:** Retrieves the connection information for the network corresponding to netHandle.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| netHandle | [NetHandle](#class-nethandle) | Yes | - | Handle to the data network. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ConnectionProperties](#class-connectionproperties) | Returns the connection information of the network. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.*

try {
    let netHandle = getDefaultNet()
    let connectionProperties = getConnectionProperties(netHandle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "getConnectionProperties failed: ${e.code} ${e.message}")
}
```

## func getDefaultHttpProxy()

```cangjie
public func getDefaultHttpProxy(): HttpProxy
```

**Function:** Retrieves the default proxy configuration information for the network. If a global proxy is set, it returns the global proxy configuration. If the process uses setAppNet to bind to a network specified by NetHandle, it returns the proxy configuration for that network. In other cases, it returns the proxy configuration for the default network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [HttpProxy](#class-httpproxy) | Returns the default proxy configuration for the network. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.*

try {
    let proxy = getDefaultHttpProxy()
    Hilog.info(0, "test", "proxy: ${proxy.host} ${proxy.port}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "getDefaultHttpProxy failed: ${e.code} ${e.message}")
}
```

## func getDefaultNet()

```cangjie
public func getDefaultNet(): NetHandle
```

**Function:** Retrieves the default active data network. Use getNetCapabilities to obtain the network type and capabilities.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [NetHandle](#class-nethandle) | Returns the default active data network. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let netHandle = getDefaultNet()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getNetCapabilities(NetHandle)

```cangjie
public func getNetCapabilities(netHandle: NetHandle): NetCapabilities
```

**Function:** Retrieves the capability information for the network corresponding to netHandle.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| netHandle | [NetHandle](#class-nethandle) | Yes | - | Handle to the data network. |

**Return Value:**

| Type | Description |
|:----|:----|
| [NetCapabilities](#class-netcapabilities) | Returns the capability information of the network. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.*

try {
    let netHandle = getDefaultNet()
    let netCapabilities = getNetCapabilities(netHandle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "getNetCapabilities failed: ${e.code} ${e.message}")
}
```## func hasDefaultNet()

```cangjie
public func hasDefaultNet(): Bool
```

**Function:** Checks whether the default data network is activated. Returns an interface, returning true if activated.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the default data network is activated.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let hasDefault = hasDefaultNet()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func isDefaultNetMetered()

```cangjie
public func isDefaultNetMetered(): Bool
```

**Function:** Checks whether data traffic usage on the current network is metered.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if data traffic usage on the current network is metered, otherwise returns false.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let isMetered = isDefaultNetMetered()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func reportNetConnected(NetHandle)

```cangjie
public func reportNetConnected(netHandle: NetHandle): Unit
```

**Function:** Reports to network management that the network is in an available state.

**Required Permission:** ohos.permission.GET_NETWORK_INFO & ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|netHandle|[NetHandle](#class-nethandle)|Yes|-|Handle of the data network. Refer to [NetHandle](#class-nethandle).|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let handle = getDefaultNet()
    reportNetConnected(handle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func reportNetDisconnected(NetHandle)

```cangjie
public func reportNetDisconnected(netHandle: NetHandle): Unit
```

**Function:** Reports to network management that the network is in an unavailable state.

**Required Permission:** ohos.permission.GET_NETWORK_INFO & ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|netHandle|[NetHandle](#class-nethandle)|Yes|-|Handle of the data network. Refer to [NetHandle](#class-nethandle).|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let handle = getDefaultNet()
    reportNetDisconnected(handle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func setAppNet(NetHandle)

```cangjie
public func setAppNet(netHandle: NetHandle): Unit
```

**Function:** Binds the app to the specified network. After binding, the app can only access the external network through the specified network.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|netHandle|[NetHandle](#class-nethandle)|Yes|-|Handle of the data network.|

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.*

try {
    let netHandle = getDefaultNet()
    setAppNet(netHandle)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "setAppNet failed: ${e.code} ${e.message}")
}
```

## class ConnectionProperties

```cangjie
public class ConnectionProperties {
    public var interfaceName: String
    public var domains: String
    public var linkAddresses: Array<LinkAddress>
    public var dnses: Array<NetAddress>
    public var routes: Array<RouteInfo>
    public var mtu: UInt32
}
```

**Function:** Network connection information class.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var dnses

```cangjie
public var dnses: Array<NetAddress>
```

**Function:** Network address. Refer to [NetAddress](#class-netaddress).

**Type:** Array\<[NetAddress](#class-netaddress)>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var domains

```cangjie
public var domains: String
```

**Function:** Belonging domain, default is "".

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var interfaceName

```cangjie
public var interfaceName: String
```

**Function:** Network interface name.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var linkAddresses

```cangjie
public var linkAddresses: Array<LinkAddress>
```

**Function:** Link information.

**Type:** Array\<[LinkAddress](#class-linkaddress)>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var mtu

```cangjie
public var mtu: UInt32
```

**Function:** Maximum Transmission Unit.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var routes

```cangjie
public var routes: Array<RouteInfo>
```

**Function:** Routing information.

**Type:** Array\<[RouteInfo](#class-routeinfo)>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## class HttpProxy

```cangjie
public class HttpProxy {
    public var host: String
    public var port: UInt32
    public var exclusionList: Array<String>
    public var username: String
    public var password: String
    public init(host: String,  port: UInt32, exclusionList: Array<String>,
        username!: String = "", password!: String = "")
}
```

**Function:** Network proxy configuration information.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var exclusionList

```cangjie
public var exclusionList: Array<String>
```

**Function:** List of hostnames that do not use the proxy. Hostnames support domain names, IP addresses, and wildcard formats. The detailed matching rules are as follows:

1. Domain name matching rules:

    (1) Exact match: The proxy server hostname matches if it is exactly the same as any hostname in the list.

    (2) Partial match: The proxy server hostname matches if it contains any hostname in the list.

    For example, if "ample.com" is set in the hostname list, then "ample.com", "www.ample.com", and "ample.com:80" will all match, while "www.example.com" and "ample.com.org" will not match.

2. IP address matching rules: The proxy server hostname matches if it is exactly the same as any IP address in the list.

3. Domain names and IP addresses can be added to the list simultaneously for matching.

4. The single "*" is the only valid wildcard. When only the wildcard is in the list, it will match all proxy server hostnames, indicating that the proxy is disabled. The wildcard can only be added alone and cannot be combined with other domain names or IP addresses in the list; otherwise, the wildcard will not take effect.

5. Matching rules are case-insensitive for hostnames.

6. When matching hostnames, protocol prefixes such as http and https are not considered.

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var host

```cangjie
public var host: String
```

**Function:** Proxy server hostname.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var password

```cangjie
public var password: String
```

**Function:** Proxy authentication password.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var port

```cangjie
public var port: UInt32
```

**Function:** Host port.

**Type:** UInt32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var username

```cangjie
public var username: String
```

**Function:** Proxy authentication username.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### init(String, UInt32, Array\<String>, String, String)

```cangjie
public init(host: String,  port: UInt32, exclusionList: Array<String>,
    username!: String = "", password!: String = "")
```

**Function:** Constructs an HttpProxy instance.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

|Parameter Name|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|host|String|Yes|-|Proxy server hostname.|
|port|UInt32|Yes|-|Host port.|
|exclusionList|Array\<String>|Yes|-|List of hostnames that do not use the proxy. Hostnames support domain names, IP addresses, and wildcard formats. The detailed matching rules are as follows:<br>1. Domain name matching rules:<br>(1) Exact match: The proxy server hostname matches if it is exactly the same as any hostname in the list.<br>(2) Partial match: The proxy server hostname matches if it contains any hostname in the list.<br>For example, if "ample.com" is set in the hostname list, then "ample.com", "www.ample.com", and "ample.com:80" will all match, while "www.example.com" and "ample.com.org" will not match.<br>2. IP address matching rules: The proxy server hostname matches if it is exactly the same as any IP address in the list.<br>3. Domain names and IP addresses can be added to the list simultaneously for matching.<br>4. The single "*" is the only valid wildcard. When only the wildcard is in the list, it will match all proxy server hostnames, indicating that the proxy is disabled. The wildcard can only be added alone and cannot be combined with other domain names or IP addresses in the list; otherwise, the wildcard will not take effect.<br>5. Matching rules are case-insensitive for hostnames.<br>6. When matching hostnames, protocol prefixes such as http and https are not considered.|
|username|String|No|""|Proxy authentication username.|
|password|String|No|""|Proxy authentication password.|## class LinkAddress

```cangjie
public class LinkAddress {
    public var address: NetAddress
    public var prefixLength: Int32
}
```

**Description:** Network link information.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var address

```cangjie
public var address: NetAddress
```

**Description:** Link address.

**Type:** [NetAddress](#class-netaddress)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var prefixLength

```cangjie
public var prefixLength: Int32
```

**Description:** Prefix length of the link address.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## class NetAddress

```cangjie
public class NetAddress {
    public var address: String
    public var family: UInt32
    public var port: UInt32
    public init(address: String, family!: UInt32 = 1, port!: UInt32 = 0)
}
```

**Description:** Network address.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var address

```cangjie
public var address: String
```

**Description:** Address.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var family

```cangjie
public var family: UInt32
```

**Description:** IPv4 = 1, IPv6 = 2, default is IPv4.

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var port

```cangjie
public var port: UInt32
```

**Description:** Port number, range [0, 65535].

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### init(String, UInt32, UInt32)

```cangjie
public init(address: String, family!: UInt32 = 1, port!: UInt32 = 0)
```

**Description:** Constructs a NetAddress instance.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| address | String | Yes | - | Address. |
| family | UInt32 | No | 1 | IPv4 = 1, IPv6 = 2, default is IPv4. |
| port | UInt32 | No | 0 | Port number, range [0, 65535]. |

## class NetBlockStatusInfo

```cangjie
public class NetBlockStatusInfo {
    public var netHandle: NetHandle
    public var blocked: Bool
}
```

**Description:** Network blocking status information.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var blocked

```cangjie
public var blocked: Bool
```

**Description:** Whether the network is blocked.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netHandle

```cangjie
public var netHandle: NetHandle
```

**Description:** Data network handle.

**Type:** [NetHandle](#class-nethandle)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## class NetCapabilities

```cangjie
public class NetCapabilities {
    public var bearerTypes: Array<NetBearType>
    public var linkUpBandwidthKbps: UInt32
    public var linkDownBandwidthKbps: UInt32
    public var networkCap: Array<NetCap>
    public init(bearerTypes: Array<NetBearType>, linkUpBandwidthKbps!: UInt32 = 0, linkDownBandwidthKbps!: UInt32 = 0,
        networkCap!: Array<NetCap> = Array<NetCap>())
}
```

**Description:** Network capability set.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var bearerTypes

```cangjie
public var bearerTypes: Array<NetBearType>
```

**Description:** Network type.

**Type:** Array\<[NetBearType](#enum-netbeartype)>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var linkDownBandwidthKbps

```cangjie
public var linkDownBandwidthKbps: UInt32
```

**Description:** Downlink (network to device) bandwidth, 0 indicates inability to evaluate current network bandwidth.

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var linkUpBandwidthKbps

```cangjie
public var linkUpBandwidthKbps: UInt32
```

**Description:** Uplink (device to network) bandwidth, 0 indicates inability to evaluate current network bandwidth.

**Type:** UInt32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var networkCap

```cangjie
public var networkCap: Array<NetCap>
```

**Description:** Specific network capabilities.

**Type:** Array\<[NetCap](#enum-netcap)>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### init(Array\<NetBearType>, UInt32, UInt32, Array\<NetCap>)

```cangjie
public init(bearerTypes: Array<NetBearType>, linkUpBandwidthKbps!: UInt32 = 0, linkDownBandwidthKbps!: UInt32 = 0,
    networkCap!: Array<NetCap> = Array<NetCap>())
```

**Description:** Network capability set.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| bearerTypes | Array\<[NetBearType](#enum-netbeartype)> | Yes | - | Network type. |
| linkUpBandwidthKbps | UInt32 | No | 0 | **Named parameter.** Uplink (device to network) bandwidth, 0 indicates inability to evaluate current network bandwidth. |
| linkDownBandwidthKbps | UInt32 | No | 0 | **Named parameter.** Downlink (network to device) bandwidth, 0 indicates inability to evaluate current network bandwidth. |
| networkCap | Array\<[NetCap](#enum-netcap)> | No | Array\<NetCap>() | Specific network capabilities. |

## class NetCapabilityInfo

```cangjie
public class NetCapabilityInfo {
    public var netHandle: NetHandle
    public var netCap: NetCapabilities
}
```

**Description:** Provides an instance of data network bearer capabilities.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netCap

```cangjie
public var netCap: NetCapabilities
```

**Description:** Stores the transmission capabilities and bearer types of the data network.

**Type:** [NetCapabilities](#class-netcapabilities)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netHandle

```cangjie
public var netHandle: NetHandle
```

**Description:** Data network handle.

**Type:** [NetHandle](#class-nethandle)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## class NetConnection

```cangjie
public class NetConnection {}
```

**Description:** Network connection handle; device transitioning from no network to having a network triggers netAvailable, netCapabilitiesChange, and netConnectionPropertiesChange events; device transitioning from having a network to no network triggers netLost event; device transitioning from WiFi to cellular triggers netLost event (WiFi lost) followed by netAvailable event (cellular available).

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### func on(NetConnectionEvent, Callback1Argument\<NetHandle>)

```cangjie
public func on(event: NetConnectionEvent, callback: Callback1Argument<NetHandle>): Unit
```

**Description:** Subscribes to network available and network lost events.

**Model Constraints:** This interface must be called after the register interface, use unregister to unsubscribe from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [NetConnectionEvent](#enum-netconnectionevent) | Yes | - | Network connection event type, only supports NetAvailable and NetLost events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[NetHandle](#class-nethandle)> | Yes | - | Callback function, returns data network handle. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Incorrect event type passed | Check the event parameter to ensure it is either NetAvailable or NetLost enum value |

### func on(NetConnectionEvent, Callback1Argument\<NetBlockStatusInfo>)

```cangjie
public func on(event: NetConnectionEvent, callback: Callback1Argument<NetBlockStatusInfo>): Unit
```

**Description:** Subscribes to network blocking status events.

**Model Constraints:** This interface must be called after the register interface, use unregister to unsubscribe from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [NetConnectionEvent](#enum-netconnectionevent) | Yes | - | Network connection event type, only supports NetBlockStatusChange event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[NetBlockStatusInfo](#class-netblockstatusinfo)> | Yes | - | Callback function, returns data network handle (netHandle) and network blocking status (blocked). |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Incorrect event type passed | Check the event parameter to ensure it is NetBlockStatusChange enum value |

### func on(NetConnectionEvent, Callback1Argument\<NetCapabilityInfo>)

```cangjie
public func on(event: NetConnectionEvent, callback: Callback1Argument<NetCapabilityInfo>): Unit
```

**Description:** Subscribes to network capability change events.

**Model Constraints:** This interface must be called after the register interface, use unregister to unsubscribe from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [NetConnectionEvent](#enum-netconnectionevent) | Yes | - | Network connection event type, only supports NetCapabilitiesChange event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[NetCapabilityInfo](#class-netcapabilityinfo)> | Yes | - | Callback function, returns data network handle (netHandle) and network capability information (netCap). |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Incorrect event type passed | Check the event parameter to ensure it is NetCapabilitiesChange enum value |

### func on(NetConnectionEvent, Callback1Argument\<NetConnectionPropertyInfo>)

```cangjie
public func on(event: NetConnectionEvent, callback: Callback1Argument<NetConnectionPropertyInfo>): Unit
```

**Description:** Subscribes to network connection information change events.

**Model Constraints:** This interface must be called after the register interface, use unregister to unsubscribe from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [NetConnectionEvent](#enum-netconnectionevent) | Yes | - | Network connection event type, only supports NetConnectionPropertiesChange event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[NetConnectionPropertyInfo](#class-netconnectionpropertyinfo)> | Yes | - | Callback function, returns data network handle (netHandle) and network connection information (connectionProperties). |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Incorrect event type passed | Check the event parameter to ensure it is NetConnectionPropertiesChange enum value |

### func on(NetConnectionEvent, Callback0Argument)

```cangjie
public func on(event: NetConnectionEvent, callback: Callback0Argument): Unit
```

**Description:** Subscribes to network unavailable events.

**Model Constraints:** This interface must be called after the register interface, use unregister to unsubscribe from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [NetConnectionEvent](#enum-netconnectionevent) | Yes | - | Network connection event type, only supports NetUnavailable event. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function, no return result. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Incorrect event type passed | Check the event parameter to ensure it is NetUnavailable enum value |

### func register()

```cangjie
public func register(): Unit
```

**Description:** Subscribes to specified network state change notifications.

**Required Permission:** ohos.permission.GET_NETWORK_INFO

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100002 | Failed to connect to the service. |
  | 2100003 | System internal error. |
  | 2101008 | The callback already exists. |
  | 2101022 | The number of requests exceeded the maximum allowed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let netCon: NetConnection = createNetConnection()
    netCon.register()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func unregister()

```cangjie
public func unregister(): Unit
```

**Description:** Unsubscribes from default network state change notifications.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, see [Network Connection Management Error Codes](./cj-errorcode-net-connection.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 2100002 | Failed to connect to the service. |
  | 2100003 | System internal error. |
  | 2101007 | The callback does not exist. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let netCon: NetConnection = createNetConnection()
    netCon.register()
    netCon.unregister()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class NetConnectionPropertyInfo

```cangjie
public class NetConnectionPropertyInfo {
    public var netHandle: NetHandle
    public var connectionProperties: ConnectionProperties
}
```

**Description:** Data for network connection change events.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var connectionProperties

```cangjie
public var connectionProperties: ConnectionProperties
```

**Description:** Network connection information.

**Type:** [ConnectionProperties](#class-connectionproperties)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netHandle

```cangjie
public var netHandle: NetHandle
```

**Description:** Data network handle.

**Type:** [NetHandle](#class-nethandle)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## class NetHandle

```cangjie
public class NetHandle {
    public var netId: Int32
}
```

**Description:** Handle for data networks. A NetHandle object must be obtained before calling its methods.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netId

```cangjie
public var netId: Int32
```

**Description:** Network ID. A value of 0 indicates no default network, while other values must be ≥100.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### func getAddressByName(String)

```cangjie
public func getAddressByName(host: String): NetAddress
```

**Description:** Resolves a hostname using the corresponding network to obtain the first IP address.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| host | String | Yes | - | Hostname to resolve. |

**Returns:**

| Type | Description |
|:----|:----|
| [NetAddress](#class-netaddress) | Returns the first IP address. |

**Exceptions:**

- BusinessException: Error codes are listed below. See [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let handle = getDefaultNet()

    let address = handle.getAddressByName("localhost")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAddressesByName(String)

```cangjie
public func getAddressesByName(host: String): Array<NetAddress>
```

**Description:** Resolves a hostname using the corresponding network to obtain all IP addresses.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| host | String | Yes | - | Hostname to resolve. |

**Returns:**

| Type | Description |
|:----|:----|
| Array\<[NetAddress](#class-netaddress)> | Returns all IP addresses. |

**Exceptions:**

- BusinessException: Error codes are listed below. See [Network Connection Management Error Codes](./cj-errorcode-net-connection.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 2100001 | Invalid parameter value. |
  | 2100002 | Operation failed. Cannot connect to service. |
  | 2100003 | System internal error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let handle = getDefaultNet()

    let addresses = handle.getAddressesByName("localhost")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class NetSpecifier

```cangjie
public class NetSpecifier {
    public var netCapabilities: NetCapabilities
    public var bearerPrivateIdentifier: String
    public init(netCapabilities: NetCapabilities, bearerPrivateIdentifier!: String = "")
}
```

**Description:** Provides an instance with data network bearer capabilities.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var bearerPrivateIdentifier

```cangjie
public var bearerPrivateIdentifier: String
```

**Description:** Network identifier. For Wi-Fi networks, the identifier is "wifi"; for cellular networks, it's "slot0" (corresponding to SIM card 1).

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var netCapabilities

```cangjie
public var netCapabilities: NetCapabilities
```

**Description:** Stores the transmission capabilities and bearer types of data networks.

**Type:** [NetCapabilities](#class-netcapabilities)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### init(NetCapabilities, String)

```cangjie
public init(netCapabilities: NetCapabilities, bearerPrivateIdentifier!: String = "")
```

**Description:** Provides an instance with data network bearer capabilities.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| netCapabilities | [NetCapabilities](#class-netcapabilities) | Yes | - | Stores the transmission capabilities and bearer types of data networks. |
| bearerPrivateIdentifier | String | No | "" | **Named parameter.** Network identifier. For Wi-Fi networks, the identifier is "wifi"; for cellular networks, it's "slot0" (corresponding to SIM card 1). |

## class RouteInfo

```cangjie
public class RouteInfo {
    public var interfaceName: String
    public var destination: LinkAddress
    public var gateway: NetAddress
    public var hasGateway: Bool
    public var isDefaultRoute: Bool
}
```

**Description:** Network routing information.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var destination

```cangjie
public var destination: LinkAddress
```

**Description:** Destination address.

**Type:** [LinkAddress](#class-linkaddress)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var gateway

```cangjie
public var gateway: NetAddress
```

**Description:** Gateway address.

**Type:** [NetAddress](#class-netaddress)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var hasGateway

```cangjie
public var hasGateway: Bool
```

**Description:** Whether a gateway exists.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var interfaceName

```cangjie
public var interfaceName: String
```

**Description:** Network interface name.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### var isDefaultRoute

```cangjie
public var isDefaultRoute: Bool
```

**Description:** Whether it is the default route.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## enum NetBearType

```cangjie
public enum NetBearType {
    | BearerCellular
    | BearerWifi
    | BearerEthernet
    | ...
}
```

**Description:** Network types.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### BearerCellular

```cangjie
BearerCellular
```

**Description:** Cellular network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### BearerEthernet

```cangjie
BearerEthernet
```

**Description:** Ethernet network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### BearerWifi

```cangjie
BearerWifi
```

**Description:** Wi-Fi network.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22## enum NetCap

```cangjie
public enum NetCap {
    | NetCapabilityMms
    | NetCapabilityNotMetered
    | NetCapabilityInternet
    | NetCapabilityNotVpn
    | NetCapabilityValidated
    | ...
}
```

**Function:** Network-specific capabilities.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilityInternet

```cangjie
NetCapabilityInternet
```

**Function:** Indicates that the network should have the capability to access the Internet, which is set by the network provider.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilityMms

```cangjie
NetCapabilityMms
```

**Function:** Indicates that the network can access the carrier's MMSC (Multimedia Message Service) to send and receive MMS.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilityNotMetered

```cangjie
NetCapabilityNotMetered
```

**Function:** Indicates that the network traffic is not metered.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilityNotVpn

```cangjie
NetCapabilityNotVpn
```

**Function:** Indicates that the network does not use a VPN (Virtual Private Network).

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilityValidated

```cangjie
NetCapabilityValidated
```

**Function:** Indicates that the network's capability to access the Internet has been successfully validated by the network management module, which is set by the network management module.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

## enum NetConnectionEvent

```cangjie
public enum NetConnectionEvent <: Equatable<NetConnectionEvent> {
    | NetAvailable
    | NetBlockStatusChange
    | NetCapabilitiesChange
    | NetConnectionPropertiesChange
    | NetLost
    | NetUnavailable
    | ...
}
```

**Function:** Network connection event types.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parent Type:**

- Equatable\<NetConnectionEvent>

### NetAvailable

```cangjie
NetAvailable
```

**Function:** Network available event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetBlockStatusChange

```cangjie
NetBlockStatusChange
```

**Function:** Network block status change event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetCapabilitiesChange

```cangjie
NetCapabilitiesChange
```

**Function:** Network capabilities change event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetConnectionPropertiesChange

```cangjie
NetConnectionPropertiesChange
```

**Function:** Network connection properties change event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetLost

```cangjie
NetLost
```

**Function:** Network lost event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### NetUnavailable

```cangjie
NetUnavailable
```

**Function:** Network unavailable event.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

### func !=(NetConnectionEvent)

```cangjie
public operator func !=(other: NetConnectionEvent): Bool
```

**Function:** Determines whether two events are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[NetConnectionEvent](#enum-netconnectionevent)|Yes|-|Another event enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two events are not equal, otherwise returns false.|

### func ==(NetConnectionEvent)

```cangjie
public operator func ==(other: NetConnectionEvent): Bool
```

**Function:** Determines whether two events are equal.

**System Capability:** SystemCapability.Communication.NetManager.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[NetConnectionEvent](#enum-netconnectionevent)|Yes|-|Another event enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two events are equal, otherwise returns false.|