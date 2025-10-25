# ohos.rpc

This module provides inter-process communication capabilities, including intra-device inter-process communication (IPC) and inter-device inter-process communication (RPC). The former is based on the Binder driver, while the latter is based on the soft bus driver.

## Importing the Module

```cangjie
import kit.IPCKit.*
```

## Usage Instructions

API example code usage instructions:

- If the first line of example code contains a "// index.cj" comment, it indicates that the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the example requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the example project and configuration template mentioned above, refer to [Cangjie Example Code Description](../cj-development-intro.md#Cangjie-Example-Code-Description).

## interface Parcelable

```cangjie
public interface Parcelable {

    func marshalling(dataOut: MessageSequence): Bool

    func unmarshalling(dataIn: MessageSequence): Bool
}
```

**Description:** During inter-process communication (IPC), writes class objects to MessageSequence and restores them from MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### func marshalling(MessageSequence)

```cangjie

func marshalling(dataOut: MessageSequence): Bool
```

**Description:** Marshals this serializable object into a MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| dataOut | [MessageSequence](#class-messagesequence) | Yes | - | The MessageSequence object to which the serializable object will be marshaled. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Marshaling succeeded; false: Marshaling failed. |

### func unmarshalling(MessageSequence)

```cangjie

func unmarshalling(dataIn: MessageSequence): Bool
```

**Description:** Unmarshals this serializable object from a MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| dataIn | [MessageSequence](#class-messagesequence) | Yes | - | The MessageSequence object containing the marshaled serializable object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Unmarshaling succeeded; false: Unmarshaling failed. |

## class Ashmem

```cangjie
public class Ashmem {
    public static const PROT_EXEC: UInt32 = 4
    public static const PROT_NONE: UInt32 = 0
    public static const PROT_READ: UInt32 = 1
    public static const PROT_WRITE: UInt32 = 2
}
```

**Description:** Provides methods related to anonymous shared memory objects, including creating, closing, mapping, and unmapping Ashmem; reading from and writing to Ashmem; obtaining Ashmem size; and setting Ashmem protection.

Shared memory is only applicable for cross-process communication within the same device.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static const PROT_EXEC

```cangjie
public static const PROT_EXEC: UInt32 = 4
```

**Description:** The mapped memory is executable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static const PROT_NONE

```cangjie
public static const PROT_NONE: UInt32 = 0
```

**Description:** The mapped memory is inaccessible.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static const PROT_READ

```cangjie
public static const PROT_READ: UInt32 = 1
```

**Description:** The mapped memory is readable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static const PROT_WRITE

```cangjie
public static const PROT_WRITE: UInt32 = 2
```

**Description:** The mapped memory is writable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static func create(String, Int32)

```cangjie

public static func create(name: String, size: Int32): Ashmem
```

**Description:** A static method that creates an Ashmem object by copying the file descriptor (fd) of an existing Ashmem object. Both Ashmem objects point to the same shared memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | The name used to query Ashmem information. |
| size | Int32 | Yes | - | The size of the Ashmem in bytes. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the created Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ashmem object;<br>3. The Ashmem instance for obtaining packaging is empty. |

### static func create(Ashmem)

```cangjie

public static func create(ashmem: Ashmem): Ashmem
```

**Description:** A static method that creates an Ashmem object by copying the file descriptor (fd) of an existing Ashmem object. Both Ashmem objects point to the same shared memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| ashmem | [Ashmem](#class-ashmem) | Yes | - | The existing Ashmem object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the created Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ashmem object;<br>3. The Ashmem instance for obtaining packaging is empty. |

### func closeAshmem()

```cangjie

public func closeAshmem(): Unit
```

**Description:** Closes this Ashmem.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### func getAshmemSize()

```cangjie

public func getAshmemSize(): Int32
```

**Description:** Gets the memory size of the Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the memory size of the Ashmem object. |

### func mapReadWriteAshmem()

```cangjie

public func mapReadWriteAshmem(): Unit
```

**Description:** Creates a readable and writable shared file mapping on the virtual address space of this process.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The parameter is not an instance of the Ashmem object. |
  | 1900001 | Failed to call mmap. |

### func mapReadonlyAshmem()

```cangjie

public func mapReadonlyAshmem(): Unit
```

**Description:** Creates a read-only shared file mapping on the virtual address space of this process.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900001 | Failed to call mmap. |

### func mapTypedAshmem(UInt32)

```cangjie

public func mapTypedAshmem(mapType: UInt32): Unit
```

**Description:** Creates a shared file mapping on the virtual address space of this process. The size of the mapped region is specified by this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:---|
| mapType | UInt32 | Yes | - | Specifies the protection level of the mapped memory region. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. Parameter type mismatch;<br>3. The passed mapType exceeds the maximum protection level. |
  | 1900001 | Failed to call mmap. |

### func readDataFromAshmem(Int64, Int64)

```cangjie

public func readDataFromAshmem(size: Int64, offset: Int64): Array<Byte>
```

**Description:** Reads data from the shared file associated with this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:--- |
| size | Int64 | Yes | - | The size of the data to be read. |
| offset | Int64 | Yes | - | The starting position of the data to be read in the memory region associated with this Ashmem object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Byte> | Returns the read data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900004 | Failed to read data from the shared memory. |

### func setProtectionType(UInt32)

```cangjie

public func setProtectionType(protectionType: UInt32): Unit
```

**Description:** Sets the protection level of the mapped memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:--- |
| protectionType | UInt32 | Yes | - | The protection type to be set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900002 | Failed to call ioctl. |

### func unmapAshmem()

```cangjie

public func unmapAshmem(): Unit
```

**Description:** Removes the address mapping of this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### func writeDataToAshmem(Array\<Byte>, Int64, Int64)

```cangjie

public func writeDataToAshmem(buf: Array<Byte>, size: Int64, offset: Int64): Unit
```

**Description:** Writes data to the shared file associated with this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
|:---|:---|:---|:---|:--- |
| buf | Array\<Byte> | Yes | - | The data to be written to the Ashmem object. |
| size | Int64 | Yes | - | The size of the data to be written. |
| offset | Int64 | Yes | - | The starting position of the data to be written in the memory region associated with this Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Failed to obtain arrayBuffer information. |
  | 1900003 | Failed to write data to the shared memory. |## class MessageSequence

```cangjie
public class MessageSequence {}
```

**Function:** During RPC or IPC processes, the sender can use the write methods provided by MessageSequence to write data to be sent into this object in a specific format. The receiver can use the read methods provided by MessageSequence to read data in specific formats from this object. Data formats include: basic types and arrays, IPC objects, interface descriptors, and custom serialized objects.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### static func closeFileDescriptor(Int32)

```cangjie
public static func closeFileDescriptor(fd: Int32): Unit
```

**Function:** Static method to close the given file descriptor.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor to be closed. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |

### static func create()

```cangjie
public static func create(): MessageSequence
```

**Function:** Static method to create a MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [MessageSequence](#class-messagesequence) | Returns the created MessageSequence object. |

**Exceptions:**

- BusinessException: For error codes, see the table below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ahmem object;<br>3. The ashmem instance for obtaining packaging is empty. |

### static func dupFileDescriptor(Int32)

```cangjie
public static func dupFileDescriptor(fd: Int32): Int32
```

**Function:** Static method to duplicate the given file descriptor.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | Represents an existing file descriptor. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the new file descriptor. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900013 | Failed to call dup. |

### func containFileDescriptors()

```cangjie
public func containFileDescriptors(): Bool
```

**Function:** Checks whether this MessageSequence object contains file descriptors.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Contains file descriptors; false: Does not contain file descriptors. |

### func getCapacity()

```cangjie
public func getCapacity(): UInt32
```

**Function:** Gets the capacity size of the current MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The capacity size of the obtained MessageSequence instance, in bytes. |

### func getRawDataCapacity()

```cangjie
public func getRawDataCapacity(): UInt32
```

**Function:** Gets the maximum raw data capacity that MessageSequence can hold.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the maximum raw data capacity that MessageSequence can hold, i.e., 128MB. |

### func getReadPosition()

```cangjie
public func getReadPosition(): UInt32
```

**Function:** Gets the read position of MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the current read position in the MessageSequence instance. |

### func getReadableBytes()

```cangjie
public func getReadableBytes(): UInt32
```

**Function:** Gets the readable byte space of MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The readable byte space of the obtained MessageSequence instance, in bytes. |

### func getSize()

```cangjie
public func getSize(): UInt32
```

**Function:** Gets the data size of the current MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The data size of the obtained MessageSequence instance, in bytes. |

### func getWritableBytes()

```cangjie
public func getWritableBytes(): UInt32
```

**Function:** Gets the writable byte space size of MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The writable byte space of the obtained MessageSequence instance, in bytes. |

### func getWritePosition()

```cangjie
public func getWritePosition(): UInt32
```

**Function:** Gets the write position of MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the current write position in the MessageSequence instance. |

### func readAshmem()

```cangjie
public func readAshmem(): Ashmem
```

**Function:** Reads an anonymous shared object from MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the anonymous shared object. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Check param failed |
  | 1900004 | Failed to read data from the shared memory. |

### func readBoolean()

```cangjie
public func readBoolean(): Bool
```

**Function:** Reads a boolean value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the read boolean value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readBooleanArray()

```cangjie
public func readBooleanArray(): Array<Bool>
```

**Function:** Reads a boolean array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Bool> | Returns the boolean array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readByte()

```cangjie
public func readByte(): Int8
```

**Function:** Reads a byte value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Int8 | Returns the byte value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readByteArray()

```cangjie
public func readByteArray(): Array<Int8>
```

**Function:** Reads a byte array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Int8> | Returns the byte array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readChar()

```cangjie
public func readChar(): UInt8
```

**Function:** Reads a single character value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
|:----|:----|
| UInt8 | Returns the single character array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |### func readCharArray()

```cangjie

public func readCharArray(): Array<UInt8>
```

**Function:** Reads a single character array from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt8> | Returns a single character array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readDouble()

```cangjie

public func readDouble(): Float64
```

**Function:** Reads a double-precision floating-point value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Float64 | Returns a double-precision floating-point value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readDoubleArray()

```cangjie

public func readDoubleArray(): Array<Float64>
```

**Function:** Reads all double-precision floating-point arrays from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Float64> | Returns a double-precision floating-point array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readException()

```cangjie

public func readException(): Unit
```

**Function:** Reads an exception from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readFileDescriptor()

```cangjie

public func readFileDescriptor(): Int32
```

**Function:** Reads a file descriptor from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Returns the file descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readFloat()

```cangjie

public func readFloat(): Float32
```

**Function:** Reads a floating-point value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Float32 | Returns the floating-point value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readFloatArray()

```cangjie

public func readFloatArray(): Array<Float32>
```

**Function:** Reads a floating-point array from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Float32> | Returns the floating-point array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readInt()

```cangjie

public func readInt(): Int32
```

**Function:** Reads an integer value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Returns the integer value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readIntArray()

```cangjie

public func readIntArray(): Array<Int32>
```

**Function:** Reads an integer array from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Int32> | Returns the integer array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readInterfaceToken()

```cangjie

public func readInterfaceToken(): String
```

**Function:** Reads an interface descriptor from the MessageSequence object. The interface descriptors are read in the order they were written to the MessageSequence. Local objects can use this information to verify the current communication.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | Returns the read interface descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readLong()

```cangjie

public func readLong(): Int64
```

**Function:** Reads a long integer value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int64 | Returns the long integer value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readLongArray()

```cangjie

public func readLongArray(): Array<Int64>
```

**Function:** Reads all long integer arrays from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Int64> | Returns the integer array. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readParcelable\<T>(T) where T \<: Parcelable

```cangjie

public func readParcelable<T>(dataIn: T): Unit where T <: Parcelable
```

**Function:** Reads member variables from the MessageSequence instance into the specified object (dataIn).

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| dataIn | T | Yes | - | The object whose member variables need to be read from the MessageSequence. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters. |
  | 1900010 | Failed to read data from the message sequence. |
  | 1900012 | Failed to call the JS callback function. |

### func readParcelableArray\<T>(Array\<T>) where T \<: Parcelable

```cangjie

public func readParcelableArray<T>(parcelableArray: Array<T>): Unit where T <: Parcelable
```

**Function:** Reads a serializable object array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| parcelableArray | Array\<T> | Yes | - | The serializable object array to be read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The length of the array passed when reading is not equal to the length passed when writing to the array; 5. The element does not exist in the array. |
  | 1900010 | Failed to read data from the message sequence. |
  | 1900012 | Failed to call the JS callback function. |

### func readRawDataBuffer(Int64)

```cangjie

public func readRawDataBuffer(size: Int64): Array<Byte>
```

**Function:** Reads raw data from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| size | Int64 | Yes | - | The size of the raw data to be read. |

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Byte> | Returns the raw data (in bytes). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900010 | Failed to read data from the message sequence. |### func readShort()

```cangjie

public func readShort(): Int16
```

**Function:** Reads a short integer value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int16 | Returns the short integer value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readShortArray()

```cangjie

public func readShortArray(): Array<Int16>
```

**Function:** Reads an array of short integers from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Int16> | The array of short integers to be read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readString()

```cangjie

public func readString(): String
```

**Function:** Reads a string value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | Returns the string value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readStringArray()

```cangjie

public func readStringArray(): Array<String>
```

**Function:** Reads an array of strings from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<String> | Returns the array of strings. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

### func readUInt16Array()

```cangjie

public func readUInt16Array(): Array<UInt16>
```

**Function:** Reads data of type Array\<UInt16> from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt16> | The data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Incorrect obtained value of typeCode. |
  | 1900010 | Failed to read data from the message sequence. |

### func readUInt32Array()

```cangjie

public func readUInt32Array(): Array<UInt32>
```

**Function:** Reads data of type Array\<UInt32> from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt32> | The data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Incorrect obtained value of typeCode. |
  | 1900010 | Failed to read data from the message sequence. |

### func readUInt64Array()

```cangjie

public func readUInt64Array(): Array<UInt64>
```

**Function:** Reads data of type Array\<UInt64> from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt64> | The data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Incorrect obtained value of typeCode. |
  | 1900010 | Failed to read data from the message sequence. |

### func readUInt8Array()

```cangjie

public func readUInt8Array(): Array<UInt8>
```

**Function:** Reads data of type Array\<UInt8> from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<UInt8> | The data read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Incorrect obtained value of typeCode. |
  | 1900010 | Failed to read data from the message sequence. |

### func reclaim()

```cangjie

public func reclaim(): Unit
```

**Function:** Releases the MessageSequence object that is no longer in use.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

### func rewindRead(UInt32)

```cangjie

public func rewindRead(pos: UInt32): Unit
```

**Function:** Resets the read position to the specified position.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| pos | UInt32 | Yes | - | The target position to start reading data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |

### func rewindWrite(UInt32)

```cangjie

public func rewindWrite(pos: UInt32): Unit
```

**Function:** Resets the write position to the specified position.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| pos | UInt32 | Yes | - | The target position to start writing data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |

### func setCapacity(UInt32)

```cangjie

public func setCapacity(size: UInt32): Unit
```

**Function:** Sets the storage capacity of the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| size | UInt32 | Yes | - | The storage capacity of the MessageSequence instance, in bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900011 | Memory allocation failed. |

### func setSize(UInt32)

```cangjie

public func setSize(size: UInt32): Unit
```

**Function:** Sets the data size contained in the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| size | UInt32 | Yes | - | The data size of the MessageSequence instance, in bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |

### func writeAshmem(Ashmem)

```cangjie

public func writeAshmem(ashmem: Ashmem): Unit
```

**Function:** Writes the specified anonymous shared object to this MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| ashmem | [Ashmem](#class-ashmem) | Yes | - | The anonymous shared object to be written to the MessageSequence. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. The parameter is not an instance of the Ashmem object. |
  | 1900003 | Failed to write data to the shared memory. |

### func writeBoolean(Bool)

```cangjie

public func writeBoolean(val: Bool): Unit
```

**Function:** Writes a boolean value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| val | Bool | Yes | - | The boolean value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeBooleanArray(Array\<Bool>)

```cangjie

public func writeBooleanArray(booleanArray: Array<Bool>): Unit
```

**Function:** Writes an array of boolean values to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Mandatory | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| booleanArray | Array\<Bool> | Yes | - | The array of boolean values to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array. |
  | 1900009 | Failed to write data to the message sequence. |### func writeByte(Int8)

```cangjie

public func writeByte(val: Int8): Unit
```

**Function:** Writes a byte value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int8 | Yes | - | The byte value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeByteArray(Array\<Int8>)

```cangjie

public func writeByteArray(byteArray: Array<Int8>): Unit
```

**Function:** Writes a byte array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| byteArray | Array\<Int8> | Yes | - | The byte array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeChar(UInt8)

```cangjie

public func writeChar(val: UInt8): Unit
```

**Function:** Writes a single character value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | UInt8 | Yes | - | The single character value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeCharArray(Array\<UInt8>)

```cangjie

public func writeCharArray(charArray: Array<UInt8>): Unit
```

**Function:** Writes a single character array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| charArray | Array\<UInt8> | Yes | - | The single character array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeDouble(Float64)

```cangjie

public func writeDouble(val: Float64): Unit
```

**Function:** Writes a double-precision floating-point value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Float64 | Yes | - | The double-precision floating-point value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeDoubleArray(Array\<Float64>)

```cangjie

public func writeDoubleArray(doubleArray: Array<Float64>): Unit
```

**Function:** Writes a double-precision floating-point array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| doubleArray | Array\<Float64> | Yes | - | The double-precision floating-point array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeFileDescriptor(Int32)

```cangjie

public func writeFileDescriptor(fd: Int32): Unit
```

**Function:** Writes a file descriptor to the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeFloat(Float32)

```cangjie

public func writeFloat(val: Float32): Unit
```

**Function:** Writes a floating-point value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Float32 | Yes | - | The floating-point value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeFloatArray(Array\<Float32>)

```cangjie

public func writeFloatArray(floatArray: Array<Float32>): Unit
```

**Function:** Writes Array\<Float32> type data to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| floatArray | Array\<Float32> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeInt(Int32)

```cangjie

public func writeInt(val: Int32): Unit
```

**Function:** Writes an integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int32 | Yes | - | The integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeIntArray(Array\<Int32>)

```cangjie

public func writeIntArray(intArray: Array<Int32>): Unit
```

**Function:** Writes an integer array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| intArray | Array\<Int32> | Yes | - | The integer array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeInterfaceToken(String)

```cangjie

public func writeInterfaceToken(token: String): Unit
```

**Function:** Writes an interface descriptor to the MessageSequence object. The remote object can use this information to validate the current communication.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| token | String | Yes | - | The string-type descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. The String length exceeds 40960 bytes; 4. The number of bytes copied to the buffer differs from the length of the obtained String. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeLong(Int64)

```cangjie

public func writeLong(val: Int64): Unit
```

**Function:** Writes a long integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int64 | Yes | - | The long integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeLongArray(Array\<Int64>)

```cangjie

public func writeLongArray(longArray: Array<Int64>): Unit
```

**Function:** Writes a long integer array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| longArray | Array\<Int64> | Yes | - | The long integer array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeNoException()

```cangjie

public func writeNoException(): Unit
```

**Function:** Writes "no exception occurred" information to the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 21

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |### func writeParcelable\<T>(T) where T \<: Parcelable

```cangjie

public func writeParcelable<T>(val: T): Unit where T <: Parcelable
```

**Function:** Writes a custom serializable object to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | T | Yes | - | The serializable object to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeParcelableArray\<T>(Array\<T>) where T \<: Parcelable

```cangjie

public func writeParcelableArray<T>(parcelableArray: Array<T>): Unit where T <: Parcelable
```

**Function:** Writes an array of serializable objects to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| parcelableArray | Array\<T> | Yes | - | The array of serializable objects to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeRawDataBuffer(Array\<Byte>, Int64)

```cangjie

public func writeRawDataBuffer(rawData: Array<Byte>, size: Int64): Unit
```

**Function:** Writes raw data to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| rawData | Array\<Byte> | Yes | - | The raw data to be written. |
| size | Int64 | Yes | - | The size of the raw data to be sent, in bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. Failed to obtain array information; 4. Failed to obtain the transferred size; 5. The transferred size is less than or equal to 0; 6. The transferred size exceeds the byte length of rawData. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeShort(Int16)

```cangjie

public func writeShort(val: Int16): Unit
```

**Function:** Writes a short integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int16 | Yes | - | The short integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeShortArray(Array\<Int16>)

```cangjie

public func writeShortArray(shortArray: Array<Int16>): Unit
```

**Function:** Writes an array of short integers to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| shortArray | Array\<Int16> | Yes | - | The array of short integers to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The element does not exist in the array; 5. Incorrect type of the element in the array. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeString(String)

```cangjie

public func writeString(val: String): Unit
```

**Function:** Writes a string value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | String | Yes | - | The string value to be written, with a length less than 40960 bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch; 3. The String length exceeds 40960 bytes; 4. The number of bytes copied to the buffer differs from the length of the obtained String. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeStringArray(Array\<String>)

```cangjie

public func writeStringArray(stringArray: Array<String>): Unit
```

**Function:** Writes an array of strings to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| stringArray | Array\<String> | Yes | - | The array of strings to be written, with each element's length less than 40960 bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. The String length exceeds 40960 bytes; 5. The number of bytes copied to the buffer differs from the length of the obtained String. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeUInt16Array(Array\<UInt16>)

```cangjie

public func writeUInt16Array(buf: Array<UInt16>): Unit
```

**Function:** Writes data of type Array\<UInt16> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt16> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. Incorrect obtained value of typeCode; 5. Failed to obtain array information. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeUInt32Array(Array\<UInt32>)

```cangjie

public func writeUInt32Array(buf: Array<UInt32>): Unit
```

**Function:** Writes data of type Array\<UInt32> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt32> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. Incorrect obtained value of typeCode; 5. Failed to obtain array information. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeUInt64Array(Array\<UInt64>)

```cangjie

public func writeUInt64Array(buf: Array<UInt64>): Unit
```

**Function:** Writes data of type Array\<UInt64> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt64> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. Incorrect obtained value of typeCode; 5. Failed to obtain array information. |
  | 1900009 | Failed to write data to the message sequence. |

### func writeUInt8Array(Array\<UInt8>)

```cangjie

public func writeUInt8Array(buf: Array<UInt8>): Unit
```

**Function:** Writes data of type Array\<UInt8> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 21

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt8> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md) and [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. The parameter is an empty array; 2. Incorrect number of parameters; 3. Parameter type mismatch; 4. Incorrect obtained value of typeCode; 5. Failed to obtain array information. |
  | 1900009 | Failed to write data to the message sequence. |