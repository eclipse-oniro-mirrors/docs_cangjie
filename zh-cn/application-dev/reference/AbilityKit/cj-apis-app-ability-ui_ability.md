# ohos.app.ability.ui_ability

AbilityConstant提供Ability相关的枚举，包括应用启动原因LaunchReason、上次退出原因LastExitReason、迁移结果OnContinueResult等。

## 导入模块

```cangjie
import kit.AbilityKit.*
```

## 权限列表

ohos.permission.DISTRIBUTED_DATASYNC

ohos.permission.PREPARE_APP_TERMINATE

ohos.permission.PRIVACY_WINDOW

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](./cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func createAbilityStageContextFromJSValue(JSContext, JSValue)

```cangjie
public func createAbilityStageContextFromJSValue(context: JSContext, input: JSValue): AbilityStageContext
```

**功能：** 从JSValue转换为AbilityStageContext类型。该转换仅可在函数传递中使用。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|是|-|ArkTS互操作上下文。|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|是|-|ArkTS统一类型。|

**返回值：**

|类型|说明|
|:----|:----|
|[AbilityStageContext](#class-abilitystagecontext)|返回AbilityStageContext类型实例。|

**示例：**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*

class MyAbilityStage <: AbilityStage {
    public override func onCreate(): Unit {
        let jsContext = JSRuntime.getCurrentContext()
        let input = this.context.toJSValue(jsContext)
        let ctx = createAbilityStageContextFromJSValue(JjsContext, input)
    }
}
```

## func createApplicationContextFromJSValue(JSContext, JSValue)

```cangjie
public func createApplicationContextFromJSValue(context: JSContext, input: JSValue): ApplicationContext
```

**功能：** 从[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)转换为[ApplicationContext](#class-applicationcontext)类型。该转换仅可在函数传递中使用。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|是|-| ArkTS互操作上下文。|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|是|-|ArkTS统一类型。|

**返回值：**

|类型|说明|
|:----|:----|
|[ApplicationContext](#class-applicationcontext)|返回 ApplicationContext 类型实例。|

**示例：**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*

class MyAbilityStage <: AbilityStage {
    public override func onCreate(): Unit {
        let jsContext = JSRuntime.getCurrentContext()
        let input = AbilityDelegatorRegistry.getAbilityDelegator().getAppContext().toJSValue(jsContext)
        let ctx = createApplicationContextFromJSValue(JjsContext, input)
    }
}
```

## func createContextFromJSValue(JSContext, JSValue)

```cangjie
public func createContextFromJSValue(context: JSContext, input: JSValue): Context
```

**功能：** 从[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)转换为[Context](./cj-apis-app-ability-ui_ability.md#class-context)类型。该转换仅可在函数传递中使用。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|是|-| ArkTS互操作上下文。|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|是|-| ArkTS统一类型。|

**返回值：**

|类型|说明|
|:----|:----|
|[Context](./cj-apis-app-ability-ui_ability.md#class-context)|返回Context类型实例。|

**示例：**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*

class MyAbilityStage <: AbilityStage {
    public override func onCreate(): Unit {
        let jsContext = JSRuntime.getCurrentContext()
        let input = this.context.toJSValue(jsContext)
        let ctx = createContextFromJSValue(JjsContext, input)
    }
}
```

## func createUIAbilityContextFromJSValue(JSContext, JSValue)

```cangjie
public func createUIAbilityContextFromJSValue(context: JSContext, input: JSValue): UIAbilityContext
```

**功能：** 从[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)转换为[UIAbilityContext](#class-uiabilitycontext)类型。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|是|-|ArkTS互操作上下文。|
|input|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|是|-|ArkTS统一类型。|

**返回值：**

|类型|说明|
|:----|:----|
|[UIAbilityContext](#class-uiabilitycontext)|返回AbilityContext类型实例。|

**示例：**

<!-- compile -->
```cangjie
import ohos.ark_interop.*
import ohos.ark_interop_helper.*
import kit.AbilityKit.*
import kit.TestKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let jsContext = JSRuntime.getCurrentContext()
        let input = this.context.toJSValue(jsContext)
        let ctx = createContextFromJSValue(JjsContext, input)
    }
}
```

## interface SystemObjectInteropTypeToJS

```cangjie
public interface SystemObjectInteropTypeToJS {
    func toJSValue(context: JSContext): JSValue
}
```

**功能：** 系统对象专用的拓展接口，以实现与[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)的互转。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### func toJSValue(JSContext)

```cangjie
func toJSValue(context: JSContext): JSValue
```

**功能：** 将仓颉对象转换成[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|context|[JSContext](../arkinterop/cj-apis-ark_interop.md#class-jscontext)|是|-|ArkTS互操作上下文。|

**返回值：**

|类型|说明|
|:----|:----|
|[JSValue](../arkinterop/cj-apis-ark_interop.md#struct-jsvalue)|ArkTS统一类型。|

## class Ability

```cangjie
abstract sealed class Ability {}
```

**功能：** [UIAbility](#class-uiability)和ExtensionAbility的基类，提供系统配置更新回调和系统内存调整回调。不支持开发者直接继承该基类。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

### static func registerCreator(String, () -> Ability)

```cangjie
public static func registerCreator(name: String, creator: () -> Ability): Unit
```

**功能：** 注册BaseAbility的对应的creator。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|name|String|是|-|注册 UIAbility 的名称。|
|creator|()->[Ability](#class-ability)|是|-|注册BaseAbility的对应的creator。|

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

let ENTRY_ABILITY_REGISTER_RESULT = Ability.registerCreator("entry", () -> MyUIAbility)

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
    }
}
```

## class AbilityStageContext

```cangjie
public class AbilityStageContext <: Context {
    public var currentHapModuleInfo: HapModuleInfo
}
```

**功能：** [AbilityStageContext](#class-abilitystagecontext)提供允许访问特定于`abilityStage`的资源的能力，包括获取AbilityStage对应的`hapModuleInfo`对象、环境变化对象。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### var currentHapModuleInfo

```cangjie
public var currentHapModuleInfo: HapModuleInfo
```

**功能：** AbilityStage对应的`hapModuleInfo`对象。

**类型：** [HapModuleInfo](./cj-apis-bundle_manager.md#class-hapmoduleinfo)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyAbilityStage <: AbilityStage {
    public override func onCreate(): Unit {
        let info = this.context.currentHapModuleInfo
    }
}
```

## class ApplicationContext

```cangjie
public class ApplicationContext <: Context {}
```

**功能：** 提供应用级别的的上下文的能力。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

## class Context

```cangjie
public open class Context <: BaseContext {}
```

**功能：** 提供ability或application的上下文的能力。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [BaseContext](./cj-apis-app-ability.md#class-basecontext)

### prop applicationInfo

```cangjie
public prop applicationInfo: ApplicationInfo
```

**功能：** 当前应用程序的信息。

**类型：** [ApplicationInfo](./cj-apis-bundle_manager.md#class-applicationinfo)

**读写能力：** 只读

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let info = this.context.applicationInfo
    }
}
```

### prop area

```cangjie
public mut prop area: AreaMode
```

**功能：** 文件分区信息。

**类型：** [AreaMode](./cj-apis-app-ability-context_constant.md#enum-areamode)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let area = this.context.area
    }
}
```

### prop filesDir

```cangjie
public prop filesDir: String
```

**功能：** 文件目录。

**类型：** String

**读写能力：** 只读

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let filesDir = this.context.filesDir
    }
}
```

### prop resourceManager

```cangjie
public prop resourceManager: ResourceManager
```

**功能：** 资源管理对象。

**类型：** [ResourceManager](../LocalizationKit/cj-apis-resource_manager.md#class-resourcemanager)

**读写能力：** 只读

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let resourceManager = this.context.resourceManager
    }
}
```

## class UIAbility

```cangjie
public open class UIAbility <: Ability {}
```

**功能：** UIAbility是包含UI界面的应用组件，继承自BaseAbility，提供组件创建、销毁、前后台切换等生命周期回调，同时也具备组件协同的能力。组件协同主要提供如下常用功能：

- Caller：由startAbilityByCall接口返回，CallerAbility(调用者)可使用Caller与CalleeAbility(被调用者)进行通信。

- Callee：UIAbility的内部对象，CalleeAbility(被调用者)可以通过Callee与Caller进行通信。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**父类型：**

- [Ability](#class-ability)

### prop context

```cangjie
public mut prop context: UIAbilityContext
```

**功能：** 上下文。

**类型：** [UIAbilityContext](#class-uiabilitycontext)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let context = this.context
    }
}
```

### prop lastRequestWant

```cangjie
public mut prop lastRequestWant: Want
```

**功能：** UIAbility最后请求时的参数。

**类型：** [Want](./cj-apis-app-ability-want.md#class-want)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let lastRequestWant = this.lastRequestWant
    }
}
```

### prop launchWant

```cangjie
public mut prop launchWant: Want
```

**功能：** UIAbility启动时的参数。

**类型：** [Want](./cj-apis-app-ability-want.md#class-want)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let launchWant = this.launchWant
    }
}
```

