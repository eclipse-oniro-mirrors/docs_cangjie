# ohos.vibrator (Vibrator)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The vibrator module provides capabilities to control motor vibration start and stop.

## Import Module

```cangjie
import kit.SensorServiceKit.*
```

## Permission List

ohos.permission.VIBRATE

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func startVibration(VibrateEffect, VibrateAttribute, AsyncCallback\<Unit>)

```cangjie
public func startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback<Unit>): Unit
```

**Function:** Starts vibration based on a specified effect and attribute. This API uses an asynchronous callback to return the result.

**Required Permission:** ohos.permission.VIBRATE

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type                                           | Required | Default | Description                                              |
|:-------------- |:--------------------------------------------- |:-------- |:------- |:-------------------------------------------------------- |
| effect         | [VibrateEffect](#enum-vibrateeffect)          | Yes      | -       | Vibration effect.                                        |
| attribute      | [VibrateAttribute](#class-vibrateattribute)   | Yes      | -       | Vibration attribute.                                     |
| callback       | AsyncCallback\<Unit>                          | Yes      | -       | Callback used to return the operation result. If the operation is successful, **err** is **undefined**; otherwise, **err** is an error object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Vibrator Error Codes](./cj-errorcode-vibrator.md).

  | Error Code ID | Error Message           |
  |:------------- |:----------------------- |
  | 201           | Permission denied.      |
  | 801           | Capability not supported. |
  | 14600101      | Device operation failed. |

**Example:**

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

## func stopVibration(VibratorStopMode, AsyncCallback\<Unit>)

```cangjie
public func stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback<Unit>): Unit
```

**Function:** Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.

**Required Permission:** ohos.permission.VIBRATE

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type                                         | Required | Default | Description                                              |
|:-------------- |:------------------------------------------- |:-------- |:------- |:-------------------------------------------------------- |
| stopMode       | [VibratorStopMode](#enum-vibratorstopmode)   | Yes      | -       | Mode to stop the vibration.                              |
| callback       | AsyncCallback\<Unit>                        | Yes      | -       | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Vibrator Error Codes](./cj-errorcode-vibrator.md).

  | Error Code ID | Error Message      |
  |:------------- |:------------------ |
  | 201           | Permission denied. |

**Example:**

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
stopVibration(VibratorStopMode.VibratorStopModeTime, { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Stop vibration failed: ${e}", "")
    }
})
```

## func isSupportEffect(String, AsyncCallback\<Bool>)

```cangjie
public func isSupportEffect(effectId: String, callback: AsyncCallback<Bool>): Unit
```

**Function:** Checks whether an effect ID is supported. This API uses an asynchronous callback to return the result.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type                  | Required | Default | Description                                              |
|:-------------- |:---------------------|:-------- |:------- |:-------------------------------------------------------- |
| effectId       | String                | Yes      | -       | Effect ID. The value is a string of a maximum of 64 characters. If the length exceeds 64 characters, the first 64 characters are used. |
| callback       | AsyncCallback\<Bool>  | Yes      | -       | Callback used to return the result. The value **true** means that the effect ID is supported, and the value **false** means the opposite. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Vibrator Error Codes](./cj-errorcode-vibrator.md).

  | Error Code ID | Error Message      |
  |:------------- |:------------------ |
  | 201           | Permission denied. |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog

isSupportEffect("haptic.clock.timer", { err, data =>
    if (let Some(e) <- err) {
        Hilog.error(0, "test", "Check failed: ${e}", "")
    } else if (let Some(supported) <- data) {
        Hilog.info(0, "test", "Is supported: ${supported}")
    }
})
```

## func isHdHapticSupported()

```cangjie
public func isHdHapticSupported(): Bool
```

**Function:** Checks whether HD vibration is supported.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Return Value:**

| Type | Description                                                                                     |
|:-----|:-----------------------------------------------------------------------------------------------|
| Bool | Boolean value indicating whether HD vibration is supported. The value **true** indicates that HD vibration is supported, and the value **false** indicates the opposite. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Vibrator Error Codes](./cj-errorcode-vibrator.md).

  | Error Code ID | Error Message           |
  |:------------- |:----------------------- |
  | 14600101      | Device operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.BusinessException

