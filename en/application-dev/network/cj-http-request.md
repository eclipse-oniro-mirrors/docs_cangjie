# HTTP Data Request

## Scenario Description

Applications initiate data requests via HTTP, supporting common methods such as GET, POST, OPTIONS, HEAD, PUT, DELETE, TRACE, and CONNECT.

## Interface Description

The HTTP data request functionality is primarily provided by the `http` module.

Using this feature requires the `ohos.permission.INTERNET` permission.  
For permission application, refer to [Declaring Permissions](../security/AccessToken/cj-declare-permissions.md).

The involved interfaces are listed in the table below. For detailed interface descriptions, refer to the [API Documentation](../../../en/application-dev/reference/NetworkKit/cj-apis-net-http.md).

| Interface Name            | Description                                            |
| ------------------------- | ----------------------------------------------------- |
| createHttp()              | Creates an HTTP request.                              |
| request()                 | Initiates an HTTP network request based on a URL.     |
| requestInStream()         | Initiates an HTTP network request and returns a streaming response. |
| destroy()                 | Aborts the request task.                              |
| onHeadersReceive()        | Subscribes to HTTP Response Header events.            |
| offHeadersReceive()       | Unsubscribes from HTTP Response Header events.        |
| onceHeadersReceive()      | Subscribes to HTTP Response Header events but triggers only once. |
| onDataReceive()           | Subscribes to HTTP streaming response data reception events. |
| offDataReceive()          | Unsubscribes from HTTP streaming response data reception events. |
| onDataEnd()               | Subscribes to HTTP streaming response data completion events. |
| offDataEnd()              | Unsubscribes from HTTP streaming response data completion events. |
| onDataReceiveProgress()   | Subscribes to HTTP streaming response data reception progress events. |
| offDataReceiveProgress()  | Unsubscribes from HTTP streaming response data reception progress events. |
| onDataSendProgress()      | Subscribes to HTTP network request data transmission progress events. |
| offDataSendProgress()     | Unsubscribes from HTTP network request data transmission progress events. |

## request Interface Development Steps

1. Import `http` from `kit.NetworkKit`.
2. Call the `createHttp()` method to create an `HttpRequest` object.
3. Call the object's `on()` method to subscribe to HTTP response header events. This interface returns before the `request` call. Subscribe to this event as needed.
4. Call the object's `request()` method, passing the HTTP request URL and optional parameters to initiate the network request.
5. Parse the returned results as needed.
6. Call the object's `off()` method to unsubscribe from HTTP response header events.
7. When the request is no longer needed, call the `destroy()` method to actively release resources.

<!-- compile -->

```cangjie
// Import packages
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import std.collection.*
import ohos.base.*
import ohos.net.http.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

// Each httpRequest corresponds to one HTTP request task and cannot be reused.
let httpRequest = createHttp()

// Request configuration
let option = HttpRequestOptions(
    method: RequestMethod.Post, // Optional, defaults to http.RequestMethod.GET
    // This field is used to pass content for POST requests
    extraData: HttpData.StringData("data to send"),
    expectDataType: HttpDataType.StringValue, // Optional, specifies the return data type
    usingCache: true, // Optional, defaults to true
    priority: 1, // Optional, defaults to 1
    // Add header fields as needed
    header: HashMap<String, String>([("content-type", "application/json")]),
    readTimeout: 60000, // Optional, defaults to 60000ms
    connectTimeout: 60000, // Optional, defaults to 60000ms
    usingProtocol: HttpProtocol.Http1_1, // Optional, protocol type defaults to system-specified
    usingProxy: UsingProxy.UseDefault, // Optional, defaults to no proxy (supported from API 10)
    caPath: "/path/to/cacert.pem", // Optional, defaults to system CA certificates (supported from API 10)
    clientCert: ClientCert(
        "/path/to/client.pem", // Default: no client certificate
        "/path/to/client.key", // If the certificate includes Key info, pass an empty string
        certType: CertType.Pem, // Optional, defaults to PEM
        keyPassword: "passwordToKey" // Optional, password for the key file
    ),
    multiFormDataList: [ // Optional, effective only when 'content-Type' in Header is 'multipart/form-data'
        MultiFormData (
            "Part1", // Data name
            "text/plain", // Data type
            data: StringData("Example data"), // Optional, data content
            remoteFileName: "example.txt" // Optional
        ),
        MultiFormData (
            "Part2", // Data name
            "text/plain", // Data type
            filePath: "/data/app/el2/100/base/com.example.myapplication/haps/entry/files/fileName.txt", // Optional, file path
            remoteFileName: "fileName.txt" // Optional
        )
    ]
)

httpRequest.request(
    // Enter the HTTP request URL, with or without parameters. Customize the URL as needed. Parameters can be specified in extraData.
    "EXAMPLE_URL",
    option,
    {
        err, resp =>
        if (let Some(v) <- err) {
            loggerError("v")
        }
        if (let Some(v) <- resp) {
            // data.result contains the HTTP response content; parse as needed
            loggerInfo("code: ${v.responseCode}")
            // data.header contains the HTTP response headers; parse as needed
            loggerInfo("header: ${v.header}")
            loggerInfo("cookies: ${v.cookies}")
            // Call destroy() to release resources when the request is no longer needed
            httpRequest.destroy()
        }
    })
```

## requestInStream Interface Development Steps

1. Import `http` from `kit.NetworkKit`.
2. Call the `createHttp()` method to create an `HttpRequest` object.
3. Call the object's `on()` method to subscribe to HTTP response header events, streaming data reception events, streaming data progress events, and streaming data completion events as needed.
4. Call the object's `requestInStream()` method, passing the HTTP request URL and optional parameters to initiate the network request.
5. Parse the returned response code as needed.
6. Call the object's `off()` method to unsubscribe from response events.
7. When the request is no longer needed, call the `destroy()` method to actively release resources.

<!-- compile -->

