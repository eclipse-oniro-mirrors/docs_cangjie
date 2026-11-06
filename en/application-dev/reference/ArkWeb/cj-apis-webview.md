# ohos.web.webview

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides web control capabilities, enabling components to display web pages.

## Import Module

```cangjie
import kit.ArkWeb.*
```

## Permission List

ohos.permission.APPROXIMATELY_LOCATION

ohos.permission.LOCATION

ohos.permission.LOCATION_IN_BACKGROUND

ohos.permission.INTERNET

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, refer to [Interface Usage Instructions](../cj-development-intro.md#接口使用说明).

## func once(String, Callback\<Unit>)

```cangjie
public func once(eventType: String, callback: Callback<Unit>): Unit
```

**Function:** Registers a one-time callback for web events of the specified type. Currently, only **webInited** is supported. This callback is triggered when the Web engine initialization is complete.

When the first **Web** component is loaded in an app, the Web engine is initialized, and the once() callback is not triggered when other **Web** components are subsequently loaded in the same app. When the app destroys the last **Web** component, if the first **Web** component is loaded again, the app re-enters the Web engine initialization process.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| eventType | String | Yes | - | Type of the Web event. Currently, only **webInited** (Web engine initialization complete) is supported. |
| callback | [Callback\<Unit>](../arkinterop/cj-api-callback_invoke.md#type-callbackt) | Yes | - | Callback invoked when the Web engine initialization is complete. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

once("webInited") {
    _ =>
        Hilog.info(0, "test", "webInited")
}
```

## class BackForwardList

```cangjie
public class BackForwardList {}
```

**Description:** The history information list of the current Webview.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### prop currentIndex

```cangjie
public prop currentIndex: Int32
```

**Description:** The index of the current page in the history list.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### prop size

```cangjie
public prop size: Int32
```

**Description:** The number of indices in the history list, with a maximum of 50 entries. When exceeded, the initial records will be overwritten.

**Type:** Int32

**Access:** Read-only

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### func getItemAtIndex(Int32)

```cangjie
public func getItemAtIndex(index: Int32): HistoryItem
```

**Description:** Retrieves the history item information at the specified index in the history list.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int32 | Yes | - | The specified index in the history list. |

**Return Value:**

| Type | Description |
|:----|:----|
| [HistoryItem](#class-historyitem) | The history item. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Invalid input parameter. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import ohos.arkui.component.button.Button
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class webview_0 {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getItemAtIndex")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getItemAtIndex")
                let backForwardList = webController.getBackForwardEntries()
                let historyItem = backForwardList.getItemAtIndex(backForwardList.currentIndex)
                Hilog.info(0, "cangjieTest", "Current historyUrl is ${historyItem.historyUrl}.")
                Hilog.info(0, "cangjieTest", "Current historyRawUrl is ${historyItem.historyRawUrl}.")
                Hilog.info(0, "cangjieTest", "Current title is ${historyItem.title}.")
                let pixelMap = historyItem.icon
                let byteInfo = pixelMap?.getPixelBytesNumber() ?? 0
                Hilog.info(0, "cangjieTest", "icon byteInfo is ${byteInfo}")
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

## class HistoryItem

```cangjie
public class HistoryItem {
    public var icon: PixelMap
    public var historyUrl: String
    public var historyRawUrl: String
    public var title: String
}
```

**Description:** Page history item.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var historyRawUrl

```cangjie
public var historyRawUrl: String
```

**Description:** The original URL address of the history item.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var historyUrl

```cangjie
public var historyUrl: String
```

**Description:** The URL address of the history item.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var title

```cangjie
public var title: String
```

**Description:** The title of the history item.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var icon

```cangjie
public var icon: ?PixelMap
```

**Description:** The PixelMap object of the history page icon.

**Type:** [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

## class HitTestValue

```cangjie
public class HitTestValue {
    public var hitTestType: WebHitTestType
    public var extra: String
}
```

**Description:** Provides information about the clicked element. For sample code, refer to [getHitTestValue](#func-gethittestvalue).

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var extra

```cangjie
public var extra: String
```

**Description:** Additional parameter information of the clicked area. If the clicked area is an image or link, the additional parameter information is its URL address.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var hitTestType

```cangjie
public var hitTestType: WebHitTestType
```

**Description:** The element type of the currently clicked area.

**Type:** [WebHitTestType](#enum-webhittesttype)

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

## class JsMessageExt

```cangjie
public class JsMessageExt {}
```

**Description:** Data encapsulation class of the execution result of the runJavaScriptExt API. Unlike conventional script execution APIs that only support string results, runJavaScriptExt supports richer return value types, and JsMessageExt provides a type-safe way to obtain these results.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### func getString()

```cangjie
public func getString(): String
```

**Function:** Obtains string-type data of the data object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String-type data obtained after the runJavaScriptExt API executes the script. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100014 | The type and value of the message do not match. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getString").onClick(
                {
                    evt =>
                        try {
                            webController.runJavaScriptExt(ScriptValueType.StringValue("test()"), { err, result =>
                                if (let Some(e) <- err) {
                                    Hilog.info(0, "test", "runJavaScriptExt failed: ${e.message}")
                                } else {
                                    let str = result?.getString() ?? ""
                                    Hilog.info(0, "test", "getString result: ${str}")
                                }
                            })
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "runJavaScriptExt failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

## class WebCookieManager

```cangjie
public class WebCookieManager {}
```

**Description:** Through WebCookie, various behaviors of cookies in Web components can be controlled. All Web components in an application share one WebCookieManager instance.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### static func clearAllCookies(Bool)

```cangjie
public static func clearAllCookies(incognito!: Bool = false): Unit
```

**Description:** Clears all cookies.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| incognito | Bool | No | false | **Named parameter.** true indicates clearing all memory cookies of the Webview in incognito mode, false indicates clearing all cookies in normal non-incognito mode. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Cookies are obtained from the web session, such as from the request of an HTTP request. In this example, the obtained cookie is assumed to be "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie
    let cookie = "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie for the specified URL
    WebCookieManager.configCookie("https://www.example.com", cookie, incognito: false)
    // ... 
    // Perform business logic here, such as loading a web page with cookies.
    // After execution, clear the cookies
    WebCookieManager.clearAllCookies()
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "ErrorCode: ${e.code}, ErrorMessage: ${e.message}")
}
```

### static func clearSessionCookie()

```cangjie
public static func clearSessionCookie(): Unit
```

**Description:** Clears all session cookies.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Cookies are obtained from the web session, such as from the request of an HTTP request. In this example, the obtained cookie is assumed to be "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie
    let cookie = "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie for the specified URL
    WebCookieManager.configCookie("https://www.example.com", cookie, incognito: false)
    // ... 
    // Perform business logic here, such as loading a web page with cookies.
    // After execution, clear the cookies
    WebCookieManager.clearSessionCookie()
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "ErrorCode: ${e.code}, ErrorMessage: ${e.message}")
}
```

### static func configCookie(String, String, Bool)

```cangjie
public static func configCookie(url: String, value: String, incognito!: Bool = false): Unit
```

**Description:** Sets the cookie value for the specified URL.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL to which the cookie belongs. It is recommended to use the complete URL. |
| value | String | Yes | - | The value of the cookie to be set. |
| incognito | Bool | No | false | true indicates setting cookies for the corresponding URL in incognito mode, false indicates setting cookies for the corresponding URL in normal non-incognito mode. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100002 | Invalid url. |
  | 17100005 | Invalid cookie value. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // Cookies are obtained from the web session, such as from the request of an HTTP request. In this example, the obtained cookie is assumed to be "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie
    let cookie = "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie for the specified URL
    WebCookieManager.configCookie("https://www.example.com", cookie, incognito: false)
    // ... 
    // Perform business logic here, such as loading a web page with cookies.
    // After execution, clear the cookies
    WebCookieManager.clearSessionCookie()
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "ErrorCode: ${e.code}, ErrorMessage: ${e.message}")
}
```