try {
    let ret = isHdHapticSupported()
    Hilog.info(0, "test", "Is HD haptic supported: ${ret}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum EffectId

```cangjie
public enum EffectId {
    | EffectClockTimer
    | ...
}
```

**Function:** Enumerates the preset vibration effect IDs. This parameter is needed when you call **startVibration** or **stopVibration** to deliver the vibration effect specified by **VibratePreset**. This parameter supports a variety of values, such as **haptic.clock.timer**.

> **NOTE**
>
> Preset effects vary according to devices. You are advised to call **isSupportEffect** to check whether the device supports the preset effect before use.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parent Types:**

- [Equatable\<EffectId\>](../arkui-cj/cj-common-types.md#class-equatable)
- ToString

### EffectClockTimer

```cangjie
EffectClockTimer
```

**Function:** Vibration effect when a user adjusts the timer.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the EffectId to its string representation.

**Return Value:**

| Type   | Description                               |
|:-------|:-----------------------------------------|
| String | A string representation of the EffectId. |

### func !=(EffectId)

```cangjie
public operator func !=(other: EffectId): Bool
```

**Function:** Compares this EffectId with another for inequality.

**Parameters:**

| Parameter | Type                  | Required | Default | Description              |
|:----------|:---------------------|:---------|:--------|:-------------------------|
| other     | [EffectId](#enum-effectid) | Yes      | -       | The EffectId to compare with. |

**Return Value:**

| Type | Description                                       |
|:-----|:--------------------------------------------------|
| Bool | True if both modes are not equal, false otherwise. |

### func ==(EffectId)

```cangjie
public operator func ==(other: EffectId): Bool
```

**Function:** Compares this EffectId with another for equality.

**Parameters:**

| Parameter | Type                  | Required | Default | Description              |
|:----------|:---------------------|:---------|:--------|:-------------------------|
| other     | [EffectId](#enum-effectid) | Yes      | -       | The EffectId to compare with. |

**Return Value:**

| Type | Description                                   |
|:-----|:----------------------------------------------|
| Bool | True if both modes are equal, false otherwise. |

## enum VibratorStopMode

```cangjie
public enum VibratorStopMode {
    | VibratorStopModeTime
    | VibratorStopModePreset
    | ...
}
```

**Function:** Enumerates vibration stop modes. This parameter is required for **stopVibration**. The stop mode must match that delivered in **VibrateEffect**.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parent Types:**

- [Equatable\<VibratorStopMode\>](../arkui-cj/cj-common-types.md#class-equatable)
- ToString

### VibratorStopModeTime

```cangjie
VibratorStopModeTime
```

**Function:** The vibration to stop is in **duration** mode.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### VibratorStopModePreset

```cangjie
VibratorStopModePreset
```

**Function:** The vibration to stop is in **EffectId** mode.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the VibratorStopMode to its string representation.

**Return Value:**

| Type   | Description                                        |
|:-------|:---------------------------------------------------|
| String | A string representation of the VibratorStopMode.   |

### func !=(VibratorStopMode)

```cangjie
public operator func !=(other: VibratorStopMode): Bool
```

**Function:** Compares this VibratorStopMode with another for inequality.

**Parameters:**

| Parameter | Type                                    | Required | Default | Description                      |
|:----------|:----------------------------------------|:---------|:--------|:---------------------------------|
| other     | [VibratorStopMode](#enum-vibratorstopmode) | Yes      | -       | The VibratorStopMode to compare with. |

**Return Value:**

| Type | Description                                       |
|:-----|:--------------------------------------------------|
| Bool | True if both modes are not equal, false otherwise. |

### func ==(VibratorStopMode)

```cangjie
public operator func ==(other: VibratorStopMode): Bool
```

**Function:** Compares this VibratorStopMode with another for equality.

**Parameters:**

| Parameter | Type                                    | Required | Default | Description                      |
|:----------|:----------------------------------------|:---------|:--------|:---------------------------------|
| other     | [VibratorStopMode](#enum-vibratorstopmode) | Yes      | -       | The VibratorStopMode to compare with. |

**Return Value:**

| Type | Description                                   |
|:-----|:----------------------------------------------|
| Bool | True if both modes are equal, false otherwise. |

## type Usage

```cangjie
public type Usage = String
```

**Function:** Enumerates the vibration scenarios. The options include **unknown**, **alarm**, **ring**, **notification**, **communication**, **touch**, **media**, **physicalFeedback**, and **simulateReality**.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

| Supported Value    | Description                          |
|:------------------|:-------------------------------------|
| "unknown"          | No specific usage scenario, lowest priority. |
| "alarm"            | Alarm scenario.                     |
| "ring"             | Ring scenario.                      |
| "notification"     | Notification scenario.              |
| "communication"    | Communication scenario.             |
| "touch"            | Touch scenario.                     |
| "media"            | Media scenario.                     |
| "physicalFeedback" | Physical feedback scenario.         |
| "simulateReality"  | Simulated reality scenario.         |

## class VibrateAttribute

```cangjie
public class VibrateAttribute {
    public mut prop id: ?Int32
    public mut prop usage: Usage
    public init(usage: Usage, id!: ?Int32 = None)
}
```

**Function:** Describes the vibration attribute.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop id

```cangjie
public mut prop id: ?Int32
```

**Function:** Vibrator ID. The default value is **0**.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop usage

```cangjie
public mut prop usage: Usage
```

**Function:** Vibration scenario. The default value is **unknown**. The value must be an enum defined in **Usage**.

**Type:** [Usage](#type-usage)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### init(Usage, ?Int32)

```cangjie
public init(usage: Usage, id!: ?Int32 = None)
```

**Function:** A constructor used to create a VibrateAttribute.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type              | Required | Default | Description                                                                  |
|:-------------- |:------------------|:-------- |:------- |:---------------------------------------------------------------------------- |
| usage          | [Usage](#type-usage) | Yes      | -       | Vibration scenario. The default value is **unknown**. The value must be an enum defined in **Usage**. |
| id             | ?Int32            | No       | None    | Vibrator ID. The default value is **0**.                                     |

**Example:**

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

**Function:** Enumerates vibration effects of the vibrator. You can specify the vibration effect when calling **startVibration**. The value can be **VibrateTimeType(VibrateTime)**, **VibratePresetType(VibratePreset)**, **VibrateFromFileType(VibrateFromFile)**, or **VibrateFromPatternType(VibrateFromPattern)**.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### VibrateTimeType(VibrateTime)

```cangjie
VibrateTimeType(VibrateTime)
```

**Function:** Vibration of the specified duration.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### VibratePresetType(VibratePreset)

```cangjie
VibratePresetType(VibratePreset)
```

**Function:** Preset vibration effect.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### VibrateFromFileType(VibrateFromFile)

```cangjie
VibrateFromFileType(VibrateFromFile)
```

**Function:** Custom vibration pattern triggered based on a vibration configuration file.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

## class VibrateTime

```cangjie
public class VibrateTime {
    public mut prop effectType: String
    public mut prop duration: Int32
    public init(effectType: String, duration: Int32)
}
```

**Function:** Represents vibration of the specified duration.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**Function:** The value is **time**, indicating vibration of the specified duration.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop duration

```cangjie
public mut prop duration: Int32
```

**Function:** Vibration duration, in ms. The value range is (0,1800000]. The maximum vibration duration varies with devices due to different component protection design specifications of drivers provided by different vendors. It is recommended that a single vibration duration be less than or equal to 10s for a better user experience.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### init(String, Int32)

```cangjie
public init(effectType: String, duration: Int32)
```

**Function:** A constructor used to create a VibrateTime.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type   | Required | Default | Description                                                                  |
|:-------------- |:-------|:-------- |:------- |:---------------------------------------------------------------------------- |
| effectType     | String | Yes      | -       | The value is **time**, indicating vibration of the specified duration.       |
| duration       | Int32  | Yes      | -       | Vibration duration, in ms. The value range is (0,1800000].                   |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let vibrateTime = VibrateTime("time", 1000)
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

**Function:** Represents the preset vibration effect. You can pass **VibratePreset** to **VibrateEffect** to specify a preset vibration effect when calling **startVibration**.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**Function:** The value **preset** means that vibration is triggered based on the specified effect.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop effectId

```cangjie
public mut prop effectId: String
```

**Function:** Effect ID. The value is a string of a maximum of 64 characters. If the length exceeds 64 characters, the first 64 characters are used.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop count

```cangjie
public mut prop count: ?Int32
```

**Function:** Number of repeated vibrations. This parameter is optional. The default value is **1**.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop intensity

```cangjie
public mut prop intensity: ?Int32
```

**Function:** Vibration intensity. This parameter is optional. The value range is [0, 100]. The default value is **100**. If vibration intensity adjustment is not supported, the default vibration intensity will be used.

**Type:** ?Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### init(String, String, ?Int32, ?Int32)

```cangjie
public init(effectType: String, effectId: String, count!: ?Int32 = None, intensity!: ?Int32 = None)
```

**Function:** A constructor used to create a VibratePreset.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type   | Required | Default | Description                                                                                              |
|:-------------- |:-------|:-------- |:------- |:-------------------------------------------------------------------------------------------------------- |
| effectType     | String | Yes      | -       | The value **preset** means that vibration is triggered based on the specified effect.                    |
| effectId       | String | Yes      | -       | Effect ID. The value is a string of a maximum of 64 characters.                                          |
| count          | ?Int32 | No       | None    | Number of repeated vibrations. This parameter is optional. The default value is **1**.                   |
| intensity      | ?Int32 | No       | None    | Vibration intensity. This parameter is optional. The value range is [0, 100]. The default value is **100**. |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let vibratePreset = VibratePreset("preset", "haptic.clock.timer", count: 1)
```

## class VibrateFromFile

```cangjie
public class VibrateFromFile {
    public mut prop effectType: String
    public mut prop hapticFd: HapticFileDescriptor
    public init(effectType: String, hapticFd: HapticFileDescriptor)
}
```

**Function:** Represents a custom vibration pattern. It is supported only by certain devices. An error code will be returned if a device does not support this vibration mode. You can pass **VibrateFromFile** to **VibrateEffect** to specify a custom vibration pattern when calling **startVibration**.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop effectType

```cangjie
public mut prop effectType: String
```

**Function:** The value **file** means vibration according to a vibration configuration file.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop hapticFd

```cangjie
public mut prop hapticFd: HapticFileDescriptor
```

**Function:** File descriptor (FD) of the vibration configuration file.

**Type:** [HapticFileDescriptor](#class-hapticfiledescriptor)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### init(String, HapticFileDescriptor)

```cangjie
public init(effectType: String, hapticFd: HapticFileDescriptor)
```

**Function:** A constructor used to create a VibrateFromFile.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type                                              | Required | Default | Description                                                |
|:-------------- |:--------------------------------------------------|:-------- |:------- |:---------------------------------------------------------- |
| effectType     | String                                            | Yes      | -       | The value **file** means vibration according to a vibration configuration file. |
| hapticFd       | [HapticFileDescriptor](#class-hapticfiledescriptor) | Yes      | -       | File descriptor (FD) of the vibration configuration file. |

**Example:**

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

**Function:** Describes the FD of a custom vibration configuration file. Ensure that the file is available, and the parameters in it can be obtained from the sandbox path through the **fileIo.open** API or from the HAP resource through the **getRawFd** API. The application scenario is as follows: The vibration sequence is stored in a file and vibration needs to be triggered based on the offset and length.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop fd

```cangjie
public mut prop fd: Int32
```

**Function:** FD of the custom vibration configuration file.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop offSet

```cangjie
public mut prop offSet: ?Int64
```

**Function:** Offset from the start position of the file, in bytes. The default value is the start position of the file, and the value cannot exceed the valid range of the file.

**Type:** ?Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### prop length

```cangjie
public mut prop length: ?Int64
```

**Function:** Resource length, in bytes. The default value is the length from the offset position to the end of the file, and the value cannot exceed the valid range of the file.

**Type:** ?Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

### init(Int32, ?Int64, ?Int64)

```cangjie
public init(fd: Int32, offSet!: ?Int64 = None, length!: ?Int64 = None)
```

**Function:** A constructor used to create a HapticFileDescriptor.

**System Capability:** SystemCapability.Sensors.MiscDevice

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type   | Required | Default | Description                                                                                          |
|:-------------- |:-------|:-------- |:------- |:---------------------------------------------------------------------------------------------------- |
| fd             | Int32  | Yes      | -       | FD of the custom vibration configuration file.                                                       |
| offSet         | ?Int64 | No       | None    | Offset from the start position of the file, in bytes. The default value is the start position of the file. |
| length         | ?Int64 | No       | None    | Resource length, in bytes. The default value is the length from the offset position to the end of the file. |

**Example:**

<!-- compile -->

```cangjie
// index.cj
import kit.SensorServiceKit.*

let descriptor = HapticFileDescriptor(Int32(1))
```
