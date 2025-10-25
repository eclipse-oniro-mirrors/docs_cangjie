# Color Management Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 18600001 Abnormal Parameter Value

**Error Message**

Parameter value is abnormal.

**Error Description**

This error code is reported when the parameter value does not meet the interface invocation requirements.

**Possible Causes**

An error will be reported if the parameter value exceeds the interface invocation range, such as an enumeration value exceeding the defined range.

**Resolution Steps**

Before defining interface parameters, ensure that the parameter values comply with the interface parameter requirements.