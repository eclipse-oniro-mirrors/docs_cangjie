# ohos.sensor (Sensors)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The sensor module provides capabilities to obtain sensor data, including retrieving sensor attribute lists, subscribing to sensor data, and some common sensor algorithms.

## Import Module

```cangjie
import kit.SensorServiceKit.*
```

## Permission List

ohos.permission.ACCELEROMETER

ohos.permission.GYROSCOPE

ohos.permission.READ_HEALTH_DATA

ohos.permission.ACTIVITY_MOTION

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func getSensorList()

```cangjie
public func getSensorList(): Array<Sensor>
```

**Function:** Retrieves all sensor information on the device.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Return Value:**

| Type                              | Description          |
|:--------------------------------- |:------------------- |
| Array\<[Sensor](#class-sensor)> | Returns the sensor attribute list. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Sensor Error Codes](./cj-errorcode-sensor.md) and [Universal Error Codes](../cj-errorcode-universal.md).
  
  | Error Code ID | Error Message                                                                                                                                |
  |:------------ |:------------------------------------------------------------------------------------------------------------------------------------------- |
  | 14500101     | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception; 3. Sensor data channel exception. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    let sensors = getSensorList()
    for (index in 0..sensors.size) {
        Hilog.info(0, "test", "Succeeded in getting sensor${index}: ${sensors[index].sensorId}", "")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "Failed to get sensor list. Code: ${e.code}, message: ${e.message}", "")
}
```

## func getSingleSensor(SensorId)

```cangjie
public func getSingleSensor(sensorType: SensorId): Sensor
```

**Function:** Retrieves information about a specified type of sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                         | Required | Default | Description     |
|:------------- |:-------------------------- |:------- |:----- |:-------------- |
| sensorType    | [SensorId](#enum-sensorid) | Yes      | -     | The sensor type. |

**Return Value:**

| Type                      | Description       |
|:----------------------- |:---------------- |
| [Sensor](#class-sensor) | Returns sensor information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Sensor Error Codes](./cj-errorcode-sensor.md) and [Universal Error Codes](../cj-errorcode-universal.md).
  
  | Error Code ID | Error Message                                                                                                                                |
  |:------------ |:------------------------------------------------------------------------------------------------------------------------------------------- |
  | 14500101     | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception; 3. Sensor data channel exception. |
  | 14500102     | The sensor is not supported by the device.                                                                                              |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    let sensors = getSingleSensor(SensorId.Accelerometer)
    Hilog.info(0, "test", "Succeeded in getting sensor: ${sensors.sensorName}", "")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

## func off(SensorId, ?CallbackObject)

```cangjie
public func off(sensorType: SensorId, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                                                                                 | Required | Default | Description                                          |
|:------------- |:---------------------------------------------------------------------------------- |:------- |:------ |:--------------------------------------------------- |
| sensorType    | [SensorId](#enum-sensorid)                                                         | Yes      | -      | The sensor type.                                      |
| callback      | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No       | None   | **Named parameter.** The callback function for asynchronously reported sensor data. The data type varies by sensor type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class SensorCallback <: Callback1Argument<OrientationResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: OrientationResponse): Unit {
        Hilog.info(0, "test", "Succeeded in getting SensorCallback1 arg: steps: ${arg.timestamp}, alpha: ${arg.alpha},  beta: ${arg.beta},  gamma: ${arg.gamma}", "")
    }
}

