# Web

Provides Web components with web display capabilities. [@ohos.web.webview](../ArkWeb/cj-apis-webview.md) offers web control functionalities.

## Import Module

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

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| src | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | **Named parameter.** The src cannot dynamically change addresses via state variables (e.g., @State). |
| controller | [WebviewController](../ArkWeb/cj-apis-webview.md#class-webviewcontroller) | Yes | - | **Named parameter.** Sets the Web controller. |

## Common Attributes/Common Events

Common Attributes: Only supports [aspectRatio](./cj-universal-attribute-layoutconstraints.md#func-aspectratiofloat64), [backdropBlur](./cj-universal-attribute-background.md#func-backdropblurfloat64), [backgroundColor](./cj-universal-attribute-background.md#func-backgroundcolorresourcecolor), [bindContentCover](./cj-universal-attribute-menu.md), [bindContextMenu](./cj-universal-attribute-menu.md#func-bindcontextmenucustombuilder-responsetype-contextmenuoptions), [bindMenu](./cj-universal-attribute-menu.md#func-bindmenuarraymenuelement), [bindSheet](./cj-universal-attribute-sheettransition.md#func-bindsheetbool-custombuilder-sheetoptions), [borderColor](./cj-universal-attribute-border.md#func-bordercolorresourcecolor), [borderRadius](./cj-common-types.md#class-borderradiuses), [borderStyle](./cj-common-types.md#enum-borderstyle), [borderWidth](./cj-universal-attribute-border.md#func-borderwidthlength), [clip](./cj-common-types.md#clip), [constraintSize](./cj-universal-attribute-size.md#func-constraintsizelength-length-length-length), [defaultFocus](./cj-universal-attribute-focus.md#func-defaultfocusbool), [focusable](./cj-universal-attribute-focus.md#func-focusablebool), [tabIndex](./cj-universal-attribute-focus.md#func-tabindexint32), [groupDefaultFocus](./cj-universal-attribute-focus.md#func-groupdefaultfocusbool), [displayPriority](./cj-universal-attribute-layoutconstraints.md#func-displaypriorityint32), [enabled](./cj-universal-attribute-enable.md#func-enabledbool), [flexBasis](./cj-universal-attribute-flexlayout.md#func-flexbasislength), [flexShrink](./cj-universal-attribute-flexlayout.md#func-flexshrinkfloat64), [layoutWeight](./cj-universal-attribute-size.md#func-layoutweightint32), [id](./cj-universal-attribute-componentid.md), [height](./cj-universal-attribute-size.md#func-heightoptionlength), [margin](./cj-universal-attribute-size.md#func-marginlength), [markAnchor](./cj-universal-attribute-location.md#func-markanchorlength-length), [mask](./cj-scroll-swipe-swiper.md#func-maskbool), [offset](./cj-apis-componentutils.md#class-offset), [width](./cj-universal-attribute-size.md#func-widthoptionlength), [zIndex](./cj-universal-attribute-zorder.md#func-zindexint32), [visibility](./cj-common-types.md#enum-visibility), [scale](./cj-animation-pagetransition.md#func-scalefloat32-float32-float32-length-length), [transform](./cj-canvas-drawing-canvasrenderingcontext2d.md#func-transformfloat64-float64-float64-float64-float64-float64), [responseRegion](./cj-universal-attribute-touchtarget.md#func-responseregionrectangle), [size](./cj-universal-attribute-size.md#func-sizelength-length), [opacity](./cj-animation-pagetransition.md#func-opacityfloat64), [shadow](./cj-universal-attribute-imageeffect.md#func-shadowfloat64-resourcecolor-float64-float64), [gesture](./cj-universal-gesture-bind.md#func-gesturemask), [sharedTransition](./cj-animation-sharedtransition.md#func-sharedtransitionstring-sharedtransitionoptions), [transition](./cj-animation-transition.md#func-transitiontransitioneffect).

<!-- note -->
Common Events: Only supports [onAppear](./cj-ui-framework.md#func-onappear---unit), [onDisAppear](./cj-ui-framework.md#func-ondisappear---unit), [onBlur](cj-ui-framework.md#func-onblur---unit), [onFocus](cj-ui-framework.md#func-onblur---unit), [onDragEnter](./cj-universal-event-drag.md#func-ondragenterdraginfo---unit), [onDragStart](./cj-universal-event-drag.md#func-ondragstartdraginfo---unit), [onDragMove](./cj-universal-event-drag.md#func-ondragmovedraginfo---unit), [onDragLeave](./cj-universal-event-drag.md#func-ondragleavedraginfo---unit), [onDrop](./cj-universal-event-drag.md#func-ondropdraginfo---unit), [onHover](./cj-universal-event-mouse.md), [onMouse](./cj-universal-event-mouse.md#func-onmousemouseevent---unit), [onKeyEvent](./cj-universal-event-key.md#func-onkeyeventkeyevent---unit), [onTouch](./cj-universal-event-touch.md#func-ontouchtouchevent---unit), [onVisibleAreaChange](./cj-ui-framework.md#func-onvisibleareachangearrayfloat64-boolfloat64---unit).

## Component Attributes

### func darkMode(WebDarkMode)

```cangjie
public func darkMode(mode: WebDarkMode): This
```

**Functionality:** Sets the Web dark mode, which is disabled by default. When dark mode is enabled, the Web will apply the dark styles defined in the webpage's media query prefers-color-scheme. If no dark styles are defined, the original appearance is maintained. To enable forced dark mode, it is recommended to use it in conjunction with [forceDarkAccess](#func-forcedarkaccessbool).

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mode | [WebDarkMode](./cj-common-types.md#enum-webdarkmode) | Yes | - | The dark mode of the Web can be off, on, or follow the system. <br> Initial value: WebDarkMode.Off. |

### func domStorageAccess(Bool)

```cangjie
public func domStorageAccess(domStorageAccess: Bool): This
```

**Functionality:** Sets whether to enable the Document Object Model Storage API (DOM Storage API) permissions.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| domStorageAccess | Bool | Yes | - | Whether to enable the Document Object Model Storage API (DOM Storage API) permissions. true means enabled, false means disabled. <br> Initial value: false. |

### func fileAccess(Bool)

```cangjie
public func fileAccess(fileAccess: Bool): This
```

**Functionality:** Sets whether to enable access to the application's file system, which is enabled by default. Files in the rawfile path are not affected by this attribute and remain accessible.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fileAccess | Bool | Yes | - | Whether to enable access to the application's file system, which is enabled by default. |

### func forceDarkAccess(Bool)

```cangjie
public func forceDarkAccess(access: Bool): This
```

**Functionality:** Sets whether to enable forced dark mode for webpages. Disabled by default. This attribute only takes effect when darkMode is enabled.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| access | Bool | Yes | - | Sets whether to enable forced dark mode for webpages. true: enabled, false: disabled. |

### func geolocationAccess(Bool)

```cangjie
public func geolocationAccess(geolocationAccess: Bool): This
```

**Functionality:** Sets whether to enable geolocation permissions, which are enabled by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| geolocationAccess | Bool | Yes | - | Sets whether to enable geolocation permissions. |

### func imageAccess(Bool)

```cangjie
public func imageAccess(imageAccess: Bool): This
```

**Functionality:** Sets whether to allow automatic loading of image resources, which is allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| imageAccess | Bool | Yes | - | Whether to allow automatic loading of image resources. |

### func javaScriptProxy(Array\<(String) -> String>, String, Array\<String>, WebviewController)

```cangjie
public func javaScriptProxy(funcList!: Array<(String) -> String>, name!: String, methodList!: Array<String>,
    controller!: WebviewController): This
```

**Functionality:** Injects a JavaScript object into the window object and calls the object's methods within the window object.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| funcList | Array\<(String)->String> | Yes | - | **Named parameter.** The synchronous methods of the JavaScript object on the application side participating in registration. |
| name | String | Yes | - | **Named parameter.** The name of the registered object, consistent with the object name called in the window. |
| methodList | Array\<String> | Yes | - | **Named parameter.** The asynchronous methods of the JavaScript object on the application side participating in registration. |
| controller | [WebviewController](../ArkWeb/cj-apis-webview.md#class-webviewcontroller) | Yes | - | **Named parameter.** Sets the Web controller. |

### func mixedMode(MixedMode)

```cangjie
public func mixedMode(mixedMode: MixedMode): This
```

**Functionality:** Sets whether to allow loading mixed content of Hypertext Transfer Protocol (HTTP) and Hypertext Transfer Protocol Secure (HTTPS), which is disallowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mixedMode | [MixedMode](#enum-mixedmode) | Yes | - | Mixed content. <br> Initial value: MixedMode.None, indicating that secure origins are not allowed to load content from insecure origins. |

### func nestedScroll(NestedScrollMode, NestedScrollMode)

```cangjie
public func nestedScroll(
    scrollForward!: NestedScrollMode,
    scrollBackward!: NestedScrollMode
): This
```

**Functionality:** Sets the nested scroll mode in both forward and backward directions to achieve scroll linkage with the parent component.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scrollForward | [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | **Named parameter.** Forward scroll direction. |
| scrollBackward | [NestedScrollMode](./cj-common-types.md#enum-nestedscrollmode) | Yes | - | **Named parameter.** Backward scroll direction. |

### func verticalScrollBarAccess(Bool)

```cangjie
public func verticalScrollBarAccess(verticalScrollBar: Bool): This
```

**Functionality:** Sets whether to display the vertical scrollbar, including the system default scrollbar and user-defined scrollbars. Displayed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| verticalScrollBar | Bool | Yes | - | Whether to display the vertical scrollbar. true means to display the vertical scrollbar, false means not to display it. <br> Initial value: true. |

### func zoomAccess(Bool)

```cangjie
public func zoomAccess(zoomAccess: Bool): This
```

**Functionality:** Sets whether to support zooming via gestures, which is allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| zoomAccess | Bool | Yes | - | Whether to support zooming via gestures. true means to support zooming via gestures, false means not to support it. <br> Initial value: true. |

## Component Events

### func onLoadIntercept(Callback\<OnLoadInterceptEvent,Bool>)

```cangjie
public func onLoadIntercept(callback: Callback<OnLoadInterceptEvent, Bool>): This
```

**Functionality:** Triggers this callback before the Web component loads a URL, used to determine whether to block this access. Allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-callback)\<[OnLoadInterceptEvent](#class-onloadinterceptevent),Bool> | Yes | - | Callback function triggered when resource loading is intercepted. <br> Return value boolean. Returns true to block this loading, otherwise allows it. |

### func onPageBegin(Callback\<OnPageBeginEvent,Unit>)

```cangjie
public func onPageBegin(callback: Callback<OnPageBeginEvent, Unit>): This
```

**Functionality:** Triggers this callback when the webpage starts loading, and only triggers in the main frame. Loading content in iframe or frameset does not trigger this callback.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-callback)\<[OnPageBeginEvent](#class-onpagebeginevent),Unit> | Yes | - | Callback function triggered when webpage loading starts. |

### func onPageEnd(Callback\<OnPageEndEvent,Unit>)

```cangjie
public func onPageEnd(callback: Callback<OnPageEndEvent, Unit>): This
```

**Functionality:** Triggers this callback when the webpage finishes loading, and only triggers in the main frame.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback](../BasicServicesKit/cj-apis-base.md#type-callback)\<[OnPageEndEvent](#class-onpageendevent),Unit> | Yes | - | Triggered when webpage loading ends. |

### func onlineImageAccess(Bool)

```cangjie
public func onlineImageAccess(onlineImageAccess: Bool): This
```

**Functionality:** Sets whether to allow loading image resources from the network (resources accessed via HTTP and HTTPS), which is allowed by default.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| onlineImageAccess | Bool | Yes | - | Whether to allow loading image resources from the network. true means to allow loading image resources from the network, false means not to allow it. <br> Initial value: true. |

## Basic Type Definitions

### class Header

```cangjie
public class Header {
    public var headerKey: String
    public var headerValue: String
}
```

**Functionality:** Describes the request/response header object returned by the Web component.

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

#### var headerKey

```cangjie
public var headerKey: String
```

**Functionality:** The key of the request/response header.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Web.Webview.Core

**Initial Version:** 21

#### var headerValue

```cangjie
public var headerValue: String
```

**Functionality:** The value of the request/response header.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:**### class OnPageBeginEvent

```cangjie
public class OnPageBeginEvent {
    public var url: String

    public init(url: String)
}
```

**Description:** Defines the function triggered when a webpage starts loading.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### var url

```cangjie
public var url: String
```

**Description:** The URL of the currently loading page.

**Type:** String

**Read-Write Attribute:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### init(String)

```cangjie

public init(url: String)
```

**Description:** Constructor.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL of the currently loading page. |

### class OnPageEndEvent

```cangjie
public class OnPageEndEvent {
    public var url: String

    public init(url: String)
}
```

**Description:** Defines the function triggered when a webpage finishes loading.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### var url

```cangjie
public var url: String
```

**Description:** The URL of the currently loaded page.

**Type:** String

**Read-Write Attribute:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### init(String)

```cangjie

public init(url: String)
```

**Description:** Constructor.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| url | String | Yes | - | The URL of the currently loaded page. |

### class OnPermissionRequestEvent

```cangjie
public class OnPermissionRequestEvent {
    public var request: PermissionRequest

    public init(request: PermissionRequest)
}
```

**Description:** Describes the parameter structure for notifying when a permission request is received.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### var request

```cangjie
public var request: PermissionRequest
```

**Description:** The object returned by the Web component for granting or denying permissions. For sample code, refer to the [onPermissionRequest](#class-onpermissionrequestevent) event.

**Type:** [PermissionRequest](#class-permissionrequest)

**Read-Write Attribute:** Read-Write

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### init(PermissionRequest)

```cangjie

public init(request: PermissionRequest)
```

**Description:** Constructor.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| request | [PermissionRequest](#class-permissionrequest) | Yes | - | The object returned by the Web component for granting or denying permissions. |

### class PermissionRequest

```cangjie
public class PermissionRequest {}
```

**Description:** The object returned by the Web component for granting or denying permissions. For sample code, refer to the [onPermissionRequest](#class-onpermissionrequestevent) event.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### func deny()

```cangjie

public func deny(): Unit
```

**Description:** Denies the permission requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### func getAccessibleResource()

```cangjie

public func getAccessibleResource(): Array<String>
```

**Description:** Gets the list of permission resources requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | The list of permission resources requested by the webpage. |

#### func getOrigin()

```cangjie

public func getOrigin(): String
```

**Description:** Gets the origin of the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The origin of the webpage requesting the permission. |

#### func grant(Array\<String>)

```cangjie

public func grant(resources: Array<String>): Unit
```

**Description:** Grants permission for screen capture operations requested by the webpage.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| resources | Array\<String> | Yes | - | The screen capture configuration. |

### class WebResourceRequest

```cangjie
public class WebResourceRequest {}
```

**Description:** The Web component resource response object.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

#### func getRequestHeader()

```cangjie

public func getRequestHeader(): Array<Header>
```

**Description:** Gets the request header information of the resource.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Header](#class-header)> | The request header information of the resource. |

#### func getRequestMethod()

```cangjie

public func getRequestMethod(): String
```

**Description:** Gets the request method.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The request method. |

#### func getRequestUrl()

```cangjie

public func getRequestUrl(): String
```

**Description:** Gets the URL information of the resource request.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The URL information of the resource request. |

#### func isMainFrame()

```cangjie

public func isMainFrame(): Bool
```

**Description:** Determines whether the resource request is for the main frame.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the resource request is for the main frame. `true` indicates it is for the main frame; `false` indicates it is not. |

#### func isRedirect()

```cangjie

public func isRedirect(): Bool
```

**Description:** Determines whether the resource request is redirected by the server.

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the resource request is redirected by the server. `true` indicates it is redirected; `false` indicates it is not. |

#### func isRequestGesture()

```cangjie

public func isRequestGesture(): Bool
```

**Description:** Determines whether the resource request is associated with a gesture (e.g., a click).

**System Capability:** SystemCapability.Web.Webview.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Whether the resource request is associated with a gesture. `true` indicates it is associated; `false` indicates it is not. |

### enum MixedMode

```cangjie
public enum MixedMode <: Equatable<MixedMode> {
    | All
    | Compatible
    | None
    | ...
}
```

**Description:** Sets the security loading mode for mixed content.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<MixedMode>

#### All

```cangjie
All
```

**Description:** Loose mode: Allows loading both HTTP and HTTPS mixed content. All insecure content can be loaded.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Compatible

```cangjie
Compatible
```

**Description:** Compatibility mode: Mixed content compatibility mode where some insecure content may be loaded.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### None

```cangjie
None
```

**Description:** Strict mode: Disallows loading HTTP and HTTPS mixed content. Prevents secure origins from loading insecure origin content.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### func !=(MixedMode)

```cangjie
public operator func !=(other: MixedMode): Bool
```

**Description:** Compares whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [MixedMode](#enum-mixedmode) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are not equal; otherwise, returns `false`. |

#### func ==(MixedMode)

```cangjie
public operator func ==(other: MixedMode): Bool
```

**Description:** Compares whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [MixedMode](#enum-mixedmode) | Yes | - | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal; otherwise, returns `false`. |## Sample Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.ArkWeb.*
import kit.PerformanceAnalysisKit.*

@Entry
@Component
class EntryView {
    let webController = WebviewController()
    @State var url: String = "www.example.com"
    func build() {
        Column(space: 10) {
            Button("refresh")
            .onClick {
                evt =>
                Hilog.info(0, "AppLogCj", "refresh")
                webController.refresh()
            }.width(400.px).height(150.px)
            Button("loadUrl")
            .onClick {
                evt =>
                Hilog.info(0, "AppLogCj", "loadUrl")
                webController.loadUrl(this.url)

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