# Drag Control

Sets whether a component can respond to drag events.

> **Note:**
>
> The ArkUI framework provides default drag capabilities for the following components, supporting responses to data drag-out or drag-in operations. Developers can also customize drag responses by implementing generic drag events.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func dragPreview(String)

```cangjie
func dragPreview(value: String): T
```

**Function:** Sets the preview image during component dragging.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The preview image during component dragging. This method is responsible for setting the preview image, and its effect depends on other methods.<br/>When a component supports dragging and also has a preview image set via [bindContextMenu](./cj-universal-attribute-menu.md#func-bindcontextmenucustombuilder-responsetype-contextmenuoptions), the long-press floating preview image will prioritize the one set by [bindContextMenu](./cj-universal-attribute-menu.md#func-bindcontextmenucustombuilder-responsetype-contextmenuoptions).<br>When a String-type ID is passed, the screenshot of the corresponding component will be used as the preview image. If the component corresponding to the ID cannot be found, or if the component's [Visibility](./cj-common-types.md#enum-visibility) property is set to `None`/`Hidden`, the component itself will be screenshot for the drag preview. Currently, the screenshot does not include visual effects such as brightness, shadows, blur, or rotation.<br>Initial value: empty. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |