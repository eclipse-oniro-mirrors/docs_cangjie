# Component Content Blur

Adds a content blur effect to the current component.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func foregroundBlurStyle(?BlurStyle)

```cangjie
func foregroundBlurStyle(value: ?BlurStyle): T
```

**Function:** Provides content blur capability for the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
| :-------   | :---------- | :------- | :-------- | :---------- |
| value | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | Yes | - | Content blur style. <br/>Initial value: BlurStyle.None. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that calls this interface. |

## func foregroundBlurStyle(?BlurStyle, ?ForegroundBlurStyleOptions)

```cangjie
func foregroundBlurStyle(value: ?BlurStyle, options: ?ForegroundBlurStyleOptions): T
```

**Function:** Provides content blur capability for the current component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
| :-------   | :---------- | :------- | :-------- | :---------- |
| value | ?[BlurStyle](./cj-common-types.md#enum-blurstyle) | Yes | - | Content blur style. |
| options | ?[ForegroundBlurStyleOptions](./cj-common-types.md#class-foregroundblurstyleoptions) | Yes | - | Content blur options. |

**Return Value:**

| Type | Description |
| :--- | :--- |
| T | Returns the component instance itself that calls this interface. |