let callback1 = SensorCallback()
let callback2 = SensorCallback()
try {
    on(SensorId.Orientation, callback1)
    on(SensorId.Orientation, callback2)
    // Only unregister callback1
    off(SensorId.Orientation, callback: callback1)
    // Unregister all callbacks for SensorId.ORIENTATION
    off(SensorId.Orientation)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

## func on\<T>(SensorId, Callback1Argument\<T>, ?Options) where T \<: Response

```cangjie
public func on<T>(sensorType: SensorId, callback: Callback1Argument<T>, option!: ?Options = None): Unit where T <: Response
```

**Function:** Subscribes to sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                                                                                          | Required | Default | Description                                  |
|:------------- |:------------------------------------------------------------------------------------------- |:------- |:------ |:------------------------------------------- |
| sensorType    | [SensorId](#enum-sensorid)                                                                  | Yes      | -      | The sensor type.                              |
| callback      | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | Yes      | -      | The callback function.                       |
| option        | ?[Options](#class-options)                                                                  | No       | None   | Optional parameter list for setting the sensor reporting frequency. Default is 200000000ns. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class AccelerometerCallback <: Callback1Argument<AccelerometerResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: AccelerometerResponse): Unit {
        Hilog.info(0, "test", "Succeeded in getting AccelerometerCallback arg: timestamp: ${arg.timestamp}, x: ${arg.x},  y: ${arg.y},  z: ${arg.z}", "")
    }
}

let callback = AccelerometerCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    on(SensorId.Accelerometer, callback, option: options)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

## func once\<T>(SensorId, Callback1Argument\<T>) where T \<: Response

```cangjie
public func once<T>(sensorType: SensorId, callback: Callback1Argument<T>): Unit where T <: Response
```

**Function:** Retrieves sensor data once.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type                                                                                          | Required | Default | Description                                |
|:------------- |:------------------------------------------------------------------------------------------- |:------- |:------ |:----------------------------------------- |
| sensorType    | [SensorId](#enum-sensorid)                                                                  | Yes      | -      | The sensor type.                            |
| callback      | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | Yes      | -      | The callback function for asynchronously reported sensor data. The data type varies by sensor type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class GyroscopeCallback <: Callback1Argument<GyroscopeResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: GyroscopeResponse): Unit {
        Hilog.info(0, "test", "Succeeded in getting GyroscopeCallback arg: timestamp: ${arg.timestamp}, x: ${arg.x},  y: ${arg.y},  z: ${arg.z}", "")
    }
}

let callback = GyroscopeCallback()
try {
    once(SensorId.Gyroscope, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

## class AccelerometerResponse

```cangjie
public class AccelerometerResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Function:** Accelerometer sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Acceleration applied to the device's x-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Acceleration applied to the device's y-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Acceleration applied to the device's z-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

## class AccelerometerUncalibratedResponse

```cangjie
public class AccelerometerUncalibratedResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var biasX: Float32
    public var biasY: Float32
    public var biasZ: Float32
}
```

**Function:** Uncalibrated accelerometer sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Parent Type:**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**Function:** Uncalibrated acceleration bias applied to the device's x-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var biasY

```cangjie
public var biasY: Float32
```

**Function:** Uncalibrated acceleration bias applied to the device's y-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**Function:** Uncalibrated acceleration bias applied to the device's z-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var x

```cangjie
public var x: Float32
```

**Function:** Uncalibrated acceleration applied to the device's x-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Uncalibrated acceleration applied to the device's y-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Uncalibrated acceleration applied to the device's z-axis, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22## class AmbientTemperatureResponse

```cangjie
public class AmbientTemperatureResponse <: Response {
    public var temperature: Float32
}
```

**Description:** Ambient temperature sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var temperature

```cangjie
public var temperature: Float32
```

**Description:** Ambient temperature (unit: Celsius).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class BarometerResponse

```cangjie
public class BarometerResponse <: Response {
    public var pressure: Float32
}
```

**Description:** Barometer sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var pressure

```cangjie
public var pressure: Float32
```

**Description:** Pressure value (unit: hectopascal).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class GravityResponse

```cangjie
public class GravityResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Description:** Gravity sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Description:** Gravity acceleration applied on the device's x-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Description:** Gravity acceleration applied on the device's y-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Description:** Gravity acceleration applied on the device's z-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class GyroscopeResponse

```cangjie
public class GyroscopeResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Description:** Gyroscope sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Description:** Angular velocity of rotation around the device's x-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Description:** Angular velocity of rotation around the device's y-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Description:** Angular velocity of rotation around the device's z-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class GyroscopeUncalibratedResponse

```cangjie
public class GyroscopeUncalibratedResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var biasX: Float32
    public var biasY: Float32
    public var biasZ: Float32
}
```

**Description:** Uncalibrated gyroscope sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**Description:** Uncalibrated angular velocity bias around the device's x-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var biasY

```cangjie
public var biasY: Float32
```

**Description:** Uncalibrated angular velocity bias around the device's y-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**Description:** Uncalibrated angular velocity bias around the device's z-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var x

```cangjie
public var x: Float32
```

**Description:** Uncalibrated angular velocity around the device's x-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Description:** Uncalibrated angular velocity around the device's y-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Description:** Uncalibrated angular velocity around the device's z-axis (unit: rad/s).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class HallResponse

```cangjie
public class HallResponse <: Response {
    public var status: Float32
}
```

**Description:** Hall effect sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var status

```cangjie
public var status: Float32
```

**Description:** Hall effect status. Detects magnetic presence around the device: 0 indicates absence, >0 indicates presence.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class HeartRateResponse

```cangjie
public class HeartRateResponse <: Response {
    public var heartRate: Float32
}
```

**Description:** Heart rate sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var heartRate

```cangjie
public var heartRate: Float32
```

**Description:** Heart rate value (unit: beats per minute, bpm).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class HumidityResponse

```cangjie
public class HumidityResponse <: Response {
    public var humidity: Float32
}
```

**Description:** Humidity sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var humidity

```cangjie
public var humidity: Float32
```

**Description:** Relative humidity value (unit: percentage, %).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22## class LightResponse

```cangjie
public class LightResponse <: Response {
    public var intensity: Float32
    public var colorTemperature:?Float32
    public var infraredLuminance:?Float32
}
```

**Function:** Ambient light sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var colorTemperature

```cangjie
public var colorTemperature:?Float32
```

**Function:** Color temperature (unit: Kelvin), optional parameter. Returns undefined at the JS layer if unsupported, otherwise returns the actual value.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var infraredLuminance

```cangjie
public var infraredLuminance:?Float32
```

**Function:** Infrared luminance (unit: cd/m²), optional parameter. Returns undefined at the JS layer if unsupported, otherwise returns the actual value.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var intensity

```cangjie
public var intensity: Float32
```

**Function:** Light intensity (unit: lux).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class LinearAccelerometerResponse

```cangjie
public class LinearAccelerometerResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Function:** Linear acceleration sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Linear acceleration applied to the device's x-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Linear acceleration applied to the device's y-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Linear acceleration applied to the device's z-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class MagneticFieldResponse

