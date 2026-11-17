# 订阅应用终止事件

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 简介

本文介绍如何使用HiAppEvent提供的仓颉接口订阅应用终止事件。接口的详细使用说明（参数限制、取值范围等）请参见[应用事件打点API文档](../reference/PerformanceAnalysisKit/cj-apis-hiappevent.md)。

## 接口说明

| 接口名                                              | 描述                                         |
| --------------------------------------------------- | -------------------------------------------- |
| addWatcher(watcher: Watcher): Option\<AppEventPackageHolder> | 添加应用事件观察者，以添加对应用事件的订阅。 |
| removeWatcher(watcher: Watcher): Unit               | 移除应用事件观察者，以移除对应用事件的订阅。 |

## 开发步骤

以订阅用户触发的应用终止事件为例，说明开发步骤。

1. 新建一个仓颉应用工程，编辑工程中的“entry > src > main > cangjie > main_ability.cj”文件，导入依赖模块：

   <!-- compile -->

   ```cangjie
   import kit.PerformanceAnalysisKit.*
   ```

2. 编辑工程中的“entry > src > main > cangjie > main_ability.cj”文件，在onCreate函数中添加系统事件的订阅，示例代码如下：

   <!-- compile -->

    ```cangjie
    let eventfilter = AppEventFilter("OS", names: ["APP_KILLED"])
    let watcher = Watcher(
        // 开发者可以自定义观察者名称，系统会使用名称来标识不同的观察者
        "watcher",
        // 开发者可以订阅感兴趣的系统事件，此处是订阅了应用终止事件
        appEventFilters: [eventfilter],
        // 开发者可以自行实现订阅实时回调函数，以便对订阅获取到的事件数据进行自定义处理
        onReceive: {
            domain: String, appEventGroups: Array<AppEventGroup> =>
                Hilog.info(0x0000, 'testTag', "HiAppEvent onReceive: domain=${domain}")
            for (eventGroup in appEventGroups) {
                // 开发者可以根据事件集合中的事件名称区分不同的系统事件
                Hilog.info(0x0000, 'testTag', "HiAppEvent eventName=${eventGroup.name}")
                for (eventInfo in eventGroup.appEventInfos) {
                    // 开发者可以对事件集合中的事件数据进行自定义处理，此处是将事件数据打印在日志中
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.domain=${eventInfo.domain}")
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.name=${eventInfo.name}")
                    for ((k, v) in eventInfo.params) {
                        // 开发者可以获取到应用终止事件发生的相关信息，重点关注time（事件触发时间）、
                        // foreground（应用前后台状态）、reason（终止原因）等字段
                        Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.params.${k}=${v}")
                    }
                }
            }
        }
        )
    HiAppEvent.addWatcher(watcher)
    ```

3. 编辑工程中的“entry > src > main > cangjie > index.cj”文件，在按钮点击函数中构造数组越界异常场景，示例代码如下：

    ```cangjie
    import std.collection.*

    // 在按钮点击函数中构造数组越界异常场景
    ArrayList<Int64>([1, 2, 3])[5..7]
    ```

4. 点击DevEco Studio界面中的运行按钮，运行应用工程。在应用界面中点击按钮可触发数组越界异常，系统将终止该应用进程，触发应用终止事件。

5. 应用被终止后，重新打开应用，会触发终止事件上报，系统会回调应用的onReceive函数，可以在Log窗口看到对系统事件数据的处理日志：

   ```text
   HiAppEvent onReceive: domain=OS
   HiAppEvent eventName=APP_KILLED
   HiAppEvent eventInfo.domain=OS
   HiAppEvent eventInfo.name=APP_KILLED
   HiAppEvent eventInfo.params.app_running_unique_id=207544
   HiAppEvent eventInfo.params.bundle_version=1.0.0
   HiAppEvent eventInfo.params.foreground=false
   HiAppEvent eventInfo.params.last_exit_detail_info={"exit_msg":"","kill_reason":"UserRequest","pid":"64555","process_name":"com.example.myapplication","process_state":"4","pss":"552792","rss":"552792","timestamp":"1794553803825","uid":"20020224"}
   HiAppEvent eventInfo.params.reason=UserRequest
   HiAppEvent eventInfo.params.time=1794553803862.000000
   ```
