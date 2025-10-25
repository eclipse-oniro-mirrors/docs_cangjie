# ohos.common_event_subscribe_info

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, please refer to [Cangjie Sample Code Description](../cj-development-intro.md#Cangjie-Sample-Code-Description).

## class CommonEventSubscribeInfo

```cangjie
public class CommonEventSubscribeInfo {
    public var events: Array<String>
    public var priority: Int32
    public var userId: Int32
    public var publisherPermission: String
    public var publisherDeviceId: String
    public var publisherBundleName: String
    public init(
        events: Array<String>,
        publisherPermission!: String = "",
        publisherDeviceId!: String = "",
        userId!: Int32 = UNDEFINED_USER,
        priority!: Int32 = 0,
        publisherBundleName!: String = ""
    )
}
```

**Function:** Used to represent subscriber information.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var events

```cangjie
public var events: Array<String>
```

**Function:** Represents the public events to subscribe to.

**Type:** Array\<String>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var priority

```cangjie
public var priority: Int32
```

**Function:** Represents the priority of the subscriber. The value range is -100 to 1000. Priorities exceeding the upper or lower limits will be set to the limit values.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var publisherBundleName

```cangjie
public var publisherBundleName: String
```

**Function:** Represents the bundleName of the publisher to subscribe to.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var publisherDeviceId

```cangjie
public var publisherDeviceId: String
```

**Function:** Represents the device ID. Obtain the udid through [@ohos.deviceInfo](./cj-apis-device_info.md) as the subscriber's device ID.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var publisherPermission

```cangjie
public var publisherPermission: String
```

**Function:** Represents the publisher's permission. The subscriber will only receive events published by senders with this permission.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var userId

```cangjie
public var userId: Int32
```

**Function:** Represents the user ID. This parameter is optional, with the default value being the current user's ID. If this parameter is specified, the value must be an existing user ID in the system.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### init(Array\<String>, String, String, Int32, Int32, String)

```cangjie
public init(
    events: Array<String>,
    publisherPermission!: String = "",
    publisherDeviceId!: String = "",
    userId!: Int32 = UNDEFINED_USER,
    priority!: Int32 = 0,
    publisherBundleName!: String = ""
)
```

**Function:** Constructs a CommonEventSubscribeInfo object.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| events | Array\<String> | Yes | - | Represents the public events to subscribe to. |
| publisherPermission | String | No | "" | **Named parameter.** Represents the publisher's permission. The subscriber will only receive events published by senders with this permission. |
| publisherDeviceId | String | No | "" | **Named parameter.** Represents the device ID. Obtain the udid through [@ohos.deviceInfo](./cj-apis-device_info.md) as the subscriber's device ID. |
| userId | Int32 | No | UNDEFINED_USER | **Named parameter.** Represents the user ID. This parameter is optional, with the default value being the current user's ID. If this parameter is specified, the value must be an existing user ID in the system. |
| priority | Int32 | No | 0 | **Named parameter.** Represents the priority of the subscriber. The value range is -100 to 1000. Priorities exceeding the upper or lower limits will be set to the limit values. |
| publisherBundleName | String | No | "" | **Named parameter.** Represents the bundleName of the publisher to subscribe to. |