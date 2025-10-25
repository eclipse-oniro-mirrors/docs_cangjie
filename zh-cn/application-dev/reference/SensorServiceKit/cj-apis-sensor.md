# ohos.sensor（传感器）

sensor模块提供了获取传感器数据的能力，包括获取传感器属性列表，订阅传感器数据，以及一些通用的传感器算法。

## 导入模块

```cangjie
import kit.SensorServiceKit.*
```

## 权限列表

ohos.permission.ACCELEROMETER

ohos.permission.GYROSCOPE

ohos.permission.READ_HEALTH_DATA

## 使用说明

API示例代码使用说明：

- 若示例代码首行有“// index.cj”注释，表示该示例可在仓颉模板工程的“index.cj”文件中编译运行。
- 若示例需获取[Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context)应用上下文，需在仓颉模板工程中的“main_ability.cj”文件中进行配置。

上述示例工程及配置模板详见[仓颉示例代码说明](../cj-development-intro.md#仓颉示例代码说明)。

## func getSensorList()

```cangjie
public func getSensorList(): Array<Sensor>
```

**功能：** 获取设备上的所有传感器信息。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**返回值：**

| 类型                              | 说明         |
|:------------------------------- |:---------- |
| Array\<[Sensor](#class-sensor)> | 返回传感器属性列表。 |

**异常：**

- BusinessException：对应错误码如下表，详见[传感器错误码](./cj-errorcode-sensor.md)和[通用错误码](../cj-errorcode-universal.md)。
  
  | 错误码ID    | 错误信息                                                                                                                                   |
  |:-------- |:-------------------------------------------------------------------------------------------------------------------------------------- |
  | 14500101 | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception;3. Sensor data channel exception. |

**示例：**

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

**功能：** 获取指定类型的传感器信息。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名        | 类型                         | 必填  | 默认值 | 说明     |
|:---------- |:-------------------------- |:--- |:--- |:------ |
| sensorType | [SensorId](#enum-sensorid) | 是   | -   | 传感器类型。 |

**返回值：**

| 类型                      | 说明       |
|:----------------------- |:-------- |
| [Sensor](#class-sensor) | 返回传感器信息。 |

**异常：**

- BusinessException：对应错误码如下表，详见[传感器错误码](./cj-errorcode-sensor.md)和[通用错误码](../cj-errorcode-universal.md)。
  
  | 错误码ID    | 错误信息                                                                                                                                   |
  |:-------- |:-------------------------------------------------------------------------------------------------------------------------------------- |
  | 14500101 | Service exception. Possible causes: 1. Sensor hdf service exception; 2. Sensor service ipc exception;3. Sensor data channel exception. |
  | 14500102 | The sensor is not supported by the device.                                                                                             |

**示例：**

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

**功能：** 取消订阅传感器数据。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名        | 类型                                                                                 | 必填  | 默认值  | 说明                                          |
|:---------- |:---------------------------------------------------------------------------------- |:--- |:---- |:------------------------------------------- |
| sensorType | [SensorId](#enum-sensorid)                                                         | 是   | -    | 传感器类型。                                      |
| callback   | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | 否   | None | **命名参数。** 回调函数，异步上报的传感器数据，每种传感器类型对应的数据类型不同。 |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

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
    // 仅取消callback1的注册
    off(SensorId
        .ORIENTATION, callback: callback1)
    // 取消注册SensorId.ORIENTATION的所有回调
    off(SensorId.ORIENTATION)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

## func on\<T>(SensorId, Callback1Argument\<T>, ?Options) where T \<: Response

```cangjie
public func on<T>(sensorType: SensorId, callback: Callback1Argument<T>, option!: ?Options = None): Unit where T <: Response
```

**功能：** 订阅传感器数据。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名        | 类型                                                                                          | 必填  | 默认值  | 说明                                  |
|:---------- |:------------------------------------------------------------------------------------------- |:--- |:---- |:----------------------------------- |
| sensorType | [SensorId](#enum-sensorid)                                                                  | 是   | -    | 传感器类型。                              |
| callback   | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | 是   | -    | 回调函数。                               |
| option     | ?[Options](#class-options)                                                                  | 否   | None | 可选参数列表，用于设置传感器上报频率，默认值为200000000ns。 |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class AccelerometerCallback <: Callback1Argument<AccelerometerResponse> {
    init() {}
    public func invoke(arg: AccelerometerResponse): Unit {
        AppLog.info(
            "Succeeded in getting AccelerometerCallback arg: timestamp: ${arg.timestamp}, x: ${arg.x},  y: ${arg.y},  z: ${arg.z}"
        )
    }
}

let callback = AccelerometerCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    on(SensorId.ACCELEROMETER, callback, option: options)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

## func once\<T>(SensorId, Callback1Argument\<T>) where T \<: Response

```cangjie
public func once<T>(sensorType: SensorId, callback: Callback1Argument<T>): Unit where T <: Response
```

**功能：** 获取一次传感器数据。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名        | 类型                                                                                          | 必填  | 默认值 | 说明                                |
|:---------- |:------------------------------------------------------------------------------------------- |:--- |:--- |:--------------------------------- |
| sensorType | [SensorId](#enum-sensorid)                                                                  | 是   | -   | 传感器类型。                            |
| callback   | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<T> | 是   | -   | 回调函数，异步上报的传感器数据，每种传感器类型对应的数据类型不同。 |

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class GyroscopeCallback <: Callback1Argument<GyroscopeResponse> {
    init() {}
    public func invoke(arg: GyroscopeResponse): Unit {
        AppLog.info(
            "Succeeded in getting GyroscopeCallback arg: timestamp: ${arg.timestamp}, x: ${arg.x},  y: ${arg.y},  z: ${arg.z}"
        )
    }
}

let callback = GyroscopeCallback()
try {
    once(SensorId.GYROSCOPE, callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
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

**功能：** 加速度传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**功能：** 施加在设备x轴的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 施加在设备y轴的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 施加在设备z轴的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

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

**功能：** 未校准加速度计传感器数据。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**功能：** 施加在设备x轴未校准的加速度偏量，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasY

```cangjie
public var biasY: Float32
```

**功能：** 施加在设备y轴未校准的加速度偏量，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**功能：** 施加在设备z轴未校准的加速度偏量，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var x

```cangjie
public var x: Float32
```

**功能：** 施加在设备x轴未校准的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 施加在设备y轴未校准的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 施加在设备z轴未校准的加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class AmbientTemperatureResponse

```cangjie
public class AmbientTemperatureResponse <: Response {
    public var temperature: Float32
}
```

**功能：** 温度传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var temperature

```cangjie
public var temperature: Float32
```

**功能：** 环境温度（单位：摄氏度）。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class BarometerResponse

```cangjie
public class BarometerResponse <: Response {
    public var pressure: Float32
}
```

**功能：** 气压计传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var pressure

```cangjie
public var pressure: Float32
```

**功能：** 压力值（单位：百帕）。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class GravityResponse

```cangjie
public class GravityResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**功能：** 重力传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**功能：** 施加在设备x轴的重力加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 施加在设备y轴的重力加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 施加在设备z轴的重力加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class GyroscopeResponse

```cangjie
public class GyroscopeResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**功能：** 陀螺仪传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**功能：** 设备x轴的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 设备y轴的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 设备z轴的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

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

**功能：** 未校准陀螺仪传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**功能：** 设备x轴未校准的旋转角速度偏量，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasY

```cangjie
public var biasY: Float32
```

**功能：** 设备y轴未校准的旋转角速度偏量，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**功能：** 设备z轴未校准的旋转角速度偏量，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var x

```cangjie
public var x: Float32
```

**功能：** 设备x轴未校准的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 设备y轴未校准的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 设备z轴未校准的旋转角速度，单位rad/s。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class HallResponse

```cangjie
public class HallResponse <: Response {
    public var status: Float32
}
```

**功能：** 霍尔传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var status

```cangjie
public var status: Float32
```

**功能：** 显示霍尔状态。测量设备周围是否存在磁力吸引，0表示没有，大于0表示有。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class HeartRateResponse

```cangjie
public class HeartRateResponse <: Response {
    public var heartRate: Float32
}
```

**功能：** 心率传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var heartRate

```cangjie
public var heartRate: Float32
```

**功能：** 心率值。测量用户的心率数值，单位：bpm。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class HumidityResponse

```cangjie
public class HumidityResponse <: Response {
    public var humidity: Float32
}
```

**功能：** 湿度传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var humidity

```cangjie
public var humidity: Float32
```

**功能：** 湿度值。测量环境的相对湿度，以百分比&nbsp;(%)&nbsp;表示。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class LightResponse

```cangjie
public class LightResponse <: Response {
    public var intensity: Float32
    public var colorTemperature:?Float32
    public var infraredLuminance:?Float32
}
```

**功能：** 环境光传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var colorTemperature

```cangjie
public var colorTemperature:?Float32
```

**功能：** 色温（单位：开尔文），可选参数，如果该参数不支持在js层返回未定义，支持则返回正常数值。

**类型：** ?Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var infraredLuminance

```cangjie
public var infraredLuminance:?Float32
```

**功能：** 红外亮度（单位：cd/m²），可选参数，如果该参数不支持在js层返回未定义，支持则返回正常数值。

**类型：** ?Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var intensity

```cangjie
public var intensity: Float32
```

**功能：** 光强（单位：勒克斯）。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class LinearAccelerometerResponse

```cangjie
public class LinearAccelerometerResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**功能：** 线性加速度传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**功能：** 施加在设备x轴的线性加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 施加在设备y轴的线性加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 施加在设备z轴的线性加速度，单位：m/s²。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class MagneticFieldResponse

```cangjie
public class MagneticFieldResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
}
```

**功能：** 磁场传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var x

```cangjie
public var x: Float32
```

**功能：** x轴环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** y轴环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** z轴环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

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

**功能：** 未校准磁场传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var biasX

```cangjie
public var biasX: Float32
```

**功能：** x轴未校准环境磁场强度偏量，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasY

```cangjie
public var biasY: Float32
```

**功能：** y轴未校准环境磁场强度偏量，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var biasZ

```cangjie
public var biasZ: Float32
```

**功能：** z轴未校准环境磁场强度偏量，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var x

```cangjie
public var x: Float32
```

**功能：** x轴未校准环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** y轴未校准环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** z轴未校准环境磁场强度，单位：μT。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class Options

```cangjie
public class Options {
    public var interval: IntervalOption
    public var sensorInfoParam:?SensorInfoParam
    public init(interval!: IntervalOption = NormalMode, sensorInfoParam!: ?SensorInfoParam = None)
}
```

**功能：** 传感器配置选项。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var interval

```cangjie
public var interval: IntervalOption
```

**功能：** 传感器上报频率。

**类型：** [IntervalOption](#enum-intervaloption)

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var sensorInfoParam

```cangjie
public var sensorInfoParam:?SensorInfoParam
```

**功能：** 传感器信息参数。

**类型：** ?[SensorInfoParam](#class-sensorinfoparam)

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### init(IntervalOption, ?SensorInfoParam)

```cangjie
public init(interval!: IntervalOption = NormalMode, sensorInfoParam!: ?SensorInfoParam = None)
```

**功能：** 构造函数，创建Options实例。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名             | 类型                                         | 必填  | 默认值        | 说明       |
|:--------------- |:------------------------------------------ |:--- |:---------- |:-------- |
| interval        | [IntervalOption](#enum-intervaloption)     | 否   | NormalMode | 传感器上报频率。 |
| sensorInfoParam | ?[SensorInfoParam](#class-sensorinfoparam) | 否   | None       | 传感器信息参数。 |

## class OrientationResponse

```cangjie
public class OrientationResponse <: Response {
    public var alpha: Float32
    public var beta: Float32
    public var gamma: Float32
}
```

**功能：** 方向传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var alpha

```cangjie
public var alpha: Float32
```

**功能：** 设备围绕Z轴的旋转角度，单位：度。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var beta

```cangjie
public var beta: Float32
```

**功能：** 设备围绕X轴的旋转角度，单位：度。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var gamma

```cangjie
public var gamma: Float32
```

**功能：** 设备围绕Y轴的旋转角度，单位：度。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class PedometerDetectionResponse

```cangjie
public class PedometerDetectionResponse <: Response {
    public var scalar: Float32
}
```

**功能：** 计步检测传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**功能：** 计步器检测。检测用户的计步动作，如果取值为1则代表用户产生了计步行走的动作，取值为0则代表用户没有发生运动。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class PedometerResponse

```cangjie
public class PedometerResponse <: Response {
    public var steps: Int64
}
```

**功能：** 计步传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var steps

```cangjie
public var steps: Int64
```

**功能：** 用户的行走步数。步数初始值是0。用户订阅计步传感器后，每行走一步，步数累计加一。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class ProximityResponse

```cangjie
public class ProximityResponse <: Response {
    public var distance: Float32
}
```

**功能：** 接近光传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var distance

```cangjie
public var distance: Float32
```

**功能：** 可见物体与设备显示器的接近程度。0表示接近，大于0表示远离。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class Response

```cangjie
public open class Response {
    public var timestamp: Int64
    public var accuracy: SensorAccuracy
}
```

**功能：** 传感器数据的时间戳。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var accuracy

```cangjie
public var accuracy: SensorAccuracy
```

**功能：** 传感器数据上报的精度档位值。

**类型：** [SensorAccuracy](#enum-sensoraccuracy)

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var timestamp

```cangjie
public var timestamp: Int64
```

**功能：** 传感器数据上报的时间戳。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class RotationVectorResponse

```cangjie
public class RotationVectorResponse <: Response {
    public var x: Float32
    public var y: Float32
    public var z: Float32
    public var w: Float32
}
```

**功能：** 旋转矢量传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var w

```cangjie
public var w: Float32
```

**功能：** 标量。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var x

```cangjie
public var x: Float32
```

**功能：** 旋转矢量x轴分量。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var y

```cangjie
public var y: Float32
```

**功能：** 旋转矢量y轴分量。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var z

```cangjie
public var z: Float32
```

**功能：** 旋转矢量z轴分量。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

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

**功能：** 指示传感器信息。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var firmwareVersion

```cangjie
public var firmwareVersion: String
```

**功能：** 传感器固件版本。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var hardwareVersion

```cangjie
public var hardwareVersion: String
```

**功能：** 传感器硬件版本。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var maxRange

```cangjie
public var maxRange: Float32
```

**功能：** 传感器测量范围的最大值。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var maxSamplePeriod

```cangjie
public var maxSamplePeriod: Int64
```

**功能：** 允许的最大采样周期。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var minSamplePeriod

```cangjie
public var minSamplePeriod: Int64
```

**功能：** 允许的最小采样周期。

**类型：** Int64

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var power

```cangjie
public var power: Float32
```

**功能：** 传感器功率的估计值，单位：mA。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var precision

```cangjie
public var precision: Float32
```

**功能：** 传感器精度。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var sensorId

```cangjie
public var sensorId: Int32
```

**功能：** 传感器类型id。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var sensorName

```cangjie
public var sensorName: String
```

**功能：** 传感器名称。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var vendorName

```cangjie
public var vendorName: String
```

**功能：** 传感器供应商。

**类型：** String

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class SensorInfoParam

```cangjie
public class SensorInfoParam {
    public var deviceId: Int32
    public var sensorIndex: Int32
    public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
}
```

**功能：** 传感器信息参数。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var deviceId

```cangjie
public var deviceId: Int32
```

**功能：** 设备ID。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### var sensorIndex

```cangjie
public var sensorIndex: Int32
```

**功能：** 传感器索引。

**类型：** Int32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### init(Int32, Int32)

```cangjie
public init(deviceId!: Int32 = -1, sensorIndex!: Int32 = 0)
```

**功能：** 构造函数，创建SensorInfoParam实例。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**参数：**

| 参数名         | 类型    | 必填  | 默认值 | 说明     |
|:----------- |:----- |:--- |:--- |:------ |
| deviceId    | Int32 | 否   | - 1 | 设备ID。  |
| sensorIndex | Int32 | 否   | 0   | 传感器索引。 |

## class SignificantMotionResponse

```cangjie
public class SignificantMotionResponse <: Response {
    public var scalar: Float32
}
```

**功能：** 有效运动传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var scalar

```cangjie
public var scalar: Float32
```

**功能：** 表示剧烈运动程度。测量三个物理轴（x、y&nbsp;和&nbsp;z）上，设备是否存在大幅度运动；若存在大幅度运动则数据上报为1。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

## class WearDetectionResponse

```cangjie
public class WearDetectionResponse <: Response {
    public var value: Float32
}
```

**功能：** 佩戴检测传感器数据，继承自[Response](#class-response)。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Response](#class-response)

### var value

```cangjie
public var value: Float32
```

**功能：** 表示设备是否被穿戴（1表示已穿戴，0表示未穿戴）。

**类型：** Float32

**读写能力：** 可读写

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

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

**功能：** 传感器上报频率的选项。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Equatable\<IntervalOption>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString

### GameMode

```cangjie
GameMode
```

**功能：** 用于指定传感器上报频率，频率值为20000000ns，该频率被设置在硬件支持的频率范围内时会生效。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### NormalMode

```cangjie
NormalMode
```

**功能：** 用于指定传感器上报频率，频率值为200000000ns，该频率被设置在硬件支持的频率范围内时会生效，值固定为'normal'字符串。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### SensorNumber(Int64)

```cangjie
SensorNumber(Int64)
```

**功能：** 自定义传感器上报频率，频率值为指定的纳秒数。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### UIMode

```cangjie
UIMode
```

**功能：** 用于指定传感器上报频率，频率值为60000000ns，该频率被设置在硬件支持的频率范围内时会生效。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### func !=(IntervalOption)

```cangjie
public operator func !=(other: IntervalOption): Bool
```

**功能：** 判断两个[IntervalOption](#enum-intervaloption) 是否不相等。

**参数：**

| 参数名   | 类型                                     | 必填  | 默认值 | 说明                                         |
|:----- |:-------------------------------------- |:--- |:--- |:------------------------------------------ |
| other | [IntervalOption](#enum-intervaloption) | 是   | -   | 传入的[IntervalOption](#enum-intervaloption)。 |

**返回值：**

| 类型   | 说明                        |
|:---- |:------------------------- |
| Bool | 如果不相等，则返回true；否则，返回false。 |

### func ==(IntervalOption)

```cangjie
public operator func ==(other: IntervalOption): Bool
```

**功能：** 判断两个[IntervalOption](#enum-intervaloption) 是否相等。

**参数：**

| 参数名   | 类型                                     | 必填  | 默认值 | 说明                                         |
|:----- |:-------------------------------------- |:--- |:--- |:------------------------------------------ |
| other | [IntervalOption](#enum-intervaloption) | 是   | -   | 传入的[IntervalOption](#enum-intervaloption)。 |

**返回值：**

| 类型   | 说明                       |
|:---- |:------------------------ |
| Bool | 如果相等，则返回true；否则，返回false。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将枚举值转换为字符串。

**返回值：**

| 类型     | 说明       |
|:------ |:-------- |
| String | 转换后的字符串。 |

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

**功能：** 传感器数据的精度。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Equatable\<SensorAccuracy>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString

### AccuracyHigh

```cangjie
AccuracyHigh
```

**功能：** 传感器高档位精度。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### AccuracyLow

```cangjie
AccuracyLow
```

**功能：** 传感器低档位精度。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### AccuracyMedium

```cangjie
AccuracyMedium
```

**功能：** 传感器中档位精度。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### AccuracyUnreliable

```cangjie
AccuracyUnreliable
```

**功能：** 传感器数据不可信。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

### func !=(SensorAccuracy)

```cangjie
public operator func !=(other: SensorAccuracy): Bool
```

**功能：** 判断两个[SensorAccuracy](#enum-sensoraccuracy) 是否不相等。

**参数：**

| 参数名   | 类型                                     | 必填  | 默认值 | 说明                                         |
|:----- |:-------------------------------------- |:--- |:--- |:------------------------------------------ |
| other | [SensorAccuracy](#enum-sensoraccuracy) | 是   | -   | 传入的[SensorAccuracy](#enum-sensoraccuracy)。 |

**返回值：**

| 类型   | 说明                        |
|:---- |:------------------------- |
| Bool | 如果不相等，则返回true；否则，返回false。 |

### func ==(SensorAccuracy)

```cangjie
public operator func ==(other: SensorAccuracy): Bool
```

**功能：** 判断两个[SensorAccuracy](#enum-sensoraccuracy) 是否相等。

**参数：**

| 参数名   | 类型                                     | 必填  | 默认值 | 说明                                         |
|:----- |:-------------------------------------- |:--- |:--- |:------------------------------------------ |
| other | [SensorAccuracy](#enum-sensoraccuracy) | 是   | -   | 传入的[SensorAccuracy](#enum-sensoraccuracy)。 |

**返回值：**

| 类型   | 说明                       |
|:---- |:------------------------ |
| Bool | 如果相等，则返回true；否则，返回false。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将枚举值转换为字符串。

**返回值：**

| 类型     | 说明       |
|:------ |:-------- |
| String | 转换后的字符串。 |

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

**功能：** 表示当前支持订阅或取消订阅的传感器类型。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**父类型：**

- [Equatable\<SensorId>](../BasicServicesKit/cj-apis-base.md#class-equatable)
- ToString

### Accelerometer

```cangjie
Accelerometer
```

**功能：** 加速度传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class AccelerometerCallback <: Callback1Argument<AccelerometerResponse> {
    init() {}
    public func invoke(arg: AccelerometerResponse): Unit {
        AppLog.info(
            "Accelerometer data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}"
        )
    }
}

let callback = AccelerometerCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.ACCELEROMETER, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.ACCELEROMETER, callback)

    // 取消订阅传感器数据
    off(SensorId.ACCELEROMETER, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### AccelerometerUncalibrated

```cangjie
AccelerometerUncalibrated
```

**功能：** 未校准加速度计传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class AccelerometerUncalibratedCallback <: Callback1Argument<AccelerometerUncalibratedResponse> {
    init() {}
    public func invoke(arg: AccelerometerUncalibratedResponse): Unit {
        AppLog.info(
            "AccelerometerUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}"
        )
    }
}

let callback = AccelerometerUncalibratedCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.ACCELEROMETERUNCALIBRATED, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.ACCELEROMETERUNCALIBRATED, callback)

    // 取消订阅传感器数据
    off(SensorId.ACCELEROMETERUNCALIBRATED, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### AmbientLight

```cangjie
AmbientLight
```

**功能：** 环境光传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class LightCallback <: Callback1Argument<LightResponse> {
    init() {}
    public func invoke(arg: LightResponse): Unit {
        AppLog.info(
            "Light data: timestamp: ${arg.timestamp}, intensity: ${arg.intensity}"
        )
    }
}

let callback = LightCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.AMBIENTLIGHT, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.AMBIENTLIGHT, callback)

    // 取消订阅传感器数据
    off(SensorId.AMBIENTLIGHT, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### AmbientTemperature

```cangjie
AmbientTemperature
```

**功能：** 环境温度传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class AmbientTemperatureCallback <: Callback1Argument<AmbientTemperatureResponse> {
    init() {}
    public func invoke(arg: AmbientTemperatureResponse): Unit {
        AppLog.info(
            "AmbientTemperature data: timestamp: ${arg.timestamp}, temperature: ${arg.temperature}"
        )
    }
}

let callback = AmbientTemperatureCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.AMBIENTTEMPERATURE, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.AMBIENTTEMPERATURE, callback)

    // 取消订阅传感器数据
    off(SensorId.AMBIENTTEMPERATURE, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Barometer

```cangjie
Barometer  
```

**功能：** 气压计传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class BarometerCallback <: Callback1Argument<BarometerResponse> {
    init() {}
    public func invoke(arg: BarometerResponse): Unit {
        AppLog.info(
            "Barometer data: timestamp: ${arg.timestamp}, pressure: ${arg.pressure}"
        )
    }
}

let callback = BarometerCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.BAROMETER, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.BAROMETER, callback)

    // 取消订阅传感器数据
    off(SensorId.BAROMETER, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Gravity

```cangjie
Gravity
```

**功能：** 重力传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class GravityCallback <: Callback1Argument<GravityResponse> {
    init() {}
    public func invoke(arg: GravityResponse): Unit {
        AppLog.info(
            "Gravity data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}"
        )
    }
}

let callback = GravityCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.GRAVITY, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.GRAVITY, callback)

    // 取消订阅传感器数据
    off(SensorId.GRAVITY, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Gyroscope

```cangjie
Gyroscope
```

**功能：** 陀螺仪传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class GyroscopeCallback <: Callback1Argument<GyroscopeResponse> {
    init() {}
    public func invoke(arg: GyroscopeResponse): Unit {
        AppLog.info(
            "Gyroscope data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}"
        )
    }
}

let callback = GyroscopeCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.GYROSCOPE, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.GYROSCOPE, callback)

    // 取消订阅传感器数据
    off(SensorId.GYROSCOPE, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### GyroscopeUncalibrated

```cangjie
GyroscopeUncalibrated
```

**功能：** 未校准陀螺仪传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class GyroscopeUncalibratedCallback <: Callback1Argument<GyroscopeUncalibratedResponse> {
    init() {}
    public func invoke(arg: GyroscopeUncalibratedResponse): Unit {
        AppLog.info(
            "GyroscopeUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}"
        )
    }
}

let callback = GyroscopeUncalibratedCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.GYROSCOPEUNCALIBRATED, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.GYROSCOPEUNCALIBRATED, callback)

    // 取消订阅传感器数据
    off(SensorId.GYROSCOPEUNCALIBRATED, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Hall

```cangjie
Hall
```

**功能：** 霍尔传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class HallCallback <: Callback1Argument<HallResponse> {
    init() {}
    public func invoke(arg: HallResponse): Unit {
        AppLog.info(
            "Hall data: timestamp: ${arg.timestamp}, status: ${arg.status}"
        )
    }
}

let callback = HallCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.HALL, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.HALL, callback)

    // 取消订阅传感器数据
    off(SensorId.HALL, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### HeartRate

```cangjie
HeartRate
```

**功能：** 心率传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class HeartRateCallback <: Callback1Argument<HeartRateResponse> {
    init() {}
    public func invoke(arg: HeartRateResponse): Unit {
        AppLog.info(
            "HeartRate data: timestamp: ${arg.timestamp}, heartRate: ${arg.heartRate}"
        )
    }
}

let callback = HeartRateCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.HEARTRATE, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.HEARTRATE, callback)

    // 取消订阅传感器数据
    off(SensorId.HEARTRATE, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Humidity

```cangjie
Humidity
```

**功能：** 湿度传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class HumidityCallback <: Callback1Argument<HumidityResponse> {
    init() {}
    public func invoke(arg: HumidityResponse): Unit {
        AppLog.info(
            "Humidity data: timestamp: ${arg.timestamp}, humidity: ${arg.humidity}"
        )
    }
}

let callback = HumidityCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.HUMIDITY, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.HUMIDITY, callback)

    // 取消订阅传感器数据
    off(SensorId.HUMIDITY, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### LinearAccelerometer

```cangjie
LinearAccelerometer
```

**功能：** 线性加速度传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class LinearAccelerometerCallback <: Callback1Argument<LinearAccelerometerResponse> {
    init() {}
    public func invoke(arg: LinearAccelerometerResponse): Unit {
        AppLog.info(
            "LinearAccelerometer data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}"
        )
    }
}

let callback = LinearAccelerometerCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.LINEARACCELEROMETER, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.LINEARACCELEROMETER, callback)

    // 取消订阅传感器数据
    off(SensorId.LINEARACCELEROMETER, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### MagneticField

```cangjie
MagneticField
```

**功能：** 磁场传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class MagneticFieldCallback <: Callback1Argument<MagneticFieldResponse> {
    init() {}
    public func invoke(arg: MagneticFieldResponse): Unit {
        AppLog.info(
            "MagneticField data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}"
        )
    }
}

let callback = MagneticFieldCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.MAGNETICFIELD, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.MAGNETICFIELD, callback)

    // 取消订阅传感器数据
    off(SensorId.MAGNETICFIELD, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### MagneticFieldUncalibrated

```cangjie
MagneticFieldUncalibrated
```

**功能：** 未校准磁场传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class MagneticFieldUncalibratedCallback <: Callback1Argument<MagneticFieldUncalibratedResponse> {
    init() {}
    public func invoke(arg: MagneticFieldUncalibratedResponse): Unit {
        AppLog.info(
            "MagneticFieldUncalibrated data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, biasX: ${arg.biasX}, biasY: ${arg.biasY}, biasZ: ${arg.biasZ}"
        )
    }
}

let callback = MagneticFieldUncalibratedCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.MAGNETICFIELDUNCALIBRATED, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.MAGNETICFIELDUNCALIBRATED, callback)

    // 取消订阅传感器数据
    off(SensorId.MAGNETICFIELDUNCALIBRATED, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Orientation

```cangjie
Orientation
```

**功能：** 方向传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class OrientationCallback <: Callback1Argument<OrientationResponse> {
    init() {}
    public func invoke(arg: OrientationResponse): Unit {
        AppLog.info(
            "Orientation data: timestamp: ${arg.timestamp}, alpha: ${arg.alpha}, beta: ${arg.beta}, gamma: ${arg.gamma}"
        )
    }
}

let callback = OrientationCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.ORIENTATION, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.ORIENTATION, callback)

    // 取消订阅传感器数据
    off(SensorId.ORIENTATION, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Pedometer

```cangjie
Pedometer
```

**功能：** 计步传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class PedometerCallback <: Callback1Argument<PedometerResponse> {
    init() {}
    public func invoke(arg: PedometerResponse): Unit {
        AppLog.info(
            "Pedometer data: timestamp: ${arg.timestamp}, steps: ${arg.steps}"
        )
    }
}

let callback = PedometerCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.PEDOMETER, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.PEDOMETER, callback)

    // 取消订阅传感器数据
    off(SensorId.PEDOMETER, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### PedometerDetection

```cangjie
PedometerDetection
```

**功能：** 计步检测传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class PedometerDetectionCallback <: Callback1Argument<PedometerDetectionResponse> {
    init() {}
    public func invoke(arg: PedometerDetectionResponse): Unit {
        AppLog.info(
            "PedometerDetection data: timestamp: ${arg.timestamp}, scalar: ${arg.scalar}"
        )
    }
}

let callback = PedometerDetectionCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.PEDOMETERDETECTION, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.PEDOMETERDETECTION, callback)

    // 取消订阅传感器数据
    off(SensorId.PEDOMETERDETECTION, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### Proximity

```cangjie
Proximity
```

**功能：** 接近光传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class ProximityCallback <: Callback1Argument<ProximityResponse> {
    init() {}
    public func invoke(arg: ProximityResponse): Unit {
        AppLog.info(
            "Proximity data: timestamp: ${arg.timestamp}, distance: ${arg.distance}"
        )
    }
}

let callback = ProximityCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.PROXIMITY, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.PROXIMITY, callback)

    // 取消订阅传感器数据
    off(SensorId.PROXIMITY, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### RotationVector

```cangjie
RotationVector
```

**功能：** 旋转矢量传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class RotationVectorCallback <: Callback1Argument<RotationVectorResponse> {
    init() {}
    public func invoke(arg: RotationVectorResponse): Unit {
        AppLog.info(
            "RotationVector data: timestamp: ${arg.timestamp}, x: ${arg.x}, y: ${arg.y}, z: ${arg.z}, w: ${arg.w}"
        )
    }
}

let callback = RotationVectorCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.ROTATIONVECTOR, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.ROTATIONVECTOR, callback)

    // 取消订阅传感器数据
    off(SensorId.ROTATIONVECTOR, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### SignificantMotion

```cangjie
SignificantMotion
```

**功能：** 有效运动传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class SignificantMotionCallback <: Callback1Argument<SignificantMotionResponse> {
    init() {}
    public func invoke(arg: SignificantMotionResponse): Unit {
        AppLog.info(
            "SignificantMotion data: timestamp: ${arg.timestamp}, scalar: ${arg.scalar}"
        )
    }
}

let callback = SignificantMotionCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.SIGNIFICANTMOTION, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.SIGNIFICANTMOTION, callback)

    // 取消订阅传感器数据
    off(SensorId.SIGNIFICANTMOTION, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### WearDetection

```cangjie
WearDetection
```

**功能：** 佩戴检测传感器。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**示例：**

<!-- compile -->

```cangjie
// index.cj

import kit.SensorServiceKit.*
import ohos.base.*

class WearDetectionCallback <: Callback1Argument<WearDetectionResponse> {
    init() {}
    public func invoke(arg: WearDetectionResponse): Unit {
        AppLog.info(
            "WearDetection data: timestamp: ${arg.timestamp}, value: ${arg.value}"
        )
    }
}

let callback = WearDetectionCallback()
let options = Options(interval = IntervalOption.SensorNumber(100000000))
try {
    // 订阅传感器数据
    on(SensorId.WEARDETECTION, callback, option: options)

    // 获取一次传感器数据
    once(SensorId.WEARDETECTION, callback)

    // 取消订阅传感器数据
    off(SensorId.WEARDETECTION, callback: callback)
} catch (e: BusinessException) {
    AppLog.error(e.toString())
}
```

### func !=(SensorId)

```cangjie
public operator func !=(other: SensorId): Bool
```

**功能：** 判断两个[SensorId](#enum-sensorid) 是否不相等。

**参数：**

| 参数名   | 类型                         | 必填  | 默认值 | 说明                             |
|:----- |:-------------------------- |:--- |:--- |:------------------------------ |
| other | [SensorId](#enum-sensorid) | 是   | -   | 传入的[SensorId](#enum-sensorid)。 |

**返回值：**

| 类型   | 说明                        |
|:---- |:------------------------- |
| Bool | 如果不相等，则返回true；否则，返回false。 |

### func ==(SensorId)

```cangjie
public operator func ==(other: SensorId): Bool
```

**功能：** 判断两个[SensorId](#enum-sensorid) 是否相等。

**参数：**

| 参数名   | 类型                         | 必填  | 默认值 | 说明                             |
|:----- |:-------------------------- |:--- |:--- |:------------------------------ |
| other | [SensorId](#enum-sensorid) | 是   | -   | 传入的[SensorId](#enum-sensorid)。 |

**返回值：**

| 类型   | 说明                       |
|:---- |:------------------------ |
| Bool | 如果相等，则返回true；否则，返回false。 |

### func getValue()

```cangjie
public func getValue(): Int32
```

**功能：** 获取枚举值。

**系统能力：** SystemCapability.Sensors.Sensor

**起始版本：** 22

**返回值：**

| 类型    | 说明   |
|:----- |:---- |
| Int32 | 枚举值。 |

### func toString()

```cangjie
public func toString(): String
```

**功能：** 将枚举值转换为字符串。

**返回值：**

| 类型     | 说明       |
|:------ |:-------- |
| String | 转换后的字符串。 |
