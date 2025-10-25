# Disabled Control

Determines whether a component is interactive. When interactive, it responds to [click events](./cj-universal-event-click.md#), [touch events](./cj-universal-event-touch.md), [drag events](./cj-universal-event-drag.md), [key events](./cj-universal-event-key.md), [focus events](../../../en/application-dev/arkui-cj/cj-common-events-focus-event.md), [mouse events](./cj-universal-event-mouse.md), and [gesture events](./cj-universal-gesture-bind.md).

> **Note:**
>
> The disabled control property only takes effect when pressed. Changing the `enabled` property during an ongoing interaction will not take effect.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func enabled(Bool)

```cangjie
public func enabled(value: Bool): This
```

**Function:** Sets whether the component is enabled.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | Bool | Yes | - | Whether the component is enabled. |