# MenuItemGroup

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This component is used to display grouped menu items (MenuItem).

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Contains [MenuItem](./cj-menu-menuitem.md) child components.

## Creating the Component

### init(?CustomBuilder, ?CustomBuilder, () -> Unit)

```cangjie
public init(header!: ?CustomBuilder, footer!: ?CustomBuilder, child!: () -> Unit = {=>})
```

**Function:** Creates a group for displaying menu items (MenuItem).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| header | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | **Named parameter.** Sets the header display information for the corresponding group. Initial value: { => }. |
| footer | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | **Named parameter.** Sets the footer display information for the corresponding group. Initial value: { => }. |
| child | () -> Unit | No | {=>} | **Named parameter.** Declares the child components within the container. |

> **Note:**
>
> When passing [CustomBuilder](./cj-common-types.md#type-custombuilder) type parameters, use bind to manage the invocation of custom builder functions. For bind usage, see the bind function description in [Framework Interfaces](./cj-ui-framework.md).

### init(?ResourceStr, ?ResourceStr, () -> Unit)

```cangjie
public init(header!: ?ResourceStr = None, footer!: ?ResourceStr = None, child!: () -> Unit = {=>})
```

**Function:** Creates a group for displaying menu items (MenuItem).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| header | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the header display information for the corresponding group. Initial value: "". |
| footer | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the footer display information for the corresponding group. Initial value: "". |
| child | () -> Unit | No | {=>} | **Named parameter.** Declares the child components within the container. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Example Code

Example Code

Refer to the [Menu](cj-menu-menu.md#example-code) component example for details.