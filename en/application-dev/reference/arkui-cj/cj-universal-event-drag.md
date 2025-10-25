# Drag Event

Drag events refer to events triggered when a component is long-pressed and dragged.

> **Note:**
>
> Pre-installed resource files within the application (i.e., resource files existing in the HAP package before installation) only support intra-application local dragging.

The ArkUI framework provides default drag capabilities for the following components, supporting drag-out or drag-in responses. Developers can also customize drag responses by implementing generic drag events.

- Components with default drag-out capability (data can be dragged from these components): [Search](./cj-text-input-search.md), [TextInput](./cj-text-input-textinput.md), [TextArea](./cj-text-input-textarea.md), [RichEditor](./cj-text-input-richeditor.md), [Text](./cj-text-input-text.md), [Image](./cj-image-video-image.md). Developers can control the use of default drag capabilities by setting the `draggable` property of these components.

- Components with default drag-in capability (target components can respond to dragged-in data): [Search](./cj-text-input-search.md), [TextInput](./cj-text-input-textinput.md), [TextArea](./cj-text-input-textarea.md), [RichEditor](./cj-text-input-richeditor.md). Developers can disable the default drag-in capability by setting the `allowDrop` property of these components to `null`.

<!--RP1--><!--RP1End-->For other components, developers must set the `draggable` property to `true` and implement data transfer-related content in interfaces such as `onDragStart` to handle drag events correctly.

> **Note:**
>
> The `Text` component must be used in conjunction with [copyOption](./cj-text-input-search.md#func-copyoptioncopyoptions), setting `copyOptions` to either `CopyOptions.InApp` or `CopyOptions.LocalDevice`.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class DragInfo

```cangjie
public class DragInfo {
    public var extraParams: String
    public var touchPoint: Position
}
```

**Function:** Configuration type for drag action parameters.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var extraParams

```cangjie
public var extraParams: String
```

**Function:** Stores additional information for drag events.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var touchPoint

```cangjie
public var touchPoint: Position
```

**Function:** Stores coordinate information of the drag point.

**Type:** [Position](./cj-common-types.md#class-position)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## class DragItemInfo

```cangjie
public class DragItemInfo {
    public var pixelMap: PixelMap = PixelMap(0)
    public var builder: CustomBuilder = { => }
    public var extraInfo: String
    public init(pixelMap: PixelMap, builder: CustomBuilder, extraInfo: String)
}
```

**Function:** Information about the component displayed during the drag process.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var builder

```cangjie
public var builder: CustomBuilder = { => }
```

**Function:** Uses a custom builder for drawing. If `pixelMap` is set, this value is ignored.

**Type:** [CustomBuilder](./cj-common-types.md#type-custombuilder)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var extraInfo

```cangjie
public var extraInfo: String
```

**Function:** Configures the description of the drag item.

**Type:** String

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### var pixelMap

```cangjie
public var pixelMap: PixelMap = PixelMap(0)
```

**Function:** Sets the image displayed during the drag process.

**Type:** [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**Read-Write Capability:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### init(PixelMap, CustomBuilder, String)

```cangjie
public init(pixelMap: PixelMap, builder: CustomBuilder, extraInfo: String)
```

**Function:** Creates an object of type `DragItemInfo`.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| pixelMap | [PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap) | Yes | - | Sets the image displayed during the drag process. |
| builder | [CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Uses a custom builder for drawing. If `pixelMap` is set, this value is ignored. |
| extraInfo | String | Yes | - | Description of the drag item. |

## func onDragEnter((DragInfo) -> Unit)

```cangjie
public func onDragEnter(event: (DragInfo) -> Unit): This
```

**Function:** Triggered when dragging enters the component's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->Unit | Yes | - | Callback function triggered when dragging enters the component's bounds. |

## func onDragLeave((DragInfo) -> Unit)

```cangjie
public func onDragLeave(event: (DragInfo) -> Unit): This
```

**Function:** Triggered when dragging leaves the component's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->Unit | Yes | - | Callback function triggered when dragging leaves the component's bounds. |

## func onDragMove((DragInfo) -> Unit)

```cangjie
public func onDragMove(event: (DragInfo) -> Unit): This
```

**Function:** Triggered when dragging moves within the component's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->Unit | Yes | - | Callback function triggered when dragging moves within the component's bounds. |

## func onDragStart((DragInfo) -> DragItemInfo)

```cangjie
public func onDragStart(event: (DragInfo) -> DragItemInfo): This
```

**Function:** Triggered when the component bound to this event is dragged for the first time, after a long press duration ≥ 500ms and finger movement distance ≥ 10vp.

For components with default drag-out capability, if developers set `onDragStart`, the developer's `onDragStart` is executed first, and the system's default drag-out capability is determined based on the execution:

- If the developer returns a custom drag image, the system's default drag image is not used.
- If the developer sets drag data, the system's default drag data is not used.

Text components [Search](./cj-text-input-search.md), [TextInput](./cj-text-input-textinput.md), [TextArea](./cj-text-input-textarea.md), [RichEditor](./cj-text-input-richeditor.md) do not support custom drag images when dragging selected text content. When `onDragStart` is used with menu preview or with components that have default drag-out capability, custom content on the preview and menu items does not support dragging.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->[DragItemInfo](#class-dragiteminfo) | Yes | - | Callback function triggered when dragging starts. The input parameter is drag event information, including drag point coordinates. The return parameter is the component information displayed during the drag process. |

## func onDragStart((DragInfo) -> CustomBuilder)

```cangjie
public func onDragStart(event: (DragInfo) -> CustomBuilder): This
```

**Function:** Overloaded drag event. Triggered when the component bound to this event is dragged for the first time, after a long press duration ≥ 500ms and finger movement distance ≥ 10vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Callback function triggered when dragging starts. The input parameter is drag event information, including drag point coordinates. The return parameter is the component information displayed during the drag process, used in conjunction with `@Builder` and `bind` methods. |

## func onDragStart((DragInfo) -> Unit)

```cangjie
public func onDragStart(event: (DragInfo) -> Unit): This
```

**Function:** Overloaded drag event. Triggered when the component bound to this event is dragged for the first time, after a long press duration ≥ 500ms and finger movement distance ≥ 10vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->Unit | Yes | - | Callback function triggered when dragging starts. The input parameter is drag event information, including drag point coordinates. The return parameter is the component information displayed during the drag process. |

## func onDrop((DragInfo) -> Unit)

```cangjie
public func onDrop(event: (DragInfo) -> Unit): This
```

**Function:** The component bound to this event can serve as a drag release target. Triggered when the drag behavior stops within the component's bounds.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([DragInfo](#class-draginfo))->Unit | Yes | - | Callback function triggered when the drag behavior stops within the component's bounds. The input parameter is drag event information, including drag point coordinates. |