# ohos.application.error_observer

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

- If the sample code has a "// index.cj" comment in the first line, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class ErrorObject

```cangjie
public class ErrorObject {
    public let name: String
    public let message: String
    public let stack: Option<String>
}
```

**Description:** Contains the exception name, exception message, and stack trace of the uncaught exception.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### let message

```cangjie
public let message: String
```

**Description:** Contains the exception message of the uncaught exception.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### let name

```cangjie
public let name: String
```

**Description:** Contains the exception name of the uncaught exception.

**Type:** String

**Access:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### let stack

```cangjie
public let stack: Option<String>
```

**Description:** Contains the stack trace of the uncaught exception.

**Type:** Option\<String>

**Access:** Read-only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

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

**Description:** Exception monitoring module.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onException

```cangjie
public var onException: Option <(ErrorObject) -> Unit>
```

**Description:** Callback when an application exception occurs and is reported to the JS layer.

**Type:** Option\<([ErrorObject](#class-errorobject))->Unit>

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onUnhandledException

```cangjie
public var onUnhandledException:(String) -> Unit
```

**Description:** Callback when an uncaught exception occurs in the application.

**Type:** (String)->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### init((String) -> Unit, Option\<(ErrorObject) -> Unit>)

```cangjie
public init(
    onUnhandledException: (String) -> Unit,
    onException!: Option<(ErrorObject) -> Unit> = None
)
```

**Description:** Constructs an exception monitoring class.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| onUnhandledException | (String)->Unit | Yes | - | Callback when an uncaught exception occurs in the application. |
| onException | Option\<([ErrorObject](#class-errorobject))->Unit> | No | None | Callback when an application exception occurs and is reported to the JS layer. |