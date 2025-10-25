# Safe Area

The safe area refers to the display area of a page that, by default, does not overlap with system-defined non-safe areas such as the status bar or navigation bar. By default, interfaces developed by developers are laid out within the safe area. Property methods are provided to allow developers to extend component rendering beyond the safe area constraints. The [expandSafeArea](./cj-universal-attribute-expandsafearea.md#func-expandsafeareaarraysafeareatype-arraysafeareaedge) attribute enables components to expand their rendering area beyond the safe area without altering the layout. The [setKeyboardAvoidMode](./cj-universal-attribute-expandsafearea.md#func-setkeyboardavoidmodevalue-keyboardavoidmode) method configures the page's avoidance mode when a virtual keyboard pops up. For components like title bars where text should not overlap with non-safe areas, it is recommended to use the `expandSafeArea` attribute to achieve an immersive effect. Alternatively, the immersive mode can be directly set via the window interface [setWindowLayoutFullScreen](./cj-apis-window.md#).

> **Note:**
>
> By default, the camera cutout area is not considered a non-safe area, and the page does not avoid the cutout.

```json5
"metadata": [
  {
    "name": "avoid_cutout",
    "value": "true",
  }
],
```

## Import Module

```cangjie
import kit.ArkUI.*
```

## func expandSafeArea(?Array\<SafeAreaType>, ?Array\<SafeAreaEdge>)

```cangjie
public func expandSafeArea(types!: ?Array<SafeAreaType> = None, edges!: ?Array<SafeAreaEdge> = None): This
```

**Function:** Expands the safe area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| types | ?Array\<[SafeAreaType](#enum-safeareatype)> | No | None | Array of safe area types. |
| edges | ?Array\<[SafeAreaEdge](#enum-safeareaedge)> | No | None | Array of safe area edges. |

## func !=(SafeAreaEdge)

```cangjie
public operator func !=(other: SafeAreaEdge): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SafeAreaEdge](#enum-safeareaedge) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal; otherwise, returns `false`. |

## func ==(SafeAreaEdge)

```cangjie
public operator func ==(other: SafeAreaEdge): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SafeAreaEdge](#enum-safeareaedge) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal; otherwise, returns `false`. |

## func !=(SafeAreaType)

```cangjie
public operator func !=(other: SafeAreaType): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SafeAreaType](#enum-safeareatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal; otherwise, returns `false`. |

## func ==(SafeAreaType)

```cangjie
public operator func ==(other: SafeAreaType): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SafeAreaType](#enum-safeareatype) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal; otherwise, returns `false`. |

## Basic Type Definitions

### enum SafeAreaEdge

```cangjie
public enum SafeAreaEdge <: Equatable<SafeAreaEdge> {
    | TOP
    | BOTTOM
    | START
    | END
    | ...
}
```

**Function:** Specifies the direction for expanding the safe area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<SafeAreaEdge>

#### BOTTOM

```cangjie
BOTTOM
```

**Function:** Bottom area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### END

```cangjie
END
```

**Function:** End area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### START

```cangjie
START
```

**Function:** Start area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### TOP

```cangjie
TOP
```

**Function:** Top area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### enum SafeAreaType

```cangjie
public enum SafeAreaType <: Equatable<SafeAreaType> {
    | SYSTEM
    | CUTOUT
    | KEYBOARD
    | ...
}
```

**Function:** Enumeration type for expanding the safe area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<SafeAreaType>

#### CUTOUT

```cangjie
CUTOUT
```

**Function:** Non-safe area of the device, such as notches or punch-hole screens.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### KEYBOARD

```cangjie
KEYBOARD
```

**Function:** Soft keyboard area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### SYSTEM

```cangjie
SYSTEM
```

**Function:** System default non-safe area, including the status bar and navigation bar.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21