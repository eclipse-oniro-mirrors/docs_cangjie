# Focus Control

Custom component focus navigation effects, allowing configuration of whether a component can receive focus and the specific focus navigation order. Focus can be switched using the Tab key or arrow keys.

> **Note:**
>
> - Custom components inherently cannot receive focus. When setting properties such as [focusable](./cj-universal-attribute-focus.md#func-focusablebool) or [enabled](./cj-universal-attribute-enable.md#func-enabledbool) to false, or setting the [visibility](./cj-universal-attribute-visibility.md#func-visibilityvisibility) property to Hidden or None, it does not affect the ability of child components to receive focus.
> - A component actively acquiring focus is not controlled by window focus.
> - For focus development reference, see [Focus Development Guide](./cj-universal-event-focus.md).

## Import Module

```cangjie
import kit.ArkUI.*
```

## func defaultFocus(?Bool)

```cangjie
func defaultFocus(value: ?Bool): T
```

**Function:** Sets whether the current component is the default focus on the current page.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| value | ?Bool | Yes | - | Determines whether the current component is the default focus on the current page. Takes effect only when the page is first created and entered for the first time. <br/>Initial value: false. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that called this interface. |

## func focusable(?Bool)

```cangjie
func focusable(value: ?Bool): T
```

**Function:** Sets whether the current component can receive focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| value | ?Bool | Yes | - | Determines whether the current component can receive focus. true means the component can receive focus, false means it cannot. <br/>Initial value: true. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that called this interface. |

## func focusOnTouch(?Bool)

```cangjie
func focusOnTouch(value: ?Bool): T
```

**Function:** Sets whether the current component supports focus acquisition via touch.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| value | ?Bool | Yes | - | Determines whether the current component supports focus acquisition via touch. true means the component supports touch focus, false means it does not. <br/>Initial value: false. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that called this interface. |

## func groupDefaultFocus(?Bool)

```cangjie
func groupDefaultFocus(value: ?Bool): T
```

**Function:** Sets whether the current component is the default focus when its container receives focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| value | ?Bool | Yes | - | Determines whether the current component is the default focus when its container receives focus. Takes effect only when the container node is first created and receives focus for the first time. true means the current component is the default focus for its container, false means it is not. <br/>Initial value: false. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that called this interface. |

## func tabIndex(?Int32)

```cangjie
func tabIndex(index: ?Int32): T
```

**Function:** Customizes the component's focus navigation behavior using the Tab key.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| index | ?Int32 | Yes | - | Customizes the component's focus navigation behavior using the Tab key. If there are components with tabIndex greater than 0, Tab key navigation will only cycle through these components in ascending order of their tabIndex values. If no components have tabIndex greater than 0, components with tabIndex equal to 0 will follow the default focus navigation rules. <br/>Initial value: 0. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that called this interface. |

## class FocusControl

```cangjie
public class FocusControl {}
```

**Function:** Focus control module.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

### static func requestFocus(?String)

```cangjie
public static func requestFocus(value: ?String): Bool
```

**Function:** A global interface usable in method statements. Calling this interface actively transfers focus to the component specified by the parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** Version 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| value | ?String | Yes | - | The target component is identified using the interface key(value: string) or id(value: string) bound to a string. <br>Returns whether focus was successfully requested for the target component. If the target component exists and can receive focus, returns true; otherwise, returns false. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| Bool | Returns whether focus was successfully requested for the target component. If the target component exists and can receive focus, returns true; otherwise, returns false. |