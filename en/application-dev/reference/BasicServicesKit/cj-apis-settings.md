# ohos.settings (Setting Data Item Names)

This module provides the capability to access setting data items.

## Importing the Module

```cangjie
import kit.BasicServicesKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

## func getValue\<T>(UIAbilityContext, T, String) where T \<: ToString

```cangjie
public func getValue<T>(context: UIAbilityContext, name: T, defValue: String): String where T <: ToString
```

**Function:** Gets the value of a data item.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | T | Yes | - | Type T must implement the ToString interface. The name of the data item. Data item names fall into the following two categories: <br>- Any existing data item in the above databases. <br>- Data items added by developers themselves. |
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

## func getValue\<T, P>(UIAbilityContext, T, String, P) where T \<: ToStringP \<: ToString

```cangjie
public func getValue<T, P>(context: UIAbilityContext, name: T, defValue: String, domainName: P): String where T <: ToString,
    P <: ToString
```

**Function:** Gets the value of a data item.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | Application context. |
| name | T | Yes | - | Type T must implement the ToString interface. The name of the data item. Data item names fall into the following two categories: <br>- Any existing data item in the above databases. <br>- Data items added by developers themselves. |
| defValue | String | Yes | - | Default value. Set by the developer, returned when the data is not found in the database. |
| domainName | P | Yes | - | Type P must implement the ToString interface. Specifies the domain name to set: <br> - domainName as DomainName.DEVICE_SHARED, <br>&nbsp;&nbsp;&nbsp;indicates the device property shared domain. <br>- domainName as DomainName.USER_PROPRERTY, <br>&nbsp;&nbsp;&nbsp;indicates the user property domain. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the value of the data item. |

**Exceptions:**

- IllegalArgumentException:

  | Error Message | Possible Cause | Handling Steps |
  | :---- | :--- | :--- |
  | The context is invalid. | Context initialization failed | Restart the application |

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

**Initial Version:** 21

**Parent Type:**

- ToString

### AutoGainTime

```cangjie
AutoGainTime
```

**Function:** Whether to automatically obtain the date, time, and time zone from the network. A value of true means automatic retrieval; false means no automatic retrieval.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### AutoGainTimeZone

```cangjie
AutoGainTimeZone
```

**Function:** Whether to automatically obtain the time zone from NITZ. A value of true means automatic retrieval; false means no automatic retrieval.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### DateFormat

```cangjie
DateFormat
```

**Function:** Date format. Date formats include MM/dd/yyyy, dd/MM/yyyy, and yyyy/MM/dd, where MM, dd, and yyyy represent month, day, and year, respectively.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### TimeFormat

```cangjie
TimeFormat
```

**Function:** Whether time is displayed in 12-hour or 24-hour format. A value of "12" indicates 12-hour format; "24" indicates 24-hour format.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the data item for setting time and date formats.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The data item for setting time and date formats. |

## enum Display

```cangjie
public enum Display <: ToString {
    | FontScale
    | ScreenBrightnessStatus
    | AutoScreenBrightness
    | ScreenOffTimeout
    | DefaultScreenRotation
    | AnimatorDurationScale
    | TransitionAnimationScale
    | WindowAnimationScale
    | DisplayInversionStatus
    | ...
}
```

**Function:** Provides data items for setting display effects.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Parent Type:**

- ToString

### AnimatorDurationScale

```cangjie
AnimatorDurationScale
```

**Function:** The scaling factor for animation duration. This affects the start delay and duration of all such animations. A value of 0 means the animation ends immediately; the default value is 1.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### AutoScreenBrightness

```cangjie
AutoScreenBrightness
```

**Function:** When auto-rotation is enabled, this property is invalid. When auto-rotation is disabled, the following values are available: 0 means screen rotation of 0 degrees; 1 means 90 degrees; 2 means 180 degrees; 3 means 270 degrees.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### DefaultScreenRotation

```cangjie
DefaultScreenRotation
```

**Function:** When auto-rotation is enabled, this property is invalid. When auto-rotation is disabled, the following values are available: 0 means screen rotation of 0 degrees; 1 means 90 degrees; 2 means 180 degrees; 3 means 270 degrees.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### DisplayInversionStatus

```cangjie
DisplayInversionStatus
```

**Function:** Whether to enable display color inversion. A value of 1 means enabled; 0 means disabled.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### FontScale

```cangjie
FontScale
```

**Function:** The scaling factor for fonts, a floating-point value.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### ScreenBrightnessStatus

```cangjie
ScreenBrightnessStatus
```

**Function:** Screen brightness. The value ranges from 0 to 255.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### ScreenOffTimeout

```cangjie
ScreenOffTimeout
```

**Function:** The waiting time (in milliseconds) for the device to enter sleep mode after inactivity.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### TransitionAnimationScale

```cangjie
TransitionAnimationScale
```

**Function:** The scaling factor for transition animations. A value of 0 disables transition animations.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### WindowAnimationScale

```cangjie
WindowAnimationScale
```

**Function:** The scaling factor for window animations. A value of 0 disables window animations.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the data item for setting display effects.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The data item for setting display effects. |

## enum DomainName

```cangjie
public enum DomainName <: ToString {
    | DeviceShared
    | UserProperty
    | ...
}
```

**Function:** Provides domain names for queries.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Parent Type:**

- ToString

### DeviceShared

```cangjie
DeviceShared
```

**Function:** Device property shared domain.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### UserProperty

```cangjie
UserProperty
```

**Function:** User property domain.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

### func toString()

```cangjie
public override func toString(): String
```

**Function:** Returns the string corresponding to the query domain name.

**System Capability:** SystemCapability.Applications.Settings.Core

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The string corresponding to the query domain name. |