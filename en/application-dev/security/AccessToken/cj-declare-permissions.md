# Declaring Permissions

When an application requests permissions, it must declare each required permission in the project configuration file; otherwise, the application will not be granted authorization.

## Declaring Permissions in the Configuration File

Applications must declare permissions in the `requestPermissions` tag of the `module.json5` configuration file.

| Attribute | Description | Data Type | Valid Values |
| :-------- | :-------- | :-------- | :-------- |
| `name` | The name of the permission to be used. | String | **Required**. Must be a system-defined permission. For valid values, refer to the [Application Permissions List](./cj-permissions-for-all.md). |
| `reason` | The reason for requesting the permission. | String | **Optional**. This field is used for app store review. It is mandatory when requesting a `user_grant` permission and requires multilingual adaptation.<br>Use string resource references in the format `$string: ***`.<br>Refer to the [Content Guidelines for Permission Usage Reasons](#content-guidelines-for-permission-usage-reasons). |
| `usedScene` | The scenario in which the permission is used. This field is used for app store review. Includes two subfields: `abilities` and `when`.<br/>- `abilities`: The names of UIAbility or ExtensionAbility components that use the permission.<br/>- `when`: The timing of invocation. | Object | `usedScene` is **required**.<br/>- `abilities`: **Optional**. Can be configured as a string array of multiple UIAbility or ExtensionAbility names.<br/>- `when`: **Optional**. If configured, only fixed values `inuse` (during use) or `always` (always) are allowed. Cannot be empty.<br/>Recommended for `user_grant` permissions. |

> **Note:**
>
> Permissions declared in submodules do not need to be repeated in the main project. Permissions will take effect across the entire application.

## Declaration Example

> **Note:**
>
> The permissions `"ohos.permission.PERMISSION1"` and `"ohos.permission.PERMISSION2"` are for illustrative purposes only and do not exist. Developers should fill in the corresponding attributes according to actual needs, following the requirements in the table above.

```json
// src/main/resources/base/element/string.json
{
  "string": [
    // ...
    {
      "name": "reason",
      "value": "reason_for_permission"
    }
  ]
}
```

```json
// src/main/module.json5
{
  "module" : {
    // ...
    "requestPermissions":[
      {
        "name" : "ohos.permission.PERMISSION1",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when":"inuse"
        }
      },
      {
        "name" : "ohos.permission.PERMISSION2",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when":"always"
        }
      }
    ]
  }
}
```

## Content Guidelines for Permission Usage Reasons

When requesting a `user_grant` permission, the `reason` field (the reason for requesting the permission) is mandatory. Developers must configure each permission to be used in the application configuration file.

However, when actually prompting the user for authorization, `user_grant` permissions will be requested in the form of [permission groups](./cj-app-permission-mgmt-overview.md#permission-groups-and-sub-permissions). For the currently supported permission groups, refer to the [Application Permission Group List](./cj-app-permission-group-list.md).

### Writing Guidelines and Recommendations for the `reason` Field

<!--RP1-->

1. Keep sentences concise and avoid unnecessary punctuation.

   **Recommended Phrase:** Used for [purpose].

   **Example:** Used for scanning QR codes and taking photos.

2. The description string should ideally be fewer than 72 characters (or 36 Chinese characters, approximately two lines in the UI). Do not exceed 256 characters to ensure a good multilingual adaptation experience.

3. If left blank, the default request reason will be displayed.

<!--RP1End-->

### Display Methods for Permission Usage Reasons

Permission usage reasons are displayed in two contexts: the authorization pop-up interface and the "Settings" interface. The "Settings" path is: Settings > Privacy > Permission Management > [App Name] > Permission Details.

1. For permissions in the "Phone, Messages, Calendar, Contacts, Call Log" permission groups, compliance with MIIT requirements mandates displaying the specific sub-permission content and purpose.

    **Phrase:** Includes sub-permission A and sub-permission B, used for [purpose].

    **Example:** Used for obtaining call status and mobile network information, for security operations and billing statistics.

2. For permissions in other permission groups, the system will use the usage reason of the first sub-permission currently requested within the group as the display reason for the entire permission group. The order within the group is fixed according to the permission group array sequence in permission management.

    Example: Permission Group A = {Permission A, Permission B, Permission C}; the requested permissions are {Permission C, Permission B}. The interface will display the usage reason for Permission B.