# ohos.geo_location_manager (Location Services)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Location services provide basic functionalities including GNSS positioning, network positioning (cellular base station, WLAN, Bluetooth positioning technologies).

> **Note:**
>
> This module's capabilities only support the WGS-84 coordinate system.

## Importing the Module

```cangjie
import kit.LocationKit.*
```

## Permission List

Before using the Location Kit system capabilities, applications must check whether they have obtained user authorization to access device location information. If authorization has not been granted, applications can request the necessary location permissions from the user.

The system provides the following location permissions:

ohos.permission.APPROXIMATELY_LOCATION: Used to obtain approximate location with an accuracy of 5 kilometers.

ohos.permission.LOCATION: Used to obtain precise location with meter-level accuracy.

ohos.permission.LOCATION_IN_BACKGROUND: Used for scenarios where the application needs to continue obtaining location information after switching to the background.

## Usage Instructions

API example code usage instructions:

- If the first line of the example code has a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above example projects and configuration templates, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#cangjie-example-code-instructions).

## class ContinuousLocationRequest

```cangjie
public class ContinuousLocationRequest {
    public init(interval: Int32, locationScenario: ScenarioValueType)
}
```

**Function:** Request parameters for continuous positioning, describing the continuous positioning requirement through a user activity scenario or a power consumption scenario.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop interval

```cangjie
public mut prop interval: Int32
```

**Function:** Represents the time interval for reporting location information, in seconds. The default value is 1, and the valid range is greater than or equal to 0. When the value is 0, there is no limit on the time interval for location reporting.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop locationScenario

```cangjie
public mut prop locationScenario: ScenarioValueType
```

