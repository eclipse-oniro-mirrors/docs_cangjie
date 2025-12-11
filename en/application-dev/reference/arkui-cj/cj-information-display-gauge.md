# Gauge

A gauge chart component that displays data in a circular (ring-style) format.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Can contain child components.

## Creating the Component

### init(?Float32, ?Float32, ?Float32, () -> Unit)

```cangjie
public init(value!: ?Float32, min!: ?Float32 = None, max!: ?Float32 = None, child!: () -> Unit = { => })
```

**Function:** Creates a gauge chart component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Float32 | Yes | - | **Named parameter.** Initial value: 0.0. The current data value of the gauge, indicating the pointer position. Used to preset the initial value when creating the component.<br>**Note:**<br>If value is outside the min and max range, min is used as the default value. |
| min | ?Float32 | No | None | **Named parameter.** Initial value: 0.0. The minimum value of the current data segment. |
| max | ?Float32 | No | None | **Named parameter.** Initial value: 100.0. The maximum value of the current data segment.<br>**Note:**<br>If max is less than min, the default values 0.0 and 100.0 are used.<br>Negative values are supported for max and min. |
| child | ()->Unit | No | { => } | **Named parameter.** Declares the child components of the current component. |

## Common Attributes/Common Events

Common attributes: All supported.

Common events: All supported.

## Component Attributes

### func colors(?Array\<(ResourceColor, Int32)>)

```cangjie
public func colors(value: ?Array<(ResourceColor, Int32)>): This
```

**Function:** Sets the colors of the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Array\<([ResourceColor](./cj-common-types.md#interface-resourcecolor), Int32)> | Yes | - | The colors of the gauge, supporting segmented color settings. |

### func colors(?Array\<(LinearGradient, Int32)>)

```cangjie
public func colors(value: ?Array<(LinearGradient, Int32)>): This
```

**Function:** Sets the segmented gradient color groups for the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Array\<([LinearGradient](cj-information-display-datapanel.md#class-lineargradient), Int32)> | Yes | - | The gradient colors of the gauge, supporting segmented color settings, up to 9 groups. LinearGradient type is defined in the datapanel component, and Int32 represents the width range of the segment color. |

### func colors(?LinearGradient)

```cangjie
public func colors(value: ?LinearGradient): This
```

**Function:** Sets the segmented gradient color groups for the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[LinearGradient](./cj-information-display-datapanel.md#class-lineargradient) | Yes | - | The gradient colors of the gauge, supporting segmented color settings, up to 9 groups. |

### func colors(?ResourceColor)

```cangjie
public func colors(value: ?ResourceColor): This
```

**Function:** Sets the color of the gauge.

If the parameter type is ResourceColor, the ring type is a single-color ring.

If the parameter type is LinearGradient, the ring type is a gradient ring.

If the parameter type is an array, the ring type is a segmented gradient ring. The first parameter is the color value. If set to a non-color type, it defaults to "0xFFE84026". The second parameter is the weight of the color. If set to a negative or non-numeric value, the weight defaults to 0.

The maximum number of segments for a segmented gradient ring is 9. If more than 9 segments are provided, the excess segments will not be displayed.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?[ResourceColor](./cj-common-types.md#interface-resourcecolor) | Yes | - | The colors of the gauge, supporting segmented color settings. |

### func description(?CustomBuilder)

```cangjie
public func description(builder: ?CustomBuilder): This
```

**Function:** Sets the description content of the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| builder | ?[CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | The description content. The content in @Builder is customizable by the developer, and text is recommended.<br>Initial value: { => }. |

### func endAngle(?Float32)

```cangjie
public func endAngle(angle: ?Float32): This
```

**Function:** Sets the end angle position.

> **Note:**
>
> If the difference between the start angle and end angle is too small, abnormal rendering may occur. Please use reasonable start and end angle positions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| angle | ?Float32 | Yes | - | The end angle position, where 0 degrees is at the 12 o'clock position, and positive angles are measured clockwise.<br>Initial value: 360.0. |

### func indicator(?ResourceStr, ?Length)

```cangjie
public func indicator(icon!: ?ResourceStr = None, space!: ?Length = None): This
```

**Function:** Sets the pointer style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| icon | ?[ResourceStr](./cj-common-types.md#interface-resourcestr) | No | None | **Named parameter.** Initial value: "default". Pointer style: "default" is a triangular arrow, "null" means no pointer. |
| space | ?[Length](./cj-common-types.md#interface-length) | No | None | **Named parameter.** Initial value: 8.0.vp. The spacing between the pointer and the outer edge of the ring (percentage not supported).<br>Unit: vp. |

### func startAngle(?Float32)

```cangjie
public func startAngle(angle: ?Float32): This
```

**Function:** Sets the start angle position of the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| angle | ?Float32 | Yes | - | The start angle position, where 0 degrees is at the 12 o'clock position, and positive angles are measured clockwise. Initial value: 0.0. |

### func strokeWidth(?Length)

```cangjie
public func strokeWidth(length: ?Length): This
```

**Function:** Sets the thickness of the ring in the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| length | ?[Length](./cj-common-types.md#interface-length) | Yes | - | The thickness of the ring in the gauge.<br>Initial value: 4.0.vp.<br>Unit: vp.<br>**Note:**<br>If set to a value less than 0, the default value is used.<br>The maximum thickness is the radius of the ring. Values exceeding this will be capped at the maximum.<br>Percentage values are not supported. |

### func trackShadow(?Float32, ?Float32, ?Float32)

```cangjie
public func trackShadow(radius!: ?Float32 = None, offsetX!: ?Float32 = None, offsetY!: ?Float32 = None): This
```

**Function:** Sets the shadow style.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| radius | ?Float32 | No | None | **Named parameter.** Initial value: 20.0. The blur radius of the shadow.<br>Unit: vp. |
| offsetX | ?Float32 | No | None | **Named parameter.** Initial value: 5.0. The X-axis offset. |
| offsetY | ?Float32 | No | None | **Named parameter.** Initial value: 5.0. The Y-axis offset. |

### func value(?Float32)

```cangjie
public func value(value: ?Float32): This
```

**Function:** Sets the data value of the gauge.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?Float32 | Yes | - | The data value of the gauge, which can be used to dynamically modify the gauge's value.<br>Initial value: 0.0. |