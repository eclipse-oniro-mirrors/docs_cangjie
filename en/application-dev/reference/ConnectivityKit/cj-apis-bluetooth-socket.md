# ohos.bluetooth.socket (Bluetooth Socket Module)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The socket module provides Bluetooth socket capabilities for establishing point-to-point connections and transmitting data between two Bluetooth devices. The two communicating parties are classified by role into a server and a client. The server creates a listening socket and registers a service with the Bluetooth subsystem, and the client initiates a connection based on the device address. Supported socket link types include RFCOMM (Serial Port Profile, SPP) and L2CAP.

## Importing the Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above example projects and configuration templates, please refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie-Example-Code-Instructions).

## func sppListen(String, SppOptions, AsyncCallback\<Int32>)

```cangjie
public func sppListen(name: String, options: SppOptions, callback: AsyncCallback<Int32>): Unit
```

**Function:** Creates a Bluetooth server listening socket. This operation registers the corresponding service with the Bluetooth subsystem, indicating the capability supported by the server. When the application no longer needs the server socket, it must actively close it through [sppCloseServerSocket](#func-sppcloseserversocketint32).

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|name|String|Yes|-|Service name.|
|options|[SppOptions](#class-sppoptions)|Yes|-|Listening parameters.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|-|Callback function. Returns the server socket ID on success. The valid value is a non-negative integer.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let options = SppOptions("00001810-0000-1000-8000-00805F9B34FB", false, SppType.SppRfcomm)
    sppListen("server1", options) {
        error: ?BusinessException, socket: ?Int32 =>
        if (let Some(e) <- error) {
            throw e
        }
        Hilog.info(0, "Bluetooth", "server socket id: " + socket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppAccept(Int32, AsyncCallback\<Int32>)

```cangjie
public func sppAccept(serverSocket: Int32, callback: AsyncCallback<Int32>): Unit
```

**Function:** Waits for a remote device to connect. Used by the server and must be called after the server socket is successfully created by [sppListen](#func-spplistenstring-sppoptions-asynccallbackint32). This API blocks in the background for a maximum of 20 seconds. If no connection request is received before the timeout, an error is returned through the callback, and the API needs to be called again.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|serverSocket|Int32|Yes|-|Server socket ID, which is returned by `sppListen`.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|-|Callback function. Returns the client socket ID when the connection is established.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // Replace it with the server socket ID obtained from the sppListen callback.
    sppAccept(serverSocket) {
        error: ?BusinessException, socket: ?Int32 =>
        if (let Some(e) <- error) {
            throw e
        }
        Hilog.info(0, "Bluetooth", "client socket id: " + socket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppConnect(String, SppOptions, AsyncCallback\<Int32>)

```cangjie
public func sppConnect(deviceId: String, options: SppOptions, callback: AsyncCallback<Int32>): Unit
```

**Function:** Connects to a remote device through a socket. Used by the client to initiate a connection request to the server.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|deviceId|String|Yes|-|Device address, for example, `11:22:33:AA:BB:FF`.|
|options|[SppOptions](#class-sppoptions)|Yes|-|Connection parameters.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32>|Yes|-|Callback function. Returns the client socket ID on success.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let options = SppOptions("00001810-0000-1000-8000-00805F9B34FB", false, SppType.SppRfcomm)
    sppConnect("11:22:33:AA:BB:FF", options) {
        error: ?BusinessException, socket: ?Int32 =>
        if (let Some(e) <- error) {
            throw e
        }
        Hilog.info(0, "Bluetooth", "client socket id: " + socket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func getDeviceId(Int32)

```cangjie
public func getDeviceId(clientSocket: Int32): String
```

**Function:** Obtains the device address of a client socket.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|clientSocket|Int32|Yes|-|Client socket ID, which is returned by `sppAccept` or `sppConnect`.|

**Return Value:**

| Type | Description |
|:----|:----|
|String|Address of the connected device.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept or sppConnect callback.
let deviceId = getDeviceId(clientSocket)
Hilog.info(0, "Bluetooth", "device id: " + deviceId)
```

## func sppCloseServerSocket(Int32)

```cangjie
public func sppCloseServerSocket(socket: Int32): Unit
```

**Function:** Closes an SPP server socket and releases related resources. After the socket is closed, the Bluetooth subsystem deletes the previously registered service.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|socket|Int32|Yes|-|Server socket ID, which is returned by `sppListen`.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let socket: Int32 = 1  // Replace it with the server socket ID obtained from the sppListen callback.
    sppCloseServerSocket(socket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppCloseClientSocket(Int32)

```cangjie
public func sppCloseClientSocket(socket: Int32): Unit
```

**Function:** Closes an SPP client socket and releases related resources.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|socket|Int32|Yes|-|Client socket ID, which is returned by `sppAccept` or `sppConnect`.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let socket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept or sppConnect callback.
    sppCloseClientSocket(socket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppWrite(Int32, ArrayBuffer)

```cangjie
public func sppWrite(clientSocket: Int32, data: ArrayBuffer): Unit
```

**Function:** Writes data through a socket.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|clientSocket|Int32|Yes|-|Client socket ID, which is returned by `sppAccept` or `sppConnect`.|
|data|ArrayBuffer|Yes|-|Data to be written.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2901054 | IO error. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept or sppConnect callback.
    let data: ArrayBuffer = [31, 32]
    sppWrite(clientSocket, data)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppReadAsync(Int32, AsyncCallback\<ArrayBuffer>)

```cangjie
public func sppReadAsync(clientSocket: Int32, callback: AsyncCallback<ArrayBuffer>): Unit
```

**Function:** Asynchronously reads data from a socket once. To read data continuously, call this API again after the callback processing is complete. Only one outstanding read is allowed for the same `clientSocket` at a time.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|clientSocket|Int32|Yes|-|Client socket ID, which is returned by `sppAccept` or `sppConnect`.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<ArrayBuffer>|Yes|-|Callback function. Returns the data read this time on success.|

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2901054 | IO error. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept or sppConnect callback.
    sppReadAsync(clientSocket) {
        error: ?BusinessException, data: ?ArrayBuffer =>
        if (let Some(e) <- error) {
            throw e
        }
        Hilog.info(0, "Bluetooth", "read size: " + data.getOrThrow().size.toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## class SppOptions

```cangjie
public class SppOptions {
    public init(uuid: String, secure: Bool, sppType: SppType)
    public mut prop uuid: String
    public mut prop secure: Bool
    public mut prop sppType: SppType
}
```

**Function:** Describes SPP socket parameters.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### init(String, Bool, SppType)

```cangjie
public init(uuid: String, secure: Bool, sppType: SppType)
```

**Function:** Creates SPP socket options.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|uuid|String|Yes|-|UUID in the SDP record.|
|secure|Bool|Yes|-|Whether to use a secure channel.|
|sppType|[SppType](#enum-spptype)|Yes|-|SPP link type.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*

let options = SppOptions("00001810-0000-1000-8000-00805F9B34FB", false, SppType.SppRfcomm)
```

### prop uuid

```cangjie
public mut prop uuid: String
```

**Function:** UUID in the SDP record.

**Type:** String

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### prop secure

```cangjie
public mut prop secure: Bool
```

**Function:** Whether to use a secure channel.

**Type:** Bool

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### prop sppType

```cangjie
public mut prop sppType: SppType
```

**Function:** SPP link type.

**Type:** [SppType](#enum-spptype)

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

## enum SppType

```cangjie
public enum SppType {
    SppRfcomm | SppL2cap | SppL2capBle | ...
}
```

**Function:** Enumerates SPP link types.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### SppRfcomm

**Function:** RFCOMM link type, corresponding to the Serial Port Profile (SPP), applicable to classic Bluetooth.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### SppL2cap

**Function:** L2CAP link type, applicable to classic Bluetooth.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### SppL2capBle

**Function:** L2CAP link type, applicable to Bluetooth Low Energy.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts SppType to its string representation.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
|String|String representation of SppType.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let text = SppType.SppRfcomm.toString()
Hilog.info(0, "Bluetooth", "spp type: " + text)
```

### func ==(SppType)

```cangjie
public operator func ==(other: SppType): Bool
```

**Function:** Checks whether two SppType values are equal.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|other|[SppType](#enum-spptype)|Yes|-|SppType to be compared.|

**Return Value:**

| Type | Description |
|:----|:----|
|Bool|Returns true if they are equal; returns false otherwise.|

### func !=(SppType)

```cangjie
public operator func !=(other: SppType): Bool
```

**Function:** Checks whether two SppType values are not equal.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 26.1.0

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
|other|[SppType](#enum-spptype)|Yes|-|SppType to be compared.|

**Return Value:**

| Type | Description |
|:----|:----|
|Bool|Returns true if they are not equal; returns false otherwise.|
