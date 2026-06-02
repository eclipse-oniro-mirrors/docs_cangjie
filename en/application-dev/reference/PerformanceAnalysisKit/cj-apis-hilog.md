# ohos.hilog (HiLog Printing)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The hilog logging system enables applications/services to output log content with specified levels, tags, and format strings, helping developers understand the operational status of applications/services and debug programs more effectively.

## Import Module

```cangjie
import kit.PerformanceAnalysisKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the above sample project and configuration template, refer to [Cangjie Sample Code Description](../cj-development-intro.md#仓颉示例代码说明).

## class Hilog

```cangjie
public class Hilog {}
```

**Description:** The logging system object that enables applications/services to output log content with specified levels, tags, and format strings. Provides logging methods for different levels: DEBUG, INFO, WARNING, ERROR, and FATAL.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### static func debug(UInt32, String, String, Array\<String>)

```cangjie
public static func debug(domain: UInt32, tag: String, format: String, args: Array<String>): Unit
```

**Description:** Prints DEBUG-level logs.

DEBUG-level logs are not printed by default in official release versions. They are only printed in debug versions or when the debug switch is enabled.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| format | String | Yes | - | The format string for log output. |
| args | Array\<String> | No | - | Arguments for the format string. |

**Example 1:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.debug(0, "testTag", "Debug: Hello world!")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

**Example 2:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.debug(0, "testTag", "Debug: Hello %{public}! %{private}", "world", "123")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func error(UInt32, String, String, Array<String>)

```cangjie
public static func error(domain: UInt32, tag: String, format: String, args: Array<String>): Unit
```

**Description:** Prints ERROR-level logs.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| format | String | Yes | - | The format string for log output. |
| args | Array\<String> | No | - | Arguments for the format string. |

**Example 1:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.error(0, "testTag", "Error: Hello world!")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

**Example 2:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.error(0, "testTag", "Error: Hello %{public}! %{private}", "world", "123")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func fatal(UInt32, String, String, Array<String>)

```cangjie
public static func fatal(domain: UInt32, tag: String, format: String, args: Array<String>): Unit
```

**Description:** Prints FATAL-level logs.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| format | String | Yes | - | The format string for log output. |
| args | Array\<String> | No | - | Arguments for the format string. |

**Example 1:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.fatal(0, "testTag", "Fatal: Hello world!")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

**Example 2:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.fatal(0, "testTag", "Fatal: Hello %{public}! %{private}", "world", "123")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func info(UInt32, String, String, Array<String>)

```cangjie
public static func info(domain: UInt32, tag: String, format: String, args: Array<String>): Unit
```

**Description:** Prints INFO-level logs.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| format | String | Yes | - | The format string for log output. |
| args | Array\<String> | No | - | Arguments for the format string. |

**Example 1:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.info(0, "testTag", "Info: Hello world!")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

**Example 2:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.info(0, "testTag", "Info: Hello %{public}! %{private}", "world", "123")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func isLoggable(UInt32, String, LogLevel)

```cangjie
public static func isLoggable(domain: UInt32, tag: String, level: LogLevel): Bool
```

**Description:** Calls this interface before printing logs to check whether logs with the specified domain identifier, tag, and level can be printed.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| level | [LogLevel](#enum-loglevel) | Yes | - | The log level. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if logs with the specified domain identifier, tag, and level can be printed; otherwise, returns `false`. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.isLoggable(0, "testTag", LogLevel.Debug)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func warn(UInt32, String, String, Array\<String>)

```cangjie
public static func warn(domain: UInt32, tag: String, format: String, args: Array<String>): Unit
```

**Description:** Prints WARN-level logs.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| domain | UInt32 | Yes | - | The domain identifier for the log, ranging from 0x0 to 0xFFFF.<br/>Developers are advised to customize the division as needed within the application. |
| tag | String | Yes | - | The log tag, which can be any string. It is recommended to identify the calling class or business behavior. |
| format | String | Yes | - | The format string for log output. |
| args | Array\<String> | No | - | Arguments for the format string. |

**Example 1:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.warn(0, "testTag", "Warn: Hello world!")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

**Example 2:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    Hilog.warn(0, "testTag", "Warn: Hello %{public}! %{private}", "world", "123")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum LogLevel

```cangjie
public enum LogLevel {
    | Debug
    | Info
    | Warning
    | Error
    | Fatal
    | ...
}
```

**Description:** Log levels.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### Debug

```cangjie
Debug
```

**Description:** Detailed process records. DEBUG-level logs allow for more detailed analysis of business processes and problem localization.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### Error

```cangjie
Error
```

**Description:** Indicates that an error has occurred in the application, affecting normal functionality or user experience. The error can be recovered but at a high cost, such as data reset.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### Fatal

```cangjie
Fatal
```

**Description:** Indicates a critical fatal exception, meaning the application is about to crash and the failure cannot be recovered.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### Info

```cangjie
Info
```

**Description:** Used to record key business process nodes, enabling the reconstruction of the main operational flow of the business.

Also used to record expected abnormal situations, such as no network signal or login failure.

These logs should be recorded by the dominant module within the business to avoid duplicate logging in multiple called modules or low-level functions.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22

### Warning

```cangjie
Warning
```

**Description:** Used to record relatively severe unexpected situations that have minimal impact on users. The application can recover automatically or through simple operations.

**System Capability:** SystemCapability.HiviewDFX.HiLog

**Since:** 22
