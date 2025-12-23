# ImageBitmap

The ImageBitmap object can store pixel data rendered by a canvas.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class ImageBitmap

```cangjie
public class ImageBitmap{
    public init(?String)
}
```

**Description:** The ImageBitmap object can store pixel data rendered by a canvas.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop width

```cangjie
public prop width: Float64
```

**Description:** The pixel width of the ImageBitmap. The default unit is vp.

**Type:** Float64

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### prop height

```cangjie
public prop height: Float64
```

**Description:** The pixel height of the ImageBitmap. The default unit is vp.

**Type:** Float64

**Access:** Read-only

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### init(?String)

```cangjie
public init(src: ?String)
```

**Description:** Constructs an ImageBitmap object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | ?String | No | - | Path to the image object. |

## Example Code

```cangjie
public class ImageBitmap{
    public init(src: String)
}
```