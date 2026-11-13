# SPP Connection and Data Transmission

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Introduction

This guide describes how to establish connections and transmit data between devices based on the Serial Port Profile (SPP). When two devices communicate over SPP, they are classified by device role into a client and a server. This guide describes the implementation on both sides.

## Implementation Principles

After obtaining the device address of the server, the client initiates a connection to the UUID specified by the server. The server device address can be obtained through the device discovery process. For details, see [Advertising and Scanning](cj-ble-development-guide.md). After the connection is established, both parties can send and receive data in both directions.

The server must register the UUID service that the client will connect to and keep listening for connections. After the connection is established, the server can receive data from the client or send data to the client.

Either the client or the server can actively disconnect. The application must determine which side performs the disconnection based on the scenario.

## Development Steps

### Applying for the Bluetooth Permission

The ohos.permission.ACCESS_BLUETOOTH permission is required. For details about how to configure and apply for permissions, see [Declaring Permissions](../../security/AccessToken/cj-declare-permissions.md) and [Requesting User Authorization](../../security/AccessToken/cj-request-user-authorization.md).

## Scenarios

Main scenarios include:

- The client initiates a connection, sends and receives data, and disconnects.
- The server creates a listening socket, accepts connections, sends and receives data, and deletes the socket.

## Interface Description

For complete Cangjie API documentation and sample code, refer to: [Bluetooth Socket Interface](../../reference/ConnectivityKit/cj-apis-bluetooth-socket.md).

| Interface Name | Function Description |
| --- | --- |
| sppListen(String, SppOptions, AsyncCallback\<Int32>) | Creates a server listening socket and registers a UUID service with the Bluetooth subsystem. |
| sppAccept(Int32, AsyncCallback\<Int32>) | The server accepts a client connection request and returns the client socket ID. |
| sppConnect(String, SppOptions, AsyncCallback\<Int32>) | The client initiates a connection to the server and returns the client socket ID. |
| sppWrite(Int32, ArrayBuffer) | Writes data through a socket. |
| sppReadAsync(Int32, AsyncCallback\<ArrayBuffer>) | Asynchronously reads data from a socket. |
| getDeviceId(Int32) | Obtains the device address corresponding to a client socket. |
| sppCloseServerSocket(Int32) | Closes a server socket and deletes the registered UUID service. |
| sppCloseClientSocket(Int32) | Closes a client socket and disconnects the connection. |

## Development Steps for Main Scenarios

### Client

#### 1. Initiating a Connection

After obtaining the target device address through the device discovery process, the client initiates a connection. The UUID used for the connection must be the same as the UUID used when the server created the socket. The Bluetooth subsystem checks whether the server supports the UUID. If the UUID is not supported, the connection fails.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let peerDevice = "XX:XX:XX:XX:XX:XX"  // Replace it with the discovered device address.
    let options = SppOptions("00009999-0000-1000-8000-00805F9B34FB", false, SppType.SppRfcomm)
    sppConnect(peerDevice, options) {
        error: ?BusinessException, clientSocket: ?Int32 =>
        if (let Some(e) <- error) {
            Hilog.info(0, "Bluetooth", "connect failed: ${e.code}")
            return
        }
        Hilog.info(0, "Bluetooth", "client socket: " + clientSocket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 2. Sending Data

After the connection is established, use the client socket ID to send data.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppConnect callback.
    let data: ArrayBuffer = [3, 4]
    sppWrite(clientSocket, data)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 3. Receiving Data

After the connection is established, call `sppReadAsync` to read data once. On success, the callback returns the content read this time. To read data continuously, call this API again after the callback processing is complete. Only one outstanding read is allowed for the same `clientSocket` at a time.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppConnect callback.
    sppReadAsync(clientSocket) {
        error: ?BusinessException, data: ?ArrayBuffer =>
        if (let Some(e) <- error) {
            Hilog.info(0, "Bluetooth", "read failed: ${e.code}")
            return
        }
        Hilog.info(0, "Bluetooth", "read size: " + data.getOrThrow().size.toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 4. Disconnecting

When the connection is no longer needed, close the client socket.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppConnect callback.
    sppCloseClientSocket(clientSocket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### Server

#### 1. Creating a Server Socket

The server creates a listening socket to register a service with the specified UUID in the Bluetooth subsystem. The service name is not restricted and can be the application name. The connection can be established only when the UUIDs of the client and server are the same.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let options = SppOptions("00009999-0000-1000-8000-00805F9B34FB", false, SppType.SppRfcomm)
    sppListen("demonstration", options) {
        error: ?BusinessException, serverSocket: ?Int32 =>
        if (let Some(e) <- error) {
            Hilog.info(0, "Bluetooth", "listen failed: ${e.code}")
            return
        }
        Hilog.info(0, "Bluetooth", "server socket: " + serverSocket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 2. Listening for Client Connections

After the server socket is successfully created, call `sppAccept` to wait for a client connection. When the connection is established, the callback returns the client socket ID.

> **Note:**
>
> This API blocks in the background for a maximum of 20 seconds. If no connection request is received before the timeout, an error is returned through the callback, and `sppAccept` must be called again to continue waiting.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // Replace it with the server socket ID obtained from the sppListen callback.
    sppAccept(serverSocket) {
        error: ?BusinessException, clientSocket: ?Int32 =>
        if (let Some(e) <- error) {
            Hilog.info(0, "Bluetooth", "accept failed: ${e.code}")
            return
        }
        Hilog.info(0, "Bluetooth", "client socket: " + clientSocket.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 3. Sending Data

After the connection is established, use the client socket ID to send data to the client.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept callback.
    let data: ArrayBuffer = [9, 8]
    sppWrite(clientSocket, data)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 4. Receiving Data

After the connection is established, call `sppReadAsync` to read client data once. To read data continuously, call this API again after the callback processing is complete. Only one outstanding read is allowed for the same `clientSocket` at a time.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // Replace it with the client socket ID obtained from the sppAccept callback.
    sppReadAsync(clientSocket) {
        error: ?BusinessException, data: ?ArrayBuffer =>
        if (let Some(e) <- error) {
            Hilog.info(0, "Bluetooth", "read failed: ${e.code}")
            return
        }
        Hilog.info(0, "Bluetooth", "read size: " + data.getOrThrow().size.toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 5. Deleting the Server Socket

When the server socket is no longer needed, call `sppCloseServerSocket` to close it. The Bluetooth subsystem deletes the previously registered UUID service, and subsequent client connection attempts fail.

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // Replace it with the server socket ID obtained from the sppListen callback.
    sppCloseServerSocket(serverSocket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## Example

For complete examples of the client and server, refer to the sample code of each API in [Bluetooth Socket Interface](../../reference/ConnectivityKit/cj-apis-bluetooth-socket.md).
