# Subscribing to appfreeze Events (Cangjie)

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

This section illustrates the development steps by implementing subscription to appfreeze events triggered when a user clicks a button.

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_bility.cj" file in the project to import the required modules:

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   import kit.PerformanceAnalysisKit.{HiAppEvent, Hilog, AppEventGroup, AppEventFilter, Watcher}
   import std.collection.HashMap
   ```

2. Edit the "entry > src > main > cangjie > main_bility.cj" file in the project and add subscription to system events in the onCreate function. Example code:

   <!-- compile -->

   ```cangjie
    let eventfilter = AppEventFilter("OS", names: ["APP_FREEZE"])
    let watcher = Watcher(
        // Developers can customize the observer name, which the system uses to identify different observers
        "watcher2",
        // Developers can subscribe to system events of interest; here, appfreeze events are subscribed to
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
                        // Developers can obtain information related to the appfreeze event
                        if (k == "hilog") {
                            Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.params.${k}=${v}")
                        } else {
                            Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.params.${k}=${v}")
                        }
                    }
                }
            }
        }
        )
    HiAppEvent.addWatcher(watcher)
   ```

3. Create a new ArkTS project and edit the "entry > src > main > ets > pages > Index.ets" file in the project. Add a button and construct an appfreeze scenario in its onClick function to trigger the appfreeze event. Example code:

   ```ts
    Button("appFreeze").onClick(()=>{
      // Construct a freeze scenario in the button click function to trigger the appfreeze event
      setTimeout(() => {
        while (true) {}
      }, 1000)
    })
   ```

4. Click the Run button in DevEco Studio to run the application project. Then, click the "appFreeze" button on the application interface to trigger an appfreeze event.

5. After the application exits due to appfreeze, re-enter the application to view the processed event data logs in the Log window:

   ```text
   HiAppEvent onReceive: domain=OS
   HiAppEvent eventName=APP_FREEZE
   HiAppEvent eventInfo.domain=OS
   HiAppEvent eventInfo.name=APP_FREEZE
   HiAppEvent eventInfo.eventType=1
   HiAppEvent eventInfo.params.time=1711440881768
   HiAppEvent eventInfo.params.foreground=true
   HiAppEvent eventInfo.params.bundle_version=1.0.0
   HiAppEvent eventInfo.params.bundle_name=com.example.myapplication
   HiAppEvent eventInfo.params.process_name=com.example.myapplication
   HiAppEvent eventInfo.params.pid=3197
   HiAppEvent eventInfo.params.uid=20010043
   HiAppEvent eventInfo.params.uuid=27fac7098da46efe1cae9904946ec06c5acc91689c365efeefb7a23a0c37df77
   HiAppEvent eventInfo.params.exception={"message":"App main thread is not response!","name":"THREAD_BLOCK_6S"}
   HiAppEvent eventInfo.params.hilog.size=77
   HiAppEvent eventInfo.params.event_handler.size=6
   HiAppEvent eventInfo.params.event_handler_size_3s=5
   HiAppEvent eventInfo.params.event_handler_size_6s=6
   HiAppEvent eventInfo.params.peer_binder.size=0
   HiAppEvent eventInfo.params.threads.size=28
   HiAppEvent eventInfo.params.memory={"pss":0,"rss":0,"sys_avail_mem":1361464,"sys_free_mem":796232,"sys_total_mem":1992340,"vss":0}
   HiAppEvent eventInfo.params.external_log=["/data/storage/el2/log/hiappevent/APP_FREEZE_1711440899240_3197.log"]
   HiAppEvent eventInfo.params.log_over_limit=false
   HiAppEvent eventInfo.params.test_data=100
   ```