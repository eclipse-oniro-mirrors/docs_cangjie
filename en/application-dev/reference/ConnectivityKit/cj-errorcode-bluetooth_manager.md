# Bluetooth Service Subsystem Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 2900001

**Error Message**

Service stopped.

**Error Description**

The Bluetooth service has stopped, and Bluetooth service-related interfaces cannot be called.

**Possible Causes**

Abnormal Bluetooth service startup.

**Resolution Steps**

Retry turning Bluetooth on or off.

## 2900003

**Error Message**

Bluetooth disabled.

**Error Description**

Bluetooth is turned off.

**Possible Causes**

Bluetooth is turned off.

**Resolution Steps**

Retry turning Bluetooth on.

## 2900004

**Error Message**

Profile not supported.

**Error Description**

The profile is not supported.

**Possible Causes**

The profile is not supported in the current device environment.

**Resolution Steps**

Check whether the device supports the profile functionality. If not, stop calling it.

## 2900005

**Error Message**

Device not connected.

**Error Description**

The device is not connected via Bluetooth.

**Possible Causes**

Abnormal device pairing.

**Resolution Steps**

Turn Bluetooth off and on again, then perform the pairing process.

## 2900006

**Error Message**

The maximum number of connections has been reached.

**Error Description**

Exceeded the maximum number of connections.

**Possible Causes**

The maximum number of connections for the device has been exceeded.

**Resolution Steps**

Check the number of paired devices to see if it exceeds the threshold.

## 2900008

**Error Message**

The value of proxy is a null pointer.

**Error Description**

pimpl or proxy is null.

**Possible Causes**

Abnormal device pairing.

**Resolution Steps**

Turn Bluetooth off and on again, then perform the pairing process.

## 2900009

**Error Message**

Fails to start scan as it is out of hardware resources.

**Description**

Starting a scan fails due to insufficient hardware resources.

**Possible Causes**

An excessive number of scan channels have been activated by this application or other applications, resulting in insufficient hardware resources.

**Solution**

If this application has never started a scan, you can turn Bluetooth off and then back on to release the scanning resources occupied by other applications.

If this application has already started a scan on another channel, you can call the **stopScan** API to halt the scan. After the hardware resources are released, restart the current scan.

## 2900010

**Error Message**

Resources have reached the upper limit.

**Description**

This error code is reported if resource usage reaches the upper limit.

**Possible Causes**

The application applies for too many resources.

**Solution**

Call the corresponding API to release resources.

## 2900013

**Error Message**

The user does not respond.

**Description**

This error code is reported if the user does not respond to the preprocessing operation.

**Possible Causes**

The user does not perform the required operation within a specified period of time. As a result, the preprocessing operation times out.

**Solution**

Perform the preprocessing operation again.

## 2900014

**Error Message**

User refuse the action.

**Description**

This error code is reported if the user rejects the preprocessing operation.

**Possible Causes**

The user rejects the preprocessing operation.

**Solution**

Perform the preprocessing operation again.

## 2900099

**Error Message**

Operation failed.

**Error Description**

Operation failed.

**Possible Causes**

The profile is not supported in the current device environment.

**Resolution Steps**

Retry the operation.

## 2900100

**Error Message**

IPC failed.

**Error Description**

IPC data transmission failed.

**Possible Causes**

Abnormal data input.

**Resolution Steps**

Check the input data.

## 2901000

**Error Message**

Read forbidden.

**Error Description**

Read operation is forbidden.

**Possible Causes**

No read operation permission.

**Resolution Steps**

Check whether read operation permission is granted.

## 2901001

**Error Message**

Write forbidden.

**Error Description**

Write operation is forbidden.

**Possible Causes**

No write operation permission.

**Resolution Steps**

Check whether write operation permission is granted.

## 2901003

**Error Message**

The connection is not established.

**Description**

This error code is reported if the GATT connection is not established.

**Possible Causes**

