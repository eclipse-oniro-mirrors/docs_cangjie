# ohos.application.error_observer

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module defines exception monitoring.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## Usage Instructions

API sample code usage instructions:

- If the sample code contains a "// index.cj" comment in the first line, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class ErrorObject

```cangjie
public class ErrorObject {
    public let name: String
    public let message: String
    public let stack: Option<String>
}
```

**Function:** Contains the exception name, exception message, and stack trace of the uncaught exception.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### let message

```cangjie
public let message: String
```

**Function:** Contains the exception message of the uncaught exception.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### let name

```cangjie
public let name: String
```

**Function:** Contains the exception name of the uncaught exception.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### let stack

```cangjie
public let stack: Option<String>
```

**Function:** Contains the stack trace of the uncaught exception.

**Type:** Option\<String>

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

## class ErrorObserver

```cangjie
public class ErrorObserver {
    public var onUnhandledException:(String) -> Unit
    public var onException: Option <(ErrorObject) -> Unit>
    public init(
        onUnhandledException: (String) -> Unit,
        onException!: Option<(ErrorObject) -> Unit> = None
    )
}
```

**Function:** Exception monitoring module.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### var onException

```cangjie
public var onException: Option <(ErrorObject) -> Unit>
```

**Function:** Callback when an application exception occurs and is reported to the JS layer.

**Type:** Option\<([ErrorObject](#class-errorobject))->Unit>

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### var onUnhandledException

```cangjie
public var onUnhandledException:(String) -> Unit
```

**Function:** Callback when an uncaught exception occurs in the application.

**Type:** (String)->Unit

**Read/Write Permission:** Read/Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### init((String) -> Unit, Option\<(ErrorObject) -> Unit>)

```cangjie
public init(
    onUnhandledException: (String) -> Unit,
    onException!: Option<(ErrorObject) -> Unit> = None
)
```

**Function:** Constructs an exception monitoring class.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| onUnhandledException | (String)->Unit | Yes | - | Callback when an uncaught exception occurs in the application. |
| onException | Option\<([ErrorObject](#class-errorobject))->Unit> | No | None | Callback when an application exception occurs and is reported to the JS layer. |

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