# ohos.app.ability.ability_stage

AbilityStage provides functionalities related to AbilityStage, including its creation and registration.

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
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of a Cangjie template project.

For the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class AbilityStage

```cangjie
public open class AbilityStage {}
```

**Description:** AbilityStage is the runtime class for Ability, providing lifecycle callbacks such as creation and destruction of Ability.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop context

```cangjie
public mut prop context: AbilityStageContext
```

**Description:** The context of AbilityStage.

**Type:** [AbilityStageContext](cj-apis-app-ability-ui_ability.md#class-abilitystagecontext)

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### static func registerCreator(String, () -> AbilityStage)

```cangjie
public static func registerCreator(moduleName: String, creator: () -> AbilityStage): Unit
```

**Description:** Registers the creator of AbilityStage.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| moduleName | String | Yes | - | Module name. |
| creator | ()->[AbilityStage](#class-abilitystage) | Yes | - | The creator of AbilityStage. |

### func onCreate()

```cangjie
public open func onCreate(): Unit
```

**Description:** Callback triggered when AbilityStage is created, used to execute initialization business logic operations.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21