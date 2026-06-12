# ohos.device_info (Device Information)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides terminal device information queries and cannot be configured by developers.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Permission List

ohos.permission.sec.ACCESS_UDID

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the above sample project and configuration template, see [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class DeviceInfo

```cangjie
public class DeviceInfo {}
```

**Function:** Provides terminal device information query methods.

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop ODID

```cangjie
public static prop ODID: String
```

**Function:** Developer Anonymous Device Identifier.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop abiList

```cangjie
public static prop abiList: String
```

**Function:** Application Binary Interface (ABI) list.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop bootloaderVersion

```cangjie
public static prop bootloaderVersion: String
```

**Function:** Bootloader version number.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop brand

```cangjie
public static prop brand: String
```

**Function:** Device brand name.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildHost

```cangjie
public static prop buildHost: String
```

**Function:** Build host.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildRootHash

```cangjie
public static prop buildRootHash: String
```

**Function:** Build version hash.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildTime

```cangjie
public static prop buildTime: String
```

**Function:** Build time.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildType

```cangjie
public static prop buildType: String
```

**Function:** Build type.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildUser

```cangjie
public static prop buildUser: String
```

**Function:** Build user.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop buildVersion

```cangjie
public static prop buildVersion: Int32
```

**Function:** Build version number, identifying the compiled build version number.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop deviceType

```cangjie
public static prop deviceType: String
```

**Function:** Device type.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop displayVersion

```cangjie
public static prop displayVersion: String
```

**Function:** Product version.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop distributionOSApiName

```cangjie
public static prop distributionOSApiName: String
```

**Function:** Distribution OS API version name.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop distributionOSApiVersion

```cangjie
public static prop distributionOSApiVersion: Int32
```

**Function:** Distribution OS API version.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop distributionOSName

```cangjie
public static prop distributionOSName: String
```

**Function:** Distribution OS name.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop distributionOSReleaseType

```cangjie
public static prop distributionOSReleaseType: String
```

**Function:** Distribution OS release type.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop distributionOSVersion

```cangjie
public static prop distributionOSVersion: String
```

**Function:** Distribution OS version number.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop featureVersion

```cangjie
public static prop featureVersion: Int32
```

**Function:** Feature version number, identifying planned new feature versions.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop firstApiVersion

```cangjie
public static prop firstApiVersion: Int32
```

**Function:** First version system software API version.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop hardwareModel

```cangjie
public static prop hardwareModel: String
```

**Function:** Hardware version number.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop hardwareProfile

```cangjie
public static prop hardwareProfile: String
```

**Function:** Hardware profile.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop incrementalVersion

```cangjie
public static prop incrementalVersion: String
```

**Function:** Incremental version number.

**Type:** String

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop majorVersion

```cangjie
public static prop majorVersion: Int32
```

**Function:** Major version number, incremented with major version updates.

**Type:** Int32

**Read/Write Permission:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22### static prop manufacture

```cangjie
public static prop manufacture: String
```

**Function:** Device manufacturer name.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop marketName

```cangjie
public static prop marketName: String
```

**Function:** External product series.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop osFullName

```cangjie
public static prop osFullName: String
```

**Function:** Operating system version.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop osReleaseType

```cangjie
public static prop osReleaseType: String
```

**Function:** System release type, with possible values:<br/>-&nbsp;Canary: Early preview version for specific developers, with no API stability guarantee.<br/>-&nbsp;Beta: Public beta version for developers, with no API stability guarantee.<br/>-&nbsp;Release: Public official version for developers, with API stability guarantee.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop productModel

```cangjie
public static prop productModel: String
```

**Function:** Certified model number.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop productSeries

```cangjie
public static prop productSeries: String
```

**Function:** Product series.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop sdkApiVersion

```cangjie
public static prop sdkApiVersion: Int32
```

**Function:** System software API version.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop sdkMinorApiVersion

```cangjie
public static prop sdkMinorApiVersion: Int32
```

**Function:** SDK Minor API version number.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 26.0.0

### static prop sdkPatchApiVersion

```cangjie
public static prop sdkPatchApiVersion: Int32
```

**Function:** SDK Patch API version number.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 26.0.0

### static prop securityPatchTag

```cangjie
public static prop securityPatchTag: String
```

**Function:** Security patch level.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop seniorVersion

```cangjie
public static prop seniorVersion: Int32
```

**Function:** Senior version number, incremented with major architectural changes or significant feature additions.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop serial

```cangjie
public static prop serial: String
```

**Function:** Device serial number.

**Type:** String

**Read/Write Capability:** Read-only

**Required Permission:** ohos.permission.sec.ACCESS_UDID

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop softwareModel

```cangjie
public static prop softwareModel: String
```

**Function:** Internal software sub-model.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop udid

```cangjie
public static prop udid: String
```

**Function:** Internal software sub-model.

**Type:** String

**Read/Write Capability:** Read-only

**Required Permission:** ohos.permission.sec.ACCESS_UDID

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

### static prop versionId

```cangjie
public static prop versionId: String
```

**Function:** Version ID.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let hardwareProfile = DeviceInfo.hardwareProfile
    Hilog.info(0, "deviceinfo", "the value of thehardwareProfile is : :${hardwareProfile}")
    let osFullName = DeviceInfo.osFullName
    Hilog.info(0, "deviceinfo", "the value of the osFullName is: :${osFullName}")
    let productModel = DeviceInfo.productModel
    Hilog.info(0, "deviceinfo", "the value of the productModelis : :${productModel}")
    let brand = DeviceInfo.brand
    Hilog.info(0, "deviceinfo", "the value of the brand is : :{brand}")
    let deviceType = DeviceInfo.deviceType
    Hilog.info(0, "deviceinfo", "the value of the deviceType is: :${deviceType}")
    let udid = DeviceInfo.udid
    Hilog.info(0, "deviceinfo", "the value of the udid is : :{udid}")
    let buildRootHash = DeviceInfo.buildRootHash
    Hilog.info(0, "deviceinfo", "the value of the buildRootHashis : :${buildRootHash}")
    let buildTime = DeviceInfo.buildTime
    Hilog.info(0, "deviceinfo", "the value of the buildTime is: :${buildTime}")
    let buildHost = DeviceInfo.buildHost
    Hilog.info(0, "deviceinfo", "the value of the buildHost is: :${buildHost}")
    let buildUser = DeviceInfo.buildUser
    Hilog.info(0, "deviceinfo", "the value of the buildUser is: :${buildUser}")
    let buildType = DeviceInfo.buildType
    Hilog.info(0, "deviceinfo", "the value of the buildType is: :${buildType}")
    let versionId = DeviceInfo.versionId
    Hilog.info(0, "deviceinfo", "the value of the versionId is: :${versionId}")
    let firstApiVersion = DeviceInfo.firstApiVersion
    Hilog.info(0, "deviceinfo", "the value of thefirstApiVersion is : :${firstApiVersion}")
    let sdkApiVersion = DeviceInfo.sdkApiVersion
    Hilog.info(0, "deviceinfo", "the value of the sdkApiVersionis : :${sdkApiVersion}")
    let buildVersion = DeviceInfo.buildVersion
    Hilog.info(0, "deviceinfo", "the value of the buildVersionis : :${buildVersion}")
    let majorVersion = DeviceInfo.majorVersion
    Hilog.info(0, "deviceinfo", "the value of the majorVersionis : :${majorVersion}")
    let displayVersion = DeviceInfo.displayVersion
    Hilog.info(0, "deviceinfo", "the value of thedisplayVersion is : :${displayVersion}")
    let serial = DeviceInfo.serial
    Hilog.info(0, "deviceinfo", "the value of the serial is : :{serial}")
    let osReleaseType = DeviceInfo.osReleaseType
    Hilog.info(0, "deviceinfo", "the value of the osReleaseTypeis : :${osReleaseType}")
    let incrementalVersion = DeviceInfo.incrementalVersion
    Hilog.info(0, "deviceinfo", "the value of theincrementalVersion is : :${incrementalVersion}")
    let securityPatchTag = DeviceInfo.securityPatchTag
    Hilog.info(0, "deviceinfo", "the value of thesecurityPatchTag is : :${securityPatchTag}")
    let abiList = DeviceInfo.abiList
    Hilog.info(0, "deviceinfo", "the value of the abiList is ::${abiList}")
    let bootloaderVersion = DeviceInfo.bootloaderVersion
    Hilog.info(0, "deviceinfo", "the value of thebootloaderVersion is : :${bootloaderVersion}")
    let hardwareModel = DeviceInfo.hardwareModel
    Hilog.info(0, "deviceinfo", "the value of the hardwareModelis : :${hardwareModel}")
    let softwareModel = DeviceInfo.softwareModel
    Hilog.info(0, "deviceinfo", "the value of the softwareModelis : :${softwareModel}")
    let productSeries = DeviceInfo.productSeries
    Hilog.info(0, "deviceinfo", "the value of the productSeriesis : :${productSeries}")
    let marketName = DeviceInfo.marketName
    Hilog.info(0, "deviceinfo", "the value of the marketName is: :${marketName}")
    let manufacture = DeviceInfo.manufacture
    Hilog.info(0, "deviceinfo", "the value of the manufactureis : :${manufacture}")
    let distributionOSName = DeviceInfo.distributionOSName
    Hilog.info(0, "deviceinfo", "the value of thedistributionOSName is : :${distributionOSName}")
    let distributionOSVersion = DeviceInfo.distributionOSVersion
    Hilog.info(0, "deviceinfo", "the value of the distributionOSVersion is : :${distributionOSVersion}")
    let distributionOSApiVersion = DeviceInfo.distributionOSApiVersion
    Hilog.info(0, "deviceinfo", "the value of the distributionOSApiVersion is : :${distributionOSApiVersion}")
    let distributionOSReleaseType = DeviceInfo.distributionOSReleaseType
    Hilog.info(0, "deviceinfo", "the value of the distributionOSReleaseType is : :${distributionOSReleaseType}")
let sdkMinorApiVersion = DeviceInfo.sdkMinorApiVersion
    Hilog.info(0, "deviceinfo", "the value of the sdkMinorApiVersion is: :${sdkMinorApiVersion}")
    let sdkPatchApiVersion = DeviceInfo.sdkPatchApiVersion
    Hilog.info(0, "deviceinfo", "the value of the sdkPatchApiVersion is: :${sdkPatchApiVersion}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func apiAvailable(Int32)

```cangjie
public func apiAvailable(version: Int32): Bool
```

**Function:** Checks whether the specified API version is available on the current device. This function provides compatibility checking across different OpenHarmony/Distribution OS versions. It automatically selects the appropriate version checking method based on the input format and API version range.

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 26.0.0

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|version|Int32|Yes|-|The API version to check. Accepts number format (e.g., 13), representing the OpenHarmony SDK API version (API 26- only).|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns `true` if the specified API version is available on the current device, `false` otherwise.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let result1 = apiAvailable(13)
Hilog.info(0, "deviceinfo", "apiAvailable(13) result: ${result1}")
```

## func apiAvailable(String)

```cangjie
public func apiAvailable(version: String): Bool
```

**Function:** Checks whether the specified API version is available on the current device. This function provides compatibility checking across different OpenHarmony/Distribution OS versions. It automatically selects the appropriate version checking method based on the input format and API version range.

**System Capability:** SystemCapability.Startup.SystemInfo

**Since Version:** 26.0.0

**Parameters:**

|Name|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|version|String|Yes|-|The API version to check. Accepts string format with dots (e.g., "26.0.0", "5.0.1"): For API 26+ (version >= 26.0.0), represents both OpenHarmony and Distribution OS API versions; For API 26- (version < 26.0.0), represents Distribution OS API version.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns `true` if the specified API version is available on the current device, `false` otherwise.|

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog

let result2 = apiAvailable("26.0.0")
Hilog.info(0, "deviceinfo", "apiAvailable(\"26.0.0\") result: ${result2}")
```