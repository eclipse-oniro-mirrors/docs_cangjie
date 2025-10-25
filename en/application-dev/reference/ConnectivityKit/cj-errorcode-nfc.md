# NFC Error Codes

> **Note:**
>
> The following only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 3100101

**Error Message**

NFC state is abnormal in service.

**Error Description**

The NFC service encountered an exception while executing NFC activation or deactivation internally.

**Possible Causes**

1. Communication exception when establishing connection with the NFC service.
2. Communication exception with the NFC chip.

**Handling Steps**

1. Retry activating or deactivating NFC.
2. Retry activating or deactivating NFC, or restart the device.

## 3100201

**Error Message**

Tag running state is abnormal in service.

**Error Description**

The NFC service encountered an error while executing Tag business logic.

**Possible Causes**

1. Tag parameter values do not match the requirements of the called function.
2. NFC was deactivated during Tag operation.
3. The connection was already disconnected before Tag operation.
4. The Tag chip returned an error status or response timeout.
5. No binding relationship was established with the NFC service, making interface calls impossible.

**Handling Steps**

1. Verify NFC parameters match the called interface requirements.
2. Activate device NFC.
3. Establish connection first before performing read/write operations.
4. Retry tapping to read the card.
5. Exit the application and retry reading the card.

## 3100202

**Error Message**

The element state is invalid.

**Error Description**

When calling the interface, the page state of the application reading the card was incorrect (page not in foreground).

**Possible Causes**

The page state of the application reading the card was incorrect (page not in foreground).

**Handling Steps**

1. Only allow calling this interface from application pages in the foreground.

## 3100203

**Error Message**

The off() can be called only when the on() has been called.

**Error Description**

The off() interface can only be called after the on() interface has been invoked.

**Possible Causes**

1. The application's foreground page directly called the off() interface without first calling on().

**Handling Steps**

1. The application's foreground page should first execute the on() interface, then call off() when exiting the page.

## 3100204

**Error Message**

Tag I/O operation failed.

**Error Description**

NFC Tag I/O operation failure.

**Possible Causes**

1. The NFC Tag does not support the executed read/write operation.

**Handling Steps**

1. The application should handle the exception or provide prompts according to business scenarios.

## 3100301

**Error Message**

Card emulation running state is abnormal in service.

**Error Description**

The NFC service encountered an error while executing card emulation business logic.

**Possible Causes**

1. NFC was deactivated during card emulation.
2. The NFC chip returned an error status or response timeout.

**Handling Steps**

1. When detecting NFC is deactivated, prompt to activate NFC.
2. Prompt to toggle NFC and reinitialize hardware.

## 3200101

**Error Message**

Connected NFC tag running state is abnormal in service.

**Error Description**

Error encountered while executing active NFC Tag business logic.

**Possible Causes**

1. Active NFC Tag parameter values do not match the requirements of the called function.
2. The active NFC Tag chip returned an error status or response timeout.

**Handling Steps**

1. Verify active NFC Tag parameters match the called interface requirements.
2. Retry tapping to read the card.