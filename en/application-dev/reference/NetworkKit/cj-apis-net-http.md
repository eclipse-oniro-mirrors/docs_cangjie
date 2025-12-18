# ohos.net.http (Data Request)

This module provides HTTP data request capabilities. Applications can initiate data requests via HTTP, supporting common methods such as GET, POST, OPTIONS, HEAD, PUT, DELETE, TRACE, and CONNECT.

## Import Module

```cangjie
import kit.NetworkKit.*
```

## Permission List

ohos.permission.INTERNET

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie-Example-Code-Instructions).

## func createHttp()

```cangjie
public func createHttp(): HttpRequest
```

**Function:** Creates an HTTP request. The request object includes functionalities such as initiating requests, aborting requests, and subscribing/unsubscribing to HTTP Response Header events. Each HttpRequest object corresponds to one HTTP request. To initiate multiple HTTP requests, a corresponding HttpRequest object must be created for each request.

> **Note:**
>
> When the request is no longer needed, the destroy method must be called to actively release the HttpRequest object.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [HttpRequest](#class-httprequest) | Returns an HttpRequest object, which includes the request, requestInStream, destroy, on, and off methods. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let httpRequest = createHttp()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createHttpResponseCache(UInt32)

```cangjie
public func createHttpResponseCache(cacheSize!: UInt32 = MAX_CACHE_SIZE): HttpResponseCache
```

**Function:** Creates a default object to store responses from HTTP access requests.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| cacheSize | UInt32 | No | MAX_CACHE_SIZE | **Named parameter.** The maximum cache size is 10*1024*1024 (10MB), defaulting to the maximum. |

**Return Value:**

| Type | Description |
|:----|:----|
| [HttpResponseCache](#class-httpresponsecache) | Returns an object that stores responses from HTTP access requests. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let httpResponseCache = createHttpResponseCache()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
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

**Function:** Client certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var certPath

```cangjie
public var certPath: String
```

**Function:** Certificate path.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var certType

```cangjie
public var certType: CertType
```

**Function:** Certificate type, default is PEM.

**Type:** [CertType](#enum-certtype)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var keyPassword

```cangjie
public var keyPassword: String
```

**Function:** Password for the certificate key.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var keyPath

```cangjie
public var keyPath: String
```

**Function:** Path to the certificate key.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### init(String, String, CertType, String)

```cangjie
public init(certPath: String, keyPath: String, certType!: CertType = CertType.Pem, keyPassword!: String = "")
```

**Function:** Constructs a ClientCert instance.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| certPath | String | Yes | - | Certificate path. |
| keyPath | String | Yes | - | Path to the certificate key. |
| certType | [CertType](#enum-certtype) | No | CertType.Pem | **Named parameter.** Certificate type, default is PEM. |
| keyPassword | String | No | "" | **Named parameter.** Password for the certificate key. |

## class DataReceiveProgressInfo

```cangjie
public class DataReceiveProgressInfo {
    public var receiveSize: Int64
    public var totalSize: Int64
}
```

**Function:** Data reception information.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var receiveSize

```cangjie
public var receiveSize: Int64
```

**Function:** Amount of data received, in bytes.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var totalSize

```cangjie
public var totalSize: Int64
```

**Function:** Total amount of data to be received, in bytes.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## class DataSendProgressInfo

```cangjie
public class DataSendProgressInfo {
    public var sendSize: Int64
    public var totalSize: Int64
}
```

**Function:** Data transmission information.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var sendSize

```cangjie
public var sendSize: Int64
```

**Function:** Amount of data sent each time, in bytes.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var totalSize

```cangjie
public var totalSize: Int64
```

**Function:** Total amount of data to be sent, in bytes.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## class HttpRequest

```cangjie
public class HttpRequest {}
```

**Function:** HTTP request task. Before calling methods of HttpRequest, you must first create a task via [createHttp](../NetworkKit/cj-apis-net-http.md#func-createhttp).

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### func destroy()

```cangjie
public func destroy(): Unit
```

**Function:** Aborts the request task.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let httpRequest = createHttp()

    httpRequest.destroy()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func off(HttpRequestEvent, ?CallbackObject)

```cangjie
public func off(event: HttpRequestEvent, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from HTTP request events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | Type of HTTP request event to unsubscribe from. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | Callback function. You can specify the callback passed in `on` to unsubscribe from the corresponding event, or omit the callback to clear all subscriptions. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only the HeadersReceive event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**Function:** Subscribes to HTTP Response Header events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports HeadersReceive event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>> | Yes | - | Callback function, returns the HTTP response header object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only the HeadersReceive event type is supported. |### func on(HttpRequestEvent, Callback1Argument\<Array\<Byte>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<Array<Byte>>): Unit
```

**Function:** Subscribes to HTTP streaming response data reception events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataReceive event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<Byte>> | Yes | - | Callback function for receiving HTTP streaming response data. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed | Check the event parameter to ensure it is a supported event type. Currently, only DataReceive event type is supported. |

### func on(HttpRequestEvent, Callback0Argument)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback0Argument): Unit
```

**Function:** Subscribes to HTTP streaming response data completion events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataEnd event. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed | Check the event parameter to ensure it is a supported event type. Currently, only DataEnd event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<DataReceiveProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataReceiveProgressInfo>): Unit
```

**Function:** Subscribes to HTTP streaming response data reception progress events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataReceiveProgress event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataReceiveProgressInfo](#class-datareceiveprogressinfo)> | Yes | - | Callback function for receiving data reception progress information, parameter is a DataReceiveProgressInfo object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed | Check the event parameter to ensure it is a supported event type. Currently, only DataReceiveProgress event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<DataSendProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataSendProgressInfo>): Unit
```

**Function:** Subscribes to HTTP network request data sending progress events.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataSendProgress event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataSendProgressInfo](#class-datasendprogressinfo)> | Yes | - | Callback function for receiving data sending progress information, parameter is a DataSendProgressInfo object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed | Check the event parameter to ensure it is a supported event type. Currently, only DataSendProgress event type is supported. |

### func once(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func once(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**Function:** Subscribes to HTTP Response Header event, which can only be triggered once. After triggering, the subscriber is removed. Uses callback as an asynchronous method.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports HeadersReceive event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>> | Yes | - | Callback function. Returns HTTP response header object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed | Check the event parameter to ensure it is a supported event type. Currently, only HeadersReceive event type is supported. |

### func request(String, HttpRequestOptions, AsyncCallback\<HttpResponse>)

```cangjie
public func request(url: String, options: HttpRequestOptions, callback: AsyncCallback<HttpResponse>): Unit
```

**Function:** Initiates an HTTP network request based on the URL address and returns the response in the callback function.

> **Note:**
>
> This interface only supports receiving data up to 5MB in size.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| options | [HttpRequestOptions](#class-httprequestoptions) | Yes | - | Refer to [HttpRequestOptions](#class-httprequestoptions). |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl error codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
  | :---- | :--- |
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
  | 2300997 | Cleartext traffic not permitted. |
  | 2300998 | It is not allowed to access this domain. |
  | 2300999 | Unknown Other Error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
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
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func request(String, AsyncCallback\<HttpResponse>)

```cangjie
public func request(url: String, callback: AsyncCallback<HttpResponse>): Unit
```

**Function:** Initiates an HTTP network request based on the URL address and returns the response in the callback function.

> **Note:**
>
> This interface only supports receiving data up to 5MB in size.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl error codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
  | :---- | :--- |
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
  | 2300997 | Cleartext traffic not permitted. |
  | 2300998 | It is not allowed to access this domain. |
  | 2300999 | Unknown Other Error. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.NetworkKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
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
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func requestInStream(String, HttpRequestOptions, AsyncCallback\<UInt32>)

```cangjie
public func requestInStream(url: String, options: HttpRequestOptions, callback: AsyncCallback<UInt32>): Unit
```

**Function:** Initiates an HTTP network request based on the URL address and configuration items, returns a streaming response, and provides the response in the callback function.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| options | [HttpRequestOptions](#class-httprequestoptions) | Yes | - | Refer to [HttpRequestOptions](#class-httprequestoptions). |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<UInt32> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl error codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
  | :---- | :--- |
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

**Function:** Type and value range of optional parameters for initiating requests.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var caPath

```cangjie
public var caPath: String
```

**Function:** If this parameter is set, the system will use the CA certificate at the user-specified path (developers must ensure the accessibility of the CA certificate at this path). Otherwise, the system will use the preset CA certificate located at: /etc/ssl/certs/cacert.pem. The certificate path is a sandbox-mapped path (developers can obtain the application sandbox path via Global.getContext().filesDir). Currently, only text-format certificates with the .pem extension are supported.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var clientCert

```cangjie
public var clientCert: ClientCert
```

**Function:** Supports transmitting client certificates.

**Type:** [ClientCert](#class-clientcert)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var connectTimeout

```cangjie
public var connectTimeout: UInt32
```

**Function:** Connection timeout duration. Unit: milliseconds (ms), default is 60000ms.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var dnsOverHttps

```cangjie
public var dnsOverHttps: String
```

**Function:** Sets the use of an HTTPS protocol server for DNS resolution.<br />The parameter must be URL-encoded in the following format: "https://host:port/path".

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var dnsServers

```cangjie
public var dnsServers: Array<String>
```

**Function:** Sets specified DNS servers for DNS resolution.<br />Multiple DNS servers can be set, up to a maximum of 3 servers. If more than 3 are provided, only the first 3 will be used.<br />Servers must be IPv4 or IPv6 addresses.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var expectDataType

```cangjie
public var expectDataType:?HttpDataType
```

**Function:** Specifies the type of returned data. By default, this field is not set. If this parameter is set, the system will prioritize returning the specified type.

**Type:** ?[HttpDataType](#enum-httpdatatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var extraData

```cangjie
public var extraData: HttpData
```

**Function:** Additional data sent with the request. By default, this field is not set.

- For HTTP requests with methods like POST and PUT, this field serves as the HTTP request content, encoded in UTF-8 as the request body.
  - When 'content-Type' is 'application/x-www-form-urlencoded', the submitted data should be URL-encoded key-value pairs in the format "key1=value1&key2=value2&key3=value3". The corresponding type for this field is typically String.
  - When 'content-Type' is 'text/xml', the corresponding type is typically String.
  - When 'content-Type' is 'application/json', the corresponding type is typically Object.
  - When 'content-Type' is 'application/octet-stream', the corresponding type is typically ArrayBuffer.
  - When 'content-Type' is 'multipart/form-data' and the field to be uploaded is a file, the corresponding type is typically ArrayBuffer.
- For HTTP requests with methods like GET, OPTIONS, DELETE, TRACE, and CONNECT, this field serves as supplementary parameters for the HTTP request. Developers need to provide string-type parameters encoded in Encode format. Object-type parameters do not require pre-encoding and will be concatenated into the URL for sending; ArrayBuffer-type parameters will not be concatenated.

The above information is for reference only and may vary depending on specific circumstances.

**Type:** [HttpData](#enum-httpdata)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var header

```cangjie
public var header: HashMap<String, String>
```

**Function:** HTTP request header fields. Default is {'content-Type': 'application/json'}.

**Type:** HashMap\<String,String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var maxLimit

```cangjie
public var maxLimit: UInt32
```

**Function:** Maximum byte limit for response messages. Default is 5MB, in bytes. Maximum value is 10MB, in bytes.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var method

```cangjie
public var method: RequestMethod
```

**Function:** Request method. Default is GET.

**Type:** [RequestMethod](#enum-requestmethod)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var multiFormDataList

```cangjie
public var multiFormDataList: Array<MultiFormData>
```

**Function:** When 'content-Type' is 'multipart/form-data', this field defines the list of data fields to be uploaded.

**Type:** Array\<[MultiFormData](#class-multiformdata)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var priority

```cangjie
public var priority: UInt32
```

**Function:** Priority, range [1,1000], default is 1. If the parameter exceeds the range, the default value 1 will be used.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var readTimeout

```cangjie
public var readTimeout: UInt32
```

**Function:** Read timeout duration. Unit: milliseconds (ms), default is 60000ms.<br />Setting it to 0 means no timeout will occur.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var resumeFrom

```cangjie
public var resumeFrom: Int64
```

**Function:** Sets the starting position for upload or download. HTTP standard (RFC 7233 Section 3.1) allows servers to ignore range requests.<br />Setting this parameter with HTTP PUT may cause unknown issues.<br />Valid range: 1~4294967296 (4GB). Values outside this range will not take effect. No default value.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var resumeTo

```cangjie
public var resumeTo: Int64
```

**Function:** Sets the ending position for upload or download. HTTP standard (RFC 7233 Section 3.1) allows servers to ignore range requests.<br />Setting this parameter with HTTP PUT may cause unknown issues.<br />Valid range: 1~4294967296 (4GB). Values outside this range will not take effect. No default value.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var usingCache

```cangjie
public var usingCache: Bool
```

**Function:** Whether to use cache. Default is true, and the cache will be read first when making a request. The cache is effective for the current process. New cache will replace old cache.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var usingProtocol

```cangjie
public var usingProtocol:?HttpProtocol
```

**Function:** Protocol to use. Default value is automatically determined by the system.

**Type:** ?[HttpProtocol](#enum-httpprotocol)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var usingProxy

```cangjie
public var usingProxy: UsingProxy
```

**Function:** Whether to use HTTP proxy. Default is USE_DEFAULT, which uses the default proxy.<br />When usingProxy is NOT_USE, no network proxy will be used.<br />When usingProxy is USE_SPECIFIED, the specified network proxy will be used.

**Type:** [UsingProxy](#enum-usingproxy)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

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

**Function:** Constructs an HttpRequestOptions instance.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| method | [RequestMethod](#enum-requestmethod) | No | RequestMethod.Get | **Named parameter.** Request method, default is GET. |
| extraData | [HttpData](#enum-httpdata) | No | HttpData.StringData("") | **Named parameter.** Additional data sent with the request. By default, this field is not set. |
| expectDataType | ?[HttpDataType](#enum-httpdatatype) | No | None | **Named parameter.** Specifies the type of returned data. By default, this field is not set. |
| usingCache | Bool | No | true | **Named parameter.** Whether to use cache. Default is true. |
| priority | UInt32 | No | 1 | **Named parameter.** Priority, range [1,1000], default is 1. |
| header | HashMap\<String,String> | No | HashMap<String,String>() | **Named parameter.** HTTP request header fields. |
| readTimeout | UInt32 | No | 60000 | **Named parameter.** Read timeout duration, in milliseconds. |
| connectTimeout | UInt32 | No | 60000 | **Named parameter.** Connection timeout duration, in milliseconds. |
| usingProtocol | ?[HttpProtocol](#enum-httpprotocol) | No | None | **Named parameter.** Protocol to use. Default value is automatically determined by the system. |
| usingProxy | [UsingProxy](#enum-usingproxy) | No | UsingProxy.UseDefault | **Named parameter.** Whether to use HTTP proxy. Default is USE_DEFAULT. |
| caPath | String | No | "" | **Named parameter.** CA certificate path. If set, the system will use the CA certificate at the specified path. |
| resumeFrom | Int64 | No | 0 | **Named parameter.** Sets the starting position for upload or download. |
| resumeTo | Int64 | No | 0 | **Named parameter.** Sets the ending position for upload or download. |
| clientCert | [ClientCert](#class-clientcert) | No | ClientCert("", "") | **Named parameter.** Supports transmitting client certificates. |
| dnsOverHttps | String | No | "" | **Named parameter.** Sets the use of an HTTPS protocol server for DNS resolution. |
| dnsServers | Array\<String> | No | Array\<String>() | **Named parameter.** Sets specified DNS servers for DNS resolution. |
| maxLimit | UInt32 | No | 5 * 1024 * 1024 | **Named parameter.** Maximum byte limit for response messages. Default is 5MB. |
| multiFormDataList | Array\<[MultiFormData](#class-multiformdata)> | No | Array\<MultiFormData>() | **Named parameter.** When 'content-Type' is 'multipart/form-data', this field defines the list of data fields to be uploaded. |

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

**Function:** Return type of the callback function for the request method.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var cookies

```cangjie
public var cookies: String
```

**Function:** Cookies returned by the server.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var header

```cangjie
public var header: HashMap<String, String>
```

**Function:** Response headers returned from the HTTP request.

**Type:** HashMap\<String,String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var performanceTiming

```cangjie
public var performanceTiming: PerformanceTiming
```

**Function:** Time consumption for each phase of the HTTP request.

**Type:** [PerformanceTiming](#class-performancetiming)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var responseCode

```cangjie
public var responseCode: UInt32
```

**Function:** Response status code.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var result

```cangjie
public var result: HttpData
```

**Function:** HTTP request returns corresponding response format content based on the content-type in the response header.

**Type:** [HttpData](#enum-httpdata)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var resultType

```cangjie
public var resultType: HttpDataType
```

**Function:** Return type.

**Type:** [HttpDataType](#enum-httpdatatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22## class HttpResponseCache

```cangjie
public class HttpResponseCache {}
```

**Function:** An object that stores HTTP request responses. Before calling methods of HttpResponseCache, a task must first be created via [createHttpResponseCache](#func-createhttpresponsecacheuint32).

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### func delete()

```cangjie
public func delete(): Unit
```

**Function:** Disables the cache and deletes its data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Example:**

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

**Function:** Writes cached data to the file system, enabling access to all cached data in the next HTTP request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Example:**

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

**Function:** The type for multipart form data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var contentType

```cangjie
public var contentType: String
```

**Function:** Data type, such as 'text/plain', 'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4', etc.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var data

```cangjie
public var data: HttpData
```

**Function:** The content of the form data.

**Type:** [HttpData](#enum-httpdata)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var filePath

```cangjie
public var filePath: String
```

**Function:** This parameter sets the body content of the MIME part based on the file content. It is used to replace `data` for setting file data as the content. If `data` is empty, `filePath` must be set. If `data` has a value, `filePath` will not take effect.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var name

```cangjie
public var name: String
```

**Function:** The name of the data.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var remoteFileName

```cangjie
public var remoteFileName: String
```

**Function:** The name of the file to be saved on the server after upload.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### init(String, String, String, HttpData, String)

```cangjie
public init(name: String, contentType: String,  remoteFileName!: String = "",
    data!: HttpData = HttpData.StringData(""), filePath!: String = "")
```

**Function:** Constructs a MultiFormData instance.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the data. |
| contentType | String | Yes | - | Data type, such as 'text/plain', 'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4', etc. |
| remoteFileName | String | No | "" | **Named parameter.** The name of the file to be saved on the server after upload. |
| data | [HttpData](#enum-httpdata) | No | HttpData.StringData("") | **Named parameter.** The content of the form data. |
| filePath | String | No | "" | **Named parameter.** This parameter sets the body content of the MIME part based on the file content. It is used to replace `data` for setting file data as the content. If `data` is empty, `filePath` must be set. If `data` has a value, `filePath` will not take effect. |

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

**Function:** Performance timing data, measured in milliseconds.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var dnsTiming

```cangjie
public var dnsTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to DNS resolution completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var firstReceiveTiming

```cangjie
public var firstReceiveTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to receiving the first byte.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var firstSendTiming

```cangjie
public var firstSendTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to sending the first byte.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var redirectTiming

```cangjie
public var redirectTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to completing all redirect steps.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var responseBodyTiming

```cangjie
public var responseBodyTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to body parsing completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var responseHeaderTiming

```cangjie
public var responseHeaderTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to header parsing completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var tcpTiming

```cangjie
public var tcpTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to TCP connection completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var tlsTiming

```cangjie
public var tlsTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to TLS connection completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var totalFinishTiming

```cangjie
public var totalFinishTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to request completion.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### var totalTiming

```cangjie
public var totalTiming: Float64
```

**Function:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) callback to the application.

**Type:** Float64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## enum CertType

```cangjie
public enum CertType {
    | Pem
    | Der
    | P12
    | ...
}
```

**Function:** Certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Der

```cangjie
Der
```

**Function:** DER certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### P12

```cangjie
P12
```

**Function:** P12 certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Pem

```cangjie
Pem
```

**Function:** PEM certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22## enum HttpData

```cangjie
public enum HttpData {
    | StringData(String)
    | ArrayData(Array<Byte>)
    | ...
}
```

**Function:** HTTP data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### ArrayData(Array\<Byte>)

```cangjie
ArrayData(Array<Byte>)
```

**Function:** Binary array.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### StringData(String)

```cangjie
StringData(String)
```

**Function:** String.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## enum HttpDataType

```cangjie
public enum HttpDataType {
    | StringValue
    | ArrayBuffer
    | ...
}
```

**Function:** HTTP data types.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### ArrayBuffer

```cangjie
ArrayBuffer
```

**Function:** Binary array type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### StringValue

```cangjie
StringValue
```

**Function:** String type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## enum HttpProtocol

```cangjie
public enum HttpProtocol {
    | Http1_1
    | Http2
    | Http3
    | ...
}
```

**Function:** HTTP protocol versions.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Http1_1

```cangjie
Http1_1
```

**Function:** Protocol HTTP/1.1.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Http2

```cangjie
Http2
```

**Function:** Protocol HTTP/2.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Http3

```cangjie
Http3
```

**Function:** Protocol HTTP/3. If the system or server does not support it, a lower version of HTTP protocol will be used for the request. Only effective for HTTPS URLs; HTTP requests will fail.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

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

**Function:** HTTP request event types.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parent Types:**

- Equatable\<HttpRequestEvent>
- Hashable
- ToString

### DataEnd

```cangjie
DataEnd
```

**Function:** HTTP streaming response data completion event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### DataReceive

```cangjie
DataReceive
```

**Function:** HTTP streaming response data reception event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### DataReceiveProgress

```cangjie
DataReceiveProgress
```

**Function:** HTTP streaming response data reception progress update event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### DataSendProgress

```cangjie
DataSendProgress
```

**Function:** HTTP network request data transmission progress update event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### HeadersReceive

```cangjie
HeadersReceive
```

**Function:** HTTP Response Header event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### func !=(HttpRequestEvent)

```cangjie
public operator func !=(other: HttpRequestEvent): Bool
```

**Function:** Compares whether two HttpRequestEvent instances are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[HttpRequestEvent](#enum-httprequestevent)|Yes|-|Another HttpRequestEvent instance to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two HttpRequestEvent instances are not equal, otherwise returns false.|

### func ==(HttpRequestEvent)

```cangjie
public operator func ==(other: HttpRequestEvent): Bool
```

**Function:** Compares whether two HttpRequestEvent instances are equal.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[HttpRequestEvent](#enum-httprequestevent)|Yes|-|Another HttpRequestEvent instance to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two HttpRequestEvent instances are equal, otherwise returns false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Gets the hash value of HttpRequestEvent.

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|Returns the hash value of HttpRequestEvent.|

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

**Function:** HTTP request methods.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Connect

```cangjie
Connect
```

**Function:** HTTP CONNECT request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Delete

```cangjie
Delete
```

**Function:** HTTP DELETE request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Get

```cangjie
Get
```

**Function:** HTTP GET request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Head

```cangjie
Head
```

**Function:** HTTP HEAD request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Options

```cangjie
Options
```

**Function:** HTTP OPTIONS request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Post

```cangjie
Post
```

**Function:** HTTP POST request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Put

```cangjie
Put
```

**Function:** HTTP PUT request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### Trace

```cangjie
Trace
```

**Function:** HTTP TRACE request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

## enum UsingProxy

```cangjie
public enum UsingProxy {
    | NotUse
    | UseDefault
    | UseSpecified(HttpProxy)
    | ...
}
```

**Function:** Types of proxy usage.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### NotUse

```cangjie
NotUse
```

**Function:** Do not use proxy.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### UseDefault

```cangjie
UseDefault
```

**Function:** Use default proxy.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22

### UseSpecified(HttpProxy)

```cangjie
UseSpecified(HttpProxy)
```

**Function:** Use specified proxy type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 22## Complete Example

```cangjie
import kit.NetworkKit.*
import ohos.base.*
import std.collection.*

// Each httpRequest corresponds to an HTTP request task and cannot be reused
let httpRequest = createHttp()
// Used to subscribe to HTTP response headers. This interface will return before the request. Can subscribe to this message based on business needs
httpRequest.onHeadersReceive({header: HashMap<String, String> =>
    Hilog.info(0, "AppLogCj", "header: ${header}")
})

let option = HttpRequestOptions(
    method: RequestMethod.POST, // Optional, defaults to http.RequestMethod.GET
    // This field is used to pass content when making POST requests
    extraData: HttpData.STRING_DATA("data to send"),
    expectDataType: HttpDataType.STRING, // Optional, specifies the type of returned data
    usingCache: true, // Optional, defaults to true
    priority: 1, // Optional, defaults to 1
    // Developers can add header fields based on their business needs
    header: HashMap<String, String>([("content-type", "application/json")]),
    readTimeout: 60000, // Optional, defaults to 60000ms
    connectTimeout: 60000, // Optional, defaults to 60000ms
    usingProtocol: HttpProtocol.HTTP1_1, // Optional, protocol type defaults to system auto-specification
    usingProxy: UsingProxy.USE_DEFAULT, // Optional, defaults to no network proxy. Supported since API 10
    caPath: "/path/to/cacert.pem", // Optional, defaults to system preset CA certificates. Supported since API 10
    clientCert: ClientCert(
        "/path/to/client.pem", // Defaults to no client certificate
        "/path/to/client.key", // If the certificate contains Key info, pass an empty string
        certType: CertType.PEM, // Optional, defaults to PEM
        keyPassword: "PASSWORD_TO_KEY" // Optional, password for the key file
    ),
    multiFormDataList: [ // Optional, only effective when 'content-Type' in Header is 'multipart/form-data'
        MultiFormData (
            "Part1", // Data name
            "text/plain", // Data type
            data: STRING_DATA("Example data"), // Optional, data content
            remoteFileName: "example.txt" // Optional
        ),
        MultiFormData (
            "Part2", // Data name
            "text/plain", // Data type
            filePath: "/data/app/el2/100/base/com.example.myapplication/haps/entry/files/fileName.txt", // Optional, pass file path
            remoteFileName: "fileName.txt" // Optional
        )
    ]
)

httpRequest.request( // Fill in the HTTP request URL address, which may or may not include parameters. The URL address needs to be customized by the developer. Request parameters can be specified in extraData
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