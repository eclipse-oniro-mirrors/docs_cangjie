# Network Connection Management Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 2100001 Invalid Parameter Value

**Error Message**

Invalid parameter value.

**Error Description**

Invalid parameter value.

**Possible Causes**

The input parameter value is out of range.

**Solution**

Check whether the input parameter value is within the correct range.

## 2100002 Failed to Connect to Service

**Error Message**

Operation failed. Cannot connect to service.

**Error Description**

Operation failed due to an exception when connecting to the system service.

**Possible Causes**

The service encountered an exception.

**Solution**

Check whether the system service is running normally.

## 2100003 System Internal Error

**Error Message**

System internal error.

**Error Description**

System internal error.

**Possible Causes**

1. Memory exception.  
2. Null pointer.

**Solution**

1. Check whether the memory space is sufficient. Free up memory and try again.  
2. System exception. Please try again later or restart the device.

## 2101007 Duplicate Callback Exists

**Error Message**

The same callback exists.

**Error Description**

A callback has already been registered.

**Possible Causes**

When activating & monitoring a specified network property and registering a callback, the callback object was registered repeatedly.

**Solution**

1. Ensure that the callback object to be registered has not been registered before.  
2. If the callback object has already been registered, use the existing registration.

## 2101008 Callback Does Not Exist

**Error Message**

The callback is not exists.

**Error Description**

The callback object does not exist.

**Possible Causes**

The request to activate & monitor a specified network property and register a callback was not executed.

**Solution**

Check the callback object to ensure that the deregistration function is called only after the registration function has been executed.

## 2101022 Maximum Number of Requests Exceeded

**Error Message**

The number of requests exceeded the maximum.

**Error Description**

The number of network requests exceeded the maximum limit.

**Possible Causes**

The number of requests to activate & monitor a specified network property exceeded the maximum limit.

**Solution**

It is recommended to locate the issue through the log message "Over the max request number."