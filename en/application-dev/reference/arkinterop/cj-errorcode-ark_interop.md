# Interoperation Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

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

The called ArkTS function encountered an exception.

**Possible Causes**

Incorrect parameter passing or logical errors in the ArkTS function implementation.

**Resolution Steps**

1. Check whether the parameters passed to the ArkTS function are correct.
2. Verify the logic of the called function.

## 34300003 Illegal Object Access

**Error Message**

The accessed object has exceeded its lifecycle.

**Error Description**

The accessed object has been released.

**Possible Causes**

- Accessing a JSValue outside its scope.
- Accessing a JSPromiseCapability that has already completed.
- Continuing to access a JSContext after the ArkTS runtime has released it.

**Resolution Steps**

Use safe references to escape the current scope for access.

## 34300004 Thread Verification Failed

**Error Message**

Interoperation attempted on a non-ArkTS runtime thread.

**Error Description**

This error code is reported when creating or accessing ArkTS objects on a non-ArkTS runtime thread.

**Possible Causes**

Creating or accessing ArkTS objects on a non-ArkTS runtime thread.

**Resolution Steps**

Before performing interoperation, use the interface `JSContext.isBindThread()` to determine whether the current thread is an ArkTS runtime thread.

## 34300005 Type Verification Failed

**Error Message**

ArkTS data type mismatch.

**Error Description**

This error code is reported when incorrect type operations are performed on ArkTS data.

**Possible Causes**

Incorrect type conversion, such as converting a number to a JSString.

**Resolution Steps**

Verify the data type before performing operations.