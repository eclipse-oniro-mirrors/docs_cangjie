# Disabled Control

Determines whether a component is interactive. When interactive, it responds to [click events](./cj-universal-event-click.md#), [touch events](./cj-universal-event-touch.md), [key events](./cj-universal-event-key.md), [focus events](../../arkui-cj/cj-common-events-focus-event.md), and [mouse events](./cj-universal-event-mouse.md).

> **Note:**
>
> The disabled control property only takes effect when pressed. Changing the `enabled` property during an ongoing interaction has no effect.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func enabled(?Bool)

```cangjie
func enabled(value: ?Bool): T
```

**Function:** Sets whether the component is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | `true`: The component is interactive and responds to operations like clicks.<br>`false`: The component is non-interactive and does not respond to operations like clicks.<br>Initial value: `true` |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |