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

This section illustrates the development steps by implementing subscription to an application killed event triggered by the user.

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_ability.cj" file in the project to import the required modules:

   <!-- compile -->

   ```cangjie
   import kit.PerformanceAnalysisKit.*
   ```

2. Edit the "entry > src > main > cangjie > main_ability.cj" file in the project and add subscription to system events in the onCreate function. Example code:

   <!-- compile -->

   ```cangjie
   let eventfilter = AppEventFilter("OS", names: ["APP_KILLED"])
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
                       // foreground/background status), and reason (termination reason)
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
