# Managing the Notification Badge

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

For unread notifications, the system provides a badge setting API to display the number of unread notifications on the badge in the upper right corner of the desktop icon.

When a notification is added, the number of unread notifications displayed on the badge needs to increase.

After a notification is viewed, the number of unread notifications displayed on the badge needs to decrease. When there are no unread notifications, the badge is not displayed.

## Available APIs

When the badge count is less than or equal to 0, the badge is cleared. When the count is greater than 99, the notification badge displays **99+**.

- Both increasing and decreasing the badge count are performed by calling the [setBadgeNumber()](../reference/NotificationKit/cj-apis-notification-manager.md#func-setbadgenumberint32-asynccallbackunit) API, and the desktop displays the badge according to the set count.

  | **API** | **Description** |
  | -------- | -------- |
  | setBadgeNumber(badgeNumber: Int32, callback: AsyncCallback\<Unit>): Unit | Sets the number count on the badge. |

## How to Develop

For details about the APIs, see [Notification Management API Reference](../reference/NotificationKit/cj-apis-notification-manager.md).

1. Import the modules.

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. Increase the badge count.

    After publishing a new notification, call [setBadgeNumber](../reference/NotificationKit/cj-apis-notification-manager.md#func-setbadgenumberint32-asynccallbackunit) to set the badge count.

    <!-- compile -->

    ```cangjie
    // index.cj

    let badgeNumber: Int32 = 9
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "Failed to set badge number. Code is ${e.code}, message is ${e.message}")
        } else {
            Hilog.info(0, "test", "Succeeded in setting badge number.")
        }
    }
    setBadgeNumber(badgeNumber, callback)
    ```

3. Decrease the badge count.

    After a notification is viewed, the application needs to call this API to set the number of remaining unread notifications, and the desktop refreshes the badge.

    <!-- compile -->

    ```cangjie
    // index.cj

    let badgeNumber: Int32 = 8
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "Failed to set badge number. Code is ${e.code}, message is ${e.message}")
        } else {
            Hilog.info(0, "test", "Succeeded in setting badge number.")
        }
    }
    setBadgeNumber(badgeNumber, callback)
    ```

## FAQs

**setBadgeNumber** is an asynchronous API. When **setBadgeNumber** is used to set badges consecutively, you should not set the value until the previous setting is complete, ensuring that the execution sequence meets the expectation.

- Negative example

    Each API call is independent and has no dependency on others, so the calling sequence cannot be guaranteed during actual execution.

    The sample code is as follows:

    <!-- compile -->

    ```cangjie
    // index.cj

    func makeCallback(tag: String): AsyncCallback<Unit> {
        return {
            err: Option<BusinessException>, data: Option<Unit> =>
            if (let Some(e) <- err) {
                Hilog.error(0, "test", "${tag} failed. Code is ${e.code}, message is ${e.message}")
            } else {
                Hilog.info(0, "test", "${tag} success.")
            }
        }
    }

    setBadgeNumber(10, makeCallback("setBadgeNumber 10"))
    setBadgeNumber(11, makeCallback("setBadgeNumber 11")) // This setting cannot be guaranteed to execute after the previous setting is complete.
    ```

- Positive example

    Dependencies existing between multiple API callings ensures that the next setting can be performed only after the previous setting is complete.

    The sample code is as follows:

    <!-- compile -->

    ```cangjie
    // index.cj

    func setBadgeSequentially(): Unit {
        setBadgeNumber(10, {
            err: Option<BusinessException>, data: Option<Unit> =>
            match (err) {
                case Some(e) =>
                    Hilog.error(0, "test", "setBadgeNumber 10 failed. Code is ${e.code}, message is ${e.message}")
                case None =>
                    Hilog.info(0, "test", "setBadgeNumber 10 success.")
                    setBadgeNumber(11, {
                        err: Option<BusinessException>, data: Option<Unit> =>
                        if (let Some(e) <- err) {
                            Hilog.error(0, "test", "setBadgeNumber 11 failed. Code is ${e.code}, message is ${e.message}")
                        } else {
                            Hilog.info(0, "test", "setBadgeNumber 11 success.")
                        }
                    })
            }
        })
    }
    ```
