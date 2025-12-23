# Component Identifier

The id serves as the unique identifier for a component and must be unique across the entire application. This module provides interfaces related to component identifiers, enabling retrieval of attributes for a specified component id, as well as the functionality to send events to a designated component id.

> **Note:**
>
> If multiple ids or keys are set for the same component, the last assigned value takes effect.

## Import Module

```cangjie
import kit.ArkUI.*
```

## func id(?String)

```cangjie
func id(value: ?String): T
```

**Functionality:** The unique identifier of a component, with uniqueness guaranteed by the user.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?String | Yes | - | The unique identifier of the component, with uniqueness guaranteed by the user. <br/>Default value: "". |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func key(?String)

```cangjie
func key(value: ?String): T
```

**Functionality:** The unique identifier of a component, with uniqueness guaranteed by the user.

This interface is intended solely for application testing. When used alongside id, the latter assigned property will override the former. It is recommended to set only the id.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| value | ?String | Yes | - | The unique identifier of the component, with uniqueness guaranteed by the user. <br/>Default value: "". |

**Return Value:**

| Type | Description |
|:---|:---|
| T | Returns the component instance itself that called this interface. |

## func getInspectorByKey(String)

```cangjie
public func getInspectorByKey(id: String): String
```

**Functionality:** Retrieves all attributes of the component with the specified id, excluding child component information. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :-------   | :---------- | :------- | :-------- | :----------|
| id   | String   | Yes   |  - | The id of the component whose attributes are to be retrieved. |

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| String   | A JSON string of the component's attribute list.<br>**Note:** <br>The string includes the component's tag, id, position information (coordinates relative to the top-left corner of the window), and relevant attribute information for testing purposes.   |

## func getInspectorTree()

```cangjie
public func getInspectorTree(): String
```

**Functionality:** Retrieves the component tree and component attributes. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| String  | A JSON object containing the component tree and attribute list. |

## func sendEventByKey(String, IntNative, String)

```cangjie
public func sendEventByKey(id: String, action: IntNative, params: String): Bool
```

**Functionality:** Sends an event to the component with the specified id. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :-------   | :---------- | :------- | :-------- | :----------|
| id     | String | Yes    |  - | The id of the component to trigger the event. |
| action | IntNative | Yes  | - | The type of event to trigger. Currently supported values:<br/>- Click event: 10.<br/>- Long press event: 11.|
| params | String | Yes    | - | Event parameters. Pass an empty string "" if no parameters are required.|

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| Bool   | Returns false if the specified id is not found; otherwise, returns true. |

## func sendTouchEvent(TouchObject)

```cangjie
public func sendTouchEvent(event: TouchObject): Bool
```

**Functionality:** Sends a touch event. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :-------   | :---------- | :------- | :-------- | :----------|
| event | [TouchObject](./cj-common-types.md#class-touchobject) | Yes   | - | The position to trigger the touch event. For details on the event parameter, refer to the introduction of TouchObject in [TouchEvent](./cj-common-types.md#class-touchevent). |

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| Bool | Returns false if the event fails to send; otherwise, returns true.|

## func sendKeyEvent(KeyEvent)

```cangjie
public func sendKeyEvent(event: KeyEvent): Bool
```

**Functionality:** Sends a key event. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :-------   | :---------- | :------- | :-------- | :----------|
| event | [KeyEvent](./cj-common-types.md#class-keyevent) | Yes    | - | The key event. For details on the event parameter, refer to the introduction of [KeyEvent](./cj-common-types.md#class-keyevent). |

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| Bool | Returns false if the event fails to send; otherwise, returns true.|

## func sendMouseEvent(MouseEvent)

```cangjie
public func sendMouseEvent(event: MouseEvent): Bool
```

**Functionality:** Sends a mouse event. This interface is intended solely for application testing. Due to its time-consuming nature, usage is not recommended.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Initial Version:** 22

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :-------   | :---------- | :------- | :-------- | :----------|
| event | [MouseEvent](./cj-common-types.md#class-mouseevent) | Yes  | -  | The mouse event. For details on the event parameter, refer to the introduction of [MouseEvent](./cj-common-types.md#class-mouseevent). |

**Return Value:**

| Type | Description |
| :-------   | :---------- |
| Bool | Returns false if the event fails to send; otherwise, returns true.|