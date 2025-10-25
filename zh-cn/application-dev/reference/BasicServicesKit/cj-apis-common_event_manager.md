# ohos.common_event_manager

本模块提供了公共事件相关的能力，包括发布公共事件、订阅公共事件、以及退订公共事件。

## 导入模块

```cangjie
import kit.BasicServicesKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## class CommonEventManager

```cangjie
public class CommonEventManager {}
```

**功能：** 本结构体提供了公共事件的管理能力。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static func createSubscriber(CommonEventSubscribeInfo)

```cangjie
public static func createSubscriber(subscribeInfo: CommonEventSubscribeInfo): CommonEventSubscriber
```

**功能：** 创建订阅者。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|subscribeInfo|[CommonEventSubscribeInfo](./cj-apis-common_event_subscribe_info.md#class-commoneventsubscribeinfo)|是|-|表示订阅信息。|

**返回值：**

|类型|说明|
|:----|:----|
|[CommonEventSubscriber](./cj-apis-common_event_subscriber.md#class-commoneventsubscriber)|订阅者对象。|

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.base.*
import ohos.business_exception.*

let subscriber: CommonEventSubscriber //用于保存创建成功的订阅者对象，后续使用其完成订阅及退订的动作
let support = Support.COMMON_EVENT_ABILITY_ADDED
//订阅者信息
let subscribeInfo: CommonEventSubscribeInfo = CommonEventSubscribeInfo([support])
//创建订阅者
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

**功能：** 发布公共事件。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|event|String|是|-|表示要发送的公共事件。|
|options|[CommonEventPublishData](./cj-apis-common_event_publish_data.md#class-commoneventpublishdata)|否|CommonEventPublishData()|**命名参数。**表示发布公共事件的属性。|

**异常：**

- BusinessException：对应错误码如下表，详见[事件错误码](./cj-errorcode-common_event_service.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 1500003 | The common event sending frequency too high. |
  | 1500007 | If error sending message to Common Event Service. |
  | 1500008 | If Common Event Service does not complete initialization. |
  | 1500009 | If error obtaining system parameters. |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.base.*
import ohos.business_exception.*

try {
    // 公共事件属性
    let pData = CommonEventPublishData(bundleName: "com.example.myapplication", data: "123321", code: 123321)
    //发布公共事件
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

**功能：** 以回调形式订阅公共事件。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|subscriber|[CommonEventSubscriber](cj-apis-common_event_subscriber.md#class-commoneventsubscriber)|是|-|表示订阅者对象。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[CommonEventData](cj-apis-common_event_data.md#class-commoneventdata)>|是|-|表示接收公共事件数据的回调函数。|

**异常：**

- BusinessException：对应错误码如下表，详见[事件错误码](./cj-errorcode-common_event_service.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | capability not supported |
  | 1500007 | If error sending message to Common Event Service. |
  | 1500008 | If Common Event Service does not complete initialization. |
  | 1500010 | The count of subscriber exceed system specification. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.base.*
import ohos.business_exception.*
import kit.PerformanceAnalysisKit.Hilog

// 订阅事件：亮屏
let events = [Support.COMMON_EVENT_SCREEN_ON]
// 订阅者信息
let info = CommonEventSubscribeInfo(events)
// 订阅者
let sub = CommonEventManager.createSubscriber(info)
// 取消订阅
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

**功能：** 取消订阅公共事件。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|subscriber|[CommonEventSubscriber](cj-apis-common_event_subscriber.md#class-commoneventsubscriber)|是|-|表示订阅者对象。|

**异常：**

- BusinessException：对应错误码如下表，详见[事件错误码](./cj-errorcode-common_event_service.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 801 | capability not supported |
  | 1500007 | If error sending message to Common Event Service. |
  | 1500008 | If Common Event Service does not complete initialization. |

**示例：**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.base.*
import ohos.business_exception.*
import kit.PerformanceAnalysisKit.Hilog

// 订阅事件：亮屏
let events = [Support.COMMON_EVENT_SCREEN_ON]
// 订阅者信息
let info = CommonEventSubscribeInfo(events)
// 订阅者
let sub = CommonEventManager.createSubscriber(info)
// 取消订阅
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
    public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE: String = "usual.event.bluetooth.host.REQ_DISCOVERABLE"
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
    public static const COMMON_EVENT_DISK_BAD_REMOVAL: String = "usual.event.data.DISK_BAD_REMOVAL"
    public static const COMMON_EVENT_DISK_MOUNTED: String = "usual.event.data.DISK_MOUNTED"
    public static const COMMON_EVENT_DISK_UNMOUNTED: String = "usual.event.data.DISK_UNMOUNTED"
    public static const COMMON_EVENT_DISK_REMOVED: String = "usual.event.data.DISK_REMOVED"
    public static const COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED: String = "usual.event.DEVICE_IDLE_MODE_CHANGED"
    public static const COMMON_EVENT_DISCHARGING: String = "usual.event.DISCHARGING"
    public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOFF"
    public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID: String = "common.event.DISTRIBUTED_ACCOUNT_TOKEN_INVALID"
    public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOUT"
    public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN: String = "common.event.DISTRIBUTED_ACCOUNT_LOGIN"
    public static const COMMON_EVENT_DRIVE_MODE: String = "common.event.DRIVE_MODE"
    public static const COMMON_EVENT_DATE_CHANGED: String = "usual.event.DATE_CHANGED"
    public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_UNAVAILABLE"
    public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_AVAILABLE"
    public static const COMMON_EVENT_FOUNDATION_READY: String = "common.event.FOUNDATION_READY"
    public static const COMMON_EVENT_HOME_MODE: String = "common.event.HOME_MODE"
    public static const COMMON_EVENT_HTTP_PROXY_CHANGE: String = "usual.event.HTTP_PROXY_CHANGE"
    public static const COMMON_EVENT_IVI_SLEEP: String = "common.event.IVI_SLEEP"
    public static const COMMON_EVENT_IVI_PAUSE: String = "common.event.IVI_PAUSE"
    public static const COMMON_EVENT_IVI_STANDBY: String = "common.event.IVI_STANDBY"
    public static const COMMON_EVENT_IVI_LASTMODE_SAVE: String = "common.event.IVI_LASTMODE_SAVE"
    public static const COMMON_EVENT_IVI_VOLTAGE_ABNORMAL: String = "common.event.IVI_VOLTAGE_ABNORMAL"
    public static const COMMON_EVENT_IVI_HIGH_TEMPERATURE: String = "common.event.IVI_HIGH_TEMPERATURE"
    public static const COMMON_EVENT_IVI_EXTREME_TEMPERATURE: String = "common.event.IVI_EXTREME_TEMPERATURE"
    public static const COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL: String = "common.event.IVI_TEMPERATURE_ABNORMAL"
    public static const COMMON_EVENT_IVI_VOLTAGE_RECOVERY: String = "common.event.IVI_VOLTAGE_RECOVERY"
    public static const COMMON_EVENT_IVI_TEMPERATURE_RECOVERY: String = "common.event.IVI_TEMPERATURE_RECOVERY"
    public static const COMMON_EVENT_IVI_ACTIVE: String = "common.event.IVI_ACTIVE"
    public static const COMMON_EVENT_LOCKED_BOOT_COMPLETED: String = "usual.event.LOCKED_BOOT_COMPLETED"
    public static const COMMON_EVENT_LOCALE_CHANGED: String = "usual.event.LOCALE_CHANGED"
    public static const COMMON_EVENT_LOCATION_MODE_STATE_CHANGED: String = "usual.event.location.MODE_STATE_CHANGED"
    public static const COMMON_EVENT_MY_PACKAGE_REPLACED: String = "usual.event.MY_PACKAGE_REPLACED"
    public static const COMMON_EVENT_MY_PACKAGE_SUSPENDED: String = "usual.event.MY_PACKAGE_SUSPENDED"
    public static const COMMON_EVENT_MY_PACKAGE_UNSUSPENDED: String = "usual.event.MY_PACKAGE_UNSUSPENDED"
    public static const COMMON_EVENT_MANAGE_PACKAGE_STORAGE: String = "usual.event.MANAGE_PACKAGE_STORAGE"
    public static const COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED: String = "usual.event.nfc.action.ADAPTER_STATE_CHANGED"
    public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED: String = "usual.event.nfc.action.RF_FIELD_ON_DETECTED"
    public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED: String = "usual.event.nfc.action.RF_FIELD_OFF_DETECTED"
    public static const COMMON_EVENT_NETWORK_STATE_CHANGED: String = "usual.event.NETWORK_STATE_CHANGED"
    public static const COMMON_EVENT_OFFICE_MODE: String = "common.event.OFFICE_MODE"
    public static const COMMON_EVENT_POWER_CONNECTED: String = "usual.event.POWER_CONNECTED"
    public static const COMMON_EVENT_POWER_DISCONNECTED: String = "usual.event.POWER_DISCONNECTED"
    public static const COMMON_EVENT_PACKAGE_ADDED: String = "usual.event.PACKAGE_ADDED"
    public static const COMMON_EVENT_PACKAGE_REPLACED: String = "usual.event.PACKAGE_REPLACED"
    public static const COMMON_EVENT_PACKAGE_REMOVED: String = "usual.event.PACKAGE_REMOVED"
    public static const COMMON_EVENT_PACKAGE_FULLY_REMOVED: String = "usual.event.PACKAGE_FULLY_REMOVED"
    public static const COMMON_EVENT_PACKAGE_CHANGED: String = "usual.event.PACKAGE_CHANGED"
    public static const COMMON_EVENT_PACKAGE_RESTARTED: String = "usual.event.PACKAGE_RESTARTED"
    public static const COMMON_EVENT_PACKAGE_DATA_CLEARED: String = "usual.event.PACKAGE_DATA_CLEARED"
    public static const COMMON_EVENT_PACKAGE_CACHE_CLEARED: String = "usual.event.PACKAGE_CACHE_CLEARED"
    public static const COMMON_EVENT_PACKAGES_SUSPENDED: String = "usual.event.PACKAGES_SUSPENDED"
    public static const COMMON_EVENT_PACKAGES_UNSUSPENDED: String = "usual.event.PACKAGES_UNSUSPENDED"
    public static const COMMON_EVENT_PACKAGE_FIRST_LAUNCH: String = "usual.event.PACKAGE_FIRST_LAUNCH"
    public static const COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION: String = "usual.event.PACKAGE_NEEDS_VERIFICATION"
    public static const COMMON_EVENT_PACKAGE_VERIFIED: String = "usual.event.PACKAGE_VERIFIED"
    public static const COMMON_EVENT_POWER_SAVE_MODE_CHANGED: String = "usual.event.POWER_SAVE_MODE_CHANGED"
    public static const COMMON_EVENT_QUICK_FIX_APPLY_RESULT: String = "usual.event.QUICK_FIX_APPLY_RESULT"
    public static const COMMON_EVENT_QUICK_FIX_REVOKE_RESULT: String = "usual.event.QUICK_FIX_REVOKE_RESULT"
    public static const COMMON_EVENT_SHUTDOWN: String = "usual.event.SHUTDOWN"
    public static const COMMON_EVENT_SCREEN_OFF: String = "usual.event.SCREEN_OFF"
    public static const COMMON_EVENT_SCREEN_ON: String = "usual.event.SCREEN_ON"
    public static const COMMON_EVENT_SPLIT_SCREEN: String = "common.event.SPLIT_SCREEN"
    public static const COMMON_EVENT_SLOT_CHANGE: String = "usual.event.SLOT_CHANGE"
    public static const COMMON_EVENT_SPN_INFO_CHANGED: String = "usual.event.SPN_INFO_CHANGED"
    public static const COMMON_EVENT_SIGNAL_INFO_CHANGED: String = "usual.event.SIGNAL_INFO_CHANGED"
    public static const COMMON_EVENT_SIM_STATE_CHANGED: String = "usual.event.SIM_STATE_CHANGED"
    public static const COMMON_EVENT_SCREEN_LOCKED: String = "usual.event.SCREEN_LOCKED"
    public static const COMMON_EVENT_SCREEN_UNLOCKED: String = "usual.event.SCREEN_UNLOCKED"
    public static const COMMON_EVENT_THERMAL_LEVEL_CHANGED: String = "usual.event.THERMAL_LEVEL_CHANGED"
    public static const COMMON_EVENT_TIME_TICK: String = "usual.event.TIME_TICK"
    public static const COMMON_EVENT_TIME_CHANGED: String = "usual.event.TIME_CHANGED"
    public static const COMMON_EVENT_TIMEZONE_CHANGED: String = "usual.event.TIMEZONE_CHANGED"
    public static const COMMON_EVENT_UID_REMOVED: String = "usual.event.UID_REMOVED"
    public static const COMMON_EVENT_USER_STARTED: String = "usual.event.USER_STARTED"
    public static const COMMON_EVENT_USER_BACKGROUND: String = "usual.event.USER_BACKGROUND"
    public static const COMMON_EVENT_USER_FOREGROUND: String = "usual.event.USER_FOREGROUND"
    public static const COMMON_EVENT_USER_SWITCHED: String = "usual.event.USER_SWITCHED"
    public static const COMMON_EVENT_USER_STARTING: String = "usual.event.USER_STARTING"
    public static const COMMON_EVENT_USER_UNLOCKED: String = "usual.event.USER_UNLOCKED"
    public static const COMMON_EVENT_USER_STOPPING: String = "usual.event.USER_STOPPING"
    public static const COMMON_EVENT_USER_STOPPED: String = "usual.event.USER_STOPPED"
    public static const COMMON_EVENT_USER_ADDED: String = "usual.event.USER_ADDED"
    public static const COMMON_EVENT_USER_REMOVED: String = "usual.event.USER_REMOVED"
    public static const COMMON_EVENT_USB_STATE: String = "usual.event.hardware.usb.action.USB_STATE"
    public static const COMMON_EVENT_USB_PORT_CHANGED: String = "usual.event.hardware.usb.action.USB_PORT_CHANGED"
    public static const COMMON_EVENT_USB_DEVICE_ATTACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_ATTACHED"
    public static const COMMON_EVENT_USB_DEVICE_DETACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_DETACHED"
    public static const COMMON_EVENT_USB_ACCESSORY_ATTACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_ATTACHED"
    public static const COMMON_EVENT_USB_ACCESSORY_DETACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_DETACHED"
    public static const COMMON_EVENT_USER_INFO_UPDATED: String = "usual.event.USER_INFO_UPDATED"
    public static const COMMON_EVENT_VOLUME_REMOVED: String = "usual.event.data.VOLUME_REMOVED"
    public static const COMMON_EVENT_VOLUME_UNMOUNTED: String = "usual.event.data.VOLUME_UNMOUNTED"
    public static const COMMON_EVENT_VOLUME_MOUNTED: String = "usual.event.data.VOLUME_MOUNTED"
    public static const COMMON_EVENT_VOLUME_BAD_REMOVAL: String = "usual.event.data.VOLUME_BAD_REMOVAL"
    public static const COMMON_EVENT_VOLUME_EJECT: String = "usual.event.data.VOLUME_EJECT"
    public static const COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED: String = "usual.event.data.VISIBLE_ACCOUNTS_UPDATED"
    public static const COMMON_EVENT_WIFI_POWER_STATE: String = "usual.event.wifi.POWER_STATE"
    public static const COMMON_EVENT_WIFI_SCAN_FINISHED: String = "usual.event.wifi.SCAN_FINISHED"
    public static const COMMON_EVENT_WIFI_RSSI_VALUE: String = "usual.event.wifi.RSSI_VALUE"
    public static const COMMON_EVENT_WIFI_CONN_STATE: String = "usual.event.wifi.CONN_STATE"
    public static const COMMON_EVENT_WIFI_HOTSPOT_STATE: String = "usual.event.wifi.HOTSPOT_STATE"
    public static const COMMON_EVENT_WIFI_AP_STA_JOIN: String = "usual.event.wifi.WIFI_HS_STA_JOIN"
    public static const COMMON_EVENT_WIFI_AP_STA_LEAVE: String = "usual.event.wifi.WIFI_HS_STA_LEAVE"
    public static const COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE: String = "usual.event.wifi.mplink.STATE_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_CONN_STATE: String = "usual.event.wifi.p2p.CONN_STATE_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_STATE_CHANGED: String = "usual.event.wifi.p2p.STATE_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED: String = "usual.event.wifi.p2p.DEVICES_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED: String = "usual.event.wifi.p2p.PEER_DISCOVERY_STATE_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED: String = "usual.event.wifi.p2p.CURRENT_DEVICE_CHANGE"
    public static const COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED: String = "usual.event.wifi.p2p.GROUP_STATE_CHANGED"
}
```