### static func existCookie(Bool)

```cangjie
public static func existCookie(incognito!: Bool = false): Bool
```

**Description:** Checks whether cookies exist in the WebCookieManager.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| incognito | Bool | No | false | **Named parameter.** true indicates checking for cookies in incognito mode, false indicates checking for cookies in normal non-incognito mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true indicates cookies exist, false indicates no cookies exist. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

let result = WebCookieManager.existCookie()
Hilog.info(0, "AppLogCj", "WebCookiemanager result: ${result}")
```

### static func fetchCookie(String, Bool)

```cangjie
public static func fetchCookie(url: String, incognito!: Bool = false): String
```

**Description:** Retrieves the cookie value for the specified URL.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL to which the cookie belongs. It is recommended to use the complete URL. |
| incognito | Bool | No | false | **Named parameter.** true indicates retrieving memory cookies of the Webview in incognito mode, false indicates retrieving cookies in normal non-incognito mode. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | The cookie value corresponding to the specified URL. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100002 | Invalid url. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

try {
    // The cookie to be set, where the format is name=value. In this example, the name is ZFY and the value is 4Mvfh8V4iYFnDc8CGowMa3KE4m0dV
    let cookie = "ZFY=4Mvfh8V4iYFnDc8CGowMa3KE4m0dV"
    // Set the cookie for the specified URL
    WebCookieManager.configCookie("https://www.example.com", cookie, incognito: false)
    // After setting, retrieve the cookie for the specified URL
    let value = WebCookieManager.fetchCookie("https://www.example.com")
    Hilog.info(0, "AppLogCj",  "WebCookieManager,fetchCookie cookie = ${value}", "")
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "ErrorCode: ${e.code}, ErrorMessage: ${e.message}", "")
}
```

### static func isCookieAllowed()

```cangjie
public static func isCookieAllowed(): Bool
```

**Description:** Checks whether the WebCookieManager instance has permission to send and receive cookies.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether permission to send and receive cookies is granted. true indicates permission is granted, false indicates permission is not granted. The default is true. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

let result = WebCookieManager.isCookieAllowed()
Hilog.info(0, "AppLogCj",  "WebCookieManager, result: ${result}")
```

### static func isThirdPartyCookieAllowed()

```cangjie
public static func isThirdPartyCookieAllowed(): Bool
```

**Description:** Checks whether the WebCookieManager instance has permission to send and receive third-party cookies.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether permission to send and receive third-party cookies is granted. true indicates permission is granted, false indicates permission is not granted. The default is false. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

let result = WebCookieManager.isThirdPartyCookieAllowed()
Hilog.info(0, "AppLogCj",  "WebCookieManager, result: ${result}")
```

### static func saveCookieAsync(AsyncCallback\<Unit>)

```cangjie
public static func saveCookieAsync(callback: AsyncCallback<Unit>): Unit
```

**Function:** Asynchronously saves all cookies (that can be obtained through fetchCookie and need to be persisted) to the disk.

> **Note:**
>
> saveCookieAsync is used to forcibly write cookies that need to be persisted to the disk. Session cookies are not persisted on PC/2-in-1 and tablet devices. Even if saveCookieAsync is called, session cookies are not written to the disk.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<Unit> | Yes | - | Callback used to indicate whether the cookies are saved. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

WebCookieManager.saveCookieAsync({ err, _ =>
    if (let Some(e) <- err) {
        Hilog.info(0, "test", "saveCookieAsync failed: ${e.message}")
    } else {
        Hilog.info(0, "test", "saveCookieAsync success")
    }
})
```

### static func putAcceptCookieEnabled(Bool)

```cangjie
public static func putAcceptCookieEnabled(accept: Bool): Unit
```

**Description:** Sets whether the WebCookieManager instance has permission to send and receive cookies.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| accept | Bool | Yes | - | Sets whether permission to send and receive cookies is granted. The default is true, indicating permission is granted. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

WebCookieManager.putAcceptCookieEnabled(false)
```

### static func putAcceptThirdPartyCookieEnabled(Bool)

## class WebCustomScheme

```cangjie
public class WebCustomScheme {}
```

**Description:** Configuration options of a custom protocol, used by customizeSchemes.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### prop isCodeCacheSupported

```cangjie
public mut prop isCodeCacheSupported: ?Bool
```

**Description:** Whether JavaScript resources of the custom protocol with this option set support code cache generation. The value **true** means that code cache generation is supported, and **false** means the opposite.

Default value: **false**.

**Type:** ?Bool

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### prop isSupportCORS

```cangjie
public mut prop isSupportCORS: Bool
```

**Description:** Whether to support cross-origin resource sharing (CORS). The value **true** means to support cross-origin resource sharing (CORS), and **false** means the opposite.

Default value: **true**.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### prop isSupportFetch

```cangjie
public mut prop isSupportFetch: Bool
```

**Description:** Whether to support fetch requests. The value **true** means to support fetch requests, and **false** means the opposite.

Default value: **true**.

**Type:** Bool

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### prop schemeName

```cangjie
public mut prop schemeName: String
```

**Description:** Custom protocol name. The maximum length is 32, and only lowercase letters, digits, '.', '+', and '-' are supported. It must start with a letter. If the preceding restrictions are not met, the custom protocol configuration does not take effect.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### init(String, Bool, Bool)

```cangjie
public init(schemeName: String, isSupportCORS: Bool, isSupportFetch: Bool)
```

**Description:** Creates a WebCustomScheme object and initializes it with the specified protocol name.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| schemeName | String | Yes | - | Custom protocol name. |
| isSupportCORS | Bool | Yes | - | Whether to support cross-origin resource sharing (CORS). The value **true** means to support cross-origin resource sharing (CORS), and **false** means the opposite. |
| isSupportFetch | Bool | Yes | - | Whether to support fetch requests. The value **true** means to support fetch requests, and **false** means the opposite. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

