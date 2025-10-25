# ohos.application.test_runner

This module provides framework testing capabilities.

## Importing the Module

```cangjie
import kit.AbilityKit.*
```

## Permission List

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample project and configuration template, refer to [Cangjie Sample Code Description](../cj-development-intro.md#仓颉示例代码说明).

## class TestRunner

```cangjie
public open class TestRunner {}
```

**Description:** Provides framework testing capabilities.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### static func registerCreator(String, () -> TestRunner)

```cangjie
public static func registerCreator(name: String, creator: () -> TestRunner): Unit
```

**Description:** Registers a function for constructing [TestRunner](#class-testrunner) objects.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Identifier for the constructor function. |
| creator | ()->[TestRunner](#class-testrunner) | Yes | - | Function for constructing [TestRunner](#class-testrunner) objects. |

### func onPrepare()

```cangjie
public open func onPrepare(): Unit
```

**Description:** Executes test cases.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func onRun()

```cangjie
public open func onRun(): Unit
```

**Description:** Prepares the unit testing environment for running test cases.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21