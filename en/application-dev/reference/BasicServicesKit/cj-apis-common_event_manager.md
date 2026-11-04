# ohos.common_event_manager

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides capabilities related to common events, including publishing common events, subscribing to common events, and unsubscribing from common events.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment on the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class CommonEventManager

```cangjie
public class CommonEventManager {}
```

**Function:** This structure provides common event management capabilities.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static func createSubscriber(CommonEventSubscribeInfo)

```cangjie
public static func createSubscriber(subscribeInfo: CommonEventSubscribeInfo): CommonEventSubscriber
```

**Function:** Creates a subscriber.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| subscribeInfo | [CommonEventSubscribeInfo](./cj-apis-common_event_subscribe_info.md#class-commoneventsubscribeinfo) | Yes | - | Indicates the subscription information. |

**Return Value:**

| Type | Description |
|:----|:----|
| [CommonEventSubscriber](./cj-apis-common_event_subscriber.md#class-commoneventsubscriber) | Subscriber object. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.ArkUI.*
import kit.CangjieKit.*

var subscriber: CommonEventSubscriber // Used to save the successfully created subscriber object for subsequent subscription and unsubscription actions.
let support = Support.COMMON_EVENT_ABILITY_ADDED
// Subscriber information
let subscribeInfo: CommonEventSubscribeInfo = CommonEventSubscribeInfo([support])
// Create subscriber
try {
    subscriber = CommonEventManager.createSubscriber(subscribeInfo)
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "errorCode = ${e.code}, errorMsg = ${e.message}")
}
```

### static func publish(String, CommonEventPublishData)

```cangjie
public static func publish(event: String, options!: CommonEventPublishData =  CommonEventPublishData()): Unit
```

**Function:** Publishes a common event.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| event | String | Yes | - | Indicates the common event to be sent. |
| options | [CommonEventPublishData](./cj-apis-common_event_publish_data.md#class-commoneventpublishdata) | No | CommonEventPublishData() | **Named parameter.** Indicates the properties of the published common event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Event Error Codes](./cj-errorcode-common_event_service.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1500003 | The common event sending frequency is too high. |
  | 1500007 | Failed to send the message to the common event service. |
  | 1500008 | Failed to initialize the common event service. |
  | 1500009 | Failed to obtain system parameters. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.ArkUI.*
import kit.CangjieKit.*

try {
    // Common event properties
    let pData = CommonEventPublishData(bundleName: "com.example.myapplication", data: "123321", code: 123321)
    // Publish common event
    CommonEventManager.publish(Support.COMMON_EVENT_SCREEN_ON, options: pData)
} catch (e: BusinessException) {
    let code = e.code
    let message = e.message
    Hilog.error(0, "AppLogCj", "publish failed, error code: ${code}, message: ${message}.")
}
```

### static func subscribe(CommonEventSubscriber, AsyncCallback\<CommonEventData>)

```cangjie
public static func subscribe(subscriber: CommonEventSubscriber, callback: AsyncCallback<CommonEventData>): Unit
```

**Function:** Subscribes to a common event in callback mode.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| subscriber | [CommonEventSubscriber](cj-apis-common_event_subscriber.md#class-commoneventsubscriber) | Yes | - | Indicates the subscriber object. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[CommonEventData](cj-apis-common_event_data.md#class-commoneventdata)> | Yes | - | Indicates the callback function for receiving common event data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Event Error Codes](./cj-errorcode-common_event_service.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 1500007 | Failed to send message to Common Event Service. |
  | 1500008 | Common Event Service did not complete initialization. |
  | 1500010 | The count of subscribers exceeds system specification. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.ArkUI.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Subscribe to event: screen on
let events = [Support.COMMON_EVENT_SCREEN_ON]
// Subscriber information
let info = CommonEventSubscribeInfo(events)
// Subscriber
let sub = CommonEventManager.createSubscriber(info)
// Unsubscribe
try {
    CommonEventManager.unsubscribe(sub)
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "errorCode = ${e.code}, errorMsg = ${e.message}")
}
```

### static func unsubscribe(CommonEventSubscriber)

```cangjie
public static func unsubscribe(subscriber: CommonEventSubscriber): Unit
```

**Function:** Unsubscribes from a common event.

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| subscriber | [CommonEventSubscriber](cj-apis-common_event_subscriber.md#class-commoneventsubscriber) | Yes | - | Indicates the subscriber object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Event Error Codes](./cj-errorcode-common_event_service.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 1500007 | Failed to send message to Common Event Service. |
  | 1500008 | Common Event Service did not complete initialization. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.ArkUI.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

// Subscribe to event: screen on
let events = [Support.COMMON_EVENT_SCREEN_ON]
// Subscriber information
let info = CommonEventSubscribeInfo(events)
// Subscriber
let sub = CommonEventManager.createSubscriber(info)
// Unsubscribe
try {
    CommonEventManager.unsubscribe(sub)
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "errorCode = ${e.code}, errorMsg = ${e.message}")
}
```

## class Support

```cangjie
public class Support {
    public static const COMMON_EVENT_ABILITY_ADDED: String = "common.event.ABILITY_ADDED"
    public static const COMMON_EVENT_ABILITY_REMOVED: String = "common.event.ABILITY_REMOVED"
    public static const COMMON_EVENT_ABILITY_UPDATED: String = "common.event.ABILITY_UPDATED"
    public static const COMMON_EVENT_ACCOUNT_DELETED: String = "usual.event.data.ACCOUNT_DELETED"
    public static const COMMON_EVENT_AIRPLANE_MODE_CHANGED: String = "usual.event.AIRPLANE_MODE"
    public static const COMMON_EVENT_BATTERY_CHANGED: String = "usual.event.BATTERY_CHANGED"
    public static const COMMON_EVENT_BATTERY_LOW: String = "usual.event.BATTERY_LOW"
    public static const COMMON_EVENT_BATTERY_OKAY: String = "usual.event.BATTERY_OKAY"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CONNECT_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CURRENT_DEVICE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.AUDIO_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CONNECT_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CURRENT_DEVICE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.PLAYING_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.AVRCP_CONNECT_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CODEC_VALUE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED: String = "usual.event.bluetooth.remotedevice.DISCOVERED"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.CLASS_VALUE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_CONNECTED"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_DISCONNECTED"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE: String = "usual.event.bluetooth.remotedevice.NAME_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE: String = "usual.event.bluetooth.remotedevice.PAIR_STATE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.BATTERY_VALUE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT: String = "usual.event.bluetooth.remotedevice.SDP_RESULT"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE: String = "usual.event.bluetooth.remotedevice.UUID_VALUE"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ: String = "usual.event.bluetooth.remotedevice.PAIRING_REQ"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL: String = "usual.event.bluetooth.remotedevice.PAIRING_CANCEL"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ: String = "usual.event.bluetooth.remotedevice.CONNECT_REQ"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY: String = "usual.event.bluetooth.remotedevice.CONNECT_REPLY"
    public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL: String = "usual.event.bluetooth.remotedevice.CONNECT_CANCEL"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.CONNECT_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AUDIO_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT: String = "usual.event.bluetooth.handsfreeunit.AG_COMMON_EVENT"
    public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AG_CALL_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE: String = "usual.event.bluetooth.host.STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE: String = "usual.event.bluetooth.hhost.REQ_DISCOVERABLE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE: String = "usual.event.bluetooth.host.REQ_ENABLE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE: String = "usual.event.bluetooth.host.REQ_DISABLE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE: String = "usual.event.bluetooth.host.SCAN_MODE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED: String = "usual.event.bluetooth.host.DISCOVERY_STARTED"
    public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED: String = "usual.event.bluetooth.host.DISCOVERY_FINISHED"
    public static const COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE: String = "usual.event.bluetooth.host.NAME_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.CONNECT_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.PLAYING_STATE_UPDATE"
    public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.AUDIO_STATE_UPDATE"
    public static const COMMON_EVENT_BUNDLE_REMOVED: String = "usual.event.BUNDLE_REMOVED"
    public static const COMMON_EVENT_BOOT_COMPLETED: String = "usual.event.BOOT_COMPLETED"
    public static const COMMON_EVENT_CONNECTIVITY_CHANGE: String = "usual.event.CONNECTIVITY_CHANGE"
    public static const COMMON_EVENT_CALL_STATE_CHANGED: String = "usual.event.CALL_STATE_CHANGED"
    public static const COMMON_EVENT_CHARGE_IDLE_MODE_CHANGED: String = "usual.event.CHARGE_IDLE_MODE_CHANGED"
    public static const COMMON_EVENT_CHARGING: String = "usual.event.CHARGING"
    public static const COMMON_EVENT_CONFIGURATION_CHANGED: String = "usual.event.CONFIGURATION_CHANGED"
    public static const COMMON_EVENT_CLOSE_SYSTEM_DIALOGS: String = "usual.event.CLOSE_SYSTEM_DIALOGS"
    public static const COMMON_EVENT_DISK_EJECT: String = "usual.event.data.DISK_EJECT"
    public static const COMMON_EVENT_DISK_UNMOUNTABLE: String = "usual.event.data.DISK_UNMOUNTABLE"
    public static const COMMON_EVENT_DISK_BAD_REMOVAL: String = "usual.event.data.DISK_BAD### static const COMMON_EVENT_ABILITY_ADDED

```cangjie
public static const COMMON_EVENT_ABILITY_ADDED: String = "common.event.ABILITY_ADDED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for ability addition.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_ABILITY_REMOVED

```cangjie
public static const COMMON_EVENT_ABILITY_REMOVED: String = "common.event.ABILITY_REMOVED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for ability removal.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_ABILITY_UPDATED

```cangjie
public static const COMMON_EVENT_ABILITY_UPDATED: String = "common.event.ABILITY_UPDATED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for ability update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_ACCOUNT_DELETED

```cangjie
public static const COMMON_EVENT_ACCOUNT_DELETED: String = "usual.event.data.ACCOUNT_DELETED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for account deletion.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_AIRPLANE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_AIRPLANE_MODE_CHANGED: String = "usual.event.AIRPLANE_MODE"
```

**Description:** Indicates a common event for airplane mode change on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BATTERY_CHANGED

```cangjie
public static const COMMON_EVENT_BATTERY_CHANGED: String = "usual.event.BATTERY_CHANGED"
```

**Description:** Indicates a common event for changes in battery charging status, level, and other information.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BATTERY_LOW

```cangjie
public static const COMMON_EVENT_BATTERY_LOW: String = "usual.event.BATTERY_LOW"
```

**Description:** Indicates a common event for low battery level.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BATTERY_OKAY

```cangjie
public static const COMMON_EVENT_BATTERY_OKAY: String = "usual.event.BATTERY_OKAY"
```

**Description:** Indicates a common event when the battery exits low-level state.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.AUDIO_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP sink audio state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.CONNECT_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP sink connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.PLAYING_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP sink playback state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.AVRCP_CONNECT_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP source AVRCP connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CODEC_VALUE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP audio codec state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CONNECT_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP source connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CURRENT_DEVICE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event when a device connected via Bluetooth A2DP becomes active.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.PLAYING_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP source playback state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AG_CALL_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth hands-free call state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT: String = "usual.event.bluetooth.handsfreeunit.AG_COMMON_EVENT"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth hands-free audio gateway state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AUDIO_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth hands-free audio state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.CONNECT_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth hands-free connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.AUDIO_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth A2DP connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CONNECT_STATE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for Bluetooth hands-free communication connection state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CURRENT_DEVICE_UPDATE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event when a device connected via Bluetooth hands-free becomes active.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED: String = "usual.event.bluetooth.host.DISCOVERY_FINISHED"
```

**Description:** Indicates a common event for Bluetooth scan completion on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED: String = "usual.event.bluetooth.host.DISCOVERY_STARTED"
```

**Description:** Indicates a common event for Bluetooth scan initiation on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE: String = "usual.event.bluetooth.host.NAME_UPDATE"
```

**Description:** Indicates a common event for Bluetooth adapter name change on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE: String = "usual.event.bluetooth.hhost.REQ_DISABLE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for user request to disable Bluetooth.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE: String = "usual.event.bluetooth.host.REQ_DISCOVERABLE"
```

**Description:** Indicates a common event for user request to enable Bluetooth scanning.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE: String = "usual.event.bluetooth.host.REQ_ENABLE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event for user request to enable Bluetooth.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22### static const COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE: String = "usual.event.bluetooth.host.SCAN_MODE_UPDATE"
```

**Description:** (Reserved event, not yet supported) Represents a common event for changes in device Bluetooth scan mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE: String = "usual.event.bluetooth.host.STATE_UPDATE"
```

**Description:** Represents a common event for changes in Bluetooth adapter state, such as Bluetooth being turned on or off.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_CONNECTED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for establishing a low-level (ACL) connection with a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_DISCONNECTED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for disconnection of a low-level (ACL) connection from a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.BATTERY_VALUE_UPDATE"
```

**Description:** (Reserved event, not yet supported) Represents a common event for the first retrieval or change in battery level of a remote Bluetooth device since the last retrieval.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.CLASS_VALUE_UPDATE"
```

**Description:** (Reserved event, not yet supported) Represents a common event for the first retrieval or change in battery level of a remote Bluetooth device since the last retrieval.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL: String = "usual.event.bluetooth.remotedevice.CONNECT_CANCEL"
```

**Description:** (Reserved event, not yet supported) Represents a common event for cancellation of connection with a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY: String = "usual.event.bluetooth.remotedevice.CONNECT_REPLY"
```

**Description:** (Reserved event, not yet supported) Represents a common event for response to a remote Bluetooth device connection request.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ: String = "usual.event.bluetooth.remotedevice.CONNECT_REQ"
```

**Description:** (Reserved event, not yet supported) Represents a common event for a remote Bluetooth device connection request.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED: String = "usual.event.bluetooth.remotedevice.DISCOVERED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for discovery of a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE: String = "usual.event.bluetooth.remotedevice.NAME_UPDATE"
```

**Description:** Represents a common event for the first retrieval or change in friendly name of a remote Bluetooth device since the last retrieval.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL: String = "usual.event.bluetooth.remotedevice.PAIRING_CANCEL"
```

**Description:** (Reserved event, not yet supported) Represents a common event for cancellation of Bluetooth pairing.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ: String = "usual.event.bluetooth.remotedevice.PAIRING_REQ"
```

**Description:** (Reserved event, not yet supported) Represents a common event for a remote Bluetooth device pairing request.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE: String = "usual.event.bluetooth.remotedevice.PAIR_STATE"
```

**Description:** (Reserved event, not yet supported) Represents a common event for changes in connection state of a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT: String = "usual.event.bluetooth.remotedevice.SDP_RESULT"
```

**Description:** (Reserved event, not yet supported) Represents a common event for SDP state of a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE: String = "usual.event.bluetooth.remotedevice.UUID_VALUE"
```

**Description:** Represents a common event for UUID connection state of a remote Bluetooth device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BOOT_COMPLETED

```cangjie
public static const COMMON_EVENT_BOOT_COMPLETED: String = "usual.event.BOOT_COMPLETED"
```

**Description:** Represents a common event for user completion of boot and system loading.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_BUNDLE_REMOVED

```cangjie
public static const COMMON_EVENT_B BUNDLE_REMOVED: String = "usual.event.BUNDLE_REMOVED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for uninstallation of an installed bundle from the device while retaining application data.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CALL_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_CALL_STATE_CHANGED: String = "usual.event.CALL_STATE_CHANGED"
```

**Description:** Represents a common event for call state updates.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CHARGE_IDLE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_CHARGE_IDLE_MODE_CHANGED: String = "usual.event.CHARGE_IDLE_MODE_CHANGED"
```

**Description:** Represents a common event for device entering charging idle mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CHARGING

```cangjie
public static const COMMON_EVENT_CHARGING: String = "usual.event.CHARGING"
```

**Description:** Represents a common event for system starting battery charging.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CLOSE_SYSTEM_DIALOGS

```cangjie
public static const COMMON_EVENT_CLOSE_SYSTEM_DIALOGS: String = "usual.event.CLOSE_SYSTEM_DIALOGS"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user closing temporary system dialogs.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CONFIGURATION_CHANGED

```cangjie
public static const COMMON_EVENT_CONFIGURATION_CHANGED: String = "usual.event.CONFIGURATION_CHANGED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for changes in device state (e.g., orientation and locale).

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_CONNECTIVITY_CHANGE

```cangjie
public static const COMMON_EVENT_CONNECTIVITY_CHANGE: String = "usual.event.CONNECTIVITY_CHANGE"
```

**Description:** Represents a common event for network connection state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DATE_CHANGED

```cangjie
public static const COMMON_EVENT_DATE_CHANGED: String = "usual.event.DATE_CHANGED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for system date changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED: String = "usual.event.DEVICE_IDLE_MODE_CHANGED"
```

**Description:** Represents a common event for changes in system standby idle mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISCHARGING

```cangjie
public static const COMMON_EVENT_DISCHARGING: String = "usual.event.DISCHARGING"
```

**Description:** Represents a common event for system stopping battery charging.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISK_BAD_REMOVAL

```cangjie
public static const COMMON_EVENT_DISK_BAD_REMOVAL: String = "usual.event.data.DISK_BAD_REMOVAL"
```

**Description:** (Reserved event, not yet supported) Represents a common event for external storage device state changing to removal while mounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISK_EJECT

```cangjie
public static const COMMON_EVENT_DISK_EJECT: String = "usual.event.data.DISK_EJECT"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user indicating intent to remove external storage media.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22### static const COMMON_EVENT_DISK_MOUNTED

```cangjie
public static const COMMON_EVENT_DISK_MOUNTED: String = "usual.event.data.DISK_MOUNTED"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for external storage device status changing to mounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISK_REMOVED

```cangjie
public static const COMMON_EVENT_DISK_REMOVED: String = "usual.event.data.DISK_REMOVED"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for external storage device status changing to removed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISK_UNMOUNTABLE

```cangjie
public static const COMMON_EVENT_DISK_UNMOUNTABLE: String = "usual.event.data.DISK_UNMOUNTABLE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for external storage device status changing to unmountable when inserted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISK_UNMOUNTED

```cangjie
public static const COMMON_EVENT_DISK_UNMOUNTED: String = "usual.event.data.DISK_UNMOUNTED"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for external storage device status changing to unmounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN: String = "common.event.DISTRIBUTED_ACCOUNT_LOGIN"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for successful distributed account login.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOFF"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for distributed account logout.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOUT"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for successful distributed account sign-out.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID: String = "common.event.DISTRIBUTED_ACCOUNT_TOKEN_INVALID"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for invalid distributed account token.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_DRIVE_MODE

```cangjie
public static const COMMON_EVENT_DRIVE_MODE: String = "common.event.DRIVE_MODE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for system entering drive mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE

```cangjie
public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_AVAILABLE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for applications installed on external storage becoming available to the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE

```cangjie
public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_UNAVAILABLE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for applications installed on external storage becoming unavailable to the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_FOUNDATION_READY

```cangjie
public static const COMMON_EVENT_FOUNDATION_READY: String = "common.event.FOUNDATION_READY"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for foundation being ready.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_HOME_MODE

```cangjie
public static const COMMON_EVENT_HOME_MODE: String = "common.event.HOME_MODE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for system entering HOME mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_HTTP_PROXY_CHANGE

```cangjie
public static const COMMON_EVENT_HTTP_PROXY_CHANGE: String = "usual.event.HTTP_PROXY_CHANGE"
```

**Function:** Indicates changes in HTTP proxy configuration.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_ACTIVE

```cangjie
public static const COMMON_EVENT_IVI_ACTIVE: String = "common.event.IVI_ACTIVE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for battery service being active.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_EXTREME_TEMPERATURE

```cangjie
public static const COMMON_EVENT_IVI_EXTREME_TEMPERATURE: String = "common.event.IVI_EXTREME_TEMPERATURE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for IVI having extremely high temperature.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_HIGH_TEMPERATURE

```cangjie
public static const COMMON_EVENT_IVI_HIGH_TEMPERATURE: String = "common.event.IVI_HIGH_TEMPERATURE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for IVI having excessively high temperature.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_LASTMODE_SAVE

```cangjie
public static const COMMON_EVENT_IVI_LASTMODE_SAVE: String = "common.event.IVI_LASTMODE_SAVE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for third-party applications saving their last mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_PAUSE

```cangjie
public static const COMMON_EVENT_IVI_PAUSE: String = "common.event.IVI_PAUSE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for IVI entering sleep mode and notifying applications to stop playback.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_SLEEP

```cangjie
public static const COMMON_EVENT_IVI_SLEEP: String = "common.event.IVI_SLEEP"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for vehicle's In-Vehicle Infotainment (IVI) system entering sleep mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_STANDBY

```cangjie
public static const COMMON_EVENT_IVI_STANDBY: String = "common.event.IVI_STANDBY"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for third-party applications pausing current work.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL

```cangjie
public static const COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL: String = "common.event.IVI_TEMPERATURE_ABNORMAL"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for vehicle system having extreme temperature.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_TEMPERATURE_RECOVERY

```cangjie
public static const COMMON_EVENT_IVI_TEMPERATURE_RECOVERY: String = "common.event.IVI_TEMPERATURE_RECOVERY"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for vehicle system temperature returning to normal.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_VOLTAGE_ABNORMAL

```cangjie
public static const COMMON_EVENT_IVI_VOLTAGE_ABNORMAL: String = "common.event.IVI_VOLTAGE_ABNORMAL"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for abnormal voltage in vehicle power system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_IVI_VOLTAGE_RECOVERY

```cangjie
public static const COMMON_EVENT_IVI_VOLTAGE_RECOVERY: String = "common.event.IVI_VOLTAGE_RECOVERY"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for vehicle power system voltage returning to normal.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_LOCALE_CHANGED

```cangjie
public static const COMMON_EVENT_LOCALE_CHANGED: String = "usual.event.LOCALE_CHANGED"
```

**Function:** Indicates a public event for device locale settings being changed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_LOCATION_MODE_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_LOCATION_MODE_STATE_CHANGED: String = "usual.event.location.MODE_STATE_CHANGED"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for system location mode being changed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_LOCKED_BOOT_COMPLETED

```cangjie
public static const COMMON_EVENT_LOCKED_BOOT_COMPLETED: String = "usual.event.LOCKED_BOOT_COMPLETED"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for user completing boot process with system loaded but screen still locked.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_MANAGE_PACKAGE_STORAGE

```cangjie
public static const COMMON_EVENT_MANAGE_PACKAGE_STORAGE: String = "usual.event.MANAGE_PACKAGE_STORAGE"
```

**Function:** (Reserved event, not yet supported) Indicates a public event for insufficient device storage space.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22### static const COMMON_EVENT_MY_PACKAGE_REPLACED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_REPLACED: String = "usual.event.MY_PACKAGE_REPLACED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where a new version of the application package has replaced the previous version.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_MY_PACKAGE_SUSPENDED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_SUSPENDED: String = "usual.event.MY_PACKAGE_SUSPENDED"
```

**Description:** Indicates a common event where an application package has been suspended.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_MY_PACKAGE_UNSUSPENDED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_UNSUSPENDED: String = "usual.event.MY_PACKAGE_UNSUSPENDED"
```

**Description:** Indicates a common event where an application package has been unsuspended.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_NETWORK_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_NETWORK_STATE_CHANGED: String = "usual.event.NETWORK_STATE_CHANGED"
```

**Description:** Indicates a common event where the network state has been updated.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED: String = "usual.event.nfc.action.ADAPTER_STATE_CHANGED"
```

**Description:** Indicates a common event where the NFC state of the device has changed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED: String = "usual.event.nfc.action.RF_FIELD_OFF_DETECTED"
```

**Description:** Indicates a common event where the NFC field strength has been detected to be off.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED: String = "usual.event.nfc.action.RF_FIELD_ON_DETECTED"
```

**Description:** Indicates a common event where the NFC field strength has been detected to be on.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_OFFICE_MODE

```cangjie
public static const COMMON_EVENT_OFFICE_MODE: String = "common.event.OFFICE_MODE"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where the system is in office mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGES_SUSPENDED

```cangjie
public static const COMMON_EVENT_PACKAGES_SUSPENDED: String = "usual.event.PACKAGES_SUSPENDED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where application packages have been suspended.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGES_UNSUSPENDED

```cangjie
public static const COMMON_EVENT_PACKAGES_UNSUSPENDED: String = "usual.event.PACKAGES_UNSUSPENDED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where application packages have been unsuspended.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_ADDED

```cangjie
public static const COMMON_EVENT_PACKAGE_ADDED: String = "usual.event.PACKAGE_ADDED"
```

**Description:** Indicates a common event where a new application package has been installed on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_CACHE_CLEARED

```cangjie
public static const COMMON_EVENT_PACKAGE_CACHE_CLEARED: String = "usual.event.PACKAGE_CACHE_CLEARED"
```

**Description:** Indicates a common event where the user has cleared the cache data of an application package.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_CHANGED

```cangjie
public static const COMMON_EVENT_PACKAGE_CHANGED: String = "usual.event.PACKAGE_CHANGED"
```

**Description:** Indicates a common event where an application package has been changed (e.g., components in the package have been enabled or disabled).

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_DATA_CLEARED

```cangjie
public static const COMMON_EVENT_PACKAGE_DATA_CLEARED: String = "usual.event.PACKAGE_DATA_CLEARED"
```

**Description:** Indicates a common event where the user has cleared the data of an application package.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_FIRST_LAUNCH

```cangjie
public static const COMMON_EVENT_PACKAGE_FIRST_LAUNCH: String = "usual.event.PACKAGE_FIRST_LAUNCH"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where an installed application has been launched for the first time.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_FULLY_REMOVED

```cangjie
public static const COMMON_EVENT_PACKAGE_FULLY_REMOVED: String = "usual.event.PACKAGE_FULLY_REMOVED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where an installed application has been completely uninstalled from the device (including application data and code).

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION

```cangjie
public static const COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION: String = "usual.event.PACKAGE_NEEDS_VERIFICATION"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where an application requires system verification.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_REMOVED

```cangjie
public static const COMMON_EVENT_PACKAGE_REMOVED: String = "usual.event.PACKAGE_REMOVED"
```

**Description:** Indicates a common event where an installed application has been uninstalled from the device, but the application data is retained.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_REPLACED

```cangjie
public static const COMMON_EVENT_PACKAGE_REPLACED: String = "usual.event.PACKAGE_REPLACED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where a new version of an installed application package has replaced the old version on the device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_RESTARTED

```cangjie
public static const COMMON_EVENT_PACKAGE_RESTARTED: String = "usual.event.PACKAGE_RESTARTED"
```

**Description:** Indicates a common event where the user has restarted an application package and killed all its processes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_PACKAGE_VERIFIED

```cangjie
public static const COMMON_EVENT_PACKAGE_VERIFIED: String = "usual.event.PACKAGE_VERIFIED"
```

**Description:** (Reserved event, not currently supported) Indicates a common event where an application has been verified by the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_POWER_CONNECTED

```cangjie
public static const COMMON_EVENT_POWER_CONNECTED: String = "usual.event.POWER_CONNECTED"
```

**Description:** Indicates a common event where the device has been connected to an external power source.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_POWER_DISCONNECTED

```cangjie
public static const COMMON_EVENT_POWER_DISCONNECTED: String = "usual.event.POWER_DISCONNECTED"
```

**Description:** Indicates a common event where the device has been disconnected from an external power source.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_POWER_SAVE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_POWER_SAVE_MODE_CHANGED: String = "usual.event.POWER_SAVE_MODE_CHANGED"
```

**Description:** Indicates a common event where the system power-saving mode has changed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_QUICK_FIX_APPLY_RESULT

```cangjie
public static const COMMON_EVENT_QUICK_FIX_APPLY_RESULT: String = "usual.event.QUICK_FIX_APPLY_RESULT"
```

**Description:** Indicates a common event for quick fix application.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_QUICK_FIX_REVOKE_RESULT

```cangjie
public static const COMMON_EVENT_QUICK_FIX_REVOKE_RESULT: String = "usual.event.QUICK_FIX_REVOKE_RESULT"
```

**Description:** Indicates a common event for revoking a quick fix event.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SCREEN_LOCKED

```cangjie
public static const COMMON_EVENT_SCREEN_LOCKED: String = "usual.event.SCREEN_LOCKED"
```

**Description:** Indicates a common event for screen lock.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SCREEN_OFF

```cangjie
public static const COMMON_EVENT_SCREEN_OFF: String = "usual.event.SCREEN_OFF"
```

**Description:** Indicates a common event where the device screen is turned off and the device is in sleep mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SCREEN_ON

```cangjie
public static const COMMON_EVENT_SCREEN_ON: String = "usual.event.SCREEN_ON"
```

**Description:** Indicates a common event where the device screen is turned on and the device is in interactive mode.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22### static const COMMON_EVENT_SCREEN_UNLOCKED

```cangjie
public static const COMMON_EVENT_SCREEN_UNLOCKED: String = "usual.event.SCREEN_UNLOCKED"
```

**Description:** Represents a common event for screen unlock.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SHUTDOWN

```cangjie
public static const COMMON_EVENT_SHUTDOWN: String = "usual.event.SHUTDOWN"
```

**Description:** Represents a common event for device shutdown.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SIGNAL_INFO_CHANGED

```cangjie
public static const COMMON_EVENT_SIGNAL_INFO_CHANGED: String = "usual.event.SIGNAL_INFO_CHANGED"
```

**Description:** Represents a common event for signal information update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SIM_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_SIM_STATE_CHANGED: String = "usual.event.SIM_STATE_CHANGED"
```

**Description:** Represents a common event for SIM card state update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SLOT_CHANGE

```cangjie
public static const COMMON_EVENT_SLOT_CHANGE: String = "usual.event.SLOT_CHANGE"
```

**Description:** Represents a common event for notification channel update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SPLIT_SCREEN

```cangjie
public static const COMMON_EVENT_SPLIT_SCREEN: String = "common.event.SPLIT_SCREEN"
```

**Description:** Represents a common event for split-screen operation.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_SPN_INFO_CHANGED

```cangjie
public static const COMMON_EVENT_SPN_INFO_CHANGED: String = "usual.event.SPN_INFO_CHANGED"
```

**Description:** Represents a common event for SPN display information update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_THERMAL_LEVEL_CHANGED

```cangjie
public static const COMMON_EVENT_THERMAL_LEVEL_CHANGED: String = "usual.event.THERMAL_LEVEL_CHANGED"
```

**Description:** Represents a common event for device thermal state.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_TIMEZONE_CHANGED

```cangjie
public static const COMMON_EVENT_TIMEZONE_CHANGED: String = "usual.event.TIMEZONE_CHANGED"
```

**Description:** Represents a common event for system timezone change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_TIME_CHANGED

```cangjie
public static const COMMON_EVENT_TIME_CHANGED: String = "usual.event.TIME_CHANGED"
```

**Description:** Represents a common event for system time setting.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_TIME_TICK

```cangjie
public static const COMMON_EVENT_TIME_TICK: String = "usual.event.TIME_TICK"
```

**Description:** Represents a common event for system time change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_UID_REMOVED

```cangjie
public static const COMMON_EVENT_UID_REMOVED: String = "usual.event.UID_REMOVED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user ID removal from the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_ACCESSORY_ATTACHED

```cangjie
public static const COMMON_EVENT_USB_ACCESSORY_ATTACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_ATTACHED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for USB accessory connection.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_ACCESSORY_DETACHED

```cangjie
public static const COMMON_EVENT_USB_ACCESSORY_DETACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_DETACHED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for USB accessory detachment.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_DEVICE_ATTACHED

```cangjie
public static const COMMON_EVENT_USB_DEVICE_ATTACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_ATTACHED"
```

**Description:** Represents a common event for USB device mounting when the user device acts as a USB host.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_DEVICE_DETACHED

```cangjie
public static const COMMON_EVENT_USB_DEVICE_DETACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_DETACHED"
```

**Description:** Represents a common event for USB device detachment when the user device acts as a USB host.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_PORT_CHANGED

```cangjie
public static const COMMON_EVENT_USB_PORT_CHANGED: String = "usual.event.hardware.usb.action.USB_PORT_CHANGED"
```

**Description:** Represents a common event for USB port state change on the user device.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USB_STATE

```cangjie
public static const COMMON_EVENT_USB_STATE: String = "usual.event.hardware.usb.action.USB_STATE"
```

**Description:** Represents a common event for USB device state change.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_ADDED

```cangjie
public static const COMMON_EVENT_USER_ADDED: String = "usual.event.USER_ADDED"
```

**Description:** Represents a common event for user addition to the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_BACKGROUND

```cangjie
public static const COMMON_EVENT_USER_BACKGROUND: String = "usual.event.USER_BACKGROUND"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user being moved to background.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_FOREGROUND

```cangjie
public static const COMMON_EVENT_USER_FOREGROUND: String = "usual.event.USER_FOREGROUND"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user being moved to foreground.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_INFO_UPDATED

```cangjie
public static const COMMON_EVENT_USER_INFO_UPDATED: String = "usual.event.USER_INFO_UPDATED"
```

**Description:** Represents a common event for user information update.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_REMOVED

```cangjie
public static const COMMON_EVENT_USER_REMOVED: String = "usual.event.USER_REMOVED"
```

**Description:** Represents a common event for user removal from the system.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_STARTED

```cangjie
public static const COMMON_EVENT_USER_STARTED: String = "usual.event.USER_STARTED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user startup.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_STARTING

```cangjie
public static const COMMON_EVENT_USER_STARTING: String = "usual.event.USER_STARTING"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user startup.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_STOPPED

```cangjie
public static const COMMON_EVENT_USER_STOPPED: String = "usual.event.USER_STOPPED"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user stop.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_STOPPING

```cangjie
public static const COMMON_EVENT_USER_STOPPING: String = "usual.event.USER_STOPPING"
```

**Description:** (Reserved event, not yet supported) Represents a common event for user being stopped.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_SWITCHED

```cangjie
public static const COMMON_EVENT_USER_SWITCHED: String = "usual.event.USER_SWITCHED"
```

**Description:** Represents a common event for ongoing user switch.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_USER_UNLOCKED

```cangjie
public static const COMMON_EVENT_USER_UNLOCKED: String = "usual.event.USER_UNLOCKED"
```

**Description:** Represents a common event for credential-encrypted storage unlock of the current user after device reboot.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22### static const COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED

```cangjie
public static const COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED: String = "usual.event.data.VISIBLE_ACCOUNTS_UPDATED"
```

**Description:** (Reserved event, currently unsupported) Indicates a common event for account visibility changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_VOLUME_BAD_REMOVAL

```cangjie
public static const COMMON_EVENT_VOLUME_BAD_REMOVAL: String = "usual.event.data.VOLUME_BAD_REMOVAL"
```

**Description:** Indicates a common event when external storage device status changes to removed while mounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_VOLUME_EJECT

```cangjie
public static const COMMON_EVENT_VOLUME_EJECT: String = "usual.event.data.VOLUME_EJECT"
```

**Description:** Indicates a common event when the user has expressed intent to remove external storage media.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_VOLUME_MOUNTED

```cangjie
public static const COMMON_EVENT_VOLUME_MOUNTED: String = "usual.event.data.VOLUME_MOUNTED"
```

**Description:** Indicates a common event when external storage device status changes to mounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_VOLUME_REMOVED

```cangjie
public static const COMMON_EVENT_VOLUME_REMOVED: String = "usual.event.data.VOLUME_REMOVED"
```

**Description:** Indicates a common event when external storage device status changes to removed.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_VOLUME_UNMOUNTED

```cangjie
public static const COMMON_EVENT_VOLUME_UNMOUNTED: String = "usual.event.data.VOLUME_UNMOUNTED"
```

**Description:** Indicates a common event when external storage device status changes to unmounted.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_AP_STA_JOIN

```cangjie
public static const COMMON_EVENT_WIFI_AP_STA_JOIN: String = "usual.event.wifi.WIFI_HS_STA_JOIN"
```

**Description:** Indicates a common event when a client joins the current device's Wi-Fi hotspot.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_AP_STA_LEAVE

```cangjie
public static const COMMON_EVENT_WIFI_AP_STA_LEAVE: String = "usual.event.wifi.WIFI_HS_STA_LEAVE"
```

**Description:** Indicates a common event when a client disconnects from the current device's Wi-Fi hotspot.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_CONN_STATE

```cangjie
public static const COMMON_EVENT_WIFI_CONN_STATE: String = "usual.event.wifi.CONN_STATE"
```

**Description:** Indicates a common event when Wi-Fi connection state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_HOTSPOT_STATE

```cangjie
public static const COMMON_EVENT_WIFI_HOTSPOT_STATE: String = "usual.event.wifi.HOTSPOT_STATE"
```

**Description:** Indicates a common event for Wi-Fi hotspot state changes, such as enabled or disabled.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE

```cangjie
public static const COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE: String = "usual.event.wifi.mplink.STATE_CHANGE"
```

**Description:** Indicates a common event when MPLink (enhanced Wi-Fi capability) state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_CONN_STATE

```cangjie
public static const COMMON_EVENT_WIFI_P2P_CONN_STATE: String = "usual.event.wifi.p2p.CONN_STATE_CHANGE"
```

**Description:** Indicates a common event when Wi-Fi P2P connection state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED: String = "usual.event.wifi.p2p.CURRENT_DEVICE_CHANGE"
```

**Description:** Indicates a common event when Wi-Fi P2P current device state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED: String = "usual.event.wifi.p2p.GROUP_STATE_CHANGED"
```

**Description:** Indicates a common event when Wi-Fi P2P group information changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED: String = "usual.event.wifi.p2p.PEER_DISCOVERY_STATE_CHANGE"
```

**Description:** Indicates a common event when Wi-Fi P2P discovery state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED: String = "usual.event.wifi.p2p.DEVICES_CHANGE"
```

**Description:** Indicates a common event when Wi-Fi P2P peer state changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_P2P_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_STATE_CHANGED: String = "usual.event.wifi.p2p.STATE_CHANGE"
```

**Description:** Indicates a common event for Wi-Fi P2P state changes (e.g., enabled/disabled).

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_POWER_STATE

```cangjie
public static const COMMON_EVENT_WIFI_POWER_STATE: String = "usual.event.wifi.POWER_STATE"
```

**Description:** Indicates a common event for Wi-Fi state changes (e.g., enabled/disabled).

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_RSSI_VALUE

```cangjie
public static const COMMON_EVENT_WIFI_RSSI_VALUE: String = "usual.event.wifi.RSSI_VALUE"
```

**Description:** Indicates a common event when Wi-Fi signal strength (RSSI) changes.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22

### static const COMMON_EVENT_WIFI_SCAN_FINISHED

```cangjie
public static const COMMON_EVENT_WIFI_SCAN_FINISHED: String = "usual.event.wifi.SCAN_FINISHED"
```

**Description:** Indicates a common event when Wi-Fi access points have been scanned and verified as available.

**Type:** String

**System Capability:** SystemCapability.Notification.CommonEvent

**Since:** 22