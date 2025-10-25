# System Application Permissions Not Available via ACL (System-Granted)

Before applying for target permissions, developers are advised to first understand the [application paths for different permissions](./cj-determine-application-mode.md). After gaining a basic understanding of the permission workflow, combine it with the specific descriptions of the following permission fields to determine whether the application can apply for the target permissions, thereby improving development efficiency.

> **Note:**
>
> - The following permissions are only available to applications with an APL level of system_basic or higher, and are not open to applications with an APL level of normal.
> - The authorization method for all the following permissions is system_grant.
> - These permissions cannot be applied for across levels via Access Control List (ACL).

For the application process, refer to [Choosing the Permission Application Method](./cj-determine-application-mode.md).

## ohos.permission.RECEIVER_STARTUP_COMPLETED

Allows an application to subscribe to boot completion broadcasts.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.SYSTEM_LIGHT_CONTROL

Allows control of system lights, including operations such as turning on/off.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.GET_ALL_APP_ACCOUNTS

Allows an application to query all application account information.

**Permission Level:** system_core

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.MANAGE_DEVICE_AUTH_CRED

Allows an application to call device authentication credential management application interfaces.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.ACCESS_AUTH_RESPOOL

Allows SAs to register authentication executors.

**Permission Level:** system_core

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.READ_ACCESSIBILITY_CONFIG

Allows an application to read accessibility configuration information.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.WRITE_APP_PUSH_DATA

Allows push services to write data into applications.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.READ_APP_PUSH_DATA

Allows push services to read data stored by push services in applications.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.NETSYS_INTERNAL

Allows SA services to call network management netsys interfaces for functions such as network diagnostics, WiFi, NIC monitoring, and iptables configuration.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.DISTRIBUTED_SOFTBUS_CENTER

Allows networking between different devices.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.RESTRICT_APPLICATION_ACTIVE

Allows the standby endurance component to publish a custom network restriction event.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.CONNECT_CELLULAR_CALL_SERVICE

Allows system services to access cellular call SAs.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.CONNECT_IMS_SERVICE

Allows system services to access IMS SAs.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.ENFORCE_USER_IDM

Allows SAs to delete IAM user information without a token.

**Permission Level:** system_core

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.WRITE_ACCESSIBILITY_CONFIG

Allows an application to set accessibility configuration information.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.ENABLE_DISTRIBUTED_HARDWARE

Allows system services to enable distributed hardware resources.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.ACCESS_SUPER_HUB

Allows an application to launch the "Transfer Station."

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 12

## ohos.permission.CALLED_UIEXTENSION_ON_LOCK_SCREEN

Allows UIExtensionAbility to display on top of the lock screen.

**Permission Level:** system_core

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 14

## ohos.permission.USE_USER_ACCESS_MANAGER

Allows an application to query and configure user identity authentication policies and verify user identity authentication results.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 18

## ohos.permission.SET_LAUNCH_REASON_MESSAGE

Allows system applications to set launch reasons when launching other applications.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 18

## ohos.permission.ACCESS_USER_ACCOUNT_INFO

Allows system applications to obtain data provided by accounts.

**Permission Level:** system_basic

**Authorization Method:** system_grant

**ACL Enabled:** false

**Initial Version:** 18