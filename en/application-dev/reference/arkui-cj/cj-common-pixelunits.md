# Pixel Units

Cangjie provides four types of pixel units, with vp as the base data unit.

| Name | Description |
|:---|:---|
| px | Physical pixel unit of the screen. |
| vp | Density-independent pixel, converted to physical screen pixels based on screen pixel density. When a value has no unit specified, the default unit is vp. On a screen with an actual width of 1440 physical pixels, 1vp is approximately equal to 3px.<br/>**Note:** <br/> The ratio between vp and px depends on the screen pixel density. |
| fp | Font pixel, similar to vp in adapting to screen density changes, and adjusts according to system font size settings. |
| lpx | Logical viewport pixel unit. The lpx unit is the ratio of the actual screen width to the logical width (configured via `designWidth`), with the default `designWidth` value being 720. When `designWidth` is 720, on a screen with an actual width of 1440 physical pixels, 1lpx equals 2px. |

## Import Module

```cangjie
import kit.ArkUI.*
```

## func fp2px(Length)

```cangjie
public func fp2px(value: Length): Option<Length>
```

**Function:** Converts a value in fp units to a value in px units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in fp units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in px units. |

## func lpx2px(Length)

```cangjie
public func lpx2px(value: Length): Option<Length>
```

**Function:** Converts a value in lpx units to a value in px units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in lpx units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in px units. |

## func px2fp(Length)

```cangjie
public func px2fp(value: Length): Option<Length>
```

**Function:** Converts a value in px units to a value in fp units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in px units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in fp units. |

## func px2lpx(Length)

```cangjie
public func px2lpx(value: Length): Option<Length>
```

**Function:** Converts a value in px units to a value in lpx units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in px units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in lpx units. |

## func px2vp(Length)

```cangjie
public func px2vp(value: Length): Option<Length>
```

**Function:** Converts a value in px units to a value in vp units.<br>Note: By default, the conversion uses the virtual pixel ratio of the screen where the current UI instance resides. If the UI instance has not been created, the conversion uses the virtual pixel ratio of the default screen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in px units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in vp units. |

## func vp2px(Length)

```cangjie
public func vp2px(value: Length): Option<Length>
```

**Function:** Converts a value in vp units to a value in px units.<br>Note: By default, the conversion uses the virtual pixel ratio of the screen where the current UI instance resides. If the UI instance has not been created, the conversion uses the virtual pixel ratio of the default screen.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](../BasicServicesKit/cj-apis-base.md#interface-length) | Yes | - | The value in vp units to be converted. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](../BasicServicesKit/cj-apis-base.md#interface-length)> | The converted value in px units. |