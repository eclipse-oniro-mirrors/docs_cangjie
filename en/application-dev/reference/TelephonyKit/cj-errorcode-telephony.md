# Telephony Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 3120001 Service Connection Error

**Error Message**

Service connection failed.

**Error Description**

The operation failed. The service cannot be connected.

**Possible Causes**

The service fails to start, or the IPC connection fails.

**Resolution Steps**

The operation is abnormal. Try again later.

## 3120002 System Internal Error

**Error Message**

System internal error.

**Error Description**

An internal system error occurs.

**Possible Causes**

The network is abnormal, or data fails to be read or written.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8300001 Input Parameter Value Out of Range

**Error Message**

The input parameter value is out of range.

**Error Description**

The value of the input parameter (for example, **slotId**) is not within the valid range. In this case, the API call will fail and the corresponding operation cannot be performed.

**Possible Causes**

The input parameter value is invalid.

**Resolution Steps**

Enter a valid parameter value.

## 8300002 Service Connection Error

**Error Message**

Service connection failed.

**Error Description**

The operation failed. The service cannot be connected.

**Possible Causes**

The service fails to start, or the IPC connection fails.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8300003 System Internal Error

**Error Message**

System internal error.

**Error Description**

An internal system error occurs.

**Possible Causes**

The network is abnormal, or data fails to be read or written.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8300004 SIM Card Not Detected

**Error Message**

No SIM card found.

**Error Description**

No SIM card is detected.

**Possible Causes**

No SIM card is inserted or the SIM card is not properly inserted.

**Resolution Steps**

Insert the SIM card or remove and insert the SIM card again.

## 8300005 Airplane Mode Is On

**Error Message**

Airplane mode is on.

**Error Description**

The requested cellular network operation cannot be performed while airplane mode is on.

**Possible Causes**

The device is in airplane mode.

**Resolution Steps**

Turn off airplane mode and retry after the network becomes available.

## 8300006 Network Not in Service

**Error Message**

Network not in service.

**Error Description**

The network is not in service, so the requested operation cannot be performed.

**Possible Causes**

The device is not registered with a network or has no available network coverage.

**Resolution Steps**

Check the SIM card and network coverage, and retry after service is restored.

## 8300011 Operation Restricted by Policy

**Error Message**

Policy is disabled.

**Error Description**

The operation is restricted by a device policy.

**Possible Causes**

A device policy prohibits the requested cellular network operation.

**Resolution Steps**

Check whether the device policy permits the operation. Contact the device administrator if necessary.

## 8300999 Internal Error

**Error Message**

Internal error.

**Error Description**

An internal error occurs.

**Possible Causes**

The problem may arise due to insufficient memory, memory operation errors, or null pointers.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8301001 SIM Card Not Activated

**Error Message**

SIM card is not activated.

**Error Description**

The SIM card is not activated.

**Possible Causes**

The SIM card is not activated.

**Resolution Steps**

Activate the SIM card.

## 8301002 Failed to Read or Update SIM Card Data

**Error Message**

The SIM card failed to read or update data.

**Error Description**

The attempt to read or update SIM card data has failed.

**Possible Causes**

The SIM card does not support the operation, or the SIM card is damaged.

**Resolution Steps**

Contact the SIM card supplier, or replace the SIM card.

## 8301003 Incorrect SIM Card Configuration

**Error Message**

Operator config error.

**Error Description**

The SIM card configuration is incorrect.

**Possible Causes**

The configuration file delivered with the SIM card is not properly preconfigured.

**Resolution Steps**

Check whether the correct SIM card is inserted.

## 8401001 Failed to Connect to the UT

**Error Message**

UT is not connected.

**Error Description**

The UT is not connected.

**Possible Causes**

The current carrier does not support sending of UT requests over a Wi-Fi network, but the device is connected to the Wi-Fi network.

**Resolution Steps**

Disconnect the Wi-Fi network and resend the UT request.

## 8800001 Input Parameter Value Out of Range

**Error Message**

The input parameter value is out of range.

**Error Description**

The value of the input parameter (for example, **slotId**) is not within the valid range. In this case, the API call will fail and the corresponding operation cannot be performed.

**Possible Causes**

The input parameter value is invalid.

**Resolution Steps**

Enter a valid parameter value.

## 8800002 Service Connection Error

**Error Message**

Service connection failed.

**Error Description**

The operation failed. The service cannot be connected.

**Possible Causes**

The service fails to start, or the IPC connection fails.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8800003 System Internal Error

**Error Message**

System internal error.

**Error Description**

An internal system error occurs.

**Possible Causes**

The network is abnormal, or data fails to be read or written.

**Resolution Steps**

The operation is abnormal. Try again later.

## 8800999 Internal Error

**Error Message**

Internal error.

**Error Description**

An internal error occurs.

**Possible Causes**

The problem may arise due to insufficient memory, memory operation errors, or null pointers.

**Resolution Steps**

The operation is abnormal. Try again later.
