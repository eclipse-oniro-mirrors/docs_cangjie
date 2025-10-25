# Introduction to appfreeze Events

HiAppEvent provides interfaces for subscribing to system appfreeze events.

[Subscribe to appfreeze events (Cangjie)](./cj-hiappevent-watcher-freeze-events-cangjie.md)

The detailed description of the params attribute in appfreeze event information is as follows:

**params Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| time     | Int32 | Event trigger time in milliseconds. |
| foreground | Bool | Whether the application is in the foreground. true indicates the application is in the foreground; false indicates it is in the background. |
| bundle_version | String | Application version. |
| bundle_name | String | Application name. |
| process_name | String | Process name of the application. |
| pid | Int32 | Process ID of the application. |
| uid | Int32 | User ID of the application. |
| uuid | String | Fault ID. |
| exception | Exception | Exception information. For details, see the exception attribute. |
| hilog | Array\<String> | Log information. |
| event_handler | Array\<String> | Unprocessed messages in the main thread. |
| event_handler_size_3s | String | Number of tasks in the task stack at 3s for the [THREAD_BLOCK_6S event](./cj-appfreeze-guidelines.md#thread_block_6s---main-thread-execution-timeout) (only applicable to this event). |
| event_handler_size_6s | String | Number of tasks in the task stack at 6s for the [THREAD_BLOCK_6S event](./cj-appfreeze-guidelines.md#thread_block_6s---main-thread-execution-timeout) (only applicable to this event). |
| peer_binder | Array\<String> | Binder call information. |
| threads | Array\<Thread> | Full thread call stack. For details, see the thread attribute. |
| memory | Memory | Memory information. For details, see the memory attribute. |
| external_log<sup>12+</sup> | Array\<String> | Path to the fault log file. **To prevent directory space limits (refer to log_over_limit) from causing new log files to fail to be written, delete log files promptly after processing.** |
| log_over_limit<sup>12+</sup> | Bool | Whether the total size of generated fault log files and existing log files exceeds the 5M limit. true indicates the limit is exceeded, and log writing fails; false indicates the limit is not exceeded. |

**exception Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| name | String | Exception type. |
| message | String | Exception reason. |

**thread Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| thread_name | String | Thread name. |
| tid | Int32 | Thread ID. |
| frames | Array\<Frame> | Thread call stack. For details, see the frame attribute. |

**frame Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| symbol | String | Function name. |
| file | String | File name. |
| buildId | String | Unique file identifier. |
| pc | String | PC register address. |
| offset | Int32 | Function offset. |

**memory Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| rss | Int32 | Actual memory usage of the process in KB. |
| vss | Int32 | Virtual memory size requested by the process from the system in KB. |
| pss | Int32 | Actual physical memory usage of the process in KB. |
| sys_free_mem | Int32 | Free memory size in KB. |
| sys_avail_mem | Int32 | Available memory size in KB. |
| sys_total_mem | Int32 | Total memory size in KB. |