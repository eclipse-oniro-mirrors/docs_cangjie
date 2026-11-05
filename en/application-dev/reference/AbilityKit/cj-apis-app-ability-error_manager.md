# ohos.app.ability.error_manager

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The ErrorManager provides capabilities for managing Ability errors, including listening to and unregistering from error events.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the example requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned example projects and configuration templates, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie-Example-Code-Instructions).

## class ErrorManager

```cangjie
public class ErrorManager {}
```

**Description:** Provides capabilities for managing Ability errors, including listening to and unregistering from error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### static func off(ErrorManagerEvent, Int32)

```cangjie
public static func off(eventType: ErrorManagerEvent, observerId: Int32): Unit
```

**Description:** Unregisters from listening to Ability error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [ErrorManagerEvent](#enum-errormanagerevent) | Yes | - | Error event type. |
| observerId | Int32 | Yes | - | Observer ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000003 | The specified ID does not exist. |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.AbilityKit.*
import kit.PerformanceAnalysisKit.*
import kit.CangjieKit.BusinessException

try {
    let observerId: Int32 = 1
    ErrorManager.off(ErrorManagerEvent.Error, observerId)
} catch (e: BusinessException) {
    Hilog.info(0, "test_errorManager", "${e.message}")
}
```

### static func on(ErrorManagerEvent, ErrorObserver)

```cangjie
public static func on(eventType: ErrorManagerEvent, observer: ErrorObserver): Int32
```

**Description:** Listens to Ability error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [ErrorManagerEvent](#enum-errormanagerevent) | Yes | - | Error event type. |
| observer | [ErrorObserver](./cj-apis-application-error_observer.md#class-errorobserver) | Yes | - | Error observer. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Observer ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000003 | The specified ID does not exist. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let observer = ErrorObserver(
        {
            errorMsg =>
                Hilog.info(0, "test_errorManager", "onUnhandledException, errorMsg:  =${errorMsg}")
        },
        onException: Some({ errorObj =>
            Hilog.info(0, "test_errorManager", "onException, name:   =${errorObj.name}")
            Hilog.info(0, "test_errorManager", "onException, message:   =${errorObj.message}")
            if (let Some(v) <-errorObj.stack) {
                Hilog.info(0, "test_errorManager", "onException, stack:    =${v}")
            }
        })
    )
    ErrorManager.on(ErrorManagerEvent.Error, observer)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum ErrorManagerEvent

```cangjie
public enum ErrorManagerEvent {
    | Error
    | ...
}
```

**Description:** Error management event types.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### Error

```cangjie
Error
```

**Description:** Error event.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22