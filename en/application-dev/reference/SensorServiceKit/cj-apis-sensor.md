# ohos.sensor (Sensors)

The sensor module provides capabilities to obtain sensor data, including retrieving sensor attribute lists, subscribing to sensor data, and some common sensor algorithms.

## Import Module

```cangjie
import kit.SensorServiceKit.*
```

## Permission List

ohos.permission.ACCELEROMETER

ohos.permission.GYROSCOPE

ohos.permission.READ_HEALTH_DATA

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above example projects and configuration templates, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## func getSensorList()

```cangjie
public func getSensorList(): Array<Sensor>
```

**Function:** Retrieves all sensor information on the device.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<[Sensor](#class-sensor)> | Returns the list of sensor attributes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Sensor Error Codes](./cj-errorcode-sensor.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14500101 | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception; 3. Sensor data channel exception. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

try {
    let sensors = getSensorList()
    for (index in 0..sensors.size) {
        AppLog.info("Succeeded in getting sensor${index}: ${sensors[index].sensorId} ")
    }
} catch (e: BusinessException) {
    AppLog.error("Failed to get sensor list. Code: ${e.code}, message: ${e.message}")
}
```

## func getSingleSensor(SensorId)

```cangjie
public func getSingleSensor(sensorType: SensorId): Sensor
```

**Function:** Retrieves information about a specified type of sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sensorType | [SensorId](#enum-sensorid) | Yes | - | The type of sensor. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Sensor](#class-sensor) | Returns the sensor information. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [Sensor Error Codes](./cj-errorcode-sensor.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 14500101 | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception; 3. Sensor data channel exception. |
  | 14500102 | The sensor is not supported by the device. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

try {
    let sensors = getSingleSensor(SensorId.ACCELEROMETER)
    AppLog.info("Succeeded in getting sensor: ${sensors.sensorName} ")
} catch (e: BusinessException) {
    AppLog.error("Failed to get sensor. Code: ${e.code}, message: ${e.message}")
}
```

## func off(SensorId, ?CallbackObject)

```cangjie
public func off(sensorType: SensorId, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sensorType | [SensorId](#enum-sensorid) | Yes | - | The type of sensor. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** The callback function for asynchronously reported sensor data. The data type varies depending on the sensor type. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

// This code can be added to the dependency definitions
class SensorCallback <: Callback1Argument<OrientationResponse> {
    init() {}
    public func invoke(arg: OrientationResponse): Unit {
        AppLog.info(
            "Succeeded in getting SensorCallback1 arg: steps: ${arg.timestamp}, alpha: ${arg.alpha},  beta: ${arg.beta},  gamma: ${arg.gamma}"
        )
    }
}

let callback1 = SensorCallback()
let callback2 = SensorCallback()
try {
    on(SensorId.ORIENTATION, callback1)
    on(SensorId.ORIENTATION, callback2)
    // Only unregister callback1
    off(SensorId
        .ORIENTATION, callback: callback1)
    // Unregister all callbacks for SensorId.ORIENTATION
    off(SensorId.ORIENTATION)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

## func on\<T>(SensorId, Callback1Argument\<T>, ?Options) where T \<: Response

```cangjie
public func on<T>(sensorType: SensorId, callback: Callback1Argument<T>, option!: ?Options = None): Unit where T <: Response
```

**Function:** Subscribes to sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sensorType | [SensorId](#enum-sensorid) | Yes | - | The type of sensor. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | Yes | - | The callback function. |
| option | ?[Options](#class-options) | No | None | Optional parameter list for setting the sensor reporting frequency. The default value is 200000000ns. |

## func once\<T>(SensorId, Callback1Argument\<T>) where T \<: Response

```cangjie
public func once<T>(sensorType: SensorId, callback: Callback1Argument<T>): Unit where T <: Response
```

**Function:** Retrieves sensor data once.

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| sensorType | [SensorId](#enum-sensorid) | Yes | - | The type of sensor. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | Yes | - | The callback function for asynchronously reported sensor data. The data type varies depending on the sensor type. |

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

**Initial Version:** 21

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Acceleration applied to the x-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Acceleration applied to the y-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Acceleration applied to the z-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

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

**Initial Version:** 21

**Parent Type:**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**Function:** Uncalibrated acceleration bias applied to the x-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var biasY

```cangjie
public var biasY: Float32
```

**Function:** Uncalibrated acceleration bias applied to the y-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var biasZ

```cangjie
public var biasZ: Float32
```

**Function:** Uncalibrated acceleration bias applied to the z-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** Uncalibrated acceleration applied to the x-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Uncalibrated acceleration applied to the y-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Uncalibrated acceleration applied to the z-axis of the device, unit: m/s².

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Sensors.Sensor

**Initial Version:** 21## class AmbientTemperatureResponse

```cangjie
public class AmbientTemperatureResponse <: Response {
    public var temperature: Float32
}
```

**Function:** Ambient temperature sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var temperature

```cangjie
public var temperature: Float32
```

**Function:** Ambient temperature (unit: Celsius).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class BarometerResponse

```cangjie
public class BarometerResponse <: Response {
    public var pressure: Float32
}
```

**Function:** Barometric pressure sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var pressure

```cangjie
public var pressure: Float32
```

**Function:** Pressure value (unit: hectopascal).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class GravityResponse

```cangjie
public class GravityResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Function:** Gravity sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Gravity acceleration applied on the device's x-axis (unit: m/s²).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Gravity acceleration applied on the device's y-axis (unit: m/s²).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Gravity acceleration applied on the device's z-axis (unit: m/s²).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class GyroscopeResponse

```cangjie
public class GyroscopeResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**Function:** Gyroscope sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**Function:** Angular velocity of rotation around the device's x-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Angular velocity of rotation around the device's y-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Angular velocity of rotation around the device's z-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Function:** Uncalibrated gyroscope sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**Function:** Uncalibrated angular velocity bias on the device's x-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var biasY

```cangjie
public var biasY: Float32
```

**Function:** Uncalibrated angular velocity bias on the device's y-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var biasZ

```cangjie
public var biasZ: Float32
```

**Function:** Uncalibrated angular velocity bias on the device's z-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** Uncalibrated angular velocity around the device's x-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Uncalibrated angular velocity around the device's y-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Uncalibrated angular velocity around the device's z-axis (unit: rad/s).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class HallResponse

```cangjie
public class HallResponse <: Response {
    public var status: Float32
}
```

**Function:** Hall effect sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var status

```cangjie
public var status: Float32
```

**Function:** Indicates Hall effect status. Detects magnetic presence around the device: 0 indicates absence, values >0 indicate presence.

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class HeartRateResponse

```cangjie
public class HeartRateResponse <: Response {
    public var heartRate: Float32
}
```

**Function:** Heart rate sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var heartRate

```cangjie
public var heartRate: Float32
```

**Function:** Heart rate value. Measures user's heart rate (unit: bpm).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class HumidityResponse

```cangjie
public class HumidityResponse <: Response {
    public var humidity: Float32
}
```

**Function:** Humidity sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var humidity

```cangjie
public var humidity: Float32
```

**Function:** Humidity value. Measures ambient relative humidity (unit: %).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class LightResponse

```cangjie
public class LightResponse <: Response {
    public var intensity: Float32
    public var colorTemperature:?Float32
    public var infraredLuminance:?Float32
}
```

**Function:** Ambient light sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var colorTemperature

```cangjie
public var colorTemperature:?Float32
```

**Function:** Color temperature (unit: Kelvin), optional parameter. Returns undefined at JS layer if unsupported, otherwise returns the actual value.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var infraredLuminance

```cangjie
public var infraredLuminance:?Float32
```

**Function:** Infrared luminance (unit: cd/m²), optional parameter. Returns undefined at JS layer if unsupported, otherwise returns the actual value.

**Type:** ?Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var intensity

```cangjie
public var intensity: Float32
```

**Function:** Light intensity (unit: lux).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Linear acceleration applied to the device's y-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Linear acceleration applied to the device's z-axis (unit: m/s²).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Ambient magnetic field strength on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Ambient magnetic field strength on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### var biasY

```cangjie
public var biasY: Float32
```

**Function:** Uncalibrated ambient magnetic field bias on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var biasZ

```cangjie
public var biasZ: Float32
```

**Function:** Uncalibrated ambient magnetic field bias on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the x-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the y-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Uncalibrated ambient magnetic field strength on the z-axis (unit: μT).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

### var interval

```cangjie
public var interval: IntervalOption
```

**Function:** Sensor reporting frequency.

**Type:** [IntervalOption](#enum-intervaloption)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var sensorInfoParam

```cangjie
public var sensorInfoParam:?SensorInfoParam
```

**Function:** Sensor information parameters.

**Type:** ?[SensorInfoParam](#class-sensorinfoparam)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### init(IntervalOption, ?SensorInfoParam)

```cangjie
public init(interval!: IntervalOption = NormalMode, sensorInfoParam!: ?SensorInfoParam = None)
```

**Function:** Constructor to create an Options instance.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| interval | [IntervalOption](#enum-intervaloption) | No | NormalMode | Sensor reporting frequency. |
| sensorInfoParam | ?[SensorInfoParam](#class-sensorinfoparam) | No | None | Sensor information parameters. |

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

**Since:** 21

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

**Since:** 21

### var beta

```cangjie
public var beta: Float32
```

**Function:** Rotation angle around the X-axis (unit: degrees).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var gamma

```cangjie
public var gamma: Float32
```

**Function:** Rotation angle around the Y-axis (unit: degrees).

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21
```## class PedometerDetectionResponse

```cangjie
public class PedometerDetectionResponse <: Response {
    public var scalar: Float32
}
```

**Function:** Pedometer detection sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**Function:** Pedometer detection. Detects user's stepping motion. A value of 1 indicates the user has performed a stepping action, while 0 indicates no movement.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class PedometerResponse

```cangjie
public class PedometerResponse <: Response {
    public var steps: Int64
}
```

**Function:** Pedometer sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var steps

```cangjie
public var steps: Int64
```

**Function:** The user's walking steps. The initial number of steps is 0. After the user subscribes to the pedometer sensor, each step taken will increment the step count by one.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class ProximityResponse

```cangjie
public class ProximityResponse <: Response {
    public var distance: Float32
}
```

**Function:** Proximity light sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var distance

```cangjie
public var distance: Float32
```

**Function:** Proximity of visible objects to the device display. 0 indicates proximity, values greater than 0 indicate distance.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class Response

```cangjie
public open class Response {
    public var timestamp: Int64
    public var accuracy: SensorAccuracy
}
```

**Function:** Timestamp of sensor data.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var accuracy

```cangjie
public var accuracy: SensorAccuracy
```

**Function:** Accuracy level value reported by sensor data.

**Type:** [SensorAccuracy](#enum-sensoraccuracy)

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var timestamp

```cangjie
public var timestamp: Int64
```

**Function:** Timestamp of sensor data reporting.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

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

**Since:** 21

### var x

```cangjie
public var x: Float32
```

**Function:** X-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var y

```cangjie
public var y: Float32
```

**Function:** Y-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var z

```cangjie
public var z: Float32
```

**Function:** Z-axis component of rotation vector.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Function:** Indicates sensor information.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var firmwareVersion

```cangjie
public var firmwareVersion: String
```

**Function:** Sensor firmware version.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var hardwareVersion

```cangjie
public var hardwareVersion: String
```

**Function:** Sensor hardware version.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var maxRange

```cangjie
public var maxRange: Float32
```

**Function:** Maximum measurement range of the sensor.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var maxSamplePeriod

```cangjie
public var maxSamplePeriod: Int64
```

**Function:** Maximum allowed sampling period.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var minSamplePeriod

```cangjie
public var minSamplePeriod: Int64
```

**Function:** Minimum allowed sampling period.

**Type:** Int64

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var power

```cangjie
public var power: Float32
```

**Function:** Estimated sensor power consumption in mA.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var precision

```cangjie
public var precision: Float32
```

**Function:** Sensor precision.

**Type:** Float32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var sensorId

```cangjie
public var sensorId: Int32
```

**Function:** Sensor type ID.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var sensorName

```cangjie
public var sensorName: String
```

**Function:** Sensor name.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var vendorName

```cangjie
public var vendorName: String
```

**Function:** Sensor vendor.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21## class SensorInfoParam

```cangjie
public class SensorInfoParam {
    public var deviceId: Int32
    public var sensorIndex: Int32
    public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
}
```

**Function:** Sensor information parameters.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var deviceId

```cangjie
public var deviceId: Int32
```

**Function:** Device ID.

**Type:** Int32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### var sensorIndex

```cangjie
public var sensorIndex: Int32
```

**Function:** Sensor index.

**Type:** Int32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### init(Int32, Int32)

```cangjie
public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
```

**Function:** Constructor to create a SensorInfoParam instance.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceId | Int32 | No | -1 | Device ID. |
| sensorIndex | Int32 | No | 0 | Sensor index. |

## class SignificantMotionResponse

```cangjie
public class SignificantMotionResponse <: Response {
    public var scalar: Float32
}
```

**Function:** Significant motion sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**Function:** Indicates the degree of significant motion. Measures whether there is significant motion on the three physical axes (x, y, and z); if significant motion is detected, the reported value is 1.

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

## class WearDetectionResponse

```cangjie
public class WearDetectionResponse <: Response {
    public var value: Float32
}
```

**Function:** Wear detection sensor data, inherits from [Response](#class-response).

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Parent Type:**

- [Response](#class-response)

### var value

```cangjie
public var value: Float32
```

**Function:** Indicates whether the device is worn (1 means worn, 0 means not worn).

**Type:** Float32

**Read/Write Permission:** Read-write

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

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

**Since:** 21

**Parent Types:**

- [Equatable\<IntervalOption>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString

### GameMode

```cangjie
GameMode
```

**Function:** Specifies the sensor reporting frequency as 20000000ns. This frequency takes effect when set within the hardware-supported frequency range.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### NormalMode

```cangjie
NormalMode
```

**Function:** Specifies the sensor reporting frequency as 200000000ns. This frequency takes effect when set within the hardware-supported frequency range, with a fixed value of the string 'normal'.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### SensorNumber(Int64)

```cangjie
SensorNumber(Int64)
```

**Function:** Custom sensor reporting frequency, specified in nanoseconds.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### UIMode

```cangjie
UIMode
```

**Function:** Specifies the sensor reporting frequency as 60000000ns. This frequency takes effect when set within the hardware-supported frequency range.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### func !=(IntervalOption)

```cangjie
public operator func !=(other: IntervalOption): Bool
```

**Function:** Determines whether two [IntervalOption](#enum-intervaloption) instances are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [IntervalOption](#enum-intervaloption) | Yes | - | The input [IntervalOption](#enum-intervaloption). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal; otherwise, returns false. |

### func ==(IntervalOption)

```cangjie
public operator func ==(other: IntervalOption): Bool
```

**Function:** Determines whether two [IntervalOption](#enum-intervaloption) instances are equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [IntervalOption](#enum-intervaloption) | Yes | - | The input [IntervalOption](#enum-intervaloption). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enum value to a string.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The converted string. |

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

**Since:** 21

**Parent Types:**

- [Equatable\<SensorAccuracy>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString

### AccuracyHigh

```cangjie
AccuracyHigh
```

**Function:** High accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AccuracyLow

```cangjie
AccuracyLow
```

**Function:** Low accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AccuracyMedium

```cangjie
AccuracyMedium
```

**Function:** Medium accuracy level for sensors.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AccuracyUnreliable

```cangjie
AccuracyUnreliable
```

**Function:** Sensor data is unreliable.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### func !=(SensorAccuracy)

```cangjie
public operator func !=(other: SensorAccuracy): Bool
```

**Function:** Determines whether two [SensorAccuracy](#enum-sensoraccuracy) instances are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [SensorAccuracy](#enum-sensoraccuracy) | Yes | - | The input [SensorAccuracy](#enum-sensoraccuracy). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal; otherwise, returns false. |

### func ==(SensorAccuracy)

```cangjie
public operator func ==(other: SensorAccuracy): Bool
```

**Function:** Determines whether two [SensorAccuracy](#enum-sensoraccuracy) instances are equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [SensorAccuracy](#enum-sensoraccuracy) | Yes | - | The input [SensorAccuracy](#enum-sensoraccuracy). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal; otherwise, returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enum value to a string.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The converted string. |

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

**Since:** 21

**Parent Types:**

- [Equatable\<SensorId>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString### Accelerometer

```cangjie
Accelerometer
```

**Function:** Acceleration sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AccelerometerUncalibrated

```cangjie
AccelerometerUncalibrated
```

**Function:** Uncalibrated accelerometer sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AmbientLight

```cangjie
AmbientLight
```

**Function:** Ambient light sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### AmbientTemperature

```cangjie
AmbientTemperature
```

**Function:** Ambient temperature sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Barometer

```cangjie
Barometer
```

**Function:** Barometric pressure sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Gravity

```cangjie
Gravity
```

**Function:** Gravity sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Gyroscope

```cangjie
Gyroscope
```

**Function:** Gyroscope sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### GyroscopeUncalibrated

```cangjie
GyroscopeUncalibrated
```

**Function:** Uncalibrated gyroscope sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Hall

```cangjie
Hall
```

**Function:** Hall effect sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### HeartRate

```cangjie
HeartRate
```

**Function:** Heart rate sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Humidity

```cangjie
Humidity
```

**Function:** Humidity sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### LinearAccelerometer

```cangjie
LinearAccelerometer
```

**Function:** Linear acceleration sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### MagneticField

```cangjie
MagneticField
```

**Function:** Magnetic field sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### MagneticFieldUncalibrated

```cangjie
MagneticFieldUncalibrated
```

**Function:** Uncalibrated magnetic field sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Orientation

```cangjie
Orientation
```

**Function:** Orientation sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Pedometer

```cangjie
Pedometer
```

**Function:** Pedometer sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### PedometerDetection

```cangjie
PedometerDetection
```

**Function:** Pedometer detection sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### Proximity

```cangjie
Proximity
```

**Function:** Proximity light sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### RotationVector

```cangjie
RotationVector
```

**Function:** Rotation vector sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### SignificantMotion

```cangjie
SignificantMotion
```

**Function:** Significant motion sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### WearDetection

```cangjie
WearDetection
```

**Function:** Wear detection sensor.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

### func !=(SensorId)

```cangjie
public operator func !=(other: SensorId): Bool
```

**Function:** Determines whether two [SensorId](#enum-sensorid) values are not equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SensorId](#enum-sensorid) | Yes | - | The input [SensorId](#enum-sensorid). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if not equal; otherwise, returns false. |

### func ==(SensorId)

```cangjie
public operator func ==(other: SensorId): Bool
```

**Function:** Determines whether two [SensorId](#enum-sensorid) values are equal.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [SensorId](#enum-sensorid) | Yes | - | The input [SensorId](#enum-sensorid). |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if equal; otherwise, returns false. |

### func getValue()

```cangjie
public func getValue(): Int32
```

**Function:** Gets the enumeration value.

**System Capability:** SystemCapability.Sensors.Sensor

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | The enumeration value. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the enumeration value to a string.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The converted string. |