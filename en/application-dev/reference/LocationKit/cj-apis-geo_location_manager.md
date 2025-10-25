# ohos.geo_location_manager (Location Services)

Location services provide basic functionalities including GNSS positioning, network positioning (cellular base station, WLAN, Bluetooth positioning technologies), geocoding, reverse geocoding, country codes, and geofencing.

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

**Required Permission:** ohos.APPROXIMATELY_LOCATION

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

**Required Permission:** ohos.APPROXIMATELY_LOCATION

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

**Required Permission:** ohos.APPROXIMATELY_LOCATION

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