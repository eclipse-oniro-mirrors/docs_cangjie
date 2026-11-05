# ohos.notification_manager (Notification Management)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The notification_manager module provides notification management capabilities. You can use this module to publish and update notifications, cancel notifications, query and request notification authorization, and set notification badges.

For details about the error codes in this section, see [Notification Error Codes](./cj-errorcode-notification.md).

## Importing the Module

```cangjie
import kit.NotificationKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-notes).

## func cancelAll(AsyncCallback\<Unit>)

```cangjie
public func cancelAll(callback: AsyncCallback<Unit>): Unit
```

**Description:** Cancels all notifications of this application. This API uses an asynchronous callback to return the result.

After cancellation, all notifications of the current application will be removed from the notification center, status bar, and other locations, and will no longer be visible to the user. This API is suitable for scenarios such as application exit or manual clearing of all notifications by the user.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback\<Unit>|Yes|-|Callback used to return the result. If the operation is successful, `err` is `None`; otherwise, `err` contains error information.|

**Exceptions:**

- BusinessException: For details about the error codes, see [Notification Error Codes](./cj-errorcode-notification.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "cancelAll failed: code=${e.code}, message=${e.message}")
    } else {
        Hilog.info(0, "test", "cancelAll success")
    }
}
cancelAll(callback)
```

## func isNotificationEnabledSync()

```cangjie
public func isNotificationEnabledSync(): Bool
```

**Description:** Synchronously queries the notification authorization status of the current application.

This API returns the result synchronously, and is suitable for quickly checking whether the current application is allowed to send notifications before publishing notifications.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|**true** if the notification is enabled, **false** otherwise.|

**Exceptions:**

- BusinessException: For details about the error codes, see [Notification Error Codes](./cj-errorcode-notification.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.PerformanceAnalysisKit.Hilog

let enabled = isNotificationEnabledSync()
Hilog.info(0, "test", "notification enabled=${enabled}")
```

## func publish(NotificationRequest, AsyncCallback\<Unit>)

```cangjie
public func publish(request: NotificationRequest, callback: AsyncCallback<Unit>): Unit
```

**Description:** Publishes a notification. This API uses an asynchronous callback to return the result.

After a notification is published, it will be displayed in the device's notification center, status bar, and other locations. If the ID and label of the newly published notification are the same as those of an already published notification, the new notification will replace the original one, achieving a notification update effect.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|request|[NotificationRequest](#class-notificationrequest)|Yes|-|Content and related configuration of the notification to publish.|
|callback|AsyncCallback\<Unit>|Yes|-|Callback used to return the result. If the operation is successful, `err` is `None`; otherwise, `err` contains error information.|

**Exceptions:**

- BusinessException: For details about the error codes, see [Notification Error Codes](./cj-errorcode-notification.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |
  | 1600004 | Notification disabled. |
  | 1600005 | Notification slot disabled. |
  | 1600007 | The notification does not exist. |
  | 1600009 | The notification sending frequency reaches the upper limit. |
  | 1600012 | No memory space. |
  | 1600014 | No permission. |
  | 1600015 | The current notification status does not support duplicate configurations. |
  | 1600016 | The notification version for this update is too low. |
  | 1600020 | The application is not allowed to send notifications due to permission settings. |
  | 1600029 | The system failed to find the ExtensionAbility instance for the custom Live View widget template. |
  | 2300007 | Network unreachable. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let basicContent = NotificationBasicContent("Title", "Notification content")
let content = NotificationContent(ContentType.NotificationContentBasicText)
content.normal = Some(basicContent)
let request = NotificationRequest(content)
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "publish failed: code=${e.code}, message=${e.message}")
    } else {
        Hilog.info(0, "test", "publish success")
    }
}
publish(request, callback)
```

## func requestEnableNotification(UIAbilityContext, AsyncCallback\<Unit>)

```cangjie
public func requestEnableNotification(context: UIAbilityContext, callback: AsyncCallback<Unit>): Unit
```

**Description:** Requests notification to be enabled for this application. This API uses an asynchronous callback to return the result.

You can call this API before publishing a notification to display a dialog box prompting the user to enable notification for your application. This API can be called only after the application UI is loaded (that is, **loadContent** is successfully called).

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|Yes|-|Application context bound to the notification dialog box.|
|callback|AsyncCallback\<Unit>|Yes|-|Callback used to return the result. If the operation is successful, `err` is `None`; otherwise, `err` contains error information.|

**Exceptions:**

- BusinessException: For details about the error codes, see [Notification Error Codes](./cj-errorcode-notification.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |
  | 1600004 | Notification disabled. |
  | 1600013 | A notification dialog box is already displayed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let ctx = Global.abilityContext // Obtain the Context application context. Configure the template manually. For details, see the usage instructions.
let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "requestEnableNotification failed: code=${e.code}, message=${e.message}")
    } else {
        Hilog.info(0, "test", "requestEnableNotification success")
    }
}
requestEnableNotification(ctx, callback)
```

## func setBadgeNumber(Int32, AsyncCallback\<Unit>)

```cangjie
public func setBadgeNumber(badgeNumber: Int32, callback: AsyncCallback<Unit>): Unit
```

**Description:** Sets the notification badge number. This API uses an asynchronous callback to return the result.

A badge is a numeric identifier displayed in the upper right corner of an application's desktop icon, used to prompt the user about the number of unprocessed notifications. After setting, the desktop icon will display the corresponding badge number.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|badgeNumber|Int32|Yes|-|Notification badge number to set. If **badgeNumber** is set to a value less than or equal to **0**, badges are cleared; if the value is greater than **99**, **99+** is displayed on the badge.|
|callback|AsyncCallback\<Unit>|Yes|-|Callback used to return the result. If the operation is successful, `err` is `None`; otherwise, `err` contains error information.|

**Exceptions:**

- BusinessException: For details about the error codes, see [Notification Error Codes](./cj-errorcode-notification.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |
  | 1600012 | No memory space. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let callback: AsyncCallback<Unit> = {
    err: Option<BusinessException>, data: Option<Unit> =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "setBadgeNumber failed: code=${e.code}, message=${e.message}")
    } else {
        Hilog.info(0, "test", "setBadgeNumber success")
    }
}
setBadgeNumber(5, callback)
```

