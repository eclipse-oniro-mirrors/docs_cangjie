# ohos.telephony.call

This module provides call management functionalities, including making phone calls, redirecting to the dialer interface, obtaining call states, formatting phone numbers, etc.

## Importing the Module

```cangjie
import kit.TelephonyKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the first line of the sample code contains a "// index.cj" comment, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the aforementioned sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## class Call

```cangjie
public class Call {}
```

**Functionality:** A class for making phone calls, providing call management functionalities, including interfaces for making calls, redirecting to the dialer interface, obtaining call states, formatting phone numbers, etc.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

### static func formatPhoneNumber(String, NumberFormatOptions)

```cangjie
public static func formatPhoneNumber(
    phoneNumber: String,
    options!: NumberFormatOptions = NumberFormatOptions()
): String
```

**Functionality:** Formats a phone number with optional formatting parameters.

The formatted phone number will be a standard numeric string, e.g., "138 xxxx xxxx", "0755 xxxx xxxx".

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| options | [NumberFormatOptions](#class-numberformatoptions) | No | NumberFormatOptions() | **Named parameter.** Formatting parameters, such as country code. |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the formatted phone number result. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

### static func formatPhoneNumberToE164(String, String)

```cangjie
public static func formatPhoneNumberToE164(phoneNumber: String, countryCode: String): String
```

**Functionality:** Formats a phone number into E.164 representation.

The phone number to be formatted must match the provided country code. For example, a Chinese phone number requires the country code "CN"; otherwise, the formatted result will be null.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| countryCode | String | Yes | - | The country code, supporting all country codes, e.g., China (CN). |

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the phone number formatted in E.164 representation. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

### static func getCallState()

```cangjie
public static func getCallState(): CallState
```

**Functionality:** Retrieves the current call state.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [CallState](#enum-callstate) | Returns the obtained call state. |

### static func hasCall()

```cangjie
public static func hasCall(): Bool
```

**Functionality:** Determines whether a call is in progress.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the determination result. `true` indicates a call is in progress; `false` indicates no call is in progress. |

### static func hasVoiceCapability()

```cangjie
public static func hasVoiceCapability(): Bool
```

**Functionality:** Checks whether the current device supports voice call capabilities.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the determination result. `true` indicates the device supports voice calls; `false` indicates it does not. |

### static func isEmergencyPhoneNumber(String, EmergencyNumberOptions)

```cangjie
public static func isEmergencyPhoneNumber(phoneNumber: String, options!: EmergencyNumberOptions = EmergencyNumberOptions(slotId: 0)): Bool
```

**Functionality:** Determines whether the given phone number is an emergency number based on the provided parameters.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |
| options | [EmergencyNumberOptions](#class-emergencynumberoptions) | No | EmergencyNumberOptions(slotId: 0) | Phone number parameters. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the determination result. `true` indicates it is an emergency number; `false` indicates it is not. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

### static func makeCall(String)

```cangjie
public static func makeCall(phoneNumber: String): Unit
```

**Functionality:** Redirects to the dialer interface and displays the number to be dialed. Background calls require the `ohos.permission.START_ABILITIES_FROM_BACKGROUND` permission.

**System Capability:** SystemCapability.Applications.Contacts

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| phoneNumber | String | Yes | - | The phone number. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

### static func makeCall(UIAbilityContext, String)

```cangjie
public static func makeCall(context: UIAbilityContext, phoneNumber: String): Unit
```

**Functionality:** Redirects to the dialer interface and displays the number to be dialed. Background calls require the `ohos.permission.START_ABILITIES_FROM_BACKGROUND` permission.

**System Capability:** SystemCapability.Applications.Contacts

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| context | [UIAbilityContext](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-uiabilitycontext) | Yes | - | The application context Context. |
| phoneNumber | String | Yes | - | The phone number. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Mandatory parameters are left unspecified; 2. Incorrect parameter types; |
  | 8300001 | Invalid parameter value. |
  | 8300002 | Operation failed. Cannot connect to service. |
  | 8300003 | System internal error. |
  | 8300999 | Unknown error code. |

## class EmergencyNumberOptions

```cangjie
public class EmergencyNumberOptions {
    public var slotId: Int32
    public init(slotId!: Int32 = 0)
}
```

**Functionality:** Optional parameters for determining whether a phone number is an emergency number.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

### var slotId

```cangjie
public var slotId: Int32
```

**Functionality:** Represents the SIM slot ID.

**Type:** Int32

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

### init(Int32)

```cangjie
public init(slotId!: Int32 = 0)
```

**Functionality:** Constructor for EmergencyNumberOptions.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| slotId | Int32 | No | 0 | SIM slot ID: Slot 1: 0; Slot 2: 1. |

## class NumberFormatOptions

```cangjie
public class NumberFormatOptions {
    public var countryCode: String
    public init(countryCode!: String = "CN")
}
```

**Functionality:** Optional parameters for formatting phone numbers.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

### var countryCode

```cangjie
public var countryCode: String
```

**Functionality:** The country code, supporting all country codes, e.g., CN (China). Default: "CN".

**Type:** String

**Read/Write Capability:** Readable and Writable

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

### init(String)

```cangjie
public init(countryCode!: String = "CN")
```

**Functionality:** Constructor for creating a NumberFormatOptions instance.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| countryCode | String | No | "CN" | The country code, supporting all country codes, e.g., CN (China). Default: "CN". |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.TelephonyKit.*

let op = NumberFormatOptions(countryCode: "CN")
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

**Functionality:** Call state codes.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21

**Parent Types:**

- Equatable\<CallState>
- ToString

### CallStateAnswered

```cangjie
CallStateAnswered
```

**Functionality:** Indicates that an incoming call has been answered.

**System Capability:** SystemCapability.Telephony.CallManager

**Initial Version:** 21### CallStateIdle

```cangjie
CallStateIdle
```

**Function:** Indicates no ongoing call.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

### CallStateOffhook

```cangjie
CallStateOffhook
```

**Function:** Indicates at least one call is in dialing, active, or held state, with no new incoming call ringing or waiting.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

### CallStateRinging

```cangjie
CallStateRinging
```

**Function:** Indicates an incoming call is ringing or waiting.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

### CallStateUnknown

```cangjie
CallStateUnknown
```

**Function:** Invalid state, returned when call state retrieval fails.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

### func !=(CallState)

```cangjie
public operator func !=(other: CallState): Bool
```

**Function:** Determines whether two enum values are unequal.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CallState](#enum-callstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the enum values are unequal, otherwise `false`. |

### func ==(CallState)

```cangjie
public operator func ==(other: CallState): Bool
```

**Function:** Determines whether two enum values are equal.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [CallState](#enum-callstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns `true` if the enum values are equal, otherwise `false`. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Retrieves the description of the enum value.

**System Capability:** SystemCapability.Telephony.CallManager

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum value. |