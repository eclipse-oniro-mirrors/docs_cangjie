# Border Settings

Configure the border style of components.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func border(?Length, ?ResourceColor, ?Length, ?BorderStyle)

```cangjie
public func border(width!: ?Length, color!: ?ResourceColor = None, radius!: ?Length = None,
    style!: ?BorderStyle = Option.None): T
```

**Function:** Sets the border style of the component. 

> **Note:**
>
> When color and radius are omitted, to ensure that borderColor and borderRadius take effect, they must be specified after border.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| width | ?[Length](./cj-common-types.md#interface-length) | Yes | - | **Named parameter.** Border width. Initial value: 0.vp |
| color | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | No | None | **Named parameter.** Border color. Initial value: Color.Black |
| radius | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Border radius. Initial value: 0.vp |
| style | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | No | Option.None | **Named parameter.** Border style. Initial value: BorderStyle.Solid |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderColor(?ResourceColor)

```cangjie
public func borderColor(value: ?ResourceColor): T
```

**Function:** Sets the border color of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | Border color. Initial value: Color.Black |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderRadius(?Length)

```cangjie
public func borderRadius(value: ?Length): T
```

**Function:** Sets the border radius of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Border radius. Initial value: 0.0.vp |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderRadius(?Length, ?Length, ?Length, ?Length)

```cangjie
public func borderRadius(topLeft!: ?Length = None, topRight!: ?Length = None, bottomLeft!: ?Length = None,
    bottomRight!: ?Length = None): T
```

**Function:** Sets the border radius for each corner of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| topLeft | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Top-left corner radius. Initial value: 0.vp |
| topRight | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Top-right corner radius. Initial value: 0.vp |
| bottomLeft | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Bottom-left corner radius. Initial value: 0.vp |
| bottomRight | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Bottom-right corner radius. Initial value: 0.vp |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderStyle(?BorderStyle)

```cangjie
public func borderStyle(value: ?BorderStyle): T
```

**Function:** Sets the border style of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[BorderStyle](./cj-common-types.md#enum-borderstyle) | Yes | - | Border style value. Initial value: BorderStyle.Solid |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderWidth(?EdgeWidths)

```cangjie
public func borderWidth(value: ?EdgeWidths): T
```

**Function:** Sets the border width of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[EdgeWidths](./cj-common-types.md#class-edgewidths) | Yes | - | Edge widths. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

## func borderWidth(?Length)

```cangjie
public func borderWidth(value: ?Length): T
```

**Function:** Sets the border width of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[Length](./cj-common-types.md#interface-length) | Yes | - | Border width. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |