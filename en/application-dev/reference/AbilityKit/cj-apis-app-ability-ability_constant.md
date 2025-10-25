# ohos.app.ability.ability_constant

AbilityConstant provides enumerations related to Ability, including application launch reason LaunchReason, last exit reason LastExitReason, migration result OnContinueResult, etc.

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

- If the first line of sample code has a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, refer to [Cangjie Sample Code Description](../cj-development-intro.md#仓颉示例代码说明).

## class LaunchParam

```cangjie
public class LaunchParam {
    public var launchReason: LaunchReason
    public var lastExitReason: LastExitReason
}
```

**Description:** Launch parameters, including launch reason and last exit reason.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var lastExitReason

```cangjie
public var lastExitReason: LastExitReason
```

**Description:** Last exit reason.

**Type:** [LastExitReason](#enum-lastexitreason)

**Access:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var launchReason

```cangjie
public var launchReason: LaunchReason
```

**Description:** Launch reason.

**Type:** [LaunchReason](#enum-launchreason)

**Access:** Readable and writable

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum LastExitReason

```cangjie
public enum LastExitReason {
    | Unknown
    | Normal
    | CppCrash
    | AppFreeze
    | ...
}
```

**Description:** Last exit reason.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### AppFreeze

```cangjie
AppFreeze
```

**Description:** Application freeze.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### CppCrash

```cangjie
CppCrash
```

**Description:** C++ crash.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Normal

```cangjie
Normal
```

**Description:** Normal exit.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Unknown

```cangjie
Unknown
```

**Description:** Unknown reason.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum LaunchReason

```cangjie
public enum LaunchReason {
    | Unknown
    | StartAbility
    | Call
    | Continuation
    | AppRecovery
    | ...
}
```

**Description:** Launch reason.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### AppRecovery

```cangjie
AppRecovery
```

**Description:** Application recovery.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Call

```cangjie
Call
```

**Description:** Call launch.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Continuation

```cangjie
Continuation
```

**Description:** Cross-device migration.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### StartAbility

```cangjie
StartAbility
```

**Description:** Launch Ability.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Unknown

```cangjie
Unknown
```

**Description:** Unknown reason.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum MemoryLevel

```cangjie
public enum MemoryLevel <: Equatable<MemoryLevel> & ToString {
    | MemoryLevelModerate
    | MemoryLevelLow
    | MemoryLevelCritical
    | ...
}
```

**Description:** Memory level.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Types:**

- [Equatable\<MemoryLevel>](#enum-memorylevel)
- ToString

### MemoryLevelCritical

```cangjie
MemoryLevelCritical
```

**Description:** Critical memory shortage.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### MemoryLevelLow

```cangjie
MemoryLevelLow
```

**Description:** Low memory.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### MemoryLevelModerate

```cangjie
MemoryLevelModerate
```

**Description:** Moderate memory.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func !=(MemoryLevel)

```cangjie
public operator func !=(other: MemoryLevel): Bool
```

**Description:** Determines whether two enumeration values are not equal.

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MemoryLevel](#enum-memorylevel)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are not equal, otherwise returns false.|

### func ==(MemoryLevel)

```cangjie
public operator func ==(other: MemoryLevel): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MemoryLevel](#enum-memorylevel)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the current enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enumeration.|

## enum OnContinueResult

```cangjie
public enum OnContinueResult {
    | Agree
    | Reject
    | Mismatch
    | ...
}
```

**Description:** Cross-device migration result.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Agree

```cangjie
Agree
```

**Description:** Agree to migrate.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Mismatch

```cangjie
Mismatch
```

**Description:** Migration mismatch.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Reject

```cangjie
Reject
```

**Description:** Reject migration.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum WindowMode

```cangjie
public enum WindowMode {
    | WindowModeFullscreen
    | WindowModeSplitPrimary
    | WindowModeSplitSecondary
    | ...
}
```

**Description:** Window mode.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21### WindowModeFullscreen

```cangjie
WindowModeFullscreen
```

**Function:** Fullscreen mode.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### WindowModeSplitPrimary

```cangjie
WindowModeSplitPrimary
```

**Function:** Primary split-screen window.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### WindowModeSplitSecondary

```cangjie
WindowModeSplitSecondary
```

**Function:** Secondary split-screen window.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21