**功能：** 本结构体提供了系统公共事件的管理能力。系统公共事件是指由系统服务或系统应用发布的事件，订阅这些公共事件需要特定的权限、使用相应的值。

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_ABILITY_ADDED

```cangjie
public static const COMMON_EVENT_ABILITY_ADDED: String = "common.event.ABILITY_ADDED"
```

**功能：** 预留事件，暂未支持）表示已添加能力的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_ABILITY_REMOVED

```cangjie
public static const COMMON_EVENT_ABILITY_REMOVED: String = "common.event.ABILITY_REMOVED"
```

**功能：** （预留事件，暂未支持）表示已删除能力的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_ABILITY_UPDATED

```cangjie
public static const COMMON_EVENT_ABILITY_UPDATED: String = "common.event.ABILITY_UPDATED"
```

**功能：** （预留事件，暂未支持）表示能力已更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_ACCOUNT_DELETED

```cangjie
public static const COMMON_EVENT_ACCOUNT_DELETED: String = "usual.event.data.ACCOUNT_DELETED"
```

**功能：** （预留事件，暂未支持）表示删除账户的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_AIRPLANE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_AIRPLANE_MODE_CHANGED: String = "usual.event.AIRPLANE_MODE"
```

**功能：** 表示设备飞行模式已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BATTERY_CHANGED

```cangjie
public static const COMMON_EVENT_BATTERY_CHANGED: String = "usual.event.BATTERY_CHANGED"
```

**功能：** 表示电池充电状态、电平和其他信息发生变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BATTERY_LOW

```cangjie
public static const COMMON_EVENT_BATTERY_LOW: String = "usual.event.BATTERY_LOW"
```

**功能：** 表示电池电量低的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BATTERY_OKAY

```cangjie
public static const COMMON_EVENT_BATTERY_OKAY: String = "usual.event.BATTERY_OKAY"
```

**功能：** 表示电池退出低电平状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.AUDIO_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP宿的音频状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.CONNECT_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP宿连接状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSINK_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsink.PLAYING_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP宿播放状态改变的普通事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_AVRCP_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.AVRCP_CONNECT_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP的AVRCP连接状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CODEC_VALUE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CODEC_VALUE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP音频编解码状态更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CONNECT_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP连接状态公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.a2dpsource.CURRENT_DEVICE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示使用蓝牙A2DP连接的设备处于活动状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_A2DPSOURCE_PLAYING_STATE_UPDATE: String = "usual.event.bluetooth.a2dpsource.PLAYING_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP播放状态改变的普通事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_CALL_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AG_CALL_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙免提呼叫状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AG_COMMON_EVENT: String = "usual.event.bluetooth.handsfreeunit.AG_COMMON_EVENT"
```

