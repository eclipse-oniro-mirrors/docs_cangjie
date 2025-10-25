# Navigation

The Navigation component serves as the root view container for route navigation, typically used as the root container for Page pages. By default, it includes a title bar, content area, and toolbar. The content area displays navigation content (child components of Navigation) on the homepage or non-homepage content (child components of NavDestination), with switching between homepage and non-homepage achieved through routing.

> **Note:**
>
> - When a NavBar nests a Navigation component, the lifecycle of the inner Navigation does not synchronize with the outer Navigation or the lifecycle of the [Full Modal](./cj-universal-attribute-bindcontentcover.md).
> - When a NavDestination has neither main/subtitles nor a back button, the title bar will not be displayed.

## Import Module

```cangjie
import kit.ArkUI.*
```

## enum BarStyle

```cangjie
public enum BarStyle <: Equatable<BarStyle> {
    | Standard
    | Stack
    | ...
}
```

**Function:** Layout mode for the title bar and content area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- Equatable\<BarStyle>

### Stack

```cangjie
Stack
```

**Function:** The title bar and content area adopt an overlay layout, with the title bar positioned above the content area.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Standard

```cangjie
Standard
```

**Function:** The title bar and content area adopt a vertical layout.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### func !=(BarStyle)

```cangjie
public operator func !=(other: BarStyle): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [BarStyle](#enum-barstyle) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise `false`. |

### func ==(BarStyle)

```cangjie
public operator func ==(other: BarStyle): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [BarStyle](#enum-barstyle) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise `false`. |

## enum NavigationTitleMode

```cangjie
public enum NavigationTitleMode <: Equatable<NavigationTitleMode> {
    | Free
    | Full
    | Mini
    | ...
}
```

**Function:** Operation mode for the route stack.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- Equatable\<NavigationTitleMode>

### Free

```cangjie
Free
```

**Function:** When the content is a scrollable component that fills one screen, the title shrinks as the content scrolls upward (the subtitle size remains unchanged and fades out). When scrolling downward to the top, the title restores to its original state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Full

```cangjie
Full
```

**Function:** Fixed to large title mode. Initial value: When only the main title exists, the title bar height is 112.vp; when both main and subtitles exist, the title bar height is 138.vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Mini

```cangjie
Mini
```

**Function:** Fixed to small title mode. Initial value: When only the main title exists, the title bar height is 56.vp; when both main and subtitles exist, the title bar height is 82.vp.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### func !=(NavigationTitleMode)

```cangjie
public operator func !=(other: NavigationTitleMode): Bool
```

**Function:** Determines whether two enum values are unequal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [NavigationTitleMode](#enum-navigationtitlemode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are unequal, otherwise `false`. |

### func ==(NavigationTitleMode)

```cangjie
public operator func ==(other: NavigationTitleMode): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [NavigationTitleMode](#enum-navigationtitlemode) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Retrieves the string representation of the current enum.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the enum. |