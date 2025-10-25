# ohos.router (Page Routing)

This module provides the capability to access different pages through different URLs, including navigating to a specified page within the application, replacing the current page with another page within the same application, returning to the previous page or a specified page, etc.

> **Note:**
>
> - Page routing methods can only be called after the page rendering is complete. During the `onInit` and `onReady` lifecycle phases, the page is still in the rendering stage, and calling page routing methods is prohibited.
> - `ohos.router` only supports pure Cangjie scenarios and is not suitable for mixed development scenarios involving ArkTS and Cangjie.
> - This feature is only available in pure Cangjie mode.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Router

```cangjie
public class Router {}
```

**Description:** Page routing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func back(String, String)

```cangjie
public func back(url!: String, params!: String = "")
```

**Description:** Returns to the previous page or a specified page, deleting all pages between the current page and the specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description |
|:----------|:-------|:---------|:--------|:------------|
| url       | String | Yes      | -       | **Named parameter.** The URL of the target page. |
| params    | String | No       | ""      | **Named parameter.** Parameters to be carried when returning to the page. |

### func back(Int32, String)

```cangjie
public func back(index!: Int32, params!: String = "")
```

**Description:** Returns to the previous page or a specified page, deleting all pages between the current page and the specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description |
|:----------|:-------|:---------|:--------|:------------|
| index     | Int32  | Yes      | -       | **Named parameter.** The index value of the target page. From the bottom to the top of the stack, the index starts from 1 and increments. |
| params    | String | No       | ""      | **Named parameter.** Parameters to be carried when returning to the page. |

### func getParams()

```cangjie
public func getParams(): Option<String>
```

**Description:** Retrieves the parameters passed from the initiating page to the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Return Value:**

| Type           | Description |
|:---------------|:------------|
| Option\<String> | Parameters passed from the initiating page to the current page. |

### func push(String, String)

```cangjie
public func push(url!: String, params!: String = "")
```

**Description:** Navigates to a specified page within the application.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description |
|:----------|:-------|:---------|:--------|:------------|
| url       | String | Yes      | -       | **Named parameter.** The URL of the target page. |
| params    | String | No       | ""      | **Named parameter.** Data to be passed to the target page during routing. The data becomes invalid when switching to another page. After navigating to the target page, use `router.getParams()` to retrieve the passed parameters. Additionally, in the web-like paradigm, parameters can be directly used in the page, such as `this.keyValue` (where `keyValue` is the key in the `params` parameter during navigation). If the target page already has this field, its value will be overwritten by the passed value.<br>**Note:**<br>The `params` parameter cannot pass methods or objects returned by system interfaces (e.g., media interface definitions and returned `PixelMap` objects). Developers are advised to extract the basic type properties from the system interface's returned objects that need to be passed and construct a `String`-type JSON object for passing. |

## class RouterState

```cangjie
public class RouterState {
    public var index: Int32
    public var name: String
    public var path: String
    public var params: String
    public init(
        index!: Int32,
        name!: String,
        path!: String,
        params!: String
    )
}
```

**Description:** Page state information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var index

```cangjie
public var index: Int32
```

**Description:** The index of the current page in the page stack. From the bottom to the top of the stack, the index starts from 1 and increments.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var name

```cangjie
public var name: String
```

**Description:** The name of the current page, corresponding to the filename.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var params

```cangjie
public var params: String
```

**Description:** Parameters carried by the current page.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var path

```cangjie
public var path: String
```

**Description:** The path of the current page.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Int32, String, String, String)

```cangjie
public init(
    index!: Int32,
    name!: String,
    path!: String,
    params!: String
)
```

**Description:** Constructs a `RouterState` object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type   | Required | Default | Description |
|:----------|:-------|:---------|:--------|:------------|
| index     | Int32  | Yes      | -       | **Named parameter.** The index of the current page in the page stack. From the bottom to the top of the stack, the index starts from 1 and increments. |
| name      | String | Yes      | -       | **Named parameter.** The name of the current page, corresponding to the filename. |
| path      | String | Yes      | -       | **Named parameter.** The path of the current page. |
| params    | String | Yes      | -       | **Named parameter.** Parameters carried by the current page. |

## enum RouterMode

```cangjie
public enum RouterMode <: Equatable<RouterMode> {
    | Standard
    | Single
    | ...
}
```

**Description:** Routing navigation modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<RouterMode>

### Single

```cangjie
Single
```

**Description:** Single-instance mode. If the target page's URL already exists in the page stack, the corresponding page is moved to the top of the stack. If the target page's URL does not exist in the stack, navigation follows the default multi-instance mode.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### Standard

```cangjie
Standard
```

**Description:** Multi-instance mode, which is the default navigation mode. The target page is added to the top of the stack, regardless of whether a page with the same URL exists in the stack.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func !=(RouterMode)

```cangjie
public operator func !=(other: RouterMode): Bool
```

**Description:** Checks for inequality between authorization states.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                | Required | Default | Description |
|:----------|:--------------------|:---------|:--------|:------------|
| other     | [RouterMode](#enum-routermode) | Yes      | -       | Authorization state. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns `true` if the authorization states are different, otherwise `false`. |

### func ==(RouterMode)

```cangjie
public operator func ==(other: RouterMode): Bool
```

**Description:** Checks for equality between authorization states.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type                | Required | Default | Description |
|:----------|:--------------------|:---------|:--------|:------------|
| other     | [RouterMode](#enum-routermode) | Yes      | -       | Authorization state. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns `true` if the authorization states are the same, otherwise `false`. |

## Example Code

### Example 1 (Page Navigation)

This example demonstrates navigation between pages.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import kit.LocalizationKit.*
import ohos.arkui.ui_context.*

@Entry
@Component
class EntryView {
    @State var active: Bool = false
    func build() {
        Column() {
            Image(@r(app.media.startIcon)).width(50).height(50).onClick {
                e => getUIContext().getRouter().pushUrl(url: "Page1")
            }.sharedTransition("sharedImage",
                options: SharedTransitionOptions(duration: 800, curve: Curve.Linear, delay: 100))
        }
    }
}
```

<!-- run -->

```cangjie
// page1.cj
package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class Page1 {
    func build() {
        Column() {
            Text("This is Page1")
            Button("back()").onClick({
                evt => getUIContext().getRouter().back()
            })
        }
    }
}
```