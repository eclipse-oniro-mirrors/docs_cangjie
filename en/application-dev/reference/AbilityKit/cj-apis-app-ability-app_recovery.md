# ohos.app.ability.app_recovery

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

AppRecovery provides functionalities related to application recovery, including process restart, etc.

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

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, configuration needs to be done in the "main_ability.cj" file of the Cangjie template project.

For details about the sample projects and configuration templates mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func restartApp()

```cangjie
public func restartApp(): Unit
```

**Functionality:** Restarts the current process and launches the first Ability that was started when the application was initiated. If this Ability has saved states, these state data will be passed as the wantParam property in the want parameter of the Ability's OnCreate lifecycle callback.

Launch rules:

If the foreground Ability of the current application supports recovery, that Ability will be relaunched.

If multiple recoverable Abilities are in the foreground, only the last one will be relaunched.

If no Ability is in the foreground, nothing will be relaunched.

Can be used in conjunction with [ErrorManager](./cj-apis-app-ability-error_manager.md#class-errormanager) related interfaces. The interval between two restarts should be greater than one minute. Repeated calls to this interface within one minute will only exit the application without restarting it. Automatic restart behavior is consistent with active restart.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.AbilityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    restartApp()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```