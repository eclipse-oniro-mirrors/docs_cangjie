# ohos.bluetooth.base_profile (Bluetooth BaseProfile Module)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The baseProfile module provides basic Profile types and related methods.

## Import Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, configuration needs to be done in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Instructions](../cj-development-intro.md#Cangjie示例代码说明).

## interface BaseProfile

```cangjie
public interface BaseProfile {
    func getConnectedDevices(): Array<String>
    func getConnectionState(deviceId: String): ProfileConnectionState
    func on(eventType: ProfileCallbackType, callback: Callback1Argument<StateChangeParam>): Unit
    func off(eventType: ProfileCallbackType, callback: CallbackObject): Unit
    func off(eventType: ProfileCallbackType): Unit
}
```

**Description:** Basic Profile type.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func getConnectedDevices()

```cangjie
func getConnectedDevices(): Array<String>
```

**Description:** Obtains the list of connected devices.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<String> | Returns the addresses of currently connected devices. For information security considerations, the device addresses obtained here are randomized MAC addresses. This randomized address remains unchanged after successful pairing; however, it will change when previously paired devices are unpaired and rescanned or when the Bluetooth service is powered off. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let a2dpSrc = createA2dpSrcProfile()
    let retArray = a2dpSrc.getConnectedDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func getConnectionState(String)

```cangjie
func getConnectionState(deviceId: String): ProfileConnectionState
```

**Description:** Obtains the connection state of a device's Profile.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | Remote device address. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate) | Returns the connection state of the Profile. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let a2dpSrc = createA2dpSrcProfile()
    let retArray = a2dpSrc.getConnectionState("XX:XX:XX:XX:XX:XX")
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType, CallbackObject)

```cangjie
func off(eventType: ProfileCallbackType, callback: CallbackObject): Unit
```

**Description:** Unsubscribes from all connection state change events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Callback event type. |
| callback | [CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | Yes | - | Callback event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let changeCallBack = StateChangeCallback()
let a2dp = createA2dpSrcProfile()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    a2dp.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType)

```cangjie
func off(eventType: ProfileCallbackType): Unit
```

**Description:** Unsubscribes from all connection state change events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Callback event type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let changeCallBack = StateChangeCallback()
let a2dp = createA2dpSrcProfile()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    a2dp.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func on(ProfileCallbackType, Callback1Argument\<StateChangeParam>)

```cangjie
func on(eventType: ProfileCallbackType, callback: Callback1Argument<StateChangeParam>): Unit
```

**Description:** Subscribes to connection state change events. Uses Callback for asynchronous callbacks.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Pass `CONNECTIONSTATECHANGE` to indicate the connection state change event type. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callbackobject)\<[StateChangeParam](#class-statechangeparam)> | Yes | - | Represents the input parameter of the callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.CangjieKit.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let changeCallBack = StateChangeCallback()
let a2dp = createA2dpSrcProfile()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## class StateChangeParam

```cangjie
public class StateChangeParam {
    public var deviceId: String
    public var state: ProfileConnectionState
    public var cause: DisconnectCause
}
```

**Description:** Describes parameters for profile state changes.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var cause

```cangjie
public var cause: DisconnectCause
```

**Description:** Indicates the reason for connection failure.

**Type:** [DisconnectCause](#enum-disconnectcause)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Description:** Indicates the Bluetooth device address.

**Type:** String

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var state

```cangjie
public var state: ProfileConnectionState
```

**Description:** Indicates the profile connection state of the Bluetooth device.

**Type:** [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate)

**Read/Write Permission:** Readable and writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## enum DisconnectCause

```cangjie
public enum DisconnectCause <: Equatable<DisconnectCause> & ToString {
    | UserDisconnect
    | ConnectFromKeyboard
    | ConnectFromMouse
    | ConnectFromCar
    | TooManyConnectedDevices
    | ConnectFailInternal
    | ...
}
```

**Description:** Reasons for connection failure.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<DisconnectCause>
- ToString

### ConnectFailInternal

```cangjie
ConnectFailInternal
```

**Description:** Internal error.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ConnectFromCar

```cangjie
ConnectFromCar
```

**Description:** Connection should be initiated from the car side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ConnectFromKeyboard

```cangjie
ConnectFromKeyboard
```

**Description:** Connection should be initiated from the keyboard side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ConnectFromMouse

```cangjie
ConnectFromMouse
```

**Description:** Connection should be initiated from the mouse side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### TooManyConnectedDevices

```cangjie
TooManyConnectedDevices
```

**Description:** Current number of connections exceeds the limit.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### UserDisconnect

```cangjie
UserDisconnect
```

**Description:** User actively disconnects.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(DisconnectCause)

```cangjie
public operator func !=(other: DisconnectCause): Bool
```

**Description:** Determines inequality for connection failure reasons.

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [DisconnectCause](#enum-disconnectcause) | Yes | - | Connection failure reason. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the connection failure reasons are different, otherwise returns false. |

### func ==(DisconnectCause)

```cangjie
public operator func ==(other: DisconnectCause): Bool
```

**Description:** Determines equality for connection failure reasons.

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| other | [DisconnectCause](#enum-disconnectcause) | Yes | - | Connection failure reason. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Bool | Returns true if the connection failure reasons are the same, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of the connection failure reason.

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | String representation of the connection failure reason. |## enum ProfileCallbackType

```cangjie
public enum ProfileCallbackType <: Equatable<ProfileCallbackType> & Hashable & ToString {
    | ConnectionStateChange
    | ...
}
```

**Description:** Callback events for Bluetooth BaseProfile.

**SystemCapability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<ProfileCallbackType>
- Hashable
- ToString

### ConnectionStateChange

```cangjie
ConnectionStateChange
```

**Description:** Indicates the connection state change event type.

**SystemCapability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(ProfileCallbackType)

```cangjie
public operator func !=(other: ProfileCallbackType): Bool
```

**Description:** Performs inequality comparison for Bluetooth BaseProfile callback events.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ProfileCallbackType](#enum-profilecallbacktype)|Yes|-|Bluetooth BaseProfile callback event.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the Bluetooth BaseProfile callback events are different, otherwise returns false.|

### func ==(ProfileCallbackType)

```cangjie
public operator func ==(other: ProfileCallbackType): Bool
```

**Description:** Performs equality comparison for Bluetooth BaseProfile callback events.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ProfileCallbackType](#enum-profilecallbacktype)|Yes|-|Bluetooth BaseProfile callback event.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the Bluetooth BaseProfile callback events are identical, otherwise returns false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Description:** Retrieves the hash value of the callback event.

**SystemCapability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|The hash value of the callback event.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Retrieves the string representation of the callback event type.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The string representation of the callback event type.|