## class NotificationBasicContent

```cangjie
public open class NotificationBasicContent {
    public mut prop title: String
    public mut prop text: String
    public mut prop additionalText: ?String
    public mut prop lockscreenPicture: ?PixelMap
    public init(title: String, text: String)
}
```

**Description:** Describes the basic text notification, which is used to display the title and body content. It serves as the basic content structure for other notification types.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop additionalText

```cangjie
public mut prop additionalText: ?String
```

**Description:** Additional notification content, which supplements the notification content and is not displayed in the notification center. It defaults to empty. The size does not exceed 3072 bytes, and the excess part will be truncated.

**Type:** ?String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop lockscreenPicture

```cangjie
public mut prop lockscreenPicture: ?PixelMap
```

**Description:** Picture displayed on the lock screen. This parameter is left empty by default. Currently, only the live view notification is supported. The total number of the picture pixel bytes cannot exceed 192 KB. The recommended picture size is 128 × 128 pixels. The display effect depends on the device capability and notification center UI style.

**Type:** ?[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop text

```cangjie
public mut prop text: String
```

**Description:** Notification body content, displayed below the title. It cannot be an empty string. The size does not exceed 3072 bytes, and the excess part will be truncated.

**Type:** String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop title

```cangjie
public mut prop title: String
```

**Description:** Notification title, displayed at the top of the notification. It cannot be an empty string. The size does not exceed 1024 bytes, and the excess part will be truncated.

**Type:** String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### init(String, String)

```cangjie
public init(title: String, text: String)
```

**Description:** A constructor used to create a NotificationBasicContent object.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|title|String|Yes|-|Notification title, displayed at the top of the notification.|
|text|String|Yes|-|Notification body content, displayed below the title.|

## class NotificationContent

```cangjie
public class NotificationContent {
    public mut prop notificationContentType: ContentType
    public mut prop normal: ?NotificationBasicContent
    public init(notificationContentType: ContentType)
}
```

**Description:** Describes the notification contents.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop normal

```cangjie
public mut prop normal: ?NotificationBasicContent
```

**Description:** Basic notification content. This parameter is used when `notificationContentType` is `NotificationContentBasicText`. The notification displays the title and body in a plain text style.

**Type:** ?[NotificationBasicContent](#class-notificationbasiccontent)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop notificationContentType

```cangjie
public mut prop notificationContentType: ContentType
```

**Description:** Notification content type, used to specify the content layout type of the notification, which determines the display style of the notification in the notification center. It must be used together with the corresponding notification content object. For example, when this parameter is set to `NotificationContentBasicText`, the `normal` field must be specified at the same time.

**Type:** [ContentType](#enum-contenttype)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### init(ContentType)

```cangjie
public init(notificationContentType: ContentType)
```

**Description:** A constructor used to create a NotificationContent object.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|notificationContentType|[ContentType](#enum-contenttype)|Yes|-|Notification content type, used to specify the content layout type of the notification.|

## class NotificationRequest

```cangjie
public class NotificationRequest {
    public mut prop content: NotificationContent
    public mut prop id: ?Int32
    public mut prop notificationSlotType: ?SlotType
    public mut prop label: ?String
    public mut prop smallIcon: ?PixelMap
    public init(content: NotificationContent)
}
```

**Description:** Defines the data structure of a notification request, which is used to describe all information about a notification, including the notification content, identifier, display style, and interaction behavior.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop content

```cangjie
public mut prop content: NotificationContent
```

**Description:** Notification display content, including the notification title and body.

**Type:** [NotificationContent](#class-notificationcontent)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop id

```cangjie
public mut prop id: ?Int32
```

**Description:** Notification ID. The default value is **0**. If a notification with the same ID exists, the notification is updated. If no notification with the same ID exists, a new notification is created.

**Type:** ?Int32

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop label

```cangjie
public mut prop label: ?String
```

**Description:** Notification label. The `label` field functions similarly to an ID and can be used alone or combined with the ID to serve as the notification identifier. It is recommended to use the ID. If the `label` is not empty when a notification is published, the corresponding `label` must also be specified when the notification is updated or deleted. The size does not exceed 202 bytes, and the excess part will be truncated. The value is empty by default.

**Type:** ?String

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop notificationSlotType

```cangjie
public mut prop notificationSlotType: ?SlotType
```

**Description:** Notification slot type. The default value is `OtherTypes`. The notification reminder mode varies depending on the notification slot type.

**Type:** ?[SlotType](#enum-slottype)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### prop smallIcon

```cangjie
public mut prop smallIcon: ?PixelMap
```

**Description:** Small notification icon. This parameter is left empty by default. The total number of the icon pixel bytes cannot exceed 192 KB. The setting does not take effect if the limit is exceeded. When **smallIcon** is not set, the notification displays the default application icon. The recommended icon size is 128 × 128 pixels. The display effect depends on the device capability and notification center UI style.

**Type:** ?[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**Accessibility:** Read-write

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### init(NotificationContent)

```cangjie
public init(content: NotificationContent)
```

**Description:** A constructor used to create a NotificationRequest object.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|content|[NotificationContent](#class-notificationcontent)|Yes|-|Notification display content, including the notification title and body.|

## enum ContentType

```cangjie
public enum ContentType {
    | NotificationContentBasicText
    | ...
}
```

**Description:** Enumerates the notification content types.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parent Types:**

- Equatable\<[ContentType](#enum-contenttype)>
- ToString

### NotificationContentBasicText

```cangjie
NotificationContentBasicText
```

**Description:** Normal text notification.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Description:** Converts the notification content type to its string representation.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the notification content type.|

### func ==(ContentType)

```cangjie
public operator func ==(other: ContentType): Bool
```

**Description:** Checks whether two notification content types are equal.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ContentType](#enum-contenttype)|Yes|-|Notification content type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|**true** if the two values are equal, **false** otherwise.|

### func !=(ContentType)

```cangjie
public operator func !=(other: ContentType): Bool
```

**Description:** Checks whether two notification content types are unequal.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[ContentType](#enum-contenttype)|Yes|-|Notification content type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|**true** if the two values are unequal, **false** otherwise.|

## enum SlotType

```cangjie
public enum SlotType {
    | ContentInformation
    | CustomerService
    | EmergencyInformation
    | LiveView
    | OtherTypes
    | ServiceInformation
    | SocialCommunication
    | UnknownType
    | ...
}
```

**Description:** Enumerates the notification slot types. Different types correspond to different `SlotLevel` values, determining the reminder behavior of the notification.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parent Types:**

- Equatable\<[SlotType](#enum-slottype)>
- ToString

### ContentInformation

```cangjie
ContentInformation
```

**Description:** Content information. This type corresponds to the notification level `LEVEL_MIN`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### CustomerService

```cangjie
CustomerService
```

**Description:** Customer service message. This type is used for messages between users and customer service providers. The messages must be initiated by users. This type corresponds to the notification level `LEVEL_DEFAULT`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### EmergencyInformation

```cangjie
EmergencyInformation
```

**Description:** Emergency event.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### LiveView

```cangjie
LiveView
```

**Description:** Live view. A third-party application cannot directly create a notification of this type. Instead, after the system proxy creates a notification, the third-party application can publish the notification with the same ID to update the specified content. This type corresponds to the notification level `LEVEL_DEFAULT`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### OtherTypes

```cangjie
OtherTypes
```

**Description:** Other types. This type corresponds to the notification level `LEVEL_MIN`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### ServiceInformation

```cangjie
ServiceInformation
```

**Description:** Service information. This type corresponds to the notification level `LEVEL_HIGH`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### SocialCommunication

```cangjie
SocialCommunication
```

**Description:** Social communication. This type corresponds to the notification level `LEVEL_HIGH`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### UnknownType

```cangjie
UnknownType
```

**Description:** Unknown type. This type corresponds to the notification level `LEVEL_MIN`.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Description:** Converts the notification slot type to its string representation.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the notification slot type.|

### func ==(SlotType)

```cangjie
public operator func ==(other: SlotType): Bool
```

**Description:** Checks whether two notification slot types are equal.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SlotType](#enum-slottype)|Yes|-|Notification slot type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|**true** if the two values are equal, **false** otherwise.|

### func !=(SlotType)

```cangjie
public operator func !=(other: SlotType): Bool
```

**Description:** Checks whether two notification slot types are unequal.

**System Capability:** SystemCapability.Notification.Notification

**Since:** 26.1.0

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[SlotType](#enum-slottype)|Yes|-|Notification slot type to compare.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|**true** if the two values are unequal, **false** otherwise.|
