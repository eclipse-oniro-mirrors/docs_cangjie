# Background Settings

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Configure the background style of components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func backgroundColor(?ResourceColor)

```cangjie
func backgroundColor(value: ?ResourceColor): T
```

**Description:** Sets the background color of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Background color. Initial value: Color.Transparent |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImage(?ResourceStr)

```cangjie
func backgroundImage(src: ?ResourceStr): T
```

**Description:** Sets the background image of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Image resource path. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImage(?ResourceStr, ?ImageRepeat)

```cangjie
func backgroundImage(src: ?ResourceStr, repeat: ?ImageRepeat): T
```

**Description:** Sets the background image and repeat mode of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| src | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | Yes | - | Image resource path. |
| repeat | ?[ImageRepeat](./cj-common-types.md#enum-imagerepeat) | Yes | - | Image repeat mode. Initial value: ImageRepeat.NoRepeat<br>**Note:** When a valid [backgroundImageResizable](#func-backgroundimageresizableresizableoptions) is set, this parameter does not take effect. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImagePosition(?Alignment)

```cangjie
func backgroundImagePosition(value: ?Alignment): T
```

**Description:** Sets the alignment of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[Alignment](./cj-common-types.md#enum-alignment) | Yes | - | Alignment mode. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImagePosition(?Length, ?Length)

```cangjie
func backgroundImagePosition(x!: ?Length, y!: ?Length): T
```

**Description:** Sets the position of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** X-axis position. Initial value: 0.vp |
| y | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Y-axis position. Initial value: 0.vp |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImageResizable(?ResizableOptions)

```cangjie
func backgroundImageResizable(value: ?ResizableOptions): T
```

**Description:** Sets the resizable options for background image stretching, that is, defining the stretchable area and fixed area of the image to implement a 9-patch-like slicing stretch effect. When a valid [ResizableOptions](./cj-common-types.md#class-resizableoptions) is set, the repeat parameter in the [backgroundImage](#func-backgroundimageresourcestr) attribute does not take effect.

> **Note:**
>
> - Only the slice field in ResizableOptions takes effect. The attribute takes effect only when both bottom and right of the slice field are greater than 0; when top + bottom is greater than the height of the original image or left + right is greater than the width of the original image, the attribute setting does not take effect.
> - When value is None, the background image is stretched as the original image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 26.1.0

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResizableOptions](./cj-common-types.md#class-resizableoptions) | Yes | - | Resizable image options for image stretching. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImageSize(?ImageSize)

```cangjie
func backgroundImageSize(value: ?ImageSize): T
```

**Description:** Sets the size of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | ?[ImageSize](./cj-common-types.md#enum-imagesize) | Yes | - | Image size. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func backgroundImageSize(?Length, ?Length)

```cangjie
func backgroundImageSize(width!: ?Length, height!: ?Length): T
```

**Description:** Sets the width and height of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Image width. Initial value: 0.vp |
| height | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Image height. Initial value: 0.vp |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |