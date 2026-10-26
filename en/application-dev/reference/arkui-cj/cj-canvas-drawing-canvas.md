# Canvas

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Provides a canvas component for custom drawing of graphics.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Does not support child components.

## Creating the Component

### init(?CanvasRenderingContext2D)

```cangjie
public init(context: ?CanvasRenderingContext2D)
```

**Function:** Constructs a Canvas component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | ?[CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d) | Yes | - | Canvas context object. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Events

### func onReady(?() -> Unit)

```cangjie
public func onReady(callback: ?() -> Unit): This
```

**Function:** Event notification when the Canvas component construction is completed. At this point, drawing on the Canvas can begin.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?() -> Unit | No | { => } | Event callback. |

**Return Value:**

| Type | Description |
|:---|:---|
| This | Returns the current component instance. |

## Basic Type Definitions

### class RenderingContextSettings

```cangjie
public class RenderingContextSettings {
    public var antialias: ?Bool
    public init(antialias!: ?Bool = None)
}
```

**Function:** An object used to set related properties when creating a rendering context.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### var antialias

```cangjie
public var antialias: ?Bool
```

**Function:** Indicates whether the Canvas has anti-aliasing enabled. The default value is false.

**Type:** ?Bool

**Read-Write Capability:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### init(?Bool)

```cangjie
public init(antialias!: ?Bool = None)
```

**Function:** Creates a RenderingContextSettings object based on the anti-aliasing parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| antialias | ?Bool | No | None | **Named parameter.** Whether to enable anti-aliasing. |

### class TextMetrics

```cangjie
public class TextMetrics {
    public let width: Float64
    public let height: Float64
}
```

**Function:** Dimensions information of text.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### let width

```cangjie
public let width: Float64
```

**Function:** The width of the string, of type double.

**Type:** Float64

**Read-Write Capability:** Read-Only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### let height

```cangjie
public let height: Float64
```

**Function:** The height of the string, of type double.

**Type:** Float64

**Read-Write Capability:** Read-Only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### class CanvasGradient

```cangjie
public class CanvasGradient {
    public func addColorStop(offset: Float64, color: ?ResourceColor): Unit
}
```

**Function:** An opaque object describing a gradient, created by createLinearGradient() or createRadialGradient().

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

#### func addColorStop(Float64, ?ResourceColor)

```cangjie
public func addColorStop(offset: Float64, color: ?ResourceColor): Unit
```

**Function:** Adds a color stop defined by an offset and color to the gradient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| offset | Float64 | Yes | - | A value between 0 and 1. Values outside this range will throw an INDEX_SIZE_ERR error. |
| color | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Sets the gradient color. |

## Example Code

### Example 1 (Using Methods from CanvasRenderingContext2D)

This example demonstrates how to use methods from CanvasRenderingContext2D to draw on a Canvas component.

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

![canvas](./figures/drawingCanvas.PNG)