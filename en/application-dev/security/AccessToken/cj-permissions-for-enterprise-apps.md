# Available Permissions for Enterprise Applications

The following permissions are available for <!--Del-->system applications and<!--DelEnd--> enterprise applications, which include general enterprise applications and MDM (Mobile Device Management) applications.

Enterprise applications have the following characteristics:

- They run exclusively on enterprise-customized devices and do not operate on consumer devices.

- Their distribution types are `enterprise_normal` (general enterprise applications) and `enterprise_mdm` (MDM applications).

<!--RP1--><!--RP1End-->

For enterprise applications, refer to [Declaring Permissions](./cj-declare-permissions.md) to request the following permissions.

> **Note:**
>
> The following permissions do not support automatic signing. Therefore, during both debugging and release phases, manual signing must be completed by following the steps in [Manual Signing](https://developer.huawei.com/consumer/en/doc/harmonyos-guides/ide-signing#section297715173233).

## ohos.permission.SET_FILE_GUARD_POLICY

Allows an application to issue file control policies.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, its permission level was system_core and was only available to MDM applications. Starting from API 14, the permission level was changed to system_basic, and the development scope was expanded to general enterprise applications.

## ohos.permission.FILE_GUARD_MANAGER

Allows an application to scan public directories and set file extended attributes.

Current extended attributes include file security levels and file labels.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, its permission level was system_core and was only available to MDM applications. Starting from API 14, the permission level was changed to system_basic, and the development scope was expanded to general enterprise applications.

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

Allows an application to interact across local system accounts.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to general enterprise applications.

## ohos.permission.GET_RUNNING_INFO

Allows an application to obtain runtime information.

This includes information about other applications' runtime states, such as Ability, Extension, and Application details.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to general enterprise applications.

## ohos.permission.RUNNING_STATE_OBSERVER

Allows an application to monitor application states.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to general enterprise applications.

## ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

Allows querying an application's basic information and other sensitive data.

Such as the application package name, version, etc.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to general enterprise applications.

## ohos.permission.GET_WIFI_CONFIG

Allows an application to obtain Wi-Fi configuration information.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**Supported Devices:** PC/2in1

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded from system applications to general enterprise applications.

## ohos.permission.SET_WIFI_CONFIG

Allows an application to configure Wi-Fi information.

This permission enables adding, deleting, and modifying Wi-Fi configurations.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to general enterprise applications.

## ohos.permission.GET_DOMAIN_ACCOUNTS

Allows an application to query domain account information.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded to general enterprise applications.

## ohos.permission.QUERY_AUDIT_EVENT

Allows enterprise security applications to query security audit events.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to MDM applications. Starting from API 14, the availability scope was expanded from MDM applications to general enterprise applications.

## ohos.permission.KILL_APP_PROCESSES

Allows system applications to terminate other application processes.

With this permission, an application can terminate other running applications, enabling necessary process management and control within the system.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-13, this permission was only available to system applications. Starting from API 14, the availability scope was expanded from system applications to general enterprise applications.

### ohos.permission.SET_TELEPHONY_ESIM_STATE_OPEN

Allows system applications and carrier applications to set eSIM nicknames and activate eSIM.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 14

**Change History:** In API 13, the permission level was normal. Starting from API 14, the permission level was changed to system_basic.

## ohos.permission.MANAGE_ENTERPRISE_WIFI_CONNECTION

Allows an application to manage Wi-Fi connections.

With this permission, operations such as enabling/disabling, connecting, and disconnecting Wi-Fi can be performed.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

**ACL Enabled:** true

**Initial Version:** 15

## ohos.permission.ACCESS_ENTERPRISE_USER_TRUSTED_CERT

Allows an application to manage user CA certificates on enterprise devices.

When enterprise applications use private CA certificates to authenticate enterprise servers on enterprise devices, this permission allows the installation and management of such certificates.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_NET_FIREWALL

Allows system applications to configure firewall rules.

Currently, only applications on 2in1 devices can request this permission.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to general enterprise applications.

## ohos.permission.GET_NET_FIREWALL

Allows system applications to query firewall rules and interception logs.

Currently, only applications on 2in1 devices can request this permission.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 12

**Change History:** From API 12-14, this permission was only available to system applications. Starting from API 15, the availability scope was expanded to general enterprise applications.

## ohos.permission.GET_DOMAIN_ACCOUNT_SERVER_CONFIGS

Allows an application to obtain domain account server configurations.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_DOMAIN_ACCOUNT_SERVER_CONFIGS

Allows an application to manage domain account server configurations.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.MANAGE_DOMAIN_ACCOUNTS

Allows an application to manage domain accounts.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.GET_SIGNATURE_INFO

Allows an application to obtain application package signature information.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.VISIBLE_WINDOW_INFO

Allows an application to obtain visible window information on the current screen.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Initial Version:** 18

## ohos.permission.SUPPORT_APP_SERVICE_EXTENSION

Allows an application to be launched as an AppServiceExtension.

With this permission, an application can be launched or connected as an AppServiceExtension by the same application or applications listed in the "appidentifierAllowList" configuration.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Supported Devices:** PC/2in1

**Initial Version:** 20

## ohos.permission.ENTERPRISE_MANAGE_EAP

Allows enterprise network security software to add private information to EAP packets.

With this permission, enterprise network security software can obtain 802.1x packets and add information to meet customized authentication requirements.

**Permission Level:** system_basic

**Authorization Mode:** system_grant

<!--Del-->
**ACL Enabled:** true<!--DelEnd-->

**Supported Devices:** PC/2in1

**Initial Version:** 20