### func onBackground()

```cangjie
public open func onBackground(): Unit
```

**功能：** UIAbility生命周期回调，当应用从前台转到后台时触发。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override onBackground() {
        let launchWant = this.launchWant
    }
}
```

### func onCreate(Want, LaunchParam)

```cangjie
public open func onCreate(want: Want, launchParam: LaunchParam): Unit
```

**功能：** UIAbility创建时回调，执行初始化业务逻辑操作。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|当前UIAbility的Want类型信息，包括UIAbility名称、Bundle名称等。|
|launchParam|[LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam)|是|-|创建 ability、上次异常退出的原因信息。|

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onCreate(want: Want, launchParam: LaunchParam): Unit {
        let launchWant = this.launchWant
    }
}
```

### func onDestroy()

```cangjie
public open func onDestroy(): Unit
```

**功能：** UIAbility销毁时回调，执行资源清理等操作。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onDestroy(): Unit {
    }
}
```

### func onForeground()

```cangjie
public open func onForeground(): Unit
```

**功能：** UIAbility生命周期回调，当应用从后台转到前台时触发。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onForeground(): Unit {
    }
}
```

### func onNewWant(Want, LaunchParam)

```cangjie
public open func onNewWant(want: Want, launchParam: LaunchParam): Unit
```

**功能：** UIAbility实例已经启动并在前台运行过，由于某些原因切换到后台，再次启动该UIAbility实例时会回调执行该方法。即UIAbility实例热启动时进入该生命周期回调。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|当前UIAbility的Want类型信息，包括ability名称、bundle名称等。|
|launchParam|[LaunchParam](./cj-apis-app-ability-ability_constant.md#class-launchparam)|是|-|Ability启动的原因、上次异常退出的原因信息。|

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onNewWant(want: Want, launchParam: LaunchParam): Unit {
    }
}
```

### func onWindowStageCreate(WindowStage)

```cangjie
public open func onWindowStageCreate(windowStage: WindowStage): Unit
```

**功能：** 当WindowStage创建后调用。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|windowStage|WindowStage|是|-|WindowStage相关信息。|

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
    }
}
```

