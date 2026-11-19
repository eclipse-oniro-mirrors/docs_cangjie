# 振动开发指导

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

## 场景介绍

当设备需要设置不同的振动效果时，可以通过马达振动接口实现，例如：设备按键设置不同时长和强度的振动，闹钟和来电设置不同强度和时长的单次或周期振动等。

详细的API介绍请参见[Vibrator API](../../reference/SensorServiceKit/cj-apis-vibrator.md)。

## 接口说明

| 名称 | 描述 |
| -------- | -------- |
| startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;Unit&gt;): Unit | 根据指定的振动效果和振动属性触发马达振动，使用Callback异步回调。 |
| stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;Unit&gt;): Unit | 按照指定模式停止马达的振动，使用Callback异步回调。 |
| isSupportEffect(effectId: String, callback: AsyncCallback&lt;Bool&gt;): Unit | 查询是否支持传入的参数effectId，使用Callback异步回调。 |
| isHdHapticSupported(): Bool | 查询是否支持高清振动。 |

## 振动效果说明

振动效果支持三种类型：

- **固定时长振动**：传入固定的振动时长，按默认强度和频率振动。对应`VibrateTime`类，`effectType`值为`"time"`。
- **预置振动**：使用系统内置的`EffectId`触发振动，适用于固定场景，如`"haptic.clock.timer"`通常用于用户调整计时器时的振感反馈。对应`VibratePreset`类，`effectType`值为`"preset"`。
- **自定义振动**：用户通过自定义振动配置文件编排振动形式。对应`VibrateFromFile`类，`effectType`值为`"file"`。仅部分设备支持，不支持时返回错误码801。

自定义振动配置文件为JSON格式，包含`MetaData`和`Channels`两部分：

1. `MetaData`属性中为文件头信息，可在如下属性中添加描述：
   - `Version`（必填）：版本号，目前为`"1.0"`。
   - `ChannelNumber`（必填）：通道数，最大支持双马达。
   - `Create`（选填）：创作时间。
   - `Description`（选填）：附加说明。

2. `Channels`属性为JSON数组，包含`Parameters`和`Pattern`：
   - `Parameters`：`Index`表示通道编号，0表示全通道，1/2分别表示左右马达。
   - `Pattern`：振动序列，包含若干`Event`。

3. `Event`支持两种振动类型：
   - `transient`：瞬态短振动，振动干脆有力，持续时间短。
   - `continuous`：稳态长振动，长时间输出强劲振动，可通过`Curve`配置振动曲线。

   `Event`属性包括：`Type`（振动事件类型）、`StartTime`（起始时间，单位ms，范围[0, 1800000]）、`Duration`（持续时间，仅`continuous`有效，单位ms，范围[0, 5000]）。

4. `Parameters`属性：`Intensity`（强度，范围[0,100]，表示最大振动量百分比）、`Frequency`（频率，范围[0,100]，55时为谐振频率振动量最大）、`Curve`（振动曲线，仅`continuous`有效，调节点数量4-16个）。

其余要求：振动事件数量不超过128个，振动配置文件长度不超过64KB。

## 开发步骤

1. 导入模块。

   <!-- compile -->

   ```cangjie
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog
   ```

2. 配置权限，具体配置方式请参见[声明权限](../../security/AccessToken/cj-declare-permissions.md)。

   需要配置`ohos.permission.VIBRATE`权限。