let scheme = WebCustomScheme("myScheme", true, false)
scheme.isCodeCacheSupported = true
Hilog.info(0, "test", "schemeName: ${scheme.schemeName}")
```

## class WebHeader

```cangjie
public class WebHeader {
    public var headerKey: String
    public var headerValue: String
    public init(headerKey: String, headerValue: String)
}
```

**Description:** Request/response header object returned by web components.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var headerKey

```cangjie
public var headerKey: String
```

**Description:** The key of request/response header.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### var headerValue

```cangjie
public var headerValue: String
```

**Description:** The value of request/response header.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### init(String, String)

```cangjie
public init(headerKey: String, headerValue: String)
```

**Description:** Constructor for WebHeader.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| headerKey | String | Yes | - | The key of request/response header. |
| headerValue | String | Yes | - | The value of request/response header. |

## class WebStorage

```cangjie
public class WebStorage {}
```

**Description:** Provides the capability of managing the Web SQL database and HTML5 Web Storage APIs. All **Web** components in an app share one WebStorage object.

> **Note:**
>
> You must load the **Web** component before calling the APIs in **WebStorage**.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### static func deleteAllData(?Bool)

```cangjie
public static func deleteAllData(incognito!: ?Bool = false): Unit
```

**Function:** Deletes all storage data used by JavaScript storage APIs, including the Web SQL Database and HTML5-supported Web storage APIs.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| incognito | ?Bool | No | false | **Named parameter.** Whether to delete all data in the Web SQL Database in incognito mode. The value **true** means to delete all data in the Web SQL Database in incognito mode, and **false** means the opposite. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("deleteAllData").onClick(
                {
                    evt =>
                        WebStorage.deleteAllData()
                        Hilog.info(0, "test", "deleteAllData done")
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

## class WebviewController

```cangjie
public class WebviewController {
    public init(webTag!: ?String = None)
}
```

**Description:** Clears the IP address owned by the primary name.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### init(?String)

```cangjie
public init(webTag!: ?String = None)
```

**Description:** Creates a WebviewController object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| webTag | ?String | No | None | Specifies the name of the web component. |

### static func setWebDebuggingAccess(Bool)

```cangjie
public static func setWebDebuggingAccess(webDebuggingAccess: Bool): Unit
```

**Description:** Sets whether to enable web page debugging functionality.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| webDebuggingAccess | Bool | Yes | - | Sets whether to enable web page debugging functionality. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Invalid input parameter. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("setWebDebuggingAccess")
            .onClick {
                evt =>
                Hilog.info(0, "AppLogCj", "setWebDebuggingAccess")
                WebviewController.setWebDebuggingAccess(true)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "AppLogCj", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "AppLogCj", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func accessBackward()

```cangjie
public func accessBackward(): Bool
```

**Function:** Checks whether the current page can go back, i.e., whether there is a back history for the current page.

You can use [getBackForwardEntries](#func-getbackforwardentries) to obtain the historical information list of the current WebView and use [accessStep](#func-accessstepint32) to determine whether to move forward or backward based on the specified number of steps.

> **Note:**
>
> If setCustomUserAgent is called when the **Web** component is loaded for the first time, the value of **accessBackward** may be **false** when there are multiple historical entries. That is, there is no backward entry. You are advised to call the **setCustomUserAgent** method to set a user agent before using **loadUrl** to load a specific page.
>
> Causes: When the **Web** component is loaded for the first time, calling setCustomUserAgent causes the component to reload and retain the initial history entry. Then the new entry replaces the initial history entry and no new history entry is generated. As a result, the value of **accessBackward** is false.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the current page can go back, and **false** otherwise. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("accessBackward").onClick(
                {
                    evt =>
                        try {
                            let canBackward = webController.accessBackward()
                            Hilog.info(0, "test", "accessBackward: ${canBackward}")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "accessBackward failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func accessForward()

```cangjie
public func accessForward(): Bool
```

**Function:** Checks whether the current page can go forward, i.e., whether there is a forward history for the current page.

You can use [getBackForwardEntries](#func-getbackforwardentries) to obtain the historical information list of the current WebView and use [accessStep](#func-accessstepint32) to determine whether to move forward or backward based on the specified number of steps.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the current page can go forward, and **false** otherwise. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("accessBackward").onClick(
                {
                    evt =>
                        try {
                            let canForward = webController.accessForward()
                            Hilog.info(0, "test", "accessForward: ${canForward}")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "accessForward failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func accessStep(Int32)

```cangjie
public func accessStep(step: Int32): Bool
```

**Description:** Checks whether the current page can go forward or backward by the specified number of steps.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| step | Int32 | Yes | - | The number of steps to jump, positive for forward, negative for backward. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the page can go forward or backward. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import ohos.arkui.component.button.Button
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class EntryView {
    var message: String = "Hello World"
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("accessStep")
             Text(this.message).onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "accessStep")
                let access = webController.accessStep(2)
                Hilog.info(0, "cangjieTest", "accessStep returns: ${access}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func backOrForward(Int32)

```cangjie
public func backOrForward(step: Int32): Unit
```

**Description:** Navigates forward or backward by the specified number of steps in the history stack. If no corresponding step exists in the history stack, no navigation occurs.

When navigating forward or backward, the already loaded web page is used directly without reloading.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| step | Int32 | Yes | - | The number of steps to navigate forward or backward. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import ohos.arkui.component.button.Button
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("backOrForward")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "backOrForward")
                webController.backOrForward(-2)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func backward()

```cangjie
public func backward(): Unit
```

**Description:** Navigates backward by one page in the history stack. Typically used in conjunction with accessBackward.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("backward")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "backward")
                webController.backward()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```### func clearHistory()

```cangjie
public func clearHistory(): Unit
```

**Function:** Deletes all forward and backward navigation history.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("clearHistory")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "clearHistory")
                webController.clearHistory()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### static func customizeSchemes(Array\<WebCustomScheme>)

```cangjie
public static func customizeSchemes(schemes: Array<WebCustomScheme>): Unit
```

