# Safe Area

The safe area refers to the display area of a page that, by default, does not overlap with system-defined non-safe areas such as the status bar or navigation bar. By default, interfaces developed by developers are laid out within the safe area. Property methods are provided to allow developers to extend component rendering beyond the safe area constraints. The [expandSafeArea](./cj-universal-attribute-expandsafearea.md#func-expandsafeareaarraysafeareatype-arraysafeareaedge) attribute enables components to extend their rendering area beyond the safe area without altering the layout. The [setKeyboardAvoidMode](./cj-universal-attribute-expandsafearea.md#func-setkeyboardavoidmodevalue-keyboardavoidmode) method configures the page's avoidance mode when a virtual keyboard pops up. For components like title bars where text should not overlap with non-safe areas, it is recommended to set the `expandSafeArea` attribute to achieve an immersive effect. Alternatively, the immersive mode can be directly enabled via the window interface [setWindowLayoutFullScreen](./cj-apis-window.md#).

## Import Module

```cangjie
import kit.ArkUI.*
```

## func expandSafeArea(?Array\<SafeAreaType>, ?Array\<SafeAreaEdge>)

```cangjie
public func expandSafeArea(types!: ?Array<SafeAreaType> = None, edges!: ?Array<SafeAreaEdge> = None): This
```

**Function:** Configures a component to extend its safe area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| types | ?Array\<[SafeAreaType](./cj-common-types.md#enum-safeareatype)> | No | None | **Named parameter.** Configures the type of safe area to extend. <br/>Initial value: [SafeAreaType.System, SafeAreaType.Cutout, SafeAreaType.Keyboard]. |
| edges | ?Array\<[SafeAreaEdge](./cj-common-types.md#enum-safeareatype)> | No | None | **Named parameter.** Configures the direction to extend the safe area. <br/>Initial value: [SafeAreaEdge.Top, SafeAreaEdge.Bottom, SafeAreaEdge.Start, SafeAreaEdge.End]. |

> **Notes:**
>
> - When using the `expandSafeArea` attribute to extend component rendering, it is recommended not to set fixed width and height for the component (except for percentages). If fixed dimensions are set, only [SafeAreaEdge.TOP, SafeAreaEdge.START] directions are supported for safe area extension, and the component size remains unchanged.
> - The safe area does not constrain the layout or size of internal components and does not clip them.
> - The `expandSafeArea` attribute does not take effect if the parent container is a scrollable container.
> - When `expandSafeArea()` is called without parameters, default values are applied. Calling `expandSafeArea([],[])` with empty arrays renders the attribute ineffective.
> - Conditions for the `expandSafeArea` attribute to take effect:
>   1. When `type` is `SafeAreaType.KEYBOARD`, it takes effect by default, and the component does not avoid the keyboard.
>   2. For other `type` settings, the component can extend into the safe area if its boundary coincides with the safe area. For example, if the device's status bar height is 100, the component's absolute position on the screen must satisfy `0 <= y <= 100`.
> - When a component extends into the safe area, events such as clicks may be intercepted by the system, prioritizing responses for system components like the status bar.
> - It is not recommended to set the `expandSafeArea` attribute for components within scrollable containers. If necessary, ensure all direct ancestor nodes up to the scrollable container are also configured with `expandSafeArea`; otherwise, the attribute may become ineffective after scrolling (see example).
> - The `expandSafeArea` attribute applies only to the current component and does not propagate to parent or child components. Thus, all relevant components must be configured accordingly.
> - When both `expandSafeArea` and `position` attributes are set, `position` takes effect first, followed by `expandSafeArea`. For components without `position` or `offset` attributes, `expandSafeArea` will not take effect if the component boundary does not overlap with the avoidance area (e.g., pop-ups or semi-modal components).
> - For scenarios where `expandSafeArea` cannot take effect, manual adjustment of component coordinates is required to place components in the avoidance area.