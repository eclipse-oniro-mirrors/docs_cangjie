# Crash Event Introduction

HiAppEvent provides interfaces for subscribing to system crash events.

[Subscribe to Crash Events (Cangjie)](./cj-hiappevent-watcher-crash-events-cangjie.md)

The detailed description of the params attribute in crash event information is as follows:

**params Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | -------------------------------- |
| time     | Int32 | Event trigger time in milliseconds. |
| crash_type | String | Crash type. Supports two crash types: CjError and NativeCrash. |
| foreground | Bool | Whether the application is in the foreground. true indicates foreground status; false indicates background status. |
| bundle_version | String | Application version. |
| bundle_name | String | Application name. |
| pid | Int32 | Process ID of the application. |
| uid | Int32 | User ID of the application. |
| uuid | String | Fault ID. |
| exception | Exception | Exception information. For details, see the exception attribute. The exception only contains brief fault information; specific fault location information can be found in the external_log file. |
| hilog | Array\<String> | Log information, displaying up to 100 lines of hilog logs. More hilog logs can be obtained through the fault log file. |
| threads | Array\<Thread> | Full thread call stack. For details, see the thread attribute. Only provided for NativeCrash type crash events. |
| external_log<sup>12+</sup> | Array\<String> | Fault log file paths. Fault log files include CPPCRASH and CjERROR. Developers can use the files in these paths to complete <!-- RP1 -->[CPPCRASH Issue Analysis](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/dfx/cppcrash-guidelines.md)<!-- RP1End --> and [CJERROR Issue Analysis](./cj-cangjiecrash-guidelines.md). **To prevent directory space from exceeding the limit (refer to log_over_limit for restrictions), which may cause new log files to fail to be written, please delete log files promptly after processing.** |
| log_over_limit<sup>12+</sup> | Bool | Whether the total size of generated fault log files and existing log files exceeds the 5M limit. true indicates the limit is exceeded, and log writing fails; false indicates the limit is not exceeded. |

**exception Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | -------------------------------- |
| name | String | Exception type. |
| message | String | Exception reason. |
| stack | String | Exception call stack. |

**signal Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | -------------------------------- |
| signo | Int32 | Signal value (si_signo attribute in siginfo_t). |
| code | Int32 | Signal value secondary classification (si_code attribute in siginfo_t). |
| address | String | Signal error address (si_address attribute in siginfo_t). |

For details, refer to <!-- RP2 -->[Signal Value & Signal Value Secondary Classification Details](https://gitcode.com/openharmony/docs/blob/master/en/application-dev/dfx/cppcrash-guidelines.md)<!-- RP2End -->.

**thread Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | -------------------------------- |
| thread_name | String | Thread name. |
| tid | Int32 | Thread ID. |
| frames | Array\<Frame> | Thread call stack. For details, see the frame attribute. |

**frame Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | -------------------------------- |
| file | String | File name. |
| symbol | String | Function name. |
| column | Int32 | Column number where the exception occurred. |
| line | Int32 | Line number where the exception occurred. |