**Function:** Grants the cross-origin request and fetch request permissions for custom protocols to the web kernel. When the Web performs a cross-origin fetch of a custom protocol, the fetch request can be intercepted by the onInterceptRequest event, so that developers can further process the request. It is recommended to call this API before any **Web** component is initialized.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| schemes | Array\<[WebCustomScheme](#class-webcustomscheme)> | Yes | - | Array of up to 10 custom schemes. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100020 | Failed to register custom schemes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    
    protected override func aboutToAppear() {
        try {
            let scheme = WebCustomScheme("schemeName", true, true)
            scheme.isCodeCacheSupported = true
            WebviewController.customizeSchemes([scheme])
            Hilog.info(0, "test", "customizeSchemes done")
        } catch (e: BusinessException) {
            Hilog.info(0, "test", "customizeSchemes failed: ${e.message}")
        }
    }
    
    func build() {
        Column(space: 10) {
            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func deleteJavaScriptRegister(String)

```cangjie
public func deleteJavaScriptRegister(name: String): Unit
```

**Function:** Deletes the specified JavaScript object registered through registerJavaScriptProxy or javaScriptProxy. The deletion takes effect after the page is reloaded.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the registered JavaScript object, which is the same as the object name invoked in the window. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100008 | Failed to delete JavaScriptProxy because it does not exist. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("deleteJavaScriptRegister").onClick(
                {
                    evt =>
                        try {
                            webController.deleteJavaScriptRegister("objName")
                            Hilog.info(0, "test", "deleteJavaScriptRegister done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "deleteJavaScriptRegister failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func enableSafeBrowsing(Bool)

```cangjie
public func enableSafeBrowsing(enable: Bool): Unit
```

**Function:** Enables the website security risk check feature. Illegal and fraudulent websites are forcibly enabled and cannot be disabled via this function.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| enable | Bool | Yes | - | Whether to enable the website security risk check feature. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("enableSafeBrowsing")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "enableSafeBrowsing")
                webController.enenableSafeBrowsing(true)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func forward()

```cangjie
public func forward(): Unit
```

**Function:** Navigates forward one page in the history stack.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("forward")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "forward")
                webController.forward()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getBackForwardEntries()

```cangjie
public func getBackForwardEntries(): BackForwardList
```

**Function:** Retrieves the current Webview's history information list.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [BackForwardList](#class-backforwardlist) | The current Webview's history information list. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getBackForwardEntries")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getBackForwardEntries")
                let backForwardList = webController.getBackForwardEntries()
                Hilog.info(0, "cangjieTest", "backForwardList currentIndex is ${backForwardList.currentIndex}")
                Hilog.info(0, "cangjieTest", "backForwardList size is ${backForwardList.size}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getCustomUserAgent()

```cangjie
public func getCustomUserAgent(): String
```

**Function:** Retrieves the custom user agent.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | The custom user agent information. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("getCustomUserAgent")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getCustomUserAgent")
                let agent = webController.getCustomUserAgent()
                Hilog.info(0, "cangjieTest", "getCustomUserAgent returns ${agent}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getHitTest()

```cangjie
public func getHitTest(): WebHitTestType
```

**Function:** Retrieves the element type of the currently clicked area.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [WebHitTestType](#enum-webhittesttype) | The element type of the clicked area. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getHitTest")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getHitTest")
                let hitType = webController.getHitTest()
                match(hitType) {
                    case WebHitTestType.EditText => Hilog.info(0, "cangjieTest", "getHitTest returns EditText")
                    case WebHitTestType.Email => Hilog.info(0, "cangjieTest", "getHitTest returns Email")
                    case WebHitTestType.Unknown => Hilog.info(0, "cangjieTest", "getHitTest returns Unknown")
                    case _ =>  ()
                }
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getHitTestValue()

```cangjie
public func getHitTestValue(): HitTestValue
```

**Function:** Retrieves the element information of the currently clicked area.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [HitTestValue](#class-hittestvalue) | The element information of the clicked area. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getHitTestValue")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getHitTestValue")
                let hitTestValue = webController.getHitTestValue()
                match(hitTestValue.hitTestType) {
                    case WebHitTestType.EditText => Hilog.info(0, "cangjieTest", "getHitTestValue returns EditText")
                    case WebHitTestType.Email => Hilog.info(0, "cangjieTest", "getHitTestValue returns Email")
                    case WebHitTestType.Unknown => Hilog.info(0, "cangjieTest", "getHitTestValue returns Unknown")
                    case _ =>  ()
                 }
                Hilog.info(0, "cangjieTest", "getHitTestValue extra returns ${hitTestValue.extra}")
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```### func getOriginalUrl()

```cangjie
public func getOriginalUrl(): String
```

**Function:** Gets the original URL of the current page.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type   | Description                  |
|:-------|:-----------------------------|
| String | The original URL of the current page. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getOriginalUrl")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getOriginalUrl")
                let url = webController.getOriginalUrl()
                Hilog.info(0, "cangjieTest", "getOriginalUrl is ${url}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getPageHeight()

```cangjie
public func getPageHeight(): Int32
```

**Function:** Gets the height of the current webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type  | Description                  |
|:------|:-----------------------------|
| Int32 | The height of the current webpage. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getOriginalUrl")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getOriginalUrl")
                let height = webController.getPageHeight()
            }.width(400.px).height(150.px)
        }
    }
}
```

### func getSecurityLevel()

```cangjie
public func getSecurityLevel(): SecurityLevel
```

**Function:** Gets the security level of the current webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type                     | Description                                                                 |
|:-------------------------|:----------------------------------------------------------------------------|
| [SecurityLevel](#enum-securitylevel) | The security level of the current webpage. Possible values: NONE, SECURE, WARNING, DANGEROUS. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getSecurityLevel")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getSecurityLevel")
                let securityLevel = webController.getSecurityLevel()
                match(securityLevel) {
                    case SecurityLevel.NoneLevel => Hilog.info(0, "cangjieTest", "getSecurityLevel returns NONE")
                    case SecurityLevel.Secure => Hilog.info(0, "cangjieTest", "getSecurityLevel returns SECURE")
                    case SecurityLevel.Warning => Hilog.info(0, "cangjieTest", "getSecurityLevel returns WARNING")
                    case SecurityLevel.Danger => Hilog.info(0, "cangjieTest", "getSecurityLevel returns DANGEROUS")
                    case _ => throw IllegalArgumentException("The type is not supported.")
                 }
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getTitle()

```cangjie
public func getTitle(): String
```

**Function:** Gets the title of the current webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type   | Description                  |
|:-------|:-----------------------------|
| String | The title of the current webpage. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getTitle")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getTitle")
                let title = webController.getTitle()
                Hilog.info(0, "cangjieTest", "getTitle returns ${title}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getUrl()

```cangjie
public func getUrl(): String
```

**Function:** Gets the URL of the current page.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type   | Description                  |
|:-------|:-----------------------------|
| String | The URL of the current page. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("getUrl")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getUrl")
                let url = webController.getUrl()
                Hilog.info(0, "cangjieTest", "getUrl is ${url}")
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getUserAgent()

```cangjie
public func getUserAgent(): String
```

**Function:** Gets the default user agent.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type   | Description                  |
|:-------|:-----------------------------|
| String | The default user agent. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("getUserAgent")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "getUserAgent")
                webController.getUserAgent()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func getWebId()

```cangjie
public func getWebId(): Int32
```

**Function:** Obtains the index value of the **Web** component, which can be used for managing multiple **Web** components.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Index value of the **Web** component. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("getWebId").onClick(
                {
                    evt =>
                        try {
                            let webId = webController.getWebId()
                            Hilog.info(0, "test", "getWebId: ${webId}")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "getWebId failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### static func initializeWebEngine()

```cangjie
public static func initializeWebEngine(): Unit
```

**Function:** Initializes the Web engine in advance, loading the dynamic library of the Web engine and automatically preconnecting to frequently visited websites in history to improve startup performance.

> **Note:**
>
> initializeWebEngine cannot be called in an asynchronous thread. Otherwise, the system breaks down.
>
> initializeWebEngine takes effect globally and needs to be called only once in an application lifecycle.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

// It is recommended that this API be called during app startup and before any Web component is created.
WebviewController.initializeWebEngine()
Hilog.info(0, "test", "initializeWebEngine done")
```

### func isIncognitoMode()

```cangjie
public func isIncognitoMode(): Bool
```

**Function:** Checks whether the current Webview is in incognito mode.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description                          |
|:-----|:-------------------------------------|
| Bool | Returns whether the Webview is in incognito mode. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :----------- | :------------ |
  | 17100001     | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("isIncognitoMode")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "isIncognitoMode")
                let bool = webController.isIncognitoMode()
                Hilog.info(0, "cangjieTest", "isIncognitoMode returns ${bool}")
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```### func isSafeBrowsingEnabled()

```cangjie
public func isSafeBrowsingEnabled(): Bool
```

**Function:** Checks whether the current webpage has enabled website security risk detection.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Whether the current webpage has enabled website security risk detection. Default is false.|

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("isSafeBrowsingEnabled")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "isSafeBrowsingEnabled")
                let bool = webController.isSafeBrowsingEnabled()
                Hilog.info(0, "cangjieTest", "isSafeBrowsingEnabled returns ${bool}")
            }.width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func onActive()

```cangjie
public func onActive(): Unit
```

**Function:** Notifies the **Web** component that it enters the active state. The application can interact with the user while in the active foreground state, and it remains in this state until the focus is moved away from it due to some event (for example, an incoming call is received or the device screen is turned off).

If the page was previously in the inactive state, the event listener registered through document.addEventListener('visibilitychange',...) in the H5 page will be triggered, and document.visibilityState changes from "hidden" to "visible".

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("onActive").onClick(
                {
                    evt =>
                        try {
                            webController.onActive()
                            Hilog.info(0, "test", "onActive done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "onActive failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)
            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func onInactive()

```cangjie
public func onInactive(): Unit
```

**Function:** Notifies the **Web** component that it enters the inactive state. You can implement the behavior to perform after the application loses focus.

When this API is called, any content that can be safely paused, such as animations and geographical locations, is paused as much as possible. However, the JavaScript is not paused. To pause the JavaScript globally, use pauseAllTimers. To reactivate the **Web** component, use onActive.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("onInactive").onClick(
                {
                    evt =>
                        try {
                            webController.onInactive()
                            Hilog.info(0, "test", "onInactive done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "onInactive failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func pageDown(Bool)

```cangjie
public func pageDown(bottom: Bool): Unit
```

**Function:** Scrolls the Webview content down by half a viewport size or jumps to the bottom of the page, controlled by the `bottom` parameter.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|bottom|Bool|Yes|-|Whether to jump to the bottom of the page. If set to false, scrolls the content down by half a viewport size. If set to true, jumps to the bottom of the page.|

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component.relation pageDown(bottom: boolean): void |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("pageDown")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "pageDown")
                webController.pageDown(true)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func pageUp(Bool)

```cangjie
public func pageUp(top: Bool): Unit
```

**Function:** Scrolls the Webview content up by half a viewport size or jumps to the top of the page, controlled by the `top` parameter.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|top|Bool|Yes|-|Whether to jump to the top of the page. If set to false, scrolls the content up by half a viewport size. If set to true, jumps to the top of the page.|

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component.relation pageUp(top: boolean): void |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("pageUp")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "pageUp")
                webController.pageUp(true)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func refresh()

```cangjie
public func refresh(): Unit
```

**Function:** Notifies the Web component to refresh the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.*
import ohos.arkui.component.button.Button

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("refresh")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "refresh")
                webController.refresh()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                Hilog.info(0, "cangjieTest", "page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                Hilog.info(0, "cangjieTest", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func registerJavaScriptProxy(Array\<(String) -> String>, String, Array\<String>)

```cangjie
public func registerJavaScriptProxy(funcs: Array<(String) -> String>, name: String, methodList: Array<String>): Unit
```

**Function:** Injects Cangjie methods into the Window object for invocation within the window context. Requires calling the [refresh](#func-refresh) interface to take effect after registration.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|funcs|Array\<(String)->String>|Yes|-|Array of application-side Cangjie methods to register. Registered Cangjie methods must have String parameters and return values.|
|name|String|Yes|-|Name of the registered Cangjie method array, matching the object name used in window context calls.|
|methodList|Array\<String>|Yes|-|Names of the application-side Cangjie methods to register. This array's length must match the `funcs` array. Subsequent equality checks for `funcs` will use `methodList`. To register new or modified `funcs`, provide a new `methodList`.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

let webController = WebviewController()
let callback: AsyncCallback<String> = {
    errorCode: Option<AsyncError>, data: Option<String> => match (errorCode) {
        case Some(e) => AppLog.error("callback error: errcode is ${e.code}")
        case _ => match (data) {
            case Some(value) =>
                AppLog.info("callback: get data successfully and data is ${value.toArray()}")
                AppLog.info("callback: get data successfully and data is ${value}")
            case _ => AppLog.error("callback: data is null")
        }
    }
}
@Entry
@Component
class EntryView {
    func build() {
        Row {
            Column {
                Button("refresh").onClick {
                    evt =>
                    AppLog.info("refresh")
                    webController.refresh()
                }.width(400.px).height(150.px)
                Button("proxy").onClick {
                    evt =>
                    AppLog.info("registerJavaScriptProxy")
                    let funcA1 = {
                        a: String =>
                        AppLog.info("funcA1 ${a}")
                        return "funcA1 " + a
                    }
                    let funcA2 = {
                        a: String =>
                        AppLog.info("funcA2 ${a}")
                        return "funcA2 " + a
                    }
                    let funcA3 = {
                        a: String =>
                        AppLog.info("funcA3 ${a}")
                        return "funcA3 " + a
                    }
                    let funcB1 = {
                        a: String =>
                        AppLog.info("funcB1 ${a}")
                        return "funcB1 " + a
                    }
                    let funcB2 = {
                        a: String =>
                        AppLog.info("funcB2 ${a}")
                        return "funcB2 " + a
                    }
                    let funcB3 = {
                        a: String =>
                        AppLog.info("funcB3 ${a}")
                        return "funcB3 " + a
                    }
                    let funcsA = [funcA1, funcA2, funcA3]
                    let funcsB = [funcB1, funcB2, funcB3]
                    let methodListA = ["testFunA1", "testFunA2", "testFunA3"]
                    let methodListB = ["testFunB1", "testFunB2", "testFunB3"]
                    try {
                        webController.registerJavaScriptProxy(funcsA, "testObjA", methodListA)
                        webController.registerJavaScriptProxy(funcsB, "testObjB", methodListB)
                    } catch (e: Exception) {
                        AppLog.info(e.message)
                    }
                }.width(400.px).height(150.px)
                Button("deleteJavaScriptRegister").onClick {
                    evt =>
                    AppLog.info("deleteJavaScriptRegister")
                    webController.deleteJavaScriptRegister("testObjA")
                }.width(400.px).height(150.px)
                Button("runProxy").onClick {
                    evt =>
                    AppLog.info("runProxy")
                    webController.runJavaScript("testObjA.testFunA2('someData')", callback)
                    webController.runJavaScript("testObjB.testFunB2('someData')", callback)
                }.width(400.px).height(150.px)

                Web(src: "www.example.com", controller: webController).onPageBegin(
                    {
                    evt => AppLog.info("page begin url: ${evt.url}")
                }).onPageEnd({
                    evt => AppLog.info("page end url: ${evt.url}")
                })
            }.width(100.percent)
        }.height(100.percent)
    }
}
```

Loaded HTML file. Place the `index.html` file under `entry\src\main\resources\rawfile`.

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
<meta charset="utf-8">
<body>
<button type="button" onclick="htmlTest()">Click Me!</button>
<p id="demo"></p>
<p id="webDemo"></p>
</body>
<script type="text/javascript">
    function htmlTest() {
      // This function call expects to return "ArkUI Web Component"
      let AStr=testObjA.testFunA2("A2 data");
      let BStr=testObjB.testFunB1("B1 data");
      testObjA.testFunA3("A3 data");
      document.getElementById("demo").innerHTML=AStr;
      document.getElementById("webDemo").innerHTML=BStr;
      console.log('objName.test result:'+ str)
    }
</script>
</html>
```

### func loadData(String, String, String, ?String, ?String)

```cangjie
public func loadData(data: String, mimeType: String, encoding: String, baseUrl!: ?String = None,
    historyUrl!: ?String = None): Unit
```

**Function:** Loads specified data.

When both baseUrl and historyUrl are empty:

If encoding is not base64 (including null values), ASCII encoding is used for octets within the secure URL character range, and the standard %xx hexadecimal encoding of the URL is used for octets outside the secure URL character range.

data must be encoded using Base64 or URL encoding. Otherwise, any hash (#) in the content must be encoded as %23. If it is not, the hash (#) is considered as the end of the content, and the remaining text is used as the document fragment identifier.

> **Note:**
>
> - To load a local image, you can assign a space to either baseUrl or historyUrl.
>
> - In the scenario of loading a local image, baseUrl and historyUrl cannot be both empty. Otherwise, the image cannot be loaded.
>
> - If the rich text in HTML contains special characters such as hash (#), you are advised to set the values of **baseUrl** and **historyUrl** to spaces.
>
> - To load texts, you need to set `<meta name="viewport" content="width=device-width, initial-scale=1.0" charset="utf-8">` to avoid inconsistent font sizes.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| data | String | Yes | - | String obtained after being base64 or URL encoded. |
| mimeType | String | Yes | - | Media type (MIME). |
| encoding | String | Yes | - | Encoding type, which can be base64 or URL. |
| baseUrl | ?String | No | None | **Named parameter.** URL (compliant with HTTP/HTTPS/data), assigned by the **Web** component to window.origin. To load a large number of HTML files, set this parameter to data. |
| historyUrl | ?String | No | None | **Named parameter.** URL used in the history. When it is not empty, the history is managed based on this URL. This parameter is invalid when baseUrl is empty. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100002 | URL error. Possible causes: 1. No valid cookie found for the specified URL. 2. The webpage corresponding to the URL is invalid, or the URL length exceeds 2\*1024\*1024. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("loadData").onClick(
                {
                    evt =>
                        try {
                            let data = "<html><body>Hello, Cangjie!</body></html>"
                            webController.loadData(data, "text/html", "utf-8",
                                baseUrl: "data:text/html;charset=utf-8,")
                            Hilog.info(0, "test", "loadData done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "loadData failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func loadUrl\<T>(T, Array\<WebHeader>) where T \<: ResourceStr

```cangjie
public func loadUrl<T>(url: T, headers!: Array<WebHeader> = Array<WebHeader>()): Unit where T <: ResourceStr
```

**Function:** Loads the specified URL.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|url|T|Yes|-|URL to load.|
|headers|Array\<[WebHeader](#class-webheader)>|No|Array\<WebHeader >()|Additional HTTP request headers for the URL.|

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error.The WebviewController must be associated with a Web component. |
  | 17100002 | Invalid url. |
  | 17100003 | Invalid resource path or file type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.LocalizationKit.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(10) {
            Button("loadUrl")
            .onClick {
                evt =>
                AppLog.info("loadUrl")
                webController.loadUrl(@rawfile("index.html"), headers)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```### func setCustomUserAgent(String)

```cangjie
public func setCustomUserAgent(userAgent: String): Unit
```

**Function:** Sets a custom user agent, which will override the system's default user agent.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| userAgent | String | Yes | - | Custom user agent information. It is recommended to first use [getUserAgent](#func-getuseragent) to obtain the current default user agent and then append custom user agent information. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.{AppResource,__GenerateResource__}

@Entry
@Component
class WebView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(space: 10) {
            Button("loadUrl").onClick(
                {
                    evt =>
                        Hilog.info(0, "test", "loadUrl")
                        webController.loadUrl(@rawfile("index.html"), headers: headers)
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func requestFocus()

```cangjie
public func requestFocus(): Unit
```

**Function:** Requests focus for the current web page.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("zoomOut").onClick(
                {
                    evt =>
                        try {
                            webController.requestFocus()
                            Hilog.info(0, "test", "requestFocus done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "requestFocus failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}
```

### func setAudioMuted(Bool)

```cangjie
public func setAudioMuted(mute: Bool): Unit
```

**Function:** Mutes the web page. Typical use cases include: the app needs to control the web page volume (such as providing a mute switch), or needs to mute during background playback.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| mute | Bool | Yes | - | Whether to mute the web page. The value **true** means to mute the web page, and **false** means to unmute it. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("setAudioMuted").onClick(
                {
                    evt =>
                        try {
                            webController.setAudioMuted(true)
                            Hilog.info(0, "test", "setAudioMuted done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "setAudioMuted failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}
```

### static func setRenderProcessMode(RenderProcessMode)

```cangjie
public static func setRenderProcessMode(mode: RenderProcessMode): Unit
```

**Function:** Sets the ArkWeb rendering subprocess mode. You can select the appropriate mode based on the app's requirements for memory usage and rendering process isolation.

You can call getRenderProcessMode() to view the ArkWeb rendering subprocess mode of the current device. The enumerated value **0** indicates the single render subprocess mode, and **1** indicates the multi-render subprocess mode. By default, mobile phones use the single render subprocess mode, and tablets and PC/2-in-1 devices use the multi-render subprocess mode. If an invalid number other than the enumerated value of **RenderProcessMode** is passed, the multi-render subprocess mode is used by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| mode | [RenderProcessMode](#enum-renderprocessmode) | Yes | - | Render subprocess mode. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.Hilog

// It is recommended that this API be called during app startup and before any Web component is created.
WebviewController.setRenderProcessMode(RenderProcessMode.Single)
Hilog.info(0, "test", "setRenderProcessMode done")
```

### func setScrollable(Bool, ?ScrollType)

```cangjie
public func setScrollable(enable: Bool, scrollType!: ?ScrollType = None): Unit
```

**Function:** Sets whether the web page is scrollable, and supports specifying the scroll type.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| enable | Bool | Yes | - | Whether the web page is scrollable. The value **true** indicates that the web page is scrollable, and **false** indicates the opposite. Default value: **true**. |
| scrollType | ?[ScrollType](#enum-scrolltype) | No | None | **Named parameter.** Scroll type supported by the web page. If this parameter is not specified, all scroll types are supported. If **enable** is set to **false**, only the specified scroll type is disabled; if no scroll type is specified, all scroll types are disabled. If **enable** is set to **true**, all scroll types are enabled regardless of the value of **scrollType**. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("setScrollable").onClick(
                {
                    evt =>
                        try {
                            // Disable web page scrolling triggered by the touchscreen, touchpad, or mouse wheel.
                            webController.setScrollable(false, scrollType: ScrollType.Event)
                            Hilog.info(0, "test", "setScrollable done")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "setScrollable failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}

```

### func stop()

```cangjie
public func stop(): Unit
```

**Function:** Stops the current page from loading.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("stop")
            .onClick {
                evt =>
                AppLog.info("stop")
                webController.stop()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

### func storeWebArchive(String, Bool, AsyncCallback\<String>)

```cangjie
public func storeWebArchive(baseName: String, autoName: Bool, callback: AsyncCallback<String>): Unit
```

**Function:** Asynchronously saves the current page via callback.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| baseName | String | Yes | - | The storage location for the offline webpage. This value cannot be empty. |
| autoName | Bool | Yes | - | Determines whether to auto-generate the filename. If false, the file is stored with the name specified in `baseName`. If true, the filename is auto-generated based on the current URL, and the file is stored in the directory specified in `baseName`. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<String> | Yes | - | Returns the file storage path. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100003 | Invalid resource path or file type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

let callback: AsyncCallback<String> = {
    errorCode: Option<AsyncError>, data: Option<String> => match (errorCode) {
        case Some(e) => AppLog.error("callback error: errcode is ${e.code}")
        case _ =>
            match (data) {
                case Some(value) =>
                    AppLog.info("callback: get data successfully and data is ${value}")
                case _ => AppLog.error("callback: data is null")
            }
    }
}
@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("storeWebArchive")
            .onClick {
                evt =>
                AppLog.info("storeWebArchive")
                webController.storeWebArchive("/data/storage/el2/base/", true, callback)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

### func zoom(Float32)

```cangjie
public func zoom(factor: Float32): Unit
```

**Function:** Adjusts the zoom level of the current webpage. `zoomAccess` must be set to `true`.

> **Note:**
>
> If the input parameter is out of the value range, this call does not take effect and the webpage zoom ratio remains unchanged.
>
> If the webpage zoom ratio has already reached its maximum or minimum, calls to zoom further in the same direction do not take effect either.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| factor | Float32 | Yes | - | Zoom factor. It is multiplied by the current webpage zoom ratio to obtain the new zoom ratio. When the input value is 1, the zoom ratio remains unchanged; a value less than 1 zooms out, and a value greater than 1 zooms in.<br>Value range: (0, 100]. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100004 | Function not enabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("zoom")
            .onClick {
                evt =>
                AppLog.info("zoom")
                webController.zoom(2.5)
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

### func zoomIn()

```cangjie
public func zoomIn(): Unit
```

**Function:** Zooms in the current webpage by 20%.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100004 | Function not enabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("zoomIn")
            .onClick {
                evt =>
                AppLog.info("zoomIn")
                webController.zoomIn()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

### func zoomOut()

```cangjie
public func zoomOut(): Unit
```

**Function:** Zooms out the current webpage by 20%.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |
  | 17100004 | Function not enabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("zoomOut")
            .onClick {
                evt =>
                AppLog.info("zoomOut")
                webController.zoomOut()
            }.width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

### func runJavaScript(String, AsyncCallback\<String>)

```cangjie
public func runJavaScript(script: String, callback: AsyncCallback<String>): Unit
```

**Function:** Asynchronously executes JavaScript and returns the result via callback. `runJavaScript` must be called after `loadUrl` completes, such as in `onPageEnd`.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| script | String | Yes | - | JavaScript script to execute. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<String> | Yes | - | Callback that returns the result of the JavaScript execution. Returns `null` if the script fails or has no return value. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

let callback: AsyncCallback<String> = {
    errorCode: Option<AsyncError>, data: Option<String> => match (errorCode) {
        case Some(e) => AppLog.error("callback error: errcode is ${e.code}")
        case _ =>
            match (data) {
                case Some(value) =>
                    AppLog.info("callback: get data successfully and data is ${value}")
                case _ => AppLog.error("callback: data is null")
            }
    }
}
@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("runJavaScript")
            .onClick {
                evt =>
                AppLog.info("runJavaScript")
                webController.runJavaScript("test()", callback)
            }.width(400.px).height(150.px)

            Web(src: ("index.html"), controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

Loaded HTML file. Place `index.html` in the `entry\src\main\resources\rawfile` directory.

```html
<!-- index.html -->
<!DOCTYPE html>
<html>
  <meta charset="utf-8">
  <body>
      Hello world!
  </body>
  <script type="text/javascript">
  function test() {
      console.log('Ark WebComponent')
      return "This value is from index.html"
  }
  </script>
</html>
```

### func runJavaScriptExt(ScriptValueType, AsyncCallback\<JsMessageExt>)

```cangjie
public func runJavaScriptExt(script: ScriptValueType, callback: AsyncCallback<JsMessageExt>): Unit
```

**Function:** Executes a JavaScript script and returns the execution result through an asynchronous callback. **runJavaScriptExt** can be invoked only after **loadUrl** is executed. For example, it can be invoked in **onPageEnd**.

Unlike runJavaScript, runJavaScriptExt supports richer return value types. You can obtain the result by type through the returned JsMessageExt object.

> **Note:**
>
> The string data passed from the frontend page to the app side is treated as JSON-formatted data and needs to be deserialized with JSON.parse.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| script | [ScriptValueType](#enum-scriptvaluetype) | Yes | - | JavaScript script, which can be passed as a string or a byte array. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallbackt)\<[JsMessageExt](#class-jsmessageext)> | Yes | - | Callback used to return the execution result. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("runJavaScriptExt").onClick(
                {
                    evt =>
                        try {
                            webController.runJavaScriptExt(ScriptValueType.StringValue("test()"), { err, result =>
                                if (let Some(e) <- err) {
                                    Hilog.info(0, "test", "runJavaScriptExt failed: ${e.message}")
                                } else {
                                    let str = result?.getString() ?? ""
                                    Hilog.info(0, "test", "runJavaScriptExt result: ${str}")
                                }
                            })
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "runJavaScriptExt failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}

```

### func scrollBy(Float32, Float32, ?Int32)

```cangjie
public func scrollBy(deltaX: Float32, deltaY: Float32, duration!: ?Int32 = None): Unit
```

**Function:** Scrolls the page by the specified offset.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| deltaX | Float32 | Yes | - | Horizontal offset, where positive values scroll right. |
| deltaY | Float32 | Yes | - | Vertical offset, where positive values scroll down. |
| duration | ?Int32 | No | None | **Named parameter.** Scroll animation duration.<br>Unit: ms.<br>If not provided, no animation is applied. Negative or zero values are treated as not provided. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("scrollBy")
            .onClick {
                evt =>
                AppLog.info("scrollBy")
                webController.scrollBy(50.0, 50.0)
            }.width(400.px).height(150.px)

            Web(src: ("index.html"), controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

Loaded HTML file. Place `index.html` in the `entry\src\main\resources\rawfile` directory.

```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <title>Demo</title>
    <style>
        body {
            width:3000px;
            height:3000px;
            padding-right:170px;
            padding-left:170px;
            border:5px solid blueviolet
        }
    </style>
</head>
<body>
Scroll Test
</body>
</html>
```

### func scrollByWithResult(Float32, Float32)

```cangjie
public func scrollByWithResult(deltaX: Float32, deltaY: Float32): Bool
```

**Function:** Scrolls the web page by the specified amount and returns whether the scrolling is successful.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| deltaX | Float32 | Yes | - | Amount to scroll by along the x-axis. The positive direction is rightward. Unit: vp |
| deltaY | Float32 | Yes | - | Amount to scroll by along the y-axis. The positive direction is downward. Unit: vp |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the current web page can scroll, and **false** otherwise. |

**Exceptions:**

- BusinessException: The error codes are as follows. For details, refer to [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkUI.LengthProp
import kit.ArkUI.Button
import kit.ArkUI.Column
import kit.ArkUI.CustomView
import kit.ArkUI.CJEntry
import kit.ArkUI.loadNativeView
import kit.ArkUI.SubscriberManager
import kit.ArkUI.LocalStorage
import ohos.arkui.state_macro_manage.Entry
import ohos.arkui.state_macro_manage.Component
import kit.ArkWeb.*
import kit.ArkUI.Web
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

@Entry
@Component
class WebView {
    let webController = WebviewController()
    func build() {
        Column(space: 10) {
            Button("scrollByWithResult").onClick(
                {
                    evt =>
                        try {
                            let result = webController.scrollByWithResult(0.0, 100.0)
                            Hilog.info(0, "test", "scrollByWithResult: ${result}")
                        } catch (e: BusinessException) {
                            Hilog.info(0, "test", "scrollByWithResult failed: ${e.message}")
                        }
                }
            ).width(400.px).height(150.px)

            Web(src: "www.example.com", controller: webController).onPageBegin({
                evt => Hilog.info(0, "test", "page begin url: ${evt.url}")
            }).onPageEnd({
                evt => Hilog.info(0, "test", "page end url: ${evt.url}")
            })
        }
    }
}

```

### func scrollTo(Float32, Float32, ?Int32)

```cangjie
public func scrollTo(x: Float32, y: Float32, duration!: ?Int32 = None): Unit
```

**Function:** Scrolls the page to the specified absolute position.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | Float32 | Yes | - | Absolute horizontal coordinate. Negative values are treated as 0. |
| y | Float32 | Yes | - | Absolute vertical coordinate. Negative values are treated as 0. |
| duration | ?Int32 | No | None | **Named parameter.** Scroll animation duration.<br>Unit: ms.<br>If not provided, no animation is applied. Negative or zero values are treated as not provided. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. The WebviewController must be associated with a Web component. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    func build() {
        Column(10) {
            Button("scrollTo")
            .onClick {
                evt =>
                AppLog.info("scrollTo")
                webController.scrollTo(50.0, 50.0)
            }.width(400.px).height(150.px)

            Web(src: ("index.html"), controller: webController)
            .onPageBegin({evt =>
                AppLog.info("page begin url: ${evt.url}")
            })
            .onPageEnd({evt =>
                AppLog.info("page end url: ${evt.url}")
            })
        }
    }
}
```

Loaded HTML file. Place `index.html` in the `entry\src\main\resources\rawfile` directory.

```html
<!--index.html-->
<!DOCTYPE html>
<html>
<head>
    <title>Demo</title>
    <style>
        body {
            width:3000px;
            height:3000px;
            padding-right:170px;
            padding-left:170px;
            border:5px solid blueviolet
        }
    </style>
## enum RenderProcessMode

```cangjie
public enum RenderProcessMode <: Equatable<RenderProcessMode> & ToString {
    | Single
    | Multiple
    | ...
}
```

**Function:** Enumerates the ArkWeb rendering subprocess mode types. You can select the appropriate mode based on the app's requirements for memory usage and rendering process isolation.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<RenderProcessMode>
- ToString

### Single

```cangjie
Single
```

**Function:** ArkWeb single render subprocess mode. In this mode, multiple **Web** components share one render subprocess.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### Multiple

```cangjie
Multiple
```

**Function:** ArkWeb multi-render subprocess mode. In this mode, each **Web** component has an independent render subprocess.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### func !=(RenderProcessMode)

```cangjie
public operator func !=(other: RenderProcessMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RenderProcessMode](#enum-renderprocessmode) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are unequal, and **false** otherwise. |

### func ==(RenderProcessMode)

```cangjie
public operator func ==(other: RenderProcessMode): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RenderProcessMode](#enum-renderprocessmode) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are equal, and **false** otherwise. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Obtains the string representation of the enum.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the enum. |

## enum ScriptValueType

```cangjie
public enum ScriptValueType <: Equatable<ScriptValueType> & ToString {
    | StringValue(String)
    | ArrayBufferValue(ArrayBuffer)
    | ...
}
```

**Function:** Defines the script type of the runJavaScriptExt API. The JavaScript script to execute can be passed as a string or a byte array.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<ScriptValueType>
- ToString

### StringValue

```cangjie
StringValue(String)
```

**Function:** The JavaScript script is passed as a string.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### ArrayBufferValue

```cangjie
ArrayBufferValue(ArrayBuffer)
```

**Function:** The JavaScript script is passed as a byte array.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### func !=(ScriptValueType)

```cangjie
public operator func !=(other: ScriptValueType): Bool
```

**Function:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScriptValueType](#enum-scriptvaluetype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are unequal, and **false** otherwise. |

### func ==(ScriptValueType)

```cangjie
public operator func ==(other: ScriptValueType): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScriptValueType](#enum-scriptvaluetype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are equal, and **false** otherwise. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Obtains the string representation of the enum.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the enum. |

## enum ScrollType

```cangjie
public enum ScrollType <: Equatable<ScrollType> & ToString {
    | Event
    | ...
}
```

**Function:** Enumerates the scroll types of the setScrollable API.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<ScrollType>
- ToString

### Event

```cangjie
Event
```

**Function:** Scroll event, which represents web page scrolling triggered through the touchscreen, touchpad, or mouse wheel.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

### func !=(ScrollType)

```cangjie
public operator func !=(other: ScrollType): Bool
```

**Function:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollType](#enum-scrolltype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are unequal, and **false** otherwise. |

### func ==(ScrollType)

```cangjie
public operator func ==(other: ScrollType): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ScrollType](#enum-scrolltype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns **true** if the enum values are equal, and **false** otherwise. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Obtains the string representation of the enum.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the enum. |

## enum SecurityLevel

```cangjie
public enum SecurityLevel <: Equatable<SecurityLevel> & ToString {
    | NoneLevel
    | Secure
    | Warning
    | Danger
    | ...
}
```

**Function:** Indicates the security level of the current webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parent Types:**

- Equatable\<SecurityLevel>
- ToString

### NoneLevel

```cangjie
NoneLevel
```

**Function:** The page is neither absolutely secure nor insecure, i.e., neutral. For example, URLs with schemes other than http/https.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Secure

```cangjie
Secure
```

**Function:** The page is secure, using HTTPS protocol with a trusted certificate.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Warning

```cangjie
Warning
```

**Function:** The page is insecure. For example, using HTTP protocol or HTTPS with outdated TLS versions.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Danger

```cangjie
Danger
```

**Function:** The page is insecure. This includes failed HTTPS attempts, unauthenticated pages, HTTPS pages containing unsafe active content, malware, phishing, or any other critical security risks.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### func !=(SecurityLevel)

```cangjie
public operator func !=(other: SecurityLevel): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SecurityLevel](../ArkData/cj-apis-distributed_kv_store.md#enum-securitylevel) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(SecurityLevel)

```cangjie
public operator func ==(other: SecurityLevel): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SecurityLevel](../ArkData/cj-apis-distributed_kv_store.md#enum-securitylevel) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the enum. |

## enum WebHitTestType

```cangjie
public enum WebHitTestType <: Equatable<WebHitTestType> & ToString {
    | EditText
    | Email
    | Unknown
    | ...
}
```

**Function:** Indicates the cursor node for [getHitTest](#func-gethittest).

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parent Types:**

- Equatable\<WebHitTestType>
- ToString

### EditText

```cangjie
EditText
```

**Function:** An editable area.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Email

```cangjie
Email
```

**Function:** An email address.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### Unknown

```cangjie
Unknown
```

**Function:** Unknown content.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

### func !=(WebHitTestType)

```cangjie
public operator func !=(other: WebHitTestType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WebHitTestType](#enum-webhittesttype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are unequal, otherwise false. |

### func ==(WebHitTestType)

```cangjie
public operator func ==(other: WebHitTestType): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [WebHitTestType](#enum-webhittesttype) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the enum. |