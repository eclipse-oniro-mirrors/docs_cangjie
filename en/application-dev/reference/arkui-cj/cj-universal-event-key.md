# Key Event

Key events refer to events triggered when components interact with input devices such as keyboards and remote controls. These events apply to all focusable components, such as Button. For components like Text and Image that are not focusable by default, key events are currently not supported. However, they can be enabled in the future by setting the `focusable` property to true.

## Import Module

```cangjie
import kit.ArkUI.*
```

## Permission List

None

## func onKeyEvent((KeyEvent) -> Unit)

```cangjie
public func onKeyEvent(event: (KeyEvent) -> Unit): This
```

**Function:** Binds a callback that triggers when a key action occurs while the component has focus.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | ([KeyEvent](#class-keyevent))->Unit | Yes | - | Callback triggered when a key action occurs while the component has focus. |

## Basic Type Definitions

### class KeyEvent

```cangjie
public class KeyEvent {
    public var keyText: String
    public var keyType: KeyType
    public var keyCode: Int32
    public var keySource: KeySource
    public var metaKey: Int32
    public var deviceId: Int64
    public var timestamp: Int64
    public init(keyText: String, keyType: KeyType, keyCode: Int32, keySource: KeySource, metaKey: Int32,
        deviceId: Int64, timestamp: Int64)
}
```

**Function:** Key event.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

### var deviceId

```cangjie
public var deviceId: Int64
```

**Function:** The ID of the input device that triggered the current key event.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var keyCode

```cangjie
public var keyCode: Int32
```

**Function:** The key code of the pressed key.

**Type:** Int32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var keySource

```cangjie
public var keySource: KeySource
```

**Function:** The type of input device that triggered the current key event.

**Type:** [KeySource](./cj-common-types.md#enum-keysource)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var keyText

```cangjie
public var keyText: String
```

**Function:** The key value of the pressed key.

**Type:** String

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var keyType

```cangjie
public var keyType: KeyType
```

**Function:** The type of the key event.

**Type:** [KeyType](./cj-common-types.md#enum-keytype)

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var metaKey

```cangjie
public var metaKey: Int32
```

**Function:** The state of the meta key when the key event occurred. 1 indicates pressed state, and 0 indicates unpressed state.

**Type:** Int32

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** The timestamp when the key event occurred.

**Type:** Int64

**Read/Write:** Read-Write

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

#### init(String, KeyType, Int32, KeySource, Int32, Int64, Int64)

```cangjie
public init(keyText: String, keyType: KeyType, keyCode: Int32, keySource: KeySource, metaKey: Int32,
    deviceId: Int64, timestamp: Int64)
```

**Function:** Constructs a key event object.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| keyText | String | Yes | - | The key value of the pressed key. |
| keyType | [KeyType](./cj-common-types.md#enum-keytype) | Yes | - | The type of the key event. |
| keyCode | Int32 | Yes | - | The key code of the pressed key. |
| keySource | [KeySource](./cj-common-types.md#enum-keysource) | Yes | - | The type of input device that triggered the current key event. |
| metaKey | Int32 | Yes | - | The state of the meta key when the key event occurred. 1 indicates pressed state, and 0 indicates unpressed state. |
| deviceId | Int64 | Yes | - | The ID of the input device that triggered the current key event. |
| timestamp | Int64 | Yes | - | The timestamp when the key event occurred. |

#### func stopPropagation()

```cangjie
public func stopPropagation(): Unit
```

**Function:** Stops the event from further propagation.

**System Capability:** SystemCapability.ArkUI.ArkUI.Full

**Since:** 21