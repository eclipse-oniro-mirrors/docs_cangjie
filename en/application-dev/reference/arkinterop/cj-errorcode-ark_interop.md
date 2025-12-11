# Interoperation Error Codes

> **Note:**
>
> The following only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 34300001 Illegal Index

**Error Message**

The index used exceeds the allowed range.

**Error Description**

This error code is reported when the specified index exceeds the permitted range.

**Possible Causes**

The specified index is less than 0 or exceeds the upper limit.

**Resolution Steps**

1. Ensure the specified index is greater than or equal to 0.
2. Ensure the specified index is less than the upper limit.

## 34300002 ArkTS Code Exception

**Error Message**

An exception occurred in the executed ArkTS code.

**Error Description**

ArkTS runtime exception or an exception occurred in the called ArkTS function.

**Possible Causes**

1. ArkTS runtime exceptions such as StackOverflow.
2. Incorrect parameters passed or logical errors in the ArkTS function implementation.

**Resolution Steps**

1. Verify the parameters passed to the ArkTS function are correct.
2. Check the logic of the called function for correctness.

## 34300003 Illegal Object Access

**Error Message**

The accessed object has exceeded its lifecycle.

**Error Description**

The accessed object has been released.

**Possible Causes**

- Accessing JSValue beyond its scope.
- The accessed JSPromiseCapability has already completed.
- Continuing to access JSContext after the ArkTS runtime has been released.

**Resolution Steps**

Use safe references to escape the current scope for access.

## 34300004 Thread Verification Failed

**Error Message**

Interoperation performed on a non-ArkTS runtime thread.

**Error Description**

This error code is reported when creating or accessing ArkTS objects on a non-ArkTS runtime thread.

**Possible Causes**

Creating or accessing ArkTS objects on a non-ArkTS runtime thread.

**Resolution Steps**

Before performing interoperation, use the interface `JSContext.isBindThread()` to verify if the current thread is an ArkTS runtime thread.

## 34300005 Type Verification Failed

**Error Message**

ArkTS data type mismatch.

**Error Description**

This error code is reported when incorrect type operations are performed on ArkTS data.

**Possible Causes**

Incorrect type conversion, such as converting a number to JSString.

**Resolution Steps**

Verify the data type before performing operations.

## 34300006 Fail To Load Module.

**Error Message**

Fail to load module which doesn't exist.

**Error Description**

Require ArkTS module from cangjie, Fail to load the module which doesn't exist.

**Possible Causes**

* The module path is incorrect.
* The device's ApiLevel does not meet the minimum requirements.

**Resolution Steps**

Check if the module path is correct, If the target is a system module, check whether the ApiLevel of the running device meets the requirements.

## 34300007 Cannot Import During Cangjie Exports

**Error Message**

Cannot requireArkModule during initializing cangjie module.

**Error Description**

Calling requireArkModule in the callback for exporting ArkTS interfaces in Cangjie will throw this exception.

**Possible Causes**

Calling requireArkModule in the callback for exporting ArkTS interfaces in Cangjie.

**Resolution Steps**

Troubleshoot whether requireArkModule is called in the exported function of the registered module, and remove the call or delay the invocation.

## 34300008 Application Does Not Support The Module

**Error Message**

The current application does not support importing the specified ArkTS module.

**Error Description**

Importing ArkTS source code modules in Cangjie applications is not yet supported, and this exception will be thrown if it occurs.

**Possible Causes**

Not support yet.

**Resolution Steps**

Switch to an ArkTS application or wait for subsequent support.
