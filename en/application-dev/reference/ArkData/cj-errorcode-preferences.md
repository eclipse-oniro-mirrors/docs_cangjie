# User Preferences Error Codes

> **Note:**
>
> This document only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 15500000 Internal Error

**Error Message**

Inner error.

**Error Description**

An internal error occurred in user preferences.

**Possible Causes**

Failed to read/write persistent files.

**Solution**

Check log information to identify the cause or contact developers for support.

## 15500010 Failed to Delete User Preferences Persistent File

**Error Message**

Failed to delete preferences file.

**Error Description**

Failed to delete the user preferences persistent file.

**Possible Causes**

System error caused file deletion failure. Possible reasons include:

1. Incorrect file name.
2. Incorrect file path.

**Solution**

1. Verify the persistent file name is correct.
2. Verify the persistent file path is correct.

## 15500019 Failed to Obtain Subscription Service

**Error Message**

Failed to obtain subscription service.

**Error Description**

Failed to acquire subscription service during inter-process subscription.

**Possible Causes**

The current platform does not support subscription services.

**Solution**

Deploy subscription services on the current platform.

## 15501002 Invalid dataGroupId Parameter in Options

**Error Message**

The data group id is not valid.

**Error Description**

Using an invalid dataGroupId parameter.

**Possible Causes**

The dataGroupId used was not properly obtained from the application market.

**Solution**

Applications should apply for dataGroupId from the application market and correctly pass this parameter.