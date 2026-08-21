# ohos.settings (Setting Data Item Names)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides the capability to access setting data items.

## Import Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code has a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

## func getValue\<T>(UIAbilityContext, T, String) where T \<: ToString

```cangjie
public func getValue<T>(context: UIAbilityContext, name: T, defValue: String): String where T <: ToString
```

**Function:** Gets the value of a data item.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | T | Yes | - | Type T must implement the ToString interface. The name of the data item. Data item names fall into the following two categories:<br>- Any existing data item in the above databases.<br>- Data items added by developers themselves. |
| defValue | String | Yes | - | Default value. Set by the developer, returned when the data is not found in the database. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the value of the data item. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | Context initialization failed | Restart the application |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let value = getValue(context, Date.DateFormat, "MM/dd/yyyy")
    Hilog.info(0, "cangjie_ohos_test", "Succeeded in getting date format: ${value}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func getValue\<T, P>(UIAbilityContext, T, String, P) where T \<: ToStringP \<: ToString

```cangjie
public func getValue<T, P>(context: UIAbilityContext, name: T, defValue: String, domainName: P): String where T <: ToString,
    P <: ToString
```

**Function:** Gets the value of a data item.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | T | Yes | - | Type T must implement the ToString interface. The name of the data item. Data item names fall into the following two categories:<br>- Any existing data item in the above databases.<br>- Data items added by developers themselves. |
| defValue | String | Yes | - | Default value. Set by the developer, returned when the data is not found in the database. |
| domainName | P | Yes | - | Type P must implement the ToString interface. Specifies the domain to set:<br> - domainName is DomainName.DEVICE_SHARED,<br>&nbsp;&nbsp;&nbsp;indicating the device property shared domain.<br>- domainName is DomainName.USER_PROPRERTY,<br>&nbsp;&nbsp;&nbsp;indicating the user property domain. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the value of the data item. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | Context initialization failed | Restart the application |

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let value = getValue(context, Display.ScreenBrightnessStatus, "100", DomainName.DeviceShared)
    Hilog.info(0, "cangjie_ohos_test", "Succeeded in getting screen brightness: ${value}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum Date

```cangjie
public enum Date <: ToString {
    | DateFormat
    | TimeFormat
    | AutoGainTime
    | AutoGainTimeZone
    | ...
}
```

**Function:** Provides data items for setting time and date formats.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Parent Type:**

- ToString

### AutoGainTime

```cangjie
AutoGainTime
```

**Function:** Whether to automatically obtain date, time, and time zone from the network. A value of true means automatic retrieval; false means no automatic retrieval.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let autoGainTime = getValue(context, Date.AutoGainTime, "false")
    Hilog.info(0, "cangjie_ohos_test", "Auto gain time setting: ${autoGainTime}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### AutoGainTimeZone

```cangjie
AutoGainTimeZone
```

**Function:** Whether to automatically obtain the time zone from NITZ. A value of true means automatic retrieval; false means no automatic retrieval.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let autoGainTimeZone = getValue(context, Date.AutoGainTimeZone, "false")
    Hilog.info(0, "cangjie_ohos_test", "Auto gain time zone setting: ${autoGainTimeZone}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### DateFormat

```cangjie
DateFormat
```

**Function:** Date format. Date formats include MM/dd/yyyy, dd/MM/yyyy, and yyyy/MM/dd, where MM, dd, and yyyy represent month, day, and year, respectively.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let dateFormat = getValue(context, Date.DateFormat, "MM/dd/yyyy")
    Hilog.info(0, "cangjie_ohos_test", "Date format setting: ${dateFormat}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### TimeFormat

```cangjie
TimeFormat
```

**Function:** Whether time is displayed in 12-hour or 24-hour format. A value of "12" means 12-hour format; "24" means 24-hour format.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let timeFormat = getValue(context, Date.TimeFormat, "24")
    Hilog.info(0, "cangjie_ohos_test", "Time format setting: ${timeFormat}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the data item for setting time and date formats.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Data item for setting time and date formats. |

## enum Display

```cangjie
public enum Display <: ToString {
    | FontScale
    | ScreenBrightnessStatus
    | AutoScreenBrightness
    | ScreenOffTimeout
    | AutoScreenBrightnessMode
    | ManualScreenBrightnessMode
    | ...
}
```

**Function:** Provides data items for setting display effects.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Parent Type:**

- ToString

### AutoScreenBrightness

```cangjie
AutoScreenBrightness
```

**Function:** When auto-rotation is enabled, this property is invalid; when auto-rotation is disabled, the following values are available: 0 means screen rotation of 0 degrees; 1 means 90 degrees; 2 means 180 degrees; 3 means 270 degrees.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let autoBrightness = getValue(context, Display.AutoScreenBrightness, "0")
    Hilog.info(0, "cangjie_ohos_test", "Auto screen brightness setting: ${autoBrightness}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### FontScale

```cangjie
FontScale
```

**Function:** The scaling factor for fonts, a floating-point value.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let fontScale = getValue(context, Display.FontScale, "1.0")
    Hilog.info(0, "cangjie_ohos_test", "Font scale setting: ${fontScale}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### ScreenBrightnessStatus

```cangjie
ScreenBrightnessStatus
```

**Function:** Screen brightness. The value ranges from 0 to 255.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let brightness = getValue(context, Display.ScreenBrightnessStatus, "128")
    Hilog.info(0, "cangjie_ohos_test", "Screen brightness setting: ${brightness}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### ScreenOffTimeout

```cangjie
ScreenOffTimeout
```

**Function:** The waiting time (in milliseconds) for the device to enter sleep mode after inactivity.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let timeout = getValue(context, Display.ScreenOffTimeout, "30000")
    Hilog.info(0, "cangjie_ohos_test", "Screen off timeout setting: ${timeout} ms")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### AutoScreenBrightnessMode

```cangjie
AutoScreenBrightnessMode
```

**Function:** The value of AutoScreenBrightness when automatic screen brightness adjustment is used.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let autoBrightness = getValue(context, Display.AutoScreenBrightness, Display.ManualScreenBrightnessMode.toString())
    if (autoBrightness == Display.AutoScreenBrightnessMode.toString()) {
        Hilog.info(0, "cangjie_ohos_test", "Current mode is auto screen brightness")
    } else {
        Hilog.info(0, "cangjie_ohos_test", "Current mode is manual screen brightness")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### ManualScreenBrightnessMode

```cangjie
ManualScreenBrightnessMode
```

**Function:** The value of AutoScreenBrightness when manual screen brightness adjustment is used.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let autoBrightness = getValue(context, Display.AutoScreenBrightness, Display.AutoScreenBrightnessMode.toString())
    if (autoBrightness == Display.ManualScreenBrightnessMode.toString()) {
        Hilog.info(0, "cangjie_ohos_test", "Current mode is manual screen brightness")
    } else {
        Hilog.info(0, "cangjie_ohos_test", "Current mode is auto screen brightness")
    }
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the data item for setting display effects.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Data item for setting display effects. |## enum DomainName

```cangjie
public enum DomainName <: ToString {
    | DeviceShared
    | UserProperty
    | ...
}
```

**Function:** Provides query domain names.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Parent Type:**

- ToString

### DeviceShared

```cangjie
DeviceShared
```

**Function:** Device property shared domain.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let value = getValue(context, Display.ScreenBrightnessStatus, "100", DomainName.DeviceShared)
    Hilog.info(0, "cangjie_ohos_test", "Device shared screen brightness: ${value}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### UserProperty

```cangjie
UserProperty
```

**Function:** User property domain.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// main_ability.cj

import kit.BasicServicesKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let context = Global.getAbilityContext()
    let value = getValue(context, Display.ScreenBrightnessStatus, "100", DomainName.UserProperty)
    Hilog.info(0, "cangjie_ohos_test", "User property screen brightness: ${value}")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the string corresponding to the query domain name.

**System Capability:** SystemCapability.Applications.Settings.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|String|String corresponding to the query domain name.|
```