**功能：** （预留事件，暂未支持）表示蓝牙免提音频网关状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.AUDIO_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙免提音频状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREEUNIT_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfreeunit.CONNECT_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙免提连接状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_AUDIO_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.AUDIO_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙A2DP连接状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CONNECT_STATE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CONNECT_STATE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示蓝牙免提通信连接状态公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HANDSFREE_AG_CURRENT_DEVICE_UPDATE: String = "usual.event.bluetooth.handsfree.ag.CURRENT_DEVICE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示连接到蓝牙免提的设备处于活动状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_FINISHED: String = "usual.event.bluetooth.host.DISCOVERY_FINISHED"
```

**功能：** 表示设备上蓝牙扫描完成的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_DISCOVERY_STARTED: String = "usual.event.bluetooth.host.DISCOVERY_STARTED"
```

**功能：** 表示设备上已启动蓝牙扫描的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_NAME_UPDATE: String = "usual.event.bluetooth.host.NAME_UPDATE"
```

**功能：** 表示设备蓝牙适配器名称已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISABLE: String = "usual.event.bluetooth.host.REQ_DISABLE"
```

**功能：** （预留事件，暂未支持）表示用户关闭蓝牙请求的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_DISCOVERABLE: String = "usual.event.bluetooth.host.REQ_DISCOVERABLE"
```

**功能：** 表示用户允许扫描蓝牙请求的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_REQ_ENABLE: String = "usual.event.bluetooth.host.REQ_ENABLE"
```

