# ohos.notification_manager（通知管理）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

notification_manager模块提供通知管理的能力，应用可使用本模块完成通知的发布与更新、取消、通知授权状态查询与申请以及通知角标设置等操作。

本节错误码的详细介绍请参见[通知错误码](./cj-errorcode-notification.md)。

## 导入模块

```cangjie
import kit.NotificationKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func cancelAll(AsyncCallback\<Unit>)

```cangjie
public func cancelAll(callback: AsyncCallback<Unit>): Unit
```

**功能：** 取消当前应用的全部通知。该接口使用异步回调返回结果。

取消后，当前应用的全部通知将从通知中心、状态栏等位置移除，不再对用户可见。适用于应用退出或用户主动清空全部通知等场景。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|callback|AsyncCallback\<Unit>|是|-|用于返回结果的回调。成功时`err`为`None`；失败时`err`包含错误信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通知错误码](./cj-errorcode-notification.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |

**示例：**

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

**功能：** 同步查询当前应用的通知授权状态。

该接口同步返回结果，适用于在发布通知前快速判断应用是否允许发送通知的场景。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示通知已启用，false表示通知未启用。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通知错误码](./cj-errorcode-notification.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |

**示例：**

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

**功能：** 发布通知。该接口使用异步回调返回结果。

发布后，通知将显示在设备的通知中心、状态栏等位置。新发布通知的ID和标签与已发布通知相同时，新通知将替换原通知，实现通知更新。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|request|[NotificationRequest](#class-notificationrequest)|是|-|待发布通知的内容和相关配置。|
|callback|AsyncCallback\<Unit>|是|-|用于返回结果的回调。成功时`err`为`None`；失败时`err`包含错误信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通知错误码](./cj-errorcode-notification.md)。

  | 错误码ID | 错误信息 |
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

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let basicContent = NotificationBasicContent("标题", "通知内容")
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

**功能：** 请求为当前应用启用通知。该接口使用异步回调返回结果。

应用可在发布通知前调用该接口，弹出对话框提示用户为应用启用通知。该接口只能在应用界面加载完成后调用，即`loadContent`调用成功后。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext)|是|-|与通知对话框绑定的应用上下文。|
|callback|AsyncCallback\<Unit>|是|-|用于返回结果的回调。成功时`err`为`None`；失败时`err`包含错误信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通知错误码](./cj-errorcode-notification.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |
  | 1600004 | Notification disabled. |
  | 1600013 | A notification dialog box is already displayed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.NotificationKit.*
import kit.CangjieKit.{AsyncCallback, BusinessException}
import kit.PerformanceAnalysisKit.Hilog

let ctx = Global.abilityContext // 此处需手动配置模板，获取Context上下文。上下文获取方式请参见使用说明。
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

**功能：** 设置通知角标数量。该接口使用异步回调返回结果。

角标是显示在应用桌面图标右上角的数字标识，用于提示用户未处理的通知数量。设置后，桌面图标将显示对应的角标数字。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|badgeNumber|Int32|是|-|要设置的通知角标数量。小于或等于0时清除角标；大于99时显示99+。|
|callback|AsyncCallback\<Unit>|是|-|用于返回结果的回调。成功时`err`为`None`；失败时`err`包含错误信息。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[通知错误码](./cj-errorcode-notification.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | Capability not supported. |
  | 1600001 | Internal error. |
  | 1600002 | Marshalling or unmarshalling error. |
  | 1600003 | Failed to connect to the service. |
  | 1600012 | No memory space. |

**示例：**

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

**功能：** 基础文本通知内容，用于展示标题和正文，是其他通知类型的基础内容结构。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop additionalText

```cangjie
public mut prop additionalText: ?String
```

**功能：** 附加通知内容，用于补充通知内容，不在通知中心显示。默认值为空。长度不超过3072字节，超出部分将被截断。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop lockscreenPicture

```cangjie
public mut prop lockscreenPicture: ?PixelMap
```

**功能：** 锁屏图片。默认值为空。当前仅实况窗通知支持。图片像素总字节数不能超过192KB，推荐尺寸为128×128像素，实际显示效果取决于设备能力和通知中心UI样式。

**类型：** ?[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop text

```cangjie
public mut prop text: String
```

**功能：** 通知正文内容，显示在标题下方。不能为空字符串。长度不超过3072字节，超出部分将被截断。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop title

```cangjie
public mut prop title: String
```

**功能：** 通知标题，显示在通知顶部。不能为空字符串。长度不超过1024字节，超出部分将被截断。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### init(String, String)

```cangjie
public init(title: String, text: String)
```

**功能：** 创建基础文本通知内容对象。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|title|String|是|-|通知标题，显示在通知顶部。|
|text|String|是|-|通知正文内容，显示在标题下方。|

## class NotificationContent

```cangjie
public class NotificationContent {
    public mut prop notificationContentType: ContentType
    public mut prop normal: ?NotificationBasicContent
    public init(notificationContentType: ContentType)
}
```

**功能：** 通知内容。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop normal

```cangjie
public mut prop normal: ?NotificationBasicContent
```

**功能：** 基础通知内容。当`notificationContentType`为`NotificationContentBasicText`时使用，通知以纯文本样式显示标题和正文。

**类型：** ?[NotificationBasicContent](#class-notificationbasiccontent)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop notificationContentType

```cangjie
public mut prop notificationContentType: ContentType
```

**功能：** 通知内容类型，用于指定通知在通知中心的内容布局类型，需与对应的通知内容对象配合使用。例如设置为`NotificationContentBasicText`时，必须同时指定`normal`字段。

**类型：** [ContentType](#enum-contenttype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### init(ContentType)

```cangjie
public init(notificationContentType: ContentType)
```

**功能：** 创建通知内容对象。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|notificationContentType|[ContentType](#enum-contenttype)|是|-|通知内容类型，用于指定通知的内容布局类型。|

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

**功能：** 通知请求数据结构，用于描述通知的内容、标识、展示样式和交互行为等信息。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop content

```cangjie
public mut prop content: NotificationContent
```

**功能：** 通知展示内容，包括通知标题和正文。

**类型：** [NotificationContent](#class-notificationcontent)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop id

```cangjie
public mut prop id: ?Int32
```

**功能：** 通知ID。默认值为0。存在相同ID的通知时更新该通知，不存在时创建新通知。

**类型：** ?Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop label

```cangjie
public mut prop label: ?String
```

**功能：** 通知标签。`label`的作用与ID类似，可以单独使用，也可以与ID组合作为通知标识。建议使用ID。发布通知时若`label`不为空，更新或删除通知时也必须指定对应的`label`。长度不超过202字节，超出部分将被截断。默认值为空字符串。

**类型：** ?String

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop notificationSlotType

```cangjie
public mut prop notificationSlotType: ?SlotType
```

**功能：** 通知槽类型。默认值为`OtherTypes`。不同通知槽类型对应不同的通知提醒方式。

**类型：** ?[SlotType](#enum-slottype)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### prop smallIcon

```cangjie
public mut prop smallIcon: ?PixelMap
```

**功能：** 通知小图标。默认值为空。图标像素总字节数不能超过192KB，超出限制时设置不生效。未设置时，通知显示应用默认图标。推荐图标尺寸为128×128像素，实际显示效果取决于设备能力和通知中心UI样式。

**类型：** ?[PixelMap](../ImageKit/cj-apis-image.md#class-pixelmap)

**读写能力：** 可读写

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### init(NotificationContent)

```cangjie
public init(content: NotificationContent)
```

**功能：** 创建通知请求对象。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|content|[NotificationContent](#class-notificationcontent)|是|-|通知展示内容，包括通知标题和正文。|

## enum ContentType

```cangjie
public enum ContentType {
    | NotificationContentBasicText
    | ...
}
```

**功能：** 通知内容类型。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**父类型：**

- Equatable\<[ContentType](#enum-contenttype)>
- ToString

### NotificationContentBasicText

```cangjie
NotificationContentBasicText
```

**功能：** 普通文本通知。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将通知内容类型转换为字符串表示。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|通知内容类型的字符串表示。|

### func ==(ContentType)

```cangjie
public operator func ==(other: ContentType): Bool
```

**功能：** 判断两个通知内容类型是否相等。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ContentType](#enum-contenttype)|是|-|待比较的通知内容类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(ContentType)

```cangjie
public operator func !=(other: ContentType): Bool
```

**功能：** 判断两个通知内容类型是否不相等。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[ContentType](#enum-contenttype)|是|-|待比较的通知内容类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|

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

**功能：** 通知槽类型。不同类型对应不同的`SlotLevel`，决定通知的提醒行为。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**父类型：**

- Equatable\<[SlotType](#enum-slottype)>
- ToString

### ContentInformation

```cangjie
ContentInformation
```

**功能：** 内容信息类型。对应通知级别`LEVEL_MIN`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### CustomerService

```cangjie
CustomerService
```

**功能：** 客服消息类型，用于用户与客服提供方之间的消息，消息必须由用户发起。对应通知级别`LEVEL_DEFAULT`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### EmergencyInformation

```cangjie
EmergencyInformation
```

**功能：** 紧急事件类型。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### LiveView

```cangjie
LiveView
```

**功能：** 实况窗类型。三方应用不能直接创建该类型通知，需由系统代理创建通知后，三方应用通过相同ID发布通知更新指定内容。对应通知级别`LEVEL_DEFAULT`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### OtherTypes

```cangjie
OtherTypes
```

**功能：** 其他类型。对应通知级别`LEVEL_MIN`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### ServiceInformation

```cangjie
ServiceInformation
```

**功能：** 服务信息类型。对应通知级别`LEVEL_HIGH`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### SocialCommunication

```cangjie
SocialCommunication
```

**功能：** 社交通信类型。对应通知级别`LEVEL_HIGH`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### UnknownType

```cangjie
UnknownType
```

**功能：** 未知类型。对应通知级别`LEVEL_MIN`。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将通知槽类型转换为字符串表示。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**返回值：**

|类型|说明|
|:----|:----|
|String|通知槽类型的字符串表示。|

### func ==(SlotType)

```cangjie
public operator func ==(other: SlotType): Bool
```

**功能：** 判断两个通知槽类型是否相等。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SlotType](#enum-slottype)|是|-|待比较的通知槽类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示相等，false表示不相等。|

### func !=(SlotType)

```cangjie
public operator func !=(other: SlotType): Bool
```

**功能：** 判断两个通知槽类型是否不相等。

**系统能力：** SystemCapability.Notification.Notification

**起始版本：** 26.1.0

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[SlotType](#enum-slottype)|是|-|待比较的通知槽类型。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true表示不相等，false表示相等。|
