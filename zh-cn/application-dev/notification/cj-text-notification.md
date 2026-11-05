# 发布文本类型通知

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

文本类型通知主要应用于发送短信息、提示信息等，当前支持普通文本类型。

**表1** 基础类型通知中的内容分类

| 类型 | 描述 |
| ---- | ---- |
| NotificationContentBasicText | 普通文本类型。 |

## 接口说明

通知发布接口说明详见下表，通知发布的详情可通过入参[NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest)来进行指定，可以包括通知内容、通知ID、通知槽类型和通知标签等信息。

| **接口名** | **描述** |
| -------- | -------- |
| publish(request: [NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest), callback: AsyncCallback\<Unit>): Unit | 发布通知。 |

## 开发步骤

详细的API说明请参见[通知管理API参考](../reference/NotificationKit/cj-apis-notification-manager.md)。

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 构造[NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest)对象，并发布通知。

    普通文本类型通知由标题、文本内容和附加信息三个字段组成，详情请参考[NotificationBasicContent](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationbasiccontent)。

    <!-- compile -->

    ```cangjie
    // index.cj

    let basicContent = NotificationBasicContent("test_title", "test_text")
    basicContent.additionalText = Some("test_additionalText")
    let content = NotificationContent(ContentType.NotificationContentBasicText) // 普通文本类型通知
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

3. （可选）更新已发布的通知。

    新发布通知的ID和标签与已发布通知相同时，新通知将替换原通知，实现通知更新。例如需要更新标题时，构造相同ID的[NotificationRequest](../reference/NotificationKit/cj-apis-notification-manager.md#class-notificationrequest)并再次调用publish接口即可。

    <!-- compile -->

    ```cangjie
    // index.cj

    let newBasicContent = NotificationBasicContent("test_title_new", "test_text_new")
    let newContent = NotificationContent(ContentType.NotificationContentBasicText)
    newContent.normal = Some(newBasicContent)
    let newRequest = NotificationRequest(newContent)
    newRequest.id = Some(1) // 与已发布通知的ID相同，实现通知更新
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