```cangjie
// Import packages
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import kit.NetworkKit.*
import std.collection.*
import ohos.base.*
import ohos.net.http.*

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

class HeadersReceiveCb <: Callback1Argument<HashMap<String, String>> {
    let callback_: (HashMap<String, String>)->Unit
    public init(callback: (HashMap<String, String>)->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException, val: HashMap<String, String>): Unit {
        callback_(val)
    }
}

class DataReceiveCb <: Callback1Argument<Array<Byte>> {
    let callback_: (Array<Byte>)->Unit
    public init(callback: (Array<Byte>)->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException, val: Array<Byte>): Unit {
        callback_(val)
    }
}

class DataEndCb <: Callback0Argument {
    let callback_: ()->Unit
    public init(callback: ()->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException): Unit {
        callback_()
    }
}

class DataReceiveProgressCb <: Callback1Argument<DataReceiveProgressInfo> {
    let callback_: (DataReceiveProgressInfo)->Unit
    public init(callback: (DataReceiveProgressInfo)->Unit) {callback_ = callback}
    public open func invoke(err: ?BusinessException, val: DataReceiveProgressInfo): Unit {
        callback_(val)
    }
}

func test() {
    // Each httpRequest corresponds to one HTTP request task and cannot be reused.
    let httpRequest = createHttp()
    // Subscribe to HTTP response header events
    let headersReceiveCallBack = HeadersReceiveCb({ header => loggerInfo("header: ${header}") })
    httpRequest.on(HttpRequestEvent.HeadersReceive, headersReceiveCallBack)
    // Subscribe to HTTP streaming response data reception events
    let res = ArrayList<Byte>()
    let dataReceiveCallBack = DataReceiveCb({ bytes =>
        res.add(all: bytes)
        loggerInfo("receive length: ${bytes.size}")
    })
    httpRequest.on(HttpRequestEvent.DataReceive, dataReceiveCallBack)

    // Subscribe to HTTP streaming response data completion events
    let dataEndCallBack = DataEndCb({ =>
        loggerInfo("No more data in response, data receive end")
        // Unsubscribe from HTTP response header events
        httpRequest.off(HttpRequestEvent.HeadersReceive)
        // Unsubscribe from HTTP streaming response data reception events
        httpRequest.off(HttpRequestEvent.DataReceive)
        // Unsubscribe from HTTP streaming response data progress events
        httpRequest.off(HttpRequestEvent.DataReceiveProgress)
        // Unsubscribe from HTTP streaming response data completion events
        httpRequest.off(HttpRequestEvent.DataEnd)
        // Call destroy() to release resources when the request is no longer needed
        httpRequest.destroy()
    })
    httpRequest.on(HttpRequestEvent.DataEnd,dataEndCallBack)
    // Subscribe to HTTP streaming response data progress events
    let dataReceiveProgressCallBack = DataReceiveProgressCb({ progress =>
        loggerInfo("dataReceiveProgress receiveSize: ${progress.receiveSize} totalSize: ${progress.totalSize}")
    })
    httpRequest.on(HttpRequestEvent.DataReceiveProgress, dataReceiveProgressCallBack)

    let option = HttpRequestOptions(
        method: RequestMethod.Post, // Optional, defaults to http.RequestMethod.GET
        // This field is used to pass content for POST requests
        extraData: HttpData.StringData("data to send"),
        expectDataType: HttpDataType.StringValue, // Optional, specifies the return data type
        usingCache: true, // Optional, defaults to true
        priority: 1, // Optional, defaults to 1
        // Add header fields as needed
        header: HashMap<String, String>([("content-type", "application/json")]),
        readTimeout: 60000, // Optional, defaults to 60000ms
        connectTimeout: 60000, // Optional, defaults to 60000ms
        usingProtocol: HttpProtocol.Http1_1, // Optional, protocol type defaults to system-specified
        usingProxy: UsingProxy.UseDefault, // Optional, defaults to no proxy (supported from API 10)
        caPath: "/path/to/cacert.pem", // Optional, defaults to system CA certificates (supported from API 10)
        clientCert: ClientCert(
            "/path/to/client.pem", // Default: no client certificate
            "/path/to/client.key", // If the certificate includes Key info, pass an empty string
            certType: CertType.Pem, // Optional, defaults to PEM
            keyPassword: "passwordToKey" // Optional, password for the key file
        ),
        multiFormDataList: [ // Optional, effective only when 'content-Type' in Header is 'multipart/form-data'
            MultiFormData (
                "Part1", // Data name
                "text/plain", // Data type
                data: StringData("Example data"), // Optional, data content
                remoteFileName: "example.txt" // Optional
            ),
            MultiFormData (
                "Part2", // Data name
                "text/plain", // Data type
                filePath: "/data/app/el2/100/base/com.example.myapplication/haps/entry/files/fileName.txt", // Optional, file path
                remoteFileName: "fileName.txt" // Optional
            )
        ]
    )

    // Enter the HTTP request URL, with or without parameters. Customize the URL as needed. Parameters can be specified in extraData.

    httpRequest.requestInStream(
        "EXAMPLE_URL",
        option,
        {err, code =>
        if (let Some(e) <- err) {
            loggerError("exception: ${e.message}")
        }
        if (let Some(respCode) <- code) {
            loggerInfo("ResponseCode: ${respCode}")
        } else {
            loggerError("response is none")
        }
    })
}
```

## Certificate Pinning

Certificate pinning can be implemented by preloading application-level certificates or preloading public key hashes of certificates. This ensures that only developer-specified certificates can establish HTTPS connections.

Both methods are configured in a configuration file located at: `src/main/resources/base/profile/network_config.json`. This configuration establishes mappings between preloaded certificates and network servers.

If the server's domain certificate is unknown, you can obtain it using the following command (replace `www.example.com` with the target domain and `www.example.com.pem` with the desired certificate filename):

