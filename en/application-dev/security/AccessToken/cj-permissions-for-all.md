# Open Permissions (System Authorization)

All permissions listed here are system-granted open permissions, available to all applications.

When an application requests a system_grant permission, the system will automatically grant the corresponding permission to the application during installation.

<!--Del-->
> **Note:**
>
> Permissions with a normal level do not involve ACL enablement fields.
<!--DelEnd-->

## Request Method

The authorization method for the following permissions is [system_grant](./cj-app-permission-mgmt-overview.md#system_grant-system-authorization). For the request method, refer to [Declaring Permissions](./cj-declare-permissions.md).

## Permission List

### ohos.permission.USE_BLUETOOTH

Allows an application to view Bluetooth configurations.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.GET_BUNDLE_INFO

Allows querying basic application information.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.PREPARE_APP_TERMINATE

Allows an application to perform custom pre-termination actions before closing.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.PRINT

Allows an application to access printing framework capabilities.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.DISCOVER_BLUETOOTH

Allows an application to configure local Bluetooth, discover remote devices, and pair/connect with them.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.ACCELEROMETER

Allows an application to read accelerometer sensor data.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.ACCESS_BIOMETRIC

Allows an application to use biometric recognition capabilities for identity authentication.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.ACCESS_NOTIFICATION_POLICY

Allows an application to access notification policies on this device.

This permission is only required when controlling ringtone changes from silent to non-silent mode.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.GET_NETWORK_INFO

Allows an application to obtain data network information.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.GET_WIFI_INFO

Allows an application to obtain Wi-Fi information.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.GYROSCOPE

Allows an application to read gyroscope sensor data.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.INTERNET

Allows using Internet networks.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.KEEP_BACKGROUND_RUNNING

Allows a Service Ability to continue running in the background.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.NFC_CARD_EMULATION

Allows an application to implement card emulation functionality.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.NFC_TAG

Allows an application to read/write Tag cards.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.PRIVACY_WINDOW

Allows an application to set a window as a privacy window, preventing screenshots or screen recordings.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.PUBLISH_AGENT_REMINDER

Allows an application to use background agent reminders.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.SET_WIFI_INFO

Allows an application to configure Wi-Fi devices.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.VIBRATE

Allows an application to control motor vibration.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.CLEAN_BACKGROUND_PROCESSES

Allows an application to clean up related background processes based on package names.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.COMMONEVENT_STICKY

Allows an application to publish sticky common events.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.MODIFY_AUDIO_SETTINGS

Allows an application to modify audio settings.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.RUNNING_LOCK

Allows an application to obtain a running lock to ensure continuous background operation.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.SET_WALLPAPER

Allows an application to set wallpapers.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.ACCESS_CERT_MANAGER

Allows an application to perform operations such as querying certificates and private credentials.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.hsdr.HSDR_ACCESS

Allows an application to access the security detection and response framework.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.RUN_DYN_CODE

Allows the system Ark runtime engine to execute dynamically delivered Ark bytecode in restricted mode.

APIs related to this permission are system APIs, and only specific system applications can request this permission.

**Permission Level:** normal

**Authorization Method:** system_grant

**Initial Version:** 12

### ohos.permission.READ_CLOUD_SYNC_CONFIG

Allows cloud-enabled applications to query application cloud synchronization configuration information.

**Permission Level:** normal

**Authorization Method:** system_grant**Initial Version:** 12  

### ohos.permission.STORE_PERSISTENT_DATA  

Allows an application to store persistent data, which will not be cleared until the device is factory reset or the system is reinstalled.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.ACCESS_EXTENSIONAL_DEVICE_DRIVER  

Allows an application to use extended functionalities of external devices.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.READ_ACCOUNT_LOGIN_STATE  

Allows an application to read the login status of a user account.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.ACCESS_SERVICE_NAVIGATION_INFO  

Allows an application to access navigation information services.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.PROTECT_SCREEN_LOCK_DATA  

Allows an application to protect its sensitive data from being accessed after the screen is locked.  

After obtaining this permission, the system creates a high-security-level directory (el5) for the user. The application can store data in this directory, which becomes inaccessible after the screen is locked.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.FILE_ACCESS_PERSIST  

Allows an application to persistently access file URIs.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.ACCESS_CAR_DISTRIBUTED_ENGINE  

Allows an application to access the distributed travel business engine.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.WINDOW_TOPMOST  

Allows an application to set a window as the topmost application window.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.INPUT_KEYBOARD_CONTROLLER  

Allows an application to configure the state of keyboard function keys.  

For example, enabling or disabling the CapsLock key. Currently, only input method applications can request this permission.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.SET_ABILITY_INSTANCE_INFO  

Allows an application to individually configure the icon and label information for each Ability.  

The configured icon and label information can be displayed in the task center and shortcut bar interfaces.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12  

### ohos.permission.NDK_START_SELF_UI_ABILITY  

Allows an application to launch an Ability within the same application via C API.  

Currently, only applications on 2-in-1 devices can request this permission.  

**Permission Level:** normal  

**Authorization Mode:** system_grant  

**Initial Version:** 12