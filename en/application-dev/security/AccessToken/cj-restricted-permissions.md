# Restricted Open Permissions

## Application Method

<!--RP1-->

The following permissions are available to normal applications, but require cross-level application through [Access Control List (ACL)](./cj-app-permission-mgmt-overview.md#Basic-Concepts-in-Permission-Mechanism).

Applications with a normal level need to declare their APL level as system_basic or higher. When developing the application installation package, modify the HarmonyAppProvision configuration file located in the SDK directory at `Toolchains / _{Version} _/ lib / UnsgnedReleasedProfileTemplate.json`, and then re-sign the application.

**Modification Method:**

Below is an example of the HarmonyAppProvision configuration file. Modify the "apl" field under "bundle-info".

```json
"bundle-info" : {
    // ...
    "apl": "system_basic",
    // ...
},
```

> **Note:**
>
> Directly modifying the HarmonyAppProvision configuration file is only for application debugging and should not be used for publishing to app markets. For commercial versions, apply for release certificates and Profile files through the respective app market.

<!--RP1End-->

## Permission List

### ohos.permission.SYSTEM_FLOAT_WINDOW

Allows applications to use floating window capabilities.

<!--RP25--><!--RP25End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.READ_CONTACTS

Allows applications to read contact data.

<!--RP33--><!--RP33End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.WRITE_CONTACTS

Allows applications to add, remove, or modify contact data.

<!--RP34--><!--RP34End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.READ_AUDIO

Allows reading audio files from user public directories.

<!--RP26--><!--RP26End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.WRITE_AUDIO

Allows modifying audio files in user public directories.

<!--RP28--><!--RP28End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.READ_IMAGEVIDEO

Allows reading image or video files from user public directories.

<!--RP27--><!--RP27End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.WRITE_IMAGEVIDEO

Allows modifying image or video files in user public directories.

<!--RP29--><!--RP29End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.READ_WRITE_DESKTOP_DIRECTORY

Allows applications to access the Desktop directory and its subdirectories in public directories.

<!--RP15-->  
Currently, only applications on 2-in-1 devices and tablets can apply for this permission.  
<!--RP15End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.ACCESS_DDK_USB

Allows extended peripheral drivers to access USB DDK interfaces for developing USB bus peripheral drivers.

<!--RP31--><!--RP31End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.ACCESS_DDK_HID

Allows extended peripheral drivers to access HID DDK interfaces for developing HID-class peripheral drivers.

<!--RP30--><!--RP30End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.READ_PASTEBOARD

Allows applications to read the clipboard.

<!--RP32--><!--RP32End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.FILE_ACCESS_PERSIST

Allows applications to persistently access file URIs.

<!--RP18--><!--RP18End-->

**Permission Level:** normal  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.INTERCEPT_INPUT_EVENT

Allows applications to intercept input events.

<!--RP24--><!--RP24End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.INPUT_MONITORING

Allows applications to monitor input events.

<!--RP23--><!--RP23End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 7  

### ohos.permission.SHORT_TERM_WRITE_IMAGEVIDEO

Allows applications to save images or videos to user public directories.

After obtaining this permission, applications receive temporary authorization (up to 30 minutes) to save images/videos. If exceeded, a re-confirmation dialog will appear.

<!--RP21--><!--RP21End-->

**Permission Level:** system_basic  
**Authorization Method:** User-granted (user_grant)  
**Initial Version:** 12  

### ohos.permission.READ_WRITE_USER_FILE

Allows applications to access and modify files in user directories.

<!--RP19-->  
Currently, only applications on 2-in-1 devices can apply for this permission.  
<!--RP19End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.READ_WRITE_USB_DEV

Allows applications to connect to devices and read/write via USB debugging.

<!--RP20-->  
Currently, only applications on 2-in-1 devices can apply for this permission.  
<!--RP20End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.GET_WIFI_PEERS_MAC

Allows applications to obtain the MAC addresses of peer Wi-Fi devices.

Required when retrieving peer device MAC addresses from Wi-Fi scan results.

<!--RP14--><!--RP14End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

**Change History:** API 12: Permission level was system_core; from API 15 onward, changed to system_basic and opened to normal applications.

### ohos.permission.kernel.DISABLE_CODE_MEMORY_PROTECTION

Allows applications to disable runtime code integrity protection for themselves.

<!--RP11-->  
For applications developed using cross-platform frameworks, exempting runtime code integrity protection. Currently, only tablet and 2-in-1 device applications can apply.  
<!--RP11End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.kernel.ALLOW_WRITABLE_CODE_MEMORY

Allows applications to request writable and executable anonymous memory.

<!--RP10-->  
For applications developed using cross-platform frameworks, requesting writable/executable anonymous memory. Currently, only tablet and 2-in-1 device applications can apply.  
<!--RP10End-->

**Permission Level:** system_basic  
**Authorization Method:** System-granted (system_grant)  
**Initial Version:** 12  

### ohos.permission.kernel.ALLOW_EXECUTABLE_FORT_MEMORY

Allows the system JS engine to request anonymous executable memory with MAP_FORT flags.

After obtaining this permission, the system engine can request MAP_FORT anonymous executable memory for just-in-time compilation, improving formal execution efficiency.

<!--RP13--><!--RP13End-->

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)
  