### func onWindowStageDestroy()

```cangjie
public open func onWindowStageDestroy(): Unit
```

**功能：** 当WindowStage销毁后调用。

**系统能力：** SystemCapability.Ability.AbilityRuntime.AbilityCore

**起始版本：** 22

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageDestroy(): Unit {
    }
}
```

## class UIAbilityContext

```cangjie
public open class UIAbilityContext <: Context {}
```

**功能：** 提供允许访问特定UIAbility的资源的能力。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [Context](./cj-apis-app-ability-ui_ability.md#class-context)

### func isTerminating()

```cangjie
public func isTerminating(): Bool
```

**功能：** 查询ability是否在terminating状态。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|Bool|true：ability当前处于terminating状态；false：不处于terminating状态。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 16000011 | The context does not exist. |

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        let isTerminating = this.context.isTerminating()
    }
}
```

### func requestDialogService(Want, AsyncCallback\<RequestResult>)

```cangjie
public func requestDialogService(want: Want, result: AsyncCallback<RequestResult>): Unit
```

**功能：** 启动支持模式对话框的ServiceExtensionAbility，并使用回调返回结果。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|需要启动的目标ServiceExtensionAbility的want信息。|
|result|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[RequestResult](./cj-apis-app-ability-dialog_request.md#class-requestresult)>|是|-| 用于返回结果的回调。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
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

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
        this.context.requestDialogService(Want(), (err: ?BusinessException, data: ?RequestResult) => {})
    }
}
```

### func startAbility(Want, ?StartOptions)

```cangjie
public func startAbility(want: Want, options!: ?StartOptions = None): Unit
```

**功能：** 携带启动参数，启动Ability。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|启动Ability的want信息。|
|options|?[StartOptions](./cj-apis-app-ability-start_options.md#class-startoptions)|否|None|启动Ability所携带的参数。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
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

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          this.context.startAbility(Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"))
    }
}
```

### func startAbilityForResult(Want, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, callback: AsyncCallback<AbilityResult>): Unit
```

**功能：** 启动Ability并在该Ability退出的时候返回执行结果（callback形式）。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|启动Ability的want信息。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult)>|是|-| 执行结果回调函数。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
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

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          this.context.startAbilityForResult(
              Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"),
              (err: ?BusinessException, data: ?AbilityResult) => {})
    }
}
```

### func startAbilityForResult(Want, StartOptions, AsyncCallback\<AbilityResult>)

```cangjie
public func startAbilityForResult(want: Want, options: StartOptions, callback: AsyncCallback<AbilityResult>): Unit
```

**功能：** 启动Ability并在该Ability退出的时候返回执行结果（callback形式）。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|want|[Want](./cj-apis-app-ability-want.md#class-want)|是|-|启动Ability的want信息。|
|options|StartOptions|是|-|启动Ability所携带的参数。|
|callback|[AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<AbilityResult>|是|-|执行结果回调函数。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
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

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          this.context.startAbilityForResult(
              Want(bundleName: "com.example.cangjieinsight", abilityName: "testAbility"), StartOptions(),
              (err: ?BusinessException, data: ?AbilityResult) => {})
    }
}
```

### func terminateSelf()

```cangjie
public func terminateSelf(): Unit
```

**功能：** 停止UIAbility自身。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          this.context.terminateSelf()
    }
}
```

### func terminateSelfWithResult(AbilityResult)

```cangjie
public func terminateSelfWithResult(parameter: AbilityResult): Unit
```

**功能：** 停止UIAbility，配合startAbilityForResult使用，返回给接口调用方AbilityResult信息。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|parameter|[AbilityResult](./cj-apis-ability-ability_result.md#class-abilityresult)|是|-|停止Ability，配合startAbilityForResult使用，返回给接口调用方AbilityResult信息。|

**异常：**

- BusinessException：对应错误码如下表，详见[通用错误码说明文档](../cj-errorcode-universal.md)。

  | 错误码ID | 错误信息 |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified. 2.Incorrect parameter types. |
  | 16000009 | An ability cannot be started or stopped in Wukong mode. |
  | 16000011 | The context does not exist. |
  | 16000050 | Internal error. |

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

class MyUIAbility <: UIAbility {
    public override func onWindowStageCreate(windowStage: WindowStage): Unit {
          this.context.terminateSelfWithResult(AbilityResult(0))
    }
}
```
