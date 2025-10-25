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

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#Cangjie-Example-Code-Description).

## func createHttp()

```cangjie
public func createHttp(): HttpRequest
```

**Function:** Creates an HTTP request. The request object includes capabilities to initiate requests, interrupt requests, and subscribe/unsubscribe to HTTP Response Header events. Each HttpRequest object corresponds to one HTTP request. To initiate multiple HTTP requests, a corresponding HttpRequest object must be created for each.

> **Note:**
>
> When the request is no longer needed, the destroy method must be called to actively release the HttpRequest object.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

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

let httpRequest = createHttp()
```

## func createHttpResponseCache(UInt32)

```cangjie
public func createHttpResponseCache(cacheSize!: UInt32 = MAX_CACHE_SIZE): HttpResponseCache
```

**Function:** Creates a default object to store responses from HTTP access requests.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
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

**Function:** Client certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var certPath

```cangjie
public var certPath: String
```

**Function:** Certificate path.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var certType

```cangjie
public var certType: CertType
```

**Function:** Certificate type, default is PEM.

**Type:** [CertType](#enum-certtype)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var keyPassword

```cangjie
public var keyPassword: String
```

**Function:** Password for the certificate key.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var keyPath

```cangjie
public var keyPath: String
```

**Function:** Path to the certificate key.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### init(String, String, CertType, String)

```cangjie
public init(certPath: String, keyPath: String, certType!: CertType = CertType.Pem, keyPassword!: String = "")
```

**Function:** Constructs a ClientCert instance.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
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

**Initial Version:** 21

### var receiveSize

```cangjie
public var receiveSize: Int64
```

**Function:** Amount of data received, in bytes.

**Type:** Int64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var totalSize

```cangjie
public var totalSize: Int64
```

**Function:** Total amount of data to receive, in bytes.

**Type:** Int64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

## class DataSendProgressInfo

```cangjie
public class DataSendProgressInfo {
    public var sendSize: Int64
    public var totalSize: Int64
}
```

**Function:** Data transmission information.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var sendSize

```cangjie
public var sendSize: Int64
```

**Function:** Amount of data sent each time, in bytes.

**Type:** Int64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### var totalSize

```cangjie
public var totalSize: Int64
```

**Function:** Total amount of data to send, in bytes.

**Type:** Int64

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

## class HttpRequest

```cangjie
public class HttpRequest {}
```

**Function:** HTTP request task. Before calling methods of HttpRequest, a task must first be created via [createHttp](../NetworkKit/cj-apis-net-http.md#func-createhttp).

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

### func destroy()

```cangjie
public func destroy(): Unit
```

**Function:** Interrupts the request task.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Example:**

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

**Function:** Unsubscribes from HTTP request events.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | Type of HTTP request event to unsubscribe from. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | Callback function. You can specify the callback passed to on to unsubscribe from the corresponding event, or omit the callback to clear all subscriptions. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | The provided event type is not supported. | Check the event parameter to ensure it is a supported event type. Currently, only the HeadersReceive event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**Function:** Subscribes to HTTP Response Header events.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports HeadersReceive events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>> | Yes | - | Callback function that returns the HTTP response header object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | The provided event type is not supported. | Check the event parameter to ensure it is a supported event type. Currently, only the HeadersReceive event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<Array\<Byte>>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<Array<Byte>>): Unit
```

**Function:** Subscribes to HTTP streaming response data reception events.

**System Capability:** SystemCapability.Communication.NetStack

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataReceive events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<Byte>> | Yes | - | Callback function for receiving HTTP streaming response data. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | The provided event type is not supported. | Check the event parameter to ensure it is a supported event type. Currently, only the DataReceive event type is supported. |### func on(HttpRequestEvent, Callback0Argument)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback0Argument): Unit
```

**Function:** Subscribes to the HTTP streaming response data reception completion event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataEnd event. |
| callback | [Callback0Argument](../arkinterop/cj-api-callback_invoke.md#class-callback0argument) | Yes | - | Callback function. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only DataEnd event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<DataReceiveProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataReceiveProgressInfo>): Unit
```

