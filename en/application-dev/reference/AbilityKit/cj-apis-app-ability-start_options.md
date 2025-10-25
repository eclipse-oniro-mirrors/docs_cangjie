# ohos.app.ability.start_options

StartOptions provides the capability to configure Ability startup options, including window mode, display ID, and other settings.

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

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class StartOptions

```cangjie
public open class StartOptions {
    public var windowMode:?WindowMode
    public var displayId: Int32
    public init(
        windowMode!: ?WindowMode = None,
        displayId!: Int32 = 0
    )
}
```

**Description:** Startup options containing configurations such as window mode and display ID.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var displayId

```cangjie
public var displayId: Int32
```

**Description:** Display ID.

**Type:** Int32

**Readable/Writable:** Yes

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var windowMode

```cangjie
public var windowMode:?WindowMode
```

**Description:** Window mode.

**Type:** ?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode)

**Readable/Writable:** Yes

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### init(?WindowMode, Int32)

```cangjie
public init(
    windowMode!: ?WindowMode = None,
    displayId!: Int32 = 0
)
```

**Description:** Constructor to create a StartOptions instance.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| windowMode | ?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode) | No | None | Window mode. |
| displayId | Int32 | No | 0 | Display ID. |