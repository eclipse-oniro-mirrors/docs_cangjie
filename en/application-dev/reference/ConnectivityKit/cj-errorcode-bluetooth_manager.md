# Bluetooth Service Subsystem Error Codes

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

Turn Bluetooth back on and retry the pairing process.

## 2900006

**Error Message**

The maximum number of connections has been reached.

**Error Description**

Exceeded the maximum number of connections.

**Possible Causes**

Exceeded the device's maximum connection limit.

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

Turn Bluetooth back on and retry the pairing process.

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

## 2901054

**Error Message**

IO error.

**Error Description**

IO transmission failed.

**Possible Causes**

IO transmission exception caused the failure.

**Resolution Steps**

Retry the operation.