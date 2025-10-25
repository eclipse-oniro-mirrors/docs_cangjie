# Network Connection Management

## Introduction

Network Connection Management provides fundamental capabilities for managing networks, including priority management of multiple network connections (WiFi, cellular, Ethernet, etc.), network quality assessment, subscription to default or specified network connection status changes, querying network connection information, DNS resolution, and other functionalities.

## Basic Concepts

- **Network Producer**: The provider of data networks, such as WiFi, cellular, Ethernet, etc.
- **Network Consumer**: The user of data networks, such as applications or system services.
- **Network Probing**: Detects network validity to avoid switching from an available network to an unavailable one. Includes binding network probing, DNS probing, HTTP probing, and HTTPS probing.
- **Network Optimization**: Selects the optimal network when multiple networks coexist. Triggered when network status, network information, or scoring changes.

## Constraints

Development Language: Cangjie

## Scenarios

Typical scenarios for Network Connection Management are as follows:

- Receiving notifications for specified network status changes.
- Retrieving all registered networks.
- Querying network connection information based on the data network.
- Resolving domain names using the corresponding network to obtain all IP addresses.

Specific development methods are described below.

## Interface Description

For the complete Cangjie API documentation and sample code, refer to [Network Connection Management](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md).

| Interface Name                                                                                | Description                                                                                                                                                            |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `getDefaultNet(): NetHandle`                                                                  | Retrieves a NetHandle object containing the netId of the default network.                                                                                        |
| `getAppNet(): NetHandle`                                                                      | Retrieves a NetHandle object containing the netId of the network bound to the App.                                                                               |
| `setAppNet(netHandle: NetHandle): Unit`                                                       | Binds the App to the specified network. The bound App can only access external networks through the specified network.                                           |
| `getDefaultNetSync(): NetHandle;`                                                             | Retrieves the default active data network synchronously. Use `getNetCapabilities` to obtain network type and capabilities.                                       |
| `hasDefaultNet(): Bool`                                                                       | Checks whether the default data network is active.                                                                                                               |
| `getAllNets(): Array<NetHandle>`                                                              | Retrieves a list of NetHandle objects for all connected networks.                                                                                               |
| `getConnectionProperties(netHandle: NetHandle): ConnectionProperties`                         | Queries the connection information of the network corresponding to the netHandle.                                                                               |
| `getNetCapabilities(netHandle: NetHandle): NetCapabilities`                                  | Retrieves the capability information of the network corresponding to the netHandle.                                                                              |
| `isDefaultNetMetered(): Bool`                                                                 | Checks whether data traffic on the current network is metered. Uses a callback for asynchronous operation.                                                       |
| `reportNetConnected(netHandle: NetHandle): Unit`                                              | Reports to network management that the network is available. Indicates a discrepancy between the app's and network management's view of network availability.    |
| `reportNetDisconnected(netHandle: NetHandle): Unit`                                           | Reports to network management that the network is unavailable. Indicates a discrepancy between the app's and network management's view of network availability. |
| `getAddressesByName(host: String): Array<NetAddress>`                                         | Resolves a domain name using the corresponding network to obtain all IP addresses.                                                                               |
| `createNetConnection(netSpecifier!: ?NetSpecifier = None, timeout!: UInt32 = 0): NetConnection` | Returns a NetConnection object. `netSpecifier` specifies the characteristics of the network of interest. `timeout` is in milliseconds.                          |
| `getAddressByName(host: String): NetAddress`                                                  | Resolves a domain name using the corresponding network to obtain one IP address. Uses a callback.                                                               |
| `onNetAvailable(callback: (NetHandle) -> Unit): Unit`                                         | Subscribes to network availability events.                                                                                                                      |
| `onNetCapabilitiesChange(callback: (NetCapabilityInfo) -> Unit): Unit`                       | Subscribes to network capability change events.                                                                                                                 |
| `onNetConnectionPropertiesChange(callback: (NetHandle, ConnectionProperties) -> Unit): Unit`  | Subscribes to network connection property change events.                                                                                                         |
| `onNetBlockStatusChange(callback: (NetHandle, Bool) -> Unit): Unit`                          | Subscribes to network block status events. Uses a callback for asynchronous operation.                                                                          |
| `onNetLost(callback: (NetHandle) -> Unit): Unit`                                              | Subscribes to network loss events.                                                                                                                              |
| `onNetUnavailable(callback: () -> Unit): Unit`                                                | Subscribes to network unavailability events.                                                                                                                    |
| `register(): Unit`                                                                            | Subscribes to notifications for specified network status changes.                                                                                              |
| `unregister(): Unit`                                                                          | Unsubscribes from notifications for default network status changes.                                                                                            |