```cangjie
public class MagneticFieldResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Function:** Magnetic field sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Ambient magnetic field strength on the x-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Ambient magnetic field strength on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Ambient magnetic field strength on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class MagneticFieldUncalibratedResponse

```cangjie
public class MagneticFieldUncalibratedResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var biasX: Float32
    public var biasY: Float32
    public var biasZ: Float32
}
```

**Function:** Uncalibrated magnetic field sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**Function:** Uncalibrated ambient magnetic field bias on the x-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var biasY

```cangjie
public var biasY: Float32
```

**Function:** Uncalibrated ambient magnetic field bias on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**Function:** Uncalibrated ambient magnetic field bias on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var x

```cangjie
public var x: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the x-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class Options

```cangjie
public class Options {
    public var interval: IntervalOption
    public var sensorInfoParam:?SensorInfoParam
    public init(interval!: IntervalOption = NormalMode, sensorInfoParam!: ?SensorInfoParam = None)
}
```

**Function:** Sensor configuration options.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var interval

```cangjie
public var interval: IntervalOption
```

**Function:** Sensor reporting frequency.

**Type:** [IntervalOption](#enum-intervaloption)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var sensorInfoParam

```cangjie
public var sensorInfoParam:?SensorInfoParam
```

**Function:** Sensor information parameters.

**Type:** ?[SensorInfoParam](#class-sensorinfoparam)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### init(IntervalOption, ?SensorInfoParam)

```cangjie
public init(interval!: IntervalOption = NormalMode, sensorInfoParam!: ?SensorInfoParam = None)
```

**Function:** Constructor to create an Options instance.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parameters:**

| Parameter        | Type                                         | Required | Default      | Description               |
|:---------------- |:------------------------------------------ |:-------- |:----------- |:------------------------ |
| interval         | [IntervalOption](#enum-intervaloption)     | No       | NormalMode  | Sensor reporting frequency. |
| sensorInfoParam  | ?[SensorInfoParam](#class-sensorinfoparam) | No       | None        | Sensor information parameters. |

## class OrientationResponse

```cangjie
public class OrientationResponse <: Response {
    public var alpha: Float32
    public var beta: Float32
    public var gamma: Float32
}
```

**Function:** Orientation sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var alpha

```cangjie
public var alpha: Float32
```

**Function:** Rotation angle around the Z-axis (unit: degrees).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var beta

```cangjie
public var beta: Float32
```

**Function:** Rotation angle around the X-axis (unit: degrees).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var gamma

```cangjie
public var gamma: Float32
```

**Function:** Rotation angle around the Y-axis (unit: degrees).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22## class PedometerDetectionResponse

```cangjie
public class PedometerDetectionResponse <: Response {
    public var scalar: Float32
}
```

**Function:** Pedometer detection sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**Function:** Pedometer detection. Detects user's step motion. A value of 1 indicates step movement, while 0 indicates no motion.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class PedometerResponse

```cangjie
public class PedometerResponse <: Response {
    public var steps: Int64
}
```

**Function:** Pedometer sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var steps

```cangjie
public var steps: Int64
```

**Function:** User's step count. Initial value is 0. After subscribing to the pedometer sensor, each step increments the count by one.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class ProximityResponse

```cangjie
public class ProximityResponse <: Response {
    public var distance: Float32
}
```

**Function:** Proximity light sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var distance

```cangjie
public var distance: Float32
```

**Function:** Proximity of visible objects to the device display. 0 indicates proximity, values >0 indicate distance.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class Response

```cangjie
public open class Response {
    public var timestamp: Int64
    public var accuracy: SensorAccuracy
}
```

**Function:** Timestamp of sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var accuracy

```cangjie
public var accuracy: SensorAccuracy
```

**Function:** Accuracy level value reported by sensor data.

**Type:** [SensorAccuracy](#enum-sensoraccuracy)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Timestamp of sensor data reporting.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class RotationVectorResponse

```cangjie
public class RotationVectorResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var w: Float32
}
```

**Function:** Rotation vector sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var w

```cangjie
public var w: Float32
```

**Function:** Scalar component.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var x

```cangjie
public var x: Float32
```

**Function:** X-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var y

```cangjie
public var y: Float32
```

**Function:** Y-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var z

```cangjie
public var z: Float32
```

**Function:** Z-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class Sensor

```cangjie
public class Sensor {
    public var sensorName: String
    public var vendorName: String
    public var firmwareVersion: String
    public var hardwareVersion: String
    public var sensorId: Int32
    public var maxRange: Float32
    public var minSamplePeriod: Int64
    public var maxSamplePeriod: Int64
    public var precision: Float32
    public var power: Float32
}
```

**Function:** Represents sensor information.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var firmwareVersion

```cangjie
public var firmwareVersion: String
```

**Function:** Firmware version of the sensor.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var hardwareVersion

```cangjie
public var hardwareVersion: String
```

**Function:** Hardware version of the sensor.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var maxRange

```cangjie
public var maxRange: Float32
```

**Function:** Maximum measurement range of the sensor.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var maxSamplePeriod

```cangjie
public var maxSamplePeriod: Int64
```

**Function:** Maximum allowed sampling period.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var minSamplePeriod

```cangjie
public var minSamplePeriod: Int64
```

**Function:** Minimum allowed sampling period.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var power

```cangjie
public var power: Float32
```

**Function:** Estimated sensor power consumption in mA.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var precision

```cangjie
public var precision: Float32
```

**Function:** Sensor precision.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var sensorId

```cangjie
public var sensorId: Int32
```

**Function:** Sensor type ID.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var sensorName

```cangjie
public var sensorName: String
```

**Function:** Sensor name.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var vendorName

```cangjie
public var vendorName: String
```

**Function:** Sensor vendor.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22## class SensorInfoParam

```cangjie
public class SensorInfoParam {
    public var deviceId: Int32
    public var sensorIndex: Int32
    public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
}
```

**Function:** Sensor information parameters.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var deviceId

```cangjie
public var deviceId: Int32
```

**Function:** Device ID.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### var sensorIndex

```cangjie
public var sensorIndex: Int32
```

**Function:** Sensor index.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### init(Int32, Int32)

```cangjie
public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
```

**Function:** Constructor to create a SensorInfoParam instance.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parameters:**

| Parameter    | Type  | Required | Default | Description     |
|:------------ |:----- |:-------- |:------- |:-------------- |
| deviceId    | Int32 | No       | -1      | Device ID.      |
| sensorIndex | Int32 | No       | 0       | Sensor index.   |

## class SignificantMotionResponse

```cangjie
public class SignificantMotionResponse <: Response {
    public var scalar: Float32
}
```

**Function:** Significant motion sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**Function:** Indicates the degree of significant motion. Measures whether there is significant motion on the three physical axes (x, y, and z); if significant motion is detected, the reported value is 1.

**Type:** Float32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## class WearDetectionResponse

```cangjie
public class WearDetectionResponse <: Response {
    public var value: Float32
}
```

**Function:** Wear detection sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Type:**

- [Response](#class-response)

### var value

```cangjie
public var value: Float32
```

**Function:** Indicates whether the device is worn (1 means worn, 0 means not worn).

**Type:** Float32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

## enum IntervalOption

```cangjie
public enum IntervalOption <: Equatable<IntervalOption> & ToString {
    | SensorNumber(Int64)
    | GameMode
    | UIMode
    | NormalMode
    | ...
}
```

**Function:** Options for sensor reporting frequency.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Types:**

- [Equatable\<IntervalOption>](../arkui-cj/cj-common-types.md#class-equatable)
- ToString

### GameMode

```cangjie
GameMode
```

**Function:** Specifies the sensor reporting frequency as 20000000ns. This frequency takes effect when set within the hardware-supported frequency range.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### NormalMode

```cangjie
NormalMode
```

**Function:** Specifies the sensor reporting frequency as 200000000ns. This frequency takes effect when set within the hardware-supported frequency range. The value is fixed as the string 'normal'.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### SensorNumber(Int64)

```cangjie
SensorNumber(Int64)
```

**Function:** Custom sensor reporting frequency, specified in nanoseconds.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### UIMode

```cangjie
UIMode
```

**Function:** Specifies the sensor reporting frequency as 60000000ns. This frequency takes effect when set within the hardware-supported frequency range.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### func !=(IntervalOption)

```cangjie
public operator func !=(other: IntervalOption): Bool
```

**Function:** Determines whether two [IntervalOption](#enum-intervaloption) instances are not equal.

**Parameters:**

| Parameter | Type                                     | Required | Default | Description                                         |
|:--------- |:---------------------------------------- |:-------- |:------- |:-------------------------------------------------- |
| other     | [IntervalOption](#enum-intervaloption)   | Yes      | -       | The input [IntervalOption](#enum-intervaloption).  |

**Return Value:**

| Type   | Description                        |
|:------ |:--------------------------------- |
| Bool   | Returns true if not equal; otherwise, false. |

### func ==(IntervalOption)

```cangjie
public operator func ==(other: IntervalOption): Bool
```

**Function:** Determines whether two [IntervalOption](#enum-intervaloption) instances are equal.

**Parameters:**

| Parameter | Type                                     | Required | Default | Description                                         |
|:--------- |:---------------------------------------- |:-------- |:------- |:-------------------------------------------------- |
| other     | [IntervalOption](#enum-intervaloption)   | Yes      | -       | The input [IntervalOption](#enum-intervaloption).  |

**Return Value:**

| Type   | Description                       |
|:------ |:-------------------------------- |
| Bool   | Returns true if equal; otherwise, false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enum value to a string.

**Return Value:**

| Type     | Description       |
|:-------- |:---------------- |
| String   | The converted string. |

## enum SensorAccuracy

```cangjie
public enum SensorAccuracy  <: Equatable<SensorAccuracy> & ToString {
    | AccuracyUnreliable
    | AccuracyLow
    | AccuracyMedium
    | AccuracyHigh
    | ...
}
```

**Function:** Accuracy of sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Types:**

- [Equatable\<SensorAccuracy>](../arkui-cj/cj-common-types.md#class-equatable)
- ToString

### AccuracyHigh

```cangjie
AccuracyHigh
```

**Function:** High accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### AccuracyLow

```cangjie
AccuracyLow
```

**Function:** Low accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### AccuracyMedium

```cangjie
AccuracyMedium
```

**Function:** Medium accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### AccuracyUnreliable

```cangjie
AccuracyUnreliable
```

**Function:** Sensor data is unreliable.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

### func !=(SensorAccuracy)

```cangjie
public operator func !=(other: SensorAccuracy): Bool
```

**Function:** Determines whether two [SensorAccuracy](#enum-sensoraccuracy) instances are not equal.

**Parameters:**

| Parameter | Type                                     | Required | Default | Description                                         |
|:--------- |:---------------------------------------- |:-------- |:------- |:-------------------------------------------------- |
| other     | [SensorAccuracy](#enum-sensoraccuracy)   | Yes      | -       | The input [SensorAccuracy](#enum-sensoraccuracy).  |

**Return Value:**

| Type   | Description                        |
|:------ |:--------------------------------- |
| Bool   | Returns true if not equal; otherwise, false. |

### func ==(SensorAccuracy)

```cangjie
public operator func ==(other: SensorAccuracy): Bool
```

**Function:** Determines whether two [SensorAccuracy](#enum-sensoraccuracy) instances are equal.

**Parameters:**

| Parameter | Type                                     | Required | Default | Description                                         |
|:--------- |:---------------------------------------- |:-------- |:------- |:-------------------------------------------------- |
| other     | [SensorAccuracy](#enum-sensoraccuracy)   | Yes      | -       | The input [SensorAccuracy](#enum-sensoraccuracy).  |

**Return Value:**

| Type   | Description                       |
|:------ |:-------------------------------- |
| Bool   | Returns true if equal; otherwise, false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enum value to a string.

**Return Value:**

| Type     | Description       |
|:-------- |:---------------- |
| String   | The converted string. |

## enum SensorId

```cangjie
public enum SensorId <: Equatable<SensorId> & ToString {
    | Accelerometer
    | Gyroscope
    | AmbientLight
    | MagneticField
    | Barometer
    | Hall
    | Proximity
    | Humidity
    | Orientation
    | Gravity
    | LinearAccelerometer
    | RotationVector
    | AmbientTemperature
    | MagneticFieldUncalibrated
    | GyroscopeUncalibrated
    | SignificantMotion
    | PedometerDetection
    | Pedometer
    | HeartRate
    | WearDetection
    | AccelerometerUncalibrated
    | ...
}
```

**Function:** Represents the currently supported sensor types for subscription or unsubscription.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Parent Types:**

- [Equatable\<SensorId>](../arkui-cj/cj-common-types.md#class-equatable)
- ToString### Accelerometer

```cangjie
Accelerometer
```

**Function:** Acceleration sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class AccelerometerCallback <: Callback1Argument<AccelerometerResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: AccelerometerResponse): Unit {
        Hilog.info(0, "test", "Accelerometer data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}", "")
    }
}

let callback = AccelerometerCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Accelerometer, callback, option: options)

    // Get sensor data once
    once(SensorId.Accelerometer, callback)

    // Unsubscribe from sensor data
    off(SensorId.Accelerometer, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### AccelerometerUncalibrated

```cangjie
AccelerometerUncalibrated
```

**Function:** Uncalibrated accelerometer sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class AccelerometerUncalibratedCallback <: Callback1Argument<AccelerometerUncalibratedResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: AccelerometerUncalibratedResponse): Unit {
        Hilog.info(0, "test", "AccelerometerUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}", "")
    }
}

let callback = AccelerometerUncalibratedCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.AccelerometerUncalibrated, callback, option: options)

    // Get sensor data once
    once(SensorId.AccelerometerUncalibrated, callback)

    // Unsubscribe from sensor data
    off(SensorId.AccelerometerUncalibrated, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### AmbientLight

```cangjie
AmbientLight
```

**Function:** Ambient light sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class LightCallback <: Callback1Argument<LightResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: LightResponse): Unit {
        Hilog.info(0, "test", "Light data: timestamp: ${arg.timestamp}, intensity: ${arg.intensity}", "")
    }
}

let callback = LightCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.AmbientLight, callback, option: options)

    // Get sensor data once
    once(SensorId.AmbientLight, callback)

    // Unsubscribe from sensor data
    off(SensorId.AmbientLight, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### AmbientTemperature

```cangjie
AmbientTemperature
```

**Function:** Ambient temperature sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class AmbientTemperatureCallback <: Callback1Argument<AmbientTemperatureResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: AmbientTemperatureResponse): Unit {
        Hilog.info(0, "test", "AmbientTemperature data: timestamp: ${arg.timestamp}, temperature: ${arg.temperature}", "")
    }
}

let callback = AmbientTemperatureCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.AmbientTemperature, callback, option: options)

    // Get sensor data once
    once(SensorId.AmbientTemperature, callback)

    // Unsubscribe from sensor data
    off(SensorId.AmbientTemperature, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Barometer

```cangjie
Barometer  
```

**Function:** Barometric pressure sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class BarometerCallback <: Callback1Argument<BarometerResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: BarometerResponse): Unit {
        Hilog.info(0, "test", "Barometer data: timestamp: ${arg.timestamp}, pressure: ${arg.pressure}", "")
    }
}

let callback = BarometerCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Barometer, callback, option: options)

    // Get sensor data once
    once(SensorId.Barometer, callback)

    // Unsubscribe from sensor data
    off(SensorId.Barometer, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Gravity

```cangjie
Gravity
```

**Function:** Gravity sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class GravityCallback <: Callback1Argument<GravityResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: GravityResponse): Unit {
        Hilog.info(0, "test", "Gravity data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}", "")
    }
}

let callback = GravityCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Gravity, callback, option: options)

    // Get sensor data once
    once(SensorId.Gravity, callback)

    // Unsubscribe from sensor data
    off(SensorId.Gravity, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Gyroscope

```cangjie
Gyroscope
```

**Function:** Gyroscope sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class GyroscopeCallback <: Callback1Argument<GyroscopeResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: GyroscopeResponse): Unit {
        Hilog.info(0, "test", "Gyroscope data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}", "")
    }
}

let callback = GyroscopeCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Gyroscope, callback, option: options)

    // Get sensor data once
    once(SensorId.Gyroscope, callback)

    // Unsubscribe from sensor data
    off(SensorId.Gyroscope, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### GyroscopeUncalibrated

```cangjie
GyroscopeUncalibrated
```

**Function:** Uncalibrated gyroscope sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class GyroscopeUncalibratedCallback <: Callback1Argument<GyroscopeUncalibratedResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: GyroscopeUncalibratedResponse): Unit {
        Hilog.info(0, "test", "GyroscopeUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}", "")
    }
}

let callback = GyroscopeUncalibratedCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.GyroscopeUncalibrated, callback, option: options)

    // Get sensor data once
    once(SensorId.GyroscopeUncalibrated, callback)

    // Unsubscribe from sensor data
    off(SensorId.GyroscopeUncalibrated, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Hall

```cangjie
Hall
```

**Function:** Hall effect sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class HallCallback <: Callback1Argument<HallResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: HallResponse): Unit {
        Hilog.info(0, "test", "Hall data: timestamp: ${arg.timestamp}, status: ${arg.status}", "")
    }
}

