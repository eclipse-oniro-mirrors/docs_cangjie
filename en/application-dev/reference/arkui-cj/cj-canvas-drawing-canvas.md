# Canvas

Provides a canvas component for custom drawing graphics.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Does not support child components.

## Creating the Component

### init(Option\<CanvasRenderingContext2D>)

```cangjie
public init(context: Option<CanvasRenderingContext2D>)
```

**Function:** Initializes a drawing canvas component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | Option<CanvasRenderingContext2D> | Yes | - | Multiple Canvas components cannot share the same [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d) object. For details, see [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Events

### func onReady(() -> Unit)

```cangjie
public func onReady(callback: () -> Unit): This
```

**Function:** Event callback when the Canvas component initialization is complete or when the Canvas component size changes.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| callback | () -> Unit | Yes | - | Event callback when the Canvas component initialization is complete or when the Canvas component size changes.<br>When this event is triggered, the canvas is cleared. After this event, the width and height of the Canvas component are determined and can be obtained. You can use Canvas-related APIs for drawing. When only the position of the Canvas component changes, only the [onAreaChange](./cj-ui-framework.md#func-onareachangeareaarea---unit) event is triggered, not the onReady event. The [onAreaChange](./cj-ui-framework.md#func-onareachangeareaarea---unit) event is triggered after the onReady event. |

## Basic Type Definitions

### class CanvasGradient

```cangjie
public class CanvasGradient {}
```

**Function:** Gradient object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

#### func addColorStop(Float64, ResourceColor)

```cangjie
public func addColorStop(offset: Float64, color: ResourceColor): Unit
```

**Function:** Sets gradient breakpoint values, including offset and color.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| offset | Float64 | Yes | - | Sets the position of the gradient point relative to the starting point as a proportion of the total length, ranging from 0 to 1. Setting offset < 0 or offset > 1 will have no gradient effect. |
| color | [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor) | Yes | - | Sets the gradient color. For the color format, refer to the string type description in [ResourceColor](../BasicServicesKit/cj-apis-base.md#interface-resourcecolor). If the color is not set in the correct format, there will be no gradient effect. |

### class RenderingContextSettings

```cangjie
public class RenderingContextSettings {
    public var antialias: Bool
    public init(antialias!: Bool = false)
}
```

**Function:** Used to configure parameters for the CanvasRenderingContext2D object, including whether to enable anti-aliasing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

#### var antialias

```cangjie
public var antialias: Bool
```

**Function:** Indicates whether the canvas has anti-aliasing enabled.

**Type:** Bool

**Read/Write Capability:** Readable and Writable

#### init(Bool)

```cangjie
public init(antialias!: Bool = false)
```

**Function:** Used to configure parameters for the CanvasRenderingContext2D object, including whether to enable anti-aliasing.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| antialias | Bool | No | false | **Named parameter.** Indicates whether the canvas has anti-aliasing enabled. Initial value: false |

### class TextMetrics

```cangjie
public class TextMetrics {
    public let width: Float64
    public let height: Float64
}
```

**Function:** Used to describe the dimensions of a text block.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

#### let height

```cangjie
public let height: Float64
```

**Function:** The height of the text block.

**Type:** Float64

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

#### let width

```cangjie
public let width: Float64
```

**Function:** The width of the text block.

**Type:** Float64

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 12

## Example Code

### Example 1 (Using Methods in CanvasRenderingContext2D)

This example demonstrates how to use methods in CanvasRenderingContext2D for drawing in a Canvas component.

<!-- run -->

```cangjie

package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    var settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
    var context: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)

    func build() {
        Flex(direction: FlexDirection.Column, alignItems: ItemAlign.Center,
            justifyContent: FlexAlign.Center) {
            Canvas(this.context).width(100.percent).height(100.percent).backgroundColor(0xffff00).onReady(
                {
                => this.context.fillRect(0.0, 30.0, 100.0, 100.0)
            })
        }.width(100.percent).height(100.percent)
    }
}
```