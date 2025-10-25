# ohos.app.ability.ability_constant

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

## class LaunchParam

```cangjie
public class LaunchParam {
    public var launchReason: LaunchReason
    public var lastExitReason: LastExitReason
}
```

**功能：** 启动参数，包含启动原因和上次退出原因。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### var lastExitReason

```cangjie
public var lastExitReason: LastExitReason
```

**功能：** 上次退出原因。

**类型：** [LastExitReason](#enum-lastexitreason)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### var launchReason

```cangjie
public var launchReason: LaunchReason
```

**功能：** 启动原因。

**类型：** [LaunchReason](#enum-launchreason)

**读写能力：** 可读写

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

## enum LastExitReason

```cangjie
public enum LastExitReason {
    | Unknown
    | Normal
    | CppCrash
    | AppFreeze
    | ...
}
```

**功能：** 上次退出原因。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### AppFreeze

```cangjie
AppFreeze
```

**功能：** 应用冻结。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### CppCrash

```cangjie
CppCrash
```

**功能：** C++崩溃。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Normal

```cangjie
Normal
```

**功能：** 正常退出。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Unknown

```cangjie
Unknown
```

**功能：** 未知原因。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

## enum LaunchReason

```cangjie
public enum LaunchReason {
    | Unknown
    | StartAbility
    | Call
    | Continuation
    | AppRecovery
    | ...
}
```

**功能：** 启动原因。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### AppRecovery

```cangjie
AppRecovery
```

**功能：** 应用恢复。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Call

```cangjie
Call
```

**功能：** 调用启动。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Continuation

```cangjie
Continuation
```

**功能：** 跨端迁移。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### StartAbility

```cangjie
StartAbility
```

**功能：** 启动Ability。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Unknown

```cangjie
Unknown
```

**功能：** 未知原因。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

## enum MemoryLevel

```cangjie
public enum MemoryLevel <: Equatable<MemoryLevel> & ToString {
    | MemoryLevelModerate
    | MemoryLevelLow
    | MemoryLevelCritical
    | ...
}
```

**功能：** 内存级别。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [Equatable\<MemoryLevel>](#enum-memorylevel)
- ToString

### MemoryLevelCritical

```cangjie
MemoryLevelCritical
```

**功能：** 内存严重不足。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### MemoryLevelLow

```cangjie
MemoryLevelLow
```

**功能：** 内存不足。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### MemoryLevelModerate

```cangjie
MemoryLevelModerate
```

**功能：** 内存适中。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### func !=(MemoryLevel)

```cangjie
public operator func !=(other: MemoryLevel): Bool
```

**功能：** 判断两个枚举值是否不相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[MemoryLevel](#enum-memorylevel)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(MemoryLevel)

```cangjie
public operator func ==(other: MemoryLevel): Bool
```

**功能：** 判断两个枚举值是否相等。

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[MemoryLevel](#enum-memorylevel)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**返回值：**

|类型|说明|
|:----|:----|
|String|当前枚举的字符串表示。|

## enum OnContinueResult

```cangjie
public enum OnContinueResult {
    | Agree
    | Reject
    | Mismatch
    | ...
}
```

**功能：** 跨端迁移结果。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Agree

```cangjie
Agree
```

**功能：** 同意迁移。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Mismatch

```cangjie
Mismatch
```

**功能：** 迁移不匹配。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### Reject

```cangjie
Reject
```

**功能：** 拒绝迁移。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

## enum WindowMode

```cangjie
public enum WindowMode {
    | WindowModeFullscreen
    | WindowModeSplitPrimary
    | WindowModeSplitSecondary
    | ...
}
```

**功能：** 窗口模式。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### WindowModeFullscreen

```cangjie
WindowModeFullscreen
```

**功能：** 全屏模式。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### WindowModeSplitPrimary

```cangjie
WindowModeSplitPrimary
```

**功能：** 分屏主窗口。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### WindowModeSplitSecondary

```cangjie
WindowModeSplitSecondary
```

**功能：** 分屏次窗口。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22
