# ohos.common_event_data

This module describes the data of common events.

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class CommonEventData

```cangjie
public class CommonEventData {
    public var event: String
    public var bundleName: String
    public var code: Int32
    public var data: String
    public var parameters: HashMap<String, ValueType>
}
```

**Function:** Data of common events.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var bundleName

```cangjie
public var bundleName: String
```

**Function:** Indicates the package name, currently empty by default.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var code

```cangjie
public var code: Int32
```

**Function:** Indicates the common event data (Int32 type) received by the subscriber. The value of this field is consistent with the data passed through the `code` field in [CommonEventPublishData](./cj-apis-common_event_publish_data.md#class-commoneventpublishdata) when the publisher uses [commonEventManager.publish](./cj-apis-common_event_manager.md#static-func-publishstring-commoneventpublishdata) to publish the common event. The default value is 0.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var data

```cangjie
public var data: String
```

**Function:** Indicates the common event data (string type) received by the subscriber. The value of this field is consistent with the data passed through the `data` field in [CommonEventPublishData](./cj-apis-common_event_publish_data.md#class-commoneventpublishdata) when the publisher uses [commonEventManager.publish](./cj-apis-common_event_manager.md#static-func-publishstring-commoneventpublishdata) to publish the common event.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var event

```cangjie
public var event: String
```

**Function:** Indicates the name of the currently received common event.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21

### var parameters

```cangjie
public var parameters: HashMap<String, ValueType>
```

**Function:** Indicates the additional information of the common event received by the subscriber. The value of this field is consistent with the data passed through the `parameters` field in [CommonEventPublishData](./cj-apis-common_event_publish_data.md#class-commoneventpublishdata) when the publisher uses [commonEventManager.publish](./cj-apis-common_event_manager.md#static-func-publishstring-commoneventpublishdata) to publish the common event.

**Type:** HashMap\<String, ValueType>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 21