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
import ohos.business_exception.BusinessException
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
import ohos.business_exception.BusinessException
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
import ohos.business_exception.BusinessException
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
import ohos.business_exception.BusinessException

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

### static func putAcceptThirdPartyCookieEnabled(B## class WebHeader

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

**Description:** Checks whether the current page can go back, i.e., whether there is a back history for the current page.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if it can go back, otherwise returns false. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [Webview Error Codes](./cj-errorcode-webview.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 17100001 | Init error. |

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
        Column(space:10) {
            Button("accessBackward")
            .onClick {
                evt =>
                Hilog.info(0, "cangjieTest", "accessBackward")
                let bool = webController.accessBackward()
                Hilog.info(0, "cangjieTest", "accessBackward returns ${bool}")
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

import kit.ArkWeb.*
import kit.UIKit.Web

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    let headers = [WebHeader("headerKey", "headerValue")]
    func build() {
        Column(10) {
            Button("setCustomUserAgent")
            .onClick {
                evt =>
                AppLog.info("setCustomUserAgent")
                webController.setCustomUserAgent("ua")
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