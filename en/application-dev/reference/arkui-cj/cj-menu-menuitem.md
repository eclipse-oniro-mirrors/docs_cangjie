# MenuItem

Used to display specific menu items in the Menu component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(() -> Unit)

```cangjie
public init(child!: () -> Unit = {=>}) 
```

**Function:** Constructs a menu item with a secondary menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| child | ()->Unit | No | { => } | **Named parameter.** Custom UI description. Use with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and bind method. |

### init(ResourceStr, ResourceStr, ResourceStr, ResourceStr, Option\<() -> Unit>)

```cangjie
public init(startIcon!: ResourceStr, content!: ResourceStr, endIcon!: ResourceStr, labelInfo!: ResourceStr,
    builder!: Option<() -> Unit> = None)
```

**Function:** Constructs a menu item with a secondary menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| startIcon | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Path of the icon displayed on the left side of the item. |
| content | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Content information of the item. |
| endIcon | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Path of the icon displayed on the right side of the item. |
| labelInfo | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Defines the end label information, such as shortcuts like Ctrl+C. |
| builder | Option\<()->Unit> | No | None | **Named parameter.** Custom UI description. Use with [@Builder](../../../en/application-dev/arkui-cj/paradigm/cj-macro-builder.md) and bind method. |

## Common Attributes/Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func contentFont(Length, FontWeight, String, FontStyle)

```cangjie
public func contentFont(
    size!: Length = 16.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: String = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the font style of the content information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | **Named parameter.** Sets the text size. When Length is Int64 or Float64, uses fp unit. Percentage settings are not supported. |
| weight | FontWeight | No | FontWeight.Normal | **Named parameter.** Sets the font weight of the text. |
| family | String | No | "HarmonyOS Sans" | **Named parameter.** Sets the font list of the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. Currently supports 'HarmonyOS Sans' font and [custom font registration](cj-apis-font.md). |
| style | FontStyle | No | FontStyle.Normal | **Named parameter.** Sets the font style of the text. |

### func contentFont(Length, FontWeight, ResourceColor, FontStyle)

```cangjie
public func contentFont(
    size!: Length = 16.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: ResourceColor = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the font style of the content information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | **Named parameter.** Sets the text size. When Length is Int64 or Float64, uses fp unit. Percentage settings are not supported. |
| weight | FontWeight | No | FontWeight.Normal | **Named parameter.** Sets the font weight of the text. |
| family | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "HarmonyOS Sans" | **Named parameter.** Sets the font list of the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. Currently supports 'HarmonyOS Sans' font and [custom font registration](cj-apis-font.md). |
| style | FontStyle | No | FontStyle.Normal | **Named parameter.** Sets the font style of the text. |

### func contentFontColor(ResourceColor)

```cangjie
public func contentFontColor(value: ResourceColor): This
```

**Function:** Sets the font color of the content information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Font color of the content information in the menu item.<br/>Initial value: 0xE5000000 |

### func labelFont(Length, FontWeight, String, FontStyle)

```cangjie
public func labelFont(
    size!: Length = 16.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: String = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the font style of the label information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | **Named parameter.** Sets the text size. When Length is Int64 or Float64, uses fp unit. Percentage settings are not supported. |
| weight | FontWeight | No | FontWeight.Normal | **Named parameter.** Sets the font weight of the text. |
| family | String | No | "HarmonyOS Sans" | **Named parameter.** Sets the font list of the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. |
| style | FontStyle | No | FontStyle.Normal | **Named parameter.** Sets the font style of the text. |

### func labelFont(Length, FontWeight, ResourceStr, FontStyle)

```cangjie
public func labelFont(
    size!: Length = 16.vp,
    weight!: FontWeight = FontWeight.Normal,
    family!: ResourceStr = "HarmonyOS Sans",
    style!: FontStyle = FontStyle.Normal
): This
```

**Function:** Sets the font style of the label information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | No | 16.vp | **Named parameter.** Sets the text size. When Length is Int64 or Float64, uses fp unit. Percentage settings are not supported. |
| weight | FontWeight | No | FontWeight.Normal | **Named parameter.** Sets the font weight of the text. |
| family | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "HarmonyOS Sans" | **Named parameter.** Sets the font list of the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. |
| style | FontStyle | No | FontStyle.Normal | **Named parameter.** Sets the font style of the text. |

### func labelFontColor(ResourceColor)

```cangjie
public func labelFontColor(value: ResourceColor): This
```

**Function:** Sets the font color of the label information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Font color of the label information in the menu item.<br/>Initial value: '0x99000000' |

### func selectIcon(Bool)

```cangjie
public func selectIcon(value: Bool): This
```

**Function:** Sets whether to display the selected icon when the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether to display the selected icon when the menu item is selected.<br/>Initial value: false<br/>true: Displays the default checkmark icon when the menu item is selected.<br/>false: Does not display any icon even if the menu item is selected. |

### func selectIcon(ResourceStr)

```cangjie
public func selectIcon(value: ResourceStr): This
```

**Function:** Sets whether to display the selected icon when the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Displays the specified icon when the menu item is selected. |

### func selected(Bool)

```cangjie
public func selected(value: Bool): This
```

**Function:** Sets whether the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the menu item is selected.<br/>Initial value: false.<br/>When true, the menu item is selected. When false, the menu item is not selected. |

## Component Events

### func onChange((Bool) -> Unit)

```cangjie
public func onChange(callback: (Bool) -> Unit): This
```

**Function:** Triggered when the selected state changes. The onChange event is only triggered when manually triggered and the MenuItem state changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | (Bool)->Unit | Yes | - | Callback triggered when the selected state changes.<br/>Returns true when selected, and false when not selected. |

## Example Code

Refer to the [Menu](cj-menu-menu.md#example-code) component example.