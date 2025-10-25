# ohos.app.ability.error_manager

The ErrorManager provides capabilities for managing Ability errors, including listening to and unregistering from error events.

## Import Module

```cangjie
import kit.AbilityKit.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## Usage Guidelines

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class ErrorManager

```cangjie
public class ErrorManager {}
```

**Description:** Provides capabilities for managing Ability errors, including listening to and unregistering from error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### static func off(ErrorManagerEvent, Int32)

```cangjie
public static func off(eventType: ErrorManagerEvent, observerId: Int32): Unit
```

**Description:** Unregisters from listening to Ability error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ErrorManagerEvent](#enum-errormanagerevent) | Yes | - | The type of error event. |
| observerId | Int32 | Yes | - | The observer ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 16000003 | The specified ID does not exist. |

### static func on(ErrorManagerEvent, ErrorObserver)

```cangjie
public static func on(eventType: ErrorManagerEvent, observer: ErrorObserver): Int32
```

**Description:** Listens to Ability error events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ErrorManagerEvent](#enum-errormanagerevent) | Yes | - | The type of error event. |
| observer | [ErrorObserver](./cj-apis-application-error_observer.md#class-errorobserver) | Yes | - | The error observer. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | The observer ID. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; 3. Parameter verification failed. |
  | 16000003 | The specified ID does not exist. |

## enum ErrorManagerEvent

```cangjie
public enum ErrorManagerEvent {
    | Error
    | ...
}
```

**Description:** Types of error management events.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Error

```cangjie
Error
```

**Description:** Error event.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21