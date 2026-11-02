# 管理通知角标

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

针对未读的通知，系统提供了角标设置接口，将未读通知个数显示在桌面图标的右上角角标上。

通知增加时，角标上显示的未读通知个数需要增加。

通知被查看后，角标上显示的未读通知个数需要减少，没有未读通知时，不显示角标。

## 接口说明

当角标设定个数取值小于或等于0时，表示清除角标。取值大于99时，通知角标将显示99+。

- 增加角标数、减少角标数，均通过[setBadgeNumber()](../reference/NotificationKit/cj-apis-notification-manager.md#func-setbadgenumberint32-asynccallbackunit)接口设置，桌面按设置的角标数呈现。

  | **接口名** | **描述** |
  | -------- | -------- |
  | setBadgeNumber(badgeNumber: Int32, callback: AsyncCallback\<Unit>): Unit | 设置角标个数。 |

## 开发步骤

详细的API说明请参见[通知管理API参考](../reference/NotificationKit/cj-apis-notification-manager.md)。

1. 导入模块。

    <!-- compile -->

    ```cangjie
    import kit.NotificationKit.*
    import kit.CangjieKit.{AsyncCallback, BusinessException}
    import kit.PerformanceAnalysisKit.Hilog
    ```

2. 增加角标个数。

    在发布完新的通知后，调用[setBadgeNumber](../reference/NotificationKit/cj-apis-notification-manager.md#func-setbadgenumberint32-asynccallbackunit)接口设置角标个数。

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

3. 减少角标个数。

    一条通知被查看后，应用需要调用接口设置剩下未读通知个数，桌面刷新角标。

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

## 常见问题

由于setBadgeNumber为异步接口，使用setBadgeNumber连续设置角标时，为了确保执行顺序符合预期，需要确保上一次设置完成后才能进行下一次设置。

- 反例

    每次接口调用是相互独立的、没有依赖关系的，实际执行时无法保证调用顺序。

    示例如下：

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
    setBadgeNumber(11, makeCallback("setBadgeNumber 11")) // 无法保证本次设置在上一次设置完成后执行
    ```

- 正例

    多次接口调用存在依赖关系，在上一次设置的回调中发起下一次设置。

    示例如下：

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
