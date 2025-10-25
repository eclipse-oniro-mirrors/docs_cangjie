# ohos.arkui.component_utils

Provides the capability to obtain the coordinates and dimensions of a component's drawing area.

## Import Module

```cangjie
import ohos.component_utils.*
import kit.ArkUI.*
```

## class ComponentInfo

```cangjie
public class ComponentInfo {
    public var size: Size
    public var localOffset: Offset
    public var windowOffset: Offset
    public var screenOffset: Offset
    public var translate: TranslateResult
    public var scale: ScaleResult
    public var rotate: RotateResult
    public var transform: VArray<Float32, $16>
    public init(size: Size, localOffset: Offset, windowOffset: Offset, screenOffset: Offset, translate: TranslateResult,
        scale: ScaleResult, rotate: RotateResult, transform: VArray<Float32, $16>)
}
```

**Description:** Information about the coordinate position and dimensions of a component instance object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var localOffset

```cangjie
public var localOffset: Offset
```

**Description:** Sets the component's information relative to its parent component.

**Type:** [Offset](#class-offset)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var rotate

```cangjie
public var rotate: RotateResult
```

**Description:** Sets the component's rotation information.

**Type:** [RotateResult](#class-rotateresult)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var scale

```cangjie
public var scale: ScaleResult
```

**Description:** Sets the component's scaling information.

**Type:** [ScaleResult](#class-scaleresult)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var screenOffset

```cangjie
public var screenOffset: Offset
```

**Description:** Sets the component's information relative to the screen.

**Type:** [Offset](#class-offset)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var size

```cangjie
public var size: Size
```

**Description:** Sets the component's dimensions.

**Type:** [Size](#class-size)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var transform

```cangjie
public var transform: VArray<Float32, $16>
```

**Description:** Sets the affine matrix information, creating a fourth-order matrix object based on the input parameters.

**Type:** VArray\<Float32,$16>

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var translate

```cangjie
public var translate: TranslateResult
```

**Description:** Sets the component's translation information.

**Type:** [TranslateResult](#class-translateresult)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var windowOffset

```cangjie
public var windowOffset: Offset
```

**Description:** Sets the component's information relative to the window.

**Type:** [Offset](#class-offset)

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Size, Offset, Offset, Offset, TranslateResult, ScaleResult, RotateResult, VArray\<Float32,$16>)

```cangjie
public init(size: Size, localOffset: Offset, windowOffset: Offset, screenOffset: Offset, translate: TranslateResult,
    scale: ScaleResult, rotate: RotateResult, transform: VArray<Float32, $16>)
```

**Description:** Constructs a ComponentInfo-type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name          | Type                              | Mandatory | Default | Description                                                                 |
|:--------------|:----------------------------------|:----------|:--------|:----------------------------------------------------------------------------|
| size          | [Size]                            | Yes       | -       | Component dimensions.                                                       |
| localOffset   | [Offset](#class-offset)           | Yes       | -       | Component's information relative to its parent component.                  |
| windowOffset  | [Offset](#class-offset)           | Yes       | -       | Component's information relative to the window.                            |
| screenOffset  | [Offset](#class-offset)           | Yes       | -       | Component's information relative to the screen.                            |
| translate     | [TranslateResult](#class-translateresult) | Yes       | -       | Component's translation information.                                        |
| scale         | [ScaleResult](#class-scaleresult) | Yes       | -       | Component's scaling information.                                            |
| rotate        | [RotateResult](#class-rotateresult) | Yes       | -       | Component's rotation information.                                           |
| transform     | VArray<Float32, $16>              | Yes       | -       | Affine matrix information, creating a fourth-order matrix object based on input parameters. |

## class ComponentUtils

```cangjie
public class ComponentUtils {}
```

**Description:** Provides the capability to obtain the coordinates and dimensions of a specified component's drawing area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### static func getRectangleById(String)

```cangjie
public static func getRectangleById(id: String): ComponentInfo
```

**Description:** Obtains the component instance object based on the component ID and synchronously returns the obtained coordinate position and dimensions to the developer through the component instance object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type   | Mandatory | Default | Description            |
|:-----|:-------|:----------|:--------|:-----------------------|
| id   | String | Yes       | -       | Specified component ID. |

**Return Value:**

| Type                          | Description                                                                 |
|:------------------------------|:----------------------------------------------------------------------------|
| [ComponentInfo](#class-componentinfo) | Component's dimensions, position, translation, scaling, rotation, and affine matrix attribute information. |

## class Offset

```cangjie
public class Offset {
    public var x: Float32
    public var y: Float32
    public init(x: Float32, y: Float32)
}
```

**Description:** Coordinate information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Description:** Sets the x-coordinate.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Description:** Sets the y-coordinate.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Float32, Float32)

```cangjie
public init(x: Float32, y: Float32)
```

**Description:** Constructs an Offset-type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type   | Mandatory | Default | Description                |
|:-----|:-------|:----------|:--------|:---------------------------|
| x    | Float32 | Yes       | -       | x-coordinate.<br>Unit: px. |
| y    | Float32 | Yes       | -       | y-coordinate.<br>Unit: px. |

## class RotateResult

```cangjie
public class RotateResult {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var centerX: Float32
    public var centerY: Float32
    public var angle: Float32
    /**
     * Defines RotateResult Type.
     */
    public init(x: Float32, y: Float32, z: Float32, centerX: Float32, centerY: Float32, angle: Float32)
}
```

**Description:** Component rotation information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var angle

```cangjie
public var angle: Float32
```

**Description:** Sets the rotation angle.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var centerX

```cangjie
public var centerX: Float32
```

**Description:** Sets the x-coordinate of the transformation center point.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var centerY

```cangjie
public var centerY: Float32
```

**Description:** Sets the y-coordinate of the transformation center point.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Description:** Sets the x-coordinate of the rotation axis vector.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Description:** Sets the y-coordinate of the rotation axis vector.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Description:** Sets the z-coordinate of the rotation axis vector.

**Type:** Float32

**Access:** Read-write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Float32, Float32, Float32, Float32, Float32, Float32)

```cangjie
/**
 * Defines RotateResult Type.
 */
public init(x: Float32, y: Float32, z: Float32, centerX: Float32, centerY: Float32, angle: Float32)
```

**Description:** Constructs a RotateResult-type object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name    | Type   | Mandatory | Default | Description                          |
|:--------|:-------|:----------|:--------|:-------------------------------------|
| x       | Float32 | Yes       | -       | x-coordinate of the rotation axis vector.<br>Unit: px. |
| y       | Float32 | Yes       | -       | y-coordinate of the rotation axis vector.<br>Unit: px. |
| z       | Float32 | Yes       | -       | z-coordinate of the rotation axis vector.<br>Unit: px. |
| centerX | Float32 | Yes       | -       | x-coordinate of the transformation center point.<br>Unit: px. |
| centerY | Float32 | Yes       | -       | y-coordinate of the transformation center point.<br>Unit: px. |
| angle   | Float32 | Yes       | -       | Rotation angle.<br>Unit: px.        |## class ScaleResult

```cangjie
public class ScaleResult {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var centerX: Float32
    public var centerY: Float32
    public init(x: Float32, y: Float32, z: Float32, centerX: Float32, centerY: Float32)
}
```

**Function:** Component scaling information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var centerX

```cangjie
public var centerX: Float32
```

**Function:** Sets the x-axis coordinate of the transformation center point.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var centerY

```cangjie
public var centerY: Float32
```

**Function:** Sets the y-axis coordinate of the transformation center point.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** Sets the scaling factor on the x-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Sets the scaling factor on the y-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Sets the scaling factor on the z-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Float32, Float32, Float32, Float32, Float32)

```cangjie
public init(x: Float32, y: Float32, z: Float32, centerX: Float32, centerY: Float32)
```

**Function:** Constructs a ScaleResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type    | Required | Default | Description |
|:----------|:--------|:---------|:--------|:------------|
| x         | Float32 | Yes      | -       | Scaling factor on the x-axis.<br>Unit: px. |
| y         | Float32 | Yes      | -       | Scaling factor on the y-axis.<br>Unit: px. |
| z         | Float32 | Yes      | -       | Scaling factor on the z-axis.<br>Unit: px. |
| centerX   | Float32 | Yes      | -       | x-axis coordinate of the transformation center point.<br>Unit: px. |
| centerY   | Float32 | Yes      | -       | y-axis coordinate of the transformation center point.<br>Unit: px. |

## class Size

```cangjie
public class Size {
    public var width: Float32
    public var height: Float32
    public init(width: Float32, height: Float32)
}
```

**Function:** Sets the component size.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var height

```cangjie
public var height: Float32
```

**Function:** Sets the component height.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var width

```cangjie
public var width: Float32
```

**Function:** Sets the component width.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Float32, Float32)

```cangjie
public init(width: Float32, height: Float32)
```

**Function:** Constructs an Offset object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type    | Required | Default | Description |
|:----------|:--------|:---------|:--------|:------------|
| width     | Float32 | Yes      | -       | Component width.<br>Unit: px. |
| height    | Float32 | Yes      | -       | Component height.<br>Unit: px. |

## class TranslateResult

```cangjie
public class TranslateResult {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public init(x: Float32, y: Float32, z: Float32)
}
```

**Function:** Component translation information.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** Sets the translation distance on the x-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Sets the translation distance on the y-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Sets the translation distance on the z-axis.

**Type:** Float32

**Readable/Writable:** Readable and Writable

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### init(Float32, Float32, Float32)

```cangjie
public init(x: Float32, y: Float32, z: Float32)
```

**Function:** Constructs a TranslateResult object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type    | Required | Default | Description |
|:----------|:--------|:---------|:--------|:------------|
| x         | Float32 | Yes      | -       | Translation distance on the x-axis.<br>Unit: px. |
| y         | Float32 | Yes      | -       | Translation distance on the y-axis.<br>Unit: px. |
| z         | Float32 | Yes      | -       | Translation distance on the z-axis.<br>Unit: px. |

**Example:**

<!-- run -->

```cangjie
package ohos_app_cangjie_entry
import kit.ArkUI.*
import ohos.arkui.state_macro_manage.*
import ohos.arkui.component_utils.ComponentUtils
import ohos.resource_manager.AppResource

@Entry
@Component
class EntryView {
    @State var message1: String = ""
    @State var message2: String = ""
    @State var message3: String = ""
    @State var x = 120
    @State var y = 10
    @State var z = 100
    func build() {
        Column {
            Image(@r(app.media.startIcon))
                .width(300)
                .height(100)
                .scale(x: 0.5, y: 0.5, z: 1.0)
                .translate(x: 20, y: 20, z: 20)
                .rotate(
                    x: 1.0,
                    y: 1.0,
                    z: 1.0,
                    centerX: 50,
                    centerY: 50,
                    angle: 300.0
                )
                .id("image")
            Button("getRectangleById").onClick ({
                evt =>
                let info = ComponentUtils.getRectangleById("image")
                message1 = info
                    .size
                    .width
                    .toString()
                message2 = info
                    .scale
                    .x
                    .toString()
                message3 = info
                    .rotate
                    .angle
                    .toString()
            })
            Text(this.message1 + this.message2 + this.message3)
                .margin(20)
                .width(300)
                .height(300)
                .borderWidth(2)
        }
    }
}
```

![componentutils](figures/componentutils.gif)