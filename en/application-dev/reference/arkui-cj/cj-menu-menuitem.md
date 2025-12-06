# MenuItem

Used to display specific menu items within a Menu component.

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

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | No | {=>} | **Named parameter.** Custom UI description. Used in combination with [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) and [bind](cj-ui-framework.md#func-bindcustomview---viewbuilder-customview) methods. |

### init(?ResourceStr, ?ResourceStr, ?ResourceStr, ?ResourceStr, Option\<() -> Unit>)

```cangjie
public init(startIcon!: ?ResourceStr, content!: ?ResourceStr, endIcon!: ?ResourceStr, labelInfo!: ?ResourceStr,
    builder!: Option<() -> Unit> = None)
```

**Function:** Constructs a menu item with a secondary menu.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| startIcon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Path to the icon displayed on the left side of the item. Initial value: "". |
| content | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Content information of the item. Initial value: "". |
| endIcon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Path to the icon displayed on the right side of the item. Initial value: "". |
| labelInfo | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | **Named parameter.** Defines the end label information, such as shortcuts like Ctrl+C. Initial value: "". |
| builder | Option\<() -> Unit> | No | None | **Named parameter.** Custom UI description. Used in combination with [@Builder](../../arkui-cj/paradigm/cj-macro-builder.md) and [bind](cj-ui-framework.md#func-bindcustomview---viewbuilder-customview) methods. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func contentFont(?Length, ?FontWeight, ?ResourceStr, ?FontStyle)

```cangjie
public func contentFont(
    size!: ?Length = None,
    weight!: ?FontWeight = None,
    family!: ?ResourceStr = None,
    style!: ?FontStyle = None
): This
```

**Function:** Sets the font style for the content information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the text size. When Length is Int64 or Float64, the unit is fp. Percentage settings are not supported. Initial value: 16.vp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Sets the font weight of the text. Initial value: FontWeight.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the font list for the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. Currently supports 'HarmonyOS Sans' font and [custom font registration](./cj-apis-uicontext-font.md). Initial value: "HarmonyOS Sans". |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Sets the font style of the text. Initial value: FontStyle.Normal. |

### func contentFontColor(?ResourceColor)

```cangjie
public func contentFontColor(value: ?ResourceColor): This
```

**Function:** Sets the font color for the content information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Font color for the content information in the menu item. Initial value: 0xE5000000. |

### func labelFont(?Length, ?FontWeight, ?ResourceStr, ?FontStyle)

```cangjie
public func labelFont(
    size!: ?Length = None,
    weight!: ?FontWeight = None,
    family!: ?ResourceStr = None,
    style!: ?FontStyle = None
): This
```

**Function:** Sets the font style for the label information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Sets the text size. When Length is Int64 or Float64, the unit is fp. Percentage settings are not supported. Initial value: 16.vp. |
| weight | ?[FontWeight](./cj-common-types.md#enum-fontweight) | No | None | **Named parameter.** Sets the font weight of the text. Initial value: FontWeight.Normal. |
| family | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Sets the font list for the text. Multiple fonts can be specified, separated by commas, with priority in order. Example: 'Arial, HarmonyOS Sans'. Initial value: "HarmonyOS Sans". |
| style | ?[FontStyle](./cj-common-types.md#enum-fontstyle) | No | None | **Named parameter.** Sets the font style of the text. Initial value: FontStyle.Normal. |

### func labelFontColor(?ResourceColor)

```cangjie
public func labelFontColor(value: ?ResourceColor): This
```

**Function:** Sets the font color for the label information in the menu item.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Font color for the label information in the menu item. Initial value: 0x99000000. |

### func selected(?Bool)

```cangjie
public func selected(value: ?Bool): This
```

**Function:** Sets whether the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether the menu item is selected. Initial value: false. |

### func selectIcon(?Bool)

```cangjie
public func selectIcon(value: ?Bool): This
```

**Function:** Sets whether to display the selected icon when the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether to display the selected icon when the menu item is selected. Initial value: false. |

### func selectIcon(?ResourceStr)

```cangjie
public func selectIcon(value: ?ResourceStr): This
```

**Function:** Sets the icon to be displayed when the menu item is selected.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Icon to be displayed when the menu item is selected. Initial value: "". |

## Component Events

### func onChange(?(Bool) -> Unit)

```cangjie
public func onChange(callback: ?(Bool) -> Unit): This
```

**Function:** Triggered when the selected state changes. The onChange event is only triggered when manually triggered and the MenuItem state changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?(Bool) -> Unit | Yes | - | Callback triggered when the selected state changes. Initial value: { res: Bool => }. |

## Example Code

Refer to the [Menu](cj-menu-menu.md#example-code) component example.