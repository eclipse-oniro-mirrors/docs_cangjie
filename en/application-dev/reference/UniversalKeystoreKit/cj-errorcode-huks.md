# HUKS Error Codes

> **Note:**
>
> The following only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 12000001 Feature Not Supported

**Error Message**

The ``${messageInfo}`` is not supported.

**Possible Causes**

The API is supported, but certain sub-features (functionalities) within the API are not supported, such as algorithm parameters.

**Resolution Steps**

Adjust the API parameters and use alternative supported parameters.

## 12000002 Missing Key Algorithm Parameter

**Error Message**

Failed to obtain the ``${messageInfo}``. It is not set in ParamSet.

**Possible Causes**

Missing relevant parameters when using the key.

**Resolution Steps**

1. Check the `errorMessage` to identify the missing key parameter.
2. Add the corresponding correct key parameter.

## 12000003 Invalid Key Algorithm Parameter

**Error Message**

Invalid ``${messageInfo}``.

**Possible Causes**

Invalid relevant parameters when using the key.

**Resolution Steps**

1. Check the `errorMessage` to identify the invalid key parameter name.
2. Modify the corresponding key parameter.

## 12000004 File Error

**Error Message**

May be one of the following:

- Insufficient storage space.
- Invalid file size.
- Failed to ``${messageInfo}``.

**Possible Causes**

File operation error.

**Resolution Steps**

1. Check if the disk space is full or if there are other file system anomalies.
2. Clean up disk space.

## 12000005 IPC Communication Error

**Error Message**

May be one of the following:

- Failed to get messages from IPC.
- IPC ``${messageInfo}``.

**Possible Causes**

Inter-process communication (IPC) error.

**Resolution Steps**

Check the error message to troubleshoot potential IPC communication issues.

## 12000006 Cryptographic Engine Operation Failed

**Error Message**

Crypto engine error.

**Possible Causes**

This error code indicates a failure in cryptographic engine operations. Possible causes include:

1. Encryption/decryption error in the cryptographic engine, possibly due to incorrect ciphertext data.
2. Incorrect key parameters.

**Resolution Steps**

1. Verify the correctness of the ciphertext data.
2. Check the encryption/decryption parameters for accuracy.

## 12000007 Key Access Failed - Key Permanently Invalidated

**Error Message**

This credential is invalidated permanently.

**Possible Causes**

This error code indicates key access failure due to permanent invalidation. Possible causes include:

1. The key has a user authentication access control attribute set to invalidate upon password reset, and device keys were cleared, causing key invalidation.
2. The key has a user authentication access control attribute set to invalidate upon new biometric enrollment, and new fingerprints or facial data were added, causing key invalidation.

**Resolution Steps**

1. Confirm the cause of authentication failure through logs.
2. If correct parameters were used but invalidation control caused authentication failure, the key can no longer be used.

## 12000008 Key Access Failed - Key Authentication Failed

**Error Message**

The authentication token verification failed.

**Possible Causes**

The key has a user authentication access control attribute set, and authentication failed due to incorrect `challenge` parameters.

**Resolution Steps**

1. Check if the `challenge` parameter for userIAM authentication is correctly assembled.
2. If the `challenge` parameter is incorrect, modify the assembly method by generating the `challenge` via HUKS and passing it to userIAM for re-authentication.

## 12000009 Key Access Failed - Key Access Timeout

**Error Message**

This authentication token timed out.

**Possible Causes**

The key has a user authentication access control attribute set, and authentication failed due to exceeding the `timeout` window.

**Resolution Steps**

If the failure is due to `timeout`, re-trigger key initialization (`init`) and re-authenticate to ensure the authentication time and key initialization time are within the configured `timeout` window.

## 12000010 Maximum Key Operation Sessions Reached

**Error Message**

The number of key operation sessions has reached the limit.

**Possible Causes**

Too many callers (within the same application or across applications) are simultaneously using HUKS for key session operations, reaching the limit (15 sessions).

**Resolution Steps**

1. Check if the same application has multiple concurrent key session operations (`init`). If so, modify the code to avoid simultaneous calls.
2. If not, other applications may be occupying sessions. Wait for them to release sessions before retrying.

## 12000011 Target Object Does Not Exist

**Error Message**

The entity does not exist.

**Possible Causes**

The key corresponding to the alias does not exist.

**Resolution Steps**

1. Check if the key alias is misspelled.
2. Verify if the key corresponding to the alias was successfully generated.

## 12000012 External Error

**Error Message**

System external error.

**Possible Causes**

External hardware errors, file errors, etc.

**Resolution Steps**

Report the error code and logs to the community for feedback.

## 12000013 Credential Not Found When Binding Biometric Access Control to Key

**Error Message**

The credential does not exist.

**Possible Causes**

When binding PIN, fingerprint, or facial recognition to a key, the relevant credential was not enrolled.

**Resolution Steps**

Enroll the relevant credential or change the binding credential type.

## 12000014 Insufficient Memory

**Error Message**

May be one of the following:

- Insufficient memory.
- Malloc failed.

**Possible Causes**

System memory is insufficient.

**Resolution Steps**

Developers should free up memory or restart the system.

## 12000015 Failed to Call Other System Services

**Error Message**

Failed to obtain the ``${messageInfo}`` information via UserIAM.

**Possible Causes**

Other system services are not running.

**Resolution Steps**

Developers should wait and retry the operation after some time.

## 12000016 Device Password Required but Not Set

**Error Message**

Device password is required but not set.

**Possible Causes**

The service restricts key usage to devices with a lock screen password set, but no lock screen password is configured.

**Resolution Steps**

Set a lock screen password or modify the key usage restrictions.