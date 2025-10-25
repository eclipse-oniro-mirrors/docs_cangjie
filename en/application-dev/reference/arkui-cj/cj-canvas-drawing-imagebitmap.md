# ImageBitmap

The ImageBitmap object can store pixel data rendered by a canvas.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ImageBitmap

```cangjie
public class ImageBitmap {
    public init(src: String)
    public init(src: String, width: Float64, height: Float64)
    public init(src: String, width: Int64, height: Int64)
    public init(date: PixelMap, unit!: LengthMetricsUnit = LengthMetricsUnit.DEFAULT)
    public init(date: String, unit: LengthMetricsUnit)
}
```

**Description:** The ImageBitmap object can store pixel data rendered by a canvas.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### prop height

```cangjie
public prop height: Float64
```

**Description:** The pixel height of the ImageBitmap. The default unit is vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-only

**Since:** 21

### prop width

```cangjie
public prop width: Float64
```

**Description:** The pixel width of the ImageBitmap. The default unit is vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Type:** Float64

**Access:** Read-only

**Since:** 21

### init(String)

```cangjie
public init(src: String)
```

**Description:** Constructs an ImageBitmap object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | String | Yes | - | The image data source supports local images.<br>1. The string format is used to load local images, such as ImageBitmap("common/images/example.jpg"). For Modules of type "entry" and "feature", the starting point of the image loading path is the current Module's ets folder. For Modules of type "har" and "shared", the starting point is the ets folder of the currently built "entry" or "feature" type Module. For Modules of type "har" and "shared", it is recommended to use the ImageSource image decoding method to decode resource images into a unified PixelMap for loading.<br>2. Supported local image types: bmp, jpg, png, svg, and webp. |

## Example Code

```cangjie
public class ImageBitmap {
    public init(src: String)
}
```