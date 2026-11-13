# ohos.bluetooth.socket（蓝牙socket模块）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

本模块提供蓝牙套接字（socket）能力，用于在两个蓝牙设备之间建立点对点连接并传输数据。通信双方按角色分为服务端与客户端：服务端创建监听套接字并向蓝牙子系统注册服务，客户端按设备地址发起连接。支持的套接字链路类型包括 RFCOMM（串口通信协议 SPP）与 L2CAP。

## 导入模块

```cangjie
import kit.ConnectivityKit.*
```

## 权限列表

ohos.permission.ACCESS_BLUETOOTH

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func sppListen(String, SppOptions, AsyncCallback\<Int32>)

```cangjie
public func sppListen(name: String, options: SppOptions, callback: AsyncCallback<Int32>): Unit
```

**功能：** 创建蓝牙服务端监听套接字。该操作会在蓝牙子系统中注册对应的服务，表示服务端支持的能力。应用不再需要该服务端套接字时，需通过 [sppCloseServerSocket](#func-sppcloseserversocketint32) 主动关闭。

**需要权限：** ohos.permission.ACCESS_BLUETOOTH

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|服务名称。|
|options|[SppOptions](#class-sppoptions)|是|-|监听参数。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32>|是|-|回调函数。创建成功时返回服务端套接字 ID，有效值为非负整数。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**示例：**

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

**功能：** 等待远端设备连接。服务端使用，须在 [sppListen](#func-spplistenstring-sppoptions-asynccallbackint32) 创建服务端套接字成功后调用。该接口在后台阻塞等待，最多等待 20 秒；超时未收到连接请求时回调返回错误，需重新调用。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|serverSocket|Int32|是|-|服务端套接字 ID，由 `sppListen` 返回。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32>|是|-|回调函数。连接建立时返回客户端套接字 ID。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let serverSocket: Int32 = 1  // 此处需替换为调用 sppListen 后回调中获取的服务端套接字 ID
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

**功能：** 通过套接字连接远端设备。客户端使用，向服务端发起连接请求。

**需要权限：** ohos.permission.ACCESS_BLUETOOTH

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|deviceId|String|是|-|设备地址，例如 `11:22:33:AA:BB:FF`。|
|options|[SppOptions](#class-sppoptions)|是|-|连接参数。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Int32>|是|-|回调函数。连接成功时返回客户端套接字 ID。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**示例：**

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

**功能：** 获取客户端套接字中的设备地址。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|clientSocket|Int32|是|-|客户端套接字 ID，由 `sppAccept` 或 `sppConnect` 返回。|

**返回值：**

|类型|说明|
|:----|:----|
|String|已连接设备的地址。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let clientSocket: Int32 = 1  // 此处需替换为 sppAccept 或 sppConnect 回调中获取的客户端套接字 ID
let deviceId = getDeviceId(clientSocket)
Hilog.info(0, "Bluetooth", "device id: " + deviceId)
```

## func sppCloseServerSocket(Int32)

```cangjie
public func sppCloseServerSocket(socket: Int32): Unit
```

**功能：** 关闭 SPP 服务端套接字并释放相关资源。关闭后，蓝牙子系统会删除此前注册的服务。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|socket|Int32|是|-|服务端套接字 ID，由 `sppListen` 返回。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let socket: Int32 = 1  // 此处需替换为 sppListen 回调中获取的服务端套接字 ID
    sppCloseServerSocket(socket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppCloseClientSocket(Int32)

```cangjie
public func sppCloseClientSocket(socket: Int32): Unit
```

**功能：** 关闭 SPP 客户端套接字并释放相关资源。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|socket|Int32|是|-|客户端套接字 ID，由 `sppAccept` 或 `sppConnect` 返回。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let socket: Int32 = 1  // 此处需替换为 sppAccept 或 sppConnect 回调中获取的客户端套接字 ID
    sppCloseClientSocket(socket)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## func sppWrite(Int32, ArrayBuffer)

```cangjie
public func sppWrite(clientSocket: Int32, data: ArrayBuffer): Unit
```

**功能：** 通过套接字写入数据。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|clientSocket|Int32|是|-|客户端套接字 ID，由 `sppAccept` 或 `sppConnect` 返回。|
|data|ArrayBuffer|是|-|待写入的数据。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2901054 | IO error. |
  | 2900099 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppAccept 或 sppConnect 回调中获取的客户端套接字 ID
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

**功能：** 从套接字异步读取一次数据。需要持续读取时，应在回调处理完成后再次调用；同一 `clientSocket` 同时只允许一个未完成的读取。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|clientSocket|Int32|是|-|客户端套接字 ID，由 `sppAccept` 或 `sppConnect` 返回。|
| callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<ArrayBuffer>|是|-|回调函数。读取成功时返回本次读取到的数据。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通用错误码](../cj-errorcode-universal.md)和[蓝牙服务子系统错误码](./cj-errorcode-bluetooth_manager.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 2901054 | IO error. |
  | 2900099 | Operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.BusinessException
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let clientSocket: Int32 = 1  // 此处需替换为 sppAccept 或 sppConnect 回调中获取的客户端套接字 ID
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

**功能：** 描述 SPP 套接字参数。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### init(String, Bool, SppType)

```cangjie
public init(uuid: String, secure: Bool, sppType: SppType)
```

**功能：** 创建 SPP 套接字选项。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|uuid|String|是|-|SDP 记录中的 UUID。|
|secure|Bool|是|-|是否使用安全通道。|
|sppType|[SppType](#enum-spptype)|是|-|SPP 链路类型。|

**示例：**

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

**功能：** SDP 记录中的 UUID。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### prop secure

```cangjie
public mut prop secure: Bool
```

**功能：** 是否使用安全通道。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### prop sppType

```cangjie
public mut prop sppType: SppType
```

**功能：** SPP 链路类型。

**类型：** [SppType](#enum-spptype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

## enum SppType

```cangjie
public enum SppType {
    SppRfcomm | SppL2cap | SppL2capBle | ...
}
```

**功能：** SPP 链路类型枚举。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### SppRfcomm

**功能：** RFCOMM 链路类型，对应串口通信协议（SPP），适用于传统蓝牙。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### SppL2cap

**功能：** L2CAP 链路类型，适用于传统蓝牙。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### SppL2capBle

**功能：** L2CAP 链路类型，适用于低功耗蓝牙。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将 SppType 转换为字符串表示。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|SppType 的字符串表示。|

**示例：**

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

**功能：** 比较两个 SppType 是否相等。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SppType](#enum-spptype)|是|-|待比较的 SppType。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|相等返回 true，否则返回 false。|

### func !=(SppType)

```cangjie
public operator func !=(other: SppType): Bool
```

**功能：** 比较两个 SppType 是否不相等。

**系统能力：** SystemCapability.Communication.Bluetooth.Core

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SppType](#enum-spptype)|是|-|待比较的 SppType。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|不相等返回 true，否则返回 false。|
