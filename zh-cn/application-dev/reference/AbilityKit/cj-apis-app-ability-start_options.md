# ohos.app.ability.start_options

StartOptions提供Ability启动选项的能力，包括窗口模式、显示ID等配置。

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

**功能：** 启动选项，包含窗口模式和显示ID等配置。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### var displayId

```cangjie
public var displayId: Int32
```

**功能：** 显示ID。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### var windowMode

```cangjie
public var windowMode:?WindowMode
```

**功能：** 窗口模式。

**类型：** ?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### init(?WindowMode, Int32)

```cangjie
public init(
    windowMode!: ?WindowMode = None,
    displayId!: Int32 = 0
)
```

**功能：** 构造函数，创建StartOptions实例。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|windowMode|?[WindowMode](cj-apis-app-ability-ability_constant.md#enum-windowmode)|否|None|窗口模式。|
|displayId|Int32|否|0|显示ID。|

**示例：**

<!-- compile -->
```cangjie
import kit.AbilityKit.*

let startOptions = StartOptions(WindowMode.FullScreen, 0)
```
