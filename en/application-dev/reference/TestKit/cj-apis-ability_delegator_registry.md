# ohos.app.ability.ability_delegator_registry

The AbilityDelegatorRegistry module provides the capability to store registered [AbilityDelegator](#class-abilitydelegator) and [AbilityDelegatorArgs](#class-abilitydelegatorargs) objects in a global registry, including obtaining the application's [AbilityDelegator](#class-abilitydelegator) object and unit test parameter objects. The interfaces in this module can only be used within test frameworks.

## Importing the Module

```cangjie
import kit.TestKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of the example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#cangjie-example-code-instructions).

## class AbilityDelegator

```cangjie
public class AbilityDelegator {}
```

**Description:** AbilityDelegator is used to create and manage an [AbilityMonitor](#class-abilitymonitor) object (which monitors lifecycle state changes of a specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)), including adding and removing [AbilityMonitor](#class-abilitymonitor) instances, waiting for a [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) to reach the OnCreate lifecycle, setting wait times, obtaining the lifecycle state of a specified Ability, retrieving the top [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) of the current application, and starting a specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func addAbilityMonitor(AbilityMonitor)

```cangjie
public func addAbilityMonitor(monitor: AbilityMonitor): Unit
```

**Description:** Adds an [AbilityMonitor](#class-abilitymonitor) instance. Concurrent calls from multiple threads are not supported.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityMonitor](#class-abilitymonitor) | Yes | - | [AbilityMonitor](#class-abilitymonitor) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | AddAbilityMonitor failed. |

### func addAbilityStageMonitor(AbilityStageMonitor)

```cangjie
public func addAbilityStageMonitor(monitor: AbilityStageMonitor): Unit
```

**Description:** Adds an [AbilityStageMonitor](#class-abilitystagemonitor) object to monitor lifecycle state changes of a specified [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityStageMonitor](#class-abilitystagemonitor) | Yes | - | [AbilityStageMonitor](#class-abilitystagemonitor) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | AddAbilityStageMonitor failed. |

### func doAbilityBackground(UIAbility)

```cangjie
public func doAbilityBackground(ability: UIAbility): Unit
```

**Description:** Schedules the lifecycle state of the specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) to the Background state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| ability | [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) | Yes | - | [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) object. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | DoAbilityBackground failed. |

### func doAbilityForeground(UIAbility)

```cangjie
public func doAbilityForeground(ability: UIAbility): Unit
```

**Description:** Schedules the lifecycle state of the specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) to the Foreground state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| ability | [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) | Yes | - | [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) object. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | DoAbilityForeground failed. |

### func executeShellCommand(String, Int64)

```cangjie
public func executeShellCommand(cmd: String, timeoutSecs!: Int64 = 0): ShellCmdResult
```

**Description:** Executes the specified Shell command.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| cmd | String | Yes | - | Shell command string. |
| timeoutSecs | Int64 | No | 0 | Command timeout duration in seconds (s). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ShellCmdResult](#class-shellcmdresult) | Returns the Shell command execution result as a [ShellCmdResult](#class-shellcmdresult) object. |

### func finishTest(String, Int64)

```cangjie
public func finishTest(msg: String, code: Int64): Unit
```

**Description:** Ends the test and prints log information to the unit test terminal console.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| msg | String | Yes | - | Log string. |
| code | Int64 | Yes | - | Log code. |

### func getAbilityState(UIAbility)

```cangjie
public func getAbilityState(ability: UIAbility): AbilityLifecycleState
```

**Description:** Obtains the lifecycle state of the specified ability.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| ability | [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) | Yes | - | Specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) object. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [AbilityLifecycleState](#enum-abilitylifecyclestate) | Lifecycle state of the specified ability. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

### func getAppContext()

```cangjie
public func getAppContext(): Context
```

**Description:** Obtains the application Context.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) | Application Context. |

### func getCurrentTopAbility()

```cangjie
public func getCurrentTopAbility(): UIAbility
```

**Description:** Obtains the top [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) of the current application.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) | Returns the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | GetCurrentTopAbility failed. |

### func print(String)

```cangjie
public func print(msg: String): Unit
```

**Description:** Prints log information to the unit test terminal console.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| msg | String | Yes | - | Log string. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |

### func removeAbilityMonitor(AbilityMonitor)

```cangjie
public func removeAbilityMonitor(monitor: AbilityMonitor): Unit
```

**Description:** Removes an added [AbilityMonitor](#class-abilitymonitor) object.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityMonitor](#class-abilitymonitor) | Yes | - | [AbilityMonitor](#class-abilitymonitor) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | RemoveAbilityMonitor failed. |

### func removeAbilityStageMonitor(AbilityStageMonitor)

```cangjie
public func removeAbilityStageMonitor(monitor: AbilityStageMonitor): Unit
```

**Description:** Removes an added [AbilityStageMonitor](#class-abilitystagemonitor) object.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityStageMonitor](#class-abilitystagemonitor) | Yes | - | [AbilityStageMonitor](#class-abilitystagemonitor) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | RemoveAbilityStageMonitor failed. |

### func startAbility(Want)

```cangjie
public func startAbility(want: Want): Future<Unit>
```

**Description:** Starts the specified [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| want | [Want](../AbilityKit/cj-apis-app-ability-want.md#class-want) | Yes | - | Parameters for starting the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability). |

### func waitAbilityMonitor(AbilityMonitor, Int64)

```cangjie
public func waitAbilityMonitor(monitor: AbilityMonitor, timeout!: Int64 = 5000): UIAbility
```

**Description:** Sets a wait time and waits for the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) matching the [AbilityMonitor](#class-abilitymonitor) instance to reach the [onCreate](../AbilityKit/cj-apis-app-ability-ui_ability.md#func-oncreatewant-launchparam) lifecycle, then returns the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) instance.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityMonitor](#class-abilitymonitor) | Yes | - | [AbilityMonitor](#class-abilitymonitor) instance. |
| timeout | Int64 | No | 5000 | Maximum wait time in milliseconds (ms). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) | Returns the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) instance. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified. 2. Incorrect parameter types. |
  | 16000100 | WaitAbilityMonitor failed. |

### func waitAbilityStageMonitor(AbilityStageMonitor, Int64)

```cangjie
public func waitAbilityStageMonitor(monitor: AbilityStageMonitor, timeout!: Int64 = 5000): AbilityStage
```

**Description:** Waits for and returns the [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage) object that matches the conditions set in the given [AbilityStageMonitor](#class-abilitystagemonitor).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

| Name | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| monitor | [AbilityStageMonitor](#class-abilitystagemonitor) | Yes | - | [AbilityStageMonitor](#class-abilitystagemonitor) instance. |
| timeout | Int64 | No | 5000 | Maximum timeout wait time in milliseconds (ms). |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage) | Returns the [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage) object. |

**Exceptions:**

For detailed error code descriptions, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](../AbilityKit/cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401## class AbilityDelegatorArgs

```cangjie
public class AbilityDelegatorArgs {}
```

**Description:** Test parameter information.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop bundleName

```cangjie
public mut prop bundleName: String
```

**Description:** The package name of the currently tested application.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop parameters

```cangjie
public mut prop parameters: HashMap<String,String>
```

**Description:** Parameters for launching the current unit test.

**Type:** HashMap\<String,String>

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop testCaseNames

```cangjie
public mut prop testCaseNames: String
```

**Description:** Test case names.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop testRunnerClassName

```cangjie
public mut prop testRunnerClassName: String
```

**Description:** The name of the test runner that executes the test cases.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## class AbilityDelegatorRegistry

```cangjie
public class AbilityDelegatorRegistry {}
```

**Description:** [AbilityDelegatorRegistry](#class-abilitydelegatorregistry) provides the capability to store registered [AbilityDelegator](#class-abilitydelegator) and [AbilityDelegatorArgs](#class-abilitydelegatorargs) objects in a global registry.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### static func getAbilityDelegator()

```cangjie
public static func getAbilityDelegator(): AbilityDelegator
```

**Description:** Obtains the [AbilityDelegator](#class-abilitydelegator) object of the application, which can be used to dispatch test framework-related functionalities.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|[AbilityDelegator](#class-abilitydelegator)|The [AbilityDelegator](#class-abilitydelegator) object, which can be used to dispatch test framework-related functionalities.|

### static func getArguments()

```cangjie
public static func getArguments(): AbilityDelegatorArgs
```

**Description:** Obtains the unit test parameter [AbilityDelegatorArgs](#class-abilitydelegatorargs) object.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|[AbilityDelegatorArgs](#class-abilitydelegatorargs)|The [AbilityDelegatorArgs](#class-abilitydelegatorargs) object, which can be used to obtain test parameters.|

## class AbilityMonitor

```cangjie
public class AbilityMonitor <: FFIData {
    public var abilityName: String
    public var moduleName: String
    public var onAbilityCreate:?(UIAbility) -> Unit
    public var onAbilityForeground:?(UIAbility) -> Unit
    public var onAbilityBackground:?(UIAbility) -> Unit
    public var onAbilityDestroy:?(UIAbility) -> Unit
    public var onWindowStageCreate:?(UIAbility) -> Unit
    public var onWindowStageRestore:?(UIAbility) -> Unit
    public var onWindowStageDestroy:?(UIAbility) -> Unit
    public init(
        abilityName: String,
        moduleName!: String = "",
        onAbilityCreate!: ?(UIAbility) -> Unit = None,
        onAbilityForeground!: ?(UIAbility) -> Unit = None,
        onAbilityBackground!: ?(UIAbility) -> Unit = None,
        onAbilityDestroy!: ?(UIAbility) -> Unit = None,
        onWindowStageCreate!: ?(UIAbility) -> Unit = None,
        onWindowStageRestore!: ?(UIAbility) -> Unit = None,
        onWindowStageDestroy!: ?(UIAbility) -> Unit = None
    )
}
```

**Description:** The [AbilityMonitor](#class-abilitymonitor) module provides the capability to match ability objects that meet specified conditions. The most recently matched ability object will be stored in [AbilityMonitor](#class-abilitymonitor).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- FFIData

### var abilityName

```cangjie
public var abilityName: String
```

**Description:** The name of the ability bound to the current [AbilityMonitor](#class-abilitymonitor).

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var moduleName

```cangjie
public var moduleName: String
```

**Description:** The module name bound to the current [AbilityMonitor](#class-abilitymonitor).

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onAbilityBackground

```cangjie
public var onAbilityBackground:?(UIAbility) -> Unit
```

**Description:** Callback function when the ability state changes to background. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onAbilityCreate

```cangjie
public var onAbilityCreate:?(UIAbility) -> Unit
```

**Description:** Callback function when the ability is initialized. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onAbilityDestroy

```cangjie
public var onAbilityDestroy:?(UIAbility) -> Unit
```

**Description:** Callback function before the ability is destroyed. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onAbilityForeground

```cangjie
public var onAbilityForeground:?(UIAbility) -> Unit
```

**Description:** Callback function when the ability state changes to foreground. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onWindowStageCreate

```cangjie
public var onWindowStageCreate:?(UIAbility) -> Unit
```

**Description:** Callback function when the window stage is created. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onWindowStageDestroy

```cangjie
public var onWindowStageDestroy:?(UIAbility) -> Unit
```

**Description:** Callback function before the window stage is destroyed. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var onWindowStageRestore

```cangjie
public var onWindowStageRestore:?(UIAbility) -> Unit
```

**Description:** Callback function when the window stage is restored. If this property is not set, the lifecycle callback will not be received.

**Type:** ?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability))->Unit

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### init(String, String, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit, ?(UIAbility) -> Unit)

```cangjie
public init(
    abilityName: String,
    moduleName!: String = "",
    onAbilityCreate!: ?(UIAbility) -> Unit = None,
    onAbilityForeground!: ?(UIAbility) -> Unit = None,
    onAbilityBackground!: ?(UIAbility) -> Unit = None,
    onAbilityDestroy!: ?(UIAbility) -> Unit = None,
    onWindowStageCreate!: ?(UIAbility) -> Unit = None,
    onWindowStageRestore!: ?(UIAbility) -> Unit = None,
    onWindowStageDestroy!: ?(UIAbility) -> Unit = None
)
```

**Description:** Constructs an [AbilityMonitor](#class-abilitymonitor) object.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|abilityName|String|Yes|-|The name of the ability bound to the current [AbilityMonitor](#class-abilitymonitor).|
|moduleName|String|No|""| **Named parameter.** The module name bound to the current [AbilityMonitor](#class-abilitymonitor).|
|onAbilityCreate|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function when the ability is initialized. None means this property is not set, and the lifecycle callback will not be received.|
|onAbilityForeground|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function when the ability state changes to foreground. None means this property is not set, and the lifecycle callback will not be received.|
|onAbilityBackground|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function when the ability state changes to background. None means this property is not set, and the lifecycle callback will not be received.|
|onAbilityDestroy|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function before the ability is destroyed. None means this property is not set, and the lifecycle callback will not be received.|
|onWindowStageCreate|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function when the window stage is created. None means this property is not set, and the lifecycle callback will not be received.|
|onWindowStageRestore|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function when the window stage is restored. None means this property is not set, and the lifecycle callback will not be received.|
|onWindowStageDestroy|?([UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability)) -> Unit|No|None| **Named parameter.** Callback function before the window stage is destroyed. None means this property is not set, and the lifecycle callback will not be received.|

## class AbilityStageMonitor

```cangjie
public class AbilityStageMonitor <: FFIData {
    public var moduleName: String
    public var srcEntrance: String
    public init(
        moduleName: String,
        srcEntrance: String
    )
}
```

**Description:** The [AbilityStageMonitor](#class-abilitystagemonitor) module provides the capability to match [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage) objects that meet specified conditions. The most recently matched [AbilityStage](../AbilityKit/cj-apis-app-ability-ability_stage.md#class-abilitystage) object will be stored in [AbilityStageMonitor](#class-abilitystagemonitor).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- FFIData

### var moduleName

```cangjie
public var moduleName: String
```

**Description:** The module name of the abilityStage to be monitored.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### var srcEntrance

```cangjie
public var srcEntrance: String
```

**Description:** The source path of the abilityStage to be monitored.

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### init(String, String)

```cangjie
public init(
    moduleName: String,
    srcEntrance: String
)
```

**Description:** Constructs an [AbilityStageMonitor](#class-abilitystagemonitor) object.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default Value|Description|
|:---|:---|:---|:---|:---|
|moduleName|String|Yes|-|The module name of the abilityStage to be monitored.|
|srcEntrance|String|Yes|-|The source path of the abilityStage to be monitored.|## class ShellCmdResult

```cangjie
public class ShellCmdResult {}
```

**Function:** Shell command execution result.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop exitCode

```cangjie
public mut prop exitCode: Int32
```

**Function:** Result code.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop stdResult

```cangjie
public mut prop stdResult: String
```

**Function:** Standard output content.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## enum AbilityLifecycleState

```cangjie
public enum AbilityLifecycleState <: Equatable<AbilityLifecycleState> & ToString {
    | Uninitialized
    | Create
    | Foreground
    | Background
    | Destroy
    | ...
}
```

**Function:** [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) lifecycle states. This enumeration type can be used with the [getAbilityState](#func-getabilitystateuiability) method of [AbilityDelegator](#class-abilitydelegator) to return different ability lifecycle states.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Types:**

- Equatable\<AbilityLifecycleState>
- ToString

### Background

```cangjie
Background
```

**Function:** Indicates the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is in background state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Create

```cangjie
Create
```

**Function:** Indicates the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is in created state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Destroy

```cangjie
Destroy
```

**Function:** Indicates the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is in destroyed state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Foreground

```cangjie
Foreground
```

**Function:** Indicates the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is in foreground state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### Uninitialized

```cangjie
Uninitialized
```

**Function:** Indicates the [UIAbility](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiability) is in invalid state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func !=(AbilityLifecycleState)

```cangjie
public operator func !=(other: AbilityLifecycleState): Bool
```

**Function:** Determines whether two enumeration values are unequal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[AbilityLifecycleState](#enum-abilitylifecyclestate)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are unequal, otherwise returns false.|

### func ==(AbilityLifecycleState)

```cangjie
public operator func ==(other: AbilityLifecycleState): Bool
```

**Function:** Determines whether two enumeration values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[AbilityLifecycleState](#enum-abilitylifecyclestate)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the current enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the current enumeration.|