**Initial Version:** 12

### ohos.permission.MANAGE_PASTEBOARD_APP_SHARE_OPTION

Allows applications to set or remove the paste scope of clipboard data.

<!--RP16--><!--RP16End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.MANAGE_UDMF_APP_SHARE_OPTION

Allows applications to set or remove the data sharing scope when using UDMF.

<!--RP17--><!--RP17End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.ACCESS_DISK_PHY_INFO

Allows applications to access hardware information of storage disks.

<!--RP3--><!--RP3End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.PRELOAD_FILE

Allows applications to preload files to improve file opening speed.

<!--RP9--><!--RP9End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.SET_PAC_URL

Allows applications to configure the Proxy Auto-Configuration (PAC) script URL.

After configuration, other applications can read and parse this script to determine whether to use a proxy based on the parsing results.

<!--RP4--><!--RP4End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.PERSONAL_MANAGE_RESTRICTIONS

Allows device management applications to manage personal device restriction policies.

<!--RP7--><!--RP7End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.START_PROVISIONING_MESSAGE

Allows applications to initiate device management provisioning workflows, activating them as personal device management applications.

<!--RP8--><!--RP8End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.USE_FRAUD_CALL_LOG_PICKER

Allows applications to use the fraudulent call log picker to access call log content.

<!--RP5--><!--RP5End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.USE_FRAUD_MESSAGES_PICKER

Allows applications to use the fraudulent SMS picker to access SMS content.

<!--RP6--><!--RP6End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.PERSISTENT_BLUETOOTH_PEERS_MAC

Allows applications to persist virtual random addresses mapped to peer Bluetooth device MAC addresses.

Obtained via BLE scanning, BR scanning, or connection monitoring, this permission enables long-term retention of virtual random addresses, unaffected by Bluetooth toggling or reboots.

<!--RP36--><!--RP36End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.ACCESS_VIRTUAL_SCREEN

Allows applications to manage virtual screens.

Authorized applications can invoke virtual screen APIs to create, use, and destroy virtual screens.

<!--RP37--><!--RP37End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.MANAGE_APN_SETTING

Allows applications to read or configure APN (Access Point Name) information.

<!--RP38--><!--RP38End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.GET_WIFI_LOCAL_MAC

Allows applications to retrieve the MAC address of local Wi-Fi devices.

<!--RP43--><!--RP43End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

**Change History:** From API 12-15, this permission was restricted to system apps; starting from API 16, it became available to regular apps on 2-in-1 devices while remaining system-app-only on other devices.

### ohos.permission.kernel.ALLOW_USE_JITFORT_INTERFACE

Allows applications to invoke JITFort interfaces for updating MAP_FORT memory content.

<!--RP12--><!--RP12End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.kernel.DISABLE_GOTPLT_RO_PROTECTION

Allows applications to disable read-only protection for the .got.plt section within processes.

<!--RP22--><!--RP22End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.USE_FRAUD_APP_PICKER

Allows applications to use the fraudulent app picker to access application information.

<!--RP2--><!--RP2End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.kernel.SUPPORT_PLUGIN

Allows host applications to install plugins.

<!--RP35--><!--RP35End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.CUSTOM_SANDBOX

Allows applications to switch sandbox types to dynamic sandbox.

<!--RP39--><!--RP39End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 12

### ohos.permission.MANAGE_SCREEN_TIME_GUARD

Allows applications to invoke screen time guard APIs for usage restrictions, app access control, and time management.

<!--RP40--><!--RP40End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Initial Version:** 20

### ohos.permission.CUSTOMIZE_SAVE_BUTTON

Allows applications to customize save button icons and text.

<!--RP41--><!--RP41End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Supported Devices:** Phone | 2-in-1 | Tablet

**Initial Version:** 20

### ohos.permission.GET_ABILITY_INFO

Allows applications to query Ability information based on URIs.

<!--RP42--><!--RP42End-->

**Permission Level:** system_basic

**Authorization Mode:** System-granted (system_grant)

**Supported Devices:** 2-in-1

**Initial Version:** 20