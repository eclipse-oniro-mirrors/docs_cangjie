# ohos.battery_info

This module primarily provides query interfaces for battery status and charging/discharging states.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code's first line contains a "// index.cj" comment, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class BatteryInfo

```cangjie
public class BatteryInfo {}
```

**Function:** Class describing battery information.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop batteryCapacityLevel

```cangjie
public static prop batteryCapacityLevel: BatteryCapacityLevel
```

**Function:** Indicates the current battery charge level of the device.

**Type:** [BatteryCapacityLevel](#enum-batterycapacitylevel)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop batterySOC

```cangjie
public static prop batterySOC: Int32
```

**Function:** Indicates the current remaining battery percentage of the device.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop batteryTemperature

```cangjie
public static prop batteryTemperature: Int32
```

**Function:** Indicates the current battery temperature of the device.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop chargingStatus

```cangjie
public static prop chargingStatus: BatteryChargeState
```

**Function:** Indicates the current charging state of the device's battery.

**Type:** [BatteryChargeState](#enum-batterychargestate)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop healthStatus

```cangjie
public static prop healthStatus: BatteryHealthState
```

**Function:** Indicates the current health status of the device's battery.

**Type:** [BatteryHealthState](#enum-batteryhealthstate)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop isBatteryPresent

```cangjie
public static prop isBatteryPresent: Bool
```

**Function:** Indicates whether the device supports a battery or if the battery is present.

**Type:** Bool

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop nowCurrent

```cangjie
public static prop nowCurrent: Int32
```

**Function:** Indicates the current battery current of the device.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop pluggedType

```cangjie
public static prop pluggedType: BatteryPluggedType
```

**Function:** Indicates the type of charger currently connected to the device.

**Type:** [BatteryPluggedType](#enum-batterypluggedtype)

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop technology

```cangjie
public static prop technology: String
```

**Function:** Indicates the current battery technology model of the device.

**Type:** String

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### static prop voltage

```cangjie
public static prop voltage: Int32
```

**Function:** Indicates the current battery voltage of the device.

**Type:** Int32

**Read/Write Capability:** Read-only

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

## enum BatteryCapacityLevel

```cangjie
public enum BatteryCapacityLevel <: Equatable<BatteryCapacityLevel> & ToString {
    | LevelFull
    | LevelHigh
    | LevelNormal
    | LevelLow
    | LevelWarning
    | LevelCritical
    | LevelShutdown
    | ...
}
```

**Function:** Represents battery charge levels.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

**Parent Types:**

- Equatable\<BatteryCapacityLevel>
- ToString

### LevelCritical

```cangjie
LevelCritical
```

**Function:** Indicates the battery charge level is critically low.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelFull

```cangjie
LevelFull
```

**Function:** Indicates the battery charge level is full.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelHigh

```cangjie
LevelHigh
```

**Function:** Indicates the battery charge level is high.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelLow

```cangjie
LevelLow
```

**Function:** Indicates the battery charge level is low.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelNormal

```cangjie
LevelNormal
```

**Function:** Indicates the battery charge level is normal.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelShutdown

```cangjie
LevelShutdown
```

**Function:** Indicates the battery charge level is at shutdown threshold.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### LevelWarning

```cangjie
LevelWarning
```

**Function:** Indicates the battery charge level is at warning threshold.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### func !=(BatteryCapacityLevel)

```cangjie
public operator func !=(other: BatteryCapacityLevel): Bool
```

**Function:** Performs inequality comparison on battery charge levels.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[BatteryCapacityLevel](#enum-batterycapacitylevel)|Yes|-|Battery charge level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery charge levels differ, otherwise false.|

### func ==(BatteryCapacityLevel)

```cangjie
public operator func ==(other: BatteryCapacityLevel): Bool
```

**Function:** Performs equality comparison on battery charge levels.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[BatteryCapacityLevel](#enum-batterycapacitylevel)|Yes|-|Battery charge level.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery charge levels are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the battery charge level.

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the battery charge level value. |

## enum BatteryChargeState

```cangjie
public enum BatteryChargeState <: Equatable<BatteryChargeState> & ToString {
    | UnknownChargeState
    | Enabled
    | Disabled
    | Full
    | ...
}
```

**Function:** Represents battery charging states.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

**Parent Types:**

- Equatable\<BatteryChargeState>
- ToString

### Disabled

```cangjie
Disabled
```

**Function:** Indicates the battery charging state is disabled.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### Enabled

```cangjie
Enabled
```

**Function:** Indicates the battery charging state is enabled.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### Full

```cangjie
Full
```

**Function:** Indicates the battery is fully charged.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### UnknownChargeState

```cangjie
UnknownChargeState
```

**Function:** Indicates the battery charging state is unknown.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Initial Version:** 21

### func !=(BatteryChargeState)

```cangjie
public operator func !=(other: BatteryChargeState): Bool
```

**Function:** Performs inequality comparison on battery charging states.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[BatteryChargeState](#enum-batterychargestate)|Yes|-|Battery charging state.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery charging states differ, otherwise false.|

### func ==(BatteryChargeState)

```cangjie
public operator func ==(other: BatteryChargeState): Bool
```

**Function:** Performs equality comparison on battery charging states.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[BatteryChargeState](#enum-batterychargestate)|Yes|-|Battery charging state.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery charging states are equal, otherwise false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the battery charging state.

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the battery charging state value. |## enum BatteryHealthState

```cangjie
public enum BatteryHealthState <: Equatable<BatteryHealthState> & ToString {
    | UnknownHealthState
    | Good
    | Overheat
    | Overvoltage
    | Cold
    | Dead
    | ...
}
```

**Description:** Represents battery health status.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

**Parent Types:**

- Equatable\<BatteryHealthState>
- ToString

### Cold

```cangjie
Cold
```

**Description:** Indicates the battery health status is in cold condition.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Dead

```cangjie
Dead
```

**Description:** Indicates the battery health status is dead.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Good

```cangjie
Good
```

**Description:** Indicates the battery health status is normal.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Overheat

```cangjie
Overheat
```

**Description:** Indicates the battery health status is overheating.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Overvoltage

```cangjie
Overvoltage
```

**Description:** Indicates the battery health status is in overvoltage condition.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### UnknownHealthState

```cangjie
UnknownHealthState
```

**Description:** Indicates the battery health status is unknown.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### func !=(BatteryHealthState)

```cangjie
public operator func !=(other: BatteryHealthState): Bool
```

**Description:** Compares battery health states for inequality.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
|other|[BatteryHealthState](#enum-batteryhealthstate)|Yes|-|Battery health status.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery health states differ, otherwise returns false. |

### func ==(BatteryHealthState)

```cangjie
public operator func ==(other: BatteryHealthState): Bool
```

**Description:** Compares battery health states for equality.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
|other|[BatteryHealthState](#enum-batteryhealthstate)|Yes|-|Battery health status.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if battery health states are identical, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of battery health status.

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the battery health status value. |

## enum BatteryPluggedType

```cangjie
public enum BatteryPluggedType <: Equatable<BatteryPluggedType> & ToString {
    | UnknownType
    | Ac
    | Usb
    | Wireless
    | ...
}
```

**Description:** Represents connected charger types.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

**Parent Types:**

- Equatable\<BatteryPluggedType>
- ToString

### Ac

```cangjie
Ac
```

**Description:** Indicates the connected charger type is AC charger.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### UnknownType

```cangjie
UnknownType
```

**Description:** Indicates the connected charger type is not obtained.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Usb

```cangjie
Usb
```

**Description:** Indicates the connected charger type is USB.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### Wireless

```cangjie
Wireless
```

**Description:** Indicates the connected charger type is wireless charger.

**System Capability:** SystemCapability.PowerManager.BatteryManager.Core

**Since:** 21

### func !=(BatteryPluggedType)

```cangjie
public operator func !=(other: BatteryPluggedType): Bool
```

**Description:** Compares charger types for inequality.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
|other|[BatteryPluggedType](#enum-batterypluggedtype)|Yes|-|Charger type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if charger types differ, otherwise returns false. |

### func ==(BatteryPluggedType)

```cangjie
public operator func ==(other: BatteryPluggedType): Bool
```

**Description:** Compares charger types for equality.

**Parameters:**

| Name | Type | Mandatory | Default | Description |
|:---|:---|:---|:---|:---|
|other|[BatteryPluggedType](#enum-batterypluggedtype)|Yes|-|Charger type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool| Returns true if charger types are identical, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of charger type information.

**Return Value:**

|Type|Description|
|:----|:----|
|String| String corresponding to the charger type value. |