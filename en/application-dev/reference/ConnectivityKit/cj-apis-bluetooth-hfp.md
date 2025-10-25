# ohos.bluetooth.hfp (Bluetooth HFP Module)

The hfp module provides methods to access Bluetooth call interfaces.

## Importing the Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template mentioned above, refer to [Cangjie Sample Code Description](../cj-development-intro.md#仓颉示例代码说明).

## func createHfpAgProfile()

```cangjie
public func createHfpAgProfile(): HandsFreeAudioGatewayProfile
```

**Function:** Creates an hfp profile instance.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| [HandsFreeAudioGatewayProfile](#class-handsfreeaudiogatewayprofile) | Returns an instance of this profile. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let hdfProfile = createHfpAgProfile()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## class HandsFreeAudioGatewayProfile

```cangjie
public class HandsFreeAudioGatewayProfile <: BaseProfile {}
```

**Function:** Before using HandsFreeAudioGatewayProfile methods, you need to create an instance of this class for operations. Construct this instance via the createHfpAgProfile() method.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parent Type:**

- [BaseProfile](cj-apis-bluetooth-base_profile.md#interface-baseprofile)

### func getConnectedDevices()

```cangjie
public func getConnectedDevices(): Array<String>
```

**Function:** Gets the list of connected devices.

**Required Permission:** ohos.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parent Type:**

- [BaseProfile](cj-apis-bluetooth-base_profile.md#interface-baseprofile)

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<String> | Returns the addresses of currently connected devices. For information security considerations, the device addresses obtained here are randomized MAC addresses. This address remains unchanged after successful pairing; however, it will change when a paired device is unpaired and rescanned or when the Bluetooth service is powered off. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

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
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let hdfProfile = createHfpAgProfile()
    let retArray = hdfProfile.getConnectedDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func getConnectionState(String)

```cangjie
public func getConnectionState(deviceId: String): ProfileConnectionState
```

**Function:** Gets the connection state of a device profile.

**Required Permission:** ohos.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | Remote device address. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate) | Returns the connection state of the profile. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900004 | Profile not supported. |
  | 2900099 | Operation failed. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.<br>2. Incorrect parameter types. 3. Parameter verification failed. | Input parameter error. | Modify the input parameters. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.base.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let hdfProfile = createHfpAgProfile()
    let ret = hdfProfile.getConnectionState("XX:XX:XX:XX:XX:XX")  // Replace with your deviceId.
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType, CallbackObject)

```cangjie
public func off(eventType: ProfileCallbackType, callback: CallbackObject): Unit
```

**Function:** Unsubscribes from connection state change events.

**Required Permission:** ohos.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](./cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Callback event type. |
| callback | [CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | Yes | - | Callback event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.<br>2. Incorrect parameter types. 3. Parameter verification failed. | Input parameter error. | Modify the input parameters. |

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
let hdfProfile = createHfpAgProfile()
try {
    hdfProfile.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    hdfProfile.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType)

```cangjie
public func off(eventType: ProfileCallbackType): Unit
```

**Function:** Unsubscribes from connection state change events.

**Required Permission:** ohos.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](./cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Callback event type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.<br>2. Incorrect parameter types. 3. Parameter verification failed. | Input parameter error. | Modify the input parameters. |

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
let hdfProfile = createHfpAgProfile()
try {
    hdfProfile.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    hdfProfile.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func on(ProfileCallbackType, Callback1Argument\<StateChangeParam>)

```cangjie
public func on(eventType: ProfileCallbackType, callback: Callback1Argument<StateChangeParam>): Unit
```

**Function:** Subscribes to connection state change events. Uses Callback for asynchronous callbacks.

**Required Permission:** ohos.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](./cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Set to CONNECTIONSTATECHANGE, indicating the connection state change event type. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[StateChangeParam](cj-apis-bluetooth-base_profile.md#class-statechangeparam)> | Yes | - | Represents the input parameters of the callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

- IllegalArgumentException:

  | Error Message | Possible Causes | Handling Steps |
  | :---- | :--- | :--- |
  | Invalid parameter. Possible causes: 1. Mandatory parameters are left unspecified.<br>2. Incorrect parameter types. 3. Parameter verification failed. | Input parameter error. | Modify the input parameters. |

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
let hdfProfile = createHfpAgProfile()
try {
    hdfProfile.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```