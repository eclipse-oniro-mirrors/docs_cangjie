# RPC Error Codes

## 1900001 mmap System Call Failed

**Error Message**

Failed to call mmap.

**Error Description**

The mmap system call execution failed.

**Possible Causes**

1. The mapping region is too large.
2. High system memory pressure with insufficient available memory for mapping.

**Resolution Steps**

1. Verify if Ashmem::create() was called with excessively large memory allocation.
2. Check whether sufficient system memory is available during mapping execution.

## 1900002 ioctl System Call Failed

**Error Message**

Failed to call ioctl.

**Error Description**

The ioctl system call execution on shared memory file descriptor failed.

**Possible Causes**

1. Invalid kernel parameters were specified.
2. The set type exceeds the type specified during shared memory mapping.

**Resolution Steps**

1. Verify if the parameters originate from Ashmem class's PROT_EXEC, PROT_READ, and PROT_WRITE.
2. Ensure the specified parameters are subsets of the types designated during shared memory mapping.

## 1900003 Shared Memory Write Failure

**Error Message**

Failed to write data to the shared memory.

**Error Description**

Data writing to shared memory failed.

**Possible Causes**

1. Single or cumulative write operations exceed mapped shared memory size.
2. PROT_WRITE mode was not set for the shared memory.

**Resolution Steps**

1. Verify if current write operations exceed the total mapped size.
2. Check whether PROT_WRITE protection permission is configured.

## 1900004 Shared Memory Read Failure

**Error Message**

Failed to read data from the shared memory.

**Error Description**

Data reading from shared memory failed.

**Possible Causes**

1. Single or cumulative read operations exceed mapped shared memory size.
2. PROT_READ mode was not set for the shared memory.

**Resolution Steps**

1. Verify if current read operations exceed the total mapped size.
2. Check whether PROT_READ protection permission is configured.

## 1900005 IPC Object Permission Error

**Error Message**

Operation allowed only for the proxy object.

**Error Description**

This operation is exclusively permitted for proxy objects.

**Possible Causes**

A method supported only by RemoteProxy was invoked on a RemoteObject.

**Resolution Steps**

Verify if RemoteObject was incorrectly used to call RemoteProxy-exclusive methods.

## 1900006 IPC Object Permission Error

**Error Message**

Operation allowed only for the remote object.

**Error Description**

This operation is exclusively permitted for remote objects.

**Possible Causes**

A method supported only by RemoteObject was invoked on a RemoteProxy.

**Resolution Steps**

Verify if RemoteProxy was incorrectly used to call RemoteObject-exclusive methods.

## 1900007 Remote Object Communication Failure

**Error Message**

Communication failed.

**Error Description**

Inter-process communication with remote object failed.

**Possible Causes**

1. The remote object has been destroyed.
2. The remote object was recreated after destruction, rendering local proxy obsolete.

**Resolution Steps**

1. Check whether the remote object still exists.
2. Verify if death notification was registered and remote object underwent destruction-recreation.

## 1900008 Invalid IPC Object

**Error Message**

The proxy or remote object is invalid.

**Error Description**

Invalid proxy or remote object detected.

**Possible Causes**

1. The proxy object has expired.
2. The remote object has been destroyed.

**Resolution Steps**

1. Investigate potential anomalies during proxy object acquisition.
2. Check whether the remote object has been destructed.

## 1900009 MessageSequence Write Failure

**Error Message**

Failed to write data to the message sequence.

**Error Description**

Data writing to MessageSequence failed.

**Possible Causes**

The sequence's default capacity has been exhausted.

**Resolution Steps**

Use MessageSequence's buffer space query methods to verify remaining capacity.

## 1900010 MessageSequence Read Failure

**Error Message**

Failed to read data from the message sequence.

**Error Description**

Data reading from MessageSequence failed.

**Possible Causes**

Read/write sequence inconsistency.

**Resolution Steps**

Ensure read operations strictly follow the write sequence.

## 1900011 Memory Allocation Failure

**Error Message**

Memory allocation failed.

**Error Description**

Memory allocation failure during serialization.

**Possible Causes**

Excessively large data write operations.

**Resolution Steps**

Verify whether written data or parameters exceed reasonable size limits.

## 1900012 JS Method Failure

**Error Message**

Failed to call the JS callback function.

**Error Description**

JavaScript callback execution failed.

**Possible Causes**

Business logic JS method returned failure.

**Resolution Steps**

Verify successful execution of business JS methods.

## 1900013 dup System Call Failed

**Error Message**

Failed to call dup.

**Error Description**

The dup system call execution failed.

**Possible Causes**

1. Process file descriptor resources exhausted.
2. Input fd parameter has been closed.

**Resolution Steps**

1. Verify validity of input fd parameter.
2. Investigate potential file descriptor resource exhaustion in the process.