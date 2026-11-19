# Subscribing to AppKilled Events (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Interface Description

For detailed usage instructions of the API interface (parameter usage restrictions, specific value ranges, etc.), please refer to the [Application Event Tracking API Documentation](../reference/PerformanceAnalysisKit/cj-apis-hiappevent.md).

**Subscription Interface Function Description:**

| Interface Name                                          | Description                                      |
| ------------------------------------------------------- | ------------------------------------------------ |
| addWatcher(watcher: Watcher): Option\<AppEventPackageHolder> | Adds an application event observer to subscribe to application events. |
| removeWatcher(watcher: Watcher): Unit                   | Removes an application event observer to unsubscribe from application events. |

## Development Steps

This section illustrates the development steps by implementing subscription to an application killed event generated in an application crash scenario.

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_ability.cj" file in the project to import the required modules:

   <!-- compile -->

   ```cangjie
   import kit.PerformanceAnalysisKit.*
   ```

2. Edit the "entry > src > main > cangjie > main_ability.cj" file in the project and add subscription to system events in the onCreate function. Example code:

   <!-- compile -->

   ```cangjie
   let eventfilter = AppEventFilter("OS", names: ["APP_CRASH"])
   let watcher = Watcher(
       // Developers can customize the observer name, which the system uses to identify different observers
       "watcher",
       // Developers can subscribe to system events of interest; here, application killed events are subscribed to
       appEventFilters: [eventfilter],
       // Developers can implement their own real-time callback function to process the subscribed event data
       onReceive: {
           domain: String, appEventGroups: Array<AppEventGroup> =>
               Hilog.info(0x0000, 'testTag', "HiAppEvent onReceive: domain=${domain}")
           for (eventGroup in appEventGroups) {
               // Developers can distinguish between different system events based on the event names in the event collection
               Hilog.info(0x0000, 'testTag', "HiAppEvent eventName=${eventGroup.name}")
               for (eventInfo in eventGroup.appEventInfos) {
                   // Developers can process the event data in the event collection; here, the event data is logged
                   Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.domain=${eventInfo.domain}")
                   Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.name=${eventInfo.name}")
                   for ((k, v) in eventInfo.params) {
                       // Developers can obtain information related to the application killed event,
                       // focusing on fields such as time (event trigger time), foreground (application
                       // foreground/background status), crash_type (crash type), exception (exception
                       // information), and external_log (crash log file path)
                       Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.params.${k}=${v}")
                   }
               }
           }
       }
   )
   HiAppEvent.addWatcher(watcher)
   ```

3. Edit the "entry > src > main > cangjie > index.cj" file in the project and add the following example code in the button click function to construct an array out-of-bounds exception scenario:

   ```cangjie
   import std.collection.*

   // Construct an array out-of-bounds exception scenario in the button click function
   ArrayList<Int64>([1, 2, 3])[5..7]
   ```

4. Click the Run button in DevEco Studio to run the application project. Clicking the button on the application interface triggers the array out-of-bounds exception, and the system terminates the application process, which triggers the application killed event.

5. After the application is terminated, reopen the application. The termination event is reported, the system calls back the onReceive function of the application, and you can view the processed event data logs in the Log window:

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
