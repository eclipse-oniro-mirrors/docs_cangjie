# ohos.system_date_time (System Time and Timezone)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module primarily consists of system time and timezone functionalities. Developers can set and retrieve the system time and timezone.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code begins with a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the aforementioned sample project and configuration template, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## class SystemDateTime

```cangjie
public class SystemDateTime {}
```

**Functionality:** System time and timezone functionality class.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

### static func getTime(Bool)

```cangjie
public static func getTime(isNanoseconds!: Bool = false): Int64
```

**Functionality:** Gets the elapsed time since the Unix epoch.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| isNanoseconds | Bool | No | false | **Named parameter.** Whether the result is in nanoseconds.<br>- true: Indicates the result is in nanoseconds (ns). <br>- false: Indicates the result is in milliseconds (ms). |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The elapsed time since the Unix epoch. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let time = SystemDateTime.getTime()
    Hilog.info(0, "cangjie_ohos_test", "Succeeded in getting time : ${time}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getTimezone()

```cangjie
public static func getTimezone(): String
```

**Functionality:** Gets the system timezone.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the system timezone. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let time = SystemDateTime.getTimezone()
    Hilog.info(0, "cangjie_ohos_test", "Succeeded to getTimezone, getTimezone is ${time} ")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getUptime(TimeType, Bool)

```cangjie
public static func getUptime(timeType: TimeType, isNanoseconds!: Bool = false): Int64
```

**Functionality:** Gets the elapsed time since system startup.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| timeType | [TimeType](#enum-timetype) | Yes | - | The type of time to retrieve. |
| isNanoseconds | Bool | No | false | **Named parameter.** Whether the result is in nanoseconds.<br/>- true: Indicates the result is in nanoseconds (ns). <br/>- false: Indicates the result is in milliseconds (ms). |

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | The elapsed time since system startup. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.BasicServicesKit.*
import kit.CangjieKit.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let time = SystemDateTime.getUptime(TimeType.Active)
    Hilog.info(0, "cangjie_ohos_test", "Succeeded to getUptime : ${time}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
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

**Functionality:** Defines the enumeration type for retrieving time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

### Active

```cangjie
Active
```

**Functionality:** The elapsed time in milliseconds since system startup, excluding deep sleep time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22

### Startup

```cangjie
Startup
```

**Functionality:** The elapsed time in milliseconds since system startup, including deep sleep time.

**System Capability:** SystemCapability.MiscServices.Time

**Since:** 22