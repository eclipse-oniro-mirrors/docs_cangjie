# Subscribing to Crash Events (Cangjie)

## Interface Description

For detailed API usage instructions (parameter constraints, value ranges, etc.), please refer to the [Application Event Tracking API Documentation](../../../en/application-dev/reference/PerformanceAnalysisKit/cj-apis-hiappevent.md).

> **Note:**
>
> Using Cangjie interfaces to subscribe to crash events includes two crash types: CjError and NativeCrash.

**Subscription Interface Functions:**

| Interface Name                                          | Description                                  |
| ------------------------------------------------------- | ------------------------------------------- |
| addWatcher(watcher: Watcher): Option\<AppEventPackageHolder> | Adds an application event observer for subscribing to application events. |
| removeWatcher(watcher: Watcher): Unit                   | Removes an application event observer for unsubscribing from application events. |

## Development Steps

This example demonstrates development steps by subscribing to crash events triggered when a user clicks a button.

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_bility.cj" file to import dependency modules:

   <!-- compile -->

   ```cangjie
   import kit.BasicServicesKit.*
   import kit.PerformanceAnalysisKit.{HiAppEvent, Hilog}
   ```

2. Add system event subscription in the onCreate function of "entry > src > main > cangjie > main_bility.cj":

   <!-- compile -->

   ```cangjie
    let eventfilter = AppEventFilter("OS", names: ["APP_CRASH"])
    let watcher = Watcher(
        // Developers can customize the observer name, which the system uses to identify different observers
        "watcher2",
        // Developers can subscribe to system events of interest; here we subscribe to crash events
        appEventFilters: [eventfilter],
        // Developers can implement the subscription callback function to customize processing of event data
        onReceive: {
            domain: String, appEventGroups: Array<AppEventGroup> =>
                Hilog.info(0x0000, 'testTag', "HiAppEvent onReceive: domain=${domain}")
            for (eventGroup in appEventGroups) {
                // Developers can distinguish different system events by their names
                Hilog.info(0x0000, 'testTag', "HiAppEvent eventName=${eventGroup.name}")
                for (eventInfo in eventGroup.appEventInfos) {
                    // Developers can process event data; here we log the event data
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.domain=${eventInfo.domain}")
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.name=${eventInfo.name}")
                    Hilog.info(0x0000, 'testTag', "HiAppEvent eventInfo.eventType.value=${eventInfo.eventType.getValue()}")
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

3. Edit "entry > src > main > cangjie > Index.cj" to add a button and construct a crash scenario in onClick to trigger the event:

   <!-- compile -->

   ```cangjie
    import stdx.encoding.json.*

    // Construct a crash scenario in the button click function to trigger application crash events
    Button("appCrash").onClick { evt =>
        let result = JsonObject.fromStr("")
    }
   ```

4. Click the Run button in DevEco Studio to launch the application. Then click the "appCrash" button to trigger a crash event. After the crash occurs, the system generates crash logs using different stack trace methods based on the crash type (CjError or NativeCrash) before callback. NativeCrash stack tracing takes about 2 seconds (actual time depends on business thread count and IPC latency). CjError triggers in-process stack tracing, while NativeCrash triggers out-of-process stack tracing, making NativeCrash tracing slower. Users can subscribe to crash events, which are reported asynchronously after stack tracing without blocking current operations.

5. If the application doesn't catch the crash exception, the system handles it and terminates the app. On next launch, HiAppEvent reports the crash event to registered listeners and triggers callback.

If the application actively catches crash exceptions, HiAppEvent will callback before app termination in these scenarios:

Scenario 1: Exception handling doesn't actively terminate the app (e.g., using [errorManger.on](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-error_manager.md#static-func-onErrorManagerEvent-errorobserver) to catch CjError, or registering NativeCrash signal handlers without termination).

Scenario 2: Exception handling takes too long, delaying app termination.

After HiAppEvent completes event reporting and callback, you can view processed system event logs in the Log window:

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