An API call is invoked when the GATT connection is not established, for example, [getServices](./cj-apis-bluetooth-ble.md#func-getservicesasynccallbackarraygattservice) or [readCharacteristicValue](./cj-apis-bluetooth-ble.md#func-readcharacteristicvalueblecharacteristic-asynccallbackblecharacteristic) is called.

**Solution**

Ensure that the GATT connection is established.

## 2901004

**Error Message**

The connection is congested.

**Description**

This error code is reported if the GATT connection is congested.

**Possible Causes**

Characteristic or descriptor read and write operations are performed frequently, causing congestion in underlying data transmission. For example, if the [writeCharacteristicValue](./cj-apis-bluetooth-ble.md#func-writecharacteristicvalueblecharacteristic-gattwritetype-asynccallbackunit) API is frequently called with [GattWriteType](./cj-apis-bluetooth-ble.md#enum-gattwritetype) being set as **WriteNoResponse**, congestion may occur.

**Solution**

Reduce the frequency of read and write operations. If **GattWriteType** is set to **WriteNoResponse**, the recommended interval is greater than 50 ms.

## 2901005

**Error Message**

The connection is not encrypted.

**Description**

This error code is reported if characteristic or descriptor read and write operations requiring the encryption permission is performed when the GATT connection is not encrypted. Whether encryption is required for the operation is subject to the permission of the characteristic or descriptor on the server.

**Possible Causes**

The GATT encryption permission is not available.

**Solution**

Check whether the encryption permission is available for the GATT connection.

## 2901006

**Error Message**

The connection is not authenticated.

**Description**

This error code is reported if characteristic or descriptor read and write operations requiring authentication is performed when the GATT connection is not authenticated. Whether authentication is required for the operation is subject to the permission of the characteristic or descriptor on the server.

**Possible Causes**

The GATT connection is not authenticated.

**Solution**

Check whether the device is paired with the peer device and whether the GATT connection is authenticated.

## 2901007

**Error Message**

The connection is not authorized.

**Description**

This error code is reported if characteristic or descriptor read and write operations requiring authorization is performed when the GATT connection is not authorized. Whether authorization is required for the operation is subject to the permission of the characteristic or descriptor on the server.

**Possible Causes**

The GATT connection is not authorized.

**Solution**

Check whether the GATT connection is authorized.

## 2901008

**Error Message**

GATT service is not found.

**Description**

The GATT service does not exist. Before obtaining the specified GATT service, ensure that the service has been added.

**Possible Causes**

The GATT service has not been added.

**Solution**

Call [addService](./cj-apis-bluetooth-ble.md#func-addservicegattservice) to add the service.

## 2901054

**Error Message**

IO error.

**Error Description**

IO transmission failed.

**Possible Causes**

IO transmission exception caused the failure.

**Resolution Steps**

Retry the operation.

## 2902050

**Error Message**

Failed to start scan as Ble scan is already started by the app.

**Description**

This error code is reported if the attempt to enable scanning fails.

**Possible Causes**

BLE scanning has been enabled.

**Solution**

Check whether scanning is enabled.

## 2902054

**Error Message**

The length of the advertising data exceeds the upper limit.

**Description**

This error code is reported if the length of the advertising data exceeds the upper limit.

**Possible Causes**

The maximum length of traditional advertising packets is 31 bytes. If the maximum length is exceeded, an exception is returned. Currently, this length limit applies only to traditional advertising but not extended advertising.

**Solution**

Check whether the length of the advertising packet exceeds the upper limit.

## 2902055

**Error Message**

Invalid advertising id.

**Description**

This error code is reported if the advertising ID is invalid.

**Possible Causes**

The input advertising ID must be the value returned by [startAdvertising](./cj-apis-bluetooth-ble.md#func-startadvertisingadvertisingparams). The invalid advertising ID is **0xFF** by default.

**Solution**

Check whether the input advertising ID is a valid advertising ID returned by [startAdvertising](./cj-apis-bluetooth-ble.md#func-startadvertisingadvertisingparams).
