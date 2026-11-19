# ohos.vibrator（振动）

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

vibrator模块提供控制马达振动启停的能力。

## 导入模块

```cangjie
import kit.SensorServiceKit.*
```

## 权限列表

ohos.permission.VIBRATE

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func startVibration(VibrateEffect, VibrateAttribute, AsyncCallback\<Unit>)

```cangjie
public func startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback<Unit>): Unit
```

**功能：** 根据指定的振动效果和振动属性触发马达振动。使用异步回调返回结果。

**需要权限：** ohos.permission.VIBRATE

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| effect | [VibrateEffect](#enum-vibrateeffect) | 是 | - | 马达振动效果，支持三种：<br>1、[VibrateTime](#class-vibratetime)：按照指定持续时间触发马达振动；<br>2、[VibratePreset](#class-vibratepreset)：按照预置振动效果触发马达振动；<br>3、[VibrateFromFile](#class-vibratefromfile)：按照自定义振动配置文件触发马达振动。|
| attribute | [VibrateAttribute](#class-vibrateattribute) | 是 | - | 马达振动属性。|
| callback | AsyncCallback\<Unit> | 是 | - | 回调函数，用于返回操作结果。当操作成功时，err为None；否则err为包含错误码和错误信息的错误对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[振动错误码](./cj-errorcode-vibrator.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 14600101 | Device operation failed. |

**示例：**

按照指定持续时间触发马达振动：

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

let vibrateTime = VibrateTime("time", 1000)
let effect = VibrateEffect.VibrateTimeType(vibrateTime)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
```

按照预置振动效果触发马达振动：

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

let vibratePreset = VibratePreset("preset", "haptic.clock.timer", count: 1)
let effect = VibrateEffect.VibratePresetType(vibratePreset)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
```

按照自定义振动配置文件触发马达振动：

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

let resourceManager = Global.getAbilityContext().resourceManager // 需获取Context应用上下文，详见本文使用说明
let rawfd = resourceManager.getRawFd("vib.json")
let hapticFd = HapticFileDescriptor(Int32(rawfd.fd), offSet: Some(Int64(rawfd.offset)), length: Some(Int64(rawfd.length)))
let vibrateFile = VibrateFromFile("file", hapticFd)
let effect = VibrateEffect.VibrateFromFileType(vibrateFile)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
resourceManager.closeRawFd("vib.json")
```

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

// fd: Int32, obtained from file API
let hapticFd = HapticFileDescriptor(Int32(1))
let vibrateFile = VibrateFromFile("file", hapticFd)
let effect = VibrateEffect.VibrateFromFileType(vibrateFile)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
```

## func stopVibration(VibratorStopMode, AsyncCallback\<Unit>)

```cangjie
public func stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback<Unit>): Unit
```

**功能：** 按照指定模式停止马达振动。使用异步回调返回结果。

**需要权限：** ohos.permission.VIBRATE

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| stopMode | [VibratorStopMode](#enum-vibratorstopmode) | 是 | - | 停止振动的模式。支持两种：<br>VibratorStopModeTime：停止duration模式的振动；<br>VibratorStopModePreset：停止预置EffectId的振动。|
| callback | AsyncCallback\<Unit> | 是 | - | 回调函数，用于返回结果。当振动停止时，err为None；否则err为错误对象。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[振动错误码](./cj-errorcode-vibrator.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |

**示例：**

停止固定时长振动：

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

let vibrateTime = VibrateTime("time", 1000)
let effect = VibrateEffect.VibrateTimeType(vibrateTime)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
// 按照VibratorStopModeTime模式停止振动
stopVibration(VibratorStopMode.VibratorStopModeTime, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Stop vibration failed: ${e}", "")
    }
})
```

停止预置振动：

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

let vibratePreset = VibratePreset("preset", "haptic.clock.timer", count: 1)
let effect = VibrateEffect.VibratePresetType(vibratePreset)
let attribute = VibrateAttribute("alarm")
startVibration(effect, attribute, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Vibration failed: ${e}", "")
    }
})
// 按照VibratorStopModePreset模式停止振动
stopVibration(VibratorStopMode.VibratorStopModePreset, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Stop vibration failed: ${e}", "")
    }
})
```

## func isSupportEffect(String, AsyncCallback\<Bool>)

```cangjie
public func isSupportEffect(effectId: String, callback: AsyncCallback<Bool>): Unit
```

**功能：** 查询是否支持预设的振动效果。使用异步回调返回结果。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| effectId | String | 是 | - | 振动效果ID。最大长度为64个字符，超过64个字符时取前64个字符。|
| callback | AsyncCallback\<Bool> | 是 | - | 回调函数，用于返回结果。值为true表示支持该效果ID，值为false表示不支持。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[振动错误码](./cj-errorcode-vibrator.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 201 | Permission denied. |

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

isSupportEffect("haptic.clock.timer", { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Check failed: ${e}", "")
    } else if (let Some(supported) <- data) {
        Hilog.info(0, "test", "Is supported: ${supported}", "")
    }
})
```

## func isHdHapticSupported()

```cangjie
public func isHdHapticSupported(): Bool
```

**功能：** 查询是否支持高清振动。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| Bool | 返回是否支持高清振动。值为true表示支持，值为false表示不支持。|

**异常：**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception)：对应错误码如下表，详见[振动错误码](./cj-errorcode-vibrator.md)。

  | 错误码ID | 错误信息 |
  | :--- | :--- |
  | 14600101 | Device operation failed. |

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let ret = isHdHapticSupported()
    Hilog.info(0, "test", "Is HD haptic supported: ${ret}", "")
} catch (e: Exception) {
    Hilog.error(0, "test", "Check HD haptic failed: ${e}", "")
}
```

## enum EffectId

```cangjie
public enum EffectId {
    | EffectClockTimer
    | ...
}
```

**功能：** 预置的振动效果。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**父类型：**

- ToString
- Equatable\<[EffectId](#enum-effectid)\>

### EffectClockTimer

```cangjie
EffectClockTimer
```

**功能：** 描述用户调整计时器时的振动效果。

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回预设振动效果的字符串表示。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| String | 预设振动效果的字符串表示。|

### func !=(EffectId)

```cangjie
public operator func !=(other: EffectId): Bool
```

**功能：** 对预设振动效果进行判不等。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
|:--- |:--- |:--- |:--- |
| other | [EffectId](#enum-effectid) | 是 | 预置的振动效果。|

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| Bool | 如果两个预设的振动效果不同返回true，否则返回false。|

### func ==(EffectId)

```cangjie
public operator func ==(other: EffectId): Bool
```

**功能：** 对预设振动效果进行判等。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
|:--- |:--- |:--- |:--- |
| other | [EffectId](#enum-effectid) | 是 | 预置的振动效果。|

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| Bool | 如果两个预设的振动效果相同返回true，否则返回false。|

## enum VibratorStopMode

```cangjie
public enum VibratorStopMode {
    | VibratorStopModeTime
    | VibratorStopModePreset
    | ...
}
```

**功能：** 停止振动的模式。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**父类型：**

- ToString
- Equatable\<[VibratorStopMode](#enum-vibratorstopmode)\>

### VibratorStopModeTime

```cangjie
VibratorStopModeTime
```

**功能：** 停止duration模式的振动。

**起始版本：** 26.1.0

### VibratorStopModePreset

```cangjie
VibratorStopModePreset
```

**功能：** 停止预置EffectId的振动。

**起始版本：** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**功能：** 返回停止振动的模式的字符串表示。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| String | 停止振动的模式的字符串表示。|

### func !=(VibratorStopMode)

```cangjie
public operator func !=(other: VibratorStopMode): Bool
```

**功能：** 对停止振动的模式进行判不等。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
|:--- |:--- |:--- |:--- |
| other | [VibratorStopMode](#enum-vibratorstopmode) | 是 | 停止振动的模式。|

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| Bool | 如果两个停止振动的模式不同返回true，否则返回false。|

### func ==(VibratorStopMode)

```cangjie
public operator func ==(other: VibratorStopMode): Bool
```

**功能：** 对停止振动的模式进行判等。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
|:--- |:--- |:--- |:--- |
| other | [VibratorStopMode](#enum-vibratorstopmode) | 是 | 停止振动的模式。|

**返回值：**

| 类型 | 说明 |
|:--- |:--- |
| Bool | 如果两个停止振动的模式相同返回true，否则返回false。|

## type Usage

```cangjie
public type Usage = String
```

**功能：** 振动使用场景。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

| 值 | 说明 |
|:--- |:--- |
| "unknown" | 没有明确使用场景，最低优先级。|
| "alarm" | 用于警报场景。|
| "ring" | 用于铃声场景。|
| "notification" | 用于通知场景。|
| "communication" | 用于通信场景。|
| "touch" | 用于触摸场景。|
| "media" | 用于多媒体场景。|
| "physicalFeedback" | 用于物理反馈场景。|
| "simulateReality" | 用于模拟现实场景。|

## class VibrateAttribute

```cangjie
public class VibrateAttribute {
    public mut prop id: ?Int32
    public mut prop usage: Usage
    public init(usage: Usage, id!: ?Int32 = None)
}
```

**功能：** 马达振动属性。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### prop id

```cangjie
public mut prop id: ?Int32
```

**功能：** 振动器id，默认值为0。

**类型：** ?Int32

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop usage

```cangjie
public mut prop usage: Usage
```

**功能：** 振动场景，默认值为unknown。

**类型：** [Usage](#type-usage)

**读写能力：** 可读写

**起始版本：** 26.1.0

### init(Usage, ?Int32)

```cangjie
public init(usage: Usage, id!: ?Int32 = None)
```

**功能：** 用于创建VibrateAttribute实例的构造函数。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| usage | [Usage](#type-usage) | 是 | - | 马达振动的使用场景。|
| id | ?Int32 | 否 | None | **命名参数。** 振动器id，默认值为0。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let attribute = VibrateAttribute("alarm")
```

## enum VibrateEffect

```cangjie
public enum VibrateEffect {
    | VibrateTimeType(VibrateTime)
    | VibratePresetType(VibratePreset)
    | VibrateFromFileType(VibrateFromFile)
    | ...
}
```

**功能：** 马达振动效果枚举。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### VibrateTimeType

```cangjie
VibrateTimeType(VibrateTime)
```

**功能：** 表示指定时长的振动。

**起始版本：** 26.1.0

### VibratePresetType

```cangjie
VibratePresetType(VibratePreset)
```

**功能：** 表示预置振动效果。

**起始版本：** 26.1.0

### VibrateFromFileType

```cangjie
VibrateFromFileType(VibrateFromFile)
```

**功能：** 表示基于振动配置文件触发的自定义振动。

**起始版本：** 26.1.0

## class VibrateTime

```cangjie
public class VibrateTime {
    public mut prop effectType: String
    public mut prop duration: Int32
    public init(effectType: String, duration: Int32)
}
```

**功能：** 表示指定时长的振动。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**功能：** 值为'time'，表示指定时长的振动。

**类型：** String

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop duration

```cangjie
public mut prop duration: Int32
```

**功能：** 振动时长，单位ms。取值范围为(0, 1800000]。建议单次振动时长不超过10s，以获得较好的用户体验。

**类型：** Int32

**读写能力：** 可读写

**起始版本：** 26.1.0

### init(String, Int32)

```cangjie
public init(effectType: String, duration: Int32)
```

**功能：** 用于创建VibrateTime实例的构造函数。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| effectType | String | 是 | - | 值为'time'，表示指定时长的振动。|
| duration | Int32 | 是 | - | 振动时长，单位ms。取值范围为(0, 1800000]。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let vTime = VibrateTime("time", 1000)
```

## class VibratePreset

```cangjie
public class VibratePreset {
    public mut prop effectType: String
    public mut prop effectId: String
    public mut prop count: ?Int32
    public mut prop intensity: ?Int32
    public init(effectType: String, effectId: String, count!: ?Int32 = None, intensity!: ?Int32 = None)
}
```

**功能：** 表示预置振动效果。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**功能：** 值为'preset'，表示按照预置振动效果触发马达振动。

**类型：** String

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop effectId

```cangjie
public mut prop effectId: String
```

**功能：** 预置振动效果ID。最大长度为64个字符，超过64个字符时取前64个字符。

**类型：** String

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop count

```cangjie
public mut prop count: ?Int32
```

**功能：** 可选参数，振动的重复次数，默认值为1。

**类型：** ?Int32

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop intensity

```cangjie
public mut prop intensity: ?Int32
```

**功能：** 可选参数，振动强度，范围为[0, 100]，默认值为100。不支持振动强度调节时使用默认振动强度。

**类型：** ?Int32

**读写能力：** 可读写

**起始版本：** 26.1.0

### init(String, String, ?Int32, ?Int32)

```cangjie
public init(effectType: String, effectId: String, count!: ?Int32 = None, intensity!: ?Int32 = None)
```

**功能：** 用于创建VibratePreset实例的构造函数。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| effectType | String | 是 | - | 值为'preset'，表示按照预置振动效果触发马达振动。|
| effectId | String | 是 | - | 预置振动效果ID。最大长度为64个字符。|
| count | ?Int32 | 否 | None | **命名参数。** 可选参数，振动的重复次数，默认值为1。|
| intensity | ?Int32 | 否 | None | **命名参数。** 可选参数，振动强度，范围为[0, 100]，默认值为100。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let vPreset = VibratePreset("preset", "haptic.clock.timer", count: 1)
```

## class VibrateFromFile

```cangjie
public class VibrateFromFile {
    public mut prop effectType: String
    public mut prop hapticFd: HapticFileDescriptor
    public init(effectType: String, hapticFd: HapticFileDescriptor)
}
```

**功能：** 表示自定义振动配置文件。仅部分设备支持，当设备不支持此振动类型时，返回错误码。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**功能：** 值为'file'，表示按照振动配置文件触发马达振动。

**类型：** String

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop hapticFd

```cangjie
public mut prop hapticFd: HapticFileDescriptor
```

**功能：** 振动配置文件描述符。

**类型：** [HapticFileDescriptor](#class-hapticfiledescriptor)

**读写能力：** 可读写

**起始版本：** 26.1.0

### init(String, HapticFileDescriptor)

```cangjie
public init(effectType: String, hapticFd: HapticFileDescriptor)
```

**功能：** 用于创建VibrateFromFile实例的构造函数。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| effectType | String | 是 | - | 值为'file'，表示按照振动配置文件触发马达振动。|
| hapticFd | [HapticFileDescriptor](#class-hapticfiledescriptor) | 是 | - | 振动配置文件描述符。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let descriptor = HapticFileDescriptor(Int32(1))
let vibrateFile = VibrateFromFile("file", descriptor)
```

## class HapticFileDescriptor

```cangjie
public class HapticFileDescriptor {
    public mut prop fd: Int32
    public mut prop offSet: ?Int64
    public mut prop length: ?Int64
    public init(fd: Int32, offSet!: ?Int64 = None, length!: ?Int64 = None)
}
```

**功能：** 自定义振动配置文件的描述符。必须确认资源文件可用，其参数可通过文件管理API从沙箱路径获取或通过资源管理API从HAP资源获取。使用场景：振动序列被存储在一个文件中，需要根据偏移量和长度进行振动。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

### prop fd

```cangjie
public mut prop fd: Int32
```

**功能：** 资源文件描述符。

**类型：** Int32

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop offSet

```cangjie
public mut prop offSet: ?Int64
```

**功能：** 距文件起始位置的偏移量，单位为字节。默认为文件起始位置，不能超出文件有效范围。

**类型：** ?Int64

**读写能力：** 可读写

**起始版本：** 26.1.0

### prop length

```cangjie
public mut prop length: ?Int64
```

**功能：** 资源长度，单位为字节。默认为从偏移量位置到文件末尾的长度，不能超出文件有效范围。

**类型：** ?Int64

**读写能力：** 可读写

**起始版本：** 26.1.0

### init(Int32, ?Int64, ?Int64)

```cangjie
public init(fd: Int32, offSet!: ?Int64 = None, length!: ?Int64 = None)
```

**功能：** 用于创建HapticFileDescriptor实例的构造函数。

**系统能力：** SystemCapability.Sensors.MiscDevice

**起始版本：** 26.1.0

**参数：**

| 参数名 | 类型 | 必填 | 默认值 | 说明 |
|:--- |:--- |:--- |:--- |:--- |
| fd | Int32 | 是 | - | 资源文件描述符。|
| offSet | ?Int64 | 否 | None | **命名参数。** 距文件起始位置的偏移量，单位为字节。默认为文件起始位置。|
| length | ?Int64 | 否 | None | **命名参数。** 资源长度，单位为字节。默认为从偏移量位置到文件末尾的长度。|

**示例：**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let descriptor = HapticFileDescriptor(Int32(1))
```
