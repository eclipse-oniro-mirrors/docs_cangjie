# Publishing a Text Notification

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Text notifications are mainly used to send short messages and prompt messages. Currently, the basic text type is supported.

**Table 1** Content types of a basic notification

| Type | Description |
| ---- | ---- |
| NotificationContentBasicText | Basic text type. |

## Available APIs

The following table describes the notification publishing APIs. Details of a published notification can be specified through the [NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest) parameter, including the notification content, notification ID, notification slot type, and notification label.

| **API** | **Description** |
| -------- | -------- |
| publish(request: [NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest), callback: AsyncCallback\<Unit>): Unit | Publishes a notification. |

## How to Develop

For details about the APIs, see [Notification Management API Reference](../reference/NotificationKit/cj-apis-notification-manager.md).

1. Import the modules.

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Create a [NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest) object and publish the notification.

    A basic text notification consists of a title, text content, and additional text. For details, see [NotificationBasicContent](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationbasiccontent).

    <!-- compile -->

    ```cangjie
    // index.cj

    let basicContent = NotificationBasicContent("test_title", "test_text")
    basicContent.additionalText = Some("test_additionalText")
    let content = NotificationContent(ContentType.NotificationContentBasicText) // Basic text notification
    content.normal = Some(basicContent)
    let request = NotificationRequest(content)
    request.id = Some(1)
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "Failed to publish notification. Code is ${e.code}, message is ${e.message}")
        } else {
            Hilog.info(0, "test", "Succeeded in publishing notification.")
        }
    }
    publish(request, callback)
    ```

3. (Optional) Update an existing notification.

    When the ID and label of a newly published notification are the same as those of an existing notification, the new notification replaces the original one, implementing notification update. For example, to update the title, create a [NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest) with the same ID and call **publish** again.

    <!-- compile -->

    ```cangjie
    // index.cj

    let newBasicContent = NotificationBasicContent("test_title_new", "test_text_new")
    let newContent = NotificationContent(ContentType.NotificationContentBasicText)
    newContent.normal = Some(newBasicContent)
    let newRequest = NotificationRequest(newContent)
    newRequest.id = Some(1) // The ID is the same as that of the published notification, implementing notification update.
    let updateCallback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "Failed to update notification. Code is ${e.code}, message is ${e.message}")
        } else {
            Hilog.info(0, "test", "Succeeded in updating notification.")
        }
    }
    publish(newRequest, updateCallback)
    ```
