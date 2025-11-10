# Router

Provides functionality to access different pages through different URLs, including navigating to a specified page within the application, replacing the current page with another page within the same application, returning to the previous page, or navigating to a specified page.

> **Note:**
>
> The following APIs require obtaining the Router object first by using the [getRouter()](./cj-apis-uicontext-uicontext.md#func-getrouter) method from [UIContext](./cj-apis-uicontext-uicontext.md#class-uicontext), and then invoking the corresponding methods through this object.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Router

```cangjie
public class Router {}
```

**Functionality:** The routing class, providing capabilities to navigate to a specified page within the application, return to the previous page, or navigate to a specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### func pushUrl(String,String)

```cangjie
public func pushUrl(url!: String, params!: String = ""): Unit
```

**Functionality:** Navigates to a specified page within the application.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type   | Required | Default | Description |
|:---------|:-------|:---------|:--------|:------------|
| url      | String | Yes      | -       | **Named parameter.** The URL of the target page. |
| params   | String | No       | ""      | **Named parameter.** Data to be passed to the target page during navigation. The data becomes invalid when switching to another page. After navigating to the target page, use getParams() to retrieve the passed parameters. |

### func back(?String,String)

```cangjie
public func back(url!: ?String = None, params!: String = ""): Unit
```

**Functionality:** Returns to the previous page or a specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type    | Required | Default | Description |
|:---------|:--------|:---------|:--------|:------------|
| url      | ?String | No       | None    | **Named parameter.** The URL of the target page. |
| params   | String  | No       | ""      | **Named parameter.** Parameters to be carried when returning to the page. |

### func back(Int32,String)

```cangjie
public func back(index!: Int32, params!: String = ""): Unit
```

**Functionality:** Returns to a specified page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description |
|:---------|:------|:---------|:--------|:------------|
| index    | Int32 | Yes      | -       | **Named parameter.** The index value of the target page. Range: [0, +∞) |
| params   | String| No       | ""      | **Named parameter.** Parameters to be carried when returning to the page. |

### func getParams()

```cangjie
public func getParams(): Option<String>
```

**Functionality:** Retrieves the parameters passed from the initiating page to the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Return Value:**

| Type          | Description |
|:--------------|:------------|
| Option<String> | Parameters passed from the initiating page to the current page. |

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

**Functionality:** Page state information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### var index

```cangjie
public var index: Int32
```

**Functionality:** Represents the index of the current page in the page stack. From the bottom to the top of the stack, the index starts from 1 and increments.

**Type:** Int32

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### var name

```cangjie
public var name: String
```

**Functionality:** Represents the name of the current page, corresponding to the file name.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### var path

```cangjie
public var path: String
```

**Functionality:** Represents the path of the current page.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### var params

```cangjie
public var params: String
```

**Functionality:** Represents the parameters carried by the current page.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### init(Int32, String, String, String)

```cangjie
public init(
    index!: Int32,
    name!: String,
    path!: String,
    params!: String
)
```

**Functionality:** Creates a RouterState object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description |
|:---------|:------|:---------|:--------|:------------|
| index    | Int32 | Yes      | -       | **Named parameter.** The index of the current page in the page stack. From the bottom to the top of the stack, the index starts from 1 and increments. |
| name     | String| Yes      | -       | **Named parameter.** The name of the current page, corresponding to the file name. |
| path     | String| Yes      | -       | **Named parameter.** The path of the current page. |
| params   | String| Yes      | -       | **Named parameter.** The parameters carried by the current page. |

## enum RouterMode

```cangjie
public enum RouterMode <: Equatable<RouterMode> {
    | Standard
    | Single
    | ...
}
```

**Functionality:** Routing navigation modes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parent Type:**

- Equatable\<[RouterMode](#enum-routermode)>

### Standard

```cangjie
Standard
```

**Functionality:** Multi-instance mode, which is the default navigation mode. The target page is added to the top of the page stack, regardless of whether a page with the same URL exists in the stack. If no routing navigation mode is specified, the default multi-instance mode is used.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### Single

```cangjie
Single
```

**Functionality:** Single-instance mode. If the target page's URL already exists in the page stack, that URL page is moved to the top of the stack. If the target page's URL does not exist in the stack, the default multi-instance mode is used for navigation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

### operator func !=(RouterMode)

```cangjie
public operator func !=(other: RouterMode): Bool
```

**Functionality:** Compares whether two enum values are not equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type               | Required | Default | Description |
|:---------|:-------------------|:---------|:--------|:------------|
| other    | [RouterMode](#enum-routermode) | Yes      | -       | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns true if the two enum values are not equal, otherwise returns false. |

### operator func ==(RouterMode)

```cangjie
public operator func ==(other: RouterMode): Bool
```

**Functionality:** Compares whether two enum values are equal.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type               | Required | Default | Description |
|:---------|:-------------------|:---------|:--------|:------------|
| other    | [RouterMode](#enum-routermode) | Yes      | -       | The other enum value to compare. |

**Return Value:**

| Type | Description |
|:-----|:------------|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |
