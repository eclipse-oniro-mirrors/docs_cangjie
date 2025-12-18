# Using HiLog for Logging (Cangjie)

During application development, you can output log information at critical code points. After running the application, you can analyze its execution by reviewing the log information (such as whether the application is running normally, the runtime sequence of the code, and whether the logical branches are functioning correctly).

## Interface Description

HiLog defines five log levels: DEBUG, INFO, WARN, ERROR, and FATAL, and provides corresponding methods to output logs at different levels. The interfaces are listed in the table below. For detailed descriptions, refer to the [API Reference](../reference/PerformanceAnalysisKit/cj-apis-hilog.md).

| Interface Name | Description |
| -------- | -------- |
| isLoggable(domain: UInt32, tag: String, level: LogLevel): Bool | Call this interface before printing logs to check whether logs with the specified domain identifier, log tag, and level can be printed. |
| debug(domain: UInt32, tag: String, format: String, args: Array\<String>): Unit | Outputs DEBUG-level logs. Used only for application/service debugging.<br/>In the DevEco Studio terminal window or cmd, use the command "hdc shell hilogcat" to set the log level to DEBUG. |
| info(domain: UInt32, tag: String, format: String, args: Array\<String>): Unit | Outputs INFO-level logs. Represents general information. |
| warn(domain: UInt32, tag: String, format: String, args: Array\<String>): Unit | Outputs WARN-level logs. Indicates the presence of a warning. |
| error(domain: UInt32, tag: String, format: String, args: Array\<String>): Unit | Outputs ERROR-level logs. Indicates the presence of an error. |
| fatal(domain: UInt32, tag: String, format: String, args: Array\<String>): Unit | Outputs FATAL-level logs. Indicates a fatal or unrecoverable error. |

### Parameter Analysis

> **Note:**
>
> - The `domain` and `tag` used in `isLoggable()` and specific log printing interfaces should be consistent.
>
> - The `level` used in `isLoggable()` should match the level of the specific log printing interface.

- **domain**: Specifies the business domain corresponding to the output log. The value ranges from 0x0000 to 0xFFFF, and developers can customize it as needed.

- **tag**: Specifies the log identifier, which can be any string. It is recommended to identify the calling class or business behavior. The tag can be up to 31 bytes; exceeding this limit will truncate the tag. Chinese characters are not recommended, as they may cause garbled text or alignment issues.

- **level**: Specifies the log level. For possible values, see [LogLevel](../reference/PerformanceAnalysisKit/cj-apis-hilog.md#enum-loglevel).

- **format**: A format string for formatted log output.

- **args**: Parameters for the format string.

## Constraints and Limitations

The maximum log length is 4096 bytes. Text exceeding this limit will be truncated.

## Development Example

Add a click event to a button to print a log when the button is clicked.

1. Create a new project and select "[Cangjie] Empty Ability."

2. In the **Project** window, click entry > src > main > cangjie, then open the index.cj file in the project. Add a button and print a log when the button is clicked.

   Sample code:

   <!-- compile -->

   ```cangjie
    // index.cj

    import kit.PerformanceAnalysisKit.*

    @Entry
    @Component
    class EntryView {
        @State
        var message: String = "Hello World"

        func build() {
            Row {
                Column {
                    Button(this.message)
                        .fontSize(50)
                        .fontWeight(FontWeight.Bold)
                        .onClick ({
                            evt => this.message = "Hello Cangjie"
                            Hilog.isLoggable(0xFF00, "testTag", LogLevel.Info)
                            Hilog.info(0xFF00, "testTag", "hello world")
                            // Set the minimum log level for the application. After setting, logs below the WARN level will not be printed.
                            Hilog.info(0x0000, 'testTag', 'this is an info level log')
                            Hilog.error(0x0000, 'testTag', 'this is an error level log')
                        })
                }.width(100.percent)
            }.height(100.percent)
        }
    }
   ```

   For example, to output an INFO-level message indicating general information, the format string is:

   ```txt
   hello world
   ```

3. Run the project on a real device and click the "Next" button on the application/service interface.

4. At the bottom of DevEco Studio, switch to the "Log" window and set the log filtering conditions.

   Select the current device and process, set the log level to Verbose, and set the search content to "testTag." The window will then display only logs that meet the criteria.

   The printed log results are:

   ```txt
   01-02 08:18:24.947   30988-30988   A0ff00/testTag                  com.example.hilogemo  I     hello World
   01-02 08:18:24.947   30988-30988   A00000/testTag                  com.example.hilogemo  E     this is an error level log
   ```