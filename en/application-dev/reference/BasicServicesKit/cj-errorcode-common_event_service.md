# Event Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 1500001 Empty Action in Want

**Error Message**  
The action field in the want parameter is null.

**Error Description**  
This error code is generated when the `Action` property in the `want` parameter for sending an event is empty.

**Possible Causes**  
The `Action` property in the `want` parameter for sending an event is empty.

**Resolution Steps**  
Check whether the `Action` property in the passed `want` parameter is empty.

## 1500002 Sandbox Application Cannot Send Common Events

**Error Message**  
A sandbox application cannot send common events.

**Error Description**  
Sandbox applications cannot send common events.

**Possible Causes**  
The sender application is a sandbox application, and the event sending is intercepted.

**Resolution Steps**  
Sandbox applications cannot send common events. Verify whether the application is a sandbox application before sending common events.

## 1500003 Excessive Event Sending Frequency

**Error Message**  
Too many common events are sent in a short period of time.

**Error Description**  
The application is sending events too frequently.

**Possible Causes**  
The application has sent too many events within a short time.

**Resolution Steps**  
Check whether the application is sending events too frequently.

## 1500004 Unable to Send System Common Events

**Error Message**  
A third-party application cannot send system common events.

**Error Description**  
The current application cannot send system common events.

**Possible Causes**  
A non-system application or non-system service is attempting to send system common events.

**Resolution Steps**  
Verify whether the current application is a system application or whether the current service is a system service.

## 1500005 Subscriber Not Found

**Error Message**  
The subscriber is not found.

**Error Description**  
The subscriber cannot be found.

**Possible Causes**  
The subscriber has been deleted.

**Resolution Steps**  
Check whether there are duplicate unsubscribe operations.

## 1500006 Invalid UserId

**Error Message**  
Invalid userId.

**Error Description**  
The userId is invalid.

**Possible Causes**  
The userId does not match the system `userId`, or the process is not a system application or system service.

**Resolution Steps**  

1. Check whether the current `userId` matches the system `userId`.
2. Verify whether the current application is a system application or system service.

## 1500007 IPC Request Sending Failed

**Error Message**  
Failed to send the message.

**Error Description**  
The `IPC` request failed to send.

**Possible Causes**  
The connection object was not successfully created.

**Resolution Steps**  
Avoid frequently establishing connections. Retry later.

## 1500008 Failed to Read Data

**Error Message**  
Failed to read the data.

**Error Description**  
An error occurred on the server side.

**Possible Causes**  
A business exception occurred while the server was processing the data.

**Resolution Steps**  
Retry later.

## 1500009 System Error

**Error Message**  
System error.

**Error Description**  
A system exception occurred while processing the business, such as failing to obtain the current system time.

**Possible Causes**  
System malfunction; an exception occurred while obtaining the current system time.

**Resolution Steps**  
Retry later.