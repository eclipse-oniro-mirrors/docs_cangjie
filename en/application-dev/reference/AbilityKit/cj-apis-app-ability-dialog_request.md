# ohos.app.ability.dialog_request

DialogRequest provides capabilities related to dialog requests, including request results and result codes.

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

For the aforementioned sample projects and configuration templates, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class RequestResult

```cangjie
public class RequestResult {
    public var result: ResultCode
    public var want: Want
}
```

**Description:** Request result, containing result code and Want information.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var result

```cangjie
public var result: ResultCode
```

**Description:** Result code.

**Type:** [ResultCode](#enum-resultcode)

**Access:** Read/Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var want

```cangjie
public var want: Want
```

**Description:** Want information.

**Type:** [Want](./cj-apis-app-ability-want.md#class-want)

**Access:** Read/Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum ResultCode

```cangjie
public enum ResultCode {
    | ResultOk
    | ResultCancel
    | ...
}
```

**Description:** Result code.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### ResultCancel

```cangjie
ResultCancel
```

**Description:** Canceled.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### ResultOk

```cangjie
ResultOk
```

**Description:** Success.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21