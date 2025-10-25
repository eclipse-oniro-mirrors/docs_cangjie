# Event Reporting

HiAppEvent provides interfaces for processing and reporting events.

## Interface Description

For detailed usage instructions of the API interfaces (parameter usage restrictions, specific value ranges, etc.), please refer to the [Application Event Tracking API Documentation](../../../en/application-dev/reference/PerformanceAnalysisKit/cj-apis-hiappevent.md).

**Data Processor Interface Functions:**

| Interface Name                              | Description                                              |
| ------------------------------------------- | ------------------------------------------------------- |
| addProcessor(processor: Processor): Int64   | Adds a data processor to enable event reporting through preset processors. |
| removeProcessor(id: Int64): Unit            | Removes a data processor to cancel preset processors.    |

**User ID Interface Functions:**

| Interface Name                                 | Description                                            |
| ---------------------------------------------- | ----------------------------------------------------- |
| setUserId(name: String, value: String): Unit   | Sets a user ID, which can be carried by data processors when reporting events. |
| getUserId(name: String): String                | Retrieves the set user ID.                            |

**User Property Interface Functions:**

| Interface Name                                       | Description                                                |
| ---------------------------------------------------- | --------------------------------------------------------- |
| setUserProperty(name: String, value: String): Unit   | Sets a user property, which can be carried by data processors when reporting events. |
| getUserProperty(name: String): String                | Retrieves the set user property.                          |

## Development Steps

Using the example of tracking button click events and reporting them via processors, the development steps are as follows:

1. Edit the "entry > src > main > cangjie > index.cj" file in the project, add a button, and include a data processor in its onClick function. The `analytics_demo` is a preset data processor library on the device. The complete sample code is as follows:

    <!-- compile -->

    ```cangjie
    internal import kit.PerformanceAnalysisKit.{Watcher as hiWatcher, Event as HEvent}
    import kit.PerformanceAnalysisKit.Hilog
    import kit.BasicServicesKit.*
    import kit.CoreFileKit.*
    import kit.AbilityKit.*
    import ohos.base.*
    import kit.PerformanceAnalysisKit.*
    import std.collection.*

    func loggerInfo(str: String) {
        Hilog.info(0, "CangjieTest", str)
    }

    func loggerError(str: String) {
        Hilog.error(0, "CangjieTest", str)
    }

    @Entry
    @Component
    class EntryView {
        @State
        var message: String = "Hello World"

        var processorId = -1

        func build() {
            Row {
                Column {
                    Button(this.message)
                    .fontSize(50)
                    .fontWeight(FontWeight.Bold)
                    .onClick {
                        evt => this.message = "Hello Cangjie"
                        // Add a data processor in the button click function
                        let eventConfig = AppEventReportConfig(
                            // Event domain definition
                            domain: "button",
                            // Event name definition
                            name: "click",
                            // Whether to report events in real-time
                            isRealTime: true
                        )
                        let processor = Processor(
                            'analytics_demo',
                            debugMode: true,
                            routeInfo: 'CN',
                            appId: '111',
                            onStartReport: true,
                            onBackgroundReport: true,
                            periodReport: 10,
                            batchReport: 5,
                            userIds: ['testUserIdName'],
                            userProperties: ['testUserPropertyName'],
                            eventConfigs: [eventConfig]
                        )
                        this.processorId = HiAppEvent.addProcessor(processor)
                    }
                }.height(100.percent)
            }.width(100.percent)
        }
    }
    ```

2. Edit the "entry > src > main > cangjie > index.cj" file, add a button, and include functions to set and retrieve a user ID in its onClick function. The complete sample code is as follows:

    <!-- compile -->

    ```cangjie
        Button("userIdTest").onClick {
                evt =>
                // Set a user ID in the button click function
                HiAppEvent.setUserId('testUserIdName', '123456')

                // Retrieve the set user ID in the button click function
                let userId = HiAppEvent.getUserId('testUserIdName')
                Hilog.info(0x0000, 'testTag', 'userId: ${userId}')
        }
    ```

3. Edit the "entry > src > main > cangjie > index.cj" file, add a button, and include functions to set and retrieve a user property in its onClick function. The complete sample code is as follows:

    <!-- compile -->

    ```cangjie
        Button("userPropertyTest").onClick {
            evt =>
            // Set a user property in the button click function
            HiAppEvent.setUserProperty('testUserPropertyName', '123456')

            // Retrieve the set user property in the button click function
            let userProperty = HiAppEvent.getUserProperty('testUserPropertyName')
            Hilog.info(0x0000, 'testTag', 'userProperty: ${userProperty}')
        }
    ```

4. Edit the "entry > src > main > cangjie > index.cj" file, add a button, and include event tracking in its onClick function to record button click events. The complete sample code is as follows:

    <!-- compile -->

    ```cangjie
        Button("writeTest").onClick {
            evt =>
            let eventParams = HashMap<String, EventValueType>([
                ("click_time", IntValue(100))
            ])
            let eventInfo: AppEventInfo = AppEventInfo(
                // Event domain definition
                "button",
                // Event name definition
                "click",
                // Event type definition
                EventType.Behavior,
                // Event parameter definition
                eventParams)

            HiAppEvent.write(eventInfo)
        }
    ```

5. Edit the "entry > src > main > cangjie > index.cj" file, add a button, and include the removal of a data processor in its onClick function (the data processor was added in Step 2). The complete sample code is as follows:

    <!-- compile -->

    ```cangjie
        Button("removeProcessorTest").onClick {
            evt =>
                // Remove the data processor in the button click function
                HiAppEvent.removeProcessor(this.processorId)
        }
    ```

6. Click the Run button in the IDE to launch the application. Then, sequentially click the buttons "addProcessorTest", "userIdTest", "userPropertyTest", "writeTest", and "removeProcessorTest" in the application interface to successfully report an event via the data processor.

   Finally, the event processor successfully receives the event data, and the following log indicating successful event tracking appears in the Log window:

   ```text
   HiAppEvent success to write event
   ```