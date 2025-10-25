# CanvasPattern

An Object instance created using the `createPattern` method, which generates an image-filling template by specifying an image and repetition method.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class CanvasPattern

```cangjie
public class CanvasPattern {
    public init()
}
```

**Description:** An Object instance created using the `createPattern` method, which generates an image-filling template by specifying an image and repetition method.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### func setTransform(Matrix2D)

```cangjie
public func setTransform(transform: Matrix2D): Unit
```

**Description:** Applies a matrix transformation to the current CanvasPattern using a Matrix2D object as the parameter.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| transform | [Matrix2D] | Yes | - | Transformation matrix. |