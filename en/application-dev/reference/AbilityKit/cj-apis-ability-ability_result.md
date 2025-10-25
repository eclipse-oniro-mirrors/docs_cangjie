# ohos.ability.ability_result

This module defines the result codes and data returned after an Ability is started and terminated.

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

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class AbilityResult

```cangjie
public class AbilityResult {
    public var resultCode: Int32
    public var want: Want
    public init(resultCode: Int32, want!: Want = Want())
}
```

**Description:** Defines the result codes and data returned after an Ability is started and terminated.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var resultCode

```cangjie
public var resultCode: Int32
```

**Description:** Defines the returned result code.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### var want

```cangjie
public var want: Want
```

**Description:** Represents Want type information, such as ability name, package name, etc.

**Type:** [Want](cj-apis-app-ability-want.md#class-want)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

### init(Int32, Want)

```cangjie
public init(resultCode: Int32, want!: Want = Want())
```

**Description:** Constructs the AbilityResult class.

**System Capability:** SystemCapability.Ability.AbilityBase

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:--------------|:-----|:--------|:-------------|:------------|
| resultCode    | Int32 | Yes | - | Represents the result code. |
| want          | [Want](cj-apis-app-ability-want.md#class-want) | No | Want() | Represents Want type information, such as ability name, package name, etc. |