**功能：** 预留事件，暂未支持）表示用户打开蓝牙请求的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_SCAN_MODE_UPDATE: String = "usual.event.bluetooth.host.SCAN_MODE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示设备蓝牙扫描模式更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_HOST_STATE_UPDATE: String = "usual.event.bluetooth.host.STATE_UPDATE"
```

**功能：** 表示蓝牙适配器状态已更改的公共事件，例如蓝牙已打开或关闭。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_CONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_CONNECTED"
```

**功能：** （预留事件，暂未支持）表示已与远程蓝牙设备建立低级别（ACL）连接的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_ACL_DISCONNECTED: String = "usual.event.bluetooth.remotedevice.ACL_DISCONNECTED"
```

**功能：** （预留事件，暂未支持）表示低电平（ACL）连接已从远程蓝牙设备断开的普通事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_BATTERY_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.BATTERY_VALUE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备的电池电量首次被检索或自上次检索以来被更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CLASS_VALUE_UPDATE: String = "usual.event.bluetooth.remotedevice.CLASS_VALUE_UPDATE"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备的电池电量首次被检索或自上次检索以来被更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_CANCEL: String = "usual.event.bluetooth.remotedevice.CONNECT_CANCEL"
```

**功能：** （预留事件，暂未支持）表示取消与远程蓝牙设备的连接的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REPLY: String = "usual.event.bluetooth.remotedevice.CONNECT_REPLY"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备连接请求响应的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_CONNECT_REQ: String = "usual.event.bluetooth.remotedevice.CONNECT_REQ"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备连接请求的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_DISCOVERED: String = "usual.event.bluetooth.remotedevice.DISCOVERED"
```

**功能：** （预留事件，暂未支持）表示发现远程蓝牙设备的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_NAME_UPDATE: String = "usual.event.bluetooth.remotedevice.NAME_UPDATE"
```

**功能：** 表示远程蓝牙设备的友好名称首次被检索或自上次检索以来被更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_CANCEL: String = "usual.event.bluetooth.remotedevice.PAIRING_CANCEL"
```

**功能：** （预留事件，暂未支持）表示取消蓝牙配对的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIRING_REQ: String = "usual.event.bluetooth.remotedevice.PAIRING_REQ"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备配对请求的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_PAIR_STATE: String = "usual.event.bluetooth.remotedevice.PAIR_STATE"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备连接状态更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_SDP_RESULT: String = "usual.event.bluetooth.remotedevice.SDP_RESULT"
```

**功能：** （预留事件，暂未支持）表示远程蓝牙设备SDP状态公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE

```cangjie
public static const COMMON_EVENT_BLUETOOTH_REMOTEDEVICE_UUID_VALUE: String = "usual.event.bluetooth.remotedevice.UUID_VALUE"
```

**功能：** 表示远程蓝牙设备UUID连接状态公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BOOT_COMPLETED

```cangjie
public static const COMMON_EVENT_BOOT_COMPLETED: String = "usual.event.BOOT_COMPLETED"
```

**功能：** 表示用户已完成引导并加载系统的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_BUNDLE_REMOVED

```cangjie
public static const COMMON_EVENT_BUNDLE_REMOVED: String = "usual.event.BUNDLE_REMOVED"
```

**功能：** （预留事件，暂未支持）表示已从设备中卸载已安装的捆绑包，但应用程序数据仍保留的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CALL_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_CALL_STATE_CHANGED: String = "usual.event.CALL_STATE_CHANGED"
```

**功能：** 表示呼叫状态更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CHARGE_IDLE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_CHARGE_IDLE_MODE_CHANGED: String = "usual.event.CHARGE_IDLE_MODE_CHANGED"
```

**功能：** 表示设备进入充电空闲模式的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CHARGING

```cangjie
public static const COMMON_EVENT_CHARGING: String = "usual.event.CHARGING"
```

**功能：** 表示系统开始为电池充电的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CLOSE_SYSTEM_DIALOGS

```cangjie
public static const COMMON_EVENT_CLOSE_SYSTEM_DIALOGS: String = "usual.event.CLOSE_SYSTEM_DIALOGS"
```

**功能：** （预留事件，暂未支持）表示用户关闭临时系统对话框的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CONFIGURATION_CHANGED

```cangjie
public static const COMMON_EVENT_CONFIGURATION_CHANGED: String = "usual.event.CONFIGURATION_CHANGED"
```

**功能：** （预留事件，暂未支持）表示设备状态（例如，方向和区域设置）已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_CONNECTIVITY_CHANGE

```cangjie
public static const COMMON_EVENT_CONNECTIVITY_CHANGE: String = "usual.event.CONNECTIVITY_CHANGE"
```

**功能：** 表示网络连接状态变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DATE_CHANGED

```cangjie
public static const COMMON_EVENT_DATE_CHANGED: String = "usual.event.DATE_CHANGED"
```

