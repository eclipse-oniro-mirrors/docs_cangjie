# System Application Available Permissions (User Authorization)

Before applying for target permissions, developers are advised to first understand the [application paths for different permissions](./cj-determine-application-mode.md). After gaining a basic understanding of the permission workflow, combine it with the specific descriptions of the following permission fields to determine whether the application can apply for the target permissions, thereby improving development efficiency.

> **Note:**
>
> - The following permissions are only available to applications with an APL level of system_basic or higher, and are not available to applications with an APL level of normal.
> - The authorization method for the following permissions is user_grant (user authorization).
> - The following permissions can be applied for across levels via [Access Control List (ACL)](./cj-app-permission-mgmt-overview.md#basic-concepts-in-permission-mechanism).

For the application process, refer to [Choosing the Permission Application Method](./cj-determine-application-mode.md).

## ohos.permission.READ_WHOLE_CALENDAR

Allows an application to read all calendar information.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.WRITE_WHOLE_CALENDAR

Allows an application to add, remove, or modify all calendar events.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.GET_INSTALLED_BUNDLE_LIST

Allows an application to read the list of installed applications.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.ANSWER_CALL

Allows an application to answer incoming calls.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.MANAGE_VOICEMAIL

Allows an application to leave messages in voicemail.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.READ_CALL_LOG

Allows an application to read call logs.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.READ_CELL_MESSAGES

Allows an application to read cell broadcast messages received by the device.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.READ_MESSAGES

Allows an application to read SMS messages.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECEIVE_MMS

Allows an application to receive and process MMS messages.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECEIVE_SMS

Allows an application to receive and process SMS messages.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.RECEIVE_WAP_MESSAGES

Allows an application to receive and process WAP messages.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.SEND_MESSAGES

Allows an application to send SMS messages.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12

## ohos.permission.WRITE_CALL_LOG

Allows an application to add, remove, or modify call logs.

**Permission Level:** system_basic

**Authorization Method:** user_grant

**ACL Enabled:** true

**Initial Version:** 12