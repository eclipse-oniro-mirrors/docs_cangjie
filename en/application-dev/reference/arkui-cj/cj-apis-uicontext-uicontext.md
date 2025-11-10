# Class (UIContext)

Provides UI context-related functionalities.

## Import Module

```cangjie
import kit.ArkUI.*
```

## class UIContext

```cangjie
public class UIContext {}
```

**Description:** UI context class that provides various UI-related functionalities.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

### func animateTo(AnimateParam, VoidCallback)

```cangjie
public func animateTo(value: AnimateParam, event: VoidCallback): Unit
```

**Description:** Provides the animateTo interface to insert transition animations for state changes caused by closure code.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [AnimateParam](./cj-common-types.md#class-animateparam) | Yes | - | Animation parameters. |
| event | [VoidCallback](./cj-common-types.md#type-VoidCallback) | Yes | - | Callback function for animation execution. |

### func createAnimator(AnimatorOptions)

```cangjie
public func createAnimator(options: AnimatorOptions): AnimatorResult
```

**Description:** Creates an animator result object (AnimatorResult).

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [AnimatorOptions](./cj-apis-uicontext-animator.md#class-animatoroptions) | Yes | - | Animation options. |

**Return Value:**

| Type | Description |
|:----|:----|
| [AnimatorResult](./cj-apis-uicontext-animator.md#class-animatorresult) | Animator result object. |

### func fp2px(Length)

```cangjie
public func fp2px(value: Length): Option<Length>
```

**Description:** Converts a value from fp units to px units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |

### func getContextMenuController()

```cangjie
public func getContextMenuController(): ContextMenuController
```

**Description:** Gets the context menu controller object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [ContextMenuController](./cj-apis-uicontext-contextmenucontroller.md#class-contextmenucontroller) | Context menu controller object. |

### func getFont()

```cangjie
public func getFont(): Font
```

**Description:** Gets the font object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Font](cj-common-types.md#class-font) | Font object. |

### func getMeasureUtils()

```cangjie
public func getMeasureUtils(): MeasureUtils
```

**Description:** Gets the measurement utility object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [MeasureUtils](./cj-apis-uicontext-measureutils.md#class-measureutils) | MeasureUtils object. |

### func getPromptAction()

```cangjie
public func getPromptAction(): PromptAction
```

**Description:** Gets the PromptAction object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [PromptAction](./cj-apis-uicontext-promptaction.md#class-promptaction) | PromptAction object. |

### func getRouter()

```cangjie
public func getRouter(): Router
```

**Description:** Gets the router object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Router](./cj-apis-uicontext-router.md#class-router) | Router object. |

### func lpx2px(Length)

```cangjie
public func lpx2px(value: Length): Option<Length>
```

**Description:** Converts a value from lpx units to px units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |

### func px2fp(Length)

```cangjie
public func px2fp(value: Length): Option<Length>
```

**Description:** Converts a value from px units to fp units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |

### func px2lpx(Length)

```cangjie
public func px2lpx(value: Length): Option<Length>
```

**Description:** Converts a value from px units to lpx units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |

### func px2vp(Length)

```cangjie
public func px2vp(value: Length): Option<Length>
```

**Description:** Converts a value from px units to vp units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |

### func showActionSheet(ActionSheetOptions)

```cangjie
public func showActionSheet(value: ActionSheetOptions): Unit
```

**Description:** Defines and displays a list popup.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [ActionSheetOptions](./cj-dialog-actionsheet.md#class-actionsheetoptions) | Yes | - | Action sheet parameters. |

### func showAlertDialog(AlertDialogParamWithConfirm)

```cangjie
public func showAlertDialog(options: AlertDialogParamWithConfirm): Unit
```

**Description:** Displays an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [AlertDialogParamWithConfirm](./cj-dialog-alertdialog.md#class-alertdialogparamwithconfirm) | Yes | - | Alert dialog parameters. |

### func showAlertDialog(AlertDialogParamWithButtons)

```cangjie
public func showAlertDialog(options: AlertDialogParamWithButtons): Unit
```

**Description:** Displays an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [AlertDialogParamWithButtons](./cj-dialog-alertdialog.md#class-alertdialogparamwithbuttons) | Yes | - | Alert dialog parameters. |

### func showAlertDialog(AlertDialogParamWithOptions)

```cangjie
public func showAlertDialog(options: AlertDialogParamWithOptions): Unit
```

**Description:** Displays an alert dialog.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| options | [AlertDialogParamWithOptions](./cj-dialog-alertdialog.md#class-alertdialogparamwithbuttons) | Yes | - | Alert dialog parameters. |

### func vp2px(Length)

```cangjie
public func vp2px(value: Length): Option<Length>
```

**Description:** Converts a value from vp units to px units.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | [Length](./cj-common-types.md#interface-length) | Yes | - | Value to convert. |

**Return Value:**

| Type | Description |
|:----|:----|
| Option\<[Length](./cj-common-types.md#interface-length)> | Converted value. |