let callback = HallCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Hall, callback, option: options)

    // Get sensor data once
    once(SensorId.Hall, callback)

    // Unsubscribe from sensor data
    off(SensorId.Hall, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```### HeartRate

```cangjie
HeartRate
```

**Function:** Heart rate sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class HeartRateCallback <: Callback1Argument<HeartRateResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: HeartRateResponse): Unit {
        Hilog.info(0, "test", "HeartRate data: timestamp: ${arg.timestamp}, heartRate: ${arg.heartRate}", "")
    }
}

let callback = HeartRateCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.HeartRate, callback, option: options)

    // Get sensor data once
    once(SensorId.HeartRate, callback)

    // Unsubscribe from sensor data
    off(SensorId.HeartRate, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Humidity

```cangjie
Humidity
```

**Function:** Humidity sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class HumidityCallback <: Callback1Argument<HumidityResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: HumidityResponse): Unit {
        Hilog.info(0, "test", "Humidity data: timestamp: ${arg.timestamp}, humidity: ${arg.humidity}", "")
    }
}

let callback = HumidityCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Humidity, callback, option: options)

    // Get sensor data once
    once(SensorId.Humidity, callback)

    // Unsubscribe from sensor data
    off(SensorId.Humidity, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### LinearAccelerometer

```cangjie
LinearAccelerometer
```

**Function:** Linear acceleration sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class LinearAccelerometerCallback <: Callback1Argument<LinearAccelerometerResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: LinearAccelerometerResponse): Unit {
        Hilog.info(0, "test", "LinearAccelerometer data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}", "")
    }
}

let callback = LinearAccelerometerCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.LinearAccelerometer, callback, option: options)

    // Get sensor data once
    once(SensorId.LinearAccelerometer, callback)

    // Unsubscribe from sensor data
    off(SensorId.LinearAccelerometer, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### MagneticField

```cangjie
MagneticField
```

**Function:** Magnetic field sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class MagneticFieldCallback <: Callback1Argument<MagneticFieldResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: MagneticFieldResponse): Unit {
        Hilog.info(0, "test", "MagneticField data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}", "")
    }
}

let callback = MagneticFieldCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.MagneticField, callback, option: options)

    // Get sensor data once
    once(SensorId.MagneticField, callback)

    // Unsubscribe from sensor data
    off(SensorId.MagneticField, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### MagneticFieldUncalibrated

```cangjie
MagneticFieldUncalibrated
```

**Function:** Uncalibrated magnetic field sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class MagneticFieldUncalibratedCallback <: Callback1Argument<MagneticFieldUncalibratedResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: MagneticFieldUncalibratedResponse): Unit {
        Hilog.info(0, "test", "MagneticFieldUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}", "")
    }
}

let callback = MagneticFieldUncalibratedCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.MagneticFieldUncalibrated, callback, option: options)

    // Get sensor data once
    once(SensorId.MagneticFieldUncalibrated, callback)

    // Unsubscribe from sensor data
    off(SensorId.MagneticFieldUncalibrated, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Orientation

```cangjie
Orientation
```

**Function:** Orientation sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class OrientationCallback <: Callback1Argument<OrientationResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: OrientationResponse): Unit {
        Hilog.info(0, "test", "Orientation data: timestamp: ${arg.timestamp}, alpha: ${arg.alpha}, beta: ${arg.beta}, gamma: ${arg.gamma}", "")
    }
}

let callback = OrientationCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Orientation, callback, option: options)

    // Get sensor data once
    once(SensorId.Orientation, callback)

    // Unsubscribe from sensor data
    off(SensorId.Orientation, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Pedometer

```cangjie
Pedometer
```

**Function:** Pedometer sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class PedometerCallback <: Callback1Argument<PedometerResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: PedometerResponse): Unit {
        Hilog.info(0, "test", "Pedometer data: timestamp: ${arg.timestamp}, steps: ${arg.steps}", "")
    }
}

let callback = PedometerCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Pedometer, callback, option: options)

    // Get sensor data once
    once(SensorId.Pedometer, callback)

    // Unsubscribe from sensor data
    off(SensorId.Pedometer, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### PedometerDetection

```cangjie
PedometerDetection
```

**Function:** Pedometer detection sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class PedometerDetectionCallback <: Callback1Argument<PedometerDetectionResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: PedometerDetectionResponse): Unit {
        Hilog.info(0, "test", "PedometerDetection data: timestamp: ${arg.timestamp}, scalar: ${arg.scalar}", "")
    }
}

let callback = PedometerDetectionCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.PedometerDetection, callback, option: options)

    // Get sensor data once
    once(SensorId.PedometerDetection, callback)

    // Unsubscribe from sensor data
    off(SensorId.PedometerDetection, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### Proximity

```cangjie
Proximity
```

**Function:** Proximity light sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class ProximityCallback <: Callback1Argument<ProximityResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: ProximityResponse): Unit {
        Hilog.info(0, "test", "Proximity data: timestamp: ${arg.timestamp}, distance: ${arg.distance}", "")
    }
}

let callback = ProximityCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.Proximity, callback, option: options)

    // Get sensor data once
    once(SensorId.Proximity, callback)

    // Unsubscribe from sensor data
    off(SensorId.Proximity, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### RotationVector

```cangjie
RotationVector
```

**Function:** Rotation vector sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class RotationVectorCallback <: Callback1Argument<RotationVectorResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: RotationVectorResponse): Unit {
        Hilog.info(0, "test", "RotationVector data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, w: ${arg.w}", "")
    }
}

let callback = RotationVectorCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.RotationVector, callback, option: options)

    // Get sensor data once
    once(SensorId.RotationVector, callback)

    // Unsubscribe from sensor data
    off(SensorId.RotationVector, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### SignificantMotion

```cangjie
SignificantMotion
```

**Function:** Significant motion sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class SignificantMotionCallback <: Callback1Argument<SignificantMotionResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: SignificantMotionResponse): Unit {
        Hilog.info(0, "test", "SignificantMotion data: timestamp: ${arg.timestamp}, scalar: ${arg.scalar}", "")
    }
}

let callback = SignificantMotionCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.SignificantMotion, callback, option: options)

    // Get sensor data once
    once(SensorId.SignificantMotion, callback)

    // Unsubscribe from sensor data
    off(SensorId.SignificantMotion, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### WearDetection

```cangjie
WearDetection
```

**Function:** Wear detection sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException
import ohos.callback_invoke.*

class WearDetectionCallback <: Callback1Argument<WearDetectionResponse> {
    init() {}
    public func invoke(err: ?BusinessException, arg: WearDetectionResponse): Unit {
        Hilog.info(0, "test", "WearDetection data: timestamp: ${arg.timestamp}, value: ${arg.value}", "")
    }
}

let callback = WearDetectionCallback()
let options = Options(interval: IntervalOption.SensorNumber(100000000))
try {
    // Subscribe to sensor data
    on(SensorId.WearDetection, callback, option: options)

    // Get sensor data once
    once(SensorId.WearDetection, callback)

    // Unsubscribe from sensor data
    off(SensorId.WearDetection, callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "Code: ${e.code}, message: ${e.message}", "")
}
```

### func !=(SensorId)

```cangjie
public operator func !=(other: SensorId): Bool
```

**Function:** Determines whether two [SensorId](#enum-sensorid) values are not equal.

**Parameters:**

| Parameter | Type                         | Required | Default | Description                              |
|:----------|:----------------------------|:---------|:--------|:----------------------------------------|
| other     | [SensorId](#enum-sensorid)  | Yes      | -       | The input [SensorId](#enum-sensorid).   |

**Return Value:**

| Type   | Description                                   |
|:-------|:---------------------------------------------|
| Bool   | Returns true if not equal; otherwise, false. |

### func ==(SensorId)

```cangjie
public operator func ==(other: SensorId): Bool
```

**Function:** Determines whether two [SensorId](#enum-sensorid) values are equal.

**Parameters:**

| Parameter | Type                         | Required | Default | Description                              |
|:----------|:----------------------------|:---------|:--------|:----------------------------------------|
| other     | [SensorId](#enum-sensorid)  | Yes      | -       | The input [SensorId](#enum-sensorid).   |

**Return Value:**

| Type   | Description                                   |
|:-------|:---------------------------------------------|
| Bool   | Returns true if equal; otherwise, false.     |

### func getValue()

```cangjie
public func getValue(): Int32
```

**Function:** Gets the enumeration value.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 22

**Return Value:**

| Type    | Description       |
|:--------|:------------------|
| Int32   | The enumeration value. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enumeration value to a string.

**Return Value:**

| Type     | Description           |
|:---------|:----------------------|
| String   | The converted string. |