# ohos.app.ability.want_constant

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

- If the first line of sample code contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Description](../cj-development-intro.md#仓颉示例代码说明).

## enum Flags

```cangjie
public enum Flags <: Equatable<Flags> & ToString {
    | FlagAuthReadUriPermission
    | FlagAuthWriteUriPermission
    | FlagAuthPersistableUriPermission
    | FlagInstallOnDemand
    | FlagStartWithoutTips
    | ...
}
```

**Function:** Flags description. Used to indicate the method for processing [Want](./cj-apis-app-ability-want.md#class-want).

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parent Types:**

- [Equatable\<Flags>](#enum-flags)
- ToString

### FlagAuthPersistableUriPermission

```cangjie
FlagAuthPersistableUriPermission
```

**Function:** Indicates that the URI can be persisted by the recipient. This field only takes effect on tablet devices. Value: 0x00000040.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### FlagAuthReadUriPermission

```cangjie
FlagAuthReadUriPermission
```

**Function:** Indicates authorization to perform read operations on the URI. Value: 0x00000001.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### FlagAuthWriteUriPermission

```cangjie
FlagAuthWriteUriPermission
```

**Function:** Indicates authorization to perform write operations on the URI. Value: 0x00000002.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### FlagInstallOnDemand

```cangjie
FlagInstallOnDemand
```

**Function:** If the specified feature is not installed, install it. Value: 0x00000800.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### FlagStartWithoutTips

```cangjie
FlagStartWithoutTips
```

**Function:** If an implicit ability launch cannot match any application, no prompt dialog will pop up. Value: 0x40000000.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### func !=(Flags)

```cangjie
public operator func !=(other: Flags): Bool
```

**Function:** Determines whether two enumeration values are not equal.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Flags](#enum-flags) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are not equal, otherwise returns false. |

### func ==(Flags)

```cangjie
public operator func ==(other: Flags): Bool
```

**Function:** Determines whether two enumeration values are equal.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Flags](#enum-flags) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func getValue()

```cangjie
public func getValue(): UInt32
```

**Function:** Gets the value represented by the current enumeration. Used to indicate the method for processing [Want](./cj-apis-app-ability-want.md#class-want).

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The value represented by the current enumeration. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported. | todo | todo |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the current enumeration. |

## enum Params

```cangjie
public enum Params <: Equatable<Params> & ToString {
    | AbilityBackToOtherMissionStack
    | AbilityRecoveryRestart
    | ContentTitleKey
    | ShareAbstractKey
    | ShareUrlKey
    | SupportContinuePageStackKey
    | SupportContinueSourceExitKey
    | ...
}
```

**Function:** [Want](./cj-apis-app-ability-want.md#class-want) Params operations.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parent Types:**

- [Equatable\<Params>](#enum-params)
- ToString

### AbilityBackToOtherMissionStack

```cangjie
AbilityBackToOtherMissionStack
```

**Function:** Indicates whether cross-mission stack return is supported. Value: ability.params.backToOtherMissionStack.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### AbilityRecoveryRestart

```cangjie
AbilityRecoveryRestart
```

**Function:** Indicates whether the current Ability has undergone a fault recovery restart. Value: ohos.ability.params.abilityRecoveryRestart.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### ContentTitleKey

```cangjie
ContentTitleKey
```

**Function:** Indicates the operation parameter for sharing titles supported by meta services. Value: ohos.extra.param.key.contentTitle.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### ShareAbstractKey

```cangjie
ShareAbstractKey
```

**Function:** Indicates the page source file. Value: ohos.param.atomicservice.pageSourceFile.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### ShareUrlKey

```cangjie
ShareUrlKey
```

**Function:** Indicates the operation parameter for sharing content supported by meta services. Value: ohos.extra.param.key.shareAbstract.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### SupportContinuePageStackKey

```cangjie
SupportContinuePageStackKey
```

**Function:** Indicates whether to migrate page stack information during cross-device migration. The default value is true, meaning page stack information is automatically migrated. Value: ohos.extra.param.key.supportContinuePageStack.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### SupportContinueSourceExitKey

```cangjie
SupportContinueSourceExitKey
```

**Function:** Indicates whether the source application exits during cross-device migration. The default value is true, meaning the source application exits automatically. Value: ohos.extra.param.key.supportContinueSourceExit.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

### func !=(Params)

```cangjie
public operator func !=(other: Params): Bool
```

**Function:** Determines whether two enumeration values are not equal.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Params](#enum-params) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are not equal, otherwise returns false. |

### func ==(Params)

```cangjie
public operator func ==(other: Params): Bool
```

**Function:** Determines whether two enumeration values are equal.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [Params](#enum-params) | Yes | - | Another enumeration value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enumeration values are equal, otherwise returns false. |

### func getValue()

```cangjie
public func getValue(): String
```

**Function:** Gets the value represented by the current enumeration. Used for [Want](./cj-apis-app-ability-want.md#class-want) Params operations.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The value represented by the current enumeration. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The type is not supported. | todo | todo |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**System Capability:** SystemCapability.Ability.AbilityBase

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string representation of the current enumeration. |
| Type       | Description                          |
|:-----------|:------------------------------------|
| String     | The string representation of the current enumeration. |
