# StepperItem

Used as a child component for pages within the [Stepper](cj-navigation-switching-stepper.md) component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Child Components

Supports a single child component.

## Creating the Component

### init(() -> Unit)

```cangjie
public init(child: () -> Unit)
```

**Function:** Creates a page child component for the [Stepper](cj-navigation-switching-stepper.md) component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| child | () -> Unit | Yes | - | The child component of StepperItem. |

## Common Attributes/Common Events

Common Attributes: All supported.

Common Events: All supported.

## Component Attributes

### func nextLabel(String)

```cangjie
public func nextLabel(value: String): This
```

**Function:** Sets the content of the right-side text button. The default value is "Start" for the last page and "Next" for other pages.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The content of the right-side text button. If the string is too long, it will first shrink, then wrap (2 lines), and finally truncate. |

### func prevLabel(String)

```cangjie
public func prevLabel(value: String): This
```

**Function:** Sets the content of the left-side text button. The first page does not have a left-side text button. When the stepper has more than one page, the default value for all pages except the first is "Back".

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The content of the left-side text button. If the string is too long, it will first shrink, then wrap (2 lines), and finally truncate. |

### func status(ItemState)

```cangjie
public func status(status!: ItemState = ItemState.Normal): This
```

**Function:** Sets the display state of the stepper's `nextLabel`.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| status | ItemState | No | ItemState.Normal | The display state of the stepper's `nextLabel`. |

## enum ItemState

```cangjie
public enum ItemState  <: Equatable<ItemState> {
    | Normal
    | Disabled
    | Waiting
    | Skip
    | ...
}
```

**Function:** Item state.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parent Type:**

- Equatable\<ItemState>

### Disabled

```cangjie
Disabled
```

**Function:** Disabled state. The right-side text button is displayed in gray and cannot be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Normal

```cangjie
Normal
```

**Function:** Normal state. The right-side text button is displayed normally and can be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Skip

```cangjie
Skip
```

**Function:** Skip state. The right-side text button defaults to "Skip". Custom logic can be defined in the `onSkip` callback of the Stepper.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### Waiting

```cangjie
Waiting
```

**Function:** Waiting state. The right-side text button is not displayed, and a progress bar is shown instead. The button cannot be clicked to proceed to the next StepperItem.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

### func !=(ItemState)

```cangjie
public operator func !=(other: ItemState): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ItemState](#enum-itemstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are not equal, otherwise returns `false`. |

### func ==(ItemState)

```cangjie
public operator func ==(other: ItemState): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ItemState](#enum-itemstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the two enum values are equal, otherwise returns `false`. |