**Function:** Represents the positioning scenario information. For valid values, see the definition of [ScenarioValueType](#enum-scenariovaluetype).

**Type:** [ScenarioValueType](#enum-scenariovaluetype)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### init(Int32, ScenarioValueType)

```cangjie
public init(interval: Int32, locationScenario: ScenarioValueType)
```

**Function:** Constructs a ContinuousLocationRequest object.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| interval | Int32 | Yes | - | Represents the time interval for reporting location information, in seconds. |
| locationScenario | [ScenarioValueType](#enum-scenariovaluetype) | Yes | - | Represents the positioning scenario information, which is a user activity scenario or a power consumption scenario. |

## class CountryCode

```cangjie
public class CountryCode {}
```

**Function:** Country code information, including the country code string and the source of the country code.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop country

```cangjie
public mut prop country: String
```

**Function:** Represents the country code string.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop countryCodeType

```cangjie
public mut prop countryCodeType: CountryCodeType
```

**Function:** Represents the source of the country code information. For valid values, see the definition of [CountryCodeType](#enum-countrycodetype).

**Type:** [CountryCodeType](#enum-countrycodetype)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

## class CurrentLocationRequest

```cangjie
public class CurrentLocationRequest {
    public var priority: LocationRequestPriority
    public var scenario: LocationRequestScenario
    public var maxAccuracy: Float32
    public var timeoutMs: Int32
    public init(priority!: LocationRequestPriority = LocationRequestPriority.FirstFix,
        scenario!: LocationRequestScenario = LocationRequestScenario.Unset, maxAccuracy!: Float32 = 0.0,
        timeoutMs!: Int32 = 5000)
}
```

**Function:** Parameters for current location information requests.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var maxAccuracy

```cangjie
public var maxAccuracy: Float32
```

**Function:** Represents accuracy information in meters.

Only effective in precise location scenarios (where both ohos.permission.APPROXIMATELY_LOCATION and ohos.permission.LOCATION permissions are granted). This field is meaningless in approximate location scenarios (where only ohos.permission.APPROXIMATELY_LOCATION is granted).

Default value is 0, with a valid range of greater than or equal to 0.

When scenario is Navigation/TrajectoryTracking/CarHailing or priority is Accuracy, it is recommended to set maxAccuracy to a value greater than 10.

When scenario is DailyLifeService/NoPower or priority is LowPower/FirstFix, it is recommended to set maxAccuracy to a value greater than 100.

**Type:** Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var priority

```cangjie
public var priority: LocationRequestPriority
```

**Function:** Represents priority information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. Valid values are defined in [LocationRequestPriority](#enum-locationrequestpriority).

**Type:** [LocationRequestPriority](#enum-locationrequestpriority)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var scenario

```cangjie
public var scenario: LocationRequestScenario
```

**Function:** Represents scenario information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. Valid values are defined in [LocationRequestScenario](#enum-locationrequestscenario).

**Type:** [LocationRequestScenario](#enum-locationrequestscenario)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var timeoutMs

```cangjie
public var timeoutMs: Int32
```

**Function:** Represents the timeout duration in milliseconds, with a minimum of 1000 milliseconds. Valid range is greater than or equal to 1000.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### init(LocationRequestPriority, LocationRequestScenario, Float32, Int32)

```cangjie
public init(priority!: LocationRequestPriority = LocationRequestPriority.FirstFix,
    scenario!: LocationRequestScenario = LocationRequestScenario.Unset, maxAccuracy!: Float32 = 0.0,
    timeoutMs!: Int32 = 5000)
```

**Function:** Constructs a CurrentLocationRequest object.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| priority | [LocationRequestPriority](#enum-locationrequestpriority) | No | LocationRequestPriority.FirstFix | **Named parameter.** Represents priority information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. Valid values are defined in [LocationRequestPriority](#enum-locationrequestpriority). |
| scenario | [LocationRequestScenario](#enum-locationrequestscenario) | No | LocationRequestScenario.Unset | **Named parameter.** Represents scenario information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. Valid values are defined in [LocationRequestScenario](#enum-locationrequestscenario). |
| maxAccuracy | Float32 | No | 0.0 | **Named parameter.** Represents accuracy information in meters.<br/>Only effective in precise location scenarios (where both ohos.permission.APPROXIMATELY_LOCATION and ohos.permission.LOCATION permissions are granted). This field is meaningless in approximate location scenarios (where only ohos.permission.APPROXIMATELY_LOCATION is granted).<br/>Default value is 0, with a valid range of greater than or equal to 0.<br/>When scenario is Navigation/TrajectoryTracking/CarHailing or priority is Accuracy, it is recommended to set maxAccuracy to a value greater than 10.<br/>When scenario is DailyLifeService/NoPower or priority is LowPower/FirstFix, it is recommended to set maxAccuracy to a value greater than 100. |
| timeoutMs | Int32 | No | 5000 | **Named parameter.** Represents the timeout duration in milliseconds, with a minimum of 1000 milliseconds. Valid range is greater than or equal to 1000. |

## class GeoLocationManager

```cangjie
public class GeoLocationManager {}
```

**Function:** A class used to provide location services.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### static func getCurrentLocation()

```cangjie
public static func getCurrentLocation(): Location
```

**Function:** Obtains the current location.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [Location](#class-location) | Returns the current location information. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*

let location = GeoLocationManager.getCurrentLocation(SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 1000))
```

### static func getCurrentLocation(CurrentLocationRequest)

```cangjie
public static func getCurrentLocation(request: CurrentLocationRequest): Location
```

**Function:** Obtains the current location.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| request | [CurrentLocationRequest](#class-currentlocationrequest) | Yes | - | Sets the location request parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Location](#class-location) | Returns the current location information. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*

let location = GeoLocationManager.getCurrentLocation(SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 1000))
```

### static func getCurrentLocation(SingleLocationRequest)

```cangjie
public static func getCurrentLocation(request: SingleLocationRequest): Location
```

**Function:** Obtains the current location.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| request | [SingleLocationRequest](#class-singlelocationrequest) | Yes | - | Sets the location request parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Location](#class-location) | Returns the current location information. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*

let location = GeoLocationManager.getCurrentLocation(SingleLocationRequest(LocatingPriority.PriorityLocatingSpeed, 1000))
```

### static func isLocationEnabled()

```cangjie
public static func isLocationEnabled(): Bool
```

**Function:** Checks whether location services are enabled.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Location services are enabled;<br/>false: Location services are disabled. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.LocationKit.*

let res = GeoLocationManager.isLocationEnabled()
```

## class Location

```cangjie
public class Location {
    public var latitude: Float64
    public var longitude: Float64
    public var altitude: Float64
    public var accuracy: Float64
    public var speed: Float64
    public var timeStamp: Int64
    public var direction: Float64
    public var timeSinceBoot: Int64
    public var additions: Array<String>
    public var additionSize: Int64
    public var additionsMap: Map<String, String>
    public var altitudeAccuracy: Float64
    public var speedAccuracy: Float64
    public var directionAccuracy: Float64
    public var uncertaintyOfTimeSinceBoot: Int64
    public var sourceType: LocationSourceType
}
```

**Function:** Location information.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var accuracy

```cangjie
public var accuracy: Float64
```

**Function:** Represents accuracy information in meters.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var additionSize

```cangjie
public var additionSize: ?Int64
```

**Function:** Number of additional information items. Valid range is greater than or equal to 0.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var additions

```cangjie
public var additions: ?Array<String>
```

**Function:** Additional information.

**Type:** Array\<String>

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var additionsMap

```cangjie
public var additionsMap: ?Map<String, String>
```

**Function:** Additional information. The specific content and order are consistent with additions.

**Type:** Map

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var altitude

```cangjie
public var altitude: Float64
```

**Function:** Represents altitude information in meters.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var altitudeAccuracy

```cangjie
public var altitudeAccuracy: ?Float64
```

**Function:** Represents the accuracy of altitude information in meters.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var direction

```cangjie
public var direction: Float64
```

**Function:** Represents heading information in degrees, with a valid range of 0 to 360.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var directionAccuracy

```cangjie
public var directionAccuracy: ?Float64
```

**Function:** Represents the accuracy of heading information in degrees, with a valid range of 0 to 360.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var latitude

```cangjie
public var latitude: Float64
```

**Function:** Represents latitude information. Positive values indicate north latitude, and negative values indicate south latitude. Valid range is -90 to 90. Only supports the WGS84 coordinate system.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var longitude

```cangjie
public var longitude: Float64
```

**Function:** Represents longitude information. Positive values indicate east longitude, and negative values indicate west longitude. Valid range is -180 to 180. Only supports the WGS84 coordinate system.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var sourceType

```cangjie
public var sourceType: ?LocationSourceType
```

**Function:** Represents the source of the location result.

**Type:** [LocationSourceType](#enum-locationsourcetype)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var speed

```cangjie
public var speed: ?Float64
```

**Function:** Represents speed information in meters per second.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var speedAccuracy

```cangjie
public var speedAccuracy: Float64
```

**Function:** Represents the accuracy of speed information in meters per second.

**Type:** Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var timeSinceBoot

```cangjie
public var timeSinceBoot: Int64
```

**Function:** Represents the location timestamp in boot time format.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var timeStamp

```cangjie
public var timeStamp: Int64
```

**Function:** Represents the location timestamp in UTC format.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var uncertaintyOfTimeSinceBoot

```cangjie
public var uncertaintyOfTimeSinceBoot: ?Int64
```

**Function:** Represents the uncertainty of the location timestamp.

**Type:** Int64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

## class LocationCommand

```cangjie
public class LocationCommand {
    public init(scenario: LocationRequestScenario, command: String)
}
```

**Function:** Extended command parameters of the location subsystem, including the target positioning scenario and the command content.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop scenario

```cangjie
public mut prop scenario: LocationRequestScenario
```

**Function:** Represents the positioning scenario for sending the command.

**Type:** [LocationRequestScenario](#enum-locationrequestscenario)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop command

```cangjie
public mut prop command: String
```

**Function:** Represents the command content to send. The string length cannot exceed 100.

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### init(LocationRequestScenario, String)

```cangjie
public init(scenario: LocationRequestScenario, command: String)
```

**Function:** Constructs an extended command parameter object of the location subsystem.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| scenario | [LocationRequestScenario](#enum-locationrequestscenario) | Yes | - | Represents the positioning scenario for sending the command. |
| command | String | Yes | - | Represents the command content to send. The string length cannot exceed 100. |

## class LocationRequest

```cangjie
public class LocationRequest {
    public init(priority!: ?LocationRequestPriority = None,
        scenario!: ?LocationRequestScenario = None, timeInterval!: ?Int32 = None,
        distanceInterval!: ?Float64 = None, maxAccuracy!: ?Float32 = None)
}
```

**Function:** Location information request parameters for continuous positioning, used to configure the positioning priority, scenario, reporting interval, and accuracy requirement.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop priority

```cangjie
public mut prop priority: ?LocationRequestPriority
```

**Function:** Represents the priority information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. The default value is FirstFix. For valid values, see the definition of [LocationRequestPriority](#enum-locationrequestpriority).

**Type:** ?[LocationRequestPriority](#enum-locationrequestpriority)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop scenario

```cangjie
public mut prop scenario: ?LocationRequestScenario
```

**Function:** Represents the scenario information. When scenario is set to Unset, the priority parameter takes effect; otherwise, it does not. If both scenario and priority are set to Unset, the location request cannot be initiated. The default value is Unset. For valid values, see the definition of [LocationRequestScenario](#enum-locationrequestscenario).

**Type:** ?[LocationRequestScenario](#enum-locationrequestscenario)

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop timeInterval

```cangjie
public mut prop timeInterval: ?Int32
```

**Function:** Represents the time interval for reporting location information, in seconds. The valid range is greater than or equal to 0. The default value is the minimum time interval allowed by the current positioning mode: 1 second for GNSS positioning and 20 seconds for network positioning. If the set value is less than the minimum interval, the minimum time interval takes effect. If the value is 0, the time interval is not verified and location information is reported directly.

**Type:** ?Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop distanceInterval

```cangjie
public mut prop distanceInterval: ?Float64
```

**Function:** Represents the distance interval for reporting location information, in meters. The default value is 0, and the valid range is greater than or equal to 0. When the value is 0, there is no limit on the distance interval for location reporting.

**Type:** ?Float64

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### prop maxAccuracy

```cangjie
public mut prop maxAccuracy: ?Float32
```

**Function:** Represents the accuracy required by the application when requesting location information from the system, in meters. The default value is 0, which means the accuracy of location information is not limited, and the valid range is greater than or equal to 0. This parameter is valid only in the precise location scenario (that is, both the ohos.permission.APPROXIMATELY_LOCATION and ohos.permission.LOCATION permissions are granted). In the approximate location scenario (that is, only the ohos.permission.APPROXIMATELY_LOCATION permission is granted), this parameter is meaningless.

When this parameter takes effect, the system compares the location information reported by the GNSS or network positioning service with the location requirement of the application. When the accuracy value (accuracy) in the location information is less than or equal to the accuracy value (maxAccuracy) required by the application, the location information is returned to the application; otherwise, the system discards the received location information.

When scenario is Navigation, TrajectoryTracking, or CarHailing, or priority is Accuracy, it is recommended to set maxAccuracy to a value greater than 10. When scenario is DailyLifeService or NoPower, or priority is LowPower or FirstFix, it is recommended to set maxAccuracy to a value greater than 100.

**Type:** ?Float32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### init(?LocationRequestPriority, ?LocationRequestScenario, ?Int32, ?Float64, ?Float32)

```cangjie
public init(priority!: ?LocationRequestPriority = None,
    scenario!: ?LocationRequestScenario = None, timeInterval!: ?Int32 = None,
    distanceInterval!: ?Float64 = None, maxAccuracy!: ?Float32 = None)
```

**Function:** Constructs a location information request object. Unset parameters use the system default values.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| priority | ?[LocationRequestPriority](#enum-locationrequestpriority) | No | None | **Named parameter.** Represents the priority information. The default value is FirstFix. |
| scenario | ?[LocationRequestScenario](#enum-locationrequestscenario) | No | None | **Named parameter.** Represents the scenario information. The default value is Unset. |
| timeInterval | ?Int32 | No | None | **Named parameter.** Represents the time interval for reporting location information, in seconds. The default value is 1. |
| distanceInterval | ?Float64 | No | None | **Named parameter.** Represents the distance interval for reporting location information, in meters. The default value is 0.0. |
| maxAccuracy | ?Float32 | No | None | **Named parameter.** Represents the accuracy value in meters. The default value is 0.0. |

## class SatelliteStatusInfo

```cangjie
public class SatelliteStatusInfo {}
```

**Function:** Satellite status information, including the number of satellites, satellite IDs, carrier-to-noise densities, altitudes, azimuths, carrier frequencies, constellation types, and additional information.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop satellitesNumber

```cangjie
public mut prop satellitesNumber: Int32
```

**Function:** Number of satellites.

**Type:** Int32

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop satelliteIds

```cangjie
public mut prop satelliteIds: Array<Int32>
```

**Function:** Satellite ID array.

**Type:** Array\<Int32\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop carrierToNoiseDensitys

```cangjie
public mut prop carrierToNoiseDensitys: Array<Float64>
```

**Function:** Satellite carrier-to-noise density array.

**Type:** Array\<Float64\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop altitudes

```cangjie
public mut prop altitudes: Array<Float64>
```

**Function:** Satellite altitude array.

**Type:** Array\<Float64\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop azimuths

```cangjie
public mut prop azimuths: Array<Float64>
```

**Function:** Satellite azimuth array.

**Type:** Array\<Float64\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop carrierFrequencies

```cangjie
public mut prop carrierFrequencies: Array<Float64>
```

**Function:** Satellite carrier frequency array.

**Type:** Array\<Float64\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop satelliteConstellation

```cangjie
public mut prop satelliteConstellation: ?Array<SatelliteConstellationCategory>
```

**Function:** Satellite constellation type array. For details, see [SatelliteConstellationCategory](#enum-satelliteconstellationcategory).

**Type:** ?Array\<[SatelliteConstellationCategory](#enum-satelliteconstellationcategory)\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### prop satelliteAdditionalInfo

```cangjie
public mut prop satelliteAdditionalInfo: ?Array<Int32>
```

**Function:** Additional information array of satellites.

**Type:** ?Array\<Int32\>

**Read/Write Capability:** Readable and writable

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

## class SingleLocationRequest

```cangjie
public class SingleLocationRequest {
    public var locatingPriority: LocatingPriority
    public var locatingTimeoutMs: Int32
    public init(locatingPriority: LocatingPriority, locatingTimeoutMs: Int32)
}
```

**Function:** Request parameters for single-shot positioning.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var locatingPriority

```cangjie
public var locatingPriority: LocatingPriority
```

**Function:** Indicates priority information. For valid values, see the definition of [LocatingPriority](#enum-locatingpriority).

**Type:** [LocatingPriority](#enum-locatingpriority)

**Access:** Read-write

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### var locatingTimeoutMs

```cangjie
public var locatingTimeoutMs: Int32
```

**Function:** Indicates the timeout duration in milliseconds, with a minimum of 1000 ms. The value must be greater than or equal to 1000.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### init(LocatingPriority, Int32)

```cangjie
public init(locatingPriority: LocatingPriority, locatingTimeoutMs: Int32)
```

**Function:** Constructs a SingleLocationRequest object.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

**Parameters:**

| Name | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| locatingPriority | [LocatingPriority](#enum-locatingpriority) | Yes | - | Indicates priority information. For valid values, see the definition of [LocatingPriority](#enum-locatingpriority). |
| locatingTimeoutMs | Int32 | Yes | - | Indicates the timeout duration in milliseconds, with a minimum of 1000 ms. The value must be greater than or equal to 1000. |

## enum CountryCodeType

```cangjie
public enum CountryCodeType {
    | CountryCodeFromLocale
    | CountryCodeFromSim
    | CountryCodeFromLocation
    | CountryCodeFromNetwork
    | ...
}
```

**Function:** Source types of the country code.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<CountryCodeType\>
- ToString

### CountryCodeFromLocale

```cangjie
CountryCodeFromLocale
```

**Function:** The country code obtained from the language configuration information of the globalization module.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### CountryCodeFromSim

```cangjie
CountryCodeFromSim
```

**Function:** The country code obtained from the SIM card.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### CountryCodeFromLocation

```cangjie
CountryCodeFromLocation
```

**Function:** The country code obtained through reverse geocoding based on the user's location information.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### CountryCodeFromNetwork

```cangjie
CountryCodeFromNetwork
```

**Function:** The country code obtained from the cellular network registration information.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the country code source type to a string representation.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the country code source type. |

### func ==(CountryCodeType)

```cangjie
public operator func ==(other: CountryCodeType): Bool
```

**Function:** Checks whether two country code source types are equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [CountryCodeType](#enum-countrycodetype) | Yes | - | The country code source type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two country code source types are equal; false otherwise. |

### func !=(CountryCodeType)

```cangjie
public operator func !=(other: CountryCodeType): Bool
```

**Function:** Checks whether two country code source types are not equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [CountryCodeType](#enum-countrycodetype) | Yes | - | The country code source type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two country code source types are not equal; false otherwise. |

## enum LocatingPriority

```cangjie
public enum LocatingPriority {
    | PriorityAccuracy
    | PriorityLocatingSpeed
    | ...
}
```

**Function:** Priority types in single-shot location requests.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### PriorityAccuracy

```cangjie
PriorityAccuracy
```

**Function:** Indicates accuracy priority.

The accuracy-first strategy uses both GNSS and network positioning technologies and returns the most accurate result within a period, which is the shorter of [SingleLocationRequest](#class-singlelocationrequest).locatingTimeoutMs and 30 seconds. This strategy consumes more hardware resources and power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### PriorityLocatingSpeed

```cangjie
PriorityLocatingSpeed
```

**Function:** Indicates fast location acquisition priority. If an application wants to quickly obtain a location, this priority type can be set.

The speed-first strategy uses both GNSS and network positioning technologies to quickly obtain location results in both indoor and outdoor scenarios. The first obtained location result is returned to the application. This strategy consumes more hardware resources and power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

## enum LocationError

```cangjie
public enum LocationError {
    | LocatingFailedDefault
    | LocatingFailedLocationPermissionDenied
    | LocatingFailedBackgroundPermissionDenied
    | LocatingFailedLocationSwitchOff
    | LocatingFailedInternetAccessFailure
    | ...
}
```

**Function:** Error information during continuous positioning.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<LocationError\>
- ToString

### LocatingFailedDefault

```cangjie
LocatingFailedDefault
```

**Function:** Default cause of a locating failure.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### LocatingFailedLocationPermissionDenied

```cangjie
LocatingFailedLocationPermissionDenied
```

**Function:** Indicates that continuous positioning fails because the verification of the ohos.permission.APPROXIMATELY_LOCATION permission or the ohos.permission.LOCATION permission fails.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### LocatingFailedBackgroundPermissionDenied

```cangjie
LocatingFailedBackgroundPermissionDenied
```

**Function:** Indicates that continuous positioning fails because the location permission verification fails when the application is in the background.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### LocatingFailedLocationSwitchOff

```cangjie
LocatingFailedLocationSwitchOff
```

**Function:** Indicates that continuous positioning fails because the location switch is off.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### LocatingFailedInternetAccessFailure

```cangjie
LocatingFailedInternetAccessFailure
```

**Function:** Indicates that the network cannot be accessed, causing network positioning to fail.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the location error information to a string representation.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the location error information. |

### func ==(LocationError)

```cangjie
public operator func ==(other: LocationError): Bool
```

**Function:** Checks whether two pieces of location error information are equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LocationError](#enum-locationerror) | Yes | - | The location error information to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two pieces of location error information are equal; false otherwise. |

### func !=(LocationError)

```cangjie
public operator func !=(other: LocationError): Bool
```

**Function:** Checks whether two pieces of location error information are not equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [LocationError](#enum-locationerror) | Yes | - | The location error information to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two pieces of location error information are not equal; false otherwise. |

## enum LocationRequestPriority

```cangjie
public enum LocationRequestPriority {
    | Unset
    | Accuracy
    | LowPower
    | FirstFix
    | ...
}
```

**Function:** Priority types for location information in location requests.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Accuracy

```cangjie
Accuracy
```

**Function:** Indicates accuracy priority.

The accuracy-first strategy mainly uses GNSS positioning technology. Network positioning technology is used before GNSS provides stable location results. During continuous positioning, if no GNSS location result is obtained for more than 30 seconds, network positioning technology is used. This strategy consumes more hardware resources and power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### FirstFix

```cangjie
FirstFix
```

**Function:** Indicates fast location acquisition priority. If an application wants to quickly obtain a location, this priority type can be set.

The speed-first strategy uses both GNSS and network positioning technologies to quickly obtain location results in both indoor and outdoor scenarios. When multiple positioning technologies provide location results, the system selects the most accurate one to return to the application. This strategy consumes more hardware resources and power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### LowPower

```cangjie
LowPower
```

**Function:** Indicates low power priority.

The low-power strategy uses only network positioning technology, which can provide location services in both indoor and outdoor scenarios. Since it relies on the distribution of nearby base stations, visible WLANs, and Bluetooth devices, the accuracy of location results may vary significantly. This strategy is recommended for scenarios where high accuracy is not required, as it effectively reduces power consumption.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Unset

```cangjie
Unset
```

**Function:** Indicates that the priority is not set, meaning [LocationRequestPriority](#enum-locationrequestpriority) is invalid.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

## enum LocationRequestScenario

```cangjie
public enum LocationRequestScenario {
    | Unset
    | Navigation
    | TrajectoryTracking
    | CarHailing
    | DailyLifeService
    | NoPower
    | ...
}
```

**Function:** Positioning scenario types in location requests.

> **Note:**
>
> When using Navigation/TrajectoryTracking/CarHailing scenarios for single-shot or continuous positioning, network positioning technology is used before GNSS provides stable location results. During continuous positioning, if no GNSS location result is obtained for more than 30 seconds, network positioning technology is used to obtain the location.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### CarHailing

```cangjie
CarHailing
```

**Function:** Indicates ride-hailing scenario.

Applicable to scenarios where users need to locate their current position for ride-hailing services, such as ride-hailing applications.

Mainly uses GNSS positioning technology, which consumes more power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### DailyLifeService

```cangjie
DailyLifeService
```

**Function:** Indicates daily service scenario.

Applicable to scenarios where precise user location is not required, such as news, online shopping, and food delivery applications.

This scenario uses only network positioning technology, which consumes less power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Navigation

```cangjie
Navigation
```

**Function:** Indicates navigation scenario.

Applicable to scenarios where real-time device location is needed outdoors, such as vehicle and pedestrian navigation.

Mainly uses GNSS positioning technology, which consumes more power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### NoPower

```cangjie
NoPower
```

**Function:** Indicates no-power scenario. In this scenario, positioning is not actively triggered. Location results are returned to the current application only when other applications perform positioning.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### TrajectoryTracking

```cangjie
TrajectoryTracking
```

**Function:** Indicates trajectory tracking scenario.

Applicable to scenarios where user location trajectories need to be recorded, such as fitness applications tracking movement paths.

Mainly uses GNSS positioning technology, which consumes more power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Unset

```cangjie
Unset
```

**Function:** Indicates that the scenario is not set, meaning [LocationRequestScenario](#enum-locationrequestscenario) is invalid.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

## enum LocationSourceType

```cangjie
public enum LocationSourceType {
    | Gnss
    | Network
    | Indoor
    | Rtk
    | ...
}
```

**Function:** Source types of location results.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Gnss

```cangjie
Gnss
```

**Function:** Indicates that the location result comes from GNSS positioning technology.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Indoor

```cangjie
Indoor
```

**Function:** Indicates that the location result comes from indoor high-precision positioning technology.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Network

```cangjie
Network
```

**Function:** Indicates that the location result comes from network positioning technology.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21

### Rtk

```cangjie
Rtk
```

**Function:** Indicates that the location result comes from outdoor high-precision positioning technology.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 21
```

## enum PowerConsumptionScenario

```cangjie
public enum PowerConsumptionScenario {
    | HighPowerConsumption
    | LowPowerConsumption
    | NoPowerConsumption
    | ...
}
```

**Function:** Power consumption scenario types in location requests.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<PowerConsumptionScenario\>
- ToString

### HighPowerConsumption

```cangjie
HighPowerConsumption
```

**Function:** High power consumption. GNSS positioning technology is used as the primary technology, and network positioning technology is used to provide services before GNSS provides stable location results. During continuous positioning, if no GNSS location result is obtained for more than 30 seconds, network positioning technology is used to obtain the location. This scenario consumes a large amount of device hardware resources and power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### LowPowerConsumption

```cangjie
LowPowerConsumption
```

**Function:** Low power consumption. This scenario is applicable to scenarios where high accuracy of the user location is not required, such as news, online shopping, and food delivery applications. This scenario uses only network positioning technology to provide services, and consumes less power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### NoPowerConsumption

```cangjie
NoPowerConsumption
```

**Function:** No power consumption. In this scenario, positioning is not actively triggered. Location results are returned to the current application only when other applications perform positioning.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the power consumption scenario type to a string representation.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the power consumption scenario type. |

### func ==(PowerConsumptionScenario)

```cangjie
public operator func ==(other: PowerConsumptionScenario): Bool
```

**Function:** Checks whether two power consumption scenario types are equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [PowerConsumptionScenario](#enum-powerconsumptionscenario) | Yes | - | The power consumption scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two power consumption scenario types are equal; false otherwise. |

### func !=(PowerConsumptionScenario)

```cangjie
public operator func !=(other: PowerConsumptionScenario): Bool
```

**Function:** Checks whether two power consumption scenario types are not equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [PowerConsumptionScenario](#enum-powerconsumptionscenario) | Yes | - | The power consumption scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two power consumption scenario types are not equal; false otherwise. |

## enum SatelliteConstellationCategory

```cangjie
public enum SatelliteConstellationCategory {
    | ConstellationCategoryUnknown
    | ConstellationCategoryGps
    | ConstellationCategorySbas
    | ConstellationCategoryGlonass
    | ConstellationCategoryQzss
    | ConstellationCategoryBeidou
    | ConstellationCategoryGalileo
    | ConstellationCategoryIrnss
    | ...
}
```

**Function:** Satellite constellation type.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parent Types:**

- Equatable\<SatelliteConstellationCategory\>
- ToString

### ConstellationCategoryUnknown

```cangjie
ConstellationCategoryUnknown
```

**Function:** Unknown constellation type.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryGps

```cangjie
ConstellationCategoryGps
```

**Function:** GPS constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategorySbas

```cangjie
ConstellationCategorySbas
```

**Function:** SBAS (Satellite-Based Augmentation System) constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryGlonass

```cangjie
ConstellationCategoryGlonass
```

**Function:** GLONASS constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryQzss

```cangjie
ConstellationCategoryQzss
```

**Function:** QZSS (Quasi-Zenith Satellite System) constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryBeidou

```cangjie
ConstellationCategoryBeidou
```

**Function:** BeiDou constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryGalileo

```cangjie
ConstellationCategoryGalileo
```

**Function:** Galileo constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### ConstellationCategoryIrnss

```cangjie
ConstellationCategoryIrnss
```

**Function:** IRNSS (Indian Regional Navigation Satellite System) constellation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the satellite constellation type to its string representation.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the satellite constellation type. |

### func ==(SatelliteConstellationCategory)

```cangjie
public operator func ==(other: SatelliteConstellationCategory): Bool
```

**Function:** Checks whether two satellite constellation types are equal.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [SatelliteConstellationCategory](#enum-satelliteconstellationcategory) | Yes | - | The satellite constellation type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two satellite constellation types are equal; false otherwise. |

### func !=(SatelliteConstellationCategory)

```cangjie
public operator func !=(other: SatelliteConstellationCategory): Bool
```

**Function:** Checks whether two satellite constellation types are not equal.

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [SatelliteConstellationCategory](#enum-satelliteconstellationcategory) | Yes | - | The satellite constellation type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two satellite constellation types are not equal; false otherwise. |

## enum ScenarioValueType

```cangjie
public enum ScenarioValueType {
    | UserActivityScenarioValue(UserActivityScenario)
    | PowerConsumptionScenarioValue(PowerConsumptionScenario)
    | ...
}
```

**Function:** Positioning scenario type, used as the scenario parameter in continuous positioning requests. A user activity scenario or a power consumption scenario can be selected.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<ScenarioValueType\>
- ToString

### UserActivityScenarioValue(UserActivityScenario)

```cangjie
UserActivityScenarioValue(UserActivityScenario)
```

**Function:** Represents the user activity scenario. For valid values, see the definition of [UserActivityScenario](#enum-useractivityscenario).

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### PowerConsumptionScenarioValue(PowerConsumptionScenario)

```cangjie
PowerConsumptionScenarioValue(PowerConsumptionScenario)
```

**Function:** Represents the power consumption scenario. For valid values, see the definition of [PowerConsumptionScenario](#enum-powerconsumptionscenario).

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the positioning scenario type to a string representation.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the positioning scenario type. |

### func ==(ScenarioValueType)

```cangjie
public operator func ==(other: ScenarioValueType): Bool
```

**Function:** Checks whether two positioning scenario types are equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ScenarioValueType](#enum-scenariovaluetype) | Yes | - | The positioning scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two positioning scenario types are equal; false otherwise. |

### func !=(ScenarioValueType)

```cangjie
public operator func !=(other: ScenarioValueType): Bool
```

**Function:** Checks whether two positioning scenario types are not equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [ScenarioValueType](#enum-scenariovaluetype) | Yes | - | The positioning scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two positioning scenario types are not equal; false otherwise. |

## enum UserActivityScenario

```cangjie
public enum UserActivityScenario {
    | Navigation
    | Sport
    | Transport
    | DailyLifeService
    | ...
}
```

**Function:** User activity scenario types in location requests.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parent Types:**

- Equatable\<UserActivityScenario\>
- ToString

### Navigation

```cangjie
Navigation
```

**Function:** Indicates the navigation scenario. This scenario is applicable to scenarios where the real-time location of the device needs to be obtained outdoors, such as vehicle and pedestrian navigation. GNSS positioning technology is mainly used to provide services, and the power consumption is high.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### Sport

```cangjie
Sport
```

**Function:** Indicates the sports scenario. This scenario is applicable to scenarios where the user's location trajectory needs to be recorded, such as the trajectory recording function of sports applications. GNSS positioning technology is mainly used to provide services, and the power consumption is high.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### Transport

```cangjie
Transport
```

**Function:** Indicates the travel scenario. This scenario is applicable to user travel scenarios, such as taking a taxi or using public transport. GNSS positioning technology is mainly used to provide services, and the power consumption is high.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### DailyLifeService

```cangjie
DailyLifeService
```

**Function:** Indicates the daily life service scenario. This scenario is applicable to scenarios where the precise location of the user does not need to be obtained, such as news, online shopping, and food delivery applications. This scenario uses only network positioning technology to provide services, and consumes less power.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

### func toString()

```cangjie
public func toString(): String
```

**Function:** Converts the user activity scenario type to a string representation.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the user activity scenario type. |

### func ==(UserActivityScenario)

```cangjie
public operator func ==(other: UserActivityScenario): Bool
```

**Function:** Checks whether two user activity scenario types are equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [UserActivityScenario](#enum-useractivityscenario) | Yes | - | The user activity scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two user activity scenario types are equal; false otherwise. |

### func !=(UserActivityScenario)

```cangjie
public operator func !=(other: UserActivityScenario): Bool
```

**Function:** Checks whether two user activity scenario types are not equal.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [UserActivityScenario](#enum-useractivityscenario) | Yes | - | The user activity scenario type to compare. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true if the two user activity scenario types are not equal; false otherwise. |

## func onLocationChange(LocationRequest, Callback1Argument\<Location>)

```cangjie
public func onLocationChange(request: LocationRequest, callback: Callback1Argument<Location>): Unit
```

**Function:** Subscribes to location changes and initiates a location request. This API uses a callback to return the result asynchronously.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| request | [LocationRequest](#class-locationrequest) | Yes | - | Sets the location request parameters. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\> | Yes | - | Callback used to receive the location information. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = LocationRequest(priority: LocationRequestPriority.FirstFix,
        scenario: LocationRequestScenario.Unset, timeInterval: 1, distanceInterval: 0.0, maxAccuracy: 0.0)
    onLocationChange(request, Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationChange(ContinuousLocationRequest, Callback1Argument\<Location>)

```cangjie
public func onLocationChange(request: ContinuousLocationRequest, callback: Callback1Argument<Location>): Unit
```

**Function:** Subscribes to location changes and initiates a location request. This API uses a callback to return the result asynchronously.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| request | [ContinuousLocationRequest](#class-continuouslocationrequest) | Yes | - | Sets the request parameters for continuous positioning. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\> | Yes | - | Callback used to receive the location information. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = ContinuousLocationRequest(1,
        ScenarioValueType.UserActivityScenarioValue(UserActivityScenario.Navigation))
    onLocationChange(request, Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationChange(?Callback1Argument\<Location>)

```cangjie
public func offLocationChange(callback!: ?Callback1Argument<Location> = None): Unit
```

**Function:** Unsubscribes from location changes and deletes the corresponding location request. The callback passed in must be the same as the callback passed in to onLocationChange; otherwise, the unsubscription fails. If no callback is passed in, all subscriptions of this type are canceled.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Location\> | No | None | **Named parameter.** Callback for which the subscription is to be canceled. If this parameter is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Location> {
    public func invoke(err: ?BusinessException, arg: Location): Unit {
        Hilog.info(0, "test", "latitude=${arg.latitude}, longitude=${arg.longitude}")
    }
}

try {
    let request = LocationRequest(priority: LocationRequestPriority.FirstFix, scenario: LocationRequestScenario.Unset)
    let callback = Callback()
    onLocationChange(request, callback)
    offLocationChange(callback: callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationError(Callback1Argument\<LocationError>)

```cangjie
public func onLocationError(callback: Callback1Argument<LocationError>): Unit
```

**Function:** Subscribes to error information during continuous positioning. This API uses a callback to return the result asynchronously.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[LocationError](#enum-locationerror)\> | Yes | - | Callback used to receive the error information during continuous positioning. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationError} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<LocationError> {
    public func invoke(err: ?BusinessException, arg: LocationError): Unit {
        Hilog.info(0, "test", "location error: ${arg.toString()}")
    }
}

try {
    onLocationError(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationError(?Callback1Argument\<LocationError>)

```cangjie
public func offLocationError(callback!: ?Callback1Argument<LocationError> = None): Unit
```

**Function:** Unsubscribes from error information during continuous positioning. The callback passed in must be the same as the callback passed in to onLocationError. If no callback is passed in, all subscriptions of this type are canceled.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[LocationError](#enum-locationerror)\> | No | None | **Named parameter.** Callback for which the subscription is to be canceled. If this parameter is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationError} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offLocationError()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onLocationEnabledChange(Callback1Argument\<Bool>)

```cangjie
public func onLocationEnabledChange(callback: Callback1Argument<Bool>): Unit
```

**Function:** Subscribes to location service status changes. This API uses a callback to return the result asynchronously. The callback returns true if the location switch is turned on, and returns false if the location switch is turned off.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Bool\> | Yes | - | Callback used to receive the location switch status. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onLocationEnabledChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<Bool> {
    public func invoke(err: ?BusinessException, arg: Bool): Unit {
        Hilog.info(0, "test", "location enabled: ${arg}")
    }
}

try {
    onLocationEnabledChange(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offLocationEnabledChange(?Callback1Argument\<Bool>)

```cangjie
public func offLocationEnabledChange(callback!: ?Callback1Argument<Bool> = None): Unit
```

**Function:** Unsubscribes from location service status changes. The callback passed in must be the same as the callback passed in to onLocationEnabledChange. If no callback is passed in, all subscriptions of this type are canceled.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<Bool\> | No | None | **Named parameter.** Callback for which the subscription is to be canceled. If this parameter is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offLocationEnabledChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offLocationEnabledChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onSatelliteStatusChange(Callback1Argument\<SatelliteStatusInfo>)

```cangjie
public func onSatelliteStatusChange(callback: Callback1Argument<SatelliteStatusInfo>): Unit
```

**Function:** Subscribes to satellite status changes. This API uses a callback to return the result asynchronously.

**Permission Required:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[SatelliteStatusInfo](#class-satellitestatusinfo)\> | Yes | - | Callback used to receive the satellite status. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onSatelliteStatusChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class SatelliteCallback <: Callback1Argument<SatelliteStatusInfo> {
    public func invoke(err: ?BusinessException, arg: SatelliteStatusInfo): Unit {
        Hilog.info(0, "test", "satellites: ${arg.satellitesNumber}, ids: ${arg.satelliteIds.size}")
    }
}

try {
    onSatelliteStatusChange(SatelliteCallback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offSatelliteStatusChange(?Callback1Argument\<SatelliteStatusInfo>)

```cangjie
public func offSatelliteStatusChange(callback!: ?Callback1Argument<SatelliteStatusInfo> = None): Unit
```

**Function:** Unsubscribes from satellite status changes. The callback passed in must be the same as the callback passed in to onSatelliteStatusChange. If no callback is passed in, all subscriptions of this type are canceled.

**Permission Required:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[SatelliteStatusInfo](#class-satellitestatusinfo)\> | No | None | Callback to be unsubscribed. If it is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offSatelliteStatusChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offSatelliteStatusChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onNmeaMessage(Callback1Argument\<String>)

```cangjie
public func onNmeaMessage(callback: Callback1Argument<String>): Unit
```

**Function:** Subscribes to NMEA message events. This API uses a callback to return the result asynchronously.

**Permission Required:** ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<String\> | Yes | - | Callback used to receive the NMEA message. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onNmeaMessage} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class NmeaCallback <: Callback1Argument<String> {
    public func invoke(err: ?BusinessException, arg: String): Unit {
        Hilog.info(0, "test", "nmea: ${arg}")
    }
}

try {
    onNmeaMessage(NmeaCallback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offNmeaMessage(?Callback1Argument\<String>)

```cangjie
public func offNmeaMessage(callback!: ?Callback1Argument<String> = None): Unit
```

**Function:** Unsubscribes from NMEA message events. The callback passed in must be the same as the callback passed in to onNmeaMessage. If no callback is passed in, all subscriptions of this type are canceled.

**Permission Required:** ohos.permission.LOCATION and ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Gnss

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<String\> | No | None | Callback to be unsubscribed. If it is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offNmeaMessage} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offNmeaMessage()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func onCountryCodeChange(Callback1Argument\<CountryCode>)

```cangjie
public func onCountryCodeChange(callback: Callback1Argument<CountryCode>): Unit
```

**Function:** Subscribes to country code change events. This API uses a callback to return the result asynchronously.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[CountryCode](#class-countrycode)\> | Yes | - | Callback used to receive the country code information. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.onCountryCodeChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

class Callback <: Callback1Argument<CountryCode> {
    public func invoke(err: ?BusinessException, arg: CountryCode): Unit {
        Hilog.info(0, "test", "country: ${arg.country}, type: ${arg.countryCodeType.toString()}")
    }
}

try {
    onCountryCodeChange(Callback())
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func offCountryCodeChange(?Callback1Argument\<CountryCode>)

```cangjie
public func offCountryCodeChange(callback!: ?Callback1Argument<CountryCode> = None): Unit
```

**Function:** Unsubscribes from country code change events. The callback passed in must be the same as the callback passed in to onCountryCodeChange. If no callback is passed in, all subscriptions of this type are canceled.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | ?[Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argumenta)\<[CountryCode](#class-countrycode)\> | No | None | **Named parameter.** Callback for which the subscription is to be canceled. If this parameter is not specified, all subscriptions are canceled. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.offCountryCodeChange} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    offCountryCodeChange()
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func getLastLocation()

```cangjie
public func getLastLocation(): Location
```

**Function:** Obtains the last location.

**Required Permission:** ohos.permission.APPROXIMATELY_LOCATION

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Return Value:**

| Type | Description |
|:----|:----|
| [Location](#class-location) | Last location information. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission verification failed. The application does not have the permission required to call the API. |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getLastLocation} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301100 | The location switch is off. |
  | 3301200 | Failed to obtain the geographical location. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let location = getLastLocation()
    Hilog.info(0, "test", "last location: (${location.latitude}, ${location.longitude})")
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func sendCommand(LocationCommand, AsyncCallback\<Unit>)

```cangjie
public func sendCommand(command: LocationCommand, callback: AsyncCallback<Unit>): Unit
```

**Function:** Sends an extended command to the components of the location subsystem. This API uses a callback to return the result asynchronously. If the command is sent successfully, err of the callback is None; otherwise, err contains the error information.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| command | [LocationCommand](#class-locationcommand) | Yes | - | Specifies the target scenario and the command to send. |
| callback | AsyncCallback\<Unit\> | Yes | - | Callback used to return the command sending result. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.sendCommand} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let command = LocationCommand(LocationRequestScenario.Navigation, "command_1")
    let callback: AsyncCallback<Unit> = {
        err: Option<BusinessException>, data: Option<Unit> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        } else {
            Hilog.info(0, "test", "sendCommand success")
        }
    }
    sendCommand(command, callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```

## func getCountryCode(AsyncCallback\<CountryCode>)

```cangjie
public func getCountryCode(callback: AsyncCallback<CountryCode>): Unit
```

**Function:** Queries the current country code. This API uses a callback to return the result asynchronously.

**System Capability:** SystemCapability.Location.Location.Core

**Since:** 26.1.0

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | AsyncCallback\<[CountryCode](#class-countrycode)\> | Yes | - | Callback used to return the country code information. |

**Exceptions:**

- [BusinessException](../arkinterop/cj-api-business_exception.md#class-businessexception): The error codes are as follows. For details, see [Location Service Error Codes](./cj-errorcode-geo_location_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. Failed to call ${geoLocationManager.getCountryCode} due to limited device capabilities. |
  | 3301000 | The location service is unavailable. |
  | 3301500 | Failed to query the area information. |

**Example:**

```cangjie
// index.cj

import kit.LocationKit.*
import kit.CangjieKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let callback: AsyncCallback<CountryCode> = {
        err: Option<BusinessException>, data: Option<CountryCode> =>
        if (let Some(e) <- err) {
            Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
        } else if (let Some(countryCode) <- data) {
            Hilog.info(0, "test", "country: ${countryCode.country}")
        }
    }
    getCountryCode(callback)
} catch (e: BusinessException) {
    Hilog.error(0, "test", "errCode: ${e.code}, message: ${e.message}")
}
```
