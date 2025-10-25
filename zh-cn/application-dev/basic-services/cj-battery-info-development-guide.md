# 电池信息开发指导

## 简介

电池信息模块提供查询设备电池状态和充放电状态的接口。通过该模块，开发者可以获取电池的电量、温度、充电状态、健康状态等信息，用于应用的电源管理或用户界面展示。

## 场景介绍

主要场景有：

- 获取当前电池电量百分比和电量等级
- 监控电池充电状态和充电器类型
- 获取电池健康状态和温度信息
- 根据电池状态调整应用行为

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[电池信息接口](../../../zh-cn/application-dev/reference/BasicServicesKit/cj-apis-battery_info.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| BatteryInfo.batterySOC | 获取当前设备剩余电池电量百分比 |
| BatteryInfo.batteryCapacityLevel | 获取当前设备电池电量等级 |
| BatteryInfo.chargingStatus | 获取当前设备电池的充电状态 |
| BatteryInfo.pluggedType | 获取当前设备连接的充电器类型 |
| BatteryInfo.healthStatus | 获取当前设备电池的健康状态 |
| BatteryInfo.batteryTemperature | 获取当前设备电池的温度 |
| BatteryInfo.voltage | 获取当前设备电池的电压 |
| BatteryInfo.nowCurrent | 获取当前设备电池的电流 |
| BatteryInfo.technology | 获取当前设备电池的技术型号 |
| BatteryInfo.isBatteryPresent | 获取设备是否支持电池或电池是否在位 |

## 开发示例

以下示例演示了如何使用电池信息模块获取设备电池状态。

### 获取基本电池信息

以下示例代码演示了如何获取电池的基本信息。

<!-- compile -->

```cangjie
// index.cj
import kit.BasicServicesKit.*
import ohos.base.*

func getBasicBatteryInfo(): Unit {
    // 获取电池电量百分比
    let batteryLevel = BatteryInfo.batterySOC
    AppLog.info("Battery level: ${batteryLevel}%")
    
    // 获取电池电量等级
    let capacityLevel = BatteryInfo.batteryCapacityLevel
    AppLog.info("Battery capacity level: ${capacityLevel.toString()}")
    
    // 检查电池是否在位
    let isPresent = BatteryInfo.isBatteryPresent
    AppLog.info("Is battery present: ${isPresent}")
    
    // 获取电池技术型号
    let technology = BatteryInfo.technology
    AppLog.info("Battery technology: ${technology}")
}
```

### 获取电池充电状态信息

以下示例代码演示了如何获取电池的充电状态信息。

<!-- compile -->

```cangjie
// index.cj
import kit.BasicServicesKit.*
import ohos.base.*

func getBatteryChargingInfo(): Unit {
    // 获取充电状态
    let chargingStatus = BatteryInfo.chargingStatus
    let chargingStatusStr = match (chargingStatus) {
        case BatteryChargeState.Enabled => "Charging"
        case BatteryChargeState.Disabled => "Not charging"
        case BatteryChargeState.Full => "Fully charged"
        case _ => "Unknown"
    }
    AppLog.info("Charging status: ${chargingStatusStr}")
    
    // 获取充电器类型
    let pluggedType = BatteryInfo.pluggedType
    let pluggedTypeStr = match (pluggedType) {
        case BatteryPluggedType.Ac => "AC charger"
        case BatteryPluggedType.Usb => "USB"
        case BatteryPluggedType.Wireless => "Wireless"
        case _ => "Unknown"
    }
    AppLog.info("Plugged type: ${pluggedTypeStr}")
}
```

### 获取电池健康和电气信息

以下示例代码演示了如何获取电池的健康状态和电气参数。

<!-- compile -->

```cangjie
// index.cj
import kit.BasicServicesKit.*
import ohos.base.*

func getBatteryHealthAndElectricalInfo(): Unit {
    // 获取电池健康状态
    let healthStatus = BatteryInfo.healthStatus
    let healthStatusStr = match (healthStatus) {
        case BatteryHealthState.Good => "Good"
        case BatteryHealthState.Overheat => "Overheat"
        case BatteryHealthState.Overvoltage => "Overvoltage"
        case BatteryHealthState.Cold => "Cold"
        case BatteryHealthState.Dead => "Dead"
        case _ => "Unknown"
    }
    AppLog.info("Battery health status: ${healthStatusStr}")
    
    // 获取电池温度 (单位: 0.1°C)
    let temperature = BatteryInfo.batteryTemperature
    let temperatureCelsius = Float32(temperature) / 10.0
    AppLog.info("Battery temperature: ${temperatureCelsius}°C (${temperature} tenths of a degree)")
    
    // 获取电池电压 (单位: mV)
    let voltage = BatteryInfo.voltage
    AppLog.info("Battery voltage: ${voltage} mV")
    
    // 获取电池电流 (单位: mA)
    let current = BatteryInfo.nowCurrent
    AppLog.info("Battery current: ${current} mA")
}
```
