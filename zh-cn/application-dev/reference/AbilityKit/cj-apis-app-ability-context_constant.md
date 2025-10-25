# ohos.app.ability.context_constant

ContextConstant提供Context相关的枚举，包括文件分区信息AreaMode等。

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

## enum AreaMode

```cangjie
public enum AreaMode <: Equatable<AreaMode> & ToString {
    | El1
    | El2
    | El3
    | El4
    | El5
    | ...
}
```

**功能：** 文件分区信息。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**父类型：**

- [Equatable\<AreaMode>](#enum-areamode)
- ToString

### El1

```cangjie
El1
```

**功能：** 文件分区1。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### El2

```cangjie
El2
```

**功能：** 文件分区2。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### El3

```cangjie
El3
```

**功能：** 文件分区3。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### El4

```cangjie
El4
```

**功能：** 文件分区4。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### El5

```cangjie
El5
```

**功能：** 文件分区5。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

### func !=(AreaMode)

```cangjie
public operator func !=(other: AreaMode): Bool
```

**功能：** 判断两个枚举值是否不相等。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AreaMode](#enum-areamode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值不相等返回true，否则返回false。|

### func ==(AreaMode)

```cangjie
public operator func ==(other: AreaMode): Bool
```

**功能：** 判断两个枚举值是否相等。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**参数：**

|参数名|类型|必填|默认值|说明|
|:---|:---|:---|:---|:---|
|other|[AreaMode](#enum-areamode)|是|-|另一个枚举值。|

**返回值：**

|类型|说明|
|:----|:----|
|Bool|两个枚举值相等返回true，否则返回false。|

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取当前枚举的字符串表示。

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**起始版本：** 22

**返回值：**

|类型|说明|
|:----|:----|
|String|当前枚举的字符串表示。|