**功能：** （预留事件，暂未支持）表示系统日期已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_DEVICE_IDLE_MODE_CHANGED: String = "usual.event.DEVICE_IDLE_MODE_CHANGED"
```

**功能：** 表示系统待机空闲模式已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISCHARGING

```cangjie
public static const COMMON_EVENT_DISCHARGING: String = "usual.event.DISCHARGING"
```

**功能：** 表示系统停止为电池充电的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_BAD_REMOVAL

```cangjie
public static const COMMON_EVENT_DISK_BAD_REMOVAL: String = "usual.event.data.DISK_BAD_REMOVAL"
```

**功能：** （预留事件，暂未支持）表示外部存储设备状态变更为挂载状态下移除的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_EJECT

```cangjie
public static const COMMON_EVENT_DISK_EJECT: String = "usual.event.data.DISK_EJECT"
```

**功能：** （预留事件，暂未支持）表示用户已表示希望删除外部存储介质的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_MOUNTED

```cangjie
public static const COMMON_EVENT_DISK_MOUNTED: String = "usual.event.data.DISK_MOUNTED"
```

**功能：** （预留事件，暂未支持）表示外部存储设备状态变更为挂载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_REMOVED

```cangjie
public static const COMMON_EVENT_DISK_REMOVED: String = "usual.event.data.DISK_REMOVED"
```

**功能：** （预留事件，暂未支持）表示外部存储设备状态变更为移除的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_UNMOUNTABLE

```cangjie
public static const COMMON_EVENT_DISK_UNMOUNTABLE: String = "usual.event.data.DISK_UNMOUNTABLE"
```

**功能：** （预留事件，暂未支持）外部存储设备状态变更为插卡情况下无法挂载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISK_UNMOUNTED

```cangjie
public static const COMMON_EVENT_DISK_UNMOUNTED: String = "usual.event.data.DISK_UNMOUNTED"
```

**功能：** （预留事件，暂未支持）表示部存储设备状态变更为卸载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN: String = "common.event.DISTRIBUTED_ACCOUNT_LOGIN"
```

**功能：** （预留事件，暂未支持）表示分布式账号登录成功的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOFF"
```

**功能：** （预留事件，暂未支持）表示分布式账号注销的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT: String = "common.event.DISTRIBUTED_ACCOUNT_LOGOUT"
```

**功能：** （预留事件，暂未支持）表示分布式账号登出成功的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID

```cangjie
public static const COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID: String = "common.event.DISTRIBUTED_ACCOUNT_TOKEN_INVALID"
```

**功能：** （预留事件，暂未支持）表示分布式账号token令牌无效的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_DRIVE_MODE

```cangjie
public static const COMMON_EVENT_DRIVE_MODE: String = "common.event.DRIVE_MODE"
```

**功能：** （预留事件，暂未支持）表示系统处于驾驶模式的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE

```cangjie
public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_AVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_AVAILABLE"
```

**功能：** （预留事件，暂未支持）表示安装在外部存储上的应用程序对系统可用的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE

```cangjie
public static const COMMON_EVENT_EXTERNAL_APPLICATIONS_UNAVAILABLE: String = "usual.event.EXTERNAL_APPLICATIONS_UNAVAILABLE"
```

**功能：** （预留事件，暂未支持）表示安装在外部存储上的应用程序对系统不可用的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_FOUNDATION_READY

```cangjie
public static const COMMON_EVENT_FOUNDATION_READY: String = "common.event.FOUNDATION_READY"
```

**功能：** （预留事件，暂未支持）表示foundation已准备好的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_HOME_MODE

```cangjie
public static const COMMON_EVENT_HOME_MODE: String = "common.event.HOME_MODE"
```

**功能：** （预留事件，暂未支持）表示系统处于HOME模式的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_HTTP_PROXY_CHANGE

```cangjie
public static const COMMON_EVENT_HTTP_PROXY_CHANGE: String = "usual.event.HTTP_PROXY_CHANGE"
```

**功能：** 表示HTTP代理的配置信息发生变化。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_ACTIVE

```cangjie
public static const COMMON_EVENT_IVI_ACTIVE: String = "common.event.IVI_ACTIVE"
```

**功能：** （预留事件，暂未支持）表示电池服务处于活动状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_EXTREME_TEMPERATURE

```cangjie
public static const COMMON_EVENT_IVI_EXTREME_TEMPERATURE: String = "common.event.IVI_EXTREME_TEMPERATURE"
```

**功能：** （预留事件，暂未支持）表示IVI温度极高的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_HIGH_TEMPERATURE

```cangjie
public static const COMMON_EVENT_IVI_HIGH_TEMPERATURE: String = "common.event.IVI_HIGH_TEMPERATURE"
```

**功能：** （预留事件，暂未支持）表示IVI温度过高的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_LASTMODE_SAVE

```cangjie
public static const COMMON_EVENT_IVI_LASTMODE_SAVE: String = "common.event.IVI_LASTMODE_SAVE"
```

**功能：** （预留事件，暂未支持）表示第三方应用保存其最后一个模式的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_PAUSE

```cangjie
public static const COMMON_EVENT_IVI_PAUSE: String = "common.event.IVI_PAUSE"
```

**功能：** （预留事件，暂未支持）表示IVI已休眠，并通知应用程序停止播放的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_SLEEP

```cangjie
public static const COMMON_EVENT_IVI_SLEEP: String = "common.event.IVI_SLEEP"
```

**功能：** （预留事件，暂未支持）表示表示车辆的车载信息娱乐（IVI）系统正在休眠的常见事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_STANDBY

```cangjie
public static const COMMON_EVENT_IVI_STANDBY: String = "common.event.IVI_STANDBY"
```

**功能：** （预留事件，暂未支持）表示第三方应用暂停当前工作的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL

```cangjie
public static const COMMON_EVENT_IVI_TEMPERATURE_ABNORMAL: String = "common.event.IVI_TEMPERATURE_ABNORMAL"
```

**功能：** （预留事件，暂未支持）表示车载系统具有极端温度的常见事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_TEMPERATURE_RECOVERY

```cangjie
public static const COMMON_EVENT_IVI_TEMPERATURE_RECOVERY: String = "common.event.IVI_TEMPERATURE_RECOVERY"
```

**功能：** （预留事件，暂未支持）表示车载系统温度恢复正常的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_VOLTAGE_ABNORMAL

```cangjie
public static const COMMON_EVENT_IVI_VOLTAGE_ABNORMAL: String = "common.event.IVI_VOLTAGE_ABNORMAL"
```