```shell
openssl s_client -servername www.example.com -connect www.example.com:443 \
    < /dev/null | sed -n "/-----BEGIN/,/-----END/p" > www.example.com.pem
```

For Windows users:
- Replace `/dev/null` with `NUL`.
- OpenSSL behavior may differ; press Enter to exit if it waits for input.
- If `sed` is unavailable, manually copy the content between `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` (including these lines).

### Preloading Application-Level Certificates

Directly preload certificate files in the app. Currently supports `.crt` and `.pem` formats.

> **Note:**
>
> Current certificate pinning in `ohos.net.http` and Image components matches hashes of all certificates in the chain. If any server certificate is updated, validation will fail. If server certificates are updated, the app version should be updated accordingly, and users should upgrade promptly to avoid connectivity issues.

### Preloading Certificate Public Key Hashes

Specify domain certificate public key hashes in the configuration to allow only matching certificates for domain access.

Calculate the public key hash using the following commands (assuming the certificate is saved as `www.example.com.pem`):

```shell
# Extract public key from certificate
openssl x509 -in www.example.com.pem -pubkey -noout > www.example.com.pubkey.pem
# Convert PEM public key to DER format
openssl asn1parse -noout -inform pem -in www.example.com.pubkey.pem -out www.example.com.pubkey.der
# Compute SHA256 of the public key and encode in base64
openssl dgst -sha256 -binary www.example.com.pubkey.der | openssl base64
```

### JSON Configuration Examples

Example for preloading application-level certificates:

```json
{
  "network-security-config": {
    "base-config": {
      "trust-anchors": [
        {
          "certificates": "/etc/security/certificates"
        }
      ]
    },
    "domain-config": [
      {
        "domains": [
          {
            "include-subdomains": true,
            "name": "example.com"
          }
        ],
        "trust-anchors": [
          {
            "certificates": "/data/storage/el1/bundle/entry/resources/resfile"
          }
        ]
      }
    ]
  }
}
```

Example for preloading certificate public key hashes:

```json
{
  "network-security-config": {
    "domain-config": [
      {
        "domains": [
          {
            "include-subdomains": true,
            "name": "server.com"
          }
        ],
        "pin-set": {
          "expiration": "2024-11-08",
          "pin": [
            {
              "digest-algorithm": "sha256",
              "digest": "FEDCBA987654321"
            }
          ]
        }
      }
    ]
  }
}
```

**Field Descriptions:**

| Field                    | Type    | Description                                                                                                                         |
| ------------------------ | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| network-security-config  | object  | Network security configuration. May contain 0 or 1 `base-config` and must contain 1 `domain-config`.                                |
| base-config              | object  | Indicates application-wide security configuration. Must contain 1 `trust-anchors`.                                                 |
| domain-config            | array   | Indicates domain-specific security configurations. May contain any number of items. Each item must contain 1 `domains` and may contain 0 or 1 `trust-anchors` or `pin-set`. |
| trust-anchors            | array   | Trusted CAs. May contain any number of items. Each item must contain 1 `certificates`.                                             |
| certificates             | string  | Path to CA certificates.                                                                                                           |
| domains                  | array   | Domains. May contain any number of items. Each item must contain 1 `name` (string: domain name) and may contain 0 or 1 `include-subdomains`. |
| include-subdomains       | boolean | Indicates whether the rule applies to subdomains.                                                                                  |
| pin-set                  | object  | Certificate public key hash settings. Must contain 1 `pin` and may contain 0 or 1 `expiration`.                                    |
| expiration               | string  | Indicates the expiration date of the public key hash.                                                                              |
| pin                      | array   | Certificate public key hashes. May contain any number of items. Each item must contain 1 `digest-algorithm` and 1 `digest`.        |
| digest-algorithm         | string  | Indicates the digest algorithm used to generate the hash. Currently only `sha256` is supported.                                    |
| digest                   | string  | Indicates the public key hash.                                                                                                     |