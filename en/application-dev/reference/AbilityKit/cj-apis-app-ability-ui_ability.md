# ohos.app.ability.ui_ability

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

For details about the sample project and configuration template mentioned above, see [Cangjie Sample Code Description](../cj-development-intro.md#Cangjie-Sample-Code-Description).

## func createAbilityStageContextFromJSValue(JSContext, JSValue)

```cangjie
public func createAbilityStageContextFromJSValue(context: JSContext, input: JSValue): AbilityStageContext
```

**Function:** Converts from JSValue to AbilityStageContext type. This conversion can only be used in function passing.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [AbilityStageContext](#class-abilitystagecontext) | Returns an instance of AbilityStageContext type. |

**Example:**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyAbilityStage <: AbilityStage {
        public override func onCreate(): Unit {
            let jsContext = JSRuntime.getCurrentContext()
            let input = this.context.toJSValue(jsContext)
            let ctx = createAbilityStageContextFromJSValue(JjsContext, input)
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createApplicationContextFromJSValue(JSContext, JSValue)

```cangjie
public func createApplicationContextFromJSValue(context: JSContext, input: JSValue): ApplicationContext
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [ApplicationContext](#class-applicationcontext) type. This conversion can only be used in function passing.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [ApplicationContext](#class-applicationcontext) | Returns an instance of ApplicationContext type. |

**Example:**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyAbilityStage <: AbilityStage {
        public override func onCreate(): Unit {
            let jsContext = JSRuntime.getCurrentContext()
            let input = AbilityDelegatorRegistry.getAbilityDelegator().getAppContext().toJSValue(jsContext)
            let ctx = createApplicationContextFromJSValue(JjsContext, input)
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createContextFromJSValue(JSContext, JSValue)

```cangjie
public func createContextFromJSValue(context: JSContext, input: JSValue): Context
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [Context](./cj-apis-app-ability-ui_ability.md#class-context) type. This conversion can only be used in function passing.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Context](./cj-apis-app-ability-ui_ability.md#class-context) | Returns an instance of Context type. |

**Example:**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyAbilityStage <: AbilityStage {
        public override func onCreate(): Unit {
            let jsContext = JSRuntime.getCurrentContext()
            let input = this.context.toJSValue(jsContext)
            let ctx = createContextFromJSValue(JjsContext, input)
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func createUIAbilityContextFromJSValue(JSContext, JSValue)

```cangjie
public func createUIAbilityContextFromJSValue(context: JSContext, input: JSValue): UIAbilityContext
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [UIAbilityContext](#class-uiabilitycontext) type.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext) | Yes | - | ArkTS interoperability context. |
| input | [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) | Yes | - | ArkTS unified type. |

**Return Value:**

| Type | Description |
|:----|:----|
| [UIAbilityContext](#class-uiabilitycontext) | Returns an instance of AbilityContext type. |

**Example:**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let jsContext = JSRuntime.getCurrentContext()
            let input = this.context.toJSValue(jsContext)
            let ctx = createContextFromJSValue(JjsContext, input)
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## interface SystemObjectInteropTypeToJS

```cangjie
public interface SystemObjectInteropTypeToJS {
    func toJSValue(context: JSContext): JSValue
}
```

**Function:** A dedicated extension interface for system objects to achieve interconversion with [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

### func toJSValue(JSContext)

```cangjie
func toJSValue(context: JSContext): JSValue
```

**Function:** Converts a Cangjie object to [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| context | [JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext) | Yes | - | ArkTS interoperability context. |

**Return Value:**

| Type | Description |
|:----|:----|
| [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) | ArkTS unified type. |

## class Ability

```cangjie
abstract sealed class Ability {}
```

**Function:** Base class for [UIAbility](#class-uiability) and ExtensionAbility, providing system configuration update callbacks and system memory adjustment callbacks. Developers cannot directly inherit from this base class.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

### static func registerCreator(String, () -> Ability)

```cangjie
public static func registerCreator(name: String, creator: () -> Ability): Unit
```

**Function:** Registers the corresponding creator for BaseAbility.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name of the registered UIAbility. |
| creator | ()->[Ability](#class-ability) | Yes | - | Corresponding creator for BaseAbility. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ENTRY_ABILITY_REGISTER_RESULT = Ability.registerCreator("entry", () -> MyUIAbility)

    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class AbilityStageContext

```cangjie
public class AbilityStageContext <: Context {
    public var currentHapModuleInfo: HapModuleInfo
}
```

**Function:** [AbilityStageContext](#class-abilitystagecontext) provides the ability to access resources specific to `abilityStage`, including obtaining the `hapModuleInfo` object corresponding to AbilityStage and environment change objects.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### var currentHapModuleInfo

```cangjie
public var currentHapModuleInfo: HapModuleInfo
```

**Function:** The `hapModuleInfo` object corresponding to AbilityStage.

**Type:** [HapModuleInfo](./cj-apis-bundle_manager.md#class-hapmoduleinfo)

**Read/Write Permission:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyAbilityStage <: AbilityStage {
        public override func onCreate(): Unit {
            let info = this.context.currentHapModuleInfo
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class ApplicationContext

```cangjie
public class ApplicationContext <: Context {}
```

**Function:** Provides capabilities for application-level context.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

## class Context

```cangjie
public open class Context <: BaseContext {}
```

**Function:** Provides capabilities for ability or application context.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parent Type:**

- [BaseContext](./cj-apis-app-ability.md#class-basecontext)

### prop applicationInfo

```cangjie
public prop applicationInfo: ApplicationInfo
```

**Function:** Information about the current application.

**Type:** [ApplicationInfo](./cj-apis-bundle_manager.md#class-applicationinfo)

**Read/Write Permission:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let info = this.context.applicationInfo
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### prop area

```cangjie
public mut prop area: AreaMode
```

**Function:** File partition information.

**Type:** [AreaMode](./cj-apis-app-ability-context_constant.md#enum-areamode)

**Read/Write Permission:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let area = this.context.area
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### prop filesDir

```cangjie
public prop filesDir: String
```

**Function:** File directory.

**Type:** String

**Read/Write Permission:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let filesDir = this.context.filesDir
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### prop resourceManager

```cangjie
public prop resourceManager: ResourceManager
```

**Function:** Resource management object.

**Type:** [ResourceManager](../LocalizationKit/cj-apis-resource_manager.md#class-resourcemanager)

**Read/Write Permission:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let resourceManager = this.context.resourceManager
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class UIAbility

```cangjie
public open class UIAbility <: Ability {}
```

**Description:** UIAbility is an application component containing UI interfaces, inheriting from BaseAbility. It provides lifecycle callbacks for component creation, destruction, foreground/background switching, and also possesses component collaboration capabilities. Component collaboration primarily offers the following common functionalities:

- Caller: Returned by the startAbilityByCall interface. CallerAbility (the caller) can use Caller to communicate with CalleeAbility (the callee).

- Callee: An internal object of UIAbility. CalleeAbility (the callee) can communicate with the Caller through Callee.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Parent Type:**

- [Ability](#class-ability)

### prop context

```cangjie
public mut prop context: UIAbilityContext
```

**Description:** The context.

**Type:** [UIAbilityContext](#class-uiabilitycontext)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let context = this.context
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### prop lastRequestWant

```cangjie
public mut prop lastRequestWant: Want
```

**Description:** The parameters when the UIAbility was last requested.

**Type:** [Want](./cj-apis-app-ability-want.md#class-want)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let lastRequestWant = this.lastRequestWant
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### prop launchWant

```cangjie
public mut prop launchWant: Want
```

**Description:** The parameters when the UIAbility is launched.

**Type:** [Want](./cj-apis-app-ability-want.md#class-want)

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let launchWant = this.launchWant
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onBackground()

```cangjie
public open func onBackground(): Unit
```

**Description:** UIAbility lifecycle callback, triggered when the application transitions from foreground to background.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override onBackground() {
            let launchWant = this.launchWant
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onCreate(Want, LaunchParam)

```cangjie
public open func onCreate(want: Want, launchParam: LaunchParam): Unit
```

**Description:** UIAbility creation callback, executes initialization business logic operations.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | Want type information of the current UIAbility, including UIAbility name, Bundle name, etc. |
| launchParam | [LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam) | Yes | - | Information about the reason for creating the ability and the last abnormal exit. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
            let launchWant = this.launchWant
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onDestroy()

```cangjie
public open func onDestroy(): Unit
```

**Description:** UIAbility destruction callback, executes resource cleanup and other operations.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onDestroy(): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onForeground()

```cangjie
public open func onForeground(): Unit
```

**Description:** UIAbility lifecycle callback, triggered when the application transitions from background to foreground.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onForeground(): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onNewWant(Want, LaunchParam)

```cangjie
public open func onNewWant(want: Want, launchParam: LaunchParam): Unit
```

**Description:** When a UIAbility instance has been started and run in the foreground, and then switched to the background for some reason, this method will be called upon restarting the UIAbility instance. That is, this lifecycle callback is entered during hot start of the UIAbility instance.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | Want type information of the current UIAbility, including ability name, bundle name, etc. |
| launchParam | [LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam) | Yes | - | Information about the reason for starting the Ability and the last abnormal exit. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onNewWant(want: Want, launchParam: LaunchParam): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onWindowStageCreate(WindowStage)

```cangjie
public open func onWindowStageCreate(windowStage: WindowStage): Unit
```

**Description:** Called when WindowStage is created.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| windowStage | WindowStage | Yes | - | Information about WindowStage. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func onWindowStageDestroy()

```cangjie
public open func onWindowStageDestroy(): Unit
```

**Description:** Called when WindowStage is destroyed.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 22

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageDestroy(): Unit {
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## class UIAbilityContext

```cangjie
public open class UIAbilityContext <: Context {}
```

**Description:** Provides the capability to access resources specific to a UIAbility.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### func isTerminating()

```cangjie
public func isTerminating(): Bool
```

**Description:** Queries whether the ability is in the terminating state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: The ability is currently in the terminating state; false: Not in the terminating state. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000011 | The context does not exist. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            let isTerminating = this.context.isTerminating()
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func requestDialogService(Want, AsyncCallback\<RequestResult>)

```cangjie
public func requestDialogService(want: Want, result: AsyncCallback<RequestResult>): Unit
```

**Function:** Starts a ServiceExtensionAbility that supports modal dialogs and returns the result via callback.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | The Want information of the target ServiceExtensionAbility to start. |
| result | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[RequestResult](./cj-apis-app-ability-dialog_request.md#class-requestresult)> | Yes | - | Callback for returning the result. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 16000001 | The specified ability does not exist. |
  | 16000002 | Incorrect ability type. |
  | 16000004 | Cannot start an invisible component. |
  | 16000005 | The specified process does not have the permission. |
  | 16000006 | Cross-user operations are not allowed. |
  | 16000008 | The crowdtesting application expires. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000010 | The call with the continuation and prepare continuation flag is forbidden. |
  | 16000011 | The context does not exist. |
  | 16000012 | The application is controlled. |
  | 16000013 | The application is controlled by EDM. |
  | 16000050 | Internal error. |
  | 16000053 | The ability is not on the top of the UI. |
  | 16000055 | Installation-free timed out. |
  | 16200001 | The caller has been released. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
            this.context.requestDialogService(Want(), (err: ?BusinessException, data: ?RequestResult) => {})
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func startAbility(Want, ?StartOptions)

```cangjie
public func startAbility(want: Want, options!: ?StartOptions = None): Unit
```

**Function:** Starts an Ability with startup parameters.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | The Want information of the Ability to start. |
| options | ?[StartOptions](./cj-apis-app-ability-start_options.md#class-startoptions) | No | None | Parameters carried when starting the Ability. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 801 | Capability not support. |
  | 16000001 | The specified ability does not exist. |
  | 16000002 | Incorrect ability type. |
  | 16000004 | Cannot start an invisible component. |
  | 16000005 | The specified process does not have the permission. |
  | 16000006 | Cross-user operations are not allowed. |
  | 16000008 | The crowdtesting application expires. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000010 | The call with the continuation and prepare continuation flag is forbidden. |
  | 16000011 | The context does not exist. |
  | 16000012 | The application is controlled. |
  | 16000013 | The application is controlled by EDM. |
  | 16000018 | Redirection to a third-party application is not allowed in API version greater than 11. |
  | 16000019 | No matching ability is found. |
  | 16000050 | Internal error. |
  | 16000053 | The ability is not on the top of the UI. |
  | 16000055 | Installation-free timed out. |
  | 16000067 | The StartOptions check failed. |
  | 16000068 | The ability is already running. |
  | 16000071 | App clone is not supported. |
  | 16000072 | App clone or multi-instance is not supported. |
  | 16000073 | The app clone index is invalid. |
  | 16000076 | The app instance key is invalid. |
  | 16000077 | The number of app instances reaches the limit. |
  | 16000078 | The multi-instance is not supported. |
  | 16000079 | The APP_INSTANCE_KEY cannot be specified. |
  | 16000080 | Creating a new instance is not supported. |
  | 16200001 | The caller has been released. |
  | 16300003 | The target application is not the current application. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
              this.context.startAbility(Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"))
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func startAbilityForResult(Want, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, callback: AsyncCallback<AbilityResult>): Unit
```

**Function:** Starts an Ability and returns the execution result when the Ability exits (callback form).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | The Want information of the Ability to start. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult)> | Yes | - | Callback function for the execution result. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 16000001 | The specified ability does not exist. |
  | 16000002 | Incorrect ability type. |
  | 16000004 | Cannot start an invisible component. |
  | 16000005 | The specified process does not have the permission. |
  | 16000006 | Cross-user operations are not allowed. |
  | 16000008 | The crowdtesting application expires. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000010 | The call with the continuation and prepare continuation flag is forbidden. |
  | 16000011 | The context does not exist. |
  | 16000012 | The application is controlled. |
  | 16000013 | The application is controlled by EDM. |
  | 16000018 | Redirection to a third-party application is not allowed in API version greater than 11. |
  | 16000019 | No matching ability is found. |
  | 16000050 | Internal error. |
  | 16000053 | The ability is not on the top of the UI. |
  | 16000055 | Installation-free timed out. |
  | 16000071 | App clone is not supported. |
  | 16000072 | App clone or multi-instance is not supported. |
  | 16000073 | The app clone index is invalid. |
  | 16000076 | The app instance key is invalid. |
  | 16000077 | The number of app instances reaches the limit. |
  | 16000078 | The multi-instance is not supported. |
  | 16000079 | The APP_INSTANCE_KEY cannot be specified. |
  | 16000080 | Creating a new instance is not supported. |
  | 16200001 | The caller has been released. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
              this.context.startAbilityForResult(
                  Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"),
                  (err: ?BusinessException, data: ?AbilityResult) => {})
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func startAbilityForResult(Want, StartOptions, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback<AbilityResult>): Unit
```

**Function:** Starts an Ability and returns the execution result when the Ability exits (callback form).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| want | [Want](./cj-apis-app-ability-want.md#class-want) | Yes | - | The Want information of the Ability to start. |
| options | StartOptions | Yes | - | Parameters carried when starting the Ability. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<AbilityResult> | Yes | - | Callback function for the execution result. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md) and [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 16000001 | The specified ability does not exist. |
  | 16000004 | Cannot start an invisible component. |
  | 16000005 | The specified process does not have the permission. |
  | 16000006 | Cross-user operations are not allowed. |
  | 16000008 | The crowdtesting application expires. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000012 | The application is controlled. |
  | 16000013 | The application is controlled by EDM. |
  | 16000018 | Redirection to a third-party application is not allowed in API version greater than 11. |
  | 16000019 | No matching ability is found. |
  | 16000050 | Internal error. |
  | 16000053 | The ability is not on the top of the UI. |
  | 16000055 | Installation-free timed out. |
  | 16000071 | App clone is not supported. |
  | 16000072 | App clone or multi-instance is not supported. |
  | 16000073 | The app clone index is invalid. |
  | 16000076 | The app instance key is invalid. |
  | 16000077 | The number of app instances reaches the limit. |
  | 16000078 | The multi-instance is not supported. |
  | 16000079 | The APP_INSTANCE_KEY cannot be specified. |
  | 16000080 | Creating a new instance is not supported. |
  | 16200001 | The caller has been released. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
              this.context.startAbilityForResult(
                  Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"), StartOptions(),
                  (err: ?BusinessException, data: ?AbilityResult) => {})
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func terminateSelf()

```cangjie
public func terminateSelf(): Unit
```

**Function:** Terminates the UIAbility itself.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
              this.context.terminateSelf()
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func terminateSelfWithResult(AbilityResult)

```cangjie
public func terminateSelfWithResult(parameter: AbilityResult): Unit
```

**Function:** Terminates the UIAbility and returns AbilityResult information to the caller when used with startAbilityForResult.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| parameter | [AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult) | Yes | - | Terminates the Ability and returns AbilityResult information to the caller when used with startAbilityForResult. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [Ability Subsystem Error Codes](./cj-errorcode-ability.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |

**Example:**

<!-- compile -->
```cangjie
import kit.AbilityKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    class MyUIAbility <: UIAbility {
        public override func onWindowStageCreate(windowStage: WindowStage): Unit {
              this.context.terminateSelfWithResult(AbilityResult(0))
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```