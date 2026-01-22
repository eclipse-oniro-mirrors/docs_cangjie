# ohos.bluetooth.ble (Bluetooth BLE Module)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The ble module provides methods for Bluetooth operation and management.

## Import Module

```cangjie
import kit.ConnectivityKit.*
```

## Permission List

ohos.permission.ACCESS_BLUETOOTH

## Usage Instructions

API sample code usage instructions:

- If the sample code has a "// index.cj" comment in the first line, it indicates that the sample can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](./../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.
- Please replace XX:XX:XX:XX:XX:XX or other addresses in the sample code with your real address.

For the above sample project and configuration template, please refer to [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## func createGattClientDevice(String)

```cangjie
public func createGattClientDevice(deviceId: String): GattClientDevice
```

**Function:** Creates a usable GattClientDevice instance.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceId | String | Yes | - | Peer device address, e.g., "XX:XX:XX:XX:XX:XX". |

**Return Value:**

| Type | Description |
|:----|:----|
| [GattClientDevice](#class-gattclientdevice) | Client-side class. An instance of this class needs to be created before using client-side methods. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 801 | Capability not supported. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    let device: GattClientDevice = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func createGattServer()

```cangjie
public func createGattServer(): GattServer
```

**Function:** Creates a usable GattServer instance.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [GattServer](#class-gattserver) | Returns a Gatt service instance. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog
import ohos.business_exception.BusinessException

try {
    let gattServer: GattServer = createGattServer()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

## func off(BluetoothBleCallbackType, ?CallbackObject)

```cangjie
public func off(eventType: BluetoothBleCallbackType, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from BLE device events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleCallbackType](#enum-bluetoothblecallbacktype) | Yes | - | Callback event. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** Indicates unsubscribing from BLE events. If this parameter is not provided, all callbacks corresponding to the type will be unsubscribed. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to the dependency definition
class BLEDeviceFindCallback <: Callback1Argument<Array<ScanResult>> {
    public func invoke(err: ?BusinessException, devices: Array<ScanResult>): Unit {
        for (device in devices) {
            Hilog.info(0, "Bluetooth", "device has find, deviceID is ${device.deviceId}, name is ${device.deviceName}")
        }
    }
}

let bleDeviceFindCallback = BLEDeviceFindCallback()
try {
    on(BluetoothBleCallbackType.BleDeviceFind, bleDeviceFindCallback)
    off(BluetoothBleCallbackType.BleDeviceFind, callback: bleDeviceFindCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func on(BluetoothBleCallbackType, Callback1Argument\<AdvertisingStateChangeInfo>)

```cangjie
public func on(eventType: BluetoothBleCallbackType, callback: Callback1Argument<AdvertisingStateChangeInfo>): Unit
```

**Function:** Subscribes to BLE advertising state changes.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleCallbackType](#enum-bluetoothblecallbacktype) | Yes | - | Set to AdvertisingStateChange, indicating advertising state event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[AdvertisingStateChangeInfo](#class-advertisingstatechangeinfo)> | Yes | - | Represents the input parameter of the callback function, advertising state. The callback function is created by the user and registered through this interface. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to the dependency definition
class AdvertisingStateChange <: Callback1Argument<AdvertisingStateChangeInfo> {
    public func invoke(err: ?BusinessException, info: AdvertisingStateChangeInfo): Unit {
        Hilog.info(0, "Bluetooth", "the advertising state is ${info.state}")
    }
}

let advertisingStateChange = AdvertisingStateChange()
try {
    on(BluetoothBleCallbackType.AdvertisingStateChange, advertisingStateChange)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func on(BluetoothBleCallbackType, Callback1Argument\<Array\<ScanResult>>)

```cangjie
public func on(eventType: BluetoothBleCallbackType, callback: Callback1Argument<Array<ScanResult>>): Unit
```

**Function:** Subscribes to BLE device discovery events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleCallbackType](#enum-bluetoothblecallbacktype) | Yes | - | Set to BleDeviceFind, indicating BLE device discovery event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Array\<[ScanResult](#class-scanresult)>> | Yes | - | Represents the input parameter of the callback function, discovered device collection. The callback function is created by the user and registered through this interface. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to the dependency definition
class BLEDeviceFindCallback <: Callback1Argument<Array<ScanResult>> {
    public func invoke(err: ?BusinessException, devices: Array<ScanResult>): Unit {
        for (device in devices) {
            Hilog.info(0, "Bluetooth", "device has find, deviceID is ${device.deviceId}, name is ${device.deviceName}")
        }
    }
}

let bleDeviceFindCallback = BLEDeviceFindCallback()
try {
    on(BluetoothBleCallbackType.BleDeviceFind, bleDeviceFindCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func startAdvertising(AdvertiseSetting, AdvertiseData, ?AdvertiseData)

```cangjie
public func startAdvertising(setting: AdvertiseSetting, advData: AdvertiseData, advResponse!: ?AdvertiseData = None): Unit
```

**Function:** Starts sending BLE advertisements.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| setting | [AdvertiseSetting](#class-advertisesetting) | Yes | - | BLE advertisement parameters. |
| advData | [AdvertiseData](#class-advertisedata) | Yes | - | BLE advertisement packet content. |
| advResponse | ?[AdvertiseData](#class-advertisedata) | No | None | **Named parameter.** BLE scan request response. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

let advertisingSettings = AdvertiseSetting()
let manufactureDataUnit = ManufactureData(
    4567u16,
    [1, 2, 3, 4]
)
let serviceDataUnit = ServiceData(
    "00001888-0000-1000-8000-00805f9b34fb",
    [5, 6, 7, 8]
)
let advertisingData = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit],
    includeDeviceName: true
)
let advertisingResponse = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit]
)
try {
    startAdvertising(advertisingSettings, advertisingData, advResponse: advertisingResponse)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func startAdvertising(AdvertisingParams)

```cangjie
public func startAdvertising(advertisingParams: AdvertisingParams): UInt32
```

**Function:** Starts sending BLE advertisements.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Initial Version:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| advertisingParams | [AdvertisingParams](#class-advertisingparams) | Yes | - | Parameters for starting BLE advertisements. |

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Advertisement ID identifier. |

**Exceptions:**

- BusinessException: Corresponding error codes are shown in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |
  | 2900010 | The number of advertising resources reaches the upper limit. |
  | 2902054 | The length of the advertising data exceeds the upper limit. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

let advertisingSettings = AdvertiseSetting()
let manufactureDataUnit = ManufactureData(
    4567u16,
    [1, 2, 3, 4]
)
let serviceDataUnit = ServiceData(
    "00001888-0000-1000-8000-00805f9b34fb",
    [5, 6, 7, 8]
)
let advertisingData = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit],
    includeDeviceName: true
)
let advertisingResponse = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit]
)
let advertisingParams = AdvertisingParams(
    advertisingSettings,
    advertisingData,
    advertisingResponse: advertisingResponse,
    duration: 300
)
try {
    let advHandle = startAdvertising(advertisingParams)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```## func startBLEScan(Array\<ScanFilter>, ?ScanOptions)

```cangjie
public func startBLEScan(filters: Array<ScanFilter>, options!: ?ScanOptions = None): Unit
```

**Function:** Initiates the BLE scanning process.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| filters | Array\<[ScanFilter](#class-scanfilter)> | Yes | - | Represents the collection of scan result filtering policies. Only device discoveries that match the filter conditions will be retained. |
| options | ?[ScanOptions](#class-scanoptions) | No | None | **Named parameter.** Represents the configuration parameters for scanning, which are optional. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Code here can be added to dependency definitions
class BLEDeviceFindCallback <: Callback1Argument<Array<ScanResult>> {
    public func invoke(err: ?BusinessException, devices: Array<ScanResult>): Unit {
        for (device in devices) {
            Hilog.info(0, "Bluetooth", "device has find, deviceID is ${device.deviceId}, name is ${device.deviceName}")
        }
    }
}

let bleDeviceFindCallback = BLEDeviceFindCallback()
try {
    on(BluetoothBleCallbackType.BleDeviceFind, bleDeviceFindCallback)
    var scanFilter = ScanFilter()
    scanFilter.serviceUUID = "00001888-0000-1000-8000-00805f9b34fb"  // Replace with your serviceUUID
    let scanOptions = ScanOptions(interval: 0, dutyMode: ScanDuty.ScanModeLowPower, matchMode: MatchMode.MatchModeAggressive, phyType: PhyType.PhyLe1M)
    startBLEScan([scanFilter], options: scanOptions)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func stopAdvertising()

```cangjie
public func stopAdvertising(): Unit
```

**Function:** Stops sending BLE advertisements.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

try {
    stopAdvertising()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func stopAdvertising(UInt32)

```cangjie
public func stopAdvertising(advertisingId: UInt32): Unit
```

**Function:** Stops sending BLE advertisements.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| advertisingId | UInt32 | Yes | - | The identifier of the advertisement to stop. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |
  | 2902055 | Invalid advertising id. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.*
import ohos.business_exception.BusinessException

let advertisingSettings = AdvertiseSetting()
let manufactureDataUnit = ManufactureData(
    4567u16,
    [1, 2, 3, 4]
)
let serviceDataUnit = ServiceData(
    "00001888-0000-1000-8000-00805f9b34fb",
    [5, 6, 7, 8]
)
let advertisingData = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit],
    includeDeviceName: true
)
let advertisingResponse = AdvertiseData(
    ["00001888-0000-1000-8000-00805f9b34fb"],
    [manufactureDataUnit],
    [serviceDataUnit]
)
let advertisingParams = AdvertisingParams(
    advertisingSettings,
    advertisingData,
    advertisingResponse: advertisingResponse,
    duration: 300
)
var advHandle: UInt32 = 0xFF
try {
    advHandle = startAdvertising(advertisingParams)
    stopAdvertising(advHandle)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## func stopBLEScan()

```cangjie
public func stopBLEScan(): Unit
```

**Function:** Stops the BLE scanning process.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

try {
    stopBLESscan()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## class AdvertiseData

```cangjie
public class AdvertiseData {
    public var serviceUUIDs: Array<String>
    public var manufactureData: Array<ManufactureData>
    public var serviceData: Array<ServiceData>
    public var includeDeviceName: Bool
    public init(
        serviceUUIDs: Array<String>,
        manufactureData: Array<ManufactureData>,
        serviceData: Array<ServiceData>,
        includeDeviceName!: Bool = false,
        includeTxPower!: Bool = false
    )
}
```

**Function:** Describes the content of a BLE advertisement packet, with a maximum length of 31 bytes.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var includeDeviceName

```cangjie
public var includeDeviceName: Bool
```

**Function:** Indicates whether to include the device name (optional). `true` means include, `false` or unset means exclude. Note that including the device name must not exceed the 31-byte limit.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureData

```cangjie
public var manufactureData: Array<ManufactureData>
```

**Function:** Represents the list of manufacturer information to be advertised.

**Type:** Array\<[ManufactureData](#class-manufacturedata)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceData

```cangjie
public var serviceData: Array<ServiceData>
```

**Function:** Represents the list of service data to be advertised.

**Type:** Array\<[ServiceData](#class-servicedata)>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUIDs

```cangjie
public var serviceUUIDs: Array<String>
```

**Function:** Represents the list of services to be advertised.

**Type:** Array\<String>

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(Array\<String>, Array\<ManufactureData>, Array\<ServiceData>, Bool, Bool)

```cangjie
public init(
    serviceUUIDs: Array<String>,
    manufactureData: Array<ManufactureData>,
    serviceData: Array<ServiceData>,
    includeDeviceName!: Bool = false,
    includeTxPower!: Bool = false
)
```

**Function:** Constructor for AdvertiseData.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| serviceUUIDs | Array\<String> | Yes | - | Represents the list of service UUIDs to be advertised. |
| manufactureData | Array\<[ManufactureData](#class-manufacturedata)> | Yes | - | Represents the list of manufacturer information to be advertised. |
| serviceData | Array\<[ServiceData](#class-servicedata)> | Yes | - | Represents the list of service data to be advertised. |
| includeDeviceName | Bool | No | false | **Named parameter.** Indicates whether to include the device name (optional). `true` means include, `false` or unset means exclude. Note that including the device name must not exceed the 31-byte limit. |
| includeTxPower | Bool | No | false | **Named parameter.** Indicates whether to include the advertisement transmission power. `true` means include, `false` means exclude (default). Including this value will occupy an additional 3 bytes in the advertisement packet. Reserved field, not supported in this version. |

## class AdvertiseSetting

```cangjie
public class AdvertiseSetting {
    public var interval: UInt16
    public var txPower: Int8
    public var connectable: Bool
    public init(interval!: UInt16 = BLE_ADV_DEFAULT_INTERVAL, txPower!: Int8 = BLE_ADV_TX_POWER_MEDIUM_VALUE, connectable!: Bool = true)
}
```

**Function:** Describes the parameters for sending BLE advertisements.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var connectable

```cangjie
public var connectable: Bool
```

**Function:** Indicates whether the advertisement is connectable. The default is `true` (connectable), `false` means non-connectable.

**Type:** Bool

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var interval

```cangjie
public var interval: UInt16
```

**Function:** Represents the advertisement interval. The minimum value is 160 slots (100ms), the maximum is 16384 slots, and the default is 1600 slots (1s).

**Type:** UInt16

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var txPower

```cangjie
public var txPower: Int8
```

**Function:** Represents the transmission power. The minimum value is -127, the maximum is 1, and the default is -7 (unit: dBm). Recommended values: High (1), Medium (-7), Low (-15).

**Type:** Int8

**Read/Write:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(UInt16, Int8, Bool)

```cangjie
public init(interval!: UInt16 = BLE_ADV_DEFAULT_INTERVAL, txPower!: Int8 = BLE_ADV_TX_POWER_MEDIUM_VALUE, connectable!: Bool = true)
```

**Function:** Constructs the parameters for sending BLE advertisements.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| interval | UInt16 | No | BLE_ADV_DEFAULT_INTERVAL | Represents the advertisement interval. The minimum value is 160 slots (100ms), the maximum is 16384 slots, and the default is 1600 slots (1s). |
| txPower | Int8 | No | BLE_ADV_TX_POWER_MEDIUM_VALUE | Represents the transmission power. The minimum value is -127, the maximum is 1, and the default is -7 (unit: dBm). Recommended values: High (1), Medium (-7), Low (-15). |
| connectable | Bool | No | true | Indicates whether the advertisement is connectable. The default is `true` (connectable), `false` means non-connectable. |## class AdvertisingParams

```cangjie
public class AdvertisingParams {
    public var advertisingSettings: AdvertiseSetting
    public var advertisingData: AdvertiseData
    public var advertisingResponse: AdvertiseData
    public var duration: UInt16
    public init(
        advertisingSettings: AdvertiseSetting,
        advertisingData: AdvertiseData,
        advertisingResponse!: AdvertiseData = AdvertiseData([], [], []),
        duration!: UInt16 = 0
    )
}
```

**Function:** Describes parameters for initial broadcast settings.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var advertisingData

```cangjie
public var advertisingData: AdvertiseData
```

**Function:** Represents the content of broadcast data packets.

**Type:** [AdvertiseData](#class-advertisedata)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var advertisingResponse

```cangjie
public var advertisingResponse: AdvertiseData
```

**Function:** Represents the response content for scan requests.

**Type:** [AdvertiseData](#class-advertisedata)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var advertisingSettings

```cangjie
public var advertisingSettings: AdvertiseSetting
```

**Function:** Represents parameters related to broadcast transmission.

**Type:** [AdvertiseSetting](#class-advertisesetting)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var duration

```cangjie
public var duration: UInt16
```

**Function:** Represents the duration of broadcast transmission. Unit is 10ms, valid range is 1 (10ms) to 65535 (655350ms). If this parameter is not specified or set to 0, broadcasting will continue indefinitely.

**Type:** UInt16

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(AdvertiseSetting, AdvertiseData, AdvertiseData, UInt16)

```cangjie
public init(
    advertisingSettings: AdvertiseSetting,
    advertisingData: AdvertiseData,
    advertisingResponse!: AdvertiseData = AdvertiseData([], [], []),
    duration!: UInt16 = 0
)
```

**Function:** AdvertisingParams constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| advertisingSettings | [AdvertiseSetting](#class-advertisesetting) | Yes | - | Parameters related to broadcast transmission. |
| advertisingData | [AdvertiseData](#class-advertisedata) | Yes | - | Content of broadcast data packets. |
| advertisingResponse | [AdvertiseData](#class-advertisedata) | No | AdvertiseData([],[],[]) | Response content for scan requests. |
| duration | UInt16 | No | 0 | **Named parameter.** Duration of broadcast transmission. Unit is 10ms, valid range is 1 (10ms) to 65535 (655350ms). If not specified or set to 0, broadcasting will continue indefinitely. |

## class AdvertisingStateChangeInfo

```cangjie
public class AdvertisingStateChangeInfo {
    public var advertisingId: Int32
    public var state: AdvertisingState
}
```

**Function:** Describes broadcast state information such as start and stop.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var advertisingId

```cangjie
public var advertisingId: Int32
```

**Function:** Represents the broadcast ID identifier.

**Type:** Int32

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var state

```cangjie
public var state: AdvertisingState
```

**Function:** Represents the broadcast state.

**Type:** [AdvertisingState](#enum-advertisingstate)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class BLECharacteristic

```cangjie
public class BLECharacteristic {
    public var serviceUUID: String
    public var characteristicUUID: String
    public var characteristicValue: Array<Byte>
    public var descriptors: Array<BLEDescriptor>
    public var properties: GattProperties
    public init(
        serviceUUID: String,
        characteristicUUID: String,
        characteristicValue: Array<Byte>,
        descriptors: Array<BLEDescriptor>,
        properties!: GattProperties = GattProperties(),
        permissions!: GattPermissions = GattPermissions(),
        characteristicValueHandle!: UInt32 = 0
    )
}
```

**Function:** Defines interface parameters for characteristics.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of a specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicValue

```cangjie
public var characteristicValue: Array<Byte>
```

**Function:** Binary value corresponding to the characteristic.

**Type:** Array\<Byte>

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var descriptors

```cangjie
public var descriptors: Array<BLEDescriptor>
```

**Function:** List of descriptors for a specific characteristic.

**Type:** Array\<[BLEDescriptor](#class-bledescriptor)>

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var properties

```cangjie
public var properties: GattProperties
```

**Function:** Describes the properties of a specific characteristic.

**Type:** [GattProperties](#class-gattproperties)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, String, Array\<Byte>, Array\<BLEDescriptor>, GattProperties, GattPermissions, UInt32)

```cangjie
public init(
    serviceUUID: String,
    characteristicUUID: String,
    characteristicValue: Array<Byte>,
    descriptors: Array<BLEDescriptor>,
    properties!: GattProperties = GattProperties(),
    permissions!: GattPermissions = GattPermissions(),
    characteristicValueHandle!: UInt32 = 0
)
```

**Function:** BLECharacteristic constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb". |
| characteristicUUID | String | Yes | - | UUID of a specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb". |
| characteristicValue | Array\<Byte> | Yes | - | Binary value corresponding to the characteristic. |
| descriptors | Array\<[BLEDescriptor](#class-bledescriptor)> | Yes | - | List of descriptors for a specific characteristic. |
| properties | [GattProperties](#class-gattproperties) | No | GattProperties() | **Named parameter.** Describes the properties of a specific characteristic. |
| permissions | [GattPermissions](#class-gattpermissions) | No | GattPermissions() | **Named parameter.** Required permissions for characteristic value read/write operations. Reserved field, not supported in this version. |
| characteristicValueHandle | UInt32 | No | 0 | **Named parameter.** Unique identifier handle for the characteristic value. When a BLE server device provides multiple characteristic values with the same UUID, this handle can distinguish between them. Reserved field, not supported in this version. |

## class BLEConnectionChangeState

```cangjie
public class BLEConnectionChangeState {
    public var deviceId: String
    public var state: ProfileConnectionState
}
```

**Function:** Describes GATT profile connection state.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the remote device address, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var state

```cangjie
public var state: ProfileConnectionState
```

**Function:** Represents the enumeration of BLE connection states.

**Type:** [ProfileConnectionState](cj-apis-bluetooth-constant.md#enum-profileconnectionstate)

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class BLEDescriptor

```cangjie
public class BLEDescriptor {
    public var serviceUUID: String
    public var characteristicUUID: String
    public var descriptorUUID: String
    public var descriptorValue: Array<Byte>
    public init(
        serviceUUID: String,
        characteristicUUID: String,
        descriptorUUID: String,
        descriptorValue: Array<Byte>,
        descriptorHandle!: UInt32 = 0,
        permissions!: GattPermissions = GattPermissions()
    )
}
```

**Function:** Defines interface parameters for descriptors.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of a specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var descriptorUUID

```cangjie
public var descriptorUUID: String
```

**Function:** UUID of a descriptor, e.g., "00002902-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var descriptorValue

```cangjie
public var descriptorValue: Array<Byte>
```

**Function:** Binary value corresponding to the descriptor.

**Type:** Array\<Byte>

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, String, String, Array\<Byte>, UInt32, GattPermissions)

```cangjie
public init(
    serviceUUID: String,
    characteristicUUID: String,
    descriptorUUID: String,
    descriptorValue: Array<Byte>,
    descriptorHandle!: UInt32 = 0,
    permissions!: GattPermissions = GattPermissions()
)
```

**Function:** BLEDescriptor constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb". |
| characteristicUUID | String | Yes | - | UUID of a specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb". |
| descriptorUUID | String | Yes | - | UUID of a descriptor, e.g., "00002902-0000-1000-8000-00805f9b34fb". |
| descriptorValue | Array\<Byte> | Yes | - | Binary value corresponding to the descriptor. |
| descriptorHandle | UInt32 | No | 0 | **Named parameter.** Unique identifier handle for the descriptor. When a BLE server device provides multiple descriptors with the same UUID, this handle can distinguish between them. Reserved field, not supported in this version. |
| permissions | [GattPermissions](#class-gattpermissions) | No | GattPermissions() | **Named parameter.** Required permissions for descriptor read/write operations. Reserved field, not supported in this version. |## class CharacteristicReadRequest

```cangjie
public class CharacteristicReadRequest {
    public var deviceId: String
    public var transId: Int32
    public var offset: Int32
    public var characteristicUUID: String
    public var serviceUUID: String
}
```

**Function:** Describes the parameter class for characteristic read request events received after server-side subscription.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the remote device address that sent the characteristic read request, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int32
```

**Function:** Represents the starting position for reading characteristic value data. For example, k indicates reading from the k-th byte. The server must fill in the same offset when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var transId

```cangjie
public var transId: Int32
```

**Function:** Represents the transaction ID of the write request. The server must fill in the same transaction ID when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class CharacteristicWriteRequest

```cangjie
public class CharacteristicWriteRequest {
    public var deviceId: String
    public var transId: Int32
    public var offset: Int32
    public var isPrepared: Bool
    public var needRsp: Bool
    public var value: Array<Byte>
    public var characteristicUUID: String
    public var serviceUUID: String
}
```

**Function:** Describes the parameter class for characteristic write request events received after server-side subscription.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the scanned device address, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var isPrepared

```cangjie
public var isPrepared: Bool
```

**Function:** Indicates whether the write request should be executed immediately. true means immediate execution.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var needRsp

```cangjie
public var needRsp: Bool
```

**Function:** Indicates whether a response should be sent to the client.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int32
```

**Function:** Represents the starting position for writing descriptor data. For example, k indicates writing from the k-th byte. The server must fill in the same offset when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var transId

```cangjie
public var transId: Int32
```

**Function:** Represents the transaction ID of the write request. The server must fill in the same transaction ID when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var value

```cangjie
public var value: Array<Byte>
```

**Function:** Represents the binary data of the descriptor to be written.

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class DescriptorReadRequest

```cangjie
public class DescriptorReadRequest {
    public var deviceId: String
    public var transId: Int32
    public var offset: Int32
    public var descriptorUUID: String
    public var characteristicUUID: String
    public var serviceUUID: String
}
```

**Function:** Describes the parameter class for descriptor read request events received after server-side subscription.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var descriptorUUID

```cangjie
public var descriptorUUID: String
```

**Function:** Represents the UUID of the descriptor, e.g., "00002902-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the remote device address that sent the descriptor read request, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int32
```

**Function:** Represents the starting position for reading descriptor data. For example, k indicates reading from the k-th byte. The server must fill in the same offset when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var transId

```cangjie
public var transId: Int32
```

**Function:** Represents the transaction ID of the read request. The server must fill in the same transaction ID when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class DescriptorWriteRequest

```cangjie
public class DescriptorWriteRequest {
    public var deviceId: String
    public var transId: Int32
    public var offset: Int32
    public var isPrepared: Bool
    public var needRsp: Bool
    public var value: Array<Byte>
    public var descriptorUUID: String
    public var characteristicUUID: String
    public var serviceUUID: String
}
```

**Function:** Describes the parameter class for descriptor write request events received after server-side subscription.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var descriptorUUID

```cangjie
public var descriptorUUID: String
```

**Function:** Represents the UUID of the descriptor, e.g., "00002902-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the remote device address that sent the descriptor write request, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var isPrepared

```cangjie
public var isPrepared: Bool
```

**Function:** Indicates whether the write request should be executed immediately.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var needRsp

```cangjie
public var needRsp: Bool
```

**Function:** Indicates whether a response should be sent to the client.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int32
```

**Function:** Represents the starting position for writing descriptor data. For example, k indicates writing from the k-th byte. The server must fill in the same offset when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var transId

```cangjie
public var transId: Int32
```

**Function:** Represents the transaction ID of the write request. The server must fill in the same transaction ID when responding.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var value

```cangjie
public var value: Array<Byte>
```

**Function:** Represents the binary data of the descriptor to be written.

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22## class GattClientDevice

```cangjie
public class GattClientDevice {}
```

**Description:** The client-side class. An instance of this class must be created via the [createGattClientDevice(String)](#func-creategattclientdevicestring) method before using client-side methods.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func close()

```cangjie
public func close(): Unit
```

**Description:** Closes the client functionality, deregisters the client from the protocol stack. After calling this interface, the [GattClientDevice](#class-gattclientdevice) instance can no longer be used.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    gattClient.close()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func connect()

```cangjie
public func connect(): Unit
```

**Description:** Initiates a connection to a remote Bluetooth Low Energy (BLE) device from the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    gattClient.connect()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func disconnect()

```cangjie
public func disconnect(): Unit
```

**Description:** Disconnects from a remote Bluetooth Low Energy (BLE) device from the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    gattClient.disconnect()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func getDeviceName()

```cangjie
public func getDeviceName(): String
```

**Description:** Retrieves the name of the remote Bluetooth Low Energy (BLE) device from the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | The name of the remote server device obtained by the client. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    let server = gattClient.getDeviceName()
    Hilog.info(0, "Bluetooth", "device name " + server)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func getRssiValue(AsyncCallback\<Int32>)

```cangjie
public func getRssiValue(callback: AsyncCallback<Int32>): Unit
```

**Description:** Retrieves the Received Signal Strength Indication (RSSI) of the remote Bluetooth Low Energy (BLE) device from the client side. This can only be used after successfully calling the [connect](#func-connect) interface.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Int32> | Yes | - | Returns the signal strength in dBm via the registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900099 | Operation failed. |
  | 2900011 | The operation is busy. The last operation is not completed. |
  | 2901003 | The connection is not established. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    gattClient.getRssiValue {
        error: ?BusinessException, rssi: ?Int32 =>
        if (let Some(e) <- error) {
            throw e
        }
        Hilog.info(0, "Bluetooth", "the rssi value is " + rssi.getOrThrow().toString())
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func getServices(AsyncCallback\<Array\<GattService>>)

```cangjie
public func getServices(callback: AsyncCallback<Array<GattService>>): Unit
```

**Description:** Discovers all services of the Bluetooth Low Energy (BLE) device from the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Array\<[GattService](#class-gattservice)>> | Yes | - | Performs service discovery on the client side. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    let services = gattClient.getServices{err: ?BusinessException, c: ?Array<GattService> =>
            let ss = c.getOrThrow()
            for (service in ss) {
                Hilog.info(0, "Bluetooth", "find serviceUUID : ${service.serviceUUID}")
            }
        }
    Hilog.info(0, "Bluetooth", "getServices success")
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func off(BluetoothBleGattClientDeviceCallbackType, ?CallbackObject)

```cangjie
public func off(eventType: BluetoothBleGattClientDeviceCallbackType, callback!: ?CallbackObject = None): Unit
```

**Description:** Unsubscribes from client-side Bluetooth Low Energy (BLE) device events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype) | Yes | - | The characteristic value change event. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** Unsubscribes from client-side Bluetooth Low Energy (BLE) device events. If this parameter is not provided, all callbacks corresponding to the type will be unsubscribed. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
let device = "XX:XX:XX:XX:XX:XX"
var connectState = ProfileConnectionState.StateDisconnected
class BLEConnectionStateChangeCallback <: Callback1Argument<BLEConnectionChangeState> {
    public func invoke(err: ?BusinessException, stateInfo: BLEConnectionChangeState): Unit {
        Hilog.info(0, "Bluetooth", "onGattServerStateChange: device=" + stateInfo.deviceId + ", state=" + stateInfo.state.toString())
        if (stateInfo.deviceId == device) {
            connectState = stateInfo.state
        }
    }
}

let bleConnectionStateChangeCallback = BLEConnectionStateChangeCallback()
try {
    gattClient.on(BluetoothBleGattClientDeviceCallbackType.BleConnectionStateChange, bleConnectionStateChangeCallback)
    gattClient.off(BluetoothBleGattClientDeviceCallbackType.BleConnectionStateChange, callback: bleConnectionStateChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattClientDeviceCallbackType, Callback1Argument\<BLECharacteristic>)

```cangjie
public func on(eventType: BluetoothBleGattClientDeviceCallbackType, callback: Callback1Argument<BLECharacteristic>): Unit
```

**Description:** Subscribes to MTU state change events on the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype) | Yes | - | Must be set to ClientBleMtuChange, indicating the MTU state change event. Incorrect values will prevent callback registration. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[BLECharacteristic](#class-blecharacteristic)> | Yes | - | Returns the MTU byte count value via the registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
class BLECharacteristicChangeCallback <: Callback1Argument<BLECharacteristic> {
    public func invoke(err: ?BusinessException, characteristic: BLECharacteristic): Unit {
        Hilog.info(0, "Bluetooth", "characteristic ${characteristic.serviceUUID} has change")
    }
}

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
let bleCharacteristicChangeCallback = BLECharacteristicChangeCallback()
try {
    gattClient.on(BluetoothBleGattClientDeviceCallbackType.ClientBleMtuChange, bleCharacteristicChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```### func on(BluetoothBleGattClientDeviceCallbackType, Callback1Argument\<BLEConnectionChangeState>)

```cangjie
public func on(
    eventType: BluetoothBleGattClientDeviceCallbackType,
    callback: Callback1Argument<BLEConnectionChangeState>
): Unit
```

**Function:** Subscribes to MTU state change events on the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype) | Yes | - | Set to BleConnectionStateChange, indicating connection state change events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[BLEConnectionChangeState](#class-bleconnectionchangestate)> | Yes | - | Returns the MTU byte count value, obtained via registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Code can be added in dependency definitions
let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
let device = "XX:XX:XX:XX:XX:XX"
var connectState = ProfileConnectionState.StateDisconnected
class BLEConnectionStateChangeCallback <: Callback1Argument<BLEConnectionChangeState> {
    public func invoke(err: ?BusinessException, stateInfo: BLEConnectionChangeState): Unit {
        Hilog.info(0, "Bluetooth", "onGattServerStateChange: device=" + stateInfo.deviceId + ", state=" + stateInfo.state.toString())
        if (stateInfo.deviceId == device) {
            connectState = stateInfo.state
        }
    }
}

let bleConnectionStateChangeCallback = BLEConnectionStateChangeCallback()
try {
    gattClient.on(BluetoothBleGattClientDeviceCallbackType.BleConnectionStateChange, bleConnectionStateChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattClientDeviceCallbackType, Callback1Argument\<Int32>)

```cangjie
public func on(eventType: BluetoothBleGattClientDeviceCallbackType, callback: Callback1Argument<Int32>): Unit
```

**Function:** Subscribes to MTU state change events on the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype) | Yes | - | Must be set to ClientBleMtuChange, indicating MTU state change events. Incorrect settings will prevent callback registration. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Int32> | Yes | - | Returns the MTU byte count value, obtained via registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Code can be added in dependency definitions
let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
class BLEMtuChangeCallback <: Callback1Argument<Int32> {
    public func invoke(err: ?BusinessException, mtu: Int32): Unit {
        Hilog.info(0, "Bluetooth", "mtu change to ${mtu}")
    }
}

let bleMtuChangeCallback = BLEMtuChangeCallback()
try {
    gattClient.on(BluetoothBleGattClientDeviceCallbackType.ClientBleMtuChange, bleMtuChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func readCharacteristicValue(BLECharacteristic, AsyncCallback\<BLECharacteristic>)

```cangjie
public func readCharacteristicValue(
    characteristic: BLECharacteristic,
    callback: AsyncCallback<BLECharacteristic>
): Unit
```

**Function:** Reads the characteristic value of a specific service from a Bluetooth Low Energy (BLE) device on the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| characteristic | [BLECharacteristic](#class-blecharacteristic) | Yes | - | The characteristic value to be read. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[BLECharacteristic](#class-blecharacteristic)> | Yes | - | The client reads the characteristic value, obtained via registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900011 | The operation is busy. The last operation is not completed. |
  | 2901000 | Read forbidden. |
  | 2900099 | Operation failed. |
  | 2901003 | The connection is not established. |
  | 2901004 | The connection is congested. |
  | 2901005 | The connection is not encrypted. |
  | 2901006 | The connection is not authenticated. |
  | 2901007 | The connection is not authorized. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address

// Create descriptors
let descBuffer: Array<Byte> = [31, 32]
let descriptor = BLEDescriptor(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    "00002902-0000-1000-8000-00805F9B34FB",
    Array<Byte>(2, repeat: 0)
)
// Create characteristics
let descriptors: Array<BLEDescriptor> = [descriptor]
let charBuffer: Array<Byte> = [21, 22]
let properties = GattProperties()

let characteristic: BLECharacteristic = BLECharacteristic(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    charBuffer,
    descriptors,
    properties: properties
)

try {
    gattClient.readCharacteristicValue(characteristic) {
        error: ?BusinessException, outData: ?BLECharacteristic =>
        if (let Some(e) <- error) {
            throw e
        }
        if (let Some(c) <- outData) {
            Hilog.info(0, "Bluetooth", "read characteristic value uuid is ${c.characteristicUUID}", "")
            let message = StringBuilder("logCharacteristic value: ")
            for (i in 0..c.characteristicValue.size) {
                message.append(c.characteristicValue[i])
            }
            Hilog.info(0, "Bluetooth", message.toString())
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func readDescriptorValue(BLEDescriptor, AsyncCallback\<BLEDescriptor>)

```cangjie
public func readDescriptorValue(descriptor: BLEDescriptor, callback: AsyncCallback<BLEDescriptor>): Unit
```

**Function:** Reads the descriptor of a specific characteristic from a BLE device on the client side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| descriptor | [BLEDescriptor](#class-bledescriptor) | Yes | - | The descriptor to be read. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<[BLEDescriptor](#class-bledescriptor)> | Yes | - | The client reads the descriptor, obtained via registered callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900011 | The operation is busy. The last operation is not complete. |
  | 2900099 | Operation failed. |
  | 2901000 | Read forbidden. |
  | 2901003 | The connection is not established. |
  | 2901004 | The connection is congested. |
  | 2901005 | The connection is not encrypted. |
  | 2901006 | The connection is not authenticated. |
  | 2901007 | The connection is not authorized. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address

let descBuffer: Array<Byte> = [31, 32]
let descriptor = BLEDescriptor(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    "00002903-0000-1000-8000-00805F9B34FB",
    Array<Byte>(2, repeat: 0)
)

try {
    gattClient.readDescriptorValue(descriptor) {
        error: ?BusinessException, outDescriptor: ?BLEDescriptor =>
        if (let Some(e) <- error) {
            throw e
        }
        if (let Some(d) <- outDescriptor) {
            Hilog.info(0, "Bluetooth", "read descriptor value uuid is ${d.descriptorUUID}")
            let message = StringBuilder("logDescriptor value: ")
            for (i in 0..d.descriptorValue.size) {
                message.append(d.descriptorValue[i])
            }
            Hilog.info(0, "Bluetooth", message.toString())
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func setBLEMtuSize(Int32)

```cangjie
public func setBLEMtuSize(mtu: Int32): Unit
```

**Function:** Negotiates the Maximum Transmission Unit (MTU) size with a remote BLE device on the client side. This can only be used after a successful connection is established via the [connect](#func-connect) interface.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| mtu | Int32 | Yes | - | Range: 22~512 bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address
try {
    gattClient.setBLEMtuSize(100)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func setCharacteristicChangeIndication(BLECharacteristic, Bool, AsyncCallback\<Unit>)

```cangjie
public func setCharacteristicChangeIndication(characteristic: BLECharacteristic, enable: Bool, callback: AsyncCallback<Unit>): Unit
```

**Function:** Sends a request to the server to set notifications for this characteristic value, requiring a response from the peer device.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| characteristic | [BLECharacteristic](#class-blecharacteristic) | Yes | - | The binary value and other parameters corresponding to the BLE device characteristic. |
| enable | Bool | Yes | - | The write type for the BLE device characteristic. |
| callback | [AsyncCallback](../arkinterop/cj-api-business_exception.md#type-asynccallback)\<Unit> | Yes | - | Callback function. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900011 | The operation is busy. The last operation is not completed. |
  | 2900099 | Operation failed. |
  | 2901003 | The connection is not established. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattClient = createGattClientDevice("XX:XX:XX:XX:XX:XX")  // Replace with your device address

// Create descriptors
let descBuffer: Array<Byte> = [31, 32]
let descriptor = BLEDescriptor(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    "00002902-0000-1000-8000-00805F9B34FB",
    Array<Byte>(2, repeat: 0)
)
// Create characteristics
let descriptors: Array<BLEDescriptor> = [descriptor]
let charBuffer: Array<Byte> = [21, 22]
let properties = GattProperties()

let characteristic: BLECharacteristic = BLECharacteristic(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    charBuffer,
    descriptors,
    properties: properties
)

try {
    gattClient.setCharacteristicChangeIndication(characteristic, false)  {
        error: ?BusinessException, c: ?Unit => if (let Some(e) <- error) {
            throw e
        }
    }
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e## class GattPermissions

```cangjie
public class GattPermissions <: Equatable<GattPermissions> {
    public var read: Bool
    public var readEncrypted: Bool
    public var readEncryptedMitm: Bool
    public var write: Bool
    public var writeEncrypted: Bool
    public var writeEncryptedMitm: Bool
    public var writeSigned: Bool
    public var writeSignedMitm: Bool
    public init (
        read!: Bool = true,
        readEncrypted!: Bool = false,
        readEncryptedMitm!: Bool = false,
        write!: Bool = true,
        writeEncrypted!: Bool = false,
        writeEncryptedMitm!: Bool = false,
        writeSigned!: Bool = false,
        writeSignedMitm!: Bool = false
    )
}
```

**Function:** Describes the required permissions for reading/writing GATT characteristic values or descriptors.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Type:**

- Equatable\<GattPermissions>

### var read

```cangjie
public var read: Bool
```

**Function:** Indicates whether reading the characteristic value or descriptor content is permitted.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var readEncrypted

```cangjie
public var readEncrypted: Bool
```

**Function:** Indicates whether reading the characteristic value or descriptor content requires encryption.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var readEncryptedMitm

```cangjie
public var readEncryptedMitm: Bool
```

**Function:** Indicates whether reading the characteristic value or descriptor content requires Man-in-the-Middle (MITM) protected encryption.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var write

```cangjie
public var write: Bool
```

**Function:** Indicates whether writing to the characteristic value or descriptor content is permitted.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var writeEncrypted

```cangjie
public var writeEncrypted: Bool
```

**Function:** Indicates whether writing to the characteristic value or descriptor content requires encryption.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var writeEncryptedMitm

```cangjie
public var writeEncryptedMitm: Bool
```

**Function:** Indicates whether writing to the characteristic value or descriptor content requires MITM-protected encryption.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var writeSigned

```cangjie
public var writeSigned: Bool
```

**Function:** Indicates whether writing to the characteristic value or descriptor content requires signature processing.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var writeSignedMitm

```cangjie
public var writeSignedMitm: Bool
```

**Function:** Indicates whether writing to the characteristic value or descriptor content requires MITM-protected signature processing.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(Bool, Bool, Bool, Bool, Bool, Bool, Bool, Bool)

```cangjie
public init (
    read!: Bool = true,
    readEncrypted!: Bool = false,
    readEncryptedMitm!: Bool = false,
    write!: Bool = true,
    writeEncrypted!: Bool = false,
    writeEncryptedMitm!: Bool = false,
    writeSigned!: Bool = false,
    writeSignedMitm!: Bool = false
)
```

**Function:** GattPermissions constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| read | Bool | No | true | Indicates whether reading the characteristic value or descriptor content is permitted.<br>true means permitted, false means not permitted. Default is true. |
| readEncrypted | Bool | No | false | Indicates whether reading the characteristic value or descriptor content requires encryption.<br>true means encryption is required for reading, false means no basic encryption is needed. Default is false. |
| readEncryptedMitm | Bool | No | false | Indicates whether reading the characteristic value or descriptor content requires MITM-protected encryption.<br>MITM protection means the operation requires authentication to prevent data tampering by third parties. true means MITM-protected encryption is required for reading, false means not required. Default is false. |
| write | Bool | No | true | Indicates whether writing to the characteristic value or descriptor content is permitted.<br>true means permitted, false means not permitted. Default is true. |
| writeEncrypted | Bool | No | false | Indicates whether writing to the characteristic value or descriptor content requires encryption.<br>true means encryption is required for writing, false means no basic encryption is needed. Default is false. |
| writeEncryptedMitm | Bool | No | false | Indicates whether writing to the characteristic value or descriptor content requires MITM-protected encryption.<br>true means MITM-protected encryption is required for writing, false means not required. Default is false. |
| writeSigned | Bool | No | false | Indicates whether writing to the characteristic value or descriptor content requires signature processing.<br>true means signature processing is required for writing, false means not required. Default is false. |
| writeSignedMitm | Bool | No | false | Indicates whether writing to the characteristic value or descriptor content requires MITM-protected signature processing.<br>true means MITM-protected signature processing is required for writing, false means not required. Default is false. |

### func !=(GattPermissions)

```cangjie
public operator func !=(other: GattPermissions): Bool
```

**Function:** Checks inequality between GattPermissions instances.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [GattPermissions](#class-gattpermissions) | Yes | - | The permissions required for descriptor read/write operations. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the permissions for descriptor read/write operations differ, otherwise returns false. |

### func ==(GattPermissions)

```cangjie
public operator func ==(other: GattPermissions): Bool
```

**Function:** Checks equality between GattPermissions instances.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [GattPermissions](#class-gattpermissions) | Yes | - | The permissions required for descriptor read/write operations. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the permissions for descriptor read/write operations are identical, otherwise returns false. |

## class GattProperties

```cangjie
public class GattProperties {
    public var write: Bool
    public var writeNoResponse: Bool
    public var read: Bool
    public var notify: Bool
    public var indicate: Bool
    public init(
        write!: Bool = true,
        writeNoResponse!: Bool = true,
        read!: Bool = true,
        notify!: Bool = false,
        indicate!: Bool = false,
        broadcast!: Bool = false,
        authenticatedSignedWrite!: Bool = false,
        extendedProperties!: Bool = false
    )
}
```

**Function:** Describes the properties of a GATT characteristic.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var indicate

```cangjie
public var indicate: Bool
```

**Function:** **Named parameter.** true indicates the characteristic can notify peer devices and requires acknowledgment.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var notify

```cangjie
public var notify: Bool
```

**Function:** **Named parameter.** true indicates the characteristic can notify peer devices.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var read

```cangjie
public var read: Bool
```

**Function:** **Named parameter.** true indicates the characteristic supports read operations.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var write

```cangjie
public var write: Bool
```

**Function:** **Named parameter.** Indicates the characteristic supports write operations. true requires acknowledgment from peer devices.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var writeNoResponse

```cangjie
public var writeNoResponse: Bool
```

**Function:** **Named parameter.** true indicates the characteristic supports write operations without requiring acknowledgment.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(Bool, Bool, Bool, Bool, Bool, Bool, Bool, Bool)

```cangjie
public init(
    write!: Bool = true,
    writeNoResponse!: Bool = true,
    read!: Bool = true,
    notify!: Bool = false,
    indicate!: Bool = false,
    broadcast!: Bool = false,
    authenticatedSignedWrite!: Bool = false,
    extendedProperties!: Bool = false
)
```

**Function:** GattProperties constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| write | Bool | No | true | **Named parameter.** Indicates the characteristic supports write operations. true requires acknowledgment from peer devices. |
| writeNoResponse | Bool | No | true | **Named parameter.** true indicates the characteristic supports write operations without requiring acknowledgment. |
| read | Bool | No | true | **Named parameter.** true indicates the characteristic supports read operations. |
| notify | Bool | No | false | **Named parameter.** true indicates the characteristic can notify peer devices. |
| indicate | Bool | No | false | **Named parameter.** true indicates the characteristic can notify peer devices and requires acknowledgment. |
| broadcast | Bool | No | false | **Named parameter.** Indicates whether the characteristic value can be broadcast by the server.<br>true means supported (server can include characteristic value as ServiceData in advertising packets), false means not supported. Default is false. Reserved field, not supported in this version. |
| authenticatedSignedWrite | Bool | No | false | **Named parameter.** Indicates whether the characteristic supports authenticated signed writes, using signature verification instead of encryption.<br>true means supported (GattPermissions' writeSigned or writeSignedMitm must be set to true), false means not supported. Default is false. Reserved field, not supported in this version. |
| extendedProperties | Bool | No | false | **Named parameter.** Indicates whether the characteristic has extended properties.<br>true means extended properties exist, false means they don't. Default is false. Reserved field, not supported in this version. |

## class GattServer

```cangjie
public class GattServer {}
```

**Function:** Server-side class. An instance of this class must be created to use server-side methods, constructed via [createGattServer()](#func-creategattserver).

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func addService(GattService)

```cangjie
public func addService(service: GattService): Unit
```

**Function:** Adds a service on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| service | [GattService](#class-gattservice) | Yes | - | The service data for the server side. BLE advertising parameters. |

**Exceptions:**

- BusinessException: Error codes are listed below. See [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Create descriptors
let descBuffer: Array<Byte> = [31, 32]
let descriptors0 = BLEDescriptor(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    "00002902-0000-1000-8000-00805F9B34FB",
    Array<Byte>(2, repeat: 0)
)
let descriptors1 = BLEDescriptor(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    "00002903-0000-1000-8000-00805F9B34FB",
    descBuffer
)

// Create characteristics
let descriptors: Array<BLEDescriptor> = [descriptors0, descriptors1]
let charBuffer: Array<Byte> = [21, 22]
let properties = GattProperties()

let characteristic: BLECharacteristic = BLECharacteristic(
    "00001810-0000-1000-8000-00805F9B34FB",
    "00001820-0000-1000-8000-00805F9B34FB",
    charBuffer,
    descriptors,
    properties: properties
)

let characteristics: Array<BLECharacteristic> = [characteristic]
let gattService: GattService = GattService(
    "00001810-0000-1000-8000-00805F9B34FB",
    true,
    characteristics,
    includeServices: Array<GattService>()
)

try {
    // Construct gattServer
    let gattServer = createGattServer()
    gattServer.addService(gattService)
} catch (e: BusinessException) {
    Hilog.error(0, "AppLogCj", "add Service error because ${e}")
}
```### func close()

```cangjie
public func close(): Unit
```

**Function:** Closes the server functionality and deregisters the server from the protocol stack. After calling this interface, the [GattServer](#class-gattserver) instance can no longer be used.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattServer = createGattServer()
try {
    gattServer.close()
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func notifyCharacteristicChanged(String, NotifyCharacteristic)

```cangjie
public func notifyCharacteristicChanged(deviceId: String, notifyCharacteristic: NotifyCharacteristic): Unit
```

**Function:** Actively notifies connected client devices when the server-side characteristic value changes.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| deviceId | String | Yes | - | The address of the client device receiving the notification, e.g., "XX:XX:XX:XX:XX:XX". |
| notifyCharacteristic | [NotifyCharacteristic](#class-notifycharacteristic) | Yes | - | The characteristic value data to be notified. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile only -->
<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattServer = createGattServer()
try {
    let charBuffer: Array<Byte> = [21, 22]
    let notifyCharacteristic = NotifyCharacteristic(
        "00001810-0000-1000-8000-00805F9B34FB",
        "00001820-0000-1000-8000-00805F9B34FB",
        charBuffer,
        false
    )
    gattServer.notifyCharacteristicChanged("XX:XX:XX:XX:XX:XX", notifyCharacteristic)  // Replace with your deviceId
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func off(BluetoothBleGattServerCallbackType, ?CallbackObject)

```cangjie
public func off(eventType: BluetoothBleGattServerCallbackType, callback!: ?CallbackObject = None): Unit
```

**Function:** Unsubscribes from server-side events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | The callback event. |
| callback | ?[CallbackObject](../arkinterop/cj-api-callback_invoke.md#class-callbackobject) | No | None | **Named parameter.** Indicates unsubscribing from BLE events. If this parameter is not provided, all callbacks corresponding to the type will be unsubscribed. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
class StateChangeCallback <: Callback1Argument<BLEConnectionChangeState> {
    public func invoke(err: ?BusinessException, state: BLEConnectionChangeState): Unit {
        Hilog.info(0, "Bluetooth", "onGattServerStateChange: device=" + state.deviceId + ", state=" + state.state.toString())
    }
}

let stateChangeCallback = StateChangeCallback()
let gattServer = createGattServer()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.ConnectionStateChange, stateChangeCallback)
    gattServer.off(BluetoothBleGattServerCallbackType.ConnectionStateChange, callback: stateChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<CharacteristicReadRequest>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<CharacteristicReadRequest>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Set to CharacteristicRead, indicating characteristic value read request events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CharacteristicReadRequest](#class-characteristicreadrequest)> | Yes | - | Returns the MTU byte count value, obtained via the registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
let gattServer = createGattServer()

class CharacteristicReadCallback <: Callback1Argument<CharacteristicReadRequest> {
    public func invoke(err: ?BusinessException, charReq: CharacteristicReadRequest): Unit {
        let deviceId: String = charReq.deviceId
        let transId: Int32 = charReq.transId
        let offset: Int32 = charReq.offset
        Hilog.info(0, "Bluetooth", "receive characteristicRead")
        let rspBuffer: Array<Byte> = [21, 22]
        let serverResponse: ServerResponse = ServerResponse(
            deviceId,
            transId,
            0,
            offset,
            rspBuffer
        )
        try {
            gattServer.sendResponse(serverResponse)
        } catch (e: BusinessException) {
            Hilog.info(0, "Bluetooth", "gattServer send response fail because ${e}")
        }
    }
}

let characteristicReadCallback = CharacteristicReadCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.CharacteristicRead, characteristicReadCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<CharacteristicWriteRequest>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<CharacteristicWriteRequest>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Set to CharacteristicWrite, indicating characteristic value write request events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[CharacteristicWriteRequest](#class-characteristicwriterequest)> | Yes | - | Returns the MTU byte count value, obtained via the registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
let gattServer = createGattServer()

class CharacteristicWriteCallback <: Callback1Argument<CharacteristicWriteRequest> {
    public func invoke(err: ?BusinessException, charReq: CharacteristicWriteRequest): Unit {
        let deviceId: String = charReq.deviceId
        let transId: Int32 = charReq.transId
        let offset: Int32 = charReq.offset
        Hilog.info(0, "Bluetooth", "receive characteristicWrite")

        Hilog.info(0, "Bluetooth", "receive characteristicWrite: needRsp=" + charReq
            .needRsp
            .toString())
        if (!charReq.needRsp) {
            return
        }
        let rspBuffer = Array<Byte>()
        let serverResponse: ServerResponse = ServerResponse(
            deviceId,
            transId,
            0,
            offset,
            rspBuffer
        )
        try {
            gattServer.sendResponse(serverResponse)
        } catch (e: BusinessException) {
            Hilog.info(0, "Bluetooth", "gattServer send response fail because ${e}")
        }
    }
}

let characteristicWriteCallback = CharacteristicWriteCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.CharacteristicWrite, characteristicWriteCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<DescriptorReadRequest>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<DescriptorReadRequest>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Set to DescriptorRead, indicating descriptor read request events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DescriptorReadRequest](#class-descriptorreadrequest)> | Yes | - | Returns the MTU byte count value, obtained via the registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
let gattServer = createGattServer()

class DescriptorReadCallback <: Callback1Argument<DescriptorReadRequest> {
    public func invoke(err: ?BusinessException, desReq: DescriptorReadRequest): Unit {
        let deviceId: String = desReq.deviceId
        let transId: Int32 = desReq.transId
        let offset: Int32 = desReq.offset
        Hilog.info(0, "Bluetooth", "receive descriptorRead")
        let rspBuffer: Array<Byte> = [31, 32]
        let serverResponse: ServerResponse = ServerResponse(
            deviceId,
            transId,
            0,
            offset,
            rspBuffer
        )
        try {
            gattServer.sendResponse(serverResponse)
        } catch (e: BusinessException) {
            Hilog.info(0, "Bluetooth", "gattServer send response fail because ${e}")
        }
    }
}

let descriptorReadCallback = DescriptorReadCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.DescriptorRead, descriptorReadCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<DescriptorWriteRequest>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<DescriptorWriteRequest>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Set to DescriptorWrite, indicating descriptor write request events. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[DescriptorWriteRequest](#class-descriptorwriterequest)> | Yes | - | Returns the MTU byte count value, obtained via the registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// This code can be added to dependency definitions
let gattServer = createGattServer()

class DescriptorWriteCallback <: Callback1Argument<DescriptorWriteRequest> {
    public func invoke(err: ?BusinessException, desReq: DescriptorWriteRequest): Unit {
        let deviceId: String = desReq.deviceId
        let transId: Int32 = desReq.transId
        let offset: Int32 = desReq.offset
        Hilog.info(0, "Bluetooth", "receive descriptorWrite")
        Hilog.info(0, "Bluetooth", "receive descriptorWrite: needRsp=" + desReq.needRsp.toString())
        if (!desReq.needRsp) {
            return
        }
        let rspBuffer = Array<Byte>()
        let serverResponse: ServerResponse = ServerResponse(
            deviceId,
            transId,
            0,
            offset,
            rspBuffer
        )
        try {
            gattServer.sendResponse(serverResponse)
        } catch (e: BusinessException) {
            Hilog.info(0, "Bluetooth", "gattServer send response fail because ${e}")
        }
    }
}

let descriptorWriteCallback = DescriptorWriteCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.DescriptorWrite, descriptorWriteCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<BLEConnectionChangeState>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<BLEConnectionChangeState>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Set to ConnectionStateChange, indicating BLE connection state change event. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<[BLEConnectionChangeState](#class-bleconnectionchangestate)> | Yes | - | Returns the MTU byte count value, obtained via registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Code can be added in dependency definitions here
let gattServer = createGattServer()

class StateChangeCallback <: Callback1Argument<BLEConnectionChangeState> {
    public func invoke(err: ?BusinessException, state: BLEConnectionChangeState): Unit {
        Hilog.info(0, "Bluetooth", "onGattServerStateChange: device=" + state.deviceId + ", state=" + state.state.toString())
    }
}

let stateChangeCallback = StateChangeCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.ConnectionStateChange, stateChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func on(BluetoothBleGattServerCallbackType, Callback1Argument\<Int32>)

```cangjie
public func on(eventType: BluetoothBleGattServerCallbackType, callback: Callback1Argument<Int32>): Unit
```

**Function:** Subscribes to MTU state change events on the server side.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| eventType | [BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype) | Yes | - | Must be set to BLE_MTU_CHANGE, indicating MTU state change event. Incorrect setting will prevent callback registration. |
| callback | [Callback1Argument](../arkinterop/cj-api-callback_invoke.md#class-callback1argument)\<Int32> | Yes | - | Returns the MTU byte count value, obtained via registered callback function. |

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

import ohos.callback_invoke.*
import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

// Code can be added in dependency definitions here
let gattServer = createGattServer()
class BLEMtuChangeCallback <: Callback1Argument<Int32> {
    public func invoke(err: ?BusinessException, mtu: Int32): Unit {
        Hilog.info(0, "Bluetooth", "mtu change to ${mtu}")
    }
}

let bleMtuChangeCallback = BLEMtuChangeCallback()
try {
    gattServer.on(BluetoothBleGattServerCallbackType.ServerBleMtuChange, bleMtuChangeCallback)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func removeService(String)

```cangjie
public func removeService(serviceUUID: String): Unit
```

**Function:** Removes an added service.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | Service UUID, e.g., "00001810-0000-1000-8000-00805F9B34FB". |

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

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattServer = createGattServer()
try {
    gattServer.removeService("00001810-0000-1000-8000-00805F9B34FB")
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

### func sendResponse(ServerResponse)

```cangjie
public func sendResponse(serverResponse: ServerResponse): Unit
```

**Function:** Server responds to client's read/write requests.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serverResponse | ServerResponse | Yes | - | Client performs service discovery. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md) and [Bluetooth Service Subsystem Error Codes](./cj-errorcode-bluetooth_manager.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 201 | Permission denied. |
  | 801 | Capability not supported. |
  | 2900001 | Service stopped. |
  | 2900003 | Bluetooth disabled. |
  | 2900099 | Operation failed. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import ohos.business_exception.*
import kit.ConnectivityKit.*
import kit.PerformanceAnalysisKit.Hilog

let gattServer = createGattServer()
try {
    let rspBuffer = Array<Byte>()
    let serverResponse: ServerResponse = ServerResponse(
        "XX:XX:XX:XX:XX:XX'", 0, 0, 0,
        rspBuffer
    )
    gattServer.sendResponse(serverResponse)
} catch (e: BusinessException) {
    Hilog.info(0, "Bluetooth", "errCode: ${e.code}, errMessage: ${e.message}", "")
}
```

## class GattService

```cangjie
public class GattService {
    public var serviceUUID: String
    public var isPrimary: Bool
    public var characteristics: Array<BLECharacteristic>
    public var includeServices: Array<GattService>
    public init(
        serviceUUID: String,
        isPrimary: Bool,
        characteristics: Array<BLECharacteristic>,
        includeServices!: Array<GattService> = []
    )
}
```

**Function:** Interface parameter definition describing a service.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristics

```cangjie
public var characteristics: Array<BLECharacteristic>
```

**Function:** List of characteristics contained in the current service.

**Type:** Array\<[BLECharacteristic](#class-blecharacteristic)>

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var includeServices

```cangjie
public var includeServices: Array<GattService>
```

**Function:** Other services that the current service depends on.

**Type:** Array\<[GattService](#class-gattservice)>

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var isPrimary

```cangjie
public var isPrimary: Bool
```

**Function:** Set to true if it's a primary service, otherwise false.

**Type:** Bool

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, Bool, Array\<BLECharacteristic>, Array\<GattService>)

```cangjie
public init(
    serviceUUID: String,
    isPrimary: Bool,
    characteristics: Array<BLECharacteristic>,
    includeServices!: Array<GattService> = []
)
```

**Function:** GattService constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | UUID of a specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb". |
| isPrimary | Bool | Yes | - | Set to true if it's a primary service, otherwise false. |
| characteristics | Array\<[BLECharacteristic](#class-blecharacteristic)> | Yes | - | List of characteristics contained in the current service. |
| includeServices | Array\<[GattService](#class-gattservice)> | No | [] | Other services that the current service depends on. |

## class ManufactureData

```cangjie
public class ManufactureData {
    public var manufactureId: UInt16
    public var manufactureValue: Array<Byte>
    public init(
        manufactureId: UInt16,
        manufactureValue: Array<Byte>
    )
}
```

**Function:** Describes the content of a BLE broadcast data packet.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureId

```cangjie
public var manufactureId: UInt16
```

**Function:** Manufacturer ID assigned by Bluetooth SIG.

**Type:** UInt16

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureValue

```cangjie
public var manufactureValue: Array<Byte>
```

**Function:** Manufacturer data sent by the manufacturer.

**Type:** Array\<Byte>

**Read/Write Capability:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(UInt16, Array\<Byte>)

```cangjie
public init(
    manufactureId: UInt16,
    manufactureValue: Array<Byte>
)
```

**Function:** ManufactureData constructor.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| manufactureId | UInt16 | Yes | - | Manufacturer ID assigned by Bluetooth SIG. |
| manufactureValue | Array\<Byte> | Yes | - | Manufacturer data sent by the manufacturer. |## class NotifyCharacteristic

```cangjie
public class NotifyCharacteristic {
    public var serviceUUID: String
    public var characteristicUUID: String
    public var characteristicValue: Array<Byte>
    public var confirm: Bool
    public init(
        serviceUUID: String,
        characteristicUUID: String,
        characteristicValue: Array<Byte>,
        confirm: Bool
    )
}
```

**Function:** Defines the characteristic notification parameters when server-side characteristic values change.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicUUID

```cangjie
public var characteristicUUID: String
```

**Function:** UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var characteristicValue

```cangjie
public var characteristicValue: Array<Byte>
```

**Function:** Binary value corresponding to the characteristic.

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var confirm

```cangjie
public var confirm: Bool
```

**Function:** Set to `true` if it's an indication requiring peer confirmation; set to `false` if it's a notification not requiring peer confirmation.

**Type:** Bool

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, String, Array\<Byte>, Bool)

```cangjie
public init(
    serviceUUID: String,
    characteristicUUID: String,
    characteristicValue: Array<Byte>,
    confirm: Bool
)
```

**Function:** Constructor for NotifyCharacteristic.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | UUID of the specific service, e.g., "00001888-0000-1000-8000-00805f9b34fb". |
| characteristicUUID | String | Yes | - | UUID of the specific characteristic, e.g., "00002a11-0000-1000-8000-00805f9b34fb". |
| characteristicValue | Array\<Byte> | Yes | - | Binary value corresponding to the characteristic. |
| confirm | Bool | Yes | - | Set to `true` for indication (requires confirmation); `false` for notification (no confirmation required). |

## class ScanFilter

```cangjie
public class ScanFilter {
    public var deviceId: String
    public var name: String
    public var serviceUUID: String
    public var serviceUuidMask: String
    public var serviceSolicitationUuid: String
    public var serviceSolicitationUuidMask: String
    public var serviceData: Array<Byte>
    public var serviceDataMask: Array<Byte>
    public var manufactureId: UInt16
    public var manufactureData: Array<Byte>
    public var manufactureDataMask: Array<Byte>
    public init(
        deviceId!: String = "",
        name!: String = "",
        serviceUUID!: String = "",
        serviceUuidMask!: String = "",
        serviceSolicitationUuid!: String = "",
        serviceSolicitationUuidMask!: String = "",
        serviceData!: Array<Byte> = [],
        serviceDataMask!: Array<Byte> = [],
        manufactureId!: UInt16 = 0,
        manufactureData!: Array<Byte> = [],
        manufactureDataMask!: Array<Byte> = []
    )
}
```

**Function:** Scan filtering parameters.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Filters BLE device addresses, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureData

```cangjie
public var manufactureData: Array<Byte>
```

**Function:** Filters devices containing specified manufacturer data, e.g., [0x1F,0x2F,0x3F].

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureDataMask

```cangjie
public var manufactureDataMask: Array<Byte>
```

**Function:** Filters devices using manufacturer data mask, e.g., [0xFF,0xFF,0xFF].

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var manufactureId

```cangjie
public var manufactureId: UInt16
```

**Function:** Filters devices containing specified manufacturer ID, e.g., 0x0006.

**Type:** UInt16

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var name

```cangjie
public var name: String
```

**Function:** Filters BLE device names.

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceData

```cangjie
public var serviceData: Array<Byte>
```

**Function:** Filters devices containing specified service data, e.g., [0x90,0x00,0xF1,0xF2].

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceDataMask

```cangjie
public var serviceDataMask: Array<Byte>
```

**Function:** Filters devices using service data mask, e.g., [0xFF,0xFF,0xFF,0xFF].

**Type:** Array\<Byte>

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceSolicitationUUID

```cangjie
public var serviceSolicitationUUID: String
```

**Function:** Filters devices containing specified service solicitation UUID, e.g., "00001888-0000-1000-8000-00805F9B34FB".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceSolicitationUUIDMask

```cangjie
public var serviceSolicitationUUIDMask: String
```

**Function:** Filters devices using service solicitation UUID mask, e.g., "FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** Filters devices containing specified service UUID, e.g., "00001888-0000-1000-8000-00805f9b34fb".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUIDMask

```cangjie
public var serviceUUIDMask: String
```

**Function:** Filters devices using service UUID mask, e.g., "FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF".

**Type:** String

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, String, String, String, String, String, Array\<Byte>, Array\<Byte>, UInt16, Array\<Byte>, Array\<Byte>)

```cangjie
public init(
    deviceId!: String = "",
    name!: String = "",
    serviceUUID!: String = "",
    serviceUuidMask!: String = "",
    serviceSolicitationUuid!: String = "",
    serviceSolicitationUuidMask!: String = "",
    serviceData!: Array<Byte> = [],
    serviceDataMask!: Array<Byte> = [],
    manufactureId!: UInt16 = 0,
    manufactureData!: Array<Byte> = [],
    manufactureDataMask!: Array<Byte> = []
)
```

**Function:** Creates a ScanFilter structure for scan filtering parameters.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| deviceId | String | No | "" | **Named parameter.** Filters BLE device addresses, e.g., "XX:XX:XX:XX:XX:XX". Reserved field, not supported in this version. |
| name | String | No | "" | **Named parameter.** Filters BLE device names. Reserved field, not supported in this version. |
| serviceUUID | String | No | "" | **Named parameter.** Filters devices containing specified service UUID, e.g., "00001888-0000-1000-8000-00805f9b34fb". Reserved field, not supported in this version. |
| serviceUuidMask | String | No | "" | **Named parameter.** Used with serviceUUID filter to partially match service UUIDs, e.g., "FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF". Reserved field, not supported in this version. |
| serviceSolicitationUuid | String | No | "" | **Named parameter.** Filters devices containing specified service solicitation UUID, e.g., "00001888-0000-1000-8000-00805F9B34FB". Reserved field, not supported in this version. |
| serviceSolicitationUuidMask | String | No | "" | **Named parameter.** Used with serviceSolicitationUuid filter to partially match service solicitation UUIDs, e.g., "FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF". Reserved field, not supported in this version. |
| serviceData | Array\<Byte> | No | [] | **Named parameter.** Filters devices containing specified service data, e.g., [0x90,0x00,0xF1,0xF2]. Reserved field, not supported in this version. |
| serviceDataMask | Array\<Byte> | No | [] | **Named parameter.** Used with serviceData filter to partially match service data, e.g., [0xFF,0xFF,0xFF,0xFF]. Reserved field, not supported in this version. |
| manufactureId | UInt16 | No | 0 | **Named parameter.** Filters devices containing specified manufacturer ID, e.g., 0x0006. Reserved field, not supported in this version. |
| manufactureData | Array\<Byte> | No | [] | **Named parameter.** Used with manufactureId filter to match manufacturer data, e.g., [0x1F,0x2F,0x3F]. Reserved field, not supported in this version. |
| manufactureDataMask | Array\<Byte> | No | [] | **Named parameter.** Used with manufactureData filter to partially match manufacturer data, e.g., [0xFF,0xFF,0xFF]. Reserved field, not supported in this version. |

## class ScanOptions

```cangjie
public class ScanOptions {
    public var interval: Int32
    public var dutyMode: ScanDuty
    public var matchMode: MatchMode
    public var phyType: PhyType
    public init(
        interval!: Int32 = 0,
        dutyMode!: ScanDuty = ScanModeLowPower,
        matchMode!: MatchMode = MatchModeAggressive,
        phyType!: PhyType = PhyLe1M,
        reportMode!: ScanReportMode = Normal
    )
}
```

**Function:** Configuration parameters for scanning.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var dutyMode

```cangjie
public var dutyMode: ScanDuty
```

**Function:** Scanning mode, default is ScanDuty.ScanModeLowPower.

**Type:** [ScanDuty](#enum-scanduty)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var interval

```cangjie
public var interval: Int32
```

**Function:** Delay time for reporting scan results, default is 0.

**Type:** Int32

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var matchMode

```cangjie
public var matchMode: MatchMode
```

**Function:** Hardware filtering match mode, default is MatchMode.MatchModeAggressive.

**Type:** [MatchMode](#enum-matchmode)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var phyType

```cangjie
public var phyType: PhyType
```

**Function:** PHY type used during scanning.

**Type:** [PhyType](#enum-phytype)

**Access:** Read-Write

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(Int32, ScanDuty, MatchMode, PhyType, ScanReportMode)

```cangjie
public init(
    interval!: Int32 = 0,
    dutyMode!: ScanDuty = ScanModeLowPower,
    matchMode!: MatchMode = MatchModeAggressive,
    phyType!: PhyType = PhyLe1M,
    reportMode!: ScanReportMode = Normal
)
```

**Function:** Creates a ScanOptions structure for scan configuration parameters.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| interval | Int32 | No | 0 | **Named parameter.** Delay time for reporting scan results, initial value is 0. |
| dutyMode | [ScanDuty](#enum-scanduty) | No | ScanModeLowPower | **Named parameter.** Scanning mode, initial value is ScanDuty.ScanModeLowPower. |
| matchMode | [MatchMode](#enum-matchmode) | No | MatchModeAggressive | **Named parameter.** Hardware filtering match mode, initial value is MatchMode.MatchModeAggressive. |
| phyType | [PhyType](#enum-phytype) | No | PhyLe1M | **Named parameter.** PHY type used during scanning. |
| reportMode | [ScanReportMode](#enum-scanreportmode) | No | Normal | **Named parameter.** Scan result data reporting mode, default is NORMAL. |## class ScanResult

```cangjie
public class ScanResult {
    public var deviceId: String
    public var rssi: Int32
    public var data: Array<Byte>
    public var deviceName: String
    public var connectable: Bool
}
```

**Function:** Data reported for scan results.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var connectable

```cangjie
public var connectable: Bool
```

**Function:** Indicates whether the scanned device is connectable. true means connectable, false means not connectable.

**Type:** Bool

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var data

```cangjie
public var data: Array<Byte>
```

**Function:** Represents the broadcast packet sent by the scanned device.

**Type:** Array\<Byte>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the address of the scanned device, e.g., "XX:XX:XX:XX:XX:XX". For information security considerations, the device address obtained here is a random MAC address. This address will not change after successful pairing; however, the random address will change when a paired device is unpaired and rescanned or when the Bluetooth service is powered off.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceName

```cangjie
public var deviceName: String
```

**Function:** Represents the name of the scanned device.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var rssi

```cangjie
public var rssi: Int32
```

**Function:** Represents the RSSI value of the scanned device.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

## class ServerResponse

```cangjie
public class ServerResponse {
    public var deviceId: String
    public var transId: Int32
    public var status: Int32
    public var offset: Int32
    public var value: Array<Byte>
    public init(
        deviceId: String,
        transId: Int32,
        status: Int32,
        offset: Int32,
        value: Array<Byte>
    )
}
```

**Function:** Describes the response parameters class for the server's reply to the client's read/write requests.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var deviceId

```cangjie
public var deviceId: String
```

**Function:** Represents the remote device address, e.g., "XX:XX:XX:XX:XX:XX".

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var offset

```cangjie
public var offset: Int32
```

**Function:** Represents the starting position of the read/write request, consistent with the offset carried in the subscribed read/write request event.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var status

```cangjie
public var status: Int32
```

**Function:** Represents the response status. Set to 0 to indicate normal.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var transId

```cangjie
public var transId: Int32
```

**Function:** Represents the transaction ID of the request, consistent with the ID carried in the subscribed read/write request event.

**Type:** Int32

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var value

```cangjie
public var value: Array<Byte>
```

**Function:** Represents the binary data of the response.

**Type:** Array\<Byte>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, Int32, Int32, Int32, Array\<Byte>)

```cangjie
public init(
    deviceId: String,
    transId: Int32,
    status: Int32,
    offset: Int32,
    value: Array<Byte>
)
```

**Function:** Describes the response parameters class for the server's reply to the client's read/write requests.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| deviceId | String | Yes | - | Represents the remote device address, e.g., "XX:XX:XX:XX:XX:XX". |
| transId | Int32 | Yes | - | Represents the transaction ID of the request, consistent with the ID carried in the subscribed read/write request event. |
| status | Int32 | Yes | - | Represents the response status. Set to 0 to indicate normal. |
| offset | Int32 | Yes | - | Represents the starting position of the read/write request, consistent with the offset carried in the subscribed read/write request event. |
| value | Array\<Byte> | Yes | - | Represents the binary data of the response. |

## class ServiceData

```cangjie
public class ServiceData {
    public var serviceUUID: String
    public var serviceValue: Array<Byte>
    public init(
        serviceUUID: String,
        serviceValue: Array<Byte>
    )
}
```

**Function:** Describes the service data content in the broadcast packet.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceUUID

```cangjie
public var serviceUUID: String
```

**Function:** Represents the UUID of the service.

**Type:** String

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### var serviceValue

```cangjie
public var serviceValue: Array<Byte>
```

**Function:** Represents the service data.

**Type:** Array\<Byte>

**Read/Write Permission:** Readable and Writable

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### init(String, Array\<Byte>)

```cangjie
public init(
    serviceUUID: String,
    serviceValue: Array<Byte>
)
```

**Function:** Describes the service data content in the broadcast packet.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| serviceUUID | String | Yes | - | Represents the UUID of the service. |
| serviceValue | Array\<Byte> | Yes | - | Represents the service data. |

## enum AdvertisingState

```cangjie
public enum AdvertisingState <: Equatable<AdvertisingState> & ToString {
    | Started
    | Enabled
    | Disabled
    | Stopped
    | ...
}
```

**Function:** Advertising state.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<AdvertisingState>
- ToString

### Disabled

```cangjie
Disabled
```

**Function:** Represents the state after temporarily stopping advertising.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### Enabled

```cangjie
Enabled
```

**Function:** Represents the state after temporarily starting advertising.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### Started

```cangjie
Started
```

**Function:** Represents the state after initially starting advertising.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### Stopped

```cangjie
Stopped
```

**Function:** Represents the state after completely stopping advertising.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(AdvertisingState)

```cangjie
public operator func !=(other: AdvertisingState): Bool
```

**Function:** Determines whether two enum values are not equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AdvertisingState](#enum-advertisingstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are not equal, otherwise returns false. |

### func ==(AdvertisingState)

```cangjie
public operator func ==(other: AdvertisingState): Bool
```

**Function:** Determines whether two enum values are equal.

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| other | [AdvertisingState](#enum-advertisingstate) | Yes | - | Another enum value. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns true if the two enum values are equal, otherwise returns false. |

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the value of the enum.

**Return Value:**

| Type | Description |
|:----|:----|
| String | The description of the enum. |## enum BluetoothBleCallbackType

```cangjie
public enum BluetoothBleCallbackType <: Equatable<BluetoothBleCallbackType> & Hashable & ToString {
    | AdvertisingStateChange
    | BleDeviceFind
    | ...
}
```

**Description:** Broadcast scanning subscription event types.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<BluetoothBleCallbackType>
- Hashable
- ToString

### AdvertisingStateChange

```cangjie
AdvertisingStateChange
```

**Description:** Indicates the broadcast state event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### BleDeviceFind

```cangjie
BleDeviceFind
```

**Description:** Indicates the BLE device discovery event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(BluetoothBleCallbackType)

```cangjie
public operator func !=(other: BluetoothBleCallbackType): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleCallbackType](#enum-bluetoothblecallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are unequal, otherwise returns false.|

### func ==(BluetoothBleCallbackType)

```cangjie
public operator func ==(other: BluetoothBleCallbackType): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleCallbackType](#enum-bluetoothblecallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Description:** Obtains the hash value of the input data.

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|The hash value of the data.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The description of the enumeration.|

## enum BluetoothBleGattClientDeviceCallbackType

```cangjie
public enum BluetoothBleGattClientDeviceCallbackType <: Equatable<BluetoothBleGattClientDeviceCallbackType> & Hashable & ToString {
    | BleCharacteristicChange
    | BleConnectionStateChange
    | ClientBleMtuChange
    | ...
}
```

**Description:** Types of client on/off events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<BluetoothBleGattClientDeviceCallbackType>
- Hashable
- ToString

### BleCharacteristicChange

```cangjie
BleCharacteristicChange
```

**Description:** Indicates the characteristic value change event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### BleConnectionStateChange

```cangjie
BleConnectionStateChange
```

**Description:** Indicates the connection state change event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ClientBleMtuChange

```cangjie
ClientBleMtuChange
```

**Description:** Indicates the MTU state change event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(BluetoothBleGattClientDeviceCallbackType)

```cangjie
public operator func !=(other: BluetoothBleGattClientDeviceCallbackType): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are unequal, otherwise returns false.|

### func ==(BluetoothBleGattClientDeviceCallbackType)

```cangjie
public operator func ==(other: BluetoothBleGattClientDeviceCallbackType): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleGattClientDeviceCallbackType](#enum-bluetoothblegattclientdevicecallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Description:** Obtains the hash value of the input data.

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|The hash value of the data.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The description of the enumeration.|

## enum BluetoothBleGattServerCallbackType

```cangjie
public enum BluetoothBleGattServerCallbackType <: Equatable<BluetoothBleGattServerCallbackType> & Hashable & ToString {
    | CharacteristicRead
    | CharacteristicWrite
    | DescriptorRead
    | DescriptorWrite
    | ConnectionStateChange
    | ServerBleMtuChange
    | ...
}
```

**Description:** Types of server on/off events.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<BluetoothBleGattServerCallbackType>
- Hashable
- ToString

### CharacteristicRead

```cangjie
CharacteristicRead
```

**Description:** Indicates the characteristic read request event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### CharacteristicWrite

```cangjie
CharacteristicWrite
```

**Description:** Indicates the characteristic write request event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ConnectionStateChange

```cangjie
ConnectionStateChange
```

**Description:** Indicates the BLE connection state change event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### DescriptorRead

```cangjie
DescriptorRead
```

**Description:** Indicates the descriptor read request event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### DescriptorWrite

```cangjie
DescriptorWrite
```

**Description:** Indicates the descriptor write request event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ServerBleMtuChange

```cangjie
ServerBleMtuChange
```

**Description:** Indicates the MTU state change event type.

**Required Permission:** ohos.permission.ACCESS_BLUETOOTH

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(BluetoothBleGattServerCallbackType)

```cangjie
public operator func !=(other: BluetoothBleGattServerCallbackType): Bool
```

**Description:** Determines whether two enumeration values are unequal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are unequal, otherwise returns false.|

### func ==(BluetoothBleGattServerCallbackType)

```cangjie
public operator func ==(other: BluetoothBleGattServerCallbackType): Bool
```

**Description:** Determines whether two enumeration values are equal.

**Parameters:**

|Name|Type|Mandatory|Default Value|Description|
|:---|:---|:---|:---|:---|
|other|[BluetoothBleGattServerCallbackType](#enum-bluetoothblegattservercallbacktype)|Yes|-|Another enumeration value.|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enumeration values are equal, otherwise returns false.|

### func hashCode()

```cangjie
public func hashCode(): Int64
```

**Description:** Obtains the hash value of the input data.

**Return Value:**

|Type|Description|
|:----|:----|
|Int64|The hash value of the data.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Obtains the value of the enumeration.

**Return Value:**

|Type|Description|
|:----|:----|
|String|The description of the enumeration.

## enum GattWriteType

```cangjie
public enum GattWriteType <: Equatable<GattWriteType> & ToString {
    | Write
    | WriteNoResponse
    | ...
}
```

**Description:** Represents GATT write types.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<GattWriteType>
- ToString

### Write

```cangjie
Write
```

**Description:** Indicates writing characteristic values that require a response from the peer device.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### WriteNoResponse

```cangjie
WriteNoResponse
```

**Description:** Indicates writing characteristic values that do not require a response from the peer device.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(GattWriteType)

```cangjie
public operator func !=(other: GattWriteType): Bool
```

**Description:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[GattWriteType](#enum-gattwritetype)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise returns false.|

### func ==(GattWriteType)

```cangjie
public operator func ==(other: GattWriteType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[GattWriteType](#enum-gattwritetype)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Returns:**

|Type|Description|
|:----|:----|
|String|The description of the enum.|

## enum MatchMode

```cangjie
public enum MatchMode <: Equatable<MatchMode> & ToString {
    | MatchModeAggressive
    | MatchModeSticky
    | ...
}
```

**Description:** Hardware filter matching modes.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<MatchMode>
- ToString

### MatchModeAggressive

```cangjie
MatchModeAggressive
```

**Description:** Indicates a lower threshold for hardware reporting scan results, such as reporting even when the scanned power is low or the number of scans is small within a period. This is the default value.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### MatchModeSticky

```cangjie
MatchModeSticky
```

**Description:** Indicates a higher threshold for hardware reporting scan results, requiring higher power thresholds and multiple scans before reporting.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(MatchMode)

```cangjie
public operator func !=(other: MatchMode): Bool
```

**Description:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MatchMode](#enum-matchmode)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise returns false.|

### func ==(MatchMode)

```cangjie
public operator func ==(other: MatchMode): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[MatchMode](#enum-matchmode)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Returns:**

|Type|Description|
|:----|:----|
|String|The description of the enum.|

## enum PhyType

```cangjie
public enum PhyType <: Equatable<PhyType> & ToString {
    | PhyLe1M
    | PhyLeAllSupported
    | ...
}
```

**Description:** Broadcast status.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<PhyType>
- ToString

### PhyLe1M

```cangjie
PhyLe1M
```

**Description:** Broadcast status.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### PhyLeAllSupported

```cangjie
PhyLeAllSupported
```

**Description:** Indicates using all PHY modes supported by the Bluetooth protocol during scanning.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(PhyType)

```cangjie
public operator func !=(other: PhyType): Bool
```

**Description:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PhyType](#enum-phytype)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise returns false.|

### func ==(PhyType)

```cangjie
public operator func ==(other: PhyType): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[PhyType](#enum-phytype)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Returns:**

|Type|Description|
|:----|:----|
|String|The description of the enum.|

## enum ScanDuty

```cangjie
public enum ScanDuty <: Equatable<ScanDuty> & ToString {
    | ScanModeLowPower
    | ScanModeBalanced
    | ScanModeLowLatency
    | ...
}
```

**Description:** Scan modes.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<ScanDuty>
- ToString

### ScanModeBalanced

```cangjie
ScanModeBalanced
```

**Description:** Indicates balanced mode.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ScanModeLowLatency

```cangjie
ScanModeLowLatency
```

**Description:** Indicates low-latency mode.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### ScanModeLowPower

```cangjie
ScanModeLowPower
```

**Description:** Indicates low-power mode, which is the default value.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(ScanDuty)

```cangjie
public operator func !=(other: ScanDuty): Bool
```

**Description:** Determines whether two enum values are not equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScanDuty](#enum-scanduty)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are not equal, otherwise returns false.|

### func ==(ScanDuty)

```cangjie
public operator func ==(other: ScanDuty): Bool
```

**Description:** Determines whether two enum values are equal.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScanDuty](#enum-scanduty)|Yes|-|Another enum value.|

**Returns:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the two enum values are equal, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Description:** Gets the value of the enum.

**Returns:**

|Type|Description|
|:----|:----|
|String|The description of the enum.|## enum ScanReportMode

```cangjie
public enum ScanReportMode <: Equatable<ScanReportMode> & ToString {
    | Normal
    | Batch
    | FenceSensitivityLow
    | FenceSensitivityHigh
    | ...
}
```

**Function:** Reporting mode for scanned data.

- This mode reduces the frequency of Bluetooth chip reporting scan results, allowing the system to remain in sleep state for longer periods, thereby lowering overall power consumption.

- In this mode, when a BLE advertisement packet matching the filter conditions is detected, it is not immediately reported. Instead, it is cached for a period (specified by the interval field in ScanOptions) before being reported.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

**Parent Types:**

- Equatable\<ScanReportMode>
- ToString

### Batch

```cangjie
Batch
```

**Function:** Batch scan reporting mode.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### FenceSensitivityHigh

```cangjie
FenceSensitivityHigh
```

**Function:** High-sensitivity fence reporting mode.

- Fence mode indicates reporting only when advertisements enter or leave the fence.

- When the scanned advertisement signal strength is low and the number of advertisements is small, high-sensitivity fence mode can be activated.

- The first detection of an advertisement enters the fence, triggering one report.

- If no advertisements are detected for a period of time, it leaves the fence, triggering one report.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### FenceSensitivityLow

```cangjie
FenceSensitivityLow
```

**Function:** Low-sensitivity fence reporting mode.

- Fence mode indicates reporting only when advertisements enter or leave the fence.

- When the scanned advertisement signal strength is high and the number of advertisements is large, low-sensitivity fence mode can be activated.

- The first detection of an advertisement enters the fence, triggering one report.

- If no advertisements are detected for a period of time, it leaves the fence, triggering one report.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### Normal

```cangjie
Normal
```

**Function:** Normal scan reporting mode. When a BLE advertisement packet matching the filter conditions is detected, it is immediately reported.

**System Capability:** SystemCapability.Communication.Bluetooth.Core

**Since:** 22

### func !=(ScanReportMode)

```cangjie
public operator func !=(other: ScanReportMode): Bool
```

**Function:** Determines inequality between scan reporting modes.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScanReportMode](#enum-scanreportmode)|Yes|-|Scan result data reporting mode|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the scan result data reporting modes are different, otherwise returns false.|

### func ==(ScanReportMode)

```cangjie
public operator func ==(other: ScanReportMode): Bool
```

**Function:** Determines equality between scan reporting modes.

**Parameters:**

|Parameter|Type|Required|Default|Description|
|:---|:---|:---|:---|:---|
|other|[ScanReportMode](#enum-scanreportmode)|Yes|-|Scan result data reporting mode|

**Return Value:**

|Type|Description|
|:----|:----|
|Bool|Returns true if the scan result data reporting modes are the same, otherwise returns false.|

### func toString()

```cangjie
public func toString(): String
```

**Function:** Gets the string representation of the scan result data reporting mode.

**Return Value:**

|Type|Description|
|:----|:----|
|String|String representation of the scan result data reporting mode.|