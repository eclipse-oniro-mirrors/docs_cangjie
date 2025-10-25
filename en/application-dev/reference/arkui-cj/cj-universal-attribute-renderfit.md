# Component Content Filling Mode

Determines how the final component content is rendered on the component during width/height animations.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func renderFit(RenderFit)

```cangjie
public func renderFit(fitMode: RenderFit): This
```

**Function:** Sets the rendering adaptation mode of the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fitMode | [RenderFit](#enum-renderfit) | Yes | - | Rendering adaptation mode. |

## func !=(RenderFit)

```cangjie
public operator func !=(other: RenderFit): Bool
```

**Function:** Determines whether two enumeration values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RenderFit](#enum-renderfit) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

## func ==(RenderFit)

```cangjie
public operator func ==(other: RenderFit): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [RenderFit](#enum-renderfit) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

## Basic Type Definitions

### enum RenderFit

```cangjie
public enum RenderFit <: Equatable<RenderFit> {
    | CENTER
    | TOP
    | BOTTOM
    | LEFT
    | RIGHT
    | TOP_LEFT
    | TOP_RIGHT
    | BOTTOM_LEFT
    | BOTTOM_RIGHT
    | RESIZE_FILL
    | RESIZE_CONTAIN
    | RESIZE_CONTAIN_TOP_LEFT
    | RESIZE_CONTAIN_BOTTOM_RIGHT
    | RESIZE_COVER
    | RESIZE_COVER_TOP_LEFT
    | RESIZE_COVER_BOTTOM_RIGHT
    | ...
}
```

**Function:** Component content filling style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<RenderFit>

#### BOTTOM

```cangjie
BOTTOM
```

**Function:** Maintains the final animation content size while keeping the content bottom-center aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### BOTTOM_LEFT

```cangjie
BOTTOM_LEFT
```

**Function:** Maintains the final animation content size while keeping the content bottom-left aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### BOTTOM_RIGHT

```cangjie
BOTTOM_RIGHT
```

**Function:** Maintains the final animation content size while keeping the content bottom-right aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### CENTER

```cangjie
CENTER
```

**Function:** Maintains the final animation content size while keeping the content center aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### LEFT

```cangjie
LEFT
```

**Function:** Maintains the final animation content size while keeping the content left aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_CONTAIN

```cangjie
RESIZE_CONTAIN
```

**Function:** Scales the final animation content while maintaining aspect ratio to ensure complete display within the component, keeping center alignment.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_CONTAIN_BOTTOM_RIGHT

```cangjie
RESIZE_CONTAIN_BOTTOM_RIGHT
```

**Function:** Scales the final animation content while maintaining aspect ratio to ensure complete display within the component. When width space remains, content stays right aligned; when height space remains, content stays bottom aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_CONTAIN_TOP_LEFT

```cangjie
RESIZE_CONTAIN_TOP_LEFT
```

**Function:** Scales the final animation content while maintaining aspect ratio to ensure complete display within the component. When width space remains, content stays left aligned; when height space remains, content stays top aligned.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_COVER

```cangjie
RESIZE_COVER
```

**Function:** Scales the final animation content while maintaining aspect ratio so that content dimensions are greater than or equal to component dimensions, keeping center alignment while displaying the central portion.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_COVER_BOTTOM_RIGHT

```cangjie
RESIZE_COVER_BOTTOM_RIGHT
```

**Function:** Scales the final animation content while maintaining aspect ratio so that content dimensions exactly match or exceed component dimensions. When width exceeds, content stays right aligned (displaying right portion); when height exceeds, content stays bottom aligned (displaying bottom portion).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_COVER_TOP_LEFT

```cangjie
RESIZE_COVER_TOP_LEFT
```

**Function:** Scales the final animation content while maintaining aspect ratio so that content dimensions exactly match or exceed component dimensions. When width exceeds, content stays left aligned (displaying left portion); when height exceeds, content stays top aligned (displaying top portion).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RESIZE_FILL

```cangjie
RESIZE_FILL
```

**Function:** Ignores the aspect ratio of final animation content, always scaling content to match component dimensions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### RIGHT

```cangjie
RIGHT
```

**Function:** Maintains the final animation content size while keeping the content right aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### TOP

```cangjie
TOP
```

**Function:** Maintains the final animation content size while keeping the content top-center aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### TOP_LEFT

```cangjie
TOP_LEFT
```

**Function:** Maintains the final animation content size while keeping the content top-left aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### TOP_RIGHT

```cangjie
TOP_RIGHT
```

**Function:** Maintains the final animation content size while keeping the content top-right aligned with the component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21