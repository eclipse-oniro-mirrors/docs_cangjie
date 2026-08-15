# ohos.telephony.call

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides call management functionalities, including making phone calls, redirecting to the dialer interface, obtaining call status, formatting phone numbers, etc.

## Import Module

```cangjie
import kit.TelephonyKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#仓颉示例代码说明).

## class Call

```cangjie
public class Call {}
```

**Description:** The call class provides call management functionalities, including interfaces for making phone calls, redirecting to the dialer interface, obtaining call status, formatting phone numbers, etc.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### static func formatPhoneNumber(String, NumberFormatOptions)

```cangjie
public static func formatPhoneNumber(
    phoneNumber: String,
    options!: NumberFormatOptions = NumberFormatOptions()
): String
```

**Description:** Formats a phone number with customizable formatting parameters.

The formatted phone number will be a standard numeric string, e.g., "138 xxxx xxxx", "0755 xxxx xxxx".

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| options | [NumberFormatOptions](#class-numberformatoptions) | No | NumberFormatOptions() | **Named parameter.** Formatting parameters, such as country code. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the formatted phone number result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2. Incorrect parameters types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result = Call.formatPhoneNumber("138xxxxxxxx", options: NumberFormatOptions(countryCode: "CN"))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func formatPhoneNumberToE164(String, String)

```cangjie
public static func formatPhoneNumberToE164(phoneNumber: String, countryCode: String): String
```

**Description:** Formats a phone number into E.164 representation.

The phone number to be formatted must match the provided country code. For example, a Chinese phone number requires the country code "CN"; otherwise, the formatted result will be null.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| countryCode | String | Yes | - | Country code, supporting all country codes, e.g., China (CN). |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the E.164 formatted phone number result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2. Incorrect parameters types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result = Call.formatPhoneNumberToE164("138xxxxxxxx", "CN")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func getCallState()

```cangjie
public static func getCallState(): CallState
```

**Description:** Retrieves the current call status.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [CallState](#enum-callstate) | Returns the obtained call status. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result: CallState = Call.getCallState()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func hasCall()

```cangjie
public static func hasCall(): Bool
```

**Description:** Checks whether there is an ongoing call.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the result of checking for an ongoing call. Returns true if there is an ongoing call, false otherwise. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result: Bool = Call.hasCall()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func hasVoiceCapability()

```cangjie
public static func hasVoiceCapability(): Bool
```

**Description:** Checks whether the current device has voice call capability.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the result of checking for voice call capability. Returns true if the device has voice call capability, false otherwise. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result: Bool = Call.hasVoiceCapability()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func isEmergencyPhoneNumber(String, EmergencyNumberOptions)

```cangjie
public static func isEmergencyPhoneNumber(phoneNumber: String, options!: EmergencyNumberOptions = EmergencyNumberOptions(slotId: 0)): Bool
```

**Description:** Determines whether the given phone number is an emergency number based on the provided parameters.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| options | [EmergencyNumberOptions](#class-emergencynumberoptions) | No | EmergencyNumberOptions(slotId: 0) | Phone number parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the result of checking whether the number is an emergency number. Returns true if it is an emergency number, false otherwise. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2. Incorrect parameters types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let result = Call.isEmergencyPhoneNumber("138xxxxxxxx", options: EmergencyNumberOptions(slotId: 1))
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func makeCall(String)

```cangjie
public static func makeCall(phoneNumber: String): Unit
```

**Description:** Redirects to the dialer interface and displays the number to be dialed. Background calls require the ohos.permission.START_ABILITIES_FROM_BACKGROUND permission.

**System Capability:** SystemCapability.Applications.Contacts

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2. Incorrect parameters types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    Call.makeCall("138xxxxxxxx")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func makeCall(UIAbilityContext, String)

```cangjie
public static func makeCall(context: UIAbilityContext, phoneNumber: String): Unit
```

**Description:** Redirects to the dialer interface and displays the number to be dialed. Background calls require the ohos.permission.START_ABILITIES_FROM_BACKGROUND permission.

**System Capability:** SystemCapability.Applications.Contacts

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The application context Context. |
| phoneNumber | String | Yes | - | The phone number. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1.Mandatory parameters are left unspecified; 2. Incorrect parameters types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.app.ability.ui_ability.UIAbilityContext
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    var ctx = Option<UIAbilityContext>.None

    Call.makeCall(ctx.getOrThrow(), "138xxxxxxxx")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```## class EmergencyNumberOptions

```cangjie
public class EmergencyNumberOptions {
    public var slotId: Int32
    public init(slotId!: Int32 = 0)
}
```

**Function:** Optional parameters for determining emergency phone numbers.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### var slotId

```cangjie
public var slotId: Int32
```

**Function:** Represents the SIM slot ID.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### init(Int32)

```cangjie
public init(slotId!: Int32 = 0)
```

**Function:** Constructor for EmergencyNumberOptions.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| slotId | Int32 | No | 0 | SIM slot ID: Slot 1: 0, Slot 2: 1. |

## class NumberFormatOptions

```cangjie
public class NumberFormatOptions {
    public var countryCode: String
    public init(countryCode!: String = "CN")
}
```

**Function:** Optional parameters for formatting phone numbers.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### var countryCode

```cangjie
public var countryCode: String
```

**Function:** Country code, supporting all country codes such as "CN" (China). Default is "CN".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### init(String)

```cangjie
public init(countryCode!: String = "CN")
```

**Function:** Constructor for creating a NumberFormatOptions instance.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| countryCode | String | No | "CN" | Country code, supporting all country codes such as "CN" (China). Default is "CN". |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.TelephonyKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let op = NumberFormatOptions(countryCode: "CN")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## enum CallState

```cangjie
public enum CallState <: Equatable<CallState> & ToString {
    | CallStateUnknown
    | CallStateIdle
    | CallStateRinging
    | CallStateOffhook
    | CallStateAnswered
    | ...
}
```

**Function:** Call state codes.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parent Types:**

- Equatable\<CallState>
- ToString

### CallStateAnswered

```cangjie
CallStateAnswered
```

**Function:** Indicates an incoming call has been answered.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### CallStateIdle

```cangjie
CallStateIdle
```

**Function:** Indicates no active calls.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### CallStateOffhook

```cangjie
CallStateOffhook
```

**Function:** Indicates at least one call is in dialing, active, or hold state, with no new incoming calls ringing or waiting.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### CallStateRinging

```cangjie
CallStateRinging
```

**Function:** Indicates an incoming call is ringing or waiting.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### CallStateUnknown

```cangjie
CallStateUnknown
```

**Function:** Invalid state, returned when call state retrieval fails.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

### func !=(CallState)

```cangjie
public operator func !=(other: CallState): Bool
```

**Function:** Determines if two enum values are not equal.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CallState](#enum-callstate) | Yes | - | Another enum value. |

**Returns:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are not equal, otherwise false. |

### func ==(CallState)

```cangjie
public operator func ==(other: CallState): Bool
```

**Function:** Determines if two enum values are equal.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CallState](#enum-callstate) | Yes | - | Another enum value. |

**Returns:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the enum values are equal, otherwise false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 22

**Returns:**

| Type | Description |
|:----|:----|
| String | Description of the enum value. |