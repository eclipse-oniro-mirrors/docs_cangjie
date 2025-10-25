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

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func createAbilityStageContextFromJSValue(JSContext, JSValue)

```cangjie
public func createAbilityStageContextFromJSValue(context: JSContext, input: JSValue): AbilityStageContext
```

**Function:** Converts from JSValue to AbilityStageContext type.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[AbilityStageContext](#class-abilitystagecontext)|Returns an instance of AbilityStageContext type.|

## func createApplicationContextFromJSValue(JSContext, JSValue)

```cangjie
public func createApplicationContextFromJSValue(context: JSContext, input: JSValue): ApplicationContext
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [ApplicationContext](#class-applicationcontext) type.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[ApplicationContext](#class-applicationcontext)|Returns an instance of ApplicationContext type.|

## func createContextFromJSValue(JSContext, JSValue)

```cangjie
public func createContextFromJSValue(context: JSContext, input: JSValue): Context
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [Context](./cj-apis-app-ability-ui_ability.md#class-context) type.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[Context](./cj-apis-app-ability-ui_ability.md#class-context)|Returns an instance of Context type.|

## func createUIAbilityContextFromJSValue(JSContext, JSValue)

```cangjie
public func createUIAbilityContextFromJSValue(context: JSContext, input: JSValue): UIAbilityContext
```

**Function:** Converts from [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue) to [UIAbilityContext](#class-uiabilitycontext) type.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|Yes|-|ArkTS interoperability context.|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|Yes|-|ArkTS unified type.|

**Return Value:**

|Type|Description|
|:----|:----|
|[UIAbilityContext](#class-uiabilitycontext)|Returns an instance of AbilityContext type.|

## interface SystemObjectInteropTypeToJS

```cangjie
public interface SystemObjectInteropTypeToJS {
    func toJSValue(context: JSContext): JSValue
}
```

**Function:** System object-specific extension interface for interoperability with [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### func toJSValue(JSContext)

```cangjie
func toJSValue(context: JSContext): JSValue
```

**Function:** Converts a Cangjie object to [JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|Yes|-|ArkTS interoperability context.|

**Return Value:**

|Type|Description|
|:----|:----|
|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|ArkTS unified type.|

## class Ability

```cangjie
abstract sealed class Ability {}
```

**Function:** Base class for [UIAbility](#class-uiability) and ExtensionAbility, providing system configuration update callbacks and system memory adjustment callbacks. Developers cannot directly inherit from this base class.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### static func registerCreator(String, () -> Ability)

```cangjie
public static func registerCreator(name: String, creator: () -> Ability): Unit
```

**Function:** Registers the corresponding creator for BaseAbility.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|name|String|Yes|-|Name of the registered UIAbility.|
|creator|()->[Ability](#class-ability)|Yes|-|Corresponding creator for BaseAbility registration.|

## class AbilityStageContext

```cangjie
public class AbilityStageContext <: Context {
    public var currentHapModuleInfo: HapModuleInfo
}
```

**Function:** [AbilityStageContext](#class-abilitystagecontext) provides the ability to access resources specific to `abilityStage`, including obtaining the `hapModuleInfo` object corresponding to AbilityStage and environment change objects.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### var currentHapModuleInfo

```cangjie
public var currentHapModuleInfo: HapModuleInfo
```

**Function:** `hapModuleInfo` object corresponding to AbilityStage.

**Type:** [HapModuleInfo](./cj-apis-bundle_manager.md#class-hapmoduleinfo)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## class ApplicationContext

```cangjie
public class ApplicationContext <: Context {}
```

**Function:** Provides application-level context capabilities.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

## class Context

```cangjie
public open class Context <: BaseContext {}
```

**Function:** Provides context capabilities for ability or application.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- [BaseContext](./cj-apis-app-ability.md#class-basecontext)

### prop applicationInfo

```cangjie
public prop applicationInfo: ApplicationInfo
```

**Function:** Information about the current application.

**Type:** [ApplicationInfo](./cj-apis-bundle_manager.md#class-applicationinfo)

**Access:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop area

```cangjie
public mut prop area: AreaMode
```

**Function:** File partition information.

**Type:** [AreaMode](./cj-apis-app-ability-context_constant.md#enum-areamode)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop filesDir

```cangjie
public prop filesDir: String
```

**Function:** File directory.

**Type:** String

**Access:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

### prop resourceManager

```cangjie
public prop resourceManager: ResourceManager
```

**Function:** Resource management object.

**Type:** [ResourceManager](../LocalizationKit/cj-apis-resource_manager.md#class-resourcemanager)

**Access:** Read-Only

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

## class UIAbility

```cangjie
public open class UIAbility <: Ability {}
```

**Function:** UIAbility is an application component containing UI interfaces, inheriting from BaseAbility. It provides lifecycle callbacks such as component creation, destruction, and foreground/background switching, as well as component collaboration capabilities. Component collaboration mainly provides the following common functions:

- Caller: Returned by the startAbilityByCall interface. CallerAbility (the caller) can use Caller to communicate with CalleeAbility (the callee).

- Callee: An internal object of UIAbility. CalleeAbility (the callee) can communicate with the Caller through Callee.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

**Parent Type:**

- [Ability](#class-ability)

### prop context

```cangjie
public mut prop context: UIAbilityContext
```

**Function:** Context.

**Type:** [UIAbilityContext](#class-uiabilitycontext)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### prop lastRequestWant

```cangjie
public mut prop lastRequestWant: Want
```

**Function:** Parameters from the last request of UIAbility.

**Type:** [Want](./cj-apis-app-ability-want.md#class-want)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### prop launchWant

```cangjie
public mut prop launchWant: Want
```

**Function:** Parameters when UIAbility is launched.

**Type:** [Want](./cj-apis-app-ability-want.md#class-want)

**Access:** Read-Write

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### func onBackground()

```cangjie
public open func onBackground(): Unit
```

**Function:** UIAbility lifecycle callback, triggered when the application transitions from foreground to background.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### func onCreate(Want, LaunchParam)

```cangjie
public open func onCreate(want: Want, launchParam: LaunchParam): Unit
```

**Function:** UIAbility creation callback, executing initialization business logic operations.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want type information of the current UIAbility, including UIAbility name, Bundle name, etc.|
|launchParam|[LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam)|Yes|-|Ability creation reason, last abnormal exit reason information.|

### func onDestroy()

```cangjie
public open func onDestroy(): Unit
```

**Function:** UIAbility destruction callback, executing resource cleanup and other operations.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### func onForeground()

```cangjie
public open func onForeground(): Unit
```

**Function:** UIAbility lifecycle callback, triggered when the application transitions from background to foreground.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

### func onNewWant(Want, LaunchParam)

```cangjie
public open func onNewWant(want: Want, launchParam: LaunchParam): Unit
```

**Function:** When a UIAbility instance has been started and run in the foreground, and then switched to the background for some reason, this method will be called upon restarting the UIAbility instance. That is, when the UIAbility instance is hot-started, it enters this lifecycle callback.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want type information of the current UIAbility, including ability name, bundle name, etc.|
|launchParam|[LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam)|Yes|-|Ability startup reason, last abnormal exit reason information.|

### func onWindowStageCreate(WindowStage)

```cangjie
public open func onWindowStageCreate(windowStage: WindowStage): Unit
```

**Function:** Called after WindowStage is created.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|windowStage|WindowStage|Yes|-|WindowStage related information.|

### func onWindowStageDestroy()

```cangjie
public open func onWindowStageDestroy(): Unit
```

**Function:** Called after WindowStage is destroyed.

**System Capability:** SystemCapability.Ability.AbilityRuntime.AbilityCore

**Since:** 21## class UIAbilityContext

```cangjie
public open class UIAbilityContext <: Context {}
```

**Description:** Provides the capability to access resources of a specific UIAbility.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parent Type:**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### func isTerminating()

```cangjie
public func isTerminating(): Bool
```

**Description:** Checks whether the ability is in the terminating state.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|true: The ability is currently in the terminating state; false: The ability is not in the terminating state.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000011 | The context does not exist. |

### func requestDialogService(Want, AsyncCallback\<RequestResult>)

```cangjie
public func requestDialogService(want: Want, result: AsyncCallback<RequestResult>): Unit
```

**Description:** Starts a ServiceExtensionAbility that supports modal dialogs and returns the result via callback.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want information of the target ServiceExtensionAbility to start.|
|result|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[RequestResult](./cj-apis-app-ability-dialog_request.md#class-requestresult)>|Yes|-|Callback for returning the result.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
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

### func startAbility(Want, ?StartOptions)

```cangjie
public func startAbility(want: Want, options!: ?StartOptions = None): Unit
```

**Description:** Starts an Ability with startup parameters.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want information of the Ability to start.|
|options|?[StartOptions](./cj-apis-app-ability-start_options.md#class-startoptions)|No|None|Parameters carried when starting the Ability.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
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

### func startAbilityForResult(Want, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, callback: AsyncCallback<AbilityResult>): Unit
```

**Description:** Starts an Ability and returns the execution result when the Ability exits (callback form).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want information of the Ability to start.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult)>|Yes|-|Callback function for the execution result.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
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

### func startAbilityForResult(Want, StartOptions, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback<AbilityResult>): Unit
```

**Description:** Starts an Ability and returns the execution result when the Ability exits (callback form).

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|Yes|-|Want information of the Ability to start.|
|options|StartOptions|Yes|-|Parameters carried when starting the Ability.|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<AbilityResult>|Yes|-|Callback function for the execution result.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | The application does not have permission to call the interface. |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
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

### func terminateSelf()

```cangjie
public func terminateSelf(): Unit
```

**Description:** Terminates the UIAbility itself.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |

### func terminateSelfWithResult(AbilityResult)

```cangjie
public func terminateSelfWithResult(parameter: AbilityResult): Unit
```

**Description:** Terminates the UIAbility and returns AbilityResult information to the caller when used with startAbilityForResult.

**System Capability:** SystemCapability.Ability.AbilityRuntime.Core

**Since:** 21

**Parameters:**

|Parameter|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|parameter|[AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult)|Yes|-|Terminates the Ability and returns AbilityResult information to the caller when used with startAbilityForResult.|

**Exceptions:**

- BusinessException: The error codes are as follows. For details, see [Universal Error Code Documentation](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |