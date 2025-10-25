# Drag Control

Sets whether a component can respond to drag events.

> **Note:**
>
> The ArkUI framework provides default drag capabilities for the following components, supporting responses to data drag-out or drag-in operations. Developers can also customize drag responses by implementing generic drag events.
>
> - Components with default drag-out capability (can drag data out from the component): [Search](./cj-text-input-search.md), [TextInput](./cj-text-input-textinput.md), [TextArea](./cj-text-input-textarea.md), [RichEditor](./cj-text-input-richeditor.md), [Text](./cj-text-input-text.md), [Image](./cj-image-video-image.md). Developers can control the use of default drag capabilities by setting the `draggable` property of these components.
>
> - Components with default drag-in capability (target component can respond to dragged-in data): [Search](./cj-text-input-search.md), [TextInput](./cj-text-input-textinput.md), [TextArea](./cj-text-input-textarea.md), [RichEditor](./cj-text-input-richeditor.md).
>
> <!--RP1--><!--RP1End-->For other components, developers need to set the `draggable` property to `true` and implement data transfer-related content in interfaces such as `onDragStart` to properly handle drag operations.
>
> The `Text` component must be used in conjunction with [copyOption](./cj-text-input-text.md#func-copyoptioncopyoptions), setting `copyOptions` to either `CopyOptions.InApp` or `CopyOptions.LocalDevice`.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func dragPreview(String)

```cangjie
public func dragPreview(value: String): This
```

**Function:** Sets the drag preview.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | Component ID. |