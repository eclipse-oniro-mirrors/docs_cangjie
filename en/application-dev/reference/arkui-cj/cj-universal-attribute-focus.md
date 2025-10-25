# Focus Control

Custom component focus navigation effects, allowing configuration of whether a component can receive focus and the specific focus navigation order, with focus switching via the Tab key or arrow keys.

> **Note:**
>
> - Custom components inherently lack focus acquisition capability. When properties such as [focusable](./cj-universal-attribute-focus.md#func-focusablebool), [enabled](./cj-universal-attribute-enable.md#func-enabledbool) are set to false, or when the [visibility](./cj-universal-attribute-visibility.md#func-visibilityvisibility) property is set to Hidden/None, this does not affect the focus acquisition capability of their child components.
> - A component actively acquiring focus is not controlled by window focus.

## Module Import

```cangjie
import kit.ArkUI.*
```

## func defaultFocus(Bool)

```cangjie
public func defaultFocus(value: Bool): This
```

**Function:** Sets whether the component is the default focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the component is the default focus. |

## func focusOnTouch(Bool)

```cangjie
public func focusOnTouch(value: Bool): This
```

**Function:** Sets whether the component acquires focus upon touch.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the component supports focus acquisition via touch. true indicates the component supports touch-based focus acquisition, false indicates it does not.<br>Initial value: false.<br>**Note:**<br>Focus can only be acquired normally when the component is clickable. |

## func focusable(Bool)

```cangjie
public func focusable(value: Bool): This
```

**Function:** Sets whether the component can acquire focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the component can acquire focus. true indicates the component can acquire focus, false indicates it cannot.<br>**Note:**<br>Components with default interaction logic such as [Button](./cj-button-picker-button.md), [TextInput](./cj-text-input-textinput.md) are focusable by default, while components like [Text](./cj-text-input-text.md), [Image](./cj-image-video-image.md) are non-focusable by default. In non-focusable state, focus events cannot be triggered. |

## func groupDefaultFocus(Bool)

```cangjie
public func groupDefaultFocus(value: Bool): This
```

**Function:** Sets whether the group is the default focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the current component is the default focus when its container acquires focus, effective only during the container node's initial focus acquisition. true indicates the current component is the container's default focus, false indicates it is not.<br>Initial value: false <br>**Note:**<br>Must be used in conjunction with tabIndex. When a container has [tabIndex](./cj-universal-attribute-focus.md#func-tabindexint32) set and a child component (or the container itself) has groupDefaultFocus(true), focus will automatically transfer to the specified component when the container first acquires focus via Tab key. If multiple components (including the container) within the container have groupDefaultFocus(true), the first component found during depth-first traversal of the component tree will be selected. |

## func tabIndex(Int32)

```cangjie
public func tabIndex(index: Int32): This
```

**Function:** Sets the component's Tab index.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| index | Int32 | Yes | - | Tab index value. |

## Basic Type Definitions

### class FocusControl

```cangjie
public class FocusControl {}
```

**Function:** Focus control module.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### static func requestFocus(String)

```cangjie
public static func requestFocus(value: String): Bool
```

**Function:** Global interface available in method statements. Calling this interface actively transfers focus to the component specified by the parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The string bound to the target component using either the key(value: string) or id(value: string) interface.<br/>Returns whether focus was successfully requested for the target component. Returns true if the target component exists and is focusable, otherwise returns false. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns whether focus was successfully requested for the target component. Returns true if the target component exists and is focusable, otherwise returns false. |