3. 触发马达振动。

   可以通过`startVibration`接口，根据指定的振动效果和振动属性触发马达振动。

   情形一：按指定持续时间振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func startVibrationTimeExample() {
       let vibrateTime = VibrateTime("time", 1000)
       let effect = VibrateEffect.VibrateTimeType(vibrateTime)
       let attribute = VibrateAttribute("alarm")
       try {
           startVibration(effect, attribute) { err =>
               if (err != None) {
                   Hilog.error(0, "test", "startVibration failed")
                   return
               }
               Hilog.info(0, "test", "startVibration success")
           }
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "startVibration exception: ${e.message}")
       }
   }
   ```

   情形二：按预置振动效果振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func startVibrationPresetExample() {
       try {
           // 先查询是否支持该效果
           isSupportEffect("haptic.clock.timer") { err, isSupport =>
               if (err != None) {
                   Hilog.error(0, "test", "isSupportEffect failed")
                   return
               }
               if (!isSupport) {
                   Hilog.info(0, "test", "effect not supported")
                   return
               }
               let vibratePreset = VibratePreset("preset", "haptic.clock.timer")
               let effect = VibrateEffect.VibratePresetType(vibratePreset)
               let attribute = VibrateAttribute("alarm")
               try {
                   startVibration(effect, attribute) { err1 =>
                       if (err1 != None) {
                           Hilog.error(0, "test", "startVibration failed")
                           return
                       }
                       Hilog.info(0, "test", "startVibration success")
                   }
               } catch (e: BusinessException) {
                   Hilog.error(0, "test", "startVibration exception: ${e.message}")
               }
           }
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "isSupportEffect exception: ${e.message}")
       }
   }
   ```

   情形三：按自定义振动配置文件振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func startVibrationFromFileExample(fd: Int32, offset: Int64, length: Int64) {
       let hapticFd = HapticFileDescriptor(Int32(fd), offSet: Some(Int64(offset)), length: Some(Int64(length)))
       let vibrateFromFile = VibrateFromFile("file", hapticFd)
       let effect = VibrateEffect.VibrateFromFileType(vibrateFromFile)
       let attribute = VibrateAttribute("ring")
       try {
           startVibration(effect, attribute) { err =>
               if (err != None) {
                   Hilog.error(0, "test", "startVibration failed")
                   return
               }
               Hilog.info(0, "test", "startVibration success")
           }
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "startVibration exception: ${e.message}")
       }
   }
   ```

4. 停止马达振动。

   通过`stopVibration`接口，按照指定模式停止马达振动。

   方式一：停止固定时长振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func stopVibrationTimeExample() {
       try {
           stopVibration(VibratorStopMode.VibratorStopModeTime) { err =>
               if (err != None) {
                   Hilog.error(0, "test", "stopVibration failed")
                   return
               }
               Hilog.info(0, "test", "stopVibration success")
           }
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "stopVibration exception: ${e.message}")
       }
   }
   ```

   方式二：停止预置效果振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func stopVibrationPresetExample() {
       try {
           stopVibration(VibratorStopMode.VibratorStopModePreset) { err =>
               if (err != None) {
                   Hilog.error(0, "test", "stopVibration failed")
                   return
               }
               Hilog.info(0, "test", "stopVibration success")
           }
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "stopVibration exception: ${e.message}")
       }
   }
   ```

   > **说明：**
   >
   > 自定义振动不支持通过`VibratorStopMode`停止。如需停止自定义振动，请停止所有模式的振动。

5. 查询是否支持高清振动。

   通过`isHdHapticSupported`接口，同步查询设备是否支持高清振动。

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func isHdHapticSupportedExample() {
       try {
           let isSupported = isHdHapticSupported()
           Hilog.info(0, "test", "isHdHapticSupported: ${isSupported}")
       } catch (e: BusinessException) {
           Hilog.error(0, "test", "isHdHapticSupported exception: ${e.message}")
       }
   }
   ```

## 备注

- 振动效果的选择应根据实际场景确定：简单提示可使用固定时长振动，系统场景可使用预置振动，个性化体验可使用自定义振动。
- `VibrateAttribute`中的`usage`用于指定振动场景，不同场景对应不同振动优先级，系统会根据优先级进行振动冲突管理。
- 自定义振动配置文件需确保资源文件可用，文件可通过ResourceManager从HAP资源中获取或通过沙箱路径访问。
<!--Del-->
## 示例代码

[振动](https://gitcode.com/openharmony/applications_app_samples_cangjie/tree/master/code/BasicFeature/DeviceManagement/Sensor)
<!--DelEnd-->
