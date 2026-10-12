# ohos.rpc

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

This module provides inter-process communication (IPC) capabilities, including intra-device IPC (based on Binder driver) and inter-device IPC (RPC, based on soft bus driver).

## Import Module

```cangjie
import kit.IPCKit.*
```

## Usage Instructions

API sample code usage instructions:

- If the sample code contains a "// index.cj" comment in its first line, it indicates the example can be compiled and run in the "index.cj" file of the Cangjie template project.
- If the sample requires obtaining the [Context](../AbilityKit/cj-apis-app-ability-ui_ability.md#class-context) application context, it needs to be configured in the "main_ability.cj" file of the Cangjie template project.

For details about the sample project and configuration template, see [Cangjie Sample Code Instructions](../cj-development-intro.md#Cangjie-Sample-Code-Instructions).

## interface Parcelable

```cangjie
public interface Parcelable {

    func marshalling(dataOut: MessageSequence): Bool

    func unmarshalling(dataIn: MessageSequence): Bool
}
```

**Description:** During inter-process communication (IPC), serializes class objects into MessageSequence and deserializes them from MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### func marshalling(MessageSequence)

```cangjie
func marshalling(dataOut: MessageSequence): Bool
```

**Description:** Marshals this serializable object into a MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
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

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
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

**Since:** 22

### static const PROT_EXEC

```cangjie
public static const PROT_EXEC: UInt32 = 4
```

**Description:** The mapped memory is executable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### static const PROT_NONE

```cangjie
public static const PROT_NONE: UInt32 = 0
```

**Description:** The mapped memory is inaccessible.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### static const PROT_READ

```cangjie
public static const PROT_READ: UInt32 = 1
```

**Description:** The mapped memory is readable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### static const PROT_WRITE

```cangjie
public static const PROT_WRITE: UInt32 = 2
```

**Description:** The mapped memory is writable.

**Type:** UInt32

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### static func create(String, Int32)

```cangjie
public static func create(name: String, size: Int32): Ashmem
```

**Description:** Static method that creates an Ashmem object by copying the file descriptor (fd) of an existing Ashmem object. Both Ashmem objects point to the same shared memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| name | String | Yes | - | Name used to query Ashmem information. |
| size | Int32 | Yes | - | Size of the Ashmem in bytes. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the created Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ashmem object;<br>3. The Ashmem instance for obtaining packaging is empty. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func create(Ashmem)

```cangjie
public static func create(ashmem: Ashmem): Ashmem
```

**Description:** Static method that creates an Ashmem object by copying the file descriptor (fd) of an existing Ashmem object. Both Ashmem objects point to the same shared memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| ashmem | [Ashmem](#class-ashmem) | Yes | - | Existing Ashmem object. |

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the created Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ashmem object;<br>3. The Ashmem instance for obtaining packaging is empty. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024) //static func create(String, Int32)
    let ashmem2 = Ashmem.create(ashmem) //static func create(Ashmem)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func closeAshmem()

```cangjie
public func closeAshmem(): Unit
```

**Description:** Closes this Ashmem.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.closeAshmem()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getAshmemSize()

```cangjie
public func getAshmemSize(): Int32
```

**Description:** Gets the memory size of the Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the memory size of the Ashmem object. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.getAshmemSize()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func mapReadWriteAshmem()

```cangjie
public func mapReadWriteAshmem(): Unit
```

**Description:** Creates a readable and writable shared file mapping in the virtual address space of this process.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900001 | Failed to call mmap. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.mapReadWriteAshmem()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func mapReadonlyAshmem()

```cangjie
public func mapReadonlyAshmem(): Unit
```

**Description:** Creates a read-only shared file mapping in the virtual address space of this process.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900001 | Failed to call mmap. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.mapReadonlyAshmem()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func mapTypedAshmem(UInt32)

```cangjie
public func mapTypedAshmem(mapType: UInt32): Unit
```

**Description:** Creates a shared file mapping in the virtual address space of this process. The size of the mapped region is specified by this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| mapType | UInt32 | Yes | - | Specifies the protection level of the mapped memory region. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900001 | Failed to call mmap. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.mapTypedAshmem(Ashmem.PROT_READ | Ashmem.PROT_WRITE)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readDataFromAshmem(Int64, Int64)

```cangjie
public func readDataFromAshmem(size: Int64, offset: Int64): Array<Byte>
```

**Description:** Reads data from the shared file associated with this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| size | Int64 | Yes | - | Size of the data to read. |
| offset | Int64 | Yes | - | Starting position of the data to read in the memory region associated with this Ashmem object. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Byte> | Returns the read data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900004 | Failed to read data from the shared memory. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.readDataFromAshmem(1, 0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setProtectionType(UInt32)

```cangjie
public func setProtectionType(protectionType: UInt32): Unit
```

**Description:** Sets the protection level of the mapped memory region.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| protectionType | UInt32 | Yes | - | Protection type to set. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900002 | Failed to call ioctl. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.setProtectionType(Ashmem.PROT_READ)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func unmapAshmem()

```cangjie
public func unmapAshmem(): Unit
```

**Description:** Removes the address mapping of this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.unmapAshmem()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeDataToAshmem(Array\<Byte>, Int64, Int64)

```cangjie
public func writeDataToAshmem(buf: Array<Byte>, size: Int64, offset: Int64): Unit
```

**Description:** Writes data to the shared file associated with this Ashmem object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<Byte> | Yes | - | Data to write to the Ashmem object. |
| size | Int64 | Yes | - | Size of the data to write. |
| offset | Int64 | Yes | - | Starting position of the data to write in the memory region associated with this Ashmem object. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900003 | Failed to write data to the shared memory. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let ashmem = Ashmem.create("ashmem", 1024*1024)
    ashmem.writeDataToAshm## class MessageSequence

```cangjie
public class MessageSequence {}
```

**Description:** Provides APIs for reading and writing data in specific format. During RPC or IPC, the sender can use the **write()** method provided by **MessageSequence** to write data in specific format to a **MessageSequence** object. The receiver can use the **read()** method provided by **MessageSequence** to read data in specific format from a **MessageSequence** object. The data formats include basic data types and arrays, IPC objects, interface tokens, and custom sequenceable objects. The read sequence must be the same as the write sequence. Otherwise, data parsing errors occurs.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

### static func closeFileDescriptor(Int32)

```cangjie
public static func closeFileDescriptor(fd: Int32): Unit
```

**Description:** Static method to close a given file descriptor.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor to be closed. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes: 1. Incorrect number of parameters; 2. Parameter type mismatch. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let filePath = "path/to/file"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    MessageSequence.closeFileDescriptor(file.fd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func create()

```cangjie
public static func create(): MessageSequence
```

**Description:** Static method to create a MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [MessageSequence](#class-messagesequence) | Returns the created MessageSequence object. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, refer to [Universal Error Codes](../cj-errorcode-universal.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 401 | Parameter error. Possible causes:<br>1. Incorrect number of parameters;<br>2. The passed parameter is not an Ahmem object;<br>3. The ashmem instance for obtaining packaging is empty. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### static func dupFileDescriptor(Int32)

```cangjie
public static func dupFileDescriptor(fd: Int32): Int32
```

**Description:** Static method to duplicate a given file descriptor.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | Represents an existing file descriptor. |

**Return Value:**

| Type | Description |
|:----|:----|
| Int32 | Returns the new file descriptor. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900013 | Failed to call dup. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let filePath = "path/to/file"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    MessageSequence.dupFileDescriptor(file.fd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func containFileDescriptors()

```cangjie
public func containFileDescriptors(): Bool
```

**Description:** Checks whether this MessageSequence object contains file descriptors.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | true: Contains file descriptors; false: Does not contain file descriptors. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.containFileDescriptors()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getCapacity()

```cangjie
public func getCapacity(): UInt32
```

**Description:** Gets the capacity size of the current MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The capacity size of the MessageSequence instance, in bytes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let result = data.getCapacity()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getRawDataCapacity()

```cangjie
public func getRawDataCapacity(): UInt32
```

**Description:** Gets the maximum raw data capacity that MessageSequence can hold.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the maximum raw data capacity that MessageSequence can hold, which is 128MB. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.getRawDataCapacity()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getReadPosition()

```cangjie
public func getReadPosition(): UInt32
```

**Description:** Gets the read position of the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the current read position in the MessageSequence instance. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let pos = data.getReadPosition()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getReadableBytes()

```cangjie
public func getReadableBytes(): UInt32
```

**Description:** Gets the readable byte space of the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The readable byte space of the MessageSequence instance, in bytes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let bytes = data.getReadableBytes()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getSize()

```cangjie
public func getSize(): UInt32
```

**Description:** Gets the data size of the current MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The data size of the MessageSequence instance, in bytes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let size = data.getSize()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func getWritableBytes()

```cangjie
public func getWritableBytes(): UInt32
```

**Description:** Gets the writable byte space size of the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | The writable byte space of the MessageSequence instance, in bytes. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let bytes = data.getWritableBytes()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func getWritePosition()

```cangjie
public func getWritePosition(): UInt32
```

**Function:** Gets the write position of the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt32 | Returns the current write position in the MessageSequence instance. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let pos = data.getWritePosition()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readAshmem()

```cangjie
public func readAshmem(): Ashmem
```

**Function:** Reads an anonymous shared object from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| [Ashmem](#class-ashmem) | Returns the anonymous shared object. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900004 | Failed to read data from the shared memory. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let ashMem = data.readAshmem()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readBoolean()

```cangjie
public func readBoolean(): Bool
```

**Function:** Reads a boolean value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Bool | Returns the read boolean value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readBoolean()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readBooleanArray()

```cangjie
public func readBooleanArray(): Array<Bool>
```

**Function:** Reads a boolean array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Bool> | Returns the boolean array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readBooleanArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readByte()

```cangjie
public func readByte(): Int8
```

**Function:** Reads a byte value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int8 | Returns the byte value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readByte()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readByteArray()

```cangjie
public func readByteArray(): Array<Int8>
```

**Function:** Reads a byte array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Int8> | Returns the byte array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :--- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readByteArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readChar()

```cangjie
public func readChar(): UInt8
```

**Function:** Reads a single character value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| UInt8 | Returns the single character value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readChar()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readCharArray()

```cangjie
public func readCharArray(): Array<UInt8>
```

**Function:** Reads a single character array from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt8> | Returns the single character array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readCharArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readDouble()

```cangjie
public func readDouble(): Float64
```

**Function:** Reads a double-precision floating-point value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Float64 | Returns the double-precision floating-point value. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readDouble()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readDoubleArray()

```cangjie
public func readDoubleArray(): Array<Float64>
```

**Function:** Reads all double-precision floating-point arrays from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Float64> | Returns the double-precision floating-point array. |

**Exceptions:**

- BusinessException: For detailed error codes, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import std.collection.ArrayList
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readDoubleArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func readException()

```cangjie
public func readException(): Unit
```

**Function:** Reads an exception from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readException()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readFileDescriptor()

```cangjie
public func readFileDescriptor(): Int32
```

**Function:** Reads a file descriptor from the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Returns the file descriptor. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readFileDescriptor()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readFloat()

```cangjie
public func readFloat(): Float32
```

**Function:** Reads a floating-point value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Float32 | Returns the floating-point value. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readFloat()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readFloatArray()

```cangjie
public func readFloatArray(): Array<Float32>
```

**Function:** Reads an array of floating-point values from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Float32> | Returns the array of floating-point values. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readFloatArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readInt()

```cangjie
public func readInt(): Int32
```

**Function:** Reads an integer value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int32 | Returns the integer value. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readInt()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readIntArray()

```cangjie
public func readIntArray(): Array<Int32>
```

**Function:** Reads an array of integer values from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Int32> | Returns the array of integer values. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readIntArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readInterfaceToken()

```cangjie
public func readInterfaceToken(): String
```

**Function:** Reads an interface token from the MessageSequence object. The interface tokens are read in the order they were written to the MessageSequence. Local objects can use this information to verify the current communication.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| String | Returns the read interface token. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readInterfaceToken()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readLong()

```cangjie
public func readLong(): Int64
```

**Function:** Reads a long integer value from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Int64 | Returns the long integer value. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readLong()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readLongArray()

```cangjie
public func readLongArray(): Array<Int64>
```

**Function:** Reads an array of long integer values from the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
| :---- | :---- |
| Array\<Int64> | Returns the array of long integer values. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readLongArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readParcelable\<T>(T) where T \<: Parcelable

```cangjie
public func readParcelable<T>(dataIn: T): Unit where T <: Parcelable
```

**Function:** Reads member variables from the MessageSequence instance into the specified object (dataIn).

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| dataIn | T | Yes | - | The object into which member variables will be read from the MessageSequence. |

**Exceptions:**

- BusinessException: Error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |
  | 1900012 | Failed to call the JS callback function. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added to dependency definitions
    class MyParcelable <: Parcelable {
        var num: Int32 = 0
        var str: String = ''

        init() {}

        init(num: Int32, str: String) {
            this.num = num
            this.str = str
        }
        public func marshalling(messageSequence: MessageSequence): Bool {
            messageSequence.writeInt(this.num)
            messageSequence.writeString(this.str)
            return true
        }
        public func unmarshalling(messageSequence: MessageSequence): Bool {
            this.num = messageSequence.readInt()
            this.str = messageSequence.readString()
            return true
        }
    }

    let parcelable = MyParcelable(1, "aaa")
    let data = MessageSequence.create()
    data.writeParcelable(parcelable)
    let ret = MyParcelable()
    data.readParcelable(ret)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func readParcelableArray\<T>(Array\<T>) where T \<: Parcelable

```cangjie
public func readParcelableArray<T>(parcelableArray: Array<T>): Unit where T <: Parcelable
```

**Function:** Reads an array of parcelable objects from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| parcelableArray | Array\<T> | Yes | - | The array of parcelable objects to be read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |
  | 1900012 | Failed to call the JS callback function. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added in dependency definitions
    class MyParcelable <: Parcelable {
        var num: Int32 = 0
        var str: String = ''

        init() {}

        init(num: Int32, str: String) {
            this.num = num
            this.str = str
        }
        public func marshalling(messageSequence: MessageSequence): Bool {
            messageSequence.writeInt(this.num)
            messageSequence.writeString(this.str)
            return true
        }
        public func unmarshalling(messageSequence: MessageSequence): Bool {
            this.num = messageSequence.readInt()
            this.str = messageSequence.readString()
            return true
        }
    }

    let parcelable = MyParcelable(1, "aaa")
    let parcelable2 = MyParcelable(2, "bbb")
    let parcelable3 = MyParcelable(3, "ccc")
    let data = MessageSequence.create()
    data.writeParcelableArray(parcelable, parcelable2, parcelable3)
    let ret: Array<Parcelable> = [MyParcelable(0, ""), MyParcelable(0, ""), MyParcelable(0, "")]
    data.readParcelableArray(ret)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readRawDataBuffer(Int64)

```cangjie
public func readRawDataBuffer(size: Int64): Array<Byte>
```

**Function:** Reads raw data from a MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| size | Int64 | Yes | - | The size of the raw data to be read. |

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Byte> | Returns the raw data (in bytes). |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readRawDataBuffer(1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readShort()

```cangjie
public func readShort(): Int16
```

**Function:** Reads a short integer value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Int16 | Returns the short integer value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readShort()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readShortArray()

```cangjie
public func readShortArray(): Array<Int16>
```

**Function:** Reads an array of short integers from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<Int16> | The array of short integers to be read. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readShortArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readString()

```cangjie
public func readString(): String
```

**Function:** Reads a string value from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| String | Returns the string value. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readString()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readStringArray()

```cangjie
public func readStringArray(): Array<String>
```

**Function:** Reads an array of strings from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<String> | Returns the array of strings. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readStringArray()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readUInt16Array()

```cangjie
public func readUInt16Array(): Array<UInt16>
```

**Function:** Reads data of type Array\<UInt16> from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt16> | The read data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readUInt16Array()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readUInt32Array()

```cangjie
public func readUInt32Array(): Array<UInt32>
```

**Function:** Reads data of type Array\<UInt32> from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt32> | The read data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readUInt32Array()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func readUInt64Array()

```cangjie
public func readUInt64Array(): Array<UInt64>
```

**Function:** Reads data of type Array\<UInt64> from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type | Description |
|:----|:----|
| Array\<UInt64> | The read data. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900010 | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readUInt64Array()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func readUInt8Array()

```cangjie
public func readUInt8Array(): Array<UInt8>
```

**Function:** Reads data of type Array\<UInt8> from a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Return Value:**

| Type         | Description       |
| :----------- | :---------------- |
| Array\<UInt8> | The read data.    |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900010      | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.readUInt8Array()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func reclaim()

```cangjie
public func reclaim(): Unit
```

**Function:** Releases a MessageSequence object that is no longer in use.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.reclaim()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func rewindRead(UInt32)

```cangjie
public func rewindRead(pos: UInt32): Unit
```

**Function:** Resets the read position to the specified offset.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description                     |
| :-------- | :---- | :------- | :------ | :------------------------------ |
| pos       | UInt32 | Yes      | -       | The target position to start reading data. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900010      | Failed to read data from the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.rewindRead(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func rewindWrite(UInt32)

```cangjie
public func rewindWrite(pos: UInt32): Unit
```

**Function:** Resets the write position to the specified offset.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description                     |
| :-------- | :---- | :------- | :------ | :------------------------------ |
| pos       | UInt32 | Yes      | -       | The target position to start writing data. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.rewindWrite(0)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setCapacity(UInt32)

```cangjie
public func setCapacity(size: UInt32): Unit
```

**Function:** Sets the storage capacity of a MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description                     |
| :-------- | :---- | :------- | :------ | :------------------------------ |
| size      | UInt32 | Yes      | -       | The storage capacity of the MessageSequence instance, in bytes. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900011      | Memory allocation failed.             |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.setCapacity(100)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func setSize(UInt32)

```cangjie
public func setSize(size: UInt32): Unit
```

**Function:** Sets the data size contained in a MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type  | Required | Default | Description                     |
| :-------- | :---- | :------- | :------ | :------------------------------ |
| size      | UInt32 | Yes      | -       | The data size of the MessageSequence instance, in bytes. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.setSize(16)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeAshmem(Ashmem)

```cangjie
public func writeAshmem(ashmem: Ashmem): Unit
```

**Function:** Writes the specified anonymous shared memory object to this MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type    | Required | Default | Description                     |
| :-------- | :------ | :------- | :------ | :------------------------------ |
| ashmem    | [Ashmem](#class-ashmem) | Yes      | -       | The anonymous shared memory object to write to the MessageSequence. |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900003      | Failed to write data to the shared memory. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let ashmem = Ashmem.create("ashmem", 1024)
    data.writeAshmem(ashmem)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeBoolean(Bool)

```cangjie
public func writeBoolean(val: Bool): Unit
```

**Function:** Writes a boolean value to a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description                     |
| :-------- | :--- | :------- | :------ | :------------------------------ |
| val       | Bool | Yes      | -       | The boolean value to write.     |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeBoolean(false)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeBooleanArray(Array\<Bool>)

```cangjie
public func writeBooleanArray(booleanArray: Array<Bool>): Unit
```

**Function:** Writes a boolean array to a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter     | Type         | Required | Default | Description                     |
| :------------ | :----------- | :------- | :------ | :------------------------------ |
| booleanArray  | Array\<Bool> | Yes      | -       | The boolean array to write.     |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeBooleanArray([false, true, false])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeByte(Int8)

```cangjie
public func writeByte(val: Int8): Unit
```

**Function:** Writes a byte value to a MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description                     |
| :-------- | :--- | :------- | :------ | :------------------------------ |
| val       | Int8 | Yes      | -       | The byte value to write.        |

**Exceptions:**

- BusinessException: Error codes are listed below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message                          |
  | :----------- | :------------------------------------- |
  | 1900009      | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeByte(2)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func writeByteArray(Array\<Int8>)

```cangjie
public func writeByteArray(byteArray: Array<Int8>): Unit
```

**Function:** Writes a byte array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| byteArray | Array\<Int8> | Yes | - | The byte array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeByteArray([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeChar(UInt8)

```cangjie
public func writeChar(val: UInt8): Unit
```

**Function:** Writes a single character value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | UInt8 | Yes | - | The single character value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeChar(97)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeCharArray(Array\<UInt8>)

```cangjie
public func writeCharArray(charArray: Array<UInt8>): Unit
```

**Function:** Writes a single character array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| charArray | Array\<UInt8> | Yes | - | The single character array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeCharArray([97, 98, 88])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeDouble(Float64)

```cangjie
public func writeDouble(val: Float64): Unit
```

**Function:** Writes a double-precision floating-point value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Float64 | Yes | - | The double-precision floating-point value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeDouble(10.2)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeDoubleArray(Array\<Float64>)

```cangjie
public func writeDoubleArray(doubleArray: Array<Float64>): Unit
```

**Function:** Writes a double-precision floating-point array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| doubleArray | Array\<Float64> | Yes | - | The double-precision floating-point array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeDoubleArray([1.1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeFileDescriptor(Int32)

```cangjie
public func writeFileDescriptor(fd: Int32): Unit
```

**Function:** Writes a file descriptor to the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| fd | Int32 | Yes | - | The file descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import kit.CoreFileKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    let filePath = "path/to/file"
    let file = FileIo.open(filePath, mode: (OpenMode.CREATE | OpenMode.READ_WRITE))
    data.writeFileDescriptor(file.fd)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeFloat(Float32)

```cangjie
public func writeFloat(val: Float32): Unit
```

**Function:** Writes a floating-point value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Float32 | Yes | - | The floating-point value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeFloat(1.2)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeFloatArray(Array\<Float32>)

```cangjie
public func writeFloatArray(floatArray: Array<Float32>): Unit
```

**Function:** Writes a floating-point array to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| floatArray | Array\<Float32> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeFloatArray([1.1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeInt(Int32)

```cangjie
public func writeInt(val: Int32): Unit
```

**Function:** Writes an integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter Name | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int32 | Yes | - | The integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeInt(10)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func writeIntArray(Array\<Int32>)

```cangjie
public func writeIntArray(intArray: Array<Int32>): Unit
```

**Function:** Writes an integer array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| intArray | Array\<Int32> | Yes | - | The integer array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeIntArray([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeInterfaceToken(String)

```cangjie
public func writeInterfaceToken(token: String): Unit
```

**Function:** Writes an interface descriptor to the MessageSequence object. The remote object can use this information to validate the communication.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| token | String | Yes | - | The string-type descriptor. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeInterfaceToken("aaa")
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeLong(Int64)

```cangjie
public func writeLong(val: Int64): Unit
```

**Function:** Writes a long integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| val | Int64 | Yes | - | The long integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeLong(10000)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeLongArray(Array\<Int64>)

```cangjie
public func writeLongArray(longArray: Array<Int64>): Unit
```

**Function:** Writes a long integer array to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| longArray | Array\<Int64> | Yes | - | The long integer array to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeLongArray([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeNoException()

```cangjie
public func writeNoException(): Unit
```

**Function:** Writes an "indication of no exception occurred" message to the MessageSequence.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeNoException()
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeParcelable\<T>(T) where T \<: Parcelable

```cangjie
public func writeParcelable<T>(val: T): Unit where T <: Parcelable
```

**Function:** Writes a custom serializable object to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| val | T | Yes | - | The serializable object to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added in dependency definitions
    class MyParcelable <: Parcelable {
        var num: Int32 = 0
        var str: String = ''

        init() {}

        init(num: Int32, str: String) {
            this.num = num
            this.str = str
        }
        public func marshalling(messageSequence: MessageSequence): Bool {
            messageSequence.writeInt(this.num)
            messageSequence.writeString(this.str)
            return true
        }
        public func unmarshalling(messageSequence: MessageSequence): Bool {
            this.num = messageSequence.readInt()
            this.str = messageSequence.readString()
            return true
        }
    }

    let parcelable = MyParcelable(1, "aaa")
    let data = MessageSequence.create()
    data.writeParcelable(parcelable)
    let ret = MyParcelable()
    data.readParcelable(ret)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeParcelableArray\<T>(Array\<T>) where T \<: Parcelable

```cangjie
public func writeParcelableArray<T>(parcelableArray: Array<T>): Unit where T <: Parcelable
```

**Function:** Writes an array of serializable objects to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| parcelableArray | Array\<T> | Yes | - | The array of serializable objects to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    // The following code can be added in dependency definitions
    class MyParcelable <: Parcelable {
        var num: Int32 = 0
        var str: String = ''

        init() {}

        init(num: Int32, str: String) {
            this.num = num
            this.str = str
        }
        public func marshalling(messageSequence: MessageSequence): Bool {
            messageSequence.writeInt(this.num)
            messageSequence.writeString(this.str)
            return true
        }
        public func unmarshalling(messageSequence: MessageSequence): Bool {
            this.num = messageSequence.readInt()
            this.str = messageSequence.readString()
            return true
        }
    }

    let parcelable = MyParcelable(1, "aaa")
    let parcelable2 = MyParcelable(2, "bbb")
    let parcelable3 = MyParcelable(3, "ccc")
    let data = MessageSequence.create()
    data.writeParcelableArray(parcelable, parcelable2, parcelable3)
    let ret: Array<Parcelable> = [MyParcelable(0, ""), MyParcelable(0, ""), MyParcelable(0, "")]
    data.readParcelableArray(ret)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeRawDataBuffer(Array\<Byte>, Int64)

```cangjie
public func writeRawDataBuffer(rawData: Array<Byte>, size: Int64): Unit
```

**Function:** Writes raw data to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Since:** 22

**Parameters:**

| Parameter | Type | Required | Default | Description |
|:---|:---|:---|:---|:---|
| rawData | Array\<Byte> | Yes | - | The raw data to be written. |
| size | Int64 | Yes | - | The size of the raw data to be sent, in bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, see [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeRawDataBuffer([1], 1)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```### func writeShort(Int16)

```cangjie
public func writeShort(val: Int16): Unit
```

**Function:** Writes a short integer value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | Int16 | Yes | - | The short integer value to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeShort(8)
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeShortArray(Array\<Int16>)

```cangjie
public func writeShortArray(shortArray: Array<Int16>): Unit
```

**Function:** Writes an array of short integers to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| shortArray | Array\<Int16> | Yes | - | The array of short integers to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeShortArray([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeString(String)

```cangjie
public func writeString(val: String): Unit
```

**Function:** Writes a string value to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| val | String | Yes | - | The string value to be written. Its length should be less than 40960 bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeString('abc')
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeStringArray(Array\<String>)

```cangjie
public func writeStringArray(stringArray: Array<String>): Unit
```

**Function:** Writes an array of strings to the MessageSequence instance.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| stringArray | Array\<String> | Yes | - | The array of strings to be written. The length of each element in the array should be less than 40960 bytes. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeStringArray(["abc", "def"])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeUInt16Array(Array\<UInt16>)

```cangjie
public func writeUInt16Array(buf: Array<UInt16>): Unit
```

**Function:** Writes data of type Array\<UInt16> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt16> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeUInt16Array([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeUInt32Array(Array\<UInt32>)

```cangjie
public func writeUInt32Array(buf: Array<UInt32>): Unit
```

**Function:** Writes data of type Array\<UInt32> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt32> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeUInt32Array([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeUInt64Array(Array\<UInt64>)

```cangjie
public func writeUInt64Array(buf: Array<UInt64>): Unit
```

**Function:** Writes data of type Array\<UInt64> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt64> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeUInt64Array([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```

### func writeUInt8Array(Array\<UInt8>)

```cangjie
public func writeUInt8Array(buf: Array<UInt8>): Unit
```

**Function:** Writes data of type Array\<UInt8> to the MessageSequence object.

**System Capability:** SystemCapability.Communication.IPC.Core

**Initial Version:** 22

**Parameters:**

| Parameter | Type | Required | Default Value | Description |
|:---|:---|:---|:---|:---|
| buf | Array\<UInt8> | Yes | - | The data to be written. |

**Exceptions:**

- BusinessException: Corresponding error codes are listed in the table below. For details, refer to [RPC Error Codes](./cj-errorcode-rpc.md).

  | Error Code ID | Error Message |
  | :---- | :--- |
  | 1900009 | Failed to write data to the message sequence. |

**Example:**

<!-- compile -->

```cangjie
// index.cj

import kit.IPCKit.*
import ohos.business_exception.BusinessException
import kit.PerformanceAnalysisKit.Hilog

try {
    let data = MessageSequence.create()
    data.writeUInt8Array([1])
} catch (e: BusinessException) {
    Hilog.info(0, "test", "${e.message}")
}
```