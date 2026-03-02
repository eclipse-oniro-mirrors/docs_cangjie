# Web

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides Web components with web display capabilities. [@ohos.web.webview](../ArkWeb/cj-apis-webview.md) offers web control functionalities.

## Importing Modules

```cangjie
import kit.ArkUI.*
```

## Subcomponents

None

## Creating Components

### init(ResourceStr, WebviewController)

```cangjie
public init(
    src!: ResourceStr,
    controller!: WebviewController
)
```

**Functionality:** Creates a Web component.

> **Note:**
>
> - Transition animations are not supported.
> - Multiple Web components on the same page must be bound to different WebviewControllers.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** The src cannot be dynamically changed via state variables (e.g., @State). |
| controller | [WebviewController](../ArkWeb/cj-apis-webview.md#class-webviewcontroller) | Yes | - | **Named parameter.** Sets the Web controller. |

## Universal Attributes/Events

Universal Attributes: Only supports [aspectRatio](./cj-universal-attribute-size.md#func-aspectratiofloat64), [backdropBlur](./cj-universal-attribute-imageeffect.md#func-backdropblurfloat64), [backgroundColor](./cj-universal-attribute-background.md#func-backgroundcolorresourcecolor), [bindContentCover](./cj-universal-attribute-menu.md), [bindContextMenu](./cj-universal-attribute-menu.md#func-bindcontextmenucustombuilder-responsetype-contextmenuoptions), [bindMenu](./cj-universal-attribute-menu.md#func-bindmenuarraymenuelement) , [bindSheet](./cj-universal-attribute-sheettransition.md#func-bindsheetbool-custombuilder-sheetoptions), [borderColor](./cj-universal-attribute-border.md#func-bordercolorresourcecolor), [borderStyle](./cj-common-types.md#enum-borderstyle), [borderWidth](./cj-universal-attribute-border.md#func-borderwidthedgewidths), [clip](./cj-common-types.md#clip), [constraintSize](./cj-universal-attribute-layoutconstraints.md#func-constraintsizelength-length-length-length), [defaultFocus](./cj-universal-attribute-focus.md#func-defaultfocusbool), [focusable](./cj-universal-attribute-focus.md#func-focusablebool), [tabIndex](./cj-universal-attribute-focus.md#func-tabindexint32), [groupDefaultFocus](./cj-universal-attribute-focus.md#func-groupdefaultfocusbool), [displayPriority](./cj-universal-attribute-size.md#func-displaypriorityint32), [enabled](./cj-universal-attribute-enable.md#func-enabledbool), [flexBasis](./cj-universal-attribute-flexlayout.md#func-flexbasislength), [flexShrink](./cj-universal-attribute-flexlayout.md#func-flexshrinkfloat64), [layoutWeight](./cj-universal-attribute-size.md#func-layoutweightint32), [id](./cj-universal-attribute-componentid.md), [height](./cj-universal-attribute-size.md#func-heightoptionlength), [touchable](./cj-apis-window.md#var-touchable), [margin](./cj-universal-attribute-size.md#func-marginlength), [markAnchor](./cj-universal-attribute-location.md#func-markanchorlength-length), [offset](./cj-apis-componentutils.md#class-offset), [width](./cj-universal-attribute-size.md#func-widthoptionlength), [zIndex](./cj-universal-attribute-zorder.md#func-zindexint32), [visibility](./cj-common-types.md#enum-visibility), [scale](./cj-animation-pagetransition.md#func-scalefloat32-float32-float32-length-length), [translate](./cj-universal-attribute-transform.md#func-translatelength-length-length), [responseRegion](./cj-universal-attribute-touchtarget.md#func-responseregionarrayrectangle), [size](./cj-universal-attribute-size.md#func-sizelength-length), [opacity](./cj-animation-pagetransition.md#func-opacityfloat64), [sharedTransition](./cj-animation-sharedtransition.md#func-sharedtransitionstring-sharedtransitionoptions), [transition](./cj-animation-transition.md#func-transitiontransitioneffect), [position](./cj-universal-attribute-location.md#func-positionlength-length), [direction](./cj-universal-attribute-layoutconstraints.md#func-directiondirection).

Universal Events: Only supports [onAppear](./cj-universal-attribute-menu.md#var-onappear), [onDisAppear](./cj-universal-attribute-menu.md#var-ondisappear), [onBlur](./cj-universal-event-focus.md#func-onblur---unit), [onFocus](./cj-universal-event-focus.md#func-onfocus---unit), [onHover](./cj-universal-event-mouse.md), [onMouse](./cj-universal-event-mouse.md#func-onmousemouseevent), [onKeyEvent](./cj-universal-event-key.md#func-onkeyeventkeyevent-unit), [onTouch](./cj-universal-event-touch.md#func-ontouchtouchevent-unit), [onVisibleAreaChange](./cj-universal-event-visibleareachange.md#func-onvisibleareachangearrayfloat64-bool-float64-unit---unit).

## Component Attributes

### func darkMode(?WebDarkMode)

```cangjie
public func darkMode(mode: ?WebDarkMode): This
```

**Functionality:** Sets the Web dark mode, which is disabled by default. When dark mode is enabled, the Web will apply the dark styles defined in the webpage's media query prefers-color-scheme. If no dark styles are defined, the original appearance is maintained. To enable forced dark mode, it is recommended to use it in conjunction with [forceDarkAccess](#func-forcedarkaccessbool).

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mode | ?[WebDarkMode](./cj-common-types.md#enum-webdarkmode) | Yes | - | The dark mode of the Web can be off, on, or follow the system. <br>Initial value: WebDarkMode.Off. |

### func domStorageAccess(?Bool)

```cangjie
public func domStorageAccess(domStorageAccess: ?Bool): This
```

**Functionality:** Sets whether to enable the Document Object Model Storage API (DOM Storage API) permission.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| domStorageAccess | ?Bool | Yes | - | Whether to enable the Document Object Model Storage API (DOM Storage API) permission. true indicates enabled, false indicates disabled. <br>Initial value: false. |

### func fileAccess(?Bool)

```cangjie
public func fileAccess(fileAccess: ?Bool): This
```

**Functionality:** Sets whether to enable access to the file system within the application, which is enabled by default. Files in the rawfile path are not affected by this attribute and remain accessible.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fileAccess | ?Bool | Yes | - | Whether to enable access to the file system within the application, which is enabled by default. <br>Initial value: false |

### func forceDarkAccess(?Bool)

```cangjie
public func forceDarkAccess(access: ?Bool): This
```

**Functionality:** Sets whether to enable forced dark mode for webpages. Disabled by default. This attribute only takes effect when darkMode is enabled.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| access | ?Bool | Yes | - | Sets whether to enable forced dark mode for webpages. true: enabled, false: disabled. <br>Initial value: false. |

### func geolocationAccess(?Bool)

```cangjie
public func geolocationAccess(geolocationAccess: ?Bool): This
```

**Functionality:** Sets whether to enable geolocation permission, which is disabled by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| geolocationAccess | ?Bool | Yes | - | Sets whether to enable geolocation permission. <br>Initial value: false. |

### func imageAccess(?Bool)

```cangjie
public func imageAccess(imageAccess: ?Bool): This
```

**Functionality:** Sets whether to allow automatic loading of image resources, which is allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| imageAccess | ?Bool | Yes | - | Whether to allow automatic loading of image resources. <br>Initial value: false. |

### func javaScriptProxy(?Array\<(String) -> String>, ?String, ?Array\<String>, ?WebviewController)

```cangjie
public func javaScriptProxy(funcList!: ?Array<(String) -> String>, name!: ?String, methodList!: ?Array<String>,
    controller!: ?WebviewController): This
```

**Functionality:** Injects a JavaScript object into the window object and calls the object's methods within the window object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| funcList | ?Array\<(String)->String> | Yes | - | **Named parameter.** The synchronous methods of the application-side JavaScript object to be registered. <br>Initial value: []. |
| name | ?String | Yes | - | **Named parameter.** The name of the registered object, which matches the object name called in the window. <br>Initial value: "". |
| methodList | ?Array\<String> | Yes | - | **Named parameter.** The asynchronous methods of the application-side JavaScript object to be registered. <br>Initial value: []. |
| controller | ?[WebviewController](../ArkWeb/cj-apis-webview.md#class-webviewcontroller) | Yes | - | **Named parameter.** Sets the Web controller. <br>Initial value: WebviewController(). |

### func mixedMode(?MixedMode)

```cangjie
public func mixedMode(mixedMode: ?MixedMode): This
```

**Functionality:** Sets whether to allow loading mixed content of Hypertext Transfer Protocol (HTTP) and Hypertext Transfer Protocol Secure (HTTPS), which is disallowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mixedMode | ?[MixedMode](./cj-common-types.md#enum-mixedmode) | Yes | - | Mixed content. <br>Initial value: MixedMode.None. Indicates that secure origins are not allowed to load content from insecure origins. |

### func nestedScroll(?NestedScrollMode, ?NestedScrollMode)

```cangjie
public func nestedScroll(
    scrollForward!: ?NestedScrollMode,
    scrollBackward!: ?NestedScrollMode
): This
```

**Functionality:** Sets the nested scrolling modes for forward and backward directions to achieve scrolling linkage with parent components.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scrollForward | ?[NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | **Named parameter.** Forward scrolling mode. <br>Initial value: NestedScrollMode.SelfFirst. |
| scrollBackward | ?[NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | **Named parameter.** Backward scrolling mode. <br>Initial value: NestedScrollMode.SelfFirst. |

### func onlineImageAccess(?Bool)

```cangjie
public func onlineImageAccess(onlineImageAccess: ?Bool): This
```

**Functionality:** Sets whether to allow loading image resources from the network (resources accessed via HTTP and HTTPS), which is disallowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| onlineImageAccess | ?Bool | Yes | - | Whether to allow loading image resources from the network. true indicates allowed, false indicates disallowed. <br>Initial value: false. |

### func verticalScrollBarAccess(?Bool)

```cangjie
public func verticalScrollBarAccess(verticalScrollBar: ?Bool): This
```

**Functionality:** Sets whether to display vertical scroll bars, including system-default scroll bars and user-defined scroll bars. Not displayed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| verticalScrollBar | ?Bool | Yes | - | Whether to display vertical scroll bars. true indicates displayed, false indicates not displayed. <br>Initial value: false. |

### func zoomAccess(?Bool)

```cangjie
public func zoomAccess(zoomAccess: ?Bool): This
```

**Functionality:** Sets whether to support zooming via gestures, which is disallowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| zoomAccess | ?Bool | Yes | - | Whether to support zooming via gestures. true indicates supported, false indicates not supported. <br>Initial value: false. |

## Component Events

### func onLoadIntercept(?Callback\<OnLoadInterceptEvent, Bool>)

```cangjie
public func onLoadIntercept(callback: ?Callback<OnLoadInterceptEvent, Bool>): This
```

**Functionality:** Triggered before the Web component loads a URL, used to determine whether to block this access. Allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?Callback\<[OnLoadInterceptEvent](#class-onloadinterceptevent), Bool> | Yes | - | Callback function triggered when resource loading is intercepted. Returns true to block the loading, otherwise allows it. <br>Initial value: { _ => true}. |

### func onPageBegin(?Callback\<OnPageBeginEvent, Unit>)

```cangjie
public func onPageBegin(callback: ?Callback<OnPageBeginEvent, Unit>): This
```

**Functionality:** Triggered when a webpage starts loading, only for the main frame. Loading of iframe or frameset content does not trigger this callback.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?Callback\<[OnPageBeginEvent](#class-onpagebeginevent), Unit> | Yes | - | Callback function triggered when webpage loading starts. <br>Initial value: { _ => }. |

### func onPageEnd(?Callback\<OnPageEndEvent, Unit>)

```cangjie
public func onPageEnd(callback: ?Callback<OnPageEndEvent, Unit>): This
```

**Functionality:** Triggered when a webpage finishes loading, only for the main frame.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?Callback\<[OnPageEndEvent](#class-onpageendevent), Unit> | Yes | - | Whether to allow loading image resources from the network. true indicates allowed, false indicates disallowed. <br>Initial value: { _ => }. |

## Basic Type Definitions

### class Header

```cangjie
public class Header {
    public var headerKey: ?String
    public var headerValue: ?String
}
```

**Functionality:** Describes the request/response header object returned by the Web component.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### var headerKey

```cangjie
public var headerKey: ?String
```

**Functionality:** The key of the request/response header.

**Type:** ?String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### var headerValue

```cangjie
public var headerValue: ?String
```

**Functionality:** The value of the request/response header### class OnPageBeginEvent

```cangjie
public class OnPageBeginEvent {
    public var url: String
    public init(url: String)
}
```

**Function:** Defines the function triggered when webpage loading begins.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### var url

```cangjie
public var url: String
```

**Function:** The URL of the currently loading page.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### init(String)

```cangjie
public init(url: String)
```

**Function:** Creates an OnPageBeginEvent object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL of the currently loading page. |

### class OnPageEndEvent

```cangjie
public class OnPageEndEvent {
    public var url: String
    public init(url: String)
}
```

**Function:** Defines the function triggered when webpage loading completes.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### var url

```cangjie
public var url: String
```

**Function:** The URL of the currently loading page.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### init(String)

```cangjie
public init(url: String)
```

**Function:** Constructor for OnPageEndEvent.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL of the currently loading page. |

### class PermissionRequest

```cangjie
public class PermissionRequest {}
```

**Function:** The object returned by Web component for granting or denying permission functionality. Example code reference [onPermissionRequest](#class-onpermissionrequestevent) event.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### func deny()

```cangjie
public func deny(): Unit
```

**Function:** Denies the permission requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### func getAccessibleResource()

```cangjie
public func getAccessibleResource(): Array<String>
```

**Function:** Gets the list of permission resources requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | The list of permission resources requested by the webpage. |

#### func getOrigin()

```cangjie
public func getOrigin(): String
```

**Function:** Gets the origin of the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | The origin of the webpage requesting permission. |

#### func grant(Array\<String>)

```cangjie
public func grant(resources: Array<String>): Unit
```

**Function:** Grants permission for screen capture operations requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| resources | Array\<String> | Yes | - | Screen capture configuration. |

### class WebResourceRequest

```cangjie
public class WebResourceRequest {}
```

**Function:** Web component resource response object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### func getRequestHeader()

```cangjie
public func getRequestHeader(): Array<Header>
```

**Function:** Gets the resource request header information.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Header](#class-header)> | Returns the resource request header information. |

#### func getRequestMethod()

```cangjie
public func getRequestMethod(): String
```

**Function:** Gets the request method.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the request method. |

#### func getRequestUrl()

```cangjie
public func getRequestUrl(): String
```

**Function:** Gets the URL information of the resource request.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the URL information of the resource request. |

#### func isMainFrame()

```cangjie
public func isMainFrame(): Bool
```

**Function:** Determines whether the resource request is for the main frame.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether the resource request is for the main frame. true indicates the request is for the main frame, false indicates it is not. |

#### func isRedirect()

```cangjie
public func isRedirect(): Bool
```

**Function:** Determines whether the resource request was redirected by the server.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether the resource request was redirected by the server. true indicates the request was redirected, false indicates it was not. |

#### func isRequestGesture()

```cangjie
public func isRequestGesture(): Bool
```

**Function:** Gets whether the resource request is associated with a gesture (e.g., click).

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether the resource request is associated with a gesture (e.g., click). true indicates association, false indicates no association. |

### class OnPermissionRequestEvent

```cangjie
public class OnPermissionRequestEvent {
    public var request: PermissionRequest
    public init(request: PermissionRequest)
}
```

**Function:** Describes the parameter structure for notifying receipt of a permission request.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### var request

```cangjie
public var request: PermissionRequest
```

**Function:** The object returned by Web component for granting or denying permission functionality. Example code reference [onPermissionRequest](#class-onpermissionrequestevent) event.

**Type:** [PermissionRequest](#class-permissionrequest)

**Access:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

#### init(PermissionRequest)

```cangjie
public init(request: PermissionRequest)
```

**Function:** Creates an OnPermissionRequestEvent object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| request | [PermissionRequest](#class-permissionrequest) | Yes | - | The object returned by Web component for granting or denying permission functionality. |

## Example Code

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.web.webview.*
import ohos.hilog.Hilog

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    @State var url: String = "www.example.com"
    func build() {
        Column(space: 10) {
            Button("refresh")
            .onClick({
                evt =>
                Hilog.info(0, "AppLogCj", "refresh")
                webController.reload()
            }).width(400.px).height(150.px)
            Button("loadUrl")
            .onClick({
                evt =>
                Hilog.info(0, "AppLogCj", "loadUrl")
                webController.loadUrl(this.url)

            }).width(400.px).height(150.px)
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