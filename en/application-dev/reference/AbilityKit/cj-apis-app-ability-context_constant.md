# ohos.app.ability.context_constant

ContextConstant provides enumerations related to Context, including file partition information such as AreaMode.

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

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## enum AreaMode

```cangjie
public enum AreaMode <: Equatable<AreaMode> & ToString {
    | El1
    | El2
    | El3
    | El4
    | El5
    | ...
}
```

**Description:** File partition information.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Types:**

- [Equatable\<AreaMode>](#enum-areamode)
- ToString

### El1

```cangjie
El1
```

**Description:** File partition 1.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### El2

```cangjie
El2
```

**Description:** File partition 2.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### El3

```cangjie
El3
```

**Description:** File partition 3.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### El4

```cangjie
El4
```

**Description:** File partition 4.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### El5

```cangjie
El5
```

**Description:** File partition 5.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func !=(AreaMode)

```cangjie
public operator func !=(other: AreaMode): Bool
```

**Description:** Determines whether two enumeration values are not equal.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AreaMode](#enum-areamode) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are not equal, otherwise returns false. |

### func ==(AreaMode)

```cangjie
public operator func ==(other: AreaMode): Bool
```

**Description:** Determines whether two enumeration values are equal.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [AreaMode](#enum-areamode) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the string representation of the current enumeration.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the current enumeration. |