## Receiving Notifications for Specified Network Status Changes

1. Declare the required permission: `ohos.permission.GET_NETWORK_INFO`. This is a normal-level permission. Ensure compliance with [Basic Principles of Permission Usage](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-principles-of-permission-usage) before applying. Then, declare the permission by referring to [Access Control - Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

2. Import `connection` from `@kit.NetworkKit`.

3. Call the [`createNetConnection`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-createnetconnectionnetspecifier-uint32) method, specifying network capabilities, network type, and timeout (optional; if not provided, defaults to the default network). This creates a NetConnection object.

4. Call the [`register()`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-register) method to subscribe to notifications for specified network status changes.

5. When the network becomes available, the `netAvailable` event callback is triggered; when unavailable, the `netUnavailable` callback is triggered.

6. When the network is no longer needed, call the [`unregister()`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-unregister) method to unsubscribe.

<!-- compile -->

```cangjie
// Import packages.
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import ohos.base.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

class NetAvailableCb <: Callback1Argument<NetHandle> {
    let callback_: (NetHandle)->Unit
    public init(callback: (NetHandle)->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException, val: NetHandle): Unit {
        callback_(val)
    }
}

class NetUnavailableCb <: Callback0Argument {
    let callback_: ()->Unit
    public init(callback: ()->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException): Unit {
        callback_()
    }
}

func test() {
    let netSpecifier = NetSpecifier(NetCapabilities([NetBearType.BearerCellular], networkCap: [NetCap.NetCapabilityInternet]))

    // Set timeout to 10s (default is 0).
    let timeout = UInt32(10 * 1000)

    // Create a NetConnection object.
    let conn = createNetConnection(netSpecifier: netSpecifier, timeout: timeout)

    // Subscribe to notifications for specified network status changes.
    conn.register()

    // Subscribe to events. If the specified network is available, notify via on_netAvailable.
    let netAvailableCallBack = NetAvailableCb({ netHandle =>
        loggerInfo("net is available, netId is ${netHandle.netId}")
    })
    conn.on(NetConnectionEvent.NetAvailable, netAvailableCallBack)

    // Subscribe to events. If the specified network is unavailable, notify via on_netUnavailable.
    let netUnAvailableCallBack = NetUnavailableCb({=> loggerInfo("net is unavailable")})
    conn.on(NetConnectionEvent.NetUnavailable, netUnAvailableCallBack)

    // When the network is no longer needed, unsubscribe by calling unregister().
    conn.unregister()
}
```

## Monitoring Default Network Changes and Proactively Rebuilding Network Connections

The default network may change based on current network status and quality, such as:

1. Switching from WiFi to cellular when WiFi signal is weak.
2. Switching from cellular to WiFi when cellular performance is poor.
3. Switching to cellular after WiFi is turned off.
4. Switching to WiFi after cellular is turned off.
5. Switching to another WiFi when the current WiFi signal is weak (cross-network scenario).
6. Switching to another cellular network when the current cellular performance is poor (cross-network scenario).

This section describes how to monitor default network changes and quickly migrate application traffic to the new default network.

### Monitoring Default Network Changes

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import ohos.base.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

class NetAvailableCb <: Callback1Argument<NetHandle> {
    let callback_: (NetHandle)->Unit
    public init(callback: (NetHandle)->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException, val: NetHandle): Unit {
        callback_(val)
    }
}

func test() {
    let netConnection = createNetConnection()
    let netAvailableCallBack = NetAvailableCb({ netHandle =>
        loggerInfo("net is available, netId is ${netHandle.netId}")
    })
    netConnection.on(NetConnectionEvent.NetAvailable, netAvailableCallBack)
}
```

## Retrieving All Registered Networks

1. Declare the required permission: `ohos.permission.GET_NETWORK_INFO`. This is a normal-level permission. Ensure compliance with [Basic Principles of Permission Usage](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-principles-of-permission-usage) before applying. Then, declare the permission by referring to [Access Control - Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

2. Import `connection` from `kit.NetworkKit`.

3. Call the [`getAllNets`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getallnets) method to retrieve a list of all connected networks.

<!-- compile -->

```cangjie
// Import packages.
import kit.NetworkKit.*
import ohos.base.*

// Retrieve a list of all connected networks.
let nets = getAllNets()
```

## Querying Network Capabilities and Connection Information Based on Data Network

1. Declare the required permission: `ohos.permission.GET_NETWORK_INFO`. This is a normal-level permission. Ensure compliance with [Basic Principles of Permission Usage](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-principles-of-permission-usage) before applying. Then, declare the permission by referring to [Access Control - Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

2. Import `connection` from `kit.NetworkKit`.

3. Call [`getDefaultNet`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getdefaultnet) to retrieve the default data network (`NetHandle`), or call [`getAllNets`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getallnets) to retrieve a list of all connected networks (`Array<NetHandle>`).

4. Call [`getNetCapabilities`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getnetcapabilitiesnethandle) to retrieve the capability information of the network corresponding to the `NetHandle`. Capabilities include network type (cellular, WiFi, Ethernet) and specific network capabilities.

5. Call [`getConnectionProperties`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getconnectionpropertiesnethandle) to retrieve the connection information of the network corresponding to the `NetHandle`.

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import ohos.base.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

extend NetCap {
    public operator func ==(that: NetCap): Bool {
        match ((this, that)) {
            case (NetCapabilityMms, NetCapabilityMms) => true
            case (NetCapabilityNotMetered, NetCapabilityNotMetered) => true
            case (NetCapabilityInternet, NetCapabilityInternet) => true
            case (NetCapabilityNotVpn, NetCapabilityNotVpn) => true
            case (NetCapabilityValidated, NetCapabilityValidated) => true
            case _ => false
        }
    }
}

extend NetBearType {
    public operator func ==(that: NetBearType): Bool {
        match ((this, that)) {
            case (BearerCellular, BearerCellular) => true
            case (BearerWifi, BearerWifi) => true
            case (BearerEthernet, BearerEthernet) => true
            case _ => false
        }
    }
}

func test() {
    // Retrieve the default data network (NetHandle).
    let netHandle = getDefaultNet()
    if (netHandle.netId == 0) {
        // If no default network exists, the netId of the retrieved NetHandle is 0 (abnormal case requiring additional handling).
        return
    }

    let caps = getNetCapabilities(netHandle)
    // Retrieve network type (bearerTypes).
    for (item in caps.bearerTypes) {
        if (item == BearerCellular) {
            // Cellular network.
            loggerInfo("BearerCellular")
        } else if (item == BearerWifi) {
            // WiFi network.
            loggerInfo("BearerWifi")
        } else if (item == BearerEthernet) {
            // Ethernet network.
            loggerInfo("BearerEthernet")
        }
    }

    // Retrieve specific network capabilities (networkCap).
    for (item in caps.networkCap) {
        if (item == NetCapabilityMms) {
            // Indicates the network can access the carrier's MMSC (Multimedia Message Service) for sending/receiving MMS.
            loggerInfo("NetCapabilityMms")
        } else if (item == NetCapabilityNotMetered) {
            // Indicates network traffic is not metered.
            loggerInfo("NetCapabilityNotMetered")
        } else if (item == NetCapabilityInternet) {
            // Indicates the network should have Internet access capability, set by the network provider.
            loggerInfo("NetCapabilityInternet")
        } else if (item == NetCapabilityNotVpn) {
            // Indicates the network does not use a VPN (Virtual Private Network).
            loggerInfo("NetCapabilityNotVpn")
        } else if (item == NetCapabilityValidated) {
            // Indicates the network's Internet access capability has been successfully validated by network management.
            loggerInfo("NetCapabilityValidated")
        }
    }

    // Retrieve connection information for the network corresponding to netHandle. Includes link and routing information.
    let props = getConnectionProperties(netHandle)

    // Retrieve a list of all connected networks (Array<NetHandle>).
    let allNets = getAllNets()

    for (item in allNets) {
        let curCap = getNetCapabilities(item)
        let curProp = getConnectionProperties(item)
    }
}
```

## Resolving Domain Names Using the Corresponding Network to Obtain All IP Addresses

1. Declare the required permission: `ohos.permission.INTERNET`. This is a normal-level permission. Ensure compliance with [Basic Principles of Permission Usage](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-principles-of-permission-usage) before applying. Then, declare the permission by referring to [Access Control - Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

2. Import `connection` from `kit.NetworkKit`.

3. Call the [`getAddressesByName`](../../../en/application-dev/reference/NetworkKit/cj-apis-net-connection.md#func-getaddressesbynamestring) method to resolve a hostname using the default network and retrieve all IP addresses.

<!-- compile -->

```cangjie
// Import packages.
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import ohos.base.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

// Resolve a hostname using the default network to retrieve all IP addresses.
func test() {
    let addrs: Array<NetAddress> = getAddressesByName("xxxx")
    loggerInfo("Succeeded to get data")
}
```