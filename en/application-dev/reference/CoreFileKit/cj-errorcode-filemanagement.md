# File Management Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

The file management subsystem error codes consist of five parts: [Basic File IO Error Codes](#basic-file-io-error-codes), [User Data Management Error Codes](#user-data-management-error-codes), [Public File Access Error Codes](#public-file-access-error-codes), [Space Statistics Error Codes](#space-statistics-error-codes), and [Device-Cloud Sync Error Codes](#device-cloud-sync-error-codes).

## Basic File IO Error Codes

### 13900001 Operation Not Permitted

**Error Message**

Operation not permitted

**Possible Causes**

The current user's file operation is not allowed.

**Resolution Steps**

Verify file permissions.

### 13900002 No Such File or Directory

**Error Message**

No such file or directory

**Possible Causes**

The file or directory does not exist.

**Resolution Steps**

Verify the file path exists.

### 13900003 No Such Process

**Error Message**

No such process

**Possible Causes**

The process does not exist.

**Resolution Steps**

1. Check if the process was unexpectedly terminated.
2. Verify if the related service is running.

### 13900004 Interrupted System Call

**Error Message**

Interrupted system call

**Possible Causes**

The system call was interrupted by another thread.

**Resolution Steps**

1. Check the multi-threading code logic.
2. Retry the system call.

### 13900005 I/O Error

**Error Message**

I/O error

**Possible Causes**

The I/O request is invalid.

**Resolution Steps**

Retry the I/O request.

### 13900006 No Such Device or Address

**Error Message**

No such device or address

**Possible Causes**

Incorrect device or address information.

**Resolution Steps**

Verify the device or address information.

### 13900007 Argument List Too Long

**Error Message**

Arg list too long

**Possible Causes**

The argument list is too long.

**Resolution Steps**

Reduce the number of arguments.

### 13900008 Bad File Descriptor

**Error Message**

Bad file descriptor

**Possible Causes**

1. The file descriptor is already closed.
2. Read/write permissions do not match.

**Resolution Steps**

1. Verify if the file descriptor is closed.
2. Verify if the file read/write permissions match.

### 13900009 No Child Processes

**Error Message**

No child processes

**Possible Causes**

Unable to create a child process.

**Resolution Steps**

Check the system's maximum process limit.

### 13900010 Resource Temporarily Unavailable

**Error Message**

Try again

**Possible Causes**

The resource is blocked.

**Resolution Steps**

Retry the resource request.

### 13900011 Out of Memory

**Error Message**

Out of memory

**Possible Causes**

Memory overflow.

**Resolution Steps**

1. Check memory usage.
2. Manage system memory usage.

### 13900012 Permission Denied

**Error Message**

Permission denied

**Possible Causes**

1. No permission for the file operation.
2. Incorrect file sandbox path address.

**Resolution Steps**

1. Verify permissions.
2. Verify the file sandbox path address.

### 13900013 Bad Address

**Error Message**

Bad address

**Possible Causes**

Incorrect address.

**Resolution Steps**

Verify the address is correct.

### 13900014 Device or Resource Busy

**Error Message**

Device or resource busy

**Possible Causes**

The requested resource is unavailable.

**Resolution Steps**

Retry the resource request.

### 13900015 File Exists

**Error Message**

File exists

**Possible Causes**

The file to be created already exists.

**Resolution Steps**

Verify the file path is correct.

### 13900016 Invalid Cross-Device Link

**Error Message**

Cross-device link

**Possible Causes**

Cross-device linking failed.

**Resolution Steps**

Verify cross-device connectivity.

### 13900017 No Such Device

**Error Message**

No such device

**Possible Causes**

The device is not recognized.

**Resolution Steps**

Verify the device connection is normal.

### 13900018 Not a Directory

**Error Message**

Not a directory

**Possible Causes**

The path is not a directory.

**Resolution Steps**

Verify the path is correct.

### 13900019 Is a Directory

**Error Message**

Is a directory

**Possible Causes**

The path is a directory.

**Resolution Steps**

Verify the path is correct.

### 13900020 Invalid Argument

**Error Message**

Invalid argument

**Possible Causes**

Invalid input parameter.

**Resolution Steps**

Verify the parameter validity.

### 13900021 Too Many Open File Descriptors

**Error Message**

File table overflow

**Possible Causes**

The process has opened too many file descriptors.

**Resolution Steps**

Close unnecessary file descriptors.

### 13900022 Too Many Open Files

**Error Message**

Too many open files

**Possible Causes**

The system has opened too many files.

**Resolution Steps**

Close unnecessary files.

### 13900023 Text File Busy

**Error Message**

Text file busy

**Possible Causes**

The program's executable file is in use.

**Resolution Steps**

Close the program being debugged.

### 13900024 File Too Large

**Error Message**

File too large

**Possible Causes**

The file size exceeds the maximum file size limit.

**Resolution Steps**

Verify the file size meets the maximum file size limit.

### 13900025 No Space Left on Device

**Error Message**

No space left on device

**Possible Causes**

Insufficient device storage space.

**Resolution Steps**

Free up device storage space.

### 13900026 Illegal Seek

**Error Message**

Illegal seek

**Possible Causes**

Using seek on a pipe or FIFO.

**Resolution Steps**

Verify seek usage.

### 13900027 Read-Only File System

**Error Message**

Read-only file system

**Possible Causes**

The file system is read-only.

**Resolution Steps**

Verify the file is read-only.

### 13900028 Too Many Links

**Error Message**

Too many links

**Possible Causes**

The file has reached the maximum number of links.

**Resolution Steps**

Clean up unused links.

### 13900029 Resource Deadlock Would Occur

**Error Message**

Resource deadlock would occur

**Possible Causes**

Resource deadlock.

**Resolution Steps**

Terminate the deadlocked process.

### 13900030 Filename Too Long

**Error Message**

Filename too Long

**Possible Causes**

The path or filename exceeds the maximum length.

**Resolution Steps**

Verify the path or filename length.

### 13900031 Function Not Implemented

**Error Message**

Function not implemented

**Possible Causes**

The system does not support this function.

**Resolution Steps**

Verify the system version.

### 13900032 Directory Not Empty

**Error Message**

Directory not empty

**Possible Causes**

The specified directory is not empty.

**Resolution Steps**

1. Verify the directory path.
2. Ensure the path is empty.

### 13900033 Too Many Symbolic Links Encountered

**Error Message**

Too many symbolic links encountered

**Possible Causes**

Too many levels of symbolic links.

**Resolution Steps**

Clean up unnecessary symbolic links.

### 13900034 Operation Would Block

**Error Message**

Operation would block

**Possible Causes**

The operation is blocked.

**Resolution Steps**

Retry the operation.

### 13900035 Invalid Request Descriptor

**Error Message**

Invalid request descriptor

**Possible Causes**

Invalid file descriptor.

**Resolution Steps**

Verify the file descriptor is valid.

### 13900036 Device Not a Stream

**Error Message**

Device not a stream

**Possible Causes**

The file descriptor does not point to a stream device.

**Resolution Steps**

Verify the file descriptor points to a stream device.

### 13900037 No Data Available

**Error Message**

No data available

**Possible Causes**

Data is unavailable.

**Resolution Steps**

Retry the data request.

### 13900038 Value Too Large for Defined Data Type

**Error Message**

Value too large for defined data type

**Possible Causes**

The value exceeds the defined data type range.

**Resolution Steps**

Modify the data type.

### 13900039 File Descriptor in Bad State

**Error Message**

File descriptor in bad state

**Possible Causes**

The file descriptor is corrupted.

**Resolution Steps**

Verify the file descriptor validity.

### 13900040 Interrupted System Call Should Be Restarted

**Error Message**

Interrupted system call should be restarted

**Possible Causes**

The system call was interrupted.

**Resolution Steps**

Retry the system call.

### 13900041 Quota Exceeded

**Error Message**

Quota exceeded

**Possible Causes**

Insufficient disk space.

**Resolution Steps**

Free up disk storage space.

### 13900042 Unknown Error

**Error Message**

Unknown error

**Possible Causes**

Internal error.

**Resolution Steps**

1. Retry the interface.
2. Restart the service.

### 13900043 No Record Locks Available

**Error Message**

No record is locks available

**Possible Causes**

Insufficient system resources.

**Resolution Steps**

Release lock resources and retry.

### 13900044 Network Is Unreachable

**Error Message**

Network is unreachable

**Possible Causes**

Network anomaly.

**Resolution Steps**

Check the network status and ensure it is normal.

### 13900045 Connection Failed

**Error Message**

Connection failed

**Possible Causes**

Device, WiFi, or Bluetooth status anomaly, causing connection failure.

**Resolution Steps**

1. Check the device and ensure its status is normal.
2. Check WiFi and Bluetooth and ensure their status is normal.

### 13900046 Connection Failed

**Error Message**

Software caused connection abort

**Possible Causes**

Device offline or WiFi/Bluetooth disconnected.

**Resolution Steps**

1. Check the device and ensure its status is normal.
2. Check WiFi and Bluetooth and ensure their status is normal.## User Data Management Error Codes

### 14000001 Invalid File Name

**Error Message**

Invalid display name

**Possible Causes**

The file name contains invalid characters.

**Resolution Steps**

Remove invalid characters.

### 14000002 Invalid URI

**Error Message**

Invalid uri

**Possible Causes**

The URI is invalid.

**Resolution Steps**

Use the URI obtained directly from the query.

### 14000003 Invalid File Extension

**Error Message**

Invalid file name extension

**Possible Causes**

Named according to file type.

**Resolution Steps**

Check the file name extension.

### 14000004 File Moved to Recycle Bin

**Error Message**

File has been put into trash bin

**Possible Causes**

The file has been deleted and moved to the recycle bin.

**Resolution Steps**

Check if the file has been moved to the recycle bin.

### 14000011 System Internal Error

**Error Message**

System inner fail

**Possible Causes**

System exception, unknown error occurred.

**Resolution Steps**

Clear background processes or restart the device.

### 14000014 Invalid Member Name

**Error Message**

Member is not a valid PhotoKey

**Possible Causes**

The input string is not a member name of the class or interface.

**Resolution Steps**

Ensure the input string is a member name of the class or interface.

## Storage Statistics Error Codes

### 13600001 IPC Communication Failure

**Error Message**

IPC error

**Possible Causes**

The called service does not exist.

**Resolution Steps**

Check if the service is running.

### 13600002 Unsupported File System Type

**Error Message**

Not supported filesystem

**Possible Causes**

The file system type being operated is not supported.

**Resolution Steps**

Modify to the correct file system type.

### 13600003 Mount Failure

**Error Message**

Failed to mount

**Possible Causes**

Failed to execute the mount command.

**Resolution Steps**

Remove the card and attempt to remount.

### 13600004 Unmount Failure

**Error Message**

Failed to unmount

**Possible Causes**

The device is busy.

**Resolution Steps**

Check if external card files are occupied by threads, and terminate the occupying threads.

### 13600005 Incorrect Volume State

**Error Message**

Incorrect volume state

**Possible Causes**

The volume state being operated is incorrect.

**Resolution Steps**

Check if the current volume state is correct.

### 13600006 Directory or Node Creation Failure

**Error Message**

Prepare directory or node error

**Possible Causes**

The directory or node already exists.

**Resolution Steps**

Check if the target directory or node exists.

### 13600007 Directory or Node Deletion Failure

**Error Message**

Delete directory or node error

**Possible Causes**

The directory or node has already been deleted.

**Resolution Steps**

Check if the target directory or node exists.

### 13600008 Object Not Found

**Error Message**

No such object

**Possible Causes**

1. Incorrect volume ID entered.  
2. Incorrect package name entered.

**Resolution Steps**

1. Check if the entered volume exists.  
2. Check if the entered application package name exists.

### 13600009 User ID Out of Range

**Error Message**

User id out of range

**Possible Causes**

Incorrect user ID entered.

**Resolution Steps**

Check if the entered user ID is within the normal range.

## Public File Access Error Codes

### 14300001 IPC Communication Failure

**Error Message**

IPC error

**Possible Causes**

1. Server-side service is unavailable.  
2. Extension mechanism exception.

**Resolution Steps**

Check if the server-side service exists.

### 14300002 Invalid URI Format

**Error Message**

Invalid uri

**Possible Causes**

Illegal URI used.

**Resolution Steps**

Check the URI format.

### 14300003 Failed to Query Server-Side Ability Information

**Error Message**

Fail to get fileextension info

**Possible Causes**

BMS interface exception.

**Resolution Steps**

System capability issue.

### 14300004 Abnormal Result Returned by js-server

**Error Message**

Get wrong result

**Possible Causes**

Server-side returned inappropriate data.

**Resolution Steps**

Check the server-side return value.

### 14300005 Notification Registration Failure

**Error Message**

Fail to register notification

**Possible Causes**

1. Server-side service is unavailable.  
2. Extension mechanism exception.

**Resolution Steps**

Check if the server-side service exists.

### 14300006 Notification Removal Failure

**Error Message**

Fail to remove notification

**Possible Causes**

1. Server-side service is unavailable.  
2. Extension mechanism exception.

**Resolution Steps**

Check if the server-side service exists.

### 14300007 Notification Agent Initialization Failure

**Error Message**

Fail to init notification agent

**Possible Causes**

Attempted to cancel notification without prior registration.

**Resolution Steps**

Check if registration was completed.

### 14300008 js-server Notification Agent Failure

**Error Message**

Fail to notify agent

**Possible Causes**

1. Service unavailable.  
2. Extension mechanism exception.

**Resolution Steps**

Check if the client is abnormal.

## Cloud Sync Error Codes

### 22400001 Cloud Status Not Ready

**Error Message**

Cloud status not ready

**Possible Causes**

1. Cloud service is not enabled.  
2. Application cloud sync switch is turned off.

**Resolution Steps**

1. Check if the account is logged in.  
2. Check if the cloud sync switch is turned on.

### 22400002 Network Unavailable

**Error Message**

Network unavailable

**Possible Causes**

Device is offline or network is unavailable.

**Resolution Steps**

Check network status.

### 22400003 Low Battery Warning

**Error Message**

Battery level warning

**Possible Causes**

Battery level is too low.

**Resolution Steps**

Enable charging mode or retry after battery level recovers.