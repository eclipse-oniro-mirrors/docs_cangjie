# Component Identification

The `id` serves as the unique identifier for a component within the entire application. This module provides interfaces related to component identification, enabling retrieval of attributes for a specified component by its `id`, as well as the functionality to send events to a component with a given `id`.

> **Note:**
>
> If multiple `id` or `key` values are set for the same component, the last one configured takes effect.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func getInspectorByKey(String)

```cangjie
public func getInspectorByKey(id: String): String
```

**Function:** Retrieves all attributes of the component with the specified `id`, excluding child component information. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | The `id` of the component whose attributes are to be retrieved. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | A JSON-formatted string listing the component's attributes.<br>**Note:** <br>The string includes the component's tag, `id`, positional information (coordinates relative to the top-left corner of the window), and relevant attribute information for testing purposes. |

## func getInspectorTree()

```cangjie
public func getInspectorTree(): String
```

**Function:** Retrieves the component tree along with component attributes. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | A JSON object containing the component tree and attribute list. |

## func sendEventByKey(String, IntNative, String)

```cangjie
public func sendEventByKey(id: String, action: IntNative, params: String): Bool
```

**Function:** Sends an event to the component with the specified `id`. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| id | String | Yes | - | The `id` of the component to trigger the event. |
| action | IntNative | Yes | - | The type of event to trigger. Currently supported values:<br/>- Click event: 10.<br/>- Long press event: 11. |
| params | String | Yes | - | Event parameters. Pass an empty string `""` if no parameters are required. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `false` if the specified `id` is not found; otherwise, returns `true`. |

## func sendKeyEvent(KeyEvent)

```cangjie
public func sendKeyEvent(event: KeyEvent): Bool
```

**Function:** Sends a key event. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [KeyEvent](./cj-universal-event-key.md#class-keyevent) | Yes | - | The key event. For details on the `event` parameter, refer to [KeyEvent](./cj-universal-event-key.md#class-keyevent). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `false` if the event fails to send; otherwise, returns `true`. |

## func sendMouseEvent(MouseEvent)

```cangjie
public func sendMouseEvent(event: MouseEvent): Bool
```

**Function:** Sends a mouse event. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [MouseEvent](./cj-universal-event-mouse.md#class-mouseevent) | Yes | - | The mouse event. For details on the `event` parameter, refer to [MouseEvent](./cj-universal-event-mouse.md#class-mouseevent). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `false` if the event fails to send; otherwise, returns `true`. |

## func sendTouchEvent(TouchObject)

```cangjie
public func sendTouchEvent(event: TouchObject): Bool
```

**Function:** Sends a touch event. This interface is intended solely for application testing purposes. Due to its time-consuming nature, its use is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| event | [TouchObject](./cj-universal-event-touch.md#class-touchobject) | Yes | - | The touch event location. For details on the `event` parameter, refer to `TouchObject` in [TouchEvent](./cj-universal-event-touch.md#class-touchevent). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `false` if the event fails to send; otherwise, returns `true`. |

## func id(String)

```cangjie
public func id(value: String): This
```

**Function:** Sets the `id` of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The unique identifier of the component. Uniqueness must be ensured by the user. |

## func key(String)

```cangjie
public func key(value: String): This
```

**Function:** Sets the key value of a component.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| value | String | Yes | - | The unique identifier of the component. Uniqueness must be ensured by the user. |