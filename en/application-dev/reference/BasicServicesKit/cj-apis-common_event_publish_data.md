# ohos.common_event_publish_data

This module describes the content and attributes of common events.

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## class CommonEventPublishData

```cangjie
public class CommonEventPublishData {
    public var bundleName: String
    public var data: String
    public var code: Int32
    public var subscriberPermissions: Array<String>
    public var isOrdered: Bool
    public var isSticky: Bool
    public var parameters: HashMap<String, ValueType>
    public init(
        bundleName!: String = "",
        data!: String = "",
        code!: Int32 = 0,
        subscriberPermissions!: Array<String> = Array<String>(),
        isOrdered!: Bool = false,
        isSticky!: Bool = false,
        parameters!: HashMap<String, ValueType> = HashMap<String, ValueType>()
    )
}
```

**Function:** Contains the content and attributes of common events.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var bundleName

```cangjie
public var bundleName: String
```

**Function:** Indicates the subscriber package name. Only subscribers with this bundleName can receive the common event.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var code

```cangjie
public var code: Int32
```

**Function:** Indicates the result code of the common event.

**Type:** Int32

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var data

```cangjie
public var data: String
```

**Function:** Indicates the custom result data of the common event.

**Type:** String

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var isOrdered

```cangjie
public var isOrdered: Bool
```

**Function:** Indicates whether the event is ordered.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var isSticky

```cangjie
public var isSticky: Bool
```

**Function:** Indicates whether the event is sticky. Only system applications or system services are allowed to send sticky events.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var parameters

```cangjie
public var parameters: HashMap<String, ValueType>
```

**Function:** Indicates additional information of the common event.

**Type:** HashMap\<String, ValueType>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var subscriberPermissions

```cangjie
public var subscriberPermissions: Array<String>
```

**Function:** Indicates the permissions of subscribers.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### init(String, String, Int32, Array\<String>, Bool, Bool, HashMap\<String,ValueType>)

```cangjie
public init(
    bundleName!: String = "",
    data!: String = "",
    code!: Int32 = 0,
    subscriberPermissions!: Array<String> = Array<String>(),
    isOrdered!: Bool = false,
    isSticky!: Bool = false,
    parameters!: HashMap<String, ValueType> = HashMap<String, ValueType>()
)
```

**Function:** Constructs a CommonEventPublishData object.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| bundleName | String | No | "" | Indicates the subscriber package name. Only subscribers with this bundleName can receive the common event. |
| data | String | No | "" | Indicates the custom result data of the common event. |
| code | Int32 | No | 0 | Indicates the result code of the common event. |
| subscriberPermissions | Array\<String> | No | Array\<String>() | **Named parameter.** Indicates the permissions of subscribers. |
| isOrdered | Bool | No | false | **Named parameter.** Indicates whether the event is ordered. |
| isSticky | Bool | No | false | **Named parameter.** Indicates whether the event is sticky. Only system applications or system services are allowed to send sticky events. |
| parameters | HashMap\<String, ValueType> | No | HashMap<String, ValueType>() | **Named parameter.** Indicates additional information of the common event. |