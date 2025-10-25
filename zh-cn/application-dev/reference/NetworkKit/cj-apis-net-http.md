# ohos.net.http（数据请求）

本模块提供HTTP数据请求能力。应用可以通过HTTP发起一个数据请求，支持常见的GET、POST、OPTIONS、HEAD、PUT、DELETE、TRACE、CONNECT方法。

## 导入模块

```cangjie
import kit.NetworkKit.*
```

## 权限列表

ohos.permission.INTERNET

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func createHttp()

```cangjie
public func createHttp(): HttpRequest
```

**功能：** 创建一个HTTP请求，请求对象功能包括发起请求、中断请求、订阅/取消订阅HTTP Response Header事件。每一个HttpRequest对象对应一个HTTP请求。如需发起多个HTTP请求，须为每个HTTP请求创建对应HttpRequest对象。

> **说明：**
>
> 当该请求使用完毕时，须调用destroy方法主动销毁HttpRequest对象。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|[HttpRequest](#class-httprequest)|返回一个HttpRequest对象，里面包括request、requestInStream、destroy、on和off方法。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*

let httpRequest = createHttp()
```

## func createHttpResponseCache(UInt32)

```cangjie
public func createHttpResponseCache(cacheSize!: UInt32 = MAX_CACHE_SIZE): HttpResponseCache
```

**功能：** 创建一个默认的对象来存储HTTP访问请求的响应。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|cacheSize|UInt32|否|MAX_CACHE_SIZE|**命名参数。** 缓存大小最大为10\*1024\*1024（10MB），默认最大。|

**返回值：**

|类型|说明|
|:----|:----|
|[HttpResponseCache](#class-httpresponsecache)|返回一个存储HTTP访问请求响应的对象。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*

let httpResponseCache = createHttpResponseCache()
```

## class ClientCert

```cangjie
public class ClientCert {
    public var certPath: String
    public var keyPath: String
    public var certType: CertType
    public var keyPassword: String
    public init(certPath: String, keyPath: String, certType!: CertType = CertType.Pem, keyPassword!: String = "")
}
```

**功能：** 客户端证书类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var certPath

```cangjie
public var certPath: String
```

**功能：** 证书路径。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var certType

```cangjie
public var certType: CertType
```

**功能：** 证书类型，默认是PEM。

**类型：** [CertType](#enum-certtype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var keyPassword

```cangjie
public var keyPassword: String
```

**功能：** 证书秘钥的密码。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var keyPath

```cangjie
public var keyPath: String
```

**功能：** 证书秘钥的路径。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### init(String, String, CertType, String)

```cangjie
public init(certPath: String, keyPath: String, certType!: CertType = CertType.Pem, keyPassword!: String = "")
```

**功能：** 构造ClientCert实例。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|certPath|String|是|-|证书路径。|
|keyPath|String|是|-|证书秘钥的路径。|
|certType|[CertType](#enum-certtype)|否|CertType.Pem|**命名参数。** 证书类型，默认是PEM。|
|keyPassword|String|否|""|**命名参数。** 证书秘钥的密码。|

## class DataReceiveProgressInfo

```cangjie
public class DataReceiveProgressInfo {
    public var receiveSize: Int64
    public var totalSize: Int64
}
```

**功能：** 数据接收信息。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var receiveSize

```cangjie
public var receiveSize: Int64
```

**功能：** 已接收的数据量单位为字节。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var totalSize

```cangjie
public var totalSize: Int64
```

**功能：** 总共要接收的数据量单位为字节。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## class DataSendProgressInfo

```cangjie
public class DataSendProgressInfo {
    public var sendSize: Int64
    public var totalSize: Int64
}
```

**功能：** 数据发送信息。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var sendSize

```cangjie
public var sendSize: Int64
```

**功能：** 每次发送的数据量单位为字节。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var totalSize

```cangjie
public var totalSize: Int64
```

**功能：** 总共要发送的数据量单位为字节。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## class HttpRequest

```cangjie
public class HttpRequest {}
```

**功能：** HTTP请求任务。在调用HttpRequest的方法前，需要先通过[createHttp](../NetworkKit/cj-apis-net-http.md#func-createhttp)创建一个任务。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### func destroy()

```cangjie
public func destroy(): Unit
```

**功能：** 中断请求任务。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*

let httpRequest = createHttp()

httpRequest.destroy()
```

### func off(HttpRequestEvent, ?CallbackObject)

```cangjie
public func off(event: HttpRequestEvent, callback!: ?CallbackObject = None): Unit
```

**功能：** 取消订阅HTTP请求事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|要取消订阅的HTTP请求事件类型。|
|callback|?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject)|否|None|回调函数。可以指定传入on中的callback取消对应的订阅，也可以不指定callback清空所有订阅。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持HeadersReceive事件类型。 |

### func on(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**功能：** 订阅HTTP Response Header 事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持HeadersReceive事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>>|是|-|回调函数，返回HTTP响应头对象。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持HeadersReceive事件类型。 |

### func on(HttpRequestEvent, Callback1Argument\<Array\<Byte>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<Array<Byte>>): Unit
```

**功能：** 订阅HTTP流式响应数据接收事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持DataReceive事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<Byte>>|是|-|回调函数，用于接收HTTP流式响应数据。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持DataReceive事件类型。 |

### func on(HttpRequestEvent, Callback0Argument)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback0Argument): Unit
```

**功能：** 订阅HTTP流式响应数据接收完毕事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持DataEnd事件。|
|callback|[Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument)|是|-|回调函数。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持DataEnd事件类型。 |

### func on(HttpRequestEvent, Callback1Argument\<DataReceiveProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataReceiveProgressInfo>): Unit
```

**功能：** 订阅HTTP流式响应数据接收进度事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持DataReceiveProgress事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataReceiveProgressInfo](#class-datareceiveprogressinfo)>|是|-|回调函数，用于接收数据接收进度信息，参数为DataReceiveProgressInfo对象。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持DataReceiveProgress事件类型。 |

### func on(HttpRequestEvent, Callback1Argument\<DataSendProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataSendProgressInfo>): Unit
```

**功能：** 订阅HTTP网络请求数据发送进度事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持DataSendProgress事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataSendProgressInfo](#class-datasendprogressinfo)>|是|-|回调函数，用于接收数据发送进度信息，参数为DataSendProgressInfo对象。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持DataSendProgress事件类型。 |

### func once(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func once(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**功能：** 订阅HTTP Response Header 事件，只能触发一次。触发之后，订阅器就会被移除。使用callback方式作为异步方法。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|[HttpRequestEvent](#enum-httprequestevent)|是|-|HTTP请求事件类型，仅支持HeadersReceive事件。|
|callback|[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>>|是|-|回调函数。返回HTTP响应头对象。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The parameter check failed. | 传入的event类型不支持 | 检查event参数，确保传入的是支持的事件类型。当前方法仅支持HeadersReceive事件类型。 |

### func request(String, HttpRequestOptions, AsyncCallback\<HttpResponse>)

```cangjie
public func request(url: String, options: HttpRequestOptions, callback: AsyncCallback<HttpResponse>): Unit
```

**功能：** 根据URL地址，发起HTTP网络请求，在callback回调函数中返回响应。

> **说明：**
>
> 此接口仅支持数据大小为5MB以内的数据接收。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|url|String|是|-|发起网络请求的URL地址。|
|options|[HttpRequestOptions](#class-httprequestoptions)|是|-|参考[HttpRequestOptions](#class-httprequestoptions)。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)>|是|-|回调函数。|

**异常：**

- BusinessException：对应错误码如下表，[HTTP错误码](./cj-errorcode-net-http.md)和[通用错误码](../cj-errorcode-universal.md)。
- HTTP接口返回错误码映射关系：2300000 + curl错误码。更多常用错误码，可参考：[curl错误码](https://curl.se/libcurl/c/libcurl-errors.html)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 201 | Permission denied. |
  | 2300001 | Unsupported protocol. |
  | 2300003 | URL using bad/illegal format or missing URL. |
  | 2300005 | Couldn't resolve proxy name. |
  | 2300006 | Couldn't resolve host name. |
  | 2300007 | Couldn't connect to server. |
  | 2300008 | Weird server reply. |
  | 2300009 | Access denied to remote resource. |
  | 2300016 | Error in the HTTP2 framing layer. |
  | 2300018 | Transferred a partial file. |
  | 2300023 | Failed writing received data to disk/application. |
  | 2300025 | Upload failed. |
  | 2300026 | Failed to open/read local data from file/application. |
  | 2300027 | Out of memory. |
  | 2300028 | Timeout was reached. |
  | 2300047 | Number of redirects hit maximum amount. |
  | 2300052 | Server returned nothing (no headers, no data). |
  | 2300055 | Failed sending data to the peer. |
  | 2300056 | Failure when receiving data from the peer. |
  | 2300058 | Problem with the local SSL certificate. |
  | 2300059 | Couldn't use specified SSL cipher. |
  | 2300060 | SSL peer certificate or SSH remote key was not OK. |
  | 2300061 | Unrecognized or bad HTTP Content or Transfer-Encoding. |
  | 2300063 | Maximum file size exceeded. |
  | 2300070 | Disk full or allocation exceeded. |
  | 2300073 | Remote file already exists. |
  | 2300077 | Problem with the SSL CA cert (path? access rights?). |
  | 2300078 | Remote file not found. |
  | 2300094 | An authentication function returned an error. |
  | 2300999 | Unknown Other Error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpRequest = createHttp()
httpRequest.request("http://www.example.com", {err, resp =>
    if (let Some(e) <- err) {
        Hilog.error(0, "AppLogCj","exception: ${e.message}")
    }
    if (let Some(r) <- resp) {
        Hilog.info(0, "http_test", "resp: ${r.responseCode}")
    } else {
        Hilog.error(0, "AppLogCj", "response is none")
    }
})
```

### func request(String, AsyncCallback\<HttpResponse>)

```cangjie
public func request(url: String, callback: AsyncCallback<HttpResponse>): Unit
```

**功能：** 根据URL地址，发起HTTP网络请求，在callback回调函数中返回响应。

> **说明：**
>
> 此接口仅支持数据大小为5MB以内的数据接收。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|url|String|是|-|发起网络请求的URL地址。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)>|是|-|回调函数。|

**异常：**

- BusinessException：对应错误码如下表，[HTTP错误码](./cj-errorcode-net-http.md)和[通用错误码](../cj-errorcode-universal.md)。
- HTTP接口返回错误码映射关系：2300000 + curl错误码。更多常用错误码，可参考：[curl错误码](https://curl.se/libcurl/c/libcurl-errors.html)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 201 | Permission denied. |
  | 2300001 | Unsupported protocol. |
  | 2300003 | URL using bad/illegal format or missing URL. |
  | 2300005 | Couldn't resolve proxy name. |
  | 2300006 | Couldn't resolve host name. |
  | 2300007 | Couldn't connect to server. |
  | 2300008 | Weird server reply. |
  | 2300009 | Access denied to remote resource. |
  | 2300016 | Error in the HTTP2 framing layer. |
  | 2300018 | Transferred a partial file. |
  | 2300023 | Failed writing received data to disk/application. |
  | 2300025 | Upload failed. |
  | 2300026 | Failed to open/read local data from file/application. |
  | 2300027 | Out of memory. |
  | 2300028 | Timeout was reached. |
  | 2300047 | Number of redirects hit maximum amount. |
  | 2300052 | Server returned nothing (no headers, no data). |
  | 2300055 | Failed sending data to the peer. |
  | 2300056 | Failure when receiving data from the peer. |
  | 2300058 | Problem with the local SSL certificate. |
  | 2300059 | Couldn't use specified SSL cipher. |
  | 2300060 | SSL peer certificate or SSH remote key was not OK. |
  | 2300061 | Unrecognized or bad HTTP Content or Transfer-Encoding. |
  | 2300063 | Maximum file size exceeded. |
  | 2300070 | Disk full or allocation exceeded. |
  | 2300073 | Remote file already exists. |
  | 2300077 | Problem with the SSL CA cert (path? access rights?). |
  | 2300078 | Remote file not found. |
  | 2300094 | An authentication function returned an error. |
  | 2300999 | Unknown Other Error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpRequest = createHttp()
httpRequest.request("http://www.example.com", {err, resp =>
    if (let Some(e) <- err) {
        Hilog.error(0, "AppLogCj","exception: ${e.message}")
    }
    if (let Some(r) <- resp) {
        Hilog.info(0, "http_test", "resp: ${r.responseCode}")
    } else {
        Hilog.error(0, "AppLogCj", "response is none")
    }
})
```

### func requestInStream(String, HttpRequestOptions, AsyncCallback\<UInt32>)

```cangjie
public func requestInStream(url: String, options: HttpRequestOptions, callback: AsyncCallback<UInt32>): Unit
```

**功能：** 根据URL地址和相关配置项，发起HTTP网络请求并返回流式响应，在callback回调函数中返回响应。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|url|String|是|-|发起网络请求的URL地址。|
|options|[HttpRequestOptions](#class-httprequestoptions)|是|-|参考[HttpRequestOptions](#class-httprequestoptions)。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<UInt32>|是|-|回调函数。|

**异常：**

- BusinessException：对应错误码如下表，[HTTP错误码](./cj-errorcode-net-http.md)和[通用错误码](../cj-errorcode-universal.md)。
- HTTP接口返回错误码映射关系：2300000 + curl错误码。更多常用错误码，可参考：[curl错误码](https://curl.se/libcurl/c/libcurl-errors.html)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 201 | Permission denied. |
  | 2300001 | Unsupported protocol. |
  | 2300003 | URL using bad/illegal format or missing URL. |
  | 2300005 | Couldn't resolve proxy name. |
  | 2300006 | Couldn't resolve host name. |
  | 2300007 | Couldn't connect to server. |
  | 2300008 | Weird server reply. |
  | 2300009 | Access denied to remote resource. |
  | 2300016 | Error in the HTTP2 framing layer. |
  | 2300018 | Transferred a partial file. |
  | 2300023 | Failed writing received data to disk/application. |
  | 2300025 | Upload failed. |
  | 2300026 | Failed to open/read local data from file/application. |
  | 2300027 | Out of memory. |
  | 2300028 | Timeout was reached. |
  | 2300047 | Number of redirects hit maximum amount. |
  | 2300052 | Server returned nothing (no headers, no data). |
  | 2300055 | Failed sending data to the peer. |
  | 2300056 | Failure when receiving data from the peer. |
  | 2300058 | Problem with the local SSL certificate. |
  | 2300059 | Couldn't use specified SSL cipher. |
  | 2300060 | SSL peer certificate or SSH remote key was not OK. |
  | 2300061 | Unrecognized or bad HTTP Content or Transfer-Encoding. |
  | 2300063 | Maximum file size exceeded. |
  | 2300070 | Disk full or allocation exceeded. |
  | 2300073 | Remote file already exists. |
  | 2300077 | Problem with the SSL CA cert (path? access rights?). |
  | 2300078 | Remote file not found. |
  | 2300094 | An authentication function returned an error. |
  | 2300999 | Unknown Other Error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpRequest = createHttp()
httpRequest.requestInStream("http://www.example.com", {err, code =>
    if (let Some(e) <- err) {
        Hilog.error(0, "AppLogCj","exception: ${e.message}")
    }
    if (let Some(respCode) <- code) {
        Hilog.info(0, "AppLogCj", "resp: ${respCode}")
    } else {
        Hilog.error(0, "AppLogCj", "response is none")
    }
})
```

### func requestInStream(String, AsyncCallback\<UInt32>)

```cangjie
public func requestInStream(url: String, callback: AsyncCallback<UInt32>): Unit
```

**功能：** 根据URL地址和相关配置项，发起HTTP网络请求并返回流式响应，在callback回调函数中返回响应。

**需要权限：** ohos.permission.INTERNET

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|url|String|是|-|发起网络请求的URL地址。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<UInt32>|是|-|回调函数。|

**异常：**

- BusinessException：对应错误码如下表，[HTTP错误码](./cj-errorcode-net-http.md)和[通用错误码](../cj-errorcode-universal.md)。
- HTTP接口返回错误码映射关系：2300000 + curl错误码。更多常用错误码，可参考：[curl错误码](https://curl.se/libcurl/c/libcurl-errors.html)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. |
  | 201 | Permission denied. |
  | 2300001 | Unsupported protocol. |
  | 2300003 | URL using bad/illegal format or missing URL. |
  | 2300005 | Couldn't resolve proxy name. |
  | 2300006 | Couldn't resolve host name. |
  | 2300007 | Couldn't connect to server. |
  | 2300008 | Weird server reply. |
  | 2300009 | Access denied to remote resource. |
  | 2300016 | Error in the HTTP2 framing layer. |
  | 2300018 | Transferred a partial file. |
  | 2300023 | Failed writing received data to disk/application. |
  | 2300025 | Upload failed. |
  | 2300026 | Failed to open/read local data from file/application. |
  | 2300027 | Out of memory. |
  | 2300028 | Timeout was reached. |
  | 2300047 | Number of redirects hit maximum amount. |
  | 2300052 | Server returned nothing (no headers, no data). |
  | 2300055 | Failed sending data to the peer. |
  | 2300056 | Failure when receiving data from the peer. |
  | 2300058 | Problem with the local SSL certificate. |
  | 2300059 | Couldn't use specified SSL cipher. |
  | 2300060 | SSL peer certificate or SSH remote key was not OK. |
  | 2300061 | Unrecognized or bad HTTP Content or Transfer-Encoding. |
  | 2300063 | Maximum file size exceeded. |
  | 2300070 | Disk full or allocation exceeded. |
  | 2300073 | Remote file already exists. |
  | 2300077 | Problem with the SSL CA cert (path? access rights?). |
  | 2300078 | Remote file not found. |
  | 2300094 | An authentication function returned an error. |
  | 2300999 | Unknown Other Error. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpRequest = createHttp()
httpRequest.requestInStream("http://www.example.com", {err, code =>
    if (let Some(e) <- err) {
        Hilog.error(0, "AppLogCj","exception: ${e.message}")
    }
    if (let Some(respCode) <- code) {
        Hilog.info(0, "AppLogCj", "resp: ${respCode}")
    } else {
        Hilog.error(0, "AppLogCj", "response is none")
    }
})
```

## class HttpRequestOptions

```cangjie
public class HttpRequestOptions {
    public var method: RequestMethod
    public var extraData: HttpData
    public var expectDataType:?HttpDataType
    public var usingCache: Bool
    public var priority: UInt32
    public var header: HashMap<String, String>
    public var readTimeout: UInt32
    public var connectTimeout: UInt32
    public var usingProtocol:?HttpProtocol
    public var usingProxy: UsingProxy
    public var caPath: String
    public var resumeFrom: Int64
    public var resumeTo: Int64
    public var clientCert: ClientCert
    public var dnsOverHttps: String
    public var dnsServers: Array<String>
    public var maxLimit: UInt32
    public var multiFormDataList: Array<MultiFormData>
    public init(method!: RequestMethod = RequestMethod.Get, extraData!: HttpData = HttpData.StringData(""),
        expectDataType!: ?HttpDataType, usingCache!: Bool = true, priority!: UInt32 = 1,
        header!: HashMap<String, String> = HashMap<String, String>(), readTimeout!: UInt32 = 60000,
        connectTimeout!: UInt32 = 60000, usingProtocol!: ?HttpProtocol,
        usingProxy!: UsingProxy = UsingProxy.UseDefault, caPath!: String = "", resumeFrom!: Int64 = 0,
        resumeTo!: Int64 = 0, clientCert!: ClientCert = ClientCert("",""), dnsOverHttps!: String = "",
        dnsServers!: Array<String> = Array<String>(), maxLimit!: UInt32 = 5 * 1024 * 1024,
        multiFormDataList!: Array<MultiFormData> = Array<MultiFormData>())
}
```

**功能：** 发起请求可选参数的类型和取值范围。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var caPath

```cangjie
public var caPath: String
```

**功能：** 如果设置了此参数，系统将使用用户指定路径的CA证书，(开发者需保证该路径下CA证书的可访问性)，否则将使用系统预设CA证书，系统预设CA证书位置：/etc/ssl/certs/cacert.pem。证书路径为沙箱映射路径（开发者可通过Global.getContext().filesDir获取应用沙箱路径）。目前仅支持后缀名为.pem的文本格式证书。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var clientCert

```cangjie
public var clientCert: ClientCert
```

**功能：** 支持传输客户端证书。

**类型：** [ClientCert](#class-clientcert)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var connectTimeout

```cangjie
public var connectTimeout: UInt32
```

**功能：** 连接超时时间。单位为毫秒（ms），默认为60000ms。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var dnsOverHttps

```cangjie
public var dnsOverHttps: String
```

**功能：** 设置使用HTTPS协议的服务器进行DNS解析。<br />参数必须以以下格式进行URL编码："https:// host:port/path"。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var dnsServers

```cangjie
public var dnsServers: Array<String>
```

**功能：** 设置指定的DNS服务器进行DNS解析。<br />可以设置多个DNS解析服务器，最多3个服务器。如果有3个以上，只取前3个。<br />服务器必须是IPv4或者IPv6地址。

**类型：** Array\<String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var expectDataType

```cangjie
public var expectDataType:?HttpDataType
```

**功能：** 指定返回数据的类型，默认无此字段。如果设置了此参数，系统将优先返回指定的类型。

**类型：** ?[HttpDataType](#enum-httpdatatype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var extraData

```cangjie
public var extraData: HttpData
```

**功能：** 发送请求的额外数据，默认无此字段。

- 当HTTP请求为POST、PUT等方法时，此字段为HTTP请求的content，以UTF-8编码形式作为请求体。
  - 当'content-Type'为'application/x-www-form-urlencoded'时，请求提交的信息主体数据应在key和value进行URL转码后按照键值对"key1=value1&key2=value2&key3=value3"的方式进行编码，该字段对应的类型通常为String。
  - 当'content-Type'为'text/xml'时，该字段对应的类型通常为String。
  - 当'content-Type'为'application/json'时，该字段对应的类型通常为Object。
  - 当'content-Type'为'application/octet-stream'时，该字段对应的类型通常为ArrayBuffer。
  - 当'content-Type'为'multipart/form-data'且需上传的字段为文件时，该字段对应的类型通常为ArrayBuffer。
- 当HTTP请求为GET、OPTIONS、DELETE、TRACE、CONNECT等方法时，此字段为HTTP请求参数的补充。开发者需传入Encode编码后的string类型参数，Object类型的参数无需预编码，参数内容会拼接到URL中进行发送；ArrayBuffer类型的参数不会做拼接处理。

以上信息仅供参考，并可能根据具体情况有所不同。

**类型：** [HttpData](#enum-httpdata)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var header

```cangjie
public var header: HashMap<String, String>
```

**功能：** HTTP请求头字段。默认{'content-Type': 'application/json'}。

**类型：** HashMap\<String,String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var maxLimit

```cangjie
public var maxLimit: UInt32
```

**功能：** 响应消息的最大字节限制，默认值为5MB，以字节为单位。最大值为10MB，以字节为单位。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var method

```cangjie
public var method: RequestMethod
```

**功能：** 请求方式，默认为GET。

**类型：** [RequestMethod](#enum-requestmethod)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var multiFormDataList

```cangjie
public var multiFormDataList: Array<MultiFormData>
```

**功能：** 当'content-Type'为'multipart/form-data'时，则上传该字段定义的数据字段表单列表。

**类型：** Array\<[MultiFormData](#class-multiformdata)>

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var priority

```cangjie
public var priority: UInt32
```

**功能：** 优先级，范围[1,1000]，默认是1。若传参超出范围则使用默认值1。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var readTimeout

```cangjie
public var readTimeout: UInt32
```

**功能：** 读取超时时间。单位为毫秒（ms），默认为60000ms。<br />设置为0表示不会出现超时情况。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var resumeFrom

```cangjie
public var resumeFrom: Int64
```

**功能：** 用于设置上传或下载起始位置。HTTP标准（RFC 7233第3.1节）允许服务器忽略范围请求。<br />使用HTTP PUT时设置此参数，可能出现未知问题。<br />取值范围是:1~4294967296(4GB)，超出范围则不生效。无默认值。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var resumeTo

```cangjie
public var resumeTo: Int64
```

**功能：** 用于设置上传或下载结束位置。HTTP标准（RFC 7233第3.1节）允许服务器忽略范围请求。<br />使用HTTP PUT时设置此参数，可能出现未知问题。<br />取值范围是:1~4294967296(4GB)，超出范围则不生效。无默认值。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var usingCache

```cangjie
public var usingCache: Bool
```

**功能：** 是否使用缓存，默认为true，请求时优先读取缓存。 缓存跟随当前进程生效。新缓存会替换旧缓存。

**类型：** Bool

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var usingProtocol

```cangjie
public var usingProtocol:?HttpProtocol
```

**功能：** 使用协议。默认值由系统自动指定。

**类型：** ?[HttpProtocol](#enum-httpprotocol)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var usingProxy

```cangjie
public var usingProxy: UsingProxy
```

**功能：** 是否使用HTTP代理，默认为USE_DEFAULT，使用默认代理。<br /> 当usingProxy为NOT_USE时，不使用网络代理。<br /> 当usingProxy为USE_SPECIFIED类型时，使用指定网络代理。

**类型：** [UsingProxy](#enum-usingproxy)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### init(RequestMethod, HttpData, ?HttpDataType, Bool, UInt32, HashMap\<String,String>, UInt32, UInt32, ?HttpProtocol, UsingProxy, String, Int64, Int64, ClientCert, String, Array\<String>, UInt32, Array\<MultiFormData>)

```cangjie
public init(method!: RequestMethod = RequestMethod.Get, extraData!: HttpData = HttpData.StringData(""),
    expectDataType!: ?HttpDataTypee, usingCache!: Bool = true, priority!: UInt32 = 1,
    header!: HashMap<String, String> = HashMap<String, String>(), readTimeout!: UInt32 = 60000,
    connectTimeout!: UInt32 = 60000, usingProtocol!: ?HttpProtocol,
    usingProxy!: UsingProxy = UsingProxy.UseDefault, caPath!: String = "", resumeFrom!: Int64 = 0,
    resumeTo!: Int64 = 0, clientCert!: ClientCert = ClientCert("",""), dnsOverHttps!: String = "",
    dnsServers!: Array<String> = Array<String>(), maxLimit!: UInt32 = 5 * 1024 * 1024,
    multiFormDataList!: Array<MultiFormData> = Array<MultiFormData>())
```

**功能：** 构造HttpRequestOptions实例。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|method|[RequestMethod](#enum-requestmethod)|否|RequestMethod.Get|**命名参数。** 请求方式，默认为GET。|
|extraData|[HttpData](#enum-httpdata)|否|HttpData.StringData("")|**命名参数。** 发送请求的额外数据，默认无此字段。|
|expectDataType|?[HttpDataType](#enum-httpdatatype)|否|None|**命名参数。** 指定返回数据的类型，默认无此字段。|
|usingCache|Bool|否|true|**命名参数。** 是否使用缓存，默认为true。|
|priority|UInt32|否|1|**命名参数。** 优先级，范围[1,1000]，默认是1。|
|header|HashMap\<String,String>|否|HashMap<String,String>()|**命名参数。** HTTP请求头字段。|
|readTimeout|UInt32|否|60000|**命名参数。** 读取超时时间，单位为毫秒。|
|connectTimeout|UInt32|否|60000|**命名参数。** 连接超时时间，单位为毫秒。|
|usingProtocol|?[HttpProtocol](#enum-httpprotocol)|否|None|**命名参数。** 使用协议，默认值由系统自动指定。|
|usingProxy|[UsingProxy](#enum-usingproxy)|否|UsingProxy.UseDefault|**命名参数。** 是否使用HTTP代理，默认为USE_DEFAULT。|
|caPath|String|否|""|**命名参数。** CA证书路径，如果设置了此参数，系统将使用用户指定路径的CA证书。|
|resumeFrom|Int64|否|0|**命名参数。** 用于设置上传或下载起始位置。|
|resumeTo|Int64|否|0|**命名参数。** 用于设置上传或下载结束位置。|
|clientCert|[ClientCert](#class-clientcert)|否|ClientCert("", "")|**命名参数。** 支持传输客户端证书。|
|dnsOverHttps|String|否|""|**命名参数。** 设置使用HTTPS协议的服务器进行DNS解析。|
|dnsServers|Array\<String>|否|Array<String>()|**命名参数。** 设置指定的DNS服务器进行DNS解析。|
|maxLimit|UInt32|否|5 * 1024 * 1024|**命名参数。** 响应消息的最大字节限制，默认值为5MB。|
|multiFormDataList|Array\<[MultiFormData](#class-multiformdata)>|否|Array<MultiFormData>()|**命名参数。** 当'content-Type'为'multipart/form-data'时，则上传该字段定义的数据字段表单列表。|

## class HttpResponse

```cangjie
public class HttpResponse {
    public var result: HttpData
    public var resultType: HttpDataType
    public var responseCode: UInt32
    public var header: HashMap<String, String>
    public var cookies: String
    public var performanceTiming: PerformanceTiming
}
```

**功能：** request方法回调函数的返回值类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var cookies

```cangjie
public var cookies: String
```

**功能：** 服务器返回的cookies。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var header

```cangjie
public var header: HashMap<String, String>
```

**功能：** 发起HTTP请求返回来的响应头。

**类型：** HashMap\<String,String>

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var performanceTiming

```cangjie
public var performanceTiming: PerformanceTiming
```

**功能：** HTTP请求的各个阶段的耗时。

**类型：** [PerformanceTiming](#class-performancetiming)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var responseCode

```cangjie
public var responseCode: UInt32
```

**功能：** 响应的状态码。

**类型：** UInt32

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var result

```cangjie
public var result: HttpData
```

**功能：** HTTP请求根据响应头中content-type类型返回对应的响应格式内容。

**类型：** [HttpData](#enum-httpdata)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var resultType

```cangjie
public var resultType: HttpDataType
```

**功能：** 返回值类型。

**类型：** [HttpDataType](#enum-httpdatatype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## class HttpResponseCache

```cangjie
public class HttpResponseCache {}
```

**功能：** 存储HTTP访问请求响应的对象。在调用HttpResponseCache的方法前，需要先通过[createHttpResponseCache](#func-createhttpresponsecacheuint32)创建一个任务。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### func delete()

```cangjie
public func delete(): Unit
```

**功能：** 禁用缓存并删除其中的数据。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.business_exception.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpResponseCache = createHttpResponseCache()
try {
    httpResponseCache.delete()
} catch (e: BusinessException) {
    Hilog.info(0, "", "${e}")
}
```

### func flush()

```cangjie
public func flush(): Unit
```

**功能：** 将缓存中的数据写入文件系统，以便在下一个HTTP请求中访问所有缓存数据。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.business_exception.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog

let httpResponseCache = createHttpResponseCache()
try {
    httpResponseCache.flush()
} catch (e: BusinessException) {
    Hilog.info(0, "", "${e}")
}
```

## class MultiFormData

```cangjie
public class MultiFormData {
    public var name: String
    public var contentType: String
    public var remoteFileName: String
    public var data: HttpData
    public var filePath: String
    public init(name: String, contentType: String,  remoteFileName!: String = "",
        data!: HttpData = HttpData.StringData(""), filePath!: String = "")
}
```

**功能：** 多部分表单数据的类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var contentType

```cangjie
public var contentType: String
```

**功能：** 数据类型，如'text/plain'，'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4'等。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var data

```cangjie
public var data: HttpData
```

**功能：** 表单数据内容。

**类型：** [HttpData](#enum-httpdata)

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var filePath

```cangjie
public var filePath: String
```

**功能：** 此参数根据文件的内容设置mime部件的正文内容。用于代替data将文件数据设置为数据内容，如果data为空，则必须设置filePath。如果data有值，则filePath不会生效。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var name

```cangjie
public var name: String
```

**功能：** 数据名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var remoteFileName

```cangjie
public var remoteFileName: String
```

**功能：** 上传到服务器保存为文件的名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### init(String, String, String, HttpData, String)

```cangjie
public init(name: String, contentType: String,  remoteFileName!: String = "",
    data!: HttpData = HttpData.StringData(""), filePath!: String = "")
```

**功能：** 构造MultiFormData实例。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|数据名称。|
|contentType|String|是|-|数据类型，如'text/plain'，'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4'等。|
|remoteFileName|String|否|""|**命名参数。** 上传到服务器保存为文件的名称。|
|data|[HttpData](#enum-httpdata)|否|HttpData.StringData("")|**命名参数。** 表单数据内容。|
|filePath|String|否|""|**命名参数。** 此参数根据文件的内容设置mime部件的正文内容。用于代替data将文件数据设置为数据内容，如果data为空，则必须设置filePath。如果data有值，则filePath不会生效。|

## class PerformanceTiming

```cangjie
public class PerformanceTiming {
    public var dnsTiming: Float64
    public var tcpTiming: Float64
    public var tlsTiming: Float64
    public var firstSendTiming: Float64
    public var firstReceiveTiming: Float64
    public var totalFinishTiming: Float64
    public var redirectTiming: Float64
    public var responseHeaderTiming: Float64
    public var responseBodyTiming: Float64
    public var totalTiming: Float64
}
```

**功能：** 性能打点数据，单位为毫秒。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var dnsTiming

```cangjie
public var dnsTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到DNS解析完成耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var firstReceiveTiming

```cangjie
public var firstReceiveTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到接收第一个字节的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var firstSendTiming

```cangjie
public var firstSendTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到开始发送第一个字节的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var redirectTiming

```cangjie
public var redirectTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到完成所有重定向步骤的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var responseBodyTiming

```cangjie
public var responseBodyTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到body解析完成的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var responseHeaderTiming

```cangjie
public var responseHeaderTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到header解析完成的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var tcpTiming

```cangjie
public var tcpTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到TCP连接完成耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var tlsTiming

```cangjie
public var tlsTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到TLS连接完成耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var totalFinishTiming

```cangjie
public var totalFinishTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求到完成请求的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### var totalTiming

```cangjie
public var totalTiming: Float64
```

**功能：** 从[request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse)请求回调到应用程序的耗时。

**类型：** Float64

**读写能力：** 可读写

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum CertType

```cangjie
public enum CertType {
    | Pem
    | Der
    | P12
    | ...
}
```

**功能：** 证书类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Der

```cangjie
Der
```

**功能：** 证书类型DER。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### P12

```cangjie
P12
```

**功能：** 证书类型P12。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Pem

```cangjie
Pem
```

**功能：** 证书类型PEM。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum HttpData

```cangjie
public enum HttpData {
    | StringData(String)
    | ArrayData(Array<Byte>)
    | ...
}
```

**功能：** HTTP的数据。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### ArrayData(Array\<Byte>)

```cangjie
ArrayData(Array<Byte>)
```

**功能：** 二进制数组。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### StringData(String)

```cangjie
StringData(String)
```

**功能：** 字符串。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum HttpDataType

```cangjie
public enum HttpDataType {
    | StringValue
    | ArrayBuffer
    | ...
}
```

**功能：** HTTP的数据类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### ArrayBuffer

```cangjie
ArrayBuffer
```

**功能：** 二进制数组类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### StringValue

```cangjie
StringValue
```

**功能：** 字符串类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum HttpProtocol

```cangjie
public enum HttpProtocol {
    | Http1_1
    | Http2
    | Http3
    | ...
}
```

**功能：** HTTP协议版本。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Http1_1

```cangjie
Http1_1
```

**功能：** 协议HTTP/1.1。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Http2

```cangjie
Http2
```

**功能：** 协议HTTP/2。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Http3

```cangjie
Http3
```

**功能：** 协议HTTP/3，若系统或服务器不支持，则使用低版本的HTTP协议请求。仅对HTTPS的URL生效，HTTP则会请求失败。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum HttpRequestEvent

```cangjie
public enum HttpRequestEvent <: Equatable<HttpRequestEvent> & Hashable & ToString {
    | HeadersReceive
    | DataReceive
    | DataEnd
    | DataReceiveProgress
    | DataSendProgress
    | ...
}
```

**功能：** HTTP请求事件类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**父类型：**

- Equatable\<HttpRequestEvent>
- Hashable
- ToString

### DataEnd

```cangjie
DataEnd
```

**功能：** HTTP流式响应数据接收完毕事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### DataReceive

```cangjie
DataReceive
```

**功能：** HTTP流式响应数据接收事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### DataReceiveProgress

```cangjie
DataReceiveProgress
```

**功能：** HTTP流式响应数据接收进度更新事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### DataSendProgress

```cangjie
DataSendProgress
```

**功能：** HTTP网络请求数据发送进度更新事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### HeadersReceive

```cangjie
HeadersReceive
```

**功能：** HTTP Response Header事件。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### func !=(HttpRequestEvent)

```cangjie
public operator func !=(other: HttpRequestEvent): Bool
```

**功能：** 比较两个HttpRequestEvent是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[HttpRequestEvent](#enum-httprequestevent)|是|-|要比较的另一个HttpRequestEvent实例。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|如果两个HttpRequestEvent不相等则返回true，否则返回false。|

### func ==(HttpRequestEvent)

```cangjie
public operator func ==(other: HttpRequestEvent): Bool
```

**功能：** 比较两个HttpRequestEvent是否相等。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[HttpRequestEvent](#enum-httprequestevent)|是|-|要比较的另一个HttpRequestEvent实例。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|如果两个HttpRequestEvent相等则返回true，否则返回false。|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**功能：** 获取HttpRequestEvent的哈希值。

**返回值：**

|类型|说明|
|:----|:----|
|Int64|返回HttpRequestEvent的哈希值。|

## enum RequestMethod

```cangjie
public enum RequestMethod {
    | Options
    | Get
    | Head
    | Post
    | Put
    | Delete
    | Trace
    | Connect
    | ...
}
```

**功能：** HTTP请求方法。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Connect

```cangjie
Connect
```

**功能：** HTTP请求CONNECT。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Delete

```cangjie
Delete
```

**功能：** HTTP请求DELETE。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Get

```cangjie
Get
```

**功能：** HTTP请求GET。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Head

```cangjie
Head
```

**功能：** HTTP请求HEAD。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Options

```cangjie
Options
```

**功能：** HTTP请求OPTIONS。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Post

```cangjie
Post
```

**功能：** HTTP请求POST。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Put

```cangjie
Put
```

**功能：** HTTP请求PUT。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### Trace

```cangjie
Trace
```

**功能：** HTTP请求TRACE。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## enum UsingProxy

```cangjie
public enum UsingProxy {
    | NotUse
    | UseDefault
    | UseSpecified(HttpProxy)
    | ...
}
```

**功能：** 使用代理的类型。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### NotUse

```cangjie
NotUse
```

**功能：** 不使用代理。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### UseDefault

```cangjie
UseDefault
```

**功能：** 使用默认代理。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

### UseSpecified(HttpProxy)

```cangjie
UseSpecified(HttpProxy)
```

**功能：** 使用指定类型代理。

**系统能力：** SystemCapability.Communication.NetStack

**起始版本：** 22

## 完整示例

```cangjie
import kit.NetworkKit.*
import ohos.base.*
import std.collection.*

// 每一个httpRequest对应一个HTTP请求任务，不可复用
let httpRequest = createHttp()
// 用于订阅HTTP响应头，此接口会比request请求先返回。可以根据业务需要订阅此消息
httpRequest.onHeadersReceive({header: HashMap<String, String> =>
    Hilog.info(0, "AppLogCj", "header: ${header}")
})

let option = HttpRequestOptions(
    method: RequestMethod.POST, // 可选，默认为http.RequestMethod.GET
    // 当使用POST请求时此字段用于传递内容
    extraData: HttpData.STRING_DATA("data to send"),
    expectDataType: HttpDataType.STRING, // 可选，指定返回数据的类型
    usingCache: true, // 可选，默认为true
    priority: 1, // 可选，默认为1
    // 开发者根据自身业务需要添加header字段
    header: HashMap<String, String>([("content-type", "application/json")]),
    readTimeout: 60000, // 可选，默认为60000ms
    connectTimeout: 60000, // 可选，默认为60000ms
    usingProtocol: HttpProtocol.HTTP1_1, // 可选，协议类型默认值由系统自动指定
    usingProxy: UsingProxy.USE_DEFAULT, //可选，默认不使用网络代理，自API 10开始支持该属性
    caPath: "/path/to/cacert.pem", // 可选，默认使用系统预设CA证书，自API 10开始支持该属性
    clientCert: ClientCert(
        "/path/to/client.pem", // 默认不使用客户端证书
        "/path/to/client.key", // 若证书包含Key信息，传入空字符串
        certType: CertType.PEM, // 可选，默认使用PEM
        keyPassword: "PASSWORD_TO_KEY" // 可选，输入key文件的密码
    ),
    multiFormDataList: [ // 可选，仅当Header中，'content-Type'为'multipart/form-data'时生效
        MultiFormData (
            "Part1", // 数据名
            "text/plain", // 数据类型
            data: STRING_DATA("Example data"), // 可选，数据内容
            remoteFileName: "example.txt" // 可选
        ),
        MultiFormData (
            "Part2", // 数据名
            "text/plain", // 数据类型
            filePath: "/data/app/el2/100/base/com.example.myapplication/haps/entry/files/fileName.txt", // 可选，传入文件路径
            remoteFileName: "fileName.txt" // 可选
        )
    ]
)

httpRequest.request( // 填写HTTP请求的URL地址，可以带参数也可以不带参数。URL地址需要开发者自定义。请求的参数可以在extraData中指定
    "http://www.example.com", { err, resp =>
        if (let Some(e) <- err) {
            Hilog.error(0, "AppLogCj","exception: ${e.message}")
            throw e
        }
        if (let Some(r) <- resp) {
            Hilog.error(0, "AppLogCj", "${r}")
        } else {
            Hilog.error(0, "AppLogCj", "resp is none")
        }
        httpRequest.destroy()
    }, options: option)
```
