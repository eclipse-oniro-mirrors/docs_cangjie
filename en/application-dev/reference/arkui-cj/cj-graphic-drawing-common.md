# Common Attributes for Graphic Drawing

Common attributes for graphic drawing are currently supported by components such as [Circle](./cj-graphic-drawing-circle.md), [Ellipse](./cj-graphic-drawing-ellipse.md), [Line](./cj-graphic-drawing-line.md), [Path](./cj-graphic-drawing-path.md), [Rect](./cj-graphic-drawing-rect.md), and [Shape](./cj-graphic-drawing-shape.md).

## Import Module

```cangjie
import kit.ArkUI.*
```

## Component Attributes

### func fill(?ResourceColor)

```cangjie
public func fill(value: ?ResourceColor): T
```

**Function:** Sets the fill color of the area. Invalid values will be processed according to the initial value. When set simultaneously with the common attribute [foregroundColor](./cj-universal-attribute-foregroundcolor.md#func-foregroundcolorcoloringstrategy), the latter attribute takes effect.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Fill color. Initial value: Color.Black. |

### func fillOpacity(?Float64)

```cangjie
public func fillOpacity(value: ?Float64): T
```

**Function:** Sets the opacity of the fill area. The value range is [0.0, 1.0]. If the given value is less than 0.0, it will be set to 0.0; if greater than 1.0, it will be set to 1.0. Other invalid values will be processed as 1.0. A value of 1.0 represents full opacity, while 0.0 represents full transparency.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Float64 | Yes | - | Fill opacity. Initial value: 1.0. |

### func fillOpacity(?AppResource)

```cangjie
public func fillOpacity(value: ?AppResource): T
```

**Function:** Sets the opacity of the fill area. The value range is [0, 1]. If the given value is less than 0, it will be set to 0; if greater than 1, it will be set to 1. Other invalid values will be processed as 1. A value of 1 represents full opacity, while 0 represents full transparency.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Fill opacity. Initial value: 1.0. |

### func stroke(?ResourceColor)

```cangjie
public func stroke(value: ?ResourceColor): T
```

**Function:** Sets the border color. By default, there is no border. Invalid values will not draw the border.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Border color. Initial value: Color.Transparent. |

### func strokeDashArray(?Array\<Length>)

```cangjie
public func strokeDashArray(value: ?Array<Length>): T
```

**Function:** Sets the border dash pattern.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Array\<[Length](./cj-common-types.md#interface-length)> | Yes | - | Border dash array. Initial value: []. |

### func strokeDashOffset(?Length)

```cangjie
public func strokeDashOffset(value: ?Length): T
```

**Function:** Sets the offset of the starting point for border drawing. Invalid values will be processed according to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Border dash offset. Initial value: 0.vp. |

### func strokeLineCap(?LineCapStyle)

```cangjie
public func strokeLineCap(value: ?LineCapStyle): T
```

**Function:** Sets the style for drawing border endpoints.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[LineCapStyle](./cj-common-types.md#enum-linecapstyle) | Yes | - | Border line cap style. Initial value: LineCapStyle.Butt. |

### func strokeLineJoin(?LineJoinStyle)

```cangjie
public func strokeLineJoin(value: ?LineJoinStyle): T
```

**Function:** Sets the style for drawing border corners.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[LineJoinStyle](./cj-common-types.md#enum-linejoinstyle) | Yes | - | Border join style. Initial value: LineJoinStyle.Miter. |

### func strokeMiterLimit(?Float64)

```cangjie
public func strokeMiterLimit(miterLimit: ?Float64): T
```

**Function:** Sets the limit for the ratio of the miter length to the border width. The miter length represents the distance from the outer intersection point to the inner intersection point of the border. The border width is the value of the strokeWidth attribute. This attribute takes effect only when the strokeLineJoin attribute is set to LineJoinStyle.Miter.<br>The valid value range for this attribute should be greater than or equal to 1.0. Values in the range [0,1) will be processed as 1.0, and other invalid values will be processed according to the initial value.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| miterLimit | ?Float64 | Yes | - | The limit for the ratio of the miter length to the border width.<br>Initial value: 4.0. |

### func strokeOpacity(?Float64)

```cangjie
public func strokeOpacity(value: ?Float64): T
```

**Function:** Sets the opacity of the border. The value range is [0.0, 1.0]. If the given value is less than 0.0, it will be set to 0.0; if greater than 1.0, it will be set to 1.0. Other invalid values will be processed as 1.0.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Float64 | Yes | - | Border opacity. Initial value: 1.0. |

### func strokeOpacity(?AppResource)

```cangjie
public func strokeOpacity(value: ?AppResource): T
```

**Function:** Sets the opacity of the border.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[AppResource](../LocalizationKit/cj-apis-resource.md#class-appresource) | Yes | - | Border opacity. Initial value: 1.0. |

### func strokeWidth(?Length)

```cangjie
public func strokeWidth(value: ?Length): T
```

**Function:** Sets the border width.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Border width. Initial value: 1.vp. |

### func antiAlias(?Bool)

```cangjie
public func antiAlias(value: ?Bool): T
```

**Function:** Sets whether to enable anti-aliasing.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Bool | Yes | - | Whether to enable anti-aliasing. Initial value: true. |

## Example Code

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import ohos.base.*
import ohos.arkui.component.*
import ohos.arkui.state_management.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
	func build() {
		Column(space: 10) {
			Text("basic")
				.fontSize(11)
				.fontColor(0xCCCCCC)
				.width(320)
			Shape() {
				Rect()
					.width(300)
					.height(50)
				Ellipse()
					.width(300)
					.height(50)
					.offset(x: 0, y: 60)
				Path()
					.width(300)
					.height(10)
					.commands("M0 0 L900 0")
					.offset(x: 0, y: 120)
			}
			.width(350)
			.height(140)
			.viewPort(x: -2, y: -2, width: 304, height: 130)
			.fill(0x317AF7)
			.stroke(Color.Black)
			.strokeWidth(4)
			.strokeDashArray([20])
			.strokeDashOffset(10)
			.strokeLineCap(LineCapStyle.Round)
			.strokeLineJoin(LineJoinStyle.Round)
			.antiAlias(true)
			// Draw a 300 * 50 rectangle with a border at points (0, 0) and (-5, -5) in Shape. The reason for setting the viewport's starting position coordinates to negative values is that the default drawing starting point is the midpoint of the line width. To fully display the border, the viewport needs to be offset by half the line width.
			Shape() {
				Rect()
					.width(300)
					.height(50)
			}
			.width(350)
			.height(80)
			.viewPort(x: 0, y: 0, width: 320, height: 70)
			.fill(0x317AF7)
			.stroke(Color.Black)
			.strokeWidth(10)

			Shape() {
				Rect()
					.width(300)
					.height(50)
			}
			.width(350)
			.height(80)
			.viewPort(x: -5, y: -5, width: 320, height: 70)
			.fill(0x317AF7)
			.stroke(Color.Black)
			.strokeWidth(10)

			Text("path")
				.fontSize(11)
				.fontColor(0xCCCCCC)
				.width(320)
			// Draw a straight-line path at point (0, -5) in Shape, with color 0xEE8443, line width 10, and dash pattern 20.
			Shape() {
				Path()
					.width(300)
					.height(10)
					.commands("M0 0 L900 0")
			}
			.width(350)
			.height(20)
			.viewPort(x: 0, y: -5, width: 300, height: 20)
			.stroke(0xEE8443)
			.strokeWidth(10)
			.strokeDashArray([20])
			// Draw a straight-line path at point (0, -5) in Shape, with color 0xEE8443, line width 10, dash pattern 20, and left offset 10.
			Shape() {
				Path()
					.width(300)
					.height(10)
					.commands("M0 0 L900 0")
			}
			.width(350)
			.height(20)
			.viewPort(x: 0, y: -5, width: 300, height: 20)
			.stroke(0xEE8443)
			.strokeWidth(10)
			.strokeDashArray([20])
			.strokeDashOffset(10)
			// Draw a straight-line path at point (0, -5) in Shape, with color 0xEE8443, line width 10, and opacity 0.5.
			Shape() {
				Path()
					.width(300)
					.height(10)
					.commands("M0 0 L900 0")
			}
			.width(350)
			.height(20)
			.viewPort(x: 0, y: -5, width: 300, height: 20)
			.stroke(0xEE8443)
			.strokeWidth(10)
			.strokeOpacity(0.5)
			// Draw a straight-line path at point (0, -5) in Shape, with color 0xEE8443, line width 10, dash pattern 20, and rounded line ends.
			Shape() {
				Path()
					.width(300)
					.height(10)
					.commands("M0 0 L900 0")
			}
			.width(350)
			.height(20)
			.viewPort(x: 0, y: -5, width: 300, height: 20)
			.stroke(0xEE8443)
			.strokeWidth(10)
			.strokeDashArray([20])
			.strokeLineCap(LineCapStyle.Round)
			// Draw a closed path at point (-20, -5) in Shape, with fill color 0x317AF7, line width 10, border color 0xEE8443, and sharp corner style (initial value).
			Shape() {
				Path()
					.width(200)
					.height(60)
					.commands("M0 0 L400 0 L400 150 Z")
			}
			.width(300)
			.height(200)
			.viewPort(x: -20, y: -5, width: 310, height: 90)
			.fill(0x317AF7)
			.stroke(0xEE8443)
			.strokeWidth(10)
			.strokeLineJoin(LineJoinStyle.Miter)
			.strokeMiterLimit(5.0)
		}.width(100.percent).margin(top: 15)
	}
}
```