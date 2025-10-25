# MenuItemGroup

This component is used to display grouped menu items (MenuItem).

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Contains [MenuItem](./cj-menu-menuitem.md) child components.

## Creating the Component

### init(ResourceStr, ResourceStr, () -> Unit)

```cangjie
public init(header!: CustomBuilder, footer!: CustomBuilder, child!: () -> Unit = {=>})
```

**Function:** Creates a group for displaying menu items (MenuItem).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| header | ResourceStr | No | "" | **Named parameter.** Sets the header display information for the corresponding group. |
| footer | ResourceStr | No | "" | **Named parameter.** Sets the footer display information for the corresponding group. |
| child | ()->Unit | No | { => } | **Named parameter.** Declares the child components within the container. |

### init(CustomBuilder, CustomBuilder, () -> Unit)

```cangjie
public init(header!: CustomBuilder, footer!: CustomBuilder, child!: () -> Unit = {=>})
```

**Function:** Creates a group for displaying menu items (MenuItem).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| header | CustomBuilder | Yes | - | **Named parameter.** Sets the header display information for the corresponding group. |
| footer | CustomBuilder | Yes | - | **Named parameter.** Sets the footer display information for the corresponding group. |
| child | ()->Unit | No | { => } | **Named parameter.** Declares the child components within the container. |

## Universal Attributes/Events

Universal Attributes: All supported.

Universal Events: All supported.

## Example Code

Example Code

For details, see the example in the [Menu](cj-menu-menu.md#example-code) component.