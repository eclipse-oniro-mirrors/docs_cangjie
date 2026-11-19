# Vibrator Development Guide

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Scenario Description

When a device needs to set different vibration effects, the motor vibration interface can be used. For example, device keys can set vibrations of different durations and intensities, and alarms and incoming calls can set single or periodic vibrations of different intensities and durations.

For detailed API documentation, refer to [Vibrator API](../../reference/SensorServiceKit/cj-apis-vibrator.md).

## Interface Specifications

| Name | Description |
| -------- | -------- |
| startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;Unit&gt;): Unit | Starts vibration based on a specified effect and attribute. This API uses an asynchronous callback to return the result. |
| stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;Unit&gt;): Unit | Stops vibration in the specified mode. This API uses an asynchronous callback to return the result. |
| isSupportEffect(effectId: String, callback: AsyncCallback&lt;Bool&gt;): Unit | Queries whether a specified effect ID is supported. This API uses an asynchronous callback to return the result. |
| isHdHapticSupported(): Bool | Queries whether HD vibration is supported. |

## Vibration Effect Description

Three types of vibration effects are supported:

- **Fixed-duration vibration**: A fixed vibration duration is specified, and the device vibrates at the default intensity and frequency. Corresponds to the `VibrateTime` class, with `effectType` set to `"time"`.
- **Preset vibration**: Uses the system built-in `EffectId` to trigger vibration, suitable for fixed scenarios. For example, `"haptic.clock.timer"` is typically used for vibration feedback when the user adjusts a timer. Corresponds to the `VibratePreset` class, with `effectType` set to `"preset"`.
- **Custom vibration**: The user arranges the vibration pattern through a custom vibration configuration file. Corresponds to the `VibrateFromFile` class, with `effectType` set to `"file"`. Only supported on some devices; returns error code 801 when unsupported.

The custom vibration configuration file is in JSON format, containing `MetaData` and `Channels` sections:

1. `MetaData` contains file header information with the following attributes:
   - `Version` (required): Version number, currently `"1.0"`.
   - `ChannelNumber` (required): Number of channels, supports up to dual motors.
   - `Create` (optional): Creation time.
   - `Description` (optional): Additional description.

2. `Channels` is a JSON array containing `Parameters` and `Pattern`:
   - `Parameters`: `Index` indicates the channel number, 0 for all channels, 1/2 for left/right motors.
   - `Pattern`: Vibration sequence containing multiple `Event` entries.

3. `Event` supports two vibration types:
   - `transient`: Transient short vibration, crisp and forceful, with short duration.
   - `continuous`: Steady-state long vibration, outputs strong vibration for extended periods, and can be configured with `Curve` for vibration curves.

   `Event` attributes include: `Type` (vibration event type), `StartTime` (start time in ms, range [0, 1800000]), `Duration` (duration, only valid for `continuous`, in ms, range [0, 5000]).

4. `Parameters` attributes: `Intensity` (intensity, range [0, 100], representing percentage of maximum vibration), `Frequency` (frequency, range [0, 100], maximum at 55), `Curve` (vibration curve, only valid for `continuous`, 4-16 adjustment points).

Other requirements: The number of vibration events must not exceed 128, and the configuration file size must not exceed 64 KB.

## Development Procedure

1. Import modules.

   <!-- compile -->

   ```cangjie
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog
   ```

2. Configure permissions. For details, see [Declaring Permissions](../../security/AccessToken/cj-declare-permissions.md).

   The `ohos.permission.VIBRATE` permission is required.

3. Trigger motor vibration.

   Use the `startVibration` API to trigger motor vibration based on a specified effect and attribute.

   Scenario 1: Vibrate for a specified duration.

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

   Scenario 2: Vibrate with a preset effect.

   <!-- compile -->

   ```cangjie
   // index.cj
   import kit.SensorServiceKit.*
   import kit.CangjieKit.AsyncCallback
   import kit.CangjieKit.BusinessException
   import kit.PerformanceAnalysisKit.Hilog

   func startVibrationPresetExample() {
       try {
           // Query whether the effect is supported first
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

   Scenario 3: Vibrate with a custom configuration file.

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

4. Stop motor vibration.

   Use the `stopVibration` API to stop motor vibration in the specified mode.

   Method 1: Stop fixed-duration vibration.

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

   Method 2: Stop preset effect vibration.

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

   > **Note:**
   >
   > Custom vibration does not support stopping via `VibratorStopMode`. To stop custom vibration, stop all vibration modes.

5. Query whether HD vibration is supported.

   Use the `isHdHapticSupported` API to synchronously query whether the device supports HD vibration.

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

## Notes

- The choice of vibration effect should be based on the actual scenario: simple notifications can use fixed-duration vibration, system scenarios can use preset vibration, and personalized experiences can use custom vibration.
- The `usage` in `VibrateAttribute` specifies the vibration scenario. Different scenarios correspond to different vibration priorities, and the system manages vibration conflicts based on priority.
- Custom vibration configuration files must ensure that the resource file is available. Files can be obtained from HAP resources via ResourceManager or accessed via sandbox paths.
