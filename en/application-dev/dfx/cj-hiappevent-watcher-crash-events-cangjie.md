# Subscribing to Crash Events (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Interface Description

For detailed API usage instructions (parameter constraints, value ranges, etc.), please refer to the [Application Event Tracking API Documentation](../reference/PerformanceAnalysisKit/cj-apis-hiappevent.md).

> **Note:**
>
> Using the Cangjie interface to subscribe to crash events includes two crash types: CjError and NativeCrash.

**Subscription Interface Functionality:**

| Interface Name                                          | Description                                  |
| ------------------------------------------------------- | -------------------------------------------- |
| addWatcher(watcher: Watcher): Option\<AppEventPackageHolder> | Method to add an application event observer for subscribing to application events. |
| removeWatcher(watcher: Watcher): Unit                   | Method to remove an application event observer for unsubscribing from application events. |

## Development Steps

Taking the example of subscribing to crash events triggered by user button clicks, the development steps are as follows:

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_bility.cj" file to import dependency modules:

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   import kit.PerformanceAnalysisKit.{HiAppEvent, Hilog}
   import ohos.hiviewdfx.hi_app_event.*
   ```

2. Add system event subscription in the onCreate function of the "entry > src > main > cangjie > main_bility.cj" file. Example:

   <!-- compile -->

   ```cangjie
    let eventfilter = AppEventFilter("OS", names: ["APP_CRASH"])
    let watcher = Watcher(
        // Developers can customize the observer name, which the system uses to identify different observers
        "watcher2",
        // Developers can subscribe to system events of interest; here, crash events are subscribed to
        appEventFilters: [eventfilter],
        // Developers can implement their own real-time callback function to process the subscribed event data
        onReceive: {
            domain: String, appEventGroups: Array<AppEventGroup> =>
                Hilog.info(0x0000, 'testTag', "HiAppEvent onReceive: domain=${domain}")
            for (eventGroup in appEventGroups) {
                // Developers can distinguish different system events based on the event names in the event collection
                Hilog.info(0x0000, 'testTag', "HiAppEvent eventName=${eventGroup.name}")
                for (eventInfo in eventGroup.appEventInfos) {
                    // Developers can process the event data in the event collection; here, the event data is logged
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.domain=${eventInfo.domain}")
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.name=${eventInfo.name}")
                    for ((k, v) in eventInfo.params) {
                        // Developers can access crash-related information
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

3. Edit "entry > src > main > cangjie > Index.cj" to add a button and construct a crash scenario in the onClick function to trigger the event. Example code:

   <!-- compile -->

   ```cangjie
    import stdx.encoding.json.*

    // Construct a crash scenario in the button click function to trigger an application crash event
    Button("appCrash").onClick ({ evt =>
        let result = JsonObject.fromStr("")
    })
   ```

4. Click the Run button in DevEco Studio to launch the application. Then, click the "appCrash" button on the application interface to trigger a crash event. After the crash event occurs, the system generates crash logs using different stack trace methods based on the crash type (CjError or NativeCrash) and then performs the callback. The NativeCrash stack trace takes about 2 seconds, with actual time depending on the number of business threads and inter-process communication delays. CjError triggers in-process stack tracing, while NativeCrash triggers out-of-process stack tracing, making NativeCrash stack tracing more time-consuming than CjError. Users can subscribe to crash events, which are reported asynchronously after stack tracing completes without blocking current business operations.

5. If the application does not catch the crash exception, the system handles it and the application exits. Upon the next launch, HiAppEvent reports the crash event to registered listeners and triggers the callback.

If the application actively catches the crash exception, HiAppEvent will trigger the callback before the application exits in the following two scenarios:

**Scenario 1:** The exception handler does not actively exit, and the application does not terminate after the crash. For example, using [errorManger.on](../reference/AbilityKit/cj-apis-app-ability-error_manager.md#static-func-onErrorManagerEvent-errorobserver) to catch CjError or registering a NativeCrash signal handler without exiting.

**Scenario 2:** The exception handling process takes too long, delaying the application exit.

After HiAppEvent reports the event and completes the callback, the processed system event data logs can be viewed in the Log window:

   ```text
   HiAppEvent onReceive: domain=OS
   HiAppEvent eventName=APP_CRASH
   HiAppEvent eventInfo.domain=OS
   HiAppEvent eventInfo.name=APP_CRASH
   HiAppEvent eventInfo.eventType.value=1
   HiAppEvent eventInfo.params.bundle_name=com.example.myapplication
   HiAppEvent eventInfo.params.bundle_version=1.0.0
   HiAppEvent eventInfo.params.crash_type=CjError
   HiAppEvent eventInfo.params.exception={"message":"none","name":"none","stack":"one"}
   HiAppEvent eventInfo.params.external_log=[/data/storage/el2/log/hiappevent/APP_CRASH_1744613860845_42711.log]
   HiAppEvent eventInfo.params.foreground=true
   HiAppEvent eventInfo.params.hilog= 10054
   HiAppEvent eventInfo.params.log_over_limit=false
   HiAppEvent eventInfo.params.pid=42711
   HiAppEvent eventInfo.params.time=1744613860665.000000
   HiAppEvent eventInfo.params.uid=20020192
   HiAppEvent eventInfo.params.uuid=4e85d04543811813ab4a2a3ed2443ebeebcca84298b89cb2460ecf99469b52de
   ```