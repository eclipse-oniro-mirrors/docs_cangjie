# NavDestination

Serves as the root container for subpages, used to display the content area of [Navigation](./cj-navigation-switching-navigation.md).

> **NOTE:**
>
> - The NavDestination component must be used in conjunction with Navigation as the root node of destination pages. When used alone, it can only function as a regular container component without routing-related capabilities.
> - If the lifecycle of intermediate pages in the page stack changes, the lifecycle events (onWillShow, onShown, onHidden, onWillDisappear) of the top Destination before navigation and after navigation will both be triggered last.
> - When NavDestination has no main/subtitle set and no back button, the title bar will not be displayed.

## Importing Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain child components.

## Creating Component

### init(() -> Unit)

```cangjie
public init(child!: () -> Unit = { => })
```

**Function:** Constructs a NavDestination container.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | No | { => } | **Named parameter.** Child components of the NavDestination container. |

## Common Attributes/Common Events

Common Attributes: Supports common attributes.

Setting layout-related attributes such as position and size is not recommended, as it may cause abnormal page display.

Common Events: All supported.

## Component Attributes

### func hideTitleBar(?Bool)

```cangjie
public func hideTitleBar(value: ?Bool): This
```

**Function:** Specifies whether to hide the title bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether to hide the title bar. Initial value: false. |

### func title(?CustomBuilder, ?NavigationTitleOptions)

```cangjie
public func title(value: ?CustomBuilder, options!: ?NavigationTitleOptions = None): This
```

**Function:** Sets the page title. When NavigationCustomTitle is used to set the height, the titleMode attribute does not take effect. When the title string is too long: (1) If no subtitle is set, the string will shrink, wrap to two lines, and then truncate with an ellipsis (...); (2) If a subtitle is set, the subtitle will shrink and then truncate with an ellipsis (...).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Page title. Initial value: {=>}. |
| options | ?[NavigationTitleOptions](./cj-navigation-switching-navigation.md#class-navigationtitleoptions) | No | None | **Named parameter.** Title bar options. |

### func title(?ResourceStr, ?NavigationTitleOptions)

```cangjie
public func title(value: ?ResourceStr, options!: ?NavigationTitleOptions = None): This
```

**Function:** Sets the page title. When NavigationCustomTitle is used to set the height, the titleMode attribute does not take effect. When the title string is too long: (1) If no subtitle is set, the string will shrink, wrap to two lines, and then truncate with an ellipsis (...); (2) If a subtitle is set, the subtitle will shrink and then truncate with an ellipsis (...).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Page title.<br>Initial value: {=>}. |
| options | ?[NavigationTitleOptions](./cj-navigation-switching-navigation.md#class-navigationtitleoptions) | No | None | **Named parameter.** Title bar options. |

## Component Events

### func onBackPressed(?() -> Bool)

```cangjie
public func onBackPressed(callback: ?() -> Bool): This
```

**Function:** This callback takes effect when there is content in the page stack bound to Navigation. When the back button is clicked, this event is triggered. A return value of true indicates overriding the back button logic, while false means navigating back to the previous page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?() -> Bool | Yes | - | Callback function triggered when the back button is clicked. A return value of true indicates overriding the back button logic, while false means navigating back to the previous page. Initial value: { => true }. |

### func onReady(?Callback\<NavDestinationContext, Unit>)

```cangjie
public func onReady(callback: ?Callback<NavDestinationContext, Unit>): This
```

**Function:** This event is triggered just before NavDestination constructs its child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback](./cj-common-types.md#type-callbackt-v)\<[NavDestinationContext](#class-navdestinationcontext), Unit> | Yes | - | Callback function triggered just before constructing child components. Initial value: { _ => }. |

## Basic Type Definitions

### class NavDestinationContext

```cangjie
public class NavDestinationContext {
    public var pathInfo: ?NavPathInfo
    public var pathStack: ?NavPathStack
    public var navDestinationId: ?String
}
```

**Function:** Context information for NavDestination.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### var navDestinationId

```cangjie
public var navDestinationId: ?String
```

**Function:** The unique ID of the current NavDestination, automatically generated by the system and unrelated to the component's common id attribute.

**Type:** ?String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### var pathInfo

```cangjie
public var pathInfo: ?NavPathInfo
```

**Function:** Parameters specified when navigating to NavDestination.

**Type:** ?[NavPathInfo](./cj-navigation-switching-navigation.md#class-navpathinfo)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

#### var pathStack

```cangjie
public var pathStack: ?NavPathStack
```

**Function:** The page stack in which the current NavDestination resides.

**Type:** ?[NavPathStack](./cj-navigation-switching-navigation.md#class-navpathstack)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since Version:** 22

## Example Code

For usage examples of NavDestination, refer to the [Navigation Example](./cj-navigation-switching-navigation.md#示例代码).