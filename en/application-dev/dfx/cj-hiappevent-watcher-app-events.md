# Subscribing to Application Events (Cangjie)

HiAppEvent provides interfaces for subscribing to application events to retrieve them locally.

## Interface Description

For detailed usage instructions of the API interfaces (parameter usage restrictions, specific value ranges, etc.), please refer to the [Application Event Logging API Documentation](../../../en/application-dev/reference/PerformanceAnalysisKit/cj-apis-hiappevent.md).

**Logging Interface Functionality:**

| Interface Name                  | Description               |
| ------------------------------- | ------------------------- |
| write(info: AppEventInfo): Unit | Application event logging method. |

**Subscription Interface Functionality:**

| Interface Name                                                   | Description                                         |
| ---------------------------------------------------------------- | -------------------------------------------------- |
| addWatcher(watcher: Watcher): Option\<AppEventPackageHolder> | Adds an application event watcher to subscribe to application events. |
| removeWatcher(watcher: Watcher): Unit                            | Removes an application event watcher to unsubscribe from application events. |

## Development Steps

Taking the implementation of logging and subscribing to button click events as an example, the development steps are as follows:

1. Create a new Cangjie application project and edit the "entry > src > main > cangjie > main_ability.cj" file in the project to import the required modules:

    <!--compile-->
    ```cangjie
    import kit.PerformanceAnalysisKit.*
    import kit.PerformanceAnalysisKit.{Watcher as hiWatcher, ValueType as HiAppEventValueType}
    import ohos.base.*
    import ohos.component.Button
    ```

2. Edit the "entry > src > main > cangjie > main_ability.cj" file in the project and add a subscription to button click events in the onCreate function. Example code:

    <!--compile-->
    ```cangjie
    var condition = TriggerCondition(row: 1, size: 120, timeOut: 0)
    var appEventFilter = [AppEventFilter("cangjie_watcher")]
    var watcher = hiWatcher(
        "watcher1",
        triggerCondition: condition,
        appEventFilters: appEventFilter,
        onTrigger: Some(
            {
                row, size, holder =>
                Hilog.info(0, "test_hiAppEvent_addWatcher_01",
                    "HiAppEvent onTrigger: curRow=${row},curSize=${size}")
                while (let Some(v) <- holder.takeNext()) {
                    let eventPkg = v
                    Hilog.info(0, "test_hiAppEvent_addWatcher_01", "HiAppEvent packageId=${eventPkg.packageId}")
                    Hilog.info(0, "test_hiAppEvent_addWatcher_01", "HiAppEvent row=${eventPkg.row}")
                    Hilog.info(0, "test_hiAppEvent_addWatcher_01", "HiAppEvent size=${eventPkg.size}")
                    for (i in 0..eventPkg.data.size) {
                        Hilog.info(0, "test_hiAppEvent_addWatcher_01", "HiAppEvent info=${eventPkg.data[i]}")
                    }
                }
            }
        )
    )
    ```

3. Edit the "entry > src > main > cangjie > index.cj" file in the project to import the required modules:

    <!--compile-->
    ```cangjie
    import kit.PerformanceAnalysisKit.*
    import kit.PerformanceAnalysisKit.{Watcher as hiWatcher, ValueType as HiAppEventValueType}
    import ohos.base.*
    ```

4. Edit the "entry > src > main > cangjie > index.cj" file in the project, add a button, and implement event logging in its onClick function to record button click events. Example code:

    <!--compile-->
    ```cangjie
    Button("writeTest").onClick({ evt =>
        // Log the button click event in the onClick function
        let eventParams: Array<Parameters> = [Parameters("click_time", INT(100))]
        let eventInfo: AppEventInfo = AppEventInfo(
            // Event domain definition
            "button",
            // Event name definition
            "click",
            // Event type definition
            EventType.BEHAVIOR,
            // Event parameter definition
            eventParams)

        HiAppEvent.write(eventInfo)
    })
    ```

5. Click the Run button in the DevEco Studio interface to run the application project. Then, click the "writeTest" button on the application interface to trigger a button click event log.

6. You can view the successful logging of the button click event and the processed log data from the subscription callback in the Log window:

   ```text
   HiAppEvent success to write event
   HiAppEvent eventPkg.packageId=0
   HiAppEvent eventPkg.row=1
   HiAppEvent eventPkg.size=124
   HiAppEvent eventPkg.info={"domain_":"button","name_":"click","type_":4,"time_":1670268234523,"tz_":"+0800","pid_":3295,"tid_":3309,"click_time":100}
   ```