**功能：** （预留事件，暂未支持）表示车辆电源系统电压异常的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_IVI_VOLTAGE_RECOVERY

```cangjie
public static const COMMON_EVENT_IVI_VOLTAGE_RECOVERY: String = "common.event.IVI_VOLTAGE_RECOVERY"
```

**功能：** （预留事件，暂未支持）表示车辆电源系统电压恢复正常的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_LOCALE_CHANGED

```cangjie
public static const COMMON_EVENT_LOCALE_CHANGED: String = "usual.event.LOCALE_CHANGED"
```

**功能：** 表示设备区域设置已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_LOCATION_MODE_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_LOCATION_MODE_STATE_CHANGED: String = "usual.event.location.MODE_STATE_CHANGED"
```

**功能：** （预留事件，暂未支持）表示系统定位模式已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_LOCKED_BOOT_COMPLETED

```cangjie
public static const COMMON_EVENT_LOCKED_BOOT_COMPLETED: String = "usual.event.LOCKED_BOOT_COMPLETED"
```

**功能：** （预留事件，暂未支持）表示用户已完成引导，系统已加载，但屏幕仍锁定的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_MANAGE_PACKAGE_STORAGE

```cangjie
public static const COMMON_EVENT_MANAGE_PACKAGE_STORAGE: String = "usual.event.MANAGE_PACKAGE_STORAGE"
```

**功能：** （预留事件，暂未支持）表示设备存储空间不足的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_MY_PACKAGE_REPLACED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_REPLACED: String = "usual.event.MY_PACKAGE_REPLACED"
```

**功能：** （预留事件，暂未支持）表示应用程序包的新版本已取代前一个版本的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_MY_PACKAGE_SUSPENDED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_SUSPENDED: String = "usual.event.MY_PACKAGE_SUSPENDED"
```

**功能：** 表示应用包被挂起的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_MY_PACKAGE_UNSUSPENDED

```cangjie
public static const COMMON_EVENT_MY_PACKAGE_UNSUSPENDED: String = "usual.event.MY_PACKAGE_UNSUSPENDED"
```

**功能：** 表示应用包未挂起的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_NETWORK_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_NETWORK_STATE_CHANGED: String = "usual.event.NETWORK_STATE_CHANGED"
```

**功能：** 表示网络状态更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_ADAPTER_STATE_CHANGED: String = "usual.event.nfc.action.ADAPTER_STATE_CHANGED"
```

**功能：** 表示设备NFC状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_OFF_DETECTED: String = "usual.event.nfc.action.RF_FIELD_OFF_DETECTED"
```

**功能：** 表示检测到NFC场强离开的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED

```cangjie
public static const COMMON_EVENT_NFC_ACTION_RF_FIELD_ON_DETECTED: String = "usual.event.nfc.action.RF_FIELD_ON_DETECTED"
```

**功能：** 表示检测到NFC场强进入的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_OFFICE_MODE

```cangjie
public static const COMMON_EVENT_OFFICE_MODE: String = "common.event.OFFICE_MODE"
```

**功能：** （预留事件，暂未支持）表示系统处于办公模式的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGES_SUSPENDED

```cangjie
public static const COMMON_EVENT_PACKAGES_SUSPENDED: String = "usual.event.PACKAGES_SUSPENDED"
```

**功能：** （预留事件，暂未支持）表示应用包已挂起的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGES_UNSUSPENDED

```cangjie
public static const COMMON_EVENT_PACKAGES_UNSUSPENDED: String = "usual.event.PACKAGES_UNSUSPENDED"
```

**功能：** （预留事件，暂未支持）表示应用包未挂起的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_ADDED

```cangjie
public static const COMMON_EVENT_PACKAGE_ADDED: String = "usual.event.PACKAGE_ADDED"
```

**功能：** 表示设备上已安装新应用包的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_CACHE_CLEARED

```cangjie
public static const COMMON_EVENT_PACKAGE_CACHE_CLEARED: String = "usual.event.PACKAGE_CACHE_CLEARED"
```

**功能：** 表示用户清除应用包缓存数据的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_CHANGED

```cangjie
public static const COMMON_EVENT_PACKAGE_CHANGED: String = "usual.event.PACKAGE_CHANGED"
```

**功能：** 表示应用包已更改的公共事件（例如，包中的组件已启用或禁用）。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_DATA_CLEARED

```cangjie
public static const COMMON_EVENT_PACKAGE_DATA_CLEARED: String = "usual.event.PACKAGE_DATA_CLEARED"
```

**功能：** 表示用户清除应用包数据的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_FIRST_LAUNCH

```cangjie
public static const COMMON_EVENT_PACKAGE_FIRST_LAUNCH: String = "usual.event.PACKAGE_FIRST_LAUNCH"
```

**功能：** （预留事件，暂未支持）表示首次启动已安装应用程序的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_FULLY_REMOVED

```cangjie
public static const COMMON_EVENT_PACKAGE_FULLY_REMOVED: String = "usual.event.PACKAGE_FULLY_REMOVED"
```

**功能：** （预留事件，暂未支持）表示已从设备中完全卸载已安装的应用程序（包括应用程序数据和代码）的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION

```cangjie
public static const COMMON_EVENT_PACKAGE_NEEDS_VERIFICATION: String = "usual.event.PACKAGE_NEEDS_VERIFICATION"
```

**功能：** （预留事件，暂未支持）表示应用需要系统校验的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_REMOVED

```cangjie
public static const COMMON_EVENT_PACKAGE_REMOVED: String = "usual.event.PACKAGE_REMOVED"
```

**功能：** 表示已从设备卸载已安装的应用程序，但应用程序数据保留的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_REPLACED

```cangjie
public static const COMMON_EVENT_PACKAGE_REPLACED: String = "usual.event.PACKAGE_REPLACED"
```

**功能：** （预留事件，暂未支持）表示已安装的应用程序包的新版本已替换设备上的旧版本的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_RESTARTED

```cangjie
public static const COMMON_EVENT_PACKAGE_RESTARTED: String = "usual.event.PACKAGE_RESTARTED"
```

**功能：** 表示用户重启应用包并杀死其所有进程的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_PACKAGE_VERIFIED

```cangjie
public static const COMMON_EVENT_PACKAGE_VERIFIED: String = "usual.event.PACKAGE_VERIFIED"
```

**功能：** （预留事件，暂未支持）表示应用已被系统校验的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_POWER_CONNECTED

