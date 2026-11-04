# ohos.app.ability.start_options

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

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

- If the first line of sample code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](./cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

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

**Function:** Startup options containing configurations such as window mode and display ID.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### var displayId

```cangjie
public var displayId: Int32
```

**Function:** Display ID.

**Type:** Int32

**Readable/Writable:** Yes

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### var windowMode

```cangjie
public var windowMode:?WindowMode
```

**Function:** Window mode.

**Type:** ?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode)

**Readable/Writable:** Yes

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### init(?WindowMode, Int32)

```cangjie
public init(
    windowMode!: ?WindowMode = None,
    displayId!: Int32 = 0
)
```

**Function:** Constructor to create a StartOptions instance.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| windowMode | ?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode) | No | None | Window mode. |
| displayId | Int32 | No | 0 | Display ID. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let startOptions = StartOptions(WindowMode.FullScreen, 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```