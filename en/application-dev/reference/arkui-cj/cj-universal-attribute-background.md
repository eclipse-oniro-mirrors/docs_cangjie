# Background Settings

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
| repeat | ?[ImageRepeat](./cj-common-types.md#enum-imagerepeat) | Yes | - | Image repeat mode. Initial value: ImageRepeat.NoRepeat |

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
func backgroundImagePosition(x!: ?Length = None, y!: ?Length = None): T
```

**Description:** Sets the position of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| x | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** X-axis position. Initial value: 0.vp |
| y | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Y-axis position. Initial value: 0.vp |

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
func backgroundImageSize(width!: ?Length = None, height!: ?Length = None): T
```

**Description:** Sets the width and height of the background image.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Image width. Initial value: 0.vp |
| height | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Image height. Initial value: 0.vp |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |