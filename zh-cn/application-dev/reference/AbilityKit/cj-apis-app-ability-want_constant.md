# ohos.app.ability.want_constant

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

**功能：** Flags说明。用于表示处理[Want](./cj-apis-app-ability-want.md#class-want)的方式。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**父类型：**

- [Equatable\<Flags>](#enum-flags)
- ToString

### FlagAuthPersistableUriPermission

```cangjie
FlagAuthPersistableUriPermission
```

**功能：** 指示该URI可被接收方持久化。该字段仅在平板类设备上生效。值为：0x00000040。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### FlagAuthReadUriPermission

```cangjie
FlagAuthReadUriPermission
```

**功能：** 指示对URI执行读取操作的授权。值为：0x00000001。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### FlagAuthWriteUriPermission

```cangjie
FlagAuthWriteUriPermission
```

**功能：** 指示对URI执行写入操作的授权。值为：0x00000002。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### FlagInstallOnDemand

```cangjie
FlagInstallOnDemand
```

**功能：** 如果未安装指定的功能，请安装该功能。值为：0x00000800。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### FlagStartWithoutTips

```cangjie
FlagStartWithoutTips
```

**功能：** 如果隐式启动能力不能匹配任何应用程序，则不会弹出提示对话框。值为：0x40000000。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### func !=(Flags)

```cangjie
public operator func !=(other: Flags): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Flags](#enum-flags)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(Flags)

```cangjie
public operator func ==(other: Flags): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Flags](#enum-flags)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func getValue()

```cangjie
public func getValue(): UInt32
```

**功能：** 获取当前枚举的所表示的值。用于表示处理[Want](./cj-apis-app-ability-want.md#class-want)的方式。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|UInt32|当前枚举所表示的值。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The type is not supported. | todo | todo |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|当前枚举的字符串表示。|

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

**功能：** [Want](./cj-apis-app-ability-want.md#class-want)的Params操作。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**父类型：**

- [Equatable\<Params>](#enum-params)
- ToString

### AbilityBackToOtherMissionStack

```cangjie
AbilityBackToOtherMissionStack
```

**功能：** 表示是否支持跨任务链返回。值为：ability.params.backToOtherMissionStack。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### AbilityRecoveryRestart

```cangjie
AbilityRecoveryRestart
```

**功能：** 指示当前Ability是否发生了故障恢复重启。值为：ohos.ability.params.abilityRecoveryRestart。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### ContentTitleKey

```cangjie
ContentTitleKey
```

**功能：** 指示元服务支持分享标题的参数的操作。值为：ohos.extra.param.key.contentTitle。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### ShareAbstractKey

```cangjie
ShareAbstractKey
```

**功能：** 指示页面源文件。值为：ohos.param.atomicservice.pageSourceFile。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### ShareUrlKey

```cangjie
ShareUrlKey
```

**功能：** 指示元服务支持分享内容的参数的操作。值为：ohos.extra.param.key.shareAbstract。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### SupportContinuePageStackKey

```cangjie
SupportContinuePageStackKey
```

**功能：** 指示在跨端迁移过程中是否迁移页面栈信息，默认值为true，自动迁移页面栈信息。值为：ohos.extra.param.key.supportContinuePageStack。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### SupportContinueSourceExitKey

```cangjie
SupportContinueSourceExitKey
```

**功能：** 指示跨端迁移源端应用是否退出，默认值为true，源端应用自动退出。值为：ohos.extra.param.key.supportContinueSourceExit。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

### func !=(Params)

```cangjie
public operator func !=(other: Params): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Params](#enum-params)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(Params)

```cangjie
public operator func ==(other: Params): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[Params](#enum-params)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func getValue()

```cangjie
public func getValue(): String
```

**功能：**  获取当前枚举的所表示的值。供[Want](./cj-apis-app-ability-want.md#class-want)的Params操作使用。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|当前枚举所表示的值。|

**异常：**

- IllegalArgumentException：

  | 错误信息 | 可能原因 | 处理步骤 |
  | :---- | :--- | :--- |
  | The type is not supported. | todo | todo |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**系统能力：** SystemCapability.Ability.AbilityBase

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|当前枚举的字符串表示。|
