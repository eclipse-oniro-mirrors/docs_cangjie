# Path

A path drawing component that generates closed custom shapes based on drawn paths.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

None

## Creating the Component

### init(ResourceStr)

```cangjie
public init(commands!: ResourceStr = "")
```

**Function:** Creates a path drawing component based on the path drawing command string.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| commands | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The command string for path drawing. |

### init(Length, Length, ResourceStr)

```cangjie
public init(width!: Length, height!: Length, commands!: ResourceStr = "")
```

**Function:** Creates a path drawing component based on the width and height of the rectangle where the path is located.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** The width of the rectangle where the path is located, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or missing, it will be processed according to the width required by its own content. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** The height of the rectangle where the path is located, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or missing, it will be processed according to the height required by its own content. |
| commands | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | No | "" | **Named parameter.** The command string for path drawing. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func commands(ResourceStr)

```cangjie
public func commands(commands: ResourceStr): This
```

**Function:** Sets the command string that conforms to the [SVG Path Description Specification](#svg-path-description-specification), with units in px. For pixel unit conversion methods, refer to [Pixel Unit Conversion](./cj-common-types.md#pixel-unit-conversion).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| commands | [ResourceStr](../BasicServicesKit/cj-apis-base.md#interface-resourcestr) | Yes | - | The command string for path drawing. Initial value: "", abnormal values are processed as the initial value. |

### func initial()

```cangjie
public override func initial()
```

**Function:** For UI framework use.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

## Basic Type Definitions

### class PathShape

```cangjie
public class PathShape <: BaseShape {
    public init(commands!: ResourceStr = "")
    public init(width!: Length, height!: Length, commands!: ResourceStr = "")
}
```

**Function:** Creates a path drawing component based on the path drawing command string.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- [BaseShape](./cj-graphic-drawing-shape.md#class-baseshape)

#### init(ResourceStr)

```cangjie
public init(commands!: ResourceStr = "")
```

**Function:** Creates a path drawing component based on the path drawing command string.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| commands | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** The command string for path drawing. |

#### init(Length, Length, ResourceStr)

```cangjie
public init(width!: Length, height!: Length, commands!: ResourceStr = "")
```

**Function:** Creates a path drawing component based on the width and height of the rectangle where the path is located.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| width | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** The width of the rectangle where the path is located, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or missing, it will be processed according to the width required by its own content. |
| height | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | **Named parameter.** The height of the rectangle where the path is located, value range ≥0.<br>Default unit: vp.<br>If the value is abnormal or missing, it will be processed according to the height required by its own content. |
| commands | [ResourceStr](./cj-common-types.md#interface-resourcestr) | No | "" | **Named parameter.** The command string for path drawing. |

## SVG Path Description Specification

The commands supported by the SVG path description specification are as follows:

| Command | Name | Parameters | Description |
|:---|:---|:---|:---|
| M | moveto | (x y) | Starts a new subpath at the given (x,y) coordinates. For example, `M 0 0` sets (0,0) as the starting point of the new subpath. |
| L | lineto | (x y) | Draws a line from the current point to the given (x,y) coordinates, which becomes the new current point. For example, `L 50 50` draws a line from the current point to (50,50) and sets (50,50) as the new starting point of the subpath. |
| H | horizontal lineto | x | Draws a horizontal line from the current point, equivalent to the L command with the y coordinate set to 0. For example, `H 50` draws a line from the current point to (50,0) and sets (50,0) as the new starting point of the subpath. |
| V | vertical lineto | y | Draws a vertical line from the current point, equivalent to the L command with the x coordinate set to 0. For example, `V 50` draws a line from the current point to (0,50) and sets (0,50) as the new starting point of the subpath. |
| C | curveto | (x1 y1 x2 y2 x y) | Draws a cubic Bézier curve from the current point to (x,y) using (x1,y1) as the control point at the start of the curve and (x2,y2) as the control point at the end of the curve. For example, `C100 100 250 100 250 200` draws a cubic Bézier curve from the current point to (250,200) and sets (250,200) as the new starting point of the subpath. |
| S | smooth curveto | (x2 y2 x y) | Draws a cubic Bézier curve from the current point to (x,y) using (x2,y2) as the control point at the end of the curve. If the previous command was C or S, the control point at the start is the reflection of the control point at the end of the previous command relative to the start point. For example, `C100 100 250 100 250 200 S400 300 400 200` sets the starting control point of the second Bézier curve as (250,300). If there is no previous command or the previous command was not C or S, the first control point coincides with the current point. |
| Q | quadratic Bézier curve | (x1 y1 x y) | Draws a quadratic Bézier curve from the current point to (x,y) using (x1,y1) as the control point. For example, `Q400 50 600 300` draws a quadratic Bézier curve from the current point to (600,300) and sets (600,300) as the new starting point of the subpath. |
| T | smooth quadratic Bézier curveto | (x y) | Draws a quadratic Bézier curve from the current point to (x,y). If the previous command was Q or T, the control point is the reflection of the control point at the end of the previous command relative to the start point. For example, `Q400 50 600 300 T1000 300` sets the control point of the second Bézier curve as (800,350). If there is no previous command or the previous command was not Q or T, the first control point coincides with the current point. |
| A | elliptical Arc | (rx ry x-axis-rotation large-arc-flag sweep-flag x y) | Draws an elliptical arc from the current point to (x,y). The size and orientation of the ellipse are defined by two radii (rx,ry) and x-axis-rotation, indicating how the entire ellipse is rotated relative to the current coordinate system (in degrees). The large-arc-flag and sweep-flag determine how the arc is drawn. |
| Z | closepath | none | Closes the current subpath by connecting it back to the initial point of the current subpath. |

For example: `commands("M0 20 L50 50 L50 100 Z")` defines a triangle starting at (0,20), drawing a line from (0,20) to (50,50), then from (50,50) to (50,100), and finally closing the path by drawing a line from (50,100) back to (0,20), forming a closed triangle.

## Example Code

Examples of drawing straight lines, straight-line shapes, and curved shapes.

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    func build() {
        Column {
            Text("Straight line")
                .size(width: 50.percent, height: 25.vp)
                .fontSize(20)
                .margin(10.vp)
            // Draw a straight line with length 600px and width 3vp
            Path()
                .width(600.px)
                .height(10.px)
                .commands("M0 0 L600 0")
                .stroke(Color.Black)
                .strokeWidth(3)

            Text('Straight line graph')
                .fontSize(20)
                .size(width: 50.percent, height: 25.vp)
                .margin(10.vp)
            // Draw straight-line shapes
            Flex(direction: FlexDirection.Row, alignItems: ItemAlign.Center, wrap: FlexWrap.Wrap) {
                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M100 0 L200 240 L0 240 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)

                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M0 0 H200 V200 H0 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)

                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M100 0 L0 100 L50 200 L150 200 L200 100 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)
            }.width(90.percent)

            Text('Curve graphics')
                .fontSize(20)
                .size(width: 50.percent, height: 25.vp)
                .margin(10.vp)
            Flex(direction: FlexDirection.Row, alignItems: ItemAlign.Center, wrap: FlexWrap.Wrap) {
                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M0 300 S100 0 240 300 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)

                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M0 150 C0 100 140 0 200 150 L100 300 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)

                Path()
                    .width(210.px)
                    .height(310.px)
                    .commands("M0 100 A30 20 20 0 0 200 100 Z")
                    .fillOpacity(0.0)
                    .stroke(Color.Black)
                    .strokeWidth(3)
            }.width(90.percent)
        }.width(100.percent)
    }
}
```

![path](./figures/path.png)