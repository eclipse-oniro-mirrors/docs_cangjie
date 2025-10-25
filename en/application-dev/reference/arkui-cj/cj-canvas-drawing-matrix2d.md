# Matrix2D

A matrix object capable of performing transformations such as scaling, rotation, and translation.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class Matrix2D

```cangjie
public class Matrix2D {
    public init(unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
}
```

**Description:** Matrix object type.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop rotateX

```cangjie
public mut prop rotateX: Float64
```

**Description:** Horizontal skew coefficient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### prop rotateY

```cangjie
public mut prop rotateY: Float64
```

**Description:** Vertical skew coefficient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### prop scaleX

```cangjie
public mut prop scaleX: Float64
```

**Description:** Horizontal scaling coefficient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### prop scaleY

```cangjie
public mut prop scaleY: Float64
```

**Description:** Vertical scaling coefficient.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### prop translateX

```cangjie
public mut prop translateX: Float64
```

**Description:** Horizontal translation distance. Default unit: vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### prop translateY

```cangjie
public mut prop translateY: Float64
```

**Description:** Vertical translation distance. Default unit: vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-Write

**Since:** 21

### init(LengthMetricsUnit)

```cangjie
public init(unit!: LengthMetricsUnit = LengthMetricsUnit.Default)
```

**Description:** Creates a Matrix2D type matrix object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| unit | [LengthMetricsUnit](./cj-common-types.md#enum-lengthmetricsunit) | No | LengthMetricsUnit.Default | **Named parameter.** Configures the unit mode of the Matrix2D object. Once configured, it cannot be dynamically changed. Configuration method is the same as [CanvasRenderingContext2D](./cj-canvas-drawing-canvasrenderingcontext2d.md#class-canvasrenderingcontext2d). |

### func identity()

```cangjie
public func identity(): This
```

**Description:** Creates an identity matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func invert()

```cangjie
public func invert(): This
```

**Description:** Obtains the inverse matrix of the current matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func rotate(Float64, Float64, Float64)

```cangjie
public func rotate(degree: Float64, rx!: Float64 = 0.0, ry!: Float64 = 0.0): This
```

**Description:** Performs right-multiplication rotation operation on the current matrix centered at the rotation point.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| degree | Float64 | Yes | - | Rotation angle in degrees. Positive values indicate clockwise direction. Convert degrees to radians via degree * Math.PI / 180. Default unit: radians. |
| rx | Float64 | No | 0.0 | **Named parameter.** Horizontal coordinate of the rotation point. Default unit: vp. |
| ry | Float64 | No | 0.0 | **Named parameter.** Vertical coordinate of the rotation point. Default unit: vp. |

### func scale(Float64, Float64)

```cangjie
public func scale(sx!: Float64 = 1.0, sy!: Float64 = 1.0): This
```

**Description:** Performs right-multiplication scaling operation on the current matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| sx | Float64 | No | 1.0 | **Named parameter.** Horizontal scaling factor. |
| sy | Float64 | No | 1.0 | **Named parameter.** Vertical scaling factor. |

### func translate(Float64, Float64)

```cangjie
public func translate(tx!: Float64 = 0.0, ty!: Float64 = 0.0): This
```

**Description:** Performs left-multiplication translation operation on the current matrix.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| tx | Float64 | No | 0.0 | **Named parameter.** Horizontal translation distance. Default unit: vp. |
| ty | Float64 | No | 0.0 | **Named parameter.** Vertical translation distance. Default unit: vp. |

## Example Code

<!-- run -->

```cangjie

package ohos_app_cangjie_entry

import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*

@Entry
@Component
class EntryView {
    private let settings: RenderingContextSettings = RenderingContextSettings(antialias: true)
    private let context1: CanvasRenderingContext2D = CanvasRenderingContext2D(this.settings)
    private let matrix: Matrix2D = Matrix2D()

    func build() {
        Row {
            Canvas(this.context1)
                .width(240.vp)
                .height(180.vp)
                .backgroundColor(0xffff00)
                .onReady(
                    {
                        =>
                        this.context1.fillRect(100.0, 20.0, 50.0, 50.0)
                        this.matrix.scaleX = 1.0
                        this.matrix.scaleY = 1.0
                        this.matrix.rotateX = -0.5
                        this.matrix.rotateY = 0.5
                        this.matrix.translateX = 10.0
                        this.matrix.translateY = 10.0
                        this.context1.setTransform(this.matrix)
                        this.context1.fillRect(100.0, 20.0, 50.0, 50.0)
                    }
                )
        }.height(100.percent).width(100.percent)
    }
}
```

![matrix2D_1](./figures/matrix2D_1.png)