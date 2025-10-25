# SE (SecureElement) Error Codes

> **Note:**
>
> The following only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 3300101 SE Service Status Abnormal

**Error Message**

IllegalStateError, an attempt is made to use an SE session that has been closed.

**Error Description**

The SE service status is abnormal.

**Possible Causes**

The SE service connection has been terminated.

**Resolution Steps**

1. Close the SE service.
2. Re-establish the connection with the SE service.

## 3300102 No Such SE Exception

**Error Message**

NoSuchElementError, the AID on the SE is not available or cannot be selected.

**Error Description**

No such SE exception.

**Possible Causes**

1. Communication exception when establishing connection with the SE service.
2. SE chip communication exception.

**Resolution Steps**

1. Close the SE service and re-establish the connection.
2. Try restarting the device.

## 3300103 Unable to Obtain Access Control Rules Exception

**Error Message**

SecurityError, the calling application cannot be granted access to this AID or the default applet on this session.

**Error Description**

Unable to obtain access control rules exception.

**Possible Causes**

1. The access rules required by the application are not available on the secure element.

**Resolution Steps**

1. Write the correct access rules to the secure element.
2. Close the SE service and re-establish the connection.

## 3300104 SE Chip IO Exception

**Error Message**

IOError, there is a communication problem to the reader or the SE.

**Error Description**

SE chip IO exception.

**Possible Causes**

1. Communication exception with the SE chip.
2. SE chip status is abnormal.

**Resolution Steps**

1. Close the SE service and re-establish the connection.
2. Try restarting the device.