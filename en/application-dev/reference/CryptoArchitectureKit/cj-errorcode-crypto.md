# Crypto Framework Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 17620001 Memory Error

**Error Message**

Memory error.

**Possible Causes**

Memory allocation failure in the current system.

**Resolution Steps**

1. Check whether the current system functions normally.
2. Verify if the business data exceeds length limits, causing the system to fail memory allocation.

## 17620002 Runtime Error

**Error Message**

Runtime error.

**Possible Causes**

Unpredictable errors occurred in the system.

**Resolution Steps**

Check whether the current system functions normally.

## 17630001 Algorithm-Related Operation Error, Third-Party Algorithm Library API Call Failed

**Error Message**

Crypto operation error.

**Possible Causes**

An error occurred during the interaction between the cryptographic algorithm framework and the third-party algorithm library.

**Resolution Steps**

1. Verify the correctness of input parameters.
2. Check whether the third-party algorithm library functions normally.