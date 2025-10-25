# 设备信息开发指导

## 简介

设备信息模块提供终端设备信息查询的接口。通过该模块，开发者可以获取设备类型信息、设备生产厂家信息、系统软件API版本信息以及设备udid信息等。

## 场景介绍

主要场景有：

- 获取当前设备类型信息
- 获取系统版本
- 获取系统软件API版本信息

## 接口说明

完整的仓颉 API 说明以及实例代码请参见：[设备信息接口](../../../../zh-cn/application-dev/reference/BasicServicesKit/cj-apis-device_info.md)。

具体接口说明如下表。

| 接口名 | 功能描述 |
| ------------------------------------------ | ----------------------------------------------------------- |
| DeviceInfo.ODID | 获取开发者匿名设备标识符 |
| DeviceInfo.abiList | 获取应用二进制接口（ABI）列表|
| DeviceInfo.bootloaderVersion | 获取Bootloader版本号|
| DeviceInfo.brand | 获取设备品牌名称 |
| DeviceInfo.buildHost | 获取构建主机 |
| DeviceInfo.buildRootHash | 获取构建版本Hash |
| DeviceInfo.buildTime | 获取构建时间 |
| DeviceInfo.buildType | 获取构建类型 |
| DeviceInfo.buildUser | 获取构建用户 |
| DeviceInfo.buildVersion | 获取构建的版本号 |
| DeviceInfo.deviceType | 获取设备类型 |
| DeviceInfo.displayVersion | 获取产品版本 |
| DeviceInfo.distributionOSApiName | 获取发行版系统api版本名称|
| DeviceInfo.distributionOSApiVersion | 获取发行版系统api版本 |
| DeviceInfo.distributionOSName | 获取发行版系统名称 |
| DeviceInfo.distributionOSReleaseType | 获取发行版系统类型 |
| DeviceInfo.distributionOSVersion | 获取发行版系统版本号 |
| DeviceInfo.featureVersion | 获取Feature版本号 |
| DeviceInfo.firstApiVersion | 获取首个版本系统软件API版本。|
| DeviceInfo.hardwareModel | 获取硬件版本号|
| DeviceInfo.hardwareProfile | 获取硬件Profile|
| DeviceInfo.incrementalVersion | 获取差异版本号|
| DeviceInfo.majorVersion | 获取Major版本号|
| DeviceInfo.manufacture | 获取设备厂家名称|
| DeviceInfo.marketName | 获取外部产品系列 |
| DeviceInfo.osFullName | 获取系统版本 |
| DeviceInfo.osReleaseType | 获取系统的发布类型 |
| DeviceInfo.productModel | 获取认证型号|
| DeviceInfo.productSeries | 获取产品系列 |
| DeviceInfo.sdkApiVersion | 获取系统软件API版本 |
| DeviceInfo.securityPatchTag | 获取安全补丁级别 |
| DeviceInfo.seniorVersion | 获取Senior版本号 |
| DeviceInfo.serial | 获取设备序列号 |
| DeviceInfo.softwareModel | 获取内部软件子型号 |
| DeviceInfo.udid | 获取设备udid |
| DeviceInfo.versionId | 获取版本ID |


## 开发示例

以下示例演示了如何使用设备信息模块查询设备信息。

### 获取设备信息

以下示例代码演示了如何获取设备信息。

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.*

let osFullName = DeviceInfo.osFullName
Hilog.info(0, "deviceinfo", "the value of the osFullName is: :${osFullName}")

let sdkApiVersion = DeviceInfo.sdkApiVersion
Hilog.info(0, "deviceinfo", "the value of the sdkApiVersionis : :${sdkApiVersion}")

let marketName = DeviceInfo.marketName
Hilog.info(0, "deviceinfo", "the value of the marketName is: :${marketName}")
}
```
