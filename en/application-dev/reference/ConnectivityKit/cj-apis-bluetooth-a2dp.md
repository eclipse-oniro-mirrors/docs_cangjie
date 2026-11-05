# ohos.bluetooth.a2dp (Bluetooth A2DP Module)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The a2dp module provides methods to access Bluetooth audio interfaces.

## Importing the Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For the above sample project and configuration template, see [Cangjie Sample Code Instructions](../cj-development-intro.md#cangjie-sample-code-instructions).

## func createA2dpSrcProfile()

```cangjie
public func createA2dpSrcProfile(): A2dpSourceProfile
```

**Function:** Creates an A2DP profile instance.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| [A2dpSourceProfile](#class-a2dpsourceprofile) | Returns an instance of this profile. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

try {
    let a2dpProfile = createA2dpSrcProfile()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

## class A2dpSourceProfile

```cangjie
public class A2dpSourceProfile <: BaseProfile {}
```

**Function:** Before using A2dpSourceProfile methods, you need to create an instance of this class for operations. Construct this instance via the [createA2dpSrcProfile()](#func-createa2dpsrcprofile) method.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parent Type:**

- [BaseProfile](cj-apis-bluetooth-base_profile.md#interface-baseprofile)

### func getConnectedDevices()

```cangjie
public func getConnectedDevices(): Array<String>
```

**Function:** Gets the list of connected devices.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<String> | Returns the addresses of currently connected devices. For security considerations, the device address obtained here is a randomized MAC address. This address remains unchanged after successful pairing. If a paired device is unpaired and rescanned or when the Bluetooth service is powered off, this randomized address will change. |

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

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

try {
    let a2dpSrc = createA2dpSrcProfile()
    let retArray = a2dpSrc.getConnectedDevices()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func getConnectionState(String)

```cangjie
public func getConnectionState(deviceId: String): ProfileConnectionState
```

**Function:** Gets the connection state of a device profile.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | Remote device address. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate) | Returns the connection state of the profile. |

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

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

try {
    let a2dpSrc = createA2dpSrcProfile()
    let retArray = a2dpSrc.getConnectionState("XX:XX:XX:XX:XX:XX")
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func getPlayingState(String)

```cangjie
public func getPlayingState(deviceId: String): PlayingState
```

**Function:** Gets the playback state of a device.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | Remote device address. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| [PlayingState](#enum-playingstate) | Playback state of the remote device. |

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

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

try {
    let a2dpSrc = createA2dpSrcProfile()
    let state = a2dpSrc.getPlayingState("XX:XX:XX:XX:XX:XX")
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType, CallbackObject)

```cangjie
public func off(eventType: ProfileCallbackType, callback: CallbackObject): Unit
```

**Function:** Unsubscribes from all connection state change events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Callback event type. |
| callback | [CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | Yes | - | Callback event. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let a2dp = createA2dpSrcProfile()
let changeCallBack = StateChangeCallback()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    a2dp.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func off(ProfileCallbackType)

```cangjie
public func off(eventType: ProfileCallbackType): Unit
```

**Function:** Unsubscribes from all connection state change events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Callback event type. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let a2dp = createA2dpSrcProfile()
let changeCallBack = StateChangeCallback()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    a2dp.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```

### func on(ProfileCallbackType, Callback1Argument\<StateChangeParam>)

```cangjie
public func on(eventType: ProfileCallbackType, callback: Callback1Argument<StateChangeParam>): Unit
```

**Function:** Subscribes to connection state change events. Uses Callback for asynchronous callbacks.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [ProfileCallbackType](cj-apis-bluetooth-base_profile.md#enum-profilecallbacktype) | Yes | - | Pass [CONNECTION_STATE_CHANGE](./cj-apis-bluetooth-base_profile.md#connectionstatechange) to indicate the connection state change event type. |
| callback | Callback1Argument\<[StateChangeParam](cj-apis-bluetooth-base_profile.md#class-statechangeparam)> | Yes | - | Represents the input parameter of the callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import kit.CangjieKit.*

// Define required dependencies here
class StateChangeCallback <: Callback1Argument<StateChangeParam> {
    public func invoke(err: ?BusinessException, arg: StateChangeParam): Unit {
        let connectionState = arg.state.toString()
        Hilog.info(0, "Bluetooth", "profile connection state has change to ${connectionState}")
    }
}

let a2dp = createA2dpSrcProfile()
let changeCallBack = StateChangeCallback()
try {
    a2dp.on(ProfileCallbackType.ConnectionStateChange, changeCallBack)
    a2dp.off(ProfileCallbackType.ConnectionStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}")
}
```## class CodecInfo

```cangjie
public class CodecInfo {
    public var codecType: CodecType
    public var codecBitsPerSample: CodecBitsPerSample
    public var codecChannelMode: CodecChannelMode
    public var codecSampleRate: CodecSampleRate
}
```

**Description:** Codec information.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var codecBitsPerSample

```cangjie
public var codecBitsPerSample: CodecBitsPerSample
```

**Description:** Represents the number of bits per sample, with an initial value of CODEC_BITS_PER_SAMPLE_NONE.

**Type:** [CodecBitsPerSample](#enum-codecbitspersample)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var codecChannelMode

```cangjie
public var codecChannelMode: CodecChannelMode
```

**Description:** Represents the channel mode of the codec, with an initial value of CODEC_CHANNEL_MODE_NONE.

**Type:** [CodecChannelMode](#enum-codecchannelmode)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var codecSampleRate

```cangjie
public var codecSampleRate: CodecSampleRate
```

**Description:** Represents the sample rate of the codec, with an initial value of CODEC_BITS_PER_SAMPLE_NONE.

**Type:** [CodecSampleRate](#enum-codecsamplerate)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var codecType

```cangjie
public var codecType: CodecType
```

**Description:** Represents the codec type, with an initial value of CODEC_TYPE_SBC.

**Type:** [CodecType](#enum-codectype)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## enum CodecBitsPerSample

```cangjie
public enum CodecBitsPerSample <: Equatable<CodecBitsPerSample> & ToString {
    | CodecBitsPerSampleNone
    | CodecBitsPerSample16
    | CodecBitsPerSample24
    | CodecBitsPerSample32
    | ...
}
```

**Description:** Number of bits per sample for Bluetooth codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<CodecBitsPerSample>
- ToString

### CodecBitsPerSample16

```cangjie
CodecBitsPerSample16
```

**Description:** 16 bits per sample.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecBitsPerSample24

```cangjie
CodecBitsPerSample24
```

**Description:** 24 bits per sample.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecBitsPerSample32

```cangjie
CodecBitsPerSample32
```

**Description:** 32 bits per sample.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecBitsPerSampleNone

```cangjie
CodecBitsPerSampleNone
```

**Description:** Unknown bits per sample.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(CodecBitsPerSample)

```cangjie
public operator func !=(other: CodecBitsPerSample): Bool
```

**Description:** Determines inequality for the number of bits per sample in Bluetooth codec.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecBitsPerSample](#enum-codecbitspersample)|Yes|-|Number of bits per sample in Bluetooth codec.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the number of bits per sample differs, otherwise returns false.|

### func ==(CodecBitsPerSample)

```cangjie
public operator func ==(other: CodecBitsPerSample): Bool
```

**Description:** Determines equality for the number of bits per sample in Bluetooth codec.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecBitsPerSample](#enum-codecbitspersample)|Yes|-|Number of bits per sample in Bluetooth codec.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the number of bits per sample is identical, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of the number of bits per sample in Bluetooth codec.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the number of bits per sample.|

## enum CodecChannelMode

```cangjie
public enum CodecChannelMode <: Equatable<CodecChannelMode> & ToString {
    | CodecChannelModeNone
    | CodecChannelModeMono
    | CodecChannelModeStereo
    | ...
}
```

**Description:** Channel mode for Bluetooth codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<CodecChannelMode>
- ToString

### CodecChannelModeMono

```cangjie
CodecChannelModeMono
```

**Description:** Mono channel.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecChannelModeNone

```cangjie
CodecChannelModeNone
```

**Description:** Unknown channel mode.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecChannelModeStereo

```cangjie
CodecChannelModeStereo
```

**Description:** Stereo channel.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(CodecChannelMode)

```cangjie
public operator func !=(other: CodecChannelMode): Bool
```

**Description:** Determines inequality for Bluetooth codec channel modes.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecChannelMode](#enum-codecchannelmode)|Yes|-|Bluetooth codec channel mode.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if channel modes differ, otherwise returns false.|

### func ==(CodecChannelMode)

```cangjie
public operator func ==(other: CodecChannelMode): Bool
```

**Description:** Determines equality for Bluetooth codec channel modes.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecChannelMode](#enum-codecchannelmode)|Yes|-|Bluetooth codec channel mode.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if channel modes are identical, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of Bluetooth codec channel mode.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of channel mode.|

## enum CodecSampleRate

```cangjie
public enum CodecSampleRate <: Equatable<CodecSampleRate> & ToString {
    | CodecSampleRateNone
    | CodecSampleRate44100
    | CodecSampleRate48000
    | CodecSampleRate88200
    | CodecSampleRate96000
    | CodecSampleRate176400
    | CodecSampleRate192000
    | ...
}
```

**Description:** Sample rate for Bluetooth codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<CodecSampleRate>
- ToString

### CodecSampleRate176400

```cangjie
CodecSampleRate176400
```

**Description:** 176.4k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRate192000

```cangjie
CodecSampleRate192000
```

**Description:** 192k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRate44100

```cangjie
CodecSampleRate44100
```

**Description:** 44.1k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRate48000

```cangjie
CodecSampleRate48000
```

**Description:** 48k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRate88200

```cangjie
CodecSampleRate88200
```

**Description:** 88.2k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRate96000

```cangjie
CodecSampleRate96000
```

**Description:** 96k sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecSampleRateNone

```cangjie
CodecSampleRateNone
```

**Description:** Unknown sample rate.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(CodecSampleRate)

```cangjie
public operator func !=(other: CodecSampleRate): Bool
```

**Description:** Determines inequality for Bluetooth codec sample rates.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecSampleRate](#enum-codecsamplerate)|Yes|-|Bluetooth codec sample rate.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if sample rates differ, otherwise returns false.|

### func ==(CodecSampleRate)

```cangjie
public operator func ==(other: CodecSampleRate): Bool
```

**Description:** Determines equality for Bluetooth codec sample rates.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecSampleRate](#enum-codecsamplerate)|Yes|-|Bluetooth codec sample rate.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if sample rates are identical, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Returns the string representation of Bluetooth codec sample rate.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of sample rate.|

```## enum CodecType

```cangjie
public enum CodecType <: Equatable<CodecType> & ToString {
    | CodecTypeInvalid
    | CodecTypeSbc
    | CodecTypeAac
    | CodecTypeL2hc
    | ...
}
```

**Function:** Bluetooth codec type.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<CodecType>
- ToString

### CodecTypeAac

```cangjie
CodecTypeAac
```

**Function:** AAC codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecTypeInvalid

```cangjie
CodecTypeInvalid
```

**Function:** Unknown codec type.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecTypeL2hc

```cangjie
CodecTypeL2hc
```

**Function:** L2HC codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CodecTypeSbc

```cangjie
CodecTypeSbc
```

**Function:** SBC codec.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(CodecType)

```cangjie
public operator func !=(other: CodecType): Bool
```

**Function:** Determines inequality between Bluetooth codec types.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecType](#enum-codectype)|Yes|-|Bluetooth codec type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if Bluetooth codec types are different, otherwise returns false.|

### func ==(CodecType)

```cangjie
public operator func ==(other: CodecType): Bool
```

**Function:** Determines equality between Bluetooth codec types.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[CodecType](#enum-codectype)|Yes|-|Bluetooth codec type.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if Bluetooth codec types are identical, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the Bluetooth codec type.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the Bluetooth codec type.|

## enum PlayingState

```cangjie
public enum PlayingState <: Equatable<PlayingState> & ToString {
    | StateNotPlaying
    | StatePlaying
    | ...
}
```

**Function:** Bluetooth A2DP playback state.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<PlayingState>
- ToString

### StateNotPlaying

```cangjie
StateNotPlaying
```

**Function:** Indicates not playing.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### StatePlaying

```cangjie
StatePlaying
```

**Function:** Indicates currently playing.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(PlayingState)

```cangjie
public operator func !=(other: PlayingState): Bool
```

**Function:** Determines inequality between Bluetooth A2DP playback states.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PlayingState](#enum-playingstate)|Yes|-|Bluetooth A2DP playback state.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if Bluetooth A2DP playback states are different, otherwise returns false.|

### func ==(PlayingState)

```cangjie
public operator func ==(other: PlayingState): Bool
```

**Function:** Determines equality between Bluetooth A2DP playback states.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PlayingState](#enum-playingstate)|Yes|-|Bluetooth A2DP playback state.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if Bluetooth A2DP playback states are identical, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Returns the string representation of the Bluetooth A2DP playback state.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the Bluetooth A2DP playback state.|