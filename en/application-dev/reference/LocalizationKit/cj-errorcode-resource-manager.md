# Resource Management Error Codes

## 9001001 Invalid Resource ID

**Error Message**

If the resId is invalid.

**Error Description**

This error occurs when the input resource ID passes type validation but corresponds to a non-existent resource.

**Possible Causes**

The input ID value does not exist.

**Resolution Steps**

Verify whether the input resource ID exists.

## 9001002 No Matching Resource Found for Current Resource ID

**Error Message**

If the resource is not found by resId.

**Error Description**

This error occurs when the input resource ID passes type validation but no matching resource can be located.

**Possible Causes**

1. The input resource ID is incorrect.
2. Resource parsing error occurred.

**Resolution Steps**

Verify whether the input resource ID meets expectations.

## 9001003 Invalid Resource Name

**Error Message**

If the resName is invalid.

**Error Description**

This error occurs when the input resource name passes type validation but corresponds to a non-existent resource.

**Possible Causes**

The input resource name does not exist.

**Resolution Steps**

Verify whether the input resource name meets expectations.

## 9001004 No Matching Resource Found for Current Resource Name

**Error Message**

If the resource is not found by resName.

**Error Description**

This error occurs when the input resource name passes type validation but no matching resource can be located.

**Possible Causes**

1. The input resource name is incorrect.
2. Resource parsing error occurred.

**Resolution Steps**

First verify whether the input resource name meets expectations.

## 9001005 Invalid Relative Path

**Error Message**

If the resource is not found by path.

**Error Description**

No corresponding resource can be found based on the input relative path.

**Possible Causes**

The input relative path is incorrect.

**Resolution Steps**

Verify whether the input relative path meets expectations.

## 9001006 Circular Reference

**Error Message**

If the resource is re-referenced too many times.

**Error Description**

Excessive reference parsing count detected.

**Possible Causes**

Circular resource reference occurred.

**Resolution Steps**

Check resource reference locations and eliminate circular references.

## 9001007 Formatting Failure for Resource Obtained by Current ID

**Error Message**

If the resource obtained by resId has formatting errors.

**Error Description**

String resource obtained by resId failed to format.

**Possible Causes**

1. Parameter type is not supported.
2. Parameter count doesn't match placeholder count.
3. Parameter types don't match placeholder types.

**Resolution Steps**

Verify whether the args parameter types match the placeholder count and types.

## 9001008 Formatting Failure for Resource Obtained by Current Name

**Error Message**

If the resource obtained by resName has formatting errors.

**Error Description**

String resource obtained by resName failed to format.

**Possible Causes**

1. Parameter type is not supported.
2. Parameter count doesn't match placeholder count.
3. Parameter types don't match placeholder types.

**Resolution Steps**

Verify whether the args parameter types match the placeholder count and types.

## 9001009 Failed to Obtain System Resource Manager

**Error Message**

If the application cannot access system resources.

**Error Description**

Failed to obtain the system resource manager.

**Possible Causes**

System resources were not loaded into the application process's sandbox path.

**Resolution Steps**

Check whether the application process contains the system resource sandbox path.

## 9001010 Invalid Overlay Path

**Error Message**

If the overlay path is invalid.

**Error Description**

The input overlay path is invalid.

**Possible Causes**

The path doesn't exist or cannot be accessed as it's not located in the corresponding application's installation directory.

**Resolution Steps**

Check the location of the input overlay path.