```cangjie
public static const COMMON_EVENT_POWER_CONNECTED: String = "usual.event.POWER_CONNECTED"
```

**功能：** 表示设备连接到外部电源的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_POWER_DISCONNECTED

```cangjie
public static const COMMON_EVENT_POWER_DISCONNECTED: String = "usual.event.POWER_DISCONNECTED"
```

**功能：** 表示设备与外部电源断开的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_POWER_SAVE_MODE_CHANGED

```cangjie
public static const COMMON_EVENT_POWER_SAVE_MODE_CHANGED: String = "usual.event.POWER_SAVE_MODE_CHANGED"
```

**功能：** 表示系统节能模式更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_QUICK_FIX_APPLY_RESULT

```cangjie
public static const COMMON_EVENT_QUICK_FIX_APPLY_RESULT: String = "usual.event.QUICK_FIX_APPLY_RESULT"
```

**功能：** 表示快速修复应用的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_QUICK_FIX_REVOKE_RESULT

```cangjie
public static const COMMON_EVENT_QUICK_FIX_REVOKE_RESULT: String = "usual.event.QUICK_FIX_REVOKE_RESULT"
```

**功能：** 表示撤销快速修复的公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SCREEN_LOCKED

```cangjie
public static const COMMON_EVENT_SCREEN_LOCKED: String = "usual.event.SCREEN_LOCKED"
```

**功能：** 表示屏幕锁定的公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SCREEN_OFF

```cangjie
public static const COMMON_EVENT_SCREEN_OFF: String = "usual.event.SCREEN_OFF"
```

**功能：** 表示设备屏幕关闭且设备处于睡眠状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SCREEN_ON

```cangjie
public static const COMMON_EVENT_SCREEN_ON: String = "usual.event.SCREEN_ON"
```

**功能：** 表示设备屏幕打开且设备处于交互状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SCREEN_UNLOCKED

```cangjie
public static const COMMON_EVENT_SCREEN_UNLOCKED: String = "usual.event.SCREEN_UNLOCKED"
```

**功能：** 表示屏幕解锁的公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SHUTDOWN

```cangjie
public static const COMMON_EVENT_SHUTDOWN: String = "usual.event.SHUTDOWN"
```

**功能：** 表示设备正在关闭的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SIGNAL_INFO_CHANGED

```cangjie
public static const COMMON_EVENT_SIGNAL_INFO_CHANGED: String = "usual.event.SIGNAL_INFO_CHANGED"
```

