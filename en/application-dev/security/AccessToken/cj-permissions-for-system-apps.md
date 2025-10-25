# System Application Permissions Available for ACL Application (System Grant)

Before applying for target permissions, developers are advised to first understand the [application paths for different permissions](./cj-determine-application-mode.md). After gaining a basic understanding of the permission workflow, combine it with the specific descriptions of the following permission fields to determine whether the application can apply for the target permission, thereby improving development efficiency.

> **Note:**
>
> - The following permissions are only available to applications with an APL level of system_basic or higher, and are not open to applications with an APL level of normal.
> - The authorization method for the following permissions is system_grant (system grant).
> - The following permissions can be applied for across levels via [Access Control List (ACL)](./cj-app-permission-mgmt-overview.md#basic-concepts-in-permission-mechanism).

For the application process, refer to [Choosing the Permission Application Method](./cj-determine-application-mode.md).

## ohos.permission.PRE_START_ATOMIC_SERVICE

Allows the app market to skip the loading dialog and pre-open a window for atomic services, displaying loading animations within the window.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_APP_KEEP_ALIVE

Allows setting keep-alive for third-party application processes.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 14

## ohos.permission.ACCESS_BBOX_DIR

Allows system applications to read log files under the bbox path.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.CONTROL_LOCATION_SWITCH

Allows applications to turn the location information switch on and off.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.LOCATION_SWITCH_IGNORED

Allows system applications to obtain location information even when the location switch is turned off.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 18

## ohos.permission.SUBSCRIBE_SWING_ABILITY

Allows applications to use the smart sensing subscription capability.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGER_SWING_MOTION

Allows applications to use the air gesture self-adaptation capability.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MOCK_LOCATION

Allows applications to use the mock location feature.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_LEARN_MORE_DIALOG

Allows system applications to launch the "Learn More" display dialog to obtain more detailed information.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 13

## ohos.permission.WRITE_PROTECTION_ADVICE_POLICY

Allows system applications to modify the "Security Advice" database.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 17

## ohos.permission.READ_PROTECTION_ADVICE_POLICY

Allows system applications to read the "Security Advice" database.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 17

## ohos.permission.PROXY_MESSAGE_AUTH

Allows system applications to call the "Messages" application authorization interface.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**Initial Version:** 18

## ohos.permission.MANAGE_SETTINGS

Allows applications to set device-level and user-level configuration data tables in SettingsData.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_SCREEN_LOCK

Allows applications to access lock screen information.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ALLOW_UPGRADE_GUIDE_ACCESS

Allows system applications to obtain application upgrade guidance data or launch the application's upgrade guidance component.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_MEDIALIB_THUMB_DB

Allows system applications to access and modify the media library database.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.AGENT_REQUIRE_FORM

Allows applications to proxy request cards.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_VPN

Allows system applications to start or stop the VPN function.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

**Change Information:** For API 10-11, ACL Enabled was false; starting from API 12, it was changed to true.

## ohos.permission.WAKEUP_VISION

Allows applications to access the voice assistant visual component.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.WAKEUP_VOICE

Allows applications to access the voice assistant wake-up component.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ATTEST_KEY

Allows applications to obtain a certificate chain for proving the legality of a key.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_PHONE_NUMBERS

Allows applications to read the device's native phone number.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACTIVATE_THEME_PACKAGE

Allows system applications to set theme content, including wallpapers, icons, skins, AOD, and fonts.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.QUERY_ACCESSIBILITY_ELEMENT

Allows batch querying of accessibility nodes.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_UNREMOVABLE_NOTIFICATION

Allows applications to publish non-removable notifications.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.UNINSTALL_BUNDLE

Allows applications to uninstall other applications.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECOVER_BUNDLE

Allows recovery of pre-installed applications.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.UPDATE_SYSTEM

Allows calling system upgrade interfaces.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.FACTORY_RESET

Allows calling factory reset interfaces.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ASSIST_DEVICE_UPDATE

Allows launching upgrade services to assist or coordinate upgrades for other devices.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.PLUGIN_UPDATE

Allows service providers to call upgrade-related interfaces for post-download and update operations of plugins and AI models.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 18

## ohos.permission.RECEIVE_UPDATE_MESSAGE

Allows applications and services to monitor key events during system upgrade processes.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_ALL_PROCESSES

Allows system services or system applications to view all files under /proc.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_LOCAL_ACCOUNTS

Allows applications to manage system local accounts.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_SYSTEM_SETTINGS

Allows applications to access or launch system settings interfaces.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_ABILITY_CONTROLLER

Allows applications to intercept Ability component launches, primarily for testing and debugging purposes (e.g., stability robustness testing).

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS_EXTENSION

Allows applications to interact across system local accounts.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.CLEAN_APPLICATION_DATA

Allows applications to clean application data.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.START_ABILITIES_FROM_BACKGROUND

Allows applications to start or access other components in the background.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_MISSIONS

Allows applications to manage tasks in the system.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

Allows applications to activate device management applications.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ENTERPRISE_CONFIG

Allows applications to activate enterprise devices.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECEIVE_ENTERPRISE_POLICY_EVENT

Allows system applications to subscribe to enterprise device management policy events.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 14

## ohos.permission.PUBLISH_SYSTEM_COMMON_EVENT

Allows applications to publish system common events.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.NOTIFICATION_CONTROLLER

Allows applications to manage notifications and subscribe to notifications.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.CLOUDDATA_CONFIG

Allows applications to obtain configuration database cloud-end information capabilities.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_DEFAULT_APPLICATION

Allows applications to query default applications.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_INTELLIGENT_VOICE

Allows applications to access intelligent voice service interfaces.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.POWER_MANAGER

Allows applications to call power management subsystem interfaces to sleep or wake up devices.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12**起始版本：** 12  

## ohos.permission.GET_SCENE_CODE  

Allows an application to obtain the current scene value of a specified application.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_ECOLOGICAL_RULE  

Allows setting scene value generation rules and associated experiences for control services.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INSTALL_ENTERPRISE_BUNDLE  

Allows an application to install enterprise InHouse applications.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INSTALL_BUNDLE  

Allows an application to install or uninstall other applications (excluding enterprise-related applications, currently including enterprise InHouse, enterprise MDM, and enterprise normal applications).  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_SHORTCUTS  

Allows an application to query shortcut information of other applications and launch shortcuts of other applications.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.OBSERVE_FORM_RUNNING  

Allows an application to monitor the running status of cards.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.WRITE_HIVIEW_SYSTEM  

Allows an application to modify hiview data.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.READ_HIVIEW_SYSTEM  

Allows an application to access hiview data.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.READ_DFX_SYSEVENT  

Allows an application to access system event logging data.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.READ_DFX_XPOWER  

Allows an application to access xpower data.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PERMISSION_USED_STATS  

Allows system applications to access permission usage records.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PERMISSION_RECORD_TOGGLE  

Allows an application to configure the permission usage recording switch.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.CAPTURE_SCREEN  

Allows an application to capture screen images.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_CERT_MANAGER_INTERNAL  

Allows an application to perform operations such as installing, uninstalling, and authorizing user public certificate credentials.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

**Change History:** From API 9–11, the permission level was system_basic; starting from API 12, it was changed to system_core.  

## ohos.permission.CLOUDFILE_SYNC  

Allows an application to use cloud synchronization capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CHANGE_OVERLAY_ENABLED_STATE  

Allows system applications to disable applications with overlay features enabled.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SCREEN_LOCK_INNER  

Allows an application to use the screen lock service to lock the screen, send lock screen events, and receive system event callbacks.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.BACKUP  

Allows an application to possess backup and recovery capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MOUNT_FORMAT_MANAGER  

Allows an application to format external storage cards.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MOUNT_UNMOUNT_MANAGER  

Allows an application to mount and unmount external storage cards.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PROXY_AUTHORIZATION_URI  

Allows an application to proxy authorization URIs.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_CAST_ENGINE_MIRROR  

Allows an application to use screen mirroring capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_CAST_ENGINE_STREAM  

Allows an application to invoke system resource projection capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE  

Allows the installation of enterprise normal application packages on enterprise devices.  

**Permission Level:** system_core  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.UPDATE_MIGRATE  

Allows data migration during the upgrade process.  

**Permission Level:** system_basic  

**Authorization Mode:** System-granted (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12**Initial Version:** 12  

## ohos.permission.MANAGE_SENSOR  

Allows applications to turn sensors on/off without directly using them.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_PRINT_JOB  

Allows applications to manage print jobs.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.securityguard.SET_MODEL_STATE  

Allows applications to control the model switch of the device risk management platform.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.UNLOCK_DEVELOPER_MODE  

Allows applications to unlock developer mode.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.CAPTURE_VOICE_DOWNLINK_AUDIO  

Allows applications to capture downlink voice audio.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_WIFI_INFO_INTERNAL  

Allows system processes to obtain Wi-Fi-related parameters.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_BUNDLE_DIR  

Allows applications to access the installation directories of other applications.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CHANGE_ABILITY_ENABLED_STATE  

Allows changing the enabled state of applications or components.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CLOUDFILE_SYNC_MANAGER  

Allows applications to manage cloud synchronization.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.DUMP  

Allows exporting system basic information and SA service information.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.DEVICE_STANDBY_EXEMPTION  

Allows applications to use resources normally during system standby mode.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PERCEIVE_SMART_POWER_SCENARIO  

Allows applications to perceive smart power consumption scenarios.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_CAMERA_CONFIG  

Allows applications to perform operations such as globally enabling/disabling the camera.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_AUDIO_CONFIG  

Allows applications to perform operations such as globally muting the microphone.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MICROPHONE_CONTROL  

Allows applications to perform persistent global microphone muting operations.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CAPTURE_PLAYBACK  

Allows system services to directly record internal audio without using the screen recording framework.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.MICROPHONE_BACKGROUND  

Allows system applications to use the microphone in the background.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.START_DLP_CRED  

Allows system applications or services to launch the DLP credential management application.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.START_SHORTCUT  

Allows applications to launch shortcuts.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PRELOAD_UI_EXTENSION_ABILITY  

Pre-launches UIExtensionAbility instances.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_DISPOSED_APP_STATUS  

Allows setting and querying the disposal status of applications.  

**Permission Level:** system_core  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_DISPOSED_APP_STATUS  

Allows querying the disposal status of applications.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.FILE_ACCESS_MANAGER  

Allows file management applications to access public data files via the FAF framework.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_PUSH_SERVICE  

Allows applications to access the Ability of the push service.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_NET_STRATEGY  

Allows applications to obtain or modify network strategy-related information and settings.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true**Initial Version:** 12  

## ohos.permission.securityguard.REQUEST_SECURITY_EVENT_INFO  

Allows an application to obtain detailed risk data.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.securityguard.REPORT_SECURITY_INFO  

Allows an application to report risk data to the device risk management platform.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_SENSITIVE_PERMISSIONS  

Allows an application to read the status of sensitive permissions of other applications.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**Supported Devices:** General  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SERVICE_DM  

Allows system applications to obtain the authentication and networking capabilities of distributed devices.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.UPLOAD_SESSION_MANAGER  

Allows an application to manage upload task sessions.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ABILITY_BACKGROUND_COMMUNICATION  

Allows an application to launch an Ability component in the background and establish a communication connection with it.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_DLP_FILE  

Allows permission configuration and management for DLP files.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_IDS  

Allows an application to query the device's unique identifier information.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_MISSIONS  

Allows an application to access task stack information.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

**Deprecated Version:** 9  

## ohos.permission.BUNDLE_ACTIVE_INFO  

Allows system applications to query the runtime duration of other applications in the foreground or background.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CONNECT_IME_ABILITY  

Allows binding to the InputMethodAbility (Input Method Ability).  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CONNECT_SCREEN_SAVER_ABILITY  

Allows binding to the ScreenSaverAbility (Screen Saver Ability).  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CONNECTIVITY_INTERNAL  

Allows an application to obtain network-related information or modify network-related settings. Currently, only system applications can request this permission.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CONTROL_TASK_SYNC_ANIMATOR  

Allows an application to use synchronized task animations.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.DOWNLOAD_SESSION_MANAGER  

Allows an application to manage download task sessions.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_DISTRIBUTED_ACCOUNTS  

Allows an application to query system distributed account information.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_LOCAL_ACCOUNTS  

Allows an application to query system local account information.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_TELEPHONY_STATE  

Allows an application to read telephony information.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_BOOSTER_SERVICE  

Allows system services or system applications to call functional interfaces such as network quality awareness, network scenario prediction, and network acceleration in the network booster service.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_WALLPAPER  

Allows an application to read wallpaper files.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GRANT_SENSITIVE_PERMISSIONS  

Allows an application to grant sensitive permissions to other applications.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**Supported Devices:** General  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.LAUNCH_DATA_PRIVACY_CENTER  

Allows an application to navigate from its privacy statement page to the "Data & Privacy" page.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.LISTEN_BUNDLE_CHANGE  

Allows an application to monitor changes in the installation, update, or uninstallation status of other applications.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_BLUETOOTH  

Allows an application to pair with Bluetooth devices and access their phonebook or messages.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_DISTRIBUTED_ACCOUNTS  

Allows an application to manage system distributed account information.**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_MEDIA_RESOURCES  

Allows applications to access and manage currently playing media resources on the device.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_SECURE_SETTINGS  

Allows applications to modify security-related system settings.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_WIFI_CONNECTION  

Allows applications to manage Wi-Fi connections.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_WIFI_HOTSPOT  

Allows applications to enable or disable Wi-Fi hotspots.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.NOTIFICATION_AGENT_CONTROLLER  

Allows applications to send proxy notifications.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PLACE_CALL  

Allows applications to make phone calls directly.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.POWER_OPTIMIZATION  

Allows system applications to configure power-saving mode, retrieve power-saving mode settings, and receive notifications of configuration changes.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PROVISIONING_MESSAGE  

Allows activation of the super device manager application.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.radio.ACCESS_FM_AM  

Allows applications to access radio-related services.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.READ_SCREEN_SAVER  

Allows applications to query screen saver status information.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REBOOT  

Allows applications to reboot the device.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REBOOT_RECOVERY  

Allows system applications to reboot the device and enter recovery mode.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REFRESH_USER_ACTION  

Allows applications to recalculate timeout periods upon receiving user events.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REMOVE_CACHE_FILES  

Allows clearing the cache of specified applications.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REQUIRE_FORM  

Allows applications to retrieve Ability Forms.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.START_DESKTOP_UI_COMPONENT  

Allows applications to launch desktop UI components.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.REVOKE_SENSITIVE_PERMISSIONS  

Allows applications to revoke sensitive permissions granted to other applications.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**Supported Devices:** General  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.RUN_ANY_CODE  

Allows applications to run unsigned code.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.sec.ACCESS_UDID  

Allows system applications to retrieve the UDID.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.securityguard.REQUEST_SECURITY_MODEL_RESULT  

Allows applications to retrieve the device's risk status.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.SET_DEFAULT_APPLICATION  

Allows applications to set or reset default applications.  

**Permission Level:** system_core  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.SET_TELEPHONY_STATE  

Allows applications to modify telephony states.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.SET_TIME  

Allows applications to modify the system time.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.SET_TIME_ZONE  

Allows applications to modify the system time zone.  

**Permission Level:** system_basic  

**Authorization Method:** System authorization (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.START_ABILITIES_FROM_BACKGROUNDAllow applications to start FA in the background.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

**Deprecated Version:** 9

## ohos.permission.START_INVISIBLE_ABILITY

Allows applications to invoke an Ability regardless of its visibility.

**Permission Level:** system_core

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.STORAGE_MANAGER

Allows applications to call storage manager service interfaces for space statistics and volume information queries.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.UPDATE_CONFIGURATION

Allows updating system configurations.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.WRITE_SCREEN_SAVER

Allows applications to modify screensaver status information.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_BLUETOOTH_LOCAL_MAC

Allows applications to obtain the local Bluetooth MAC address.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_BLUETOOTH_PEERS_MAC

Allows applications to obtain the real Bluetooth MAC address of peripheral devices.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.USE_USER_IDM

Allows applications to access system identity credential information.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_USER_IDM

Allows the enrollment and management of user identity authentication credentials.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_PIN_AUTH

Allows registration of PIN authentication processes to obtain callback for PIN data.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_USER_AUTH_INTERNAL

Allows calling internal system interfaces of the unified identity authentication service.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SUPPORT_USER_AUTH

Access permission for the unified user authentication control resource pool.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_SENSING_WITH_ULTRASOUND

Allows applications to use ultrasonic sensing.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_DISTRIBUTED_HARDWARE

Allows system services or system applications to access distributed hardware resources.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.INSTANTSHARE_SWITCH_CONTROL

Allows system services or system applications to change the instant sharing switch status.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_INSTANTSHARE_SERVICE

Allows system services or system applications to access the instant sharing service.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_INSTANTSHARE_PRIVATE_ABILITY

Allows system services or system applications to use instant sharing private application capabilities.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_MCP_AUTHORIZATION

Allows MCP host applications to proxy their child applications for user account authorization login.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_BUNDLE_RESOURCES

Allows querying application resource information.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.COOPERATE_MANAGER

Allows system applications to enable cross-device keyboard and mouse capabilities.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.PERCEIVE_TRAIL

Allows system applications to use MSDP trail perception functionality.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXECUTE_INSIGHT_INTENT

Allows system applications to execute intent invocations.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.VERIFY_ACTIVATION_LOCK

Allows applications to verify the legitimacy of activation lock credentials.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_OUC

Allows system applications to launch software update capabilities.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_FINGERPRINT_AUTH

Allows calling interfaces to configure and manage fingerprint authentication modules.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.TRUSTED_RING_HASH_DATA_PERMISSION

Allows applications to send data to the trusted ring of critical assets.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.INPUT_CONTROL_DISPATCHING

Allows system applications to block shortcut key distribution logic.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_TRUSTED_RING

Allows the use of capabilities provided by the trusted ring service for critical assets.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.USE_TRUSTED_RING

Allows applications or services to utilize the trusted ring joining capability for critical assets.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECEIVE_APP_INSTALL_INFO_CHANGE

Allows applications to monitor the installation progress of other applications.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.LAUNCH_SPAMSHIELD_PAGE

Allows applications to access the spam interception page.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_SPAMSHIELD_SERVICE

Allows applications to access spam interception capabilities.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_SECURITY_PRIVACY_CENTER

Allows services to integrate with the Security and Privacy Center.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_SECURITY_PRIVACY_ADVICE

Allows system applications to obtain advisory data from the Security and Privacy Center.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_SECURITY_PRIVACY_ADVICE

Allows system applications to process protection recommendations from the Security and Privacy Center.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.USE_SECURITY_PRIVACY_MESSAGER

Allows system services to invoke permission management-related interfaces.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_PRIVACY_INDICATOR

Allows system applications to obtain detailed information about privacy permission event notifications.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_PRIVACY_INDICATOR

Allows system applications to control the display status of privacy permission event notifications.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXEMPT_PRIVACY_INDICATOR

Allows applications to use permissions without displaying notifications.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXEMPT_CAMERA_PRIVACY_INDICATOR

Allows applications to use camera permissions without displaying notifications.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXEMPT_MICROPHONE_PRIVACY_INDICATOR

Allows applications to use microphone permissions without displaying notifications.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXEMPT_LOCATION_PRIVACY_INDICATOR

Allows applications to use location permissions without displaying notifications.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.EXEMPT_PRIVACY_SECURITY_CENTER

Allows system applications to hide permission details in the "Privacy and Security" section.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 13

## ohos.permission.GET_SUPER_PRIVACY

Allows retrieval of the super privacy mode status.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_SUPER_PRIVACY

Allows configuration of the super privacy mode status.

**Permission Level:** system_core

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_PRIVATE_SPACE_MANAGER

Allows system applications or services to launch private space management.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_PRIVATE_SPACE_PASSWORD_PROTECT

Allows system applications to invoke password protection interfaces for private space services.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_PASSWORDVAULT_ABILITY

Allows system applications or services to launch password vault capabilities.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_TEXTAUTOFILL_ABILITY

Allows system applications or services to launch the text autofill application management page.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_LOWPOWER_MANAGER

Allows system applications or services to send messages to the lowpowermanager.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_APP_BOOT

Allows system applications to configure auto-start settings for other applications upon boot.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_ACCOUNT_KIT_SERVICE

Allows account services to query and modify account data.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.REQUEST_ANONYMOUS_ATTEST

Allows system applications to utilize device anonymous attestation capabilities.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_ACCOUNT_KIT_UI

Allows system applications to launch the account user authentication interface.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.START_RECENT_ABILITY

Allows applications to launch a specified UIAbility. If the UIAbility has multiple instances, the most recently launched instance will be started.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_CLOUD_SYNC_CONFIG

Allows cloud-integrated applications to manage cloud synchronization configurations.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_FINDDEVICE

Allows applications to launch the "Find Device" application.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_FINDSERVICE

Allows system applications to retrieve the status of the "Find My Device" toggle and enable it.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.READ_FINDSERVICE

Allows system applications to read the status of the "Find My Device" toggle.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_USB_CONFIG

Allows applications to manage USB device functionalities and ports.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.START_SYSTEM_DIALOG

Allows applications to launch system modal dialogs.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_STATUSBAR_ICON

Allows applications to access status bar icons.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** TRUE

**Initial Version:** 12

## ohos.permission.MANAGE_SYSTEM_AUDIO_EFFECTS

Allows applications to manage system audio effects.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SECURE_PASTE

Allows applications to silently read clipboard content.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_CODE_PROTECT_INFO

Allows system applications to configure cloud-side public keys and encrypted working keys, and negotiate code protection key information.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_ADVANCED_SECURITY_MODE

Allows applications to modify Shield Guardian mode configurations.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SET_DEVELOPER_MODE

Allows applications to modify developer mode configurations.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.DISABLE_PERMISSION_DIALOG

Allows system applications to configure whether specified applications can launch permission dialogs.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_ACTIVATION_LOCK

Allows applications to manage device activation locks.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_PRIVATE_PHOTOS

Allows applications to access system-preset hidden albums and files within them.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECORD_VOICE_CALL

Allows applications to record call content.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_APP_INSTALL_INFO

Allows applications to create and manage application installation tasks.

**Permission Level:** system_core

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_APP_UNINSTALL

Allows system applications to uninstall other applications.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 19

## ohos.permission.ACCESS_ADVANCED_SECURITY_MODE

Allows system applications to open the Shield Guardian mode configuration interface.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ACCESS_HIVIEWX

Allows system applications to launch the "User Experience Improvement Program".

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 12**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ACCESS_HIVIEWCARE

Allows system applications to activate intelligent detection capabilities.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.SET_SANDBOX_POLICY

Allows system applications to configure dynamic sandbox policies.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.CHECK_SANDBOX_POLICY

Allows system applications or services to query sandbox control policies of other applications.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 15

## ohos.permission.TRIGGER_ACTIVATIONLOCK

Allows system SAs to invoke "Find My Device" functionality.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.WRITE_PRIVACY_PUSH_DATA

Allows applications to write privacy-sensitive Push data to another application.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.READ_PRIVACY_PUSH_DATA

Allows applications to read Push-based privacy data from another application.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.MANAGE_NEARLINK

Allows applications to pair SparkLink devices and access device contacts or messages.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.GET_NEARLINK_LOCAL_MAC

Allows applications to obtain the local SparkLink MAC address.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.GET_NEARLINK_PEER_MAC

Allows applications to obtain peer devices' SparkLink MAC addresses.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.MANAGE_UWB

Allows system applications to manage UWB functionality.

Examples include enabling/disabling UWB, querying chip types, and checking UWB capabilities.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.USE_UWB_RANGING

Allows system applications to utilize UWB ranging functionality.

Examples include opening ranging sessions, initiating ranging, stopping ranging, and closing ranging sessions.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.MANAGE_FINDNETWORK

Allows applications to manage "Find My" network switches and perform device pairing/unpairing operations.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.OPERATE_FINDNETWORK

Allows applications to invoke "Find My" network operation interfaces.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.QUERY_FINDNETWORK_LOCATION

Allows applications to query offline device locations via the "Find My" network.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.REGISTER_FINDNETWORK_ACCESSORY

Allows applications and system services to initiate accessory registration processes for the Find My network.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 13

## ohos.permission.MANAGE_SHUTDOWN_FINDNETWORK

Allows applications and system services to manage device shutdown location tracking functionality.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 15

## ohos.permission.MANAGE_RGM

Allows system services or applications to manage RGM.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ACCESS_PROTOCOL_DFX_DATA

Allows system applications to read communication failure and system statistical data.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ACCESS_PROTOCOL_DFX_STATE

Allows system applications to enable/disable communication protocol-related switches.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ACCESS_CMAP_SERVICE

Allows system applications to access communication map services.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 14

## ohos.permission.MANAGE_USER_ACCOUNT_INFO

Allows system applications and SAs to invoke account services.

**Permission level:** system_core

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ALLOW_TIPS_ACCESS

Allows system applications to launch exposed components of other system applications.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.ACCESS_AI_ABILITY

Allows applications and system SAs to invoke voice/vision service interfaces.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.READ_HEALTH_MOTION

Allows system applications to read step counts and three-ring fitness data.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12

## ohos.permission.hsdr.REQUEST_HSDR

Allows system applications to access cloud query functionality of the security detection response framework's security policies.

**Permission level:** system_basic

**Authorization method:** System-granted (system_grant)

**ACL enabled:** true

**Initial version:** 12**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.WRITE_GTOKEN_POLICY  

Allows system applications to write application control policies.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.READ_GTOKEN_POLICY  

Allows system applications to read application control policies.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.NOTIFY_DEBUG_ASSERT_RESULT  

Allows applications to set debug assertion results.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.QUERY_PASSWORD_VAULT_DATA  

Allows applications to retrieve password vault account data.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.WRITE_ACCOUNT_LOGIN_STATE  

Allows user accounts to write their own login status to the data management service.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS_AS_USER  

Allows U0 user-space services to invoke account open capability APIs.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.SUBSCRIBE_NOTIFICATION_WINDOW_STATE  

Allows applications to subscribe to broadcasts sent when the notification panel is displayed or collapsed.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CHANGE_DISPLAYMODE  

Allows system applications to change screen modes.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MIGRATE_DATA  

Allows applications to migrate data from the input path to a specified directory.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_DYNAMIC_ICON  

Allows applications to use dynamic icons.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CHANGE_BUNDLE_UNINSTALL_STATE  

Allows system applications to change the uninstallable state of specified applications.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_STYLUS_EVENT  

Allows system applications to use stylus system capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.USE_CLOUD_DRIVE_SERVICE  

Allows applications and services to use cloud drive services for device-cloud data synchronization.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** TRUE  

**Initial Version:** 12  

## ohos.permission.USE_CLOUD_BACKUP_SERVICE  

Allows applications and services to trigger cloud backup task execution and notify backup-related events.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** TRUE  

**Initial Version:** 12  

## ohos.permission.USE_CLOUD_COMMON_SERVICE  

Allows applications to obtain cloud-related information and resources through cloud common services.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** TRUE  

**Initial Version:** 12  

## ohos.permission.PRELOAD_APPLICATION  

Allows system applications or system services to preload application processes.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ENABLE_EXPERIENCE_HBM  

Allows applications to enable High Brightness Mode (HBM) for the screen.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.SET_PROCESS_CACHE_STATE  

Allows applications to configure whether to support application caching and fast startup after caching.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SYSTEM_APP_CERT  

Allows callers to manage and use system business certificate credentials.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_USER_TRUSTED_CERT  

Allows callers to manage user CA certificates.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_LOCAL_BACKUP  

Allows applications to access local backup data directories.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CAST_AUDIO_OUTPUT  

Allows system casting/collaboration applications to initiate audio casting.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.WRITE_RINGTONE  

Allows the ringtone library to perform write operations.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_ACCOUNT_MINORS_INFO  

Allows system applications to retrieve minor user account information.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_LOCAL_THEME  

Allows system applications to access locally downloaded theme content.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SHADER_CACHE_DIR  

Allows system applications to access the shader_cache root directory.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INSTALL_CLONE_BUNDLE  

Allows applications to install cloned applications.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.UNINSTALL_CLONE_BUNDLE  

Allows applications to uninstall cloned applications.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SCREEN_LOCK_MEDIA_DATA  

Allows applications to continue accessing media images and video data after the screen is locked.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SCREEN_LOCK_ALL_DATA  

Allows applications to continue accessing sensitive data such as media images and videos, call logs, call recordings, SMS content, and emails after the screen is locked.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_DEVICE_COLLABORATION_PRIVATE_ABILITY  

Allows system services or system applications to access private multi-screen collaboration capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_FILE_CONTENT_SHARE  

Allows system services or system applications to access shared file content.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_RINGTONE_RESOURCE  

Allows system applications to access and write to the public directory of ringtone data.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SUBSCRIPTION_CAPSULE_DATA  

Allows system applications to access subscription capsule data.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SEARCH_SERVICE  

Allows system applications to invoke local search capabilities provided by the integrated search service.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INJECT_INPUT_EVENT  

Allows system applications to inject input events.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.QUERY_SECURITY_EVENT  

Allows applications to retrieve detailed risk data.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REPORT_SECURITY_EVENT  

Allows applications to report risk data to the device risk management platform.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.QUERY_SECURITY_MODEL_RESULT  

Allows applications to query the execution results of security models.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_SECURITY_GUARD_CONFIG  

Allows applications to manage configurations of the device risk management component.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.COLLECT_SECURITY_EVENT  

Allows applications to collect security events.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.QUERY_SECURITY_POLICY_FROM_CLOUD  

Allows applications to query security policies from the cloud.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.REPORT_SECURITY_EVENT_TO_CLOUD  

Allows applications to report security events to the cloud.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_SCAN_SERVICE  

Allows system applications to invoke the code value distribution capability provided by the scan-to-access service.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_FACTORY_OTA_DIR  

Allows system applications to access the wireless upgrade directory.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_MOUSE_CURSOR  

Allows system applications to configure mouse cursor-related states.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.FILTER_INPUT_EVENT  

Allows system applications to filter input events.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INPUT_DEVICE_CONTROLLER  

Allows applications to query and configure input device-related states.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACTIVATE_DEVICE_PSI  

Allows system applications or system services to report device activation status.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.DUMP_AUDIO  

Allows applications to enable the audio framework dump capability, saving audio data to local storage.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.RECEIVE_FUSION_MESSAGES  

Allows system services or system applications to receive fusion service messages.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.RECEIVE_BMS_BROKER_MESSAGES  

Allows system services or system applications to receive package management broker service messages.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_FUSION_MANAGER  

Allows system services or system applications to access fusion services.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PUBLISH_LOCATION_EVENT  

Allows applications to publish public events related to location management.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_MULTICORE_HYBRID_ABILITY  

Allows applications to access smartwatch system services.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_DEVICE_COLLABORATION_SERVICE  

Allows applications to use multi-screen service capabilities.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_APP_DOMAIN_BUNDLE_INFO  

Allows applications to access the mapping relationship between applications and domain names.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.OPEN_FILE  

Allows system applications to launch the file management application and open files/folders.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PROCESS_FILE_COPY_PASTE  

Allows system applications to launch the file management application and copy, cut, or paste files.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CLEAR_RECYCLEBIN  

Allows system applications to launch the file management application and empty the recycle bin.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_FILE_THUMBNAIL  

Allows system services to obtain file thumbnails.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.NETWORK_DHCP  

Allows system applications to request and assign IP addresses via DHCP.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ALLOW_CONNECT_CAR  

Allows applications to connect to in-vehicle infotainment systems.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_IDM_WIDGET  

Allows system applications to launch user credential input widgets.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.MANAGE_ACCESSORY  

Allows applications to obtain accessory (keyboard, mouse, etc.) information, send data to accessories, and receive responses.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.COLLECT_ACCESSORY_LOG  

Allows applications to collect logs from accessories (keyboard, mouse, etc.).  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.INSTALL_INTERNALTESTING_BUNDLE  

Allows applications to install developer internal testing builds.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PUBLISH_DISPLAY_ROTATION_EVENT  

Allows SAs to send screen rotation status information to applications or system services.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.PUBLISH_CAST_PLUGGED_EVENT  

Allows SAs to send casting cable insertion/removal status information to applications or system services.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GET_ETHERNET_LOCAL_MAC  

Allows applications to query the current MAC address of an Ethernet connection.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.ALLOW_SHOW_NON_SECURE_WINDOWS  

Allows modal UIExtension to disable hiding of non-secure windows.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.ACCESS_DISTRIBUTED_MODEM  

Allows system services to access virtual modems.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.GET_TELEPHONY_ESIM_STATE  

Allows system applications to obtain eSIM profile information and device chip activation attributes.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.SET_TELEPHONY_ESIM_STATE  

Allows system applications to modify eSIM profile files and perform eSIM upgrades.  

**Permission Level:** system_basic  

**Authorization Mode:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.CAMERA_BACKGROUND  

Allows system applications to use the camera in the background.  

**Permission Level:** system_core  

**Authorization Mode:** system_grant**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.CALLED_TRANSITION_ON_LOCK_SCREEN  

Allows an application to be launched and directly transitioned by another application on the lock screen.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.CALLED_BELOW_LOCK_SCREEN  

Allows an application to be launched while the device is in the locked state.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.ACCESS_ANALYTICS  

Allows system services to access and read the contents of files under the path `/data/log/faultlog/faultlogger`.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.START_RESTORE_NOTIFICATION  

Allows system applications to subscribe to events indicating the start of restoration by the backup framework.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.READ_WEATHER_DATA  

Allows applications to read weather data.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.ACCESS_MCU_LOG_DIR  

Allows system applications to access the MCU (microcontroller unit) log directory.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.GRANT_SHORT_TERM_WRITE_MEDIAVIDEO  

Allows system applications or system services to grant third-party applications temporary access permissions for storing images and videos.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.CHECK_QUICKFIX_RESULT  

Allows system services or applications to check the installation results of patches.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

**Change Information:** From API 12-13, the scope was limited to system services. Starting from API 14, the scope has been expanded to system applications.  

## ohos.permission.USER_AUTH_FROM_BACKGROUND  

Allows applications/services to initiate user authentication requests in the background.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.MANAGE_RECOVERY_KEY  

Allows applications to create or delete recovery keys.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.UTILIZE_RECOVERY_KEY  

Allows applications to use recovery keys to reset the lock screen password or recover user data.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.ACCESS_CONFIDENTIAL_COMPUTING_ZONE  

Allows applications to access the confidential computing zone.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.SYNC_ASSET_BETWEEN_TRUSTED_ACCOUNT  

Allows applications to synchronize critical assets between devices logged in with the same trusted account.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.GET_RECOVERY_KEY_BRIEF_INFORMATION  

Allows applications to retrieve brief information about recovery keys.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.ACCESS_VIRTUAL_KEYBOARD  

Allows applications/services to update/query the virtual keyboard status.  

With this permission, applications can update the virtual keyboard status, and services can query it. Currently, this permission can only be requested in 2-in-1 device scenarios.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.READ_APP_LOCK  

Allows system applications to read the application lock status.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.WRITE_APP_LOCK  

Allows system applications to modify the application lock status.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.ACCESS_APP_LOCK  

Allows applications to access the application lock.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 13  

## ohos.permission.ACCESS_APP_SINGLE_PERMISSION_MANAGEMENT  

Allows applications to launch the interface for modifying permissions granted to other applications.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 15  

## ohos.permission.ACCESS_APP_INSTALL_DIR  

Allows system applications to access the installation file directory.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 14  

## ohos.permission.ACCESS_ACCOUNT_SERVICE_EXTENSION_ABILITY  

Allows system applications to invoke services provided by the Account ServiceExtensionAbility.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 15  

## ohos.permission.ANTI_FRAUD  

Allows applications to integrate risk control probes to detect device-side risks, with the results serving as inputs for cloud-side risk decision-making.  

**Permission Level:** system_basic  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.EXEMPT_CAPTURE_SCREEN_AUTHORIZE  

Allows applications to initiate screen recording without triggering the privacy authorization pop-up window.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 15  

## ohos.permission.STORAGE_MANAGER_CRYPT  

Allows system applications and system services to call interfaces for encryption and decryption operations.  

**Permission Level:** system_core  

**Authorization Method:** System grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

## ohos.permission.WATCH_READ_EMERGENCY_INFO  

Allows applications to read SOS personal emergency information data.**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.WATCH_WRITE_EMERGENCY_INFO  

Allows applications to write SOS personal emergency information data.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.WATCH_START_SOS_SERVICE  

Allows applications to enable or access SOS services.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

**Change Log:** From API 12-14, this permission was only available to system services; starting from API 15, it was extended to system applications.  

## ohos.permission.ACCESS_DLP_HIDE_INFO  

Allows system applications to launch the anti-peeping protection settings page.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.DLP_GET_HIDE_STATUS  

Allows system applications to use information hiding interfaces and obtain the ability to check information hiding status.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.GET_ANIM_POLICY  

Allows system applications to register animation plugins and obtain animation usage policies.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.VIRTUAL_KEYBOARD_WINDOW  

Allows system applications to create virtual keyboard windows.  

System applications must obtain this permission to successfully create virtual keyboard windows. Currently, only system applications on 2-in-1 devices can apply for this permission.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 15  

## ohos.permission.GET_FAMILY_INFO  

Allows system applications to retrieve group information from "Family Sharing."  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_FUSION_AWARENESS_DATA  

Allows system applications to obtain fusion awareness data.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_ACCOUNT_RECOMMENDATION_DATA  

Allows applications to read "Account Suggestion" data and launch the Account Suggestion list UIExtensionAbility.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.GET_PAGE_INFO  

Allows system applications to obtain specified application page information.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_DDK_DRIVERS  

Allows extended peripheral driver clients to bind to extended peripheral driver servers.  

This permission is used for verifying the binding of extended peripheral clients to servers. Specific rules include:  

1. The target extended peripheral server described in the `value` field of the client's permission declaration must be either already published or published together.  
2. The capabilities provided by the target extended peripheral server must align with the business requirements of the extended peripheral client.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Carries Additional Data:** Yes  

**Initial Version:** 18  

## ohos.permission.ACCESS_DDK_SCSI_PERIPHERAL  

Allows extended peripheral drivers to access SCSI DDK interfaces for developing SCSI Peripheral extended peripheral drivers.  

Supports the development of the following types of peripheral drivers:  
Peripherals connected to the host via USB bus, meeting the following criteria:  

1. The peripheral's `InterfaceClass` is Mass Storage (0x08), and `InterfaceSubClass` is SCSI Transparent Command Set (0x06).  
2. The peripheral can emulate SCSI devices in a manner transparent to the operating system.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_DDK_USB_SERIAL  

Allows extended peripheral drivers to access USBSerial DDK interfaces for developing USB Serial extended peripheral drivers.  

Supports the development of the following types of peripheral drivers:  
Peripherals connected to the host via USB bus, meeting the following criteria:  

1. The peripheral's `InterfaceClass` is Communication Device Class (0x02), and `InterfaceSubClass` follows the ACMSubClass model (0x02).  
2. The peripheral supports emulating traditional serial communication via USB interfaces.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_CUSTOM_RINGTONE  

Allows applications to access the ringtone library.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_STARTUPGUIDE  

Allows system applications to access general data and public events of the startup wizard application.  

Only applications on smartphones, tablets, and 2-in-1 devices can apply for this permission.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_DEVAUTH_CRED_MGR  

Allows system applications or system services to access the credential management module of the Device Mutual Trust Authentication SA.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_DEVAUTH_CRED_PRIVILEGE  

Allows system applications or system services to access the credential management and authentication modules of the Device Mutual Trust Authentication SA, enabling them to query and authenticate other business credentials.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_DEVAUTH_CRED_AUTH  

Allows system applications or system services to access the credential authentication module of the Device Mutual Trust Authentication SA.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ANTIFRAUD_DETECT  

Allows system applications to perform anti-fraud detection.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ANTIFRAUD_PICTURE_DETECT  

Allows system applications to perform face-swapping detection in images.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ANTIFRAUD_MODEL_DOWNLOAD  

Allows system applications to use model download-related interfaces.  

**Permission Level:** system_basic  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_APP_CLONE_DIR  

Allows system applications to access installation file paths cloned from other devices.  

**Permission Level:** system_core  

**Authorization Mode:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ACCESS_MEDIALIB_RESTORE  

Allows applications to mount media recovery paths.**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 17  

## ohos.permission.ACCESS_TRUST_LIST_OOBE_MANAGER  

Allows applications to manage the list of apps that can be launched during the out-of-box experience (OOBE) setup.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.GET_NETWORK_STATS  

Allows system applications to retrieve historical network traffic data.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 12  

**Change Log:** For API versions 10-11, ACL was disabled (false); starting from API 12, it was changed to true.  

## ohos.permission.READ_DLP_HIDE_SWITCH  

Allows system applications to read data from the screen peeking prompt database.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.WRITE_DLP_HIDE_SWITCH  

Allows system applications to write data to the screen peeking prompt database.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.INSTALL_PLUGIN_BUNDLE  

Allows applications to call interfaces for installing plugins.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 19  

## ohos.permission.ENTERPRISE_ACCESS_DLP_FILE  

Allows applications to call interfaces for accessing DLP files in the enterprise workspace.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** 2in1  

**Initial Version:** 20  

## ohos.permission.UNINSTALL_PLUGIN_BUNDLE  

Allows applications to call interfaces for uninstalling plugins.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 19  

## ohos.permission.GET_EDM_CONFIG  

Allows system applications to view industry-customized configuration files.  

Used to protect the visibility of industry-customized configurations, such as boot animations, boot logos, desktop layouts, wallpapers, etc.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.READ_DHA  

Allows applications to read device health attestation information.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.WRITE_DHA  

Allows applications to write device health attestation information.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.NOTIFY_DHA  

Allows applications to notify device health attestation events.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.CHANGE_DEFAULT_APPLICATION  

Allows applications to monitor changes to the "default application" settings.  

Users can set "default applications" in the system, such as specifying an app to open certain file types. When the "default application" changes, a corresponding event will be triggered.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 19  

## ohos.permission.SEND_NOTIFICATION_CROSS_USER  

Allows applications to send notifications to specified users in the system.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

## ohos.permission.ALLOW_ACCESS_TIPS  

Allows system applications to launch components provided by Tips.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 18  

### ohos.permission.UPDATE_FONT  

Allows applications to install and uninstall fonts.  

**Permission Level:** system_basic  

**Authorization Method:** system_grant  

**ACL Enabled:** true  

**Initial Version:** 19  

## ohos.permission.ACCESSIBILITY_EXTENSION_ABILITY  

Allows applications to query and manipulate on-screen components via accessibility service interfaces.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**Supported Devices:** General  

**ACL Enabled:** true  

**Initial Version:** 20  

## ohos.permission.READ_SOUND_RECORD_IN_FILE_MANAGER  

Allows applications to read audio recording files from the file manager directory.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** Phone | 2in1 | Tablet  

**Initial Version:** 20  

## ohos.permission.WRITE_SOUND_RECORD_IN_FILE_MANAGER  

Allows applications to write audio recording files to the file manager directory.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** Phone | 2in1 | Tablet  

**Initial Version:** 20  

## ohos.permission.SANDBOX_ACCESS_MANAGER  

Allows applications to access the sandbox directories of other applications.  

**Permission Level:** system_core  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Initial Version:** 17  

## ohos.permission.REQUEST_DISABLE_NOTIFICATION  

Allows background upload/download tasks of applications to be hidden from the notification bar.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** General  

**Initial Version:** 20  

## ohos.permission.RESTORE_APP  

Allows system applications to launch recovery dialogs for app restoration.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** Phone | 2in1 | Tablet  

**Initial Version:** 20  

## ohos.permission.ALLOW_IOURING  

Allows system applications to use io_uring-related system calls for asynchronous I/O operations.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** General  

**Initial Version:** 20  

## ohos.permission.NFC_NOTIFICATION  

Allows applications to publish NFC notification-related public events.  

**Permission Level:** system_basic  

**Authorization Method:** System Grant (system_grant)**ACL Enabled:** true  

**Supported Devices:** Phone  

**Initial Version:** 20  

## ohos.permission.kernel.ALLOW_APP_CODE_DECRYPT  

Allows system applications or system services to invoke kernel interfaces for code decryption.  

With this permission, applications or services can access kernel interfaces across processes to request decryption of encrypted code content, preventing unauthorized access and further protecting application code assets.  

**Permission Level:** system_core  

**Authorization Method:** System-granted (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** General  

**Initial Version:** 20  

## ohos.permission.GRANT_URI_PERMISSION_AS_CALLER  

Allows an application to grant URI access permissions to a target application on behalf of the caller.  

**Permission Level:** system_core  

**Authorization Method:** System-granted (system_grant)  

**ACL Enabled:** true  

**Supported Devices:** General  

**Initial Version:** 20