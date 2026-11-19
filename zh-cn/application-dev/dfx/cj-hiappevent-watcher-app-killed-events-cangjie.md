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

以订阅应用崩溃场景生成的应用终止事件为例，说明开发步骤。

1. 新建一个仓颉应用工程，编辑工程中的“entry > src > main > cangjie > main_ability.cj”文件，导入依赖模块：

   <!-- compile -->

   ```cangjie
   import kit.PerformanceAnalysisKit.*
   ```

2. 编辑工程中的“entry > src > main > cangjie > main_ability.cj”文件，在onCreate函数中添加系统事件的订阅，示例代码如下：

   <!-- compile -->

    ```cangjie
    let eventfilter = AppEventFilter("OS", names: ["APP_CRASH"])
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
                        // foreground（应用前后台状态）、crash_type（崩溃类型）、exception（异常信息）、
                        // external_log（崩溃日志文件路径）等字段
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
   HiAppEvent eventName=APP_CRASH
   HiAppEvent eventInfo.domain=OS
   HiAppEvent eventInfo.name=APP_CRASH
   HiAppEvent eventInfo.params.app_running_unique_id=17321655454838526938
   HiAppEvent eventInfo.params.bundle_name=com.example.myapplication
   HiAppEvent eventInfo.params.bundle_version=1.0.0
   HiAppEvent eventInfo.params.crash_type=CjError
   HiAppEvent eventInfo.params.exception={"message":"none","name":"none","stack":"one","thread_name":"e.myapplication"}
   HiAppEvent eventInfo.params.external_log=[/data/storage/el2/log/hiappevent/APP_CRASH_1795069726047_32554.log]
   HiAppEvent eventInfo.params.foreground=true
   HiAppEvent eventInfo.params.hilog=[11-19 14:28:42.857 32554 32554 I C05405/cjappspawn/CompConfig: [nodict]GetConfigByApp: GetDataShareData return 0 result, 11-19 14:28:42.857 32554 32554 E C01301/cjappspawn/Ability: [page_config_manager.cpp62]configJson_ is empty, 11-19 14:28:42.858 32554 32554 I C02D06/cjappspawn/XCollie: Application is in starting period., 11-19 14:28:42.859 32554 32554 I C04209/cjappspawn/WMSImms: NotifyAvoidAreaChange: win 924 api 26 type 0 area top [0 0 1260 123] , 11-19 14:28:42.859 32554 32554 I C04209/cjappspawn/WMSImms: NotifyAvoidAreaChange: win 924 api 26 type 1 area top [494 36 273 72] , 11-19 14:28:42.859 32554 32554 I C04209/cjappspawn/WMSImms: NotifyAvoidAreaChange: win 924 api 26 type 2 area empty, 11-19 14:28:42.859 32554 32554 I C04209/cjappspawn/WMSImms: NotifyAvoidAreaChange: win 924 api 26 type 3 area empty, 11-19 14:28:42.859 32554 32554 I C04209/cjappspawn/WMSImms: NotifyAvoidAreaChange: win 924 api 26 type 4 area bottom [409 2629 442 91] , 11-19 14:28:42.860 32554 32554 I C03922/cjappspawn/AceNavigation: [(100000:100000:scope)] disable forceSplit, mode:0, 11-19 14:28:42.860 32554 32554 I C04208/cjappspawn/WMSLayout: UpdateViewportConfig: Id: 924, reason: 0, viewportRect: [0 0 1260 2720], displayOrientation: 0, config[0, 0, 0, 3.250000], 11-19 14:28:42.860 32554 32554 I C03900/cjappspawn/Ace: [(100000:100000:scope)] router.Push pagePath = , 11-19 14:28:42.860 32554 32554 I C03900/cjappspawn/Ace: [(100000:100000:scope)] PageRouterManager LoadPage[1]: EntryView., 11-19 14:28:42.861 32554 32571 I C03900/cjappspawn/Ace: [(-1:100000:singleton)] [com.example.myapplication][entry][100000]: window focus, 11-19 14:28:42.861 32554 32554 I A01E00/cjappspawn/CJ-FFIBind: FFIData id duplicate: 4 with cache!, 11-19 14:28:42.861 32554 32554 I C03900/cjappspawn/Ace: [(100000:100000:scope)] LoadNativeView start, 11-19 14:28:42.861 32554 32571 I C04207/cjappspawn/WMSFocus: NotifyApplicationFocusChangedResult: 1, 11-19 14:28:42.861 32554 32554 I C03900/cjappspawn/Ace: [(100000:100000:scope)] OHOSAceFrameworkNGLoadCJView end., 11-19 14:28:42.861 32554 32571 I C04207/cjappspawn/WMSFocus: ProcessNotifyHighlightChange: timeStamp:1795069719556, highlightId:924, isHighlight:1,isSyncNotify:0, old:0, new:1795069719556, current:1795069722861, 11-19 14:28:42.861 32554 32571 I C04207/cjappspawn/WMSFocus: NotifyHighlightChange: windowId: 924, isHighlight: 1,, 11-19 14:28:42.861 32554 32571 I C03900/cjappspawn/Ace: [(-1:100000:singleton)] [com.example.myapplication][entry][100000]:window active, 11-19 14:28:42.864 32554 32570 I C04208/cjappspawn/WMSLayout: NotifySingleHandTransformChange: id:924, posX:0, posY:0, scaleX:1.000000, scaleY:1.000000, 11-19 14:28:42.864 32554 32631 W C057C1/cjappspawn/IPCWorkThread: ThreadHandler: proto:0 policy:0 name:OS_IPC_3_32631 invoker:3669720704, 11-19 14:28:42.864 32554 32554 I C03900/cjappspawn/Ace: [(100000:100000:scope)] Native TextController constructed: 13, 11-19 14:28:42.864 32554 32554 W C03926/cjappspawn/AceTheme: [(100000:100000:scope)] style text_pattern not contains linear_split_child_min_size!, 11-19 14:28:42.864 32554 32554 W C03926/cjappspawn/AceTheme: [(100000:100000:scope)] style text_pattern not contains menu_celia_ask_is_support!, 11-19 14:28:42.865 32554 32554 W C03926/cjappspawn/AceTheme: [(100000:100000:scope)] style 125829872 not contains app_theme_pattern!, 11-19 14:28:42.865 32554 32554 W C01E00/cjappspawn/ResourceManager: by id=125835722 limitPaths is empty, 11-19 14:28:42.865 32554 32554 E C01E00/cjappspawn/ResourceManager: ref id not found, 11-19 14:28:42.865 32554 32554 W C01E00/cjappspawn/ResourceManager: by id=125835722 limitPaths is empty, 11-19 14:28:42.865 32554 32554 E C01E00/cjappspawn/ResourceManager: ref id not found, 11-19 14:28:42.865 32554 32554 W C03937/cjappspawn/AceResource: [(100000:100000:scope)] Get pattern by name error, name=app_theme_pattern, bundleName: com.example.myapplication, moduleName: entry, 11-19 14:28:42.865 32554 32554 W C01E00/cjappspawn/ResourceManager: by id=125835722 limitPaths is empty
   HiAppEvent eventInfo.params.log_over_limit=false
   HiAppEvent eventInfo.params.pid=32554
   HiAppEvent eventInfo.params.process_name=com.example.myapplication
   HiAppEvent eventInfo.params.time=1795069725620.000000
   HiAppEvent eventInfo.params.uid=20020224
   HiAppEvent eventInfo.params.uuid=2831b8f6bcf0e9f66337c049b6af44f7759a0d2eed13ca801d7976155e8f0771
   ```
