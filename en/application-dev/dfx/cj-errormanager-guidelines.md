# Error Management Development Guide

## Scenario Description

When an application's code contains specification issues or errors, exceptions and errors may occur during runtime, such as uncaught exceptions or application lifecycle timeouts. After an error occurs, the application will terminate abnormally. Error logs are typically stored in local user storage, making it inconvenient for developers to diagnose issues. Therefore, application developers can use error management interfaces to promptly report relevant errors and logs to their service platform before the application exits, facilitating issue identification.

After using the `errormanager` interface to monitor exceptions and errors, the application will not terminate. If the sole purpose is to obtain error logs, it is recommended to use [hiappevent](./cj-hiappevent-watcher-crash-events.md).

## Interface Description

The application error management interface is provided by the [errorManager](../../../en/application-dev/reference/AbilityKit/cj-apis-app-ability-error_manager.md#class-errormanager) module. Developers can import it as needed. For details, refer to the [Development Example](#Development Example).

**Error Management Interface Functionality:**

| Interface Name                                                                 | Description                                                                 |
| ------------------------------------------------------------------------------ | --------------------------------------------------------------------------- |
| `on(eventType: ErrorManagerEvent, observer: ErrorObserver): Int32`            | Registers an error observer. After registration, if the program crashes, the uncaught exception mechanism will be triggered. |
| `off(eventType: ErrorManagerEvent, observerId: Int32): Unit`                   | Unregisters an error observer.                                              |

<!-- waiting -->
**Error Observer (ErrorObserver) Interface Functionality:**

| Interface Name                                      | Description                                                                 |
| --------------------------------------------------- | --------------------------------------------------------------------------- |
| `onUnhandledException(errMsg: String): Unit`       | This callback is invoked when an exception is thrown during program execution and not caught by any `try-catch` statement. The `errMsg` content is fixed as "Uncaught exception was found." |
| `onException?(errObject: ErrorObject): Unit`       | This callback is invoked when an exception is thrown during program execution and not caught by any `try-catch` statement. The `errObject` contains the uncaught exception's name, message, and stack trace. |

## Development Example

<!-- compile -->

```cangjie
import kit.PerformanceAnalysisKit.Hilog
import kit.BasicServicesKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.window.WindowStage

func loggerInfo(str: String) {
    Hilog.info(0, "CangjieTest", str)
}

func loggerError(str: String) {
    Hilog.error(0, "CangjieTest", str)
}

let registerId: Int32 = -1
let callback: ErrorObserver = ErrorObserver(
    {
        errMsg: String => loggerInfo(errMsg)
    },
    onException: Some(
        {
            errorObj =>
            loggerInfo('onException, name: ${errorObj.name}')
            loggerInfo('onException, message: ${errorObj.message}')
            if (let Some(v) <- errorObj.stack) {
                loggerInfo('onException, stack: ${v}')
            }
        }
    )
)

var abilityWant: Want = Want()

public class EntryAbility <: UIAbility {
    public func onCreate(want: Want, launchParam: LaunchParam) {
        loggerInfo("[Demo] EntryAbility onCreate")
        let registerId = ErrorManager.on(ErrorManagerEvent.Error, callback)
        abilityWant = want
    }

    public override func onDestroy() {
        loggerInfo("[Demo] EntryAbility onDestroy")
        ErrorManager.off(ErrorManagerEvent.Error, registerId)
    }

    public func onWindowStageCreate(windowStage: WindowStage) {
        // Main window is created, set main page for this ability
        loggerInfo("[Demo] EntryAbility onWindowStageCreate")

        windowStage.loadContent("pages/index")
    }

    public func onWindowStageDestroy() {
        // Main window is destroyed, release UI related resources
        loggerInfo("[Demo] EntryAbility onWindowStageDestroy")
    }

    public override func onForeground() {
        // Ability has brought to foreground
        loggerInfo("[Demo] EntryAbility onForeground")
    }

    public override func onBackground() {
        // Ability has back to background
        loggerInfo("[Demo] EntryAbility onBackground")
    }
}
```