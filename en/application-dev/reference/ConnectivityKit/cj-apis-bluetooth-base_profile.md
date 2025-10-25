# ohos.bluetooth.base_profile (Bluetooth BaseProfile Module)

The baseProfile module provides fundamental Profile types and related methods.

## Import Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Guidelines

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample projects and configuration templates, refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

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

**Since:** 21

### func getConnectedDevices()

```cangjie
func getConnectedDevices(): Array<String>
```

**Description:** Obtains the list of connected devices.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<String> | Returns the addresses of currently connected devices. For information security considerations, the device addresses obtained here are randomized MAC addresses. This address remains unchanged after successful pairing; however, it will change when a paired device is unpaired and rescanned or when the Bluetooth service is powered off. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

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

import ohos.base.*
import ohos.business_exception.*
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

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | Remote device address. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate) | Returns the connection state of the Profile. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.business_exception.*
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

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Callback event type. |
| callback | [CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | Yes | - | Callback event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
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

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Callback event type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
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

**Description:** Subscribes to connection state change events. Uses Callback for asynchronous notification.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Pass `CONNECTIONSTATECHANGE` to indicate the connection state change event type. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callbackobject)\<[StateChangeParam](#class-statechangeparam)> | Yes | - | Represents the input parameter of the callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 401 | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.2. Incorrect parameter types. 3. Parameter verification failed. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import ohos.callback_invoke.*
import ohos.business_exception.*
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

**Description:** Describes profile state change parameters.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### var cause

```cangjie
public var cause: DisconnectCause
```

**Description:** Indicates the reason for connection failure.

**Type:** [DisconnectCause](#enum-disconnectcause)

**Access:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### var deviceId

```cangjie
public var deviceId: String
```

**Description:** Indicates the Bluetooth device address.

**Type:** String

**Access:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### var state

```cangjie
public var state: ProfileConnectionState
```

**Description:** Indicates the profile connection state of the Bluetooth device.

**Type:** [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate)

**Access:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21## enum DisconnectCause

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

**Function:** Reasons for connection failure.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

**Parent Types:**

- Equatable\<DisconnectCause>
- ToString

### ConnectFailInternal

```cangjie
ConnectFailInternal
```

**Function:** Internal error.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### ConnectFromCar

```cangjie
ConnectFromCar
```

**Function:** Connection should be initiated from the vehicle side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### ConnectFromKeyboard

```cangjie
ConnectFromKeyboard
```

**Function:** Connection should be initiated from the keyboard side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### ConnectFromMouse

```cangjie
ConnectFromMouse
```

**Function:** Connection should be initiated from the mouse side.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### TooManyConnectedDevices

```cangjie
TooManyConnectedDevices
```

**Function:** Current number of connections exceeds the limit.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### UserDisconnect

```cangjie
UserDisconnect
```

**Function:** User actively disconnected.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### func !=(DisconnectCause)

```cangjie
public operator func !=(other: DisconnectCause): Bool
```

**Function:** Determines inequality of connection failure reasons.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DisconnectCause](#enum-disconnectcause) | Yes | - | Connection failure reason. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if connection failure reasons are different, otherwise returns false. |

### func ==(DisconnectCause)

```cangjie
public operator func ==(other: DisconnectCause): Bool
```

**Function:** Determines equality of connection failure reasons.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [DisconnectCause](#enum-disconnectcause) | Yes | - | Connection failure reason. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if connection failure reasons are the same, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the connection failure reason.

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the connection failure reason. |

## enum ProfileCallbackType

```cangjie
public enum ProfileCallbackType <: Equatable<ProfileCallbackType> & Hashable & ToString {
    | ConnectionStateChange
    | ...
}
```

**Function:** Bluetooth BaseProfile callback events.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

**Parent Types:**

- Equatable\<ProfileCallbackType>
- Hashable
- ToString

### ConnectionStateChange

```cangjie
ConnectionStateChange
```

**Function:** Indicates the connection state change event type.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

### func !=(ProfileCallbackType)

```cangjie
public operator func !=(other: ProfileCallbackType): Bool
```

**Function:** Determines inequality of Bluetooth BaseProfile callback events.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Bluetooth BaseProfile callback event. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if Bluetooth BaseProfile callback events are different, otherwise returns false. |

### func ==(ProfileCallbackType)

```cangjie
public operator func ==(other: ProfileCallbackType): Bool
```

**Function:** Determines equality of Bluetooth BaseProfile callback events.

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| other | [ProfileCallbackType](#enum-profilecallbacktype) | Yes | - | Bluetooth BaseProfile callback event. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if Bluetooth BaseProfile callback events are the same, otherwise returns false. |

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Function:** Gets the hash value of the callback event.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int64 | Hash value of the callback event. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the callback event type.

**Return Value:**

| Type | Description |
|:----|:----|
| String | String representation of the callback event type. |