# SwipeGesture

Used to trigger swipe events, recognized successfully when swipe speed exceeds 100vp/s.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func !=(SwipeDirection)

```cangjie
public operator func !=(other: SwipeDirection): Bool
```

**Function:** Determines whether two enumeration values are unequal

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeDirection](#enum-swipedirection) | Yes | - | Enumeration value to compare |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are unequal, otherwise returns false. |

## func ==(SwipeDirection)

```cangjie
public operator func ==(other: SwipeDirection): Bool
```

**Function:** Determines whether two enumeration values are equal

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SwipeDirection](#enum-swipedirection) | Yes | - | Enumeration value to compare |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

## Basic Type Definitions

### enum SwipeDirection

```cangjie
public enum SwipeDirection <: Equatable<SwipeDirection> {
    | Horizontal
    | Vertical
    | All
    | ...
}
```

**Function:** Specifies the swipe direction for triggering swipe gestures.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parent Type:**

- Equatable\<SwipeDirection>

#### All

```cangjie
All
```

**Function:** All directions.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Horizontal

```cangjie
Horizontal
```

**Function:** Horizontal direction, triggered when the angle between finger swipe direction and x-axis is less than 45 degrees.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### Vertical

```cangjie
Vertical
```

**Function:** Vertical direction, triggered when the angle between finger swipe direction and y-axis is less than 45 degrees.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21