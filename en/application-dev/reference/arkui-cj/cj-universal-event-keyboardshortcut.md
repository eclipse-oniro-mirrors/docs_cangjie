# Component Keyboard Shortcut Events

Developers can set custom key combinations for components, with each component supporting multiple key combinations.

Even if a component is not focused or not displayed on its current page, it will respond to custom key combinations as long as it is mounted on the component tree of the focused window.

When setting key combinations, developers can also define custom events. Pressing the key combination will trigger the custom event. If no custom event is set, the key combination behavior will be consistent with the click behavior.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func keyboardShortcut(FunctionKey, Array\<ModifierKey>)

```cangjie
public func keyboardShortcut(value: FunctionKey, keys: Array<ModifierKey>): This
```

**Function:** Sets custom key combinations for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [FunctionKey](./cj-common-types.md#enum-functionkey) | Yes | - | A single character for the hotkey (characters that can be input via keyboard). |
| keys | Array\<[ModifierKey](./cj-common-types.md#enum-modifierkey)> | Yes | - | Key combination for the hotkey. |

## func keyboardShortcut(String, Array\<ModifierKey>)

```cangjie
public func keyboardShortcut(value: String, keys: Array<ModifierKey>): This
```

**Function:** Sets custom key combinations for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | A single character for the hotkey (characters that can be input via keyboard). |
| keys | Array\<[ModifierKey](./cj-common-types.md#enum-modifierkey)> | Yes | - | Key combination for the hotkey. Can be empty only when value is FunctionKey. |

## func keyboardShortcut(FunctionKey, Array\<ModifierKey>, () -> Unit)

```cangjie
public func keyboardShortcut(value: FunctionKey, keys: Array<ModifierKey>, action: () -> Unit): This
```

**Function:** Sets custom key combinations for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [FunctionKey](./cj-common-types.md#enum-functionkey) | Yes | - | FunctionKey for the hotkey. |
| keys | Array\<[ModifierKey](./cj-common-types.md#enum-modifierkey)> | Yes | - | Key combination for the hotkey. Can be empty only when value is FunctionKey. |
| action | () -> Unit | Yes | - | Callback for the custom event triggered when the key combination is successfully pressed. |

## func keyboardShortcut(String, Array\<ModifierKey>, () -> Unit)

```cangjie
public func keyboardShortcut(value: String, keys: Array<ModifierKey>, action: () -> Unit): This
```

**Function:** Sets custom key combinations for components.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | A single character for the hotkey (characters that can be input via keyboard). |
| keys | Array\<[ModifierKey](./cj-common-types.md#enum-modifierkey)> | Yes | - | Key combination for the hotkey. Can be empty only when value is FunctionKey. |
| action | () -> Unit | Yes | - | Callback for the custom event triggered when the key combination is successfully pressed. |