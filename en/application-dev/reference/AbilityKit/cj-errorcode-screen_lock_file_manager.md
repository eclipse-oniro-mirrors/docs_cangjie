# Lock Screen Sensitive Data Management Error Codes

## 29300001 Invalid Input Parameter

**Error Message**

Invalid DataType.

**Error Description**

Parameter error occurred when calling the interface for applying or canceling sensitive data access permissions under lock screen.

**Possible Causes**

This error code indicates parameter validation failure, where the input dataType is neither MEDIA_DATA nor ALL_DATA.

**Resolution Steps**

Check input parameters and correct them to valid values.

## 29300002 System Service Abnormal

**Error Message**

The system ability work abnormally.

**Error Description**

This error code indicates abnormal operation of system services.

**Possible Causes**

1. The lock screen sensitive data management service failed to start normally.
2. IPC data read/write operation failed.

**Resolution Steps**

Internal system service exception occurred. Please retry later or restart the device.

## 29300003 Application Has Not Enabled Lock Screen Data Protection

**Error Message**

The application is not enabled the data protection under lock screen.

**Error Description**

The application has not enabled lock screen sensitive data protection functionality.

**Possible Causes**

1. The application did not configure ohos.permission.PROTECT_SCREEN_LOCK_DATA permission in requestpermissions to enable lock screen sensitive data protection.
2. Current hardware does not support lock screen sensitive data protection functionality.

**Resolution Steps**

Configure ohos.permission.PROTECT_SCREEN_LOCK_DATA permission in requestpermissions to enable application lock screen sensitive data protection.

## 29300004 Lock Screen Sensitive Data Access Permission Released

**Error Message**

File access is denied.

**Error Description**

Lock screen sensitive data access permission has been released.

**Possible Causes**

Lock screen sensitive data access permission has been released.

**Resolution Steps**

Sensitive data cannot be accessed under lock screen. If needed, prompt the user to unlock the screen first. Sensitive data will become available after unlocking.

## 29300005 Lock Screen Data Access Permission Not Requested

**Error Message**

File access was not acquired.

**Error Description**

Attempted to call the cancel interface for sensitive data access permissions under lock screen without first requesting the permission.

**Possible Causes**

This error code indicates that lock screen sensitive data access permission was not requested prior to release.

**Resolution Steps**

Check whether the current interface is properly paired. Always request lock screen sensitive data access permission before releasing it.