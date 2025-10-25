# Application File Access (Cangjie)

Applications need to perform operations such as viewing, creating, reading, writing, deleting, moving, copying, and retrieving attributes on application files within the application file directory. The specific methods are described below.

## Interface Description

Developers can implement application file access capabilities through basic file operation interfaces ([ohos.file_fs](../../../en/application-dev/reference/CoreFileKit/cj-apis-file_fs.md)). The main functionalities are listed in the following table.

| Interface Name | Functionality | Interface Type |
| ------------ | ---------------------- | -------- |
| access       | Check if a file exists | Method   |
| close        | Close a file           | Method   |
| copyFile     | Copy a file            | Method   |
| createStream | Open a file stream based on file path | Method |
| listFile     | List all filenames in a directory | Method |
| mkdir        | Create a directory     | Method   |
| moveFile     | Move a file            | Method   |
| open         | Open a file            | Method   |
| read         | Read data from a file  | Method   |
| rename       | Rename a file or directory | Method |
| rmdir        | Delete an entire directory | Method |
| stat         | Retrieve detailed file attribute information | Method |
| unlink       | Delete a single file   | Method   |
| write        | Write data to a file   | Method   |
| Stream.close | Close a file stream    | Method   |
| Stream.flush | Flush a file stream    | Method   |
| Stream.write | Write data to a stream file | Method |
| Stream.read  | Read data from a stream file | Method |
| File.fd      | Retrieve file descriptor | Property |
| OpenMode     | Set file opening flags | Property |
| Filter       | Set file filtering configuration items | Type |

## Development Examples

Before accessing application files, developers need to obtain the application file path. The following example demonstrates how to retrieve the HAP-level file path from AbilityContext. For details on obtaining AbilityContext, refer to [Obtaining UIAbility Context Information](../application-models/cj-uiability-usage.md#obtaining-context-information-of-uiability).

Below are examples of several common operations.

### Creating and Reading/Writing a File

The following example code demonstrates how to create a new file and perform read/write operations on it.
> Note:
>
> For Global definition, refer to [Usage Instructions](../../../en/application-dev/reference/cj-development-intro.md)

<!-- compile -->

```cangjie
// xxx.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// Refer to the "Obtaining UIAbility Context Information" section
let context = Global.getAbilityContext() // Obtain the context application context; see usage instructions for details
// Obtain the application file path
let filesDir = context.filesDirectory

func createFile(): Unit {
    // Create and open the file if it does not exist; open the file if it exists
    let file = FileFs.open(filesDir + '/test.txt', mode: OpenMode.READ_WRITE.mode | OpenMode.CREATE.mode)
    // Write content to the file
    let writeLen = FileFs.write(file.fd, "Try to write str.")
    AppLog.info("The length of str is: ${writeLen}")
    let bufSize = 4096
    var readSize = 0
    // Create an Array<Byte> object of size 1024 bytes to store data read from the file
    let array = Array<Byte>(1024, repeat: 0)
    // Set the read offset and length
    let readOptions = ReadOptions(
        offset: readSize,
        length: UIntNative(bufSize)
    )
    // Read file content into the ArrayBuffer object and return the actual number of bytes read
    let readLen = FileFs.read(file.fd, array, options: readOptions)
    AppLog.info("the content of file: ${String.fromUtf8(array[..readLen])}")
    // Close the file
    FileFs.close(file)
}
```

### Reading File Content and Writing to Another File

The following example code demonstrates how to read content from one file and write it to another file.

<!-- compile -->

```cangjie
// xxx.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// Refer to the "Obtaining UIAbility Context Information" section
let context = Global.getAbilityContext() // Obtain the context application context; see usage instructions for details
// Obtain the application file path
let filesDir = context.filesDirectory

func readWriteFile() {
    // Open the file
    let srcFile = FileFs.open(filesDir + '/test.txt', mode: OpenMode.READ_WRITE.mode | OpenMode.CREATE.mode)
    let destFile = FileFs.open(filesDir + '/destFile.txt', mode: OpenMode.READ_WRITE.mode | OpenMode.CREATE.mode)
    // Read content from the source file and write it to the destination file
    let bufSize = 4096
    var readSize = 0
    let buf = Array<Byte>(bufSize, repeat: 0)
    var readOptions = ReadOptions(
        offset: readSize,
        length: UIntNative(bufSize)
    )
    var readLen = FileFs.read(srcFile.fd, buf, options: readOptions)
    while (readLen > 0) {
        readSize += readLen
        let writeOptions = WriteOptions(
            length: UIntNative(readLen)
        )
        FileFs.write(destFile.fd, buf, options: writeOptions)
        readOptions.offset = readSize
        readLen = FileFs.read(srcFile.fd, buf, options: readOptions)
    }
    // Close the file
    FileFs.close(srcFile)
    FileFs.close(destFile)
}
```

> **Note:**
>
> When using read/write interfaces, pay attention to the offset parameter setting. For existing files that have been read or written, the file offset pointer defaults to the end position of the last read/write operation.

### Reading/Writing Files Using Streams

The following example code demonstrates how to use stream interfaces to read content from test.txt and write it to destFile.txt.

<!-- compile -->

```cangjie
// xxx.cj
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// Refer to the "Obtaining UIAbility Context Information" section
let context = getContext()
// Obtain the application file path
let filesDir = context.filesDirectory

func readWriteFileWithStream() {
    // Create and open the input file stream
    let inputStream = FileFs.createStream(filesDir + '/test.txt', 'r+')
    // Create and open the output file stream
    let outputStream = FileFs.createStream(filesDir + '/destFile.txt', "w+")

    let bufSize = 4096
    var readSize = 0
    let buf = Array<Byte>(bufSize, repeat: 0)
    var readOptions = ReadOptions(
        offset: readSize,
        length: UIntNative(bufSize)
    )
    // Read content from the source file using streams and write it to the destination file
    var readLen = inputStream.read(buf, options: readOptions)
    readSize += readLen
    while (readLen > 0) {
        outputStream.write(buf[0..readLen])
        readOptions.offset = readSize
        readLen = inputStream.read(buf, options: readOptions)
        readSize += readLen
    }
    // Close the file stream
    inputStream.close()
    outputStream.close()
}
```

> **Note:**
>
> When using stream interfaces, ensure timely closure of streams. Stream interfaces do not support concurrent read/write operations.

### Viewing File List

The following example code demonstrates how to view a file list.

<!-- compile -->

```cangjie
import kit.CoreFileKit.*
import kit.CoreFileKit.*
import kit.AbilityKit.*
import ohos.base.*

// Refer to the "Obtaining UIAbility Context Information" section
let context = getContext()
// Obtain the application file path
let filesDir = context.filesDirectory

// View file list
func getListFile() {
    let listFileOption = ListFileOptions(
        recursion: false,
        listNum: 0,
        filter: Filter(
            suffix: [".png", ".jpg", ".txt"],
            displayName: ["test*"],
            fileSizeOver: 0,
            lastModifiedAfter: 10000.0
        )
    )
    let files = FileFs.listFile(filesDir, options: listFileOption)
    for (item in files) {
        AppLog.info("The name of file: ${item}")
    }
}
```