# ohos.system_date_time (System Time & Timezone)

This module primarily consists of system time and timezone functionalities. Developers can set and retrieve system time and timezone information.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of a Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration must be done in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## class SystemDateTime

```cangjie
public class SystemDateTime {}
```

**Description:** Class for system time and timezone functionalities.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

### static func getTime(Bool)

```cangjie
public static func getTime(isNanoseconds!: Bool = false): Int64
```

**Description:** Gets the elapsed time since the Unix epoch.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| isNanoseconds | Bool | No | false | **Named parameter.** Whether to return the result in nanoseconds.<br>- true: Returns the result in nanoseconds (ns).<br>- false: Returns the result in milliseconds (ms). |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Elapsed time since the Unix epoch. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.base.*

try {
    let time = SystemDateTime.getTime()
    Hilog.info(0, "cangjie_ohos_test", "Succeeded in getting time : ${time}")
} catch (e: Exception) {
    Hilog.info(0, "cangjie_ohos_test", "Failed to get time: ${e.toString()}")
}
```

### static func getTimezone()

```cangjie
public static func getTimezone(): String
```

**Description:** Gets the system timezone.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the system timezone. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.base.*

try {
    let time = SystemDateTime.getTimezone()
    Hilog.info(0, "cangjie_ohos_test", "Succeeded to getTimezone, getTimezone is ${time} ")
} catch (e: Exception) {
    Hilog.info(0, "cangjie_ohos_test", "Failed to getTimezone: ${e.toString()}")
}
```

### static func getUptime(TimeType, Bool)

```cangjie
public static func getUptime(timeType: TimeType, isNanoseconds!: Bool = false): Int64
```

**Description:** Gets the elapsed time since system startup.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| timeType | [TimeType](#enum-timetype) | Yes | - | Type of time to retrieve. |
| isNanoseconds | Bool | No | false | **Named parameter.** Whether to return the result in nanoseconds.<br/>- true: Returns the result in nanoseconds (ns).<br/>- false: Returns the result in milliseconds (ms). |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Elapsed time since system startup. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import ohos.base.*

try {
    let time = SystemDateTime.getUptime(TimeType.Active)
    Hilog.info(0, "cangjie_ohos_test", "Succeeded to getUptime : ${time}")
} catch (e: Exception) {
    Hilog.info(0, "cangjie_ohos_test", "Failed to getUptime: ${e.toString()}")
}
```

## enum TimeType

```cangjie
public enum TimeType {
    | Startup
    | Active
    | ...
}
```

**Description:** Defines enumeration types for retrieving time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

### Active

```cangjie
Active
```

**Description:** Milliseconds elapsed since system startup, excluding deep sleep time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21

### Startup

```cangjie
Startup
```

**Description:** Milliseconds elapsed since system startup, including deep sleep time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 21