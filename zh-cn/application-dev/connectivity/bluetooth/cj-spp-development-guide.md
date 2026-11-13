# 通过SPP连接和传输数据

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 简介

本指南主要提供基于串口通信协议（Serial Port Profile，SPP）实现设备间连接和传输数据的开发指导。两个设备进行 SPP 通信时，依据设备角色可区分为客户端与服务端，本指南分别说明两端的实现方法。

## 实现原理

客户端获取服务端的设备地址后，向服务端指定的 UUID 发起连接。服务端设备地址可通过查找设备流程获取，详见[查找设备](cj-ble-development-guide.md)。两端连接建立后，即可双向发送与接收数据。

服务端需要注册客户端待连接的 UUID 服务，并保持连接监听。连接建立后，服务端可接收客户端数据或向客户端发送数据。

客户端与服务端均可主动断开连接，应用需根据场景决定由哪一端执行断开操作。

## 开发步骤

### 申请蓝牙权限

需要申请权限 ohos.permission.ACCESS_BLUETOOTH。如何配置和申请权限，请参考[声明权限](../../security/AccessToken/cj-declare-permissions.md)和[向用户申请授权](../../security/AccessToken/cj-request-user-authorization.md)。

## 场景介绍

主要场景有：

- 客户端发起连接、收发数据、断开连接
- 服务端创建监听套接字、接受连接、收发数据、删除套接字

## 接口说明

完整的仓颉 API 说明以及示例代码请参见：[蓝牙 socket 接口](../../reference/ConnectivityKit/cj-apis-bluetooth-socket.md)。

| 接口名 | 功能描述 |
| --- | --- |
| sppListen(String, SppOptions, AsyncCallback\<Int32>) | 创建服务端监听套接字，并在蓝牙子系统中注册 UUID 服务。 |
| sppAccept(Int32, AsyncCallback\<Int32>) | 服务端接受客户端连接请求，返回客户端套接字 ID。 |
| sppConnect(String, SppOptions, AsyncCallback\<Int32>) | 客户端向服务端发起连接，返回客户端套接字 ID。 |
| sppWrite(Int32, ArrayBuffer) | 通过套接字写入数据。 |
| sppReadAsync(Int32, AsyncCallback\<ArrayBuffer>) | 从套接字异步读取数据。 |
| getDeviceId(Int32) | 获取客户端套接字对应的设备地址。 |
| sppCloseServerSocket(Int32) | 关闭服务端套接字，删除已注册的 UUID 服务。 |
| sppCloseClientSocket(Int32) | 关闭客户端套接字，断开连接。 |

## 主要场景开发步骤

### 客户端

#### 1. 发起连接

客户端通过查找设备流程获取目标设备地址后发起连接。连接使用的 UUID 必须与服务端创建套接字时的 UUID 一致；蓝牙子系统会校验服务端是否支持该 UUID，不支持则连接失败。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let peerDevice = "XX:XX:XX:XX:XX:XX"  // 请替换为查找到的设备地址
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

#### 2. 发送数据

连接建立后，使用客户端套接字 ID 发送数据。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppConnect 回调中获取的客户端套接字 ID
    let data: ArrayBuffer = [3, 4]
    sppWrite(clientSocket, data)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 3. 接收数据

连接建立后，调用 `sppReadAsync` 读取一次数据，读取成功时回调返回本次读取到的内容。需要持续读取时，应在回调处理完成后再次调用；同一 `clientSocket` 同时只允许一个未完成的读取。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppConnect 回调中获取的客户端套接字 ID
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

#### 4. 断开连接

不再需要连接时，关闭客户端套接字。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppConnect 回调中获取的客户端套接字 ID
    sppCloseClientSocket(clientSocket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### 服务端

#### 1. 创建服务端套接字

服务端通过创建监听套接字，在蓝牙子系统中注册指定 UUID 的服务。服务名称无限制，可使用应用名称。只有客户端与服务端的 UUID 一致时，连接才能建立。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
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

#### 2. 监听客户端连接

服务端套接字创建成功后，调用 `sppAccept` 等待客户端连接。连接建立后回调返回客户端套接字 ID。

> **说明：**
>
> 该接口在后台阻塞等待，最多等待 20 秒；超时未收到连接请求时回调返回错误，需重新调用 `sppAccept` 继续等待。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // 此处需替换为 sppListen 回调中获取的服务端套接字 ID
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

#### 3. 发送数据

连接建立后，使用客户端套接字 ID 向客户端发送数据。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppAccept 回调中获取的客户端套接字 ID
    let data: ArrayBuffer = [9, 8]
    sppWrite(clientSocket, data)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

#### 4. 接收数据

连接建立后，调用 `sppReadAsync` 读取一次客户端数据。需要持续读取时，应在回调处理完成后再次调用；同一 `clientSocket` 同时只允许一个未完成的读取。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppAccept 回调中获取的客户端套接字 ID
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

#### 5. 删除服务端套接字

不再需要服务端套接字时，调用 `sppCloseServerSocket` 关闭。蓝牙子系统会删除此前注册的 UUID 服务，此后客户端发起连接会失败。

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // 此处需替换为 sppListen 回调中获取的服务端套接字 ID
    sppCloseServerSocket(serverSocket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## 示例代码

客户端与服务端的完整示例可参考 [蓝牙 socket 接口](../../reference/ConnectivityKit/cj-apis-bluetooth-socket.md) 中各接口的示例代码。
