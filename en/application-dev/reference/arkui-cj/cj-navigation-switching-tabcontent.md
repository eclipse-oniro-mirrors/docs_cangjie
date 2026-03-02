# TabContent

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Used exclusively within Tabs, corresponding to the content view of a switchable tab.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Supports a single child component.

> **Note:**
>
> Can embed system components and custom components, supports rendering control types ([if/else](../../arkui-cj/rendering_control/cj-rendering-control-ifelse.md), [ForEach](cj-state-rendering-foreach.md), and [LazyForEach](cj-state-rendering-lazyforeach.md)).

## Creating the Component

### init()

```cangjie
public init()
```

**Function:** Creates a TabContent container without child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a TabContent container with child components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | ()->Unit | Yes | - | Declares the child components within the container. |

## Common Attributes/Common Events

Common Attributes: All supported.

> **Note:**
>
> - The TabContent component does not support setting common width attributes; its width defaults to filling the parent Tabs component.
> - The TabContent component does not support setting common height attributes; its height is determined by the parent Tabs component and the TabBar component height.
> - When the vertical attribute is false, the above two restrictions are swapped.
> - The TabContent component does not support scrolling when content is too long. For scrolling, nest a List component inside.
> - It is recommended to use consistent parameter types for the tabBar attribute across all TabContent child components of the Tabs component.
> - If the TabContent contains focusable components, navigation between TabContent and TabBar components within the Tabs component is only controllable via keyboard arrow keys.

Common Events: All supported.

## Component Attributes

### func tabBar(?CustomBuilder)

```cangjie
public func tabBar(content: ?CustomBuilder): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| content | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Content displayed on the TabBar. Initial value: { => }. |

> **Note:**
>
> - If the set content exceeds the space provided by the TabBar, it will be clipped.
> - When passing [CustomBuilder](./cj-common-types.md#type-custombuilder) type parameters, use bind to manage the invocation of custom builder functions. For bind usage, see the bind function description in [Framework Interfaces](./cj-ui-framework.md).

### func tabBar(?ResourceStr)

```cangjie
public func tabBar(content: ?ResourceStr): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| content | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Content displayed on the TabBar. Initial value: "". |

> **Note:**
>
> If the set content exceeds the space provided by the TabBar, it will be clipped.

### func tabBar(?ResourceStr, ?ResourceStr)

```cangjie
public func tabBar(icon!: ?ResourceStr = None, text!: ?ResourceStr = None): This
```

**Function:** Sets the content displayed on the TabBar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| icon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** TabBar icon. Initial value: "". |
| text | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** TabBar text. Initial value: "". |

> **Note:**
>
> - The bottom tab style does not include an indicator.
> - If the icon fails to display, a gray blank block will be shown.

## Example Code

See [tabs](cj-navigation-switching-tabs.md)