**功能：** 表示信号信息更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SIM_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_SIM_STATE_CHANGED: String = "usual.event.SIM_STATE_CHANGED"
```

**功能：** 表示SIM卡状态更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SLOT_CHANGE

```cangjie
public static const COMMON_EVENT_SLOT_CHANGE: String = "usual.event.SLOT_CHANGE"
```

**功能：** 表示通知通道更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SPLIT_SCREEN

```cangjie
public static const COMMON_EVENT_SPLIT_SCREEN: String = "common.event.SPLIT_SCREEN"
```

**功能：** 表示分屏的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_SPN_INFO_CHANGED

```cangjie
public static const COMMON_EVENT_SPN_INFO_CHANGED: String = "usual.event.SPN_INFO_CHANGED"
```

**功能：** 表示spn显示信息已更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_THERMAL_LEVEL_CHANGED

```cangjie
public static const COMMON_EVENT_THERMAL_LEVEL_CHANGED: String = "usual.event.THERMAL_LEVEL_CHANGED"
```

**功能：** 表示设备热状态的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_TIMEZONE_CHANGED

```cangjie
public static const COMMON_EVENT_TIMEZONE_CHANGED: String = "usual.event.TIMEZONE_CHANGED"
```

**功能：** 表示系统时区更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_TIME_CHANGED

```cangjie
public static const COMMON_EVENT_TIME_CHANGED: String = "usual.event.TIME_CHANGED"
```

**功能：** 表示设置系统时间的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_TIME_TICK

```cangjie
public static const COMMON_EVENT_TIME_TICK: String = "usual.event.TIME_TICK"
```

**功能：** 表示系统时间更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_UID_REMOVED

```cangjie
public static const COMMON_EVENT_UID_REMOVED: String = "usual.event.UID_REMOVED"
```

**功能：** （预留事件，暂未支持）表示用户ID已从系统中删除的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_ACCESSORY_ATTACHED

```cangjie
public static const COMMON_EVENT_USB_ACCESSORY_ATTACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_ATTACHED"
```

**功能：** （预留事件，暂未支持）表示已连接USB附件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_ACCESSORY_DETACHED

```cangjie
public static const COMMON_EVENT_USB_ACCESSORY_DETACHED: String = "usual.event.hardware.usb.action.USB_ACCESSORY_DETACHED"
```

**功能：** （预留事件，暂未支持）表示USB附件被卸载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_DEVICE_ATTACHED

```cangjie
public static const COMMON_EVENT_USB_DEVICE_ATTACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_ATTACHED"
```

**功能：** 表示用户设备作为USB主机时，USB设备已挂载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_DEVICE_DETACHED

```cangjie
public static const COMMON_EVENT_USB_DEVICE_DETACHED: String = "usual.event.hardware.usb.action.USB_DEVICE_DETACHED"
```

**功能：** 表示用户设备作为USB主机时，USB设备被卸载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_PORT_CHANGED

```cangjie
public static const COMMON_EVENT_USB_PORT_CHANGED: String = "usual.event.hardware.usb.action.USB_PORT_CHANGED"
```

**功能：** 表示用户设备的USB端口状态发生改变的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USB_STATE

```cangjie
public static const COMMON_EVENT_USB_STATE: String = "usual.event.hardware.usb.action.USB_STATE"
```

**功能：** 表示USB设备状态发生变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_ADDED

```cangjie
public static const COMMON_EVENT_USER_ADDED: String = "usual.event.USER_ADDED"
```

**功能：** 表示用户已添加到系统中的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_BACKGROUND

```cangjie
public static const COMMON_EVENT_USER_BACKGROUND: String = "usual.event.USER_BACKGROUND"
```

**功能：** （预留事件，暂未支持）表示用户已被带到后台的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_FOREGROUND

```cangjie
public static const COMMON_EVENT_USER_FOREGROUND: String = "usual.event.USER_FOREGROUND"
```

**功能：** （预留事件，暂未支持）表示用户已被带到前台的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_INFO_UPDATED

```cangjie
public static const COMMON_EVENT_USER_INFO_UPDATED: String = "usual.event.USER_INFO_UPDATED"
```

**功能：** 表示用户信息已更新的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_REMOVED

```cangjie
public static const COMMON_EVENT_USER_REMOVED: String = "usual.event.USER_REMOVED"
```

**功能：** 表示用户已从系统中删除的公共事件的动作。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_STARTED

```cangjie
public static const COMMON_EVENT_USER_STARTED: String = "usual.event.USER_STARTED"
```

**功能：** （预留事件，暂未支持）表示用户已启动的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_STARTING

```cangjie
public static const COMMON_EVENT_USER_STARTING: String = "usual.event.USER_STARTING"
```

**功能：** （预留事件，暂未支持）表示用户已启动的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_STOPPED

```cangjie
public static const COMMON_EVENT_USER_STOPPED: String = "usual.event.USER_STOPPED"
```

**功能：** （预留事件，暂未支持）表示用户已停止的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_STOPPING

```cangjie
public static const COMMON_EVENT_USER_STOPPING: String = "usual.event.USER_STOPPING"
```

**功能：** （预留事件，暂未支持）表示要停止用户的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_SWITCHED

```cangjie
public static const COMMON_EVENT_USER_SWITCHED: String = "usual.event.USER_SWITCHED"
```

**功能：** 表示用户切换正在发生的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_USER_UNLOCKED

```cangjie
public static const COMMON_EVENT_USER_UNLOCKED: String = "usual.event.USER_UNLOCKED"
```

**功能：** 表示设备重启后解锁时，当前用户的凭据加密存储已解锁的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED

```cangjie
public static const COMMON_EVENT_VISIBLE_ACCOUNTS_UPDATED: String = "usual.event.data.VISIBLE_ACCOUNTS_UPDATED"
```

**功能：** （预留事件，暂未支持）表示账户可见更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VOLUME_BAD_REMOVAL

```cangjie
public static const COMMON_EVENT_VOLUME_BAD_REMOVAL: String = "usual.event.data.VOLUME_BAD_REMOVAL"
```

**功能：** 表示外部存储设备状态变更为挂载状态下移除的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VOLUME_EJECT

```cangjie
public static const COMMON_EVENT_VOLUME_EJECT: String = "usual.event.data.VOLUME_EJECT"
```

**功能：** 表示用户已表示希望删除外部存储介质的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VOLUME_MOUNTED

```cangjie
public static const COMMON_EVENT_VOLUME_MOUNTED: String = "usual.event.data.VOLUME_MOUNTED"
```

**功能：** 表示外部存储设备状态变更为挂载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VOLUME_REMOVED

```cangjie
public static const COMMON_EVENT_VOLUME_REMOVED: String = "usual.event.data.VOLUME_REMOVED"
```

**功能：** 表示外部存储设备状态变更为移除的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_VOLUME_UNMOUNTED

```cangjie
public static const COMMON_EVENT_VOLUME_UNMOUNTED: String = "usual.event.data.VOLUME_UNMOUNTED"
```

**功能：** 表示外部存储设备状态变更为卸载的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_AP_STA_JOIN

```cangjie
public static const COMMON_EVENT_WIFI_AP_STA_JOIN: String = "usual.event.wifi.WIFI_HS_STA_JOIN"
```

**功能：** 表示客户端加入当前设备Wi-Fi热点的普通事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_AP_STA_LEAVE

```cangjie
public static const COMMON_EVENT_WIFI_AP_STA_LEAVE: String = "usual.event.wifi.WIFI_HS_STA_LEAVE"
```

**功能：** 表示客户端已断开与当前设备Wi-Fi热点的连接的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_CONN_STATE

```cangjie
public static const COMMON_EVENT_WIFI_CONN_STATE: String = "usual.event.wifi.CONN_STATE"
```

**功能：** 表示Wi-Fi连接状态发生改变的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_HOTSPOT_STATE

```cangjie
public static const COMMON_EVENT_WIFI_HOTSPOT_STATE: String = "usual.event.wifi.HOTSPOT_STATE"
```

**功能：** 表示Wi-Fi热点状态的公共事件，如启用或禁用。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE

```cangjie
public static const COMMON_EVENT_WIFI_MPLINK_STATE_CHANGE: String = "usual.event.wifi.mplink.STATE_CHANGE"
```

**功能：** 表示MPLink（增强Wi-Fi功能）状态已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_CONN_STATE

```cangjie
public static const COMMON_EVENT_WIFI_P2P_CONN_STATE: String = "usual.event.wifi.p2p.CONN_STATE_CHANGE"
```

**功能：** 表示Wi-Fi P2P连接状态改变的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_CURRENT_DEVICE_STATE_CHANGED: String = "usual.event.wifi.p2p.CURRENT_DEVICE_CHANGE"
```

**功能：** 表示Wi-Fi P2P当前设备状态变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_GROUP_STATE_CHANGED: String = "usual.event.wifi.p2p.GROUP_STATE_CHANGED"
```

**功能：** 表示Wi-Fi P2P群组信息已更改的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_PEERS_DISCOVERY_STATE_CHANGED: String = "usual.event.wifi.p2p.PEER_DISCOVERY_STATE_CHANGE"
```

**功能：** 表示Wi-Fi P2P发现状态变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_PEERS_STATE_CHANGED: String = "usual.event.wifi.p2p.DEVICES_CHANGE"
```

**功能：** 表示Wi-Fi P2P对等体状态变化的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_P2P_STATE_CHANGED

```cangjie
public static const COMMON_EVENT_WIFI_P2P_STATE_CHANGED: String = "usual.event.wifi.p2p.STATE_CHANGE"
```

**功能：** 表示Wi-Fi P2P状态（如启用和禁用）公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_POWER_STATE

```cangjie
public static const COMMON_EVENT_WIFI_POWER_STATE: String = "usual.event.wifi.POWER_STATE"
```

**功能：** 表示Wi-Fi状态（如启用和禁用）公共事件的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_RSSI_VALUE

```cangjie
public static const COMMON_EVENT_WIFI_RSSI_VALUE: String = "usual.event.wifi.RSSI_VALUE"
```

**功能：** 表示Wi-Fi信号强度（RSSI）改变的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22

### static const COMMON_EVENT_WIFI_SCAN_FINISHED

```cangjie
public static const COMMON_EVENT_WIFI_SCAN_FINISHED: String = "usual.event.wifi.SCAN_FINISHED"
```

**功能：** 表示Wi-Fi接入点已被扫描并证明可用的公共事件。

**类型：** String

**系统能力：** SystemCapability.Notification.CommonEvent

**起始版本：** 22
