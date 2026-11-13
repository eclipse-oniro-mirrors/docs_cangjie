# ohos.telephony.sim（SIM卡管理）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

SIM卡管理模块提供卡类型CardType和卡状态SimState枚举，支持枚举值比较和字符串转换。当前版本未提供SIM卡信息查询或状态修改接口。

## 导入模块

```cangjie
import kit.TelephonyKit.*
```

## 使用说明

API示例代码使用说明：

- 若示例代码首行有"// index.cj"注释，表示该示例可在仓颉模板工程的"index.cj"文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的"main_ability.cj"文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## enum CardType

```cangjie
public enum CardType {
    | CtNationalRoamingCard
    | CuDualModeCard
    | DualModeCgCard
    | DualModeTelecomLteCard
    | DualModeUgCard
    | SingleModeIsimCard
    | SingleModeRuimCard
    | SingleModeSimCard
    | SingleModeUsimCard
    | UnknownCard
    | ...
}
```

**功能：** 卡类型。

**扩展：**

- [extend CardType <: ToString](#extend-cardtype--tostring)
- [extend CardType <: Equatable\<CardType>](#extend-cardtype--equatablecardtype)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### CtNationalRoamingCard

```cangjie
CtNationalRoamingCard
```

**功能：** 中国电信内部漫游卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### CuDualModeCard

```cangjie
CuDualModeCard
```

**功能：** 中国联通双模卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### DualModeCgCard

```cangjie
DualModeCgCard
```

**功能：** 双卡模式C+G。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### DualModeTelecomLteCard

```cangjie
DualModeTelecomLteCard
```

**功能：** 双模式电信LTE卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### DualModeUgCard

```cangjie
DualModeUgCard
```

**功能：** 双模式UG卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SingleModeIsimCard

```cangjie
SingleModeIsimCard
```

**功能：** 单一ISIM卡类型。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SingleModeRuimCard

```cangjie
SingleModeRuimCard
```

**功能：** 单RUIM卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SingleModeSimCard

```cangjie
SingleModeSimCard
```

**功能：** 单SIM卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SingleModeUsimCard

```cangjie
SingleModeUsimCard
```

**功能：** 单USIM卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### UnknownCard

```cangjie
UnknownCard
```

**功能：** 未知类型。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## enum SimState

```cangjie
public enum SimState {
    | SimStateLoaded
    | SimStateLocked
    | SimStateNotPresent
    | SimStateNotReady
    | SimStateReady
    | SimStateUnknown
    | ...
}
```

**功能：** SIM卡状态。

**扩展：**

- [extend SimState <: ToString](#extend-simstate--tostring)
- [extend SimState <: Equatable\<SimState>](#extend-simstate--equatablesimstate)

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateLoaded

```cangjie
SimStateLoaded
```

**功能：** 表示SIM卡处于loaded状态，即SIM卡在位且所有卡文件加载完毕。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateLocked

```cangjie
SimStateLocked
```

**功能：** 表示SIM卡处于locked状态，即SIM卡被PIN、PUK或网络锁锁定。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateNotPresent

```cangjie
SimStateNotPresent
```

**功能：** 表示SIM卡处于not present状态，即卡槽中没有插入SIM卡。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateNotReady

```cangjie
SimStateNotReady
```

**功能：** 表示SIM卡处于not ready状态，即SIM卡在位但无法正常工作。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateReady

```cangjie
SimStateReady
```

**功能：** 表示SIM卡处于ready状态，即SIM卡在位且工作正常。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

### SimStateUnknown

```cangjie
SimStateUnknown
```

**功能：** SIM卡状态未知，即无法获取准确的状态。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

## extend CardType <: Equatable\<CardType>

```cangjie
extend CardType <: Equatable<CardType>
```

**功能：** 为 CardType 类型扩展 Equatable\<CardType> 接口，支持相等比较。

**被扩展类型：**

- [CardType](#enum-cardtype)

**扩展接口：**

- Equatable\<[CardType](#enum-cardtype)>

### func ==(CardType)

```cangjie
public operator func ==(other: CardType): Bool
```

**功能：** 判断两个 CardType 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CardType](#enum-cardtype) | 是 | 需要比较的CardType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 CardType 相等则返回 true，否则返回 false。|

### func !=(CardType)

```cangjie
public operator func !=(other: CardType): Bool
```

**功能：** 判断两个 CardType 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [CardType](#enum-cardtype) | 是 | 需要比较的CardType对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 CardType 不相等则返回 true，否则返回 false。|

## extend CardType <: ToString

```cangjie
extend CardType <: ToString
```

**功能：** 为 CardType 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [CardType](#enum-cardtype)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|

## extend SimState <: Equatable\<SimState>

```cangjie
extend SimState <: Equatable<SimState>
```

**功能：** 为 SimState 类型扩展 Equatable\<SimState> 接口，支持相等比较。

**被扩展类型：**

- [SimState](#enum-simstate)

**扩展接口：**

- Equatable\<[SimState](#enum-simstate)>

### func ==(SimState)

```cangjie
public operator func ==(other: SimState): Bool
```

**功能：** 判断两个 SimState 是否相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [SimState](#enum-simstate) | 是 | 需要比较的SimState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 SimState 相等则返回 true，否则返回 false。|

### func !=(SimState)

```cangjie
public operator func !=(other: SimState): Bool
```

**功能：** 判断两个 SimState 是否不相等。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |
| other | [SimState](#enum-simstate) | 是 | 需要比较的SimState对象。 |

**返回值：**

|类型 | 说明 |
|:----|:----|
|Bool| 如果两个 SimState 不相等则返回 true，否则返回 false。|

## extend SimState <: ToString

```cangjie
extend SimState <: ToString
```

**功能：** 为 SimState 类型扩展 ToString 接口，支持字符串转换。

**被扩展类型：**

- [SimState](#enum-simstate)

**扩展接口：**

- ToString

### func toString()

```cangjie
public func toString(): String
```

**功能：** 获取枚举的值。

**系统能力：** SystemCapability.Telephony.CoreService

**起始版本：** 26.1.0

**返回值：**

|类型 | 说明 |
|:----|:----|
|String| 枚举的说明。|
