# General Error Codes

## 201 Permission Verification Failed

**Error Message**  
Permission verification failed. The application does not have the permission required to call the API.

**Error Description**  
Permission verification failed. The application lacks the necessary permissions to use this API and needs to apply for authorization.

**Possible Causes**  
This error code indicates a permission verification failure, typically occurring when attempting to call an API without the required permissions.

**Resolution Steps**  
Verify whether your application has the necessary permissions to call the API.

## 202 System API Permission Verification Failed

**Error Message**  
Permission verification failed. A non-system application calls a system API.

**Error Description**  
Permission verification failed. A non-system application attempted to use a system API.

**Possible Causes**  
A non-system application invoked a system API. Please verify whether system APIs are being used.

**Resolution Steps**  
Check if system APIs are being called and remove such calls if present.

## 401 Parameter Check Failed

**Error Message**  
Parameter error. Possible causes:  
1. Mandatory parameters are left unspecified;  
2. Incorrect parameter types;  
3. Parameter verification failed.

**Error Description**  
1. Required parameters are missing.  
2. Parameter types are incorrect.  
3. Parameter validation failed.

**Possible Causes**  
1. Mandatory parameters were not provided.  
2. Parameter type error (Type Error).  
3. Incorrect parameter count (Argument Count Error).  
4. Null parameter error (Null Argument Error).  
5. Parameter format error (Format Error).  
6. Parameter value range error (Value Range Error).

**Resolution Steps**  
Verify whether all required parameters are provided and whether the parameter types are correct. For parameter validation failures, review the parameter specifications and troubleshoot based on the possible causes listed.

## 801 API Not Supported by This Device

**Error Message**  
Capability not supported. Failed to call the API due to limited device capabilities.

**Error Description**  
This device does not support the API. Typically used when a device supports the SysCap but has limited support for specific APIs.

**Possible Causes**  
The API is not supported by this device.

**Resolution Steps**  
Check whether the device supports the API being used.