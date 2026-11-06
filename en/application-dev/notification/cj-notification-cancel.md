# Canceling a Notification

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

When the user taps a notification and the application is launched to the foreground, the application can cancel the published notification.

When the user taps the desktop icon to launch the application to the foreground, after the user views the in-application messages, the application can cancel the notifications of these viewed messages.

For example:

Scenario 1: The user receives an IM message from a friend and taps the notification to enter the application to view the message. The application can then cancel the related notification reminder.

Scenario 2: The user receives an IM message from a friend and enters the application from the desktop icon to view the message. The application can then cancel the related notification reminder.

## Available APIs

The notification canceling API is as follows. For API details, see [ohos.notification_manager (Notification Management)](../reference/NotificationKit/cj-apis-notification-manager.md).

| **API** | **Description** |
| -------- | -------- |
| cancelAll(callback: AsyncCallback\<Unit>): Unit | Cancels all notifications published by this application. |

## How to Develop

This section uses canceling a `text notification` as an example. The canceling operations of other notification types are similar.

1. Import the modules.

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Publish a notification.

    For details, see [Publishing a Text Notification](./cj-text-notification.md).

3. Cancel the notification.

    <!-- compile -->

    ```cangjie
    // index.cj

    // After the application is launched to the foreground and the message is viewed, call this API to cancel all notifications published by this application.
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "Failed to cancel notification. Code is ${e.code}, message is ${e.message}")
        } else {
            Hilog.info(0, "test", "Succeeded in canceling notification.")
        }
    }
    cancelAll(callback)
    ```
