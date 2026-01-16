# Half-Modal Transition

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Use the `bindSheet` property to bind a half-modal page to a component. When the component is inserted, the size of the half-modal can be determined by setting a custom or default built-in height.

> **Note:**
>
> Routing navigation is not supported.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func bindSheet(?Bool, CustomBuilder, ?SheetOptions)

```cangjie
func bindSheet(isShow: ?Bool, builder: CustomBuilder, options!: ?SheetOptions): T
```

**Function:** Binds a half-modal page to a component, which is displayed upon clicking.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| isShow | ?Bool | Yes | - | Whether to display the half-modal page. <br>Initial value: `false`. |
| builder | [CustomBuilder](./cj-common-types.md#type-custombuilder) | Yes | - | Configures the content of the half-modal page. |
| options | ?[SheetOptions](./cj-common-types.md#class-sheetoptions) | Yes | - | **Named parameter.** Configures optional properties of the half-modal page. <br/>Initial value: `SheetOptions()`. |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that calls this interface. |

> **Notes:**
>
> - In cases of upward dragging for a single-level half-modal or upward sliding for multi-level switching, the content updates the display area after dragging ends or level switching completes.
> - A half-modal is a popup strictly bound to its host node. To achieve an effect similar to "displaying the half-modal the moment the page appears," ensure the host node is already mounted on the tree. If `isShow` is set to `true` before the host node is mounted, the half-modal will not take effect. It is recommended to use the [`onAppear`](./cj-universal-event-appear.md#func-onappear---unit) function to ensure the half-modal is displayed only after the host node is mounted.
> - Especially when [`SheetMode`](./cj-common-types.md#enum-sheetmode) = `Embedded`, in addition to the host node, ensure the corresponding page node is successfully mounted.
> - The exit animation of the half-modal page cannot be interrupted, and no other gesture actions are responsive during the animation. Currently, the exit animation uses a spring curve, which includes a visually subtle trailing effect. Therefore, when the half-modal exits, it may appear visually gone, but the animation might not have fully ended. Attempting to click and reopen the half-modal during this time will not work. Wait until the animation completely finishes before reopening.

