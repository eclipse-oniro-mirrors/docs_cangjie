# 使用SIM卡类型和状态枚举

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 场景介绍

ohos.telephony.sim从26.1.0版本开始提供CardType和SimState枚举，用于表示SIM卡类型和状态。两种枚举均支持相等、不等比较和toString字符串转换。

当前模块只有枚举定义，没有读取卡类型、读取卡状态或修改SIM卡状态的接口。创建一个枚举值不会查询设备，也不会改变设备上的SIM卡。

## 基本概念

CardType表示卡类型，例如SingleModeSimCard表示SIM卡，SingleModeUsimCard表示USIM卡，UnknownCard表示未知卡类型。完整成员见[CardType](../reference/TelephonyKit/cj-apis-telephony-sim.md#enum-cardtype)。

SimState表示SIM卡状态：

| 枚举值 | 含义 |
| :--- | :--- |
| SimStateUnknown | 未知状态。 |
| SimStateNotPresent | 没有SIM卡。 |
| SimStateLocked | SIM卡已锁定。 |
| SimStateNotReady | SIM卡未就绪。 |
| SimStateReady | SIM卡已就绪。 |
| SimStateLoaded | SIM卡数据已加载。 |

SIM卡就绪与蜂窝网络已注册是不同的状态。需要查询网络注册状态时，参考[获取蜂窝网络信息](cj-telephony-network-guidelines.md)。

## 开发步骤

1. 从TelephonyKit导入CardType和SimState。使用枚举比较和字符串转换本身不需要申请权限。
2. 使用==或!=进行比较，使用match为不同状态选择处理逻辑。枚举支持未来扩展，match应保留通配分支。
3. 如需输出日志，调用toString或将状态转换为业务展示文本。不要将日志字符串作为卡类型、卡状态的判断依据。

## 示例代码

以下示例手工创建USIM卡和就绪状态两个枚举值，只演示类型的使用方式，不读取实际SIM卡状态。将函数添加到仓颉工程并调用useSimEnums。

```cangjie
import kit.TelephonyKit.{CardType, SimState}
import kit.PerformanceAnalysisKit.Hilog

func describeSimState(state: SimState): String {
    match (state) {
        case SimState.SimStateUnknown => return "Unknown"
        case SimState.SimStateNotPresent => return "Not present"
        case SimState.SimStateLocked => return "Locked"
        case SimState.SimStateNotReady => return "Not ready"
        case SimState.SimStateReady => return "Ready"
        case SimState.SimStateLoaded => return "Loaded"
        case _ => return "Other state"
    }
}

func useSimEnums(): Unit {
    let cardType = CardType.SingleModeUsimCard
    let state = SimState.SimStateReady
    if (cardType == CardType.SingleModeUsimCard && state != SimState.SimStateNotPresent) {
        Hilog.info(0, "TelephonyExample", "Card: ${cardType.toString()}, state: ${describeSimState(state)}", [])
    }
}
```

完整枚举成员、运算符和版本信息见[ohos.telephony.sim](../reference/TelephonyKit/cj-apis-telephony-sim.md)。