**Function:** Subscribes to the HTTP streaming response data reception progress event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataReceiveProgress event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataReceiveProgressInfo](#class-datareceiveprogressinfo)> | Yes | - | Callback function for receiving data reception progress information, with the parameter being a DataReceiveProgressInfo object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only DataReceiveProgress event type is supported. |

### func on(HttpRequestEvent, Callback1Argument\<DataSendProgressInfo>)

```cangjie
public func on(event: HttpRequestEvent, callback: Callback1Argument<DataSendProgressInfo>): Unit
```

**Function:** Subscribes to the HTTP network request data sending progress event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports DataSendProgress event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DataSendProgressInfo](#class-datasendprogressinfo)> | Yes | - | Callback function for receiving data sending progress information, with the parameter being a DataSendProgressInfo object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only DataSendProgress event type is supported. |

### func once(HttpRequestEvent, Callback1Argument\<HashMap\<String,String>>)

```cangjie
public func once(event: HttpRequestEvent, callback: Callback1Argument<HashMap<String, String>>): Unit
```

**Function:** Subscribes to the HTTP Response Header event, which can only be triggered once. After triggering, the subscriber will be removed. Uses callback as an asynchronous method.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | HTTP request event type, only supports HeadersReceive event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<HashMap\<String,String>> | Yes | - | Callback function. Returns the HTTP response header object. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The parameter check failed. | Unsupported event type passed in | Check the event parameter to ensure it is a supported event type. Currently, only HeadersReceive event type is supported. |

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

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| options | [HttpRequestOptions](#class-httprequestoptions) | Yes | - | Refer to [HttpRequestOptions](#class-httprequestoptions). |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)> | Yes | - | Callback function. |

**Exceptions:**

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl Error Codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
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

**Example:**

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

**Function:** Initiates an HTTP network request based on the URL address and returns the response in the callback function.

> **Note:**
>
> This interface only supports receiving data up to 5MB in size.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[HttpResponse](#class-httpresponse)> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl Error Codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
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

**Example:**

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

**Function:** Initiates an HTTP network request based on the URL address and related configuration items, returns a streaming response, and returns the response in the callback function.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| options | [HttpRequestOptions](#class-httprequestoptions) | Yes | - | Refer to [HttpRequestOptions](#class-httprequestoptions). |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<UInt32> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below, [HTTP Error Codes](./cj-errorcode-net-http.md) and [Universal Error Codes](../cj-errorcode-universal.md).
- HTTP interface return error code mapping: 2300000 + curl error code. For more common error codes, refer to: [curl Error Codes](https://curl.se/libcurl/c/libcurl-errors.html).

  | Error Code ID | Error Message |
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

**Example:**

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

**Function:** Initiates an HTTP network request based on the URL address and related configuration items, returns a streaming response, and returns the response in the callback function.

**Required Permission:** ohos.permission.INTERNET

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | URL address for initiating the network request. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_ex## class HttpRequestOptions

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

**Description:** Optional parameters for initiating requests, including their types and value ranges.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var caPath

```cangjie
public var caPath: String
```

**Description:** If this parameter is set, the system will use the CA certificate at the user-specified path (developers must ensure the accessibility of the CA certificate at this path). Otherwise, the system will use the preset CA certificate located at: /etc/ssl/certs/cacert.pem. The certificate path is a sandbox-mapped path (developers can obtain the application sandbox path via Global.getContext().filesDir). Currently, only text-format certificates with the .pem extension are supported.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var clientCert

```cangjie
public var clientCert: ClientCert
```

**Description:** Supports transmitting client certificates.

**Type:** [ClientCert](#class-clientcert)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var connectTimeout

```cangjie
public var connectTimeout: UInt32
```

**Description:** Connection timeout duration. Unit: milliseconds (ms), default is 60000ms.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var dnsOverHttps

```cangjie
public var dnsOverHttps: String
```

**Description:** Sets the use of an HTTPS protocol server for DNS resolution.<br />The parameter must be URL-encoded in the following format: "https://host:port/path".

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var dnsServers

```cangjie
public var dnsServers: Array<String>
```

**Description:** Sets specified DNS servers for DNS resolution.<br />Multiple DNS servers can be set, up to a maximum of 3 servers. If more than 3 are provided, only the first 3 will be used.<br />Servers must be IPv4 or IPv6 addresses.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var expectDataType

```cangjie
public var expectDataType:?HttpDataType
```

**Description:** Specifies the type of returned data. By default, this field is not set. If this parameter is set, the system will prioritize returning the specified type.

**Type:** ?[HttpDataType](#enum-httpdatatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var extraData

```cangjie
public var extraData: HttpData
```

**Description:** Additional data sent with the request. By default, this field is not set.

- For HTTP requests with methods like POST, PUT, etc., this field serves as the HTTP request content, encoded in UTF-8 as the request body.
  - When 'content-Type' is 'application/x-www-form-urlencoded', the submitted form data should be URL-encoded key-value pairs in the format "key1=value1&key2=value2&key3=value3". The corresponding type for this field is typically String.
  - When 'content-Type' is 'text/xml', the corresponding type is typically String.
  - When 'content-Type' is 'application/json', the corresponding type is typically Object.
  - When 'content-Type' is 'application/octet-stream', the corresponding type is typically ArrayBuffer.
  - When 'content-Type' is 'multipart/form-data' and the field to be uploaded is a file, the corresponding type is typically ArrayBuffer.
- For HTTP requests with methods like GET, OPTIONS, DELETE, TRACE, CONNECT, etc., this field serves as supplementary parameters for the HTTP request. Developers need to provide string-type parameters encoded in Encode format. Object-type parameters do not require pre-encoding and will be appended to the URL for sending; ArrayBuffer-type parameters will not be appended.

The above information is for reference only and may vary depending on specific circumstances.

**Type:** [HttpData](#enum-httpdata)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var header

```cangjie
public var header: HashMap<String, String>
```

**Description:** HTTP request header fields. Default is {'content-Type': 'application/json'}.

**Type:** HashMap\<String,String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var maxLimit

```cangjie
public var maxLimit: UInt32
```

**Description:** Maximum byte limit for response messages, default is 5MB, in bytes. Maximum value is 10MB, in bytes.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var method

```cangjie
public var method: RequestMethod
```

**Description:** Request method, default is GET.

**Type:** [RequestMethod](#enum-requestmethod)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var multiFormDataList

```cangjie
public var multiFormDataList: Array<MultiFormData>
```

**Description:** When 'content-Type' is 'multipart/form-data', this field defines the list of form data fields to be uploaded.

**Type:** Array\<[MultiFormData](#class-multiformdata)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var priority

```cangjie
public var priority: UInt32
```

**Description:** Priority, range [1,1000], default is 1. If the provided value is out of range, the default value of 1 will be used.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var readTimeout

```cangjie
public var readTimeout: UInt32
```

**Description:** Read timeout duration. Unit: milliseconds (ms), default is 60000ms.<br />Setting it to 0 means no timeout will occur.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var resumeFrom

```cangjie
public var resumeFrom: Int64
```

**Description:** Sets the starting position for upload or download. HTTP standards (RFC 7233 Section 3.1) allow servers to ignore range requests.<br />Setting this parameter with HTTP PUT may cause unknown issues.<br />Valid range: 1~4294967296 (4GB). Values outside this range will not take effect. No default value.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var resumeTo

```cangjie
public var resumeTo: Int64
```

**Description:** Sets the ending position for upload or download. HTTP standards (RFC 7233 Section 3.1) allow servers to ignore range requests.<br />Setting this parameter with HTTP PUT may cause unknown issues.<br />Valid range: 1~4294967296 (4GB). Values outside this range will not take effect. No default value.

**Type:** Int64

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var usingCache

```cangjie
public var usingCache: Bool
```

**Description:** Whether to use cache, default is true. The request will prioritize reading from the cache. Cache is effective for the current process. New cache will replace old cache.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var usingProtocol

```cangjie
public var usingProtocol:?HttpProtocol
```

**Description:** Protocol to use. Default value is automatically determined by the system.

**Type:** ?[HttpProtocol](#enum-httpprotocol)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var usingProxy

```cangjie
public var usingProxy: UsingProxy
```

**Description:** Whether to use HTTP proxy, default is USE_DEFAULT, which uses the default proxy.<br />When usingProxy is NOT_USE, no network proxy will be used.<br />When usingProxy is USE_SPECIFIED, the specified network proxy will be used.

**Type:** [UsingProxy](#enum-usingproxy)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Description:** Constructs an instance of HttpRequestOptions.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| method | [RequestMethod](#enum-requestmethod) | No | RequestMethod.Get | **Named parameter.** Request method, default is GET. |
| extraData | [HttpData](#enum-httpdata) | No | HttpData.StringData("") | **Named parameter.** Additional data sent with the request. By default, this field is not set. |
| expectDataType | ?[HttpDataType](#enum-httpdatatype) | No | None | **Named parameter.** Specifies the type of returned data. By default, this field is not set. |
| usingCache | Bool | No | true | **Named parameter.** Whether to use cache, default is true. |
| priority | UInt32 | No | 1 | **Named parameter.** Priority, range [1,1000], default is 1. |
| header | HashMap\<String,String> | No | HashMap<String,String>() | **Named parameter.** HTTP request header fields. |
| readTimeout | UInt32 | No | 60000 | **Named parameter.** Read timeout duration, in milliseconds. |
| connectTimeout | UInt32 | No | 60000 | **Named parameter.** Connection timeout duration, in milliseconds. |
| usingProtocol | ?[HttpProtocol](#enum-httpprotocol) | No | None | **Named parameter.** Protocol to use. Default value is automatically determined by the system. |
| usingProxy | [UsingProxy](#enum-usingproxy) | No | UsingProxy.UseDefault | **Named parameter.** Whether to use HTTP proxy, default is USE_DEFAULT. |
| caPath | String | No | "" | **Named parameter.** CA certificate path. If this parameter is set, the system will use the user-specified CA certificate. |
| resumeFrom | Int64 | No | 0 | **Named parameter.** Sets the starting position for upload or download. |
| resumeTo | Int64 | No | 0 | **Named parameter.** Sets the ending position for upload or download. |
| clientCert | [ClientCert](#class-clientcert) | No | ClientCert("", "") | **Named parameter.** Supports transmitting client certificates. |
| dnsOverHttps | String | No | "" | **Named parameter.** Sets the use of an HTTPS protocol server for DNS resolution. |
| dnsServers | Array\<String> | No | Array<String>() | **Named parameter.** Sets specified DNS servers for DNS resolution. |
| maxLimit | UInt32 | No | 5 * 1024 * 1024 | **Named parameter.** Maximum byte limit for response messages, default is 5MB. |
| multiFormDataList | Array\<[MultiFormData](#class-multiformdata)> | No | Array<MultiFormData>() | **Named parameter.** When 'content-Type' is 'multipart/form-data', this field defines the list of form data fields to be uploaded. |

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

**Description:** Return type for the callback function of the request method.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var cookies

```cangjie
public var cookies: String
```

**Description:** Cookies returned by the server.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var header

```cangjie
public var header: HashMap<String, String>
```

**Description:** Response headers returned from the HTTP request.

**Type:** HashMap\<String,String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var performanceTiming

```cangjie
public var performanceTiming: PerformanceTiming
```

**Description:** Time consumption for each phase of the HTTP request.

**Type:** [PerformanceTiming](#class-performancetiming)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var responseCode

```cangjie
public var responseCode: UInt32
```

**Description:** Response status code.

**Type:** UInt32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var result

```cangjie
public var result: HttpData
```

**Description:** HTTP request returns corresponding response format content based on the content-type in the response header.

**Type:** [HttpData](#enum-httpdata)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var resultType

```cangjie
public var resultType: HttpDataType
```

**Description:** Return value type.

**Type:** [HttpDataType](#enum-httpdatatype)

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21## class HttpResponseCache

```cangjie
public class HttpResponseCache {}
```

**Description:** An object that stores HTTP request responses. Before calling methods of HttpResponseCache, a task must first be created via [createHttpResponseCache](#func-createhttpresponsecacheuint32).

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### func delete()

```cangjie
public func delete(): Unit
```

**Description:** Disables the cache and deletes its data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Description:** Writes cached data to the file system, enabling access to all cached data in the next HTTP request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Description:** The type for multipart form data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var contentType

```cangjie
public var contentType: String
```

**Description:** The data type, such as 'text/plain', 'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4', etc.

**Type:** String

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var data

```cangjie
public var data: HttpData
```

**Description:** The content of the form data.

**Type:** [HttpData](#enum-httpdata)

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var filePath

```cangjie
public var filePath: String
```

**Description:** This parameter sets the body content of the MIME part based on the file's content. It is used to replace `data` for setting file data as the content. If `data` is empty, `filePath` must be set. If `data` has a value, `filePath` will not take effect.

**Type:** String

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** The name of the data.

**Type:** String

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var remoteFileName

```cangjie
public var remoteFileName: String
```

**Description:** The name of the file to be saved on the server after upload.

**Type:** String

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### init(String, String, String, HttpData, String)

```cangjie
public init(name: String, contentType: String,  remoteFileName!: String = "",
    data!: HttpData = HttpData.StringData(""), filePath!: String = "")
```

**Description:** Constructs a MultiFormData instance.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name of the data. |
| contentType | String | Yes | - | The data type, such as 'text/plain', 'image/png', 'image/jpeg', 'audio/mpeg', 'video/mp4', etc. |
| remoteFileName | String | No | "" | **Named parameter.** The name of the file to be saved on the server after upload. |
| data | [HttpData](#enum-httpdata) | No | HttpData.StringData("") | **Named parameter.** The content of the form data. |
| filePath | String | No | "" | **Named parameter.** This parameter sets the body content of the MIME part based on the file's content. It is used to replace `data` for setting file data as the content. If `data` is empty, `filePath` must be set. If `data` has a value, `filePath` will not take effect. |

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

**Description:** Performance timing data, measured in milliseconds.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var dnsTiming

```cangjie
public var dnsTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to DNS resolution completion.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var firstReceiveTiming

```cangjie
public var firstReceiveTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to receiving the first byte.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var firstSendTiming

```cangjie
public var firstSendTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to sending the first byte.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var redirectTiming

```cangjie
public var redirectTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to completing all redirect steps.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var responseBodyTiming

```cangjie
public var responseBodyTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to parsing the response body.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var responseHeaderTiming

```cangjie
public var responseHeaderTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to parsing the response header.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var tcpTiming

```cangjie
public var tcpTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to TCP connection completion.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var tlsTiming

```cangjie
public var tlsTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to TLS connection completion.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var totalFinishTiming

```cangjie
public var totalFinishTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) to request completion.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### var totalTiming

```cangjie
public var totalTiming: Float64
```

**Description:** Time taken from the [request](#func-requeststring-httprequestoptions-asynccallbackhttpresponse) callback to the application.

**Type:** Float64

**Read-Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

## enum CertType

```cangjie
public enum CertType {
    | Pem
    | Der
    | P12
    | ...
}
```

**Description:** Certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Der

```cangjie
Der
```

**Description:** DER certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### P12

```cangjie
P12
```

**Description:** P12 certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Pem

```cangjie
Pem
```

**Description:** PEM certificate type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21## enum HttpData

```cangjie
public enum HttpData {
    | StringData(String)
    | ArrayData(Array<Byte>)
    | ...
}
```

**Function:** HTTP data.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### ArrayData(Array\<Byte>)

```cangjie
ArrayData(Array<Byte>)
```

**Function:** Binary array.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### StringData(String)

```cangjie
StringData(String)
```

**Function:** String.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Since:** 21

### ArrayBuffer

```cangjie
ArrayBuffer
```

**Function:** Binary array type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### StringValue

```cangjie
StringValue
```

**Function:** String type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Since:** 21

### Http1_1

```cangjie
Http1_1
```

**Function:** HTTP/1.1 protocol.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Http2

```cangjie
Http2
```

**Function:** HTTP/2 protocol.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Http3

```cangjie
Http3
```

**Function:** HTTP/3 protocol. If the system or server does not support it, lower version HTTP protocols will be used for the request. Only effective for HTTPS URLs; HTTP requests will fail.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### DataReceive

```cangjie
DataReceive
```

**Function:** HTTP streaming response data reception event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### DataReceiveProgress

```cangjie
DataReceiveProgress
```

**Function:** HTTP streaming response data reception progress update event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### DataSendProgress

```cangjie
DataSendProgress
```

**Function:** HTTP network request data transmission progress update event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### HeadersReceive

```cangjie
HeadersReceive
```

**Function:** HTTP Response Header event.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### func !=(HttpRequestEvent)

```cangjie
public operator func !=(other: HttpRequestEvent): Bool
```

**Function:** Compares whether two HttpRequestEvent instances are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | Another HttpRequestEvent instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two HttpRequestEvent instances are not equal, otherwise returns false. |

### func ==(HttpRequestEvent)

```cangjie
public operator func ==(other: HttpRequestEvent): Bool
```

**Function:** Compares whether two HttpRequestEvent instances are equal.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [HttpRequestEvent](#enum-httprequestevent) | Yes | - | Another HttpRequestEvent instance to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two HttpRequestEvent instances are equal, otherwise returns false. |

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Gets the hash value of HttpRequestEvent.

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Returns the hash value of HttpRequestEvent. |

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

**Since:** 21

### Connect

```cangjie
Connect
```

**Function:** HTTP CONNECT request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Delete

```cangjie
Delete
```

**Function:** HTTP DELETE request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Get

```cangjie
Get
```

**Function:** HTTP GET request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Head

```cangjie
Head
```

**Function:** HTTP HEAD request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Options

```cangjie
Options
```

**Function:** HTTP OPTIONS request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Post

```cangjie
Post
```

**Function:** HTTP POST request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Put

```cangjie
Put
```

**Function:** HTTP PUT request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### Trace

```cangjie
Trace
```

**Function:** HTTP TRACE request.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

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

**Since:** 21

### NotUse

```cangjie
NotUse
```

**Function:** Do not use proxy.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### UseDefault

```cangjie
UseDefault
```

**Function:** Use default proxy.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21

### UseSpecified(HttpProxy)

```cangjie
UseSpecified(HttpProxy)
```

**Function:** Use specified proxy type.

**System Capability:** SystemCapability.Communication.NetStack

**Since:** 21## Complete Example

```cangjie
import kit.NetworkKit.*
import ohos.base.*
import std.collection.*

// Each httpRequest corresponds to an HTTP request task and cannot be reused
let httpRequest = createHttp()
// Used to subscribe to HTTP response headers. This interface returns before the request. Can subscribe to this message based on business needs
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
    usingProtocol: HttpProtocol.HTTP1_1, // Optional, protocol type default is automatically specified by the system
    usingProxy: UsingProxy.USE_DEFAULT, // Optional, defaults to no network proxy. Supported since API 10
    caPath: "/path/to/cacert.pem", // Optional, defaults to system preset CA certificates. Supported since API 10
    clientCert: ClientCert(
        "/path/to/client.pem", // Defaults to no client certificate
        "/path/to/client.key", // If the certificate contains Key info, pass an empty string
        certType: CertType.PEM, // Optional, defaults to PEM
        keyPassword: "PASSWORD_TO_KEY" // Optional, password for key file
    ),
    multiFormDataList: [ // Optional, only takes effect when 'content-Type' in Header is 'multipart/form-data'
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

httpRequest.request( // Fill in the URL address for the HTTP request, with or without parameters. URL needs to be customized by developers. Request parameters can be specified in extraData
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