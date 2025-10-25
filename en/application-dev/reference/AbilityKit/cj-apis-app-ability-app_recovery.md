# ohos.app.ability.app_recovery

AppRecovery provides functionalities related to application recovery, including process restart.

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

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## func restartApp()

```cangjie
public func restartApp(): Unit
```

**Functionality:** Restarts the current process and launches the first Ability that was started when the application launched. If this Ability has saved state data, these state parameters will be passed in the wantParam attribute of the want parameter during the Ability's OnCreate lifecycle callback.

Launch rules:

If the foreground Ability of the current application supports recovery, that Ability will be relaunched.

If multiple recoverable Abilities are in the foreground, only the last one will be relaunched.

If no Ability is in the foreground, nothing will be launched.

Can be used in conjunction with [ErrorManager](./cj-apis-app-ability-error_manager.md#class-errormanager) related interfaces. The interval between two restarts should be more than one minute. Repeated calls to this interface within one minute will only exit the application without restarting it. Automatic restart behavior is consistent with active restart.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.AbilityKit.*

restartApp()
```