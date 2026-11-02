# Requesting Notification Authorization

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

An application must obtain user authorization before sending notifications. Before publishing a notification, call [requestEnableNotification()](../reference/NotificationKit/cj-apis-notification-manager.md#func-requestenablenotificationuiabilitycontext-asynccallbackunit) to display a dialog box asking the user whether to allow the application to send notifications. After the user rejects the authorization, calling this API again returns error code 1600004, indicating that the notification switch is off.

## Available APIs

For API details, see [ohos.notification_manager (Notification Management)](../reference/NotificationKit/cj-apis-notification-manager.md).

**Table 1** Notification authorization APIs

| **API** | **Description** |
| -------- | -------- |
| isNotificationEnabledSync(): Bool | Synchronously queries whether notification is authorized. |
| requestEnableNotification(context: [UIAbilityContext](../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext), callback: AsyncCallback\<Unit>): Unit | Requests permission to send notifications. The first call displays a dialog box for the user to choose. |

## How to Develop

1. Import the modules.

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Query the notification authorization status of the current application.

    <!-- compile -->

    ```cangjie
    // index.cj

    let enabled = isNotificationEnabledSync()
    Hilog.info(0, "test", "isNotificationEnabledSync success, enabled: ${enabled}")
    ```

3. Display the notification dialog box to request notification authorization from the user.

    Before publishing a notification, the application can call [requestEnableNotification](../reference/NotificationKit/cj-apis-notification-manager.md#func-requestenablenotificationuiabilitycontext-asynccallbackunit) to display a dialog box asking the user whether to allow the application to send notifications. You can determine whether the user has granted the authorization based on the error code of this API. If the error code returned is 1600004, the authorization is rejected.

    <!-- compile -->

    ```cangjie
    // index.cj

    let ctx = Global.abilityContext // The template must be configured manually to obtain the Context.
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            if (e.code == 1600004) {
                Hilog.error(0, "test", "requestEnableNotification refused, code is ${e.code}, message is ${e.message}")
            } else {
                Hilog.error(0, "test", "requestEnableNotification failed, code is ${e.code}, message is ${e.message}")
            }
        } else {
            Hilog.info(0, "test", "requestEnableNotification success")
        }
    }
    requestEnableNotification(ctx, callback)
    ```

    > **NOTE:**
    >
    > This API can be called only after the application UI is loaded, that is, after `loadContent` is successfully called.
