# Available Permissions for Enterprise Applications

The following permissions are available for <!--Del-->system applications and<!--DelEnd--> enterprise applications, which include regular enterprise applications and MDM (Mobile Device Management) applications.

Enterprise applications have the following characteristics:

- They run only on enterprise-customized devices and will not operate on regular consumer devices.

- Their distribution types are `enterprise_normal` (regular enterprise applications) and `enterprise_mdm` (MDM applications).

<!--RP1--><!--RP1End-->

For enterprise applications, refer to [Declaring Permissions](./cj-declare-permissions.md) to request the following permissions.

> **Note:**
>
> The following permissions do not support automatic signing. Therefore, during both debugging and release phases, manual signing must be completed by following the steps in [Manual Signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

## ohos.permission.SET_FILE_GUARD_POLICY

Allows applications to issue file control policies.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, the permission level was system_core and was only available to MDM applications. Starting from API 14, the permission level was changed to system_basic, and the development scope was expanded to include regular enterprise applications.

## ohos.permission.FILE_GUARD_MANAGER

Allows applications to scan public directories and set file extended attributes.

Current extended attributes include file security levels and file labels.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, the permission level was system_core and was only available to MDM applications. Starting from API 14, the permission level was changed to system_basic, and the development scope was expanded to include regular enterprise applications.

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

Allows applications to interact across local system accounts.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to regular enterprise applications.

## ohos.permission.GET_RUNNING_INFO

Allows applications to obtain runtime information.

This includes information about other applications' runtime states, such as Ability, Extension, and Application details.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to regular enterprise applications.

## ohos.permission.RUNNING_STATE_OBSERVER

Allows applications to monitor application states.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to regular enterprise applications.

## ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

Allows querying basic and other sensitive information about applications.

This includes details such as package names and versions.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to regular enterprise applications.

## ohos.permission.GET_WIFI_CONFIG

Allows applications to obtain Wi-Fi configuration information.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**Supported Devices:** 2in1

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded from system applications to regular enterprise applications.

## ohos.permission.SET_WIFI_CONFIG

Allows applications to configure Wi-Fi information.

This includes adding, deleting, and modifying Wi-Fi configurations.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to regular enterprise applications.

## ohos.permission.GET_DOMAIN_ACCOUNTS

Allows applications to query domain account information.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded to regular enterprise applications.

## ohos.permission.QUERY_AUDIT_EVENT

Allows enterprise security applications to query security audit events.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to MDM applications. Starting from API 14, the availability scope was expanded from MDM applications to regular enterprise applications.

## ohos.permission.KILL_APP_PROCESSES

Allows system applications to terminate other application processes.

With this permission, applications can terminate other running applications, enabling necessary management and control of system processes.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to regular enterprise applications.

### ohos.permission.SET_TELEPHONY_ESIM_STATE_OPEN

Allows system applications and carrier applications to set eSIM nicknames and activate eSIM.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 14

**Change History:** In API 13, the permission level was normal. Starting from API 14, the permission level was changed to system_basic.

## ohos.permission.MANAGE_ENTERPRISE_WIFI_CONNECTION

Allows applications to manage Wi-Fi connections.

With this permission, applications can perform operations such as enabling/disabling, connecting, and disconnecting Wi-Fi.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

**ACL Enabled:** true

**Initial Version:** 15

## ohos.permission.ACCESS_ENTERPRISE_USER_TRUSTED_CERT

Allows applications to manage user CA certificates on enterprise devices.

When enterprise applications use private CA certificates to authenticate enterprise servers on enterprise devices, this permission enables them to install private CA certificates onto the devices and manage these certificates.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_NET_FIREWALL

Allows system applications to configure firewall rules.

Currently, only applications on 2in1 devices can request this permission.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to regular enterprise applications.

## ohos.permission.GET_NET_FIREWALL

Allows system applications to query firewall rules and interception records.

Currently, only applications on 2in1 devices can request this permission.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to regular enterprise applications.

## ohos.permission.GET_DOMAIN_ACCOUNT_SERVER_CONFIGS

Allows applications to obtain domain account server configurations.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_DOMAIN_ACCOUNT_SERVER_CONFIGS

Allows applications to manage domain account server configurations.

**Permission Level:** system_basic

**Authorization Method:** System-granted (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_DOMAIN_ACCOUNTSAllow applications to manage domain accounts.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.GET_SIGNATURE_INFO

Allow applications to obtain signature information of application packages.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.VISIBLE_WINDOW_INFO

Allow applications to obtain visible window information of the current screen.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.SUPPORT_APP_SERVICE_EXTENSION

Allow applications to be launched as AppServiceExtension.

After obtaining this permission, the application can be launched or connected as an AppServiceExtension by applications within the same package or those listed in the "appidentifierAllowList" configuration.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Supported Devices:** 2in1

**Initial Version:** 20

## ohos.permission.ENTERPRISE_MANAGE_EAP

Allow enterprise network security software to add private information in EAP packets.

After obtaining this permission, enterprise network security software can acquire 802.1x packets and add information to meet customized authentication requirements.

**Permission Level:** system_basic

**Authorization Method:** System grant (system_grant)

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Supported Devices:** 2in1

**Initial Version:** 20