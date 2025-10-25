# Methods for Requesting Permissions

When an application accesses data or performs operations, it needs to evaluate whether the action requires relevant permissions. If the target permission is confirmed necessary, the application must declare the target permission in its installation package.

Each permission has different levels and authorization methods, and the way to request permissions also varies. Before requesting permissions, developers need to perform the following steps:

1. **Confirm the permission type** of the target permission. This can be verified by searching in the corresponding permission list page.
2. Follow the corresponding **operation path** to request the permission.

Applications can request permissions based on the target permission's scope of availability and authorization method by referring to the following operation paths.

## <!--Del-->Normal-Level<!--DelEnd--> Application Permission Request Methods

| Permission Type | Authorization Method | Operation Path |
| :-------------- | :------------------- | :------------- |
| [Open Permission (System Authorization)](./cj-permissions-for-all.md) | system_grant | [Declare Permission](./cj-declare-permissions.md) &gt; Access Interface |
| [Open Permission (User Authorization)](./cj-permissions-for-all-user.md) | user_grant | [Declare Permission](./cj-declare-permissions.md) &gt; [Request User Authorization](./cj-request-user-authorization.md) &gt; Access Interface |
| <!--Del-->[System Permission Allowed via ACL (System Authorization)](./cj-permissions-for-system-apps.md)<br><!--DelEnd-->[Restricted Open Permission](./cj-restricted-permissions.md) | system_grant | <!--RP1-->[Request Restricted Permission Usage](./cj-declare-permissions-in-acl.md)<!--RP1End--> &gt; [Declare Permission](./cj-declare-permissions.md) &gt; Access Interface |
| <!--Del-->[System Permission Allowed via ACL (User Authorization)](./cj-permissions-for-system-apps-user.md)<br><!--DelEnd-->[Restricted Open Permission](./cj-restricted-permissions.md) | user_grant | <!--RP1-->[Request Restricted Permission Usage](./cj-declare-permissions-in-acl.md)<!--RP1End--> &gt; [Declare Permission](./cj-declare-permissions.md) &gt; [Request User Authorization](./cj-request-user-authorization.md) &gt; Access Interface |

<!--Del-->
> **Note:**
>
> - If the ACL enablement (`system_basic` level permission) is set to `false`, normal-level applications cannot request this permission.
> - Currently, [cross-level permission requests via ACL](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing) can be completed using DevEco Studio, but this method is only for application debugging and cannot be used for releasing apps to the market. For commercial versions, apply for release certificates and Profile files in the corresponding app market.

## system_basic-Level Application Permission Request Methods

| Permission Level | Authorization Method | ACL Enablement | Operation Path |
| ---------------- | -------------------- | -------------- | -------------- |
| normal, system_basic | system_grant | - | [Declare Permission](./cj-declare-permissions.md) &gt; Access Interface |
| normal, system_basic | user_grant | - | [Declare Permission](./cj-declare-permissions.md) &gt; [Request User Authorization](./cj-request-user-authorization.md) &gt; Access Interface |
| system_core | system_grant | true | [Request Restricted Permission Usage](./cj-declare-permissions-in-acl.md) &gt; [Declare Permission](./cj-declare-permissions.md) &gt; Access Interface |
| system_core | user_grant | true | [Request Restricted Permission Usage](./cj-declare-permissions-in-acl.md) &gt; [Declare Permission](./cj-declare-permissions.md) &gt; [Request User Authorization](./cj-request-user-authorization.md) &gt; Access Interface |

If an application needs to declare its APL level as `system_basic` or higher, the `HarmonyAppProvision` configuration file must be modified during the development of the installation package. This file is located in the SDK directory at `Toolchains / _{Version} _/ lib / UnsgnedReleasedProfileTemplate.json`, and the application must be re-signed afterward.

**Modification Method:**

Below is an example of the `HarmonyAppProvision` configuration file. Modify the `"apl"` field under `"bundle-info"`.

```json
"bundle-info" : {
    // ...
    "apl": "system_basic",
    // ...
},
```

> **Note:**
>
> Directly modifying the `HarmonyAppProvision` configuration file is only for application debugging and cannot be used for releasing apps to the market. For commercial versions, apply for release certificates and Profile files in the corresponding app market.
<!--DelEnd-->