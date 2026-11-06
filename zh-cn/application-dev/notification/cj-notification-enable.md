# 请求通知授权

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

应用需要获取用户授权才能发送通知。在通知发布前调用[requestEnableNotification()](../reference/NotificationKit/cj-apis-notification-manager.md#func-requestenablenotificationuiabilitycontext-asynccallbackunit)接口，弹窗让用户选择是否允许发送通知。用户拒绝授权后，再次调用该接口时返回错误码1600004，表示通知开关处于关闭状态。

## 接口说明

接口详情参见[ohos.notification_manager（通知管理）](../reference/NotificationKit/cj-apis-notification-manager.md)。

**表1** 通知授权接口功能介绍

| **接口名** | **描述** |
| -------- | -------- |
| isNotificationEnabledSync(): Bool | 同步查询通知是否授权。 |
| requestEnableNotification(context: [UIAbilityContext](../reference/AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext), callback: AsyncCallback\<Unit>): Unit | 请求发送通知的许可，第一次调用会弹窗让用户选择。 |

## 开发步骤

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 查询当前应用的通知授权状态。

    <!-- compile -->

    ```cangjie
    // index.cj

    let enabled = isNotificationEnabledSync()
    Hilog.info(0, "test", "isNotificationEnabledSync success, enabled: ${enabled}")
    ```

3. 拉起通知弹窗，向用户请求通知授权。

    应用可在发布通知前调用[requestEnableNotification](../reference/NotificationKit/cj-apis-notification-manager.md#func-requestenablenotificationuiabilitycontext-asynccallbackunit)接口，弹窗让用户选择是否允许发送通知。可通过该接口的错误码判断用户是否授权，若返回的错误码为1600004，即为拒绝授权。

    <!-- compile -->

    ```cangjie
    // index.cj

    let ctx = Global.abilityContext // 此处需手动配置模板，获取Context上下文。
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

    > **注意：**
    >
    > 该接口只能在应用界面加载完成后调用，即`loadContent`调用成功后。
