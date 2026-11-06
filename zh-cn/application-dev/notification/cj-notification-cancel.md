# 取消通知

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

用户点击通知并拉起应用到前台时，应用可以取消已发布的通知。

用户点击桌面图标拉起应用到前台时，用户查看后的应用内消息，应用可以选择取消这些已查看消息的通知。

例如：

场景1：用户收到某个好友的IM消息，点击通知进入应用查看消息后，应用可以取消相关通知提醒。

场景2：用户收到某个好友的IM消息，从桌面图标进入应用查看消息后，应用可以取消相关通知提醒。

## 接口说明

通知取消接口如下。接口详情参见[ohos.notification_manager（通知管理）](../reference/NotificationKit/cj-apis-notification-manager.md)。

| **接口名** | **描述** |
| -------- | -------- |
| cancelAll(callback: AsyncCallback\<Unit>): Unit | 取消所有该应用发布的通知。 |

## 开发步骤

本文以取消`文本类型通知`为例进行说明，其他类型通知取消操作与此类似。

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 发布通知。

    参考[发布文本类型通知](./cj-text-notification.md)。

3. 取消通知。

    <!-- compile -->

    ```cangjie
    // index.cj

    // 当拉起应用到前台，查看消息后，调用该接口取消该应用发布的全部通知。
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
