# Introduction to AppKilled Events

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

An application flash exit refers to the unexpected exit of an application during use. When an application behaves abnormally, for example, consuming excessive system resources such as CPU and memory, the system manages the application based on rules to maintain its health status. Typically, the system kills the application by sending the SIGKILL signal (the signal value is 9) to the application through the service process. By default, the OS does not generate maintenance and debugging information such as stack logs for the SIGKILL behavior. As a result, no log is generated in the faultlogger when the application exits.

HiAppEvent provides interfaces for subscribing to application killed events.

[Subscribing to AppKilled Events (Cangjie)](./cj-hiappevent-watcher-app-killed-events-cangjie.md)

The detailed description of the `params` attribute in the application killed event is as follows:

**params Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| time     | Float64 | Event trigger time, in milliseconds. |
| reason  | String | Termination reason. For the value range, see the **reason attribute**. |
| foreground | Bool | Whether the application is in the foreground. `true` indicates that the application is in the foreground; `false` indicates that the application is in the background.|
| app_running_unique_id | String | Unique ID associated with the application at runtime. This parameter is supported since API version 24. |
| bundle_version | String | Application version information. This parameter is supported since API version 24. |
| last_exit_detail_info | String | Detailed information before the app exits. For details, see the **last_exit_detail_info attribute**. This parameter is supported since API version 26.0.0. |

**reason Attribute:**

| Type                            | Description                              |
| ----------------------------- | ------------------------------- |
| LowMemoryKill                 | The system is low on memory, triggering process termination in ascending order of priority.        |
| SwapFull                      | The swap space is almost used up.                    |
| ResourceLeak(IonLeak)         | The Ion memory used by the application exceeds the threshold.                   |
| ResourceLeak(GpuRsLeak)       | The GPU memory used by the ArkUI component of the application in the Render Service process exceeds the threshold. |
| ResourceLeak(GpuLeak)         | The GPU memory used by the application in its own process exceeds the threshold.                    |
| ResourceLeak(AshmemLeak)      | The Ashmem memory used by the application exceeds the threshold.                 |
| ResourceLeak(CES)             | The CES registration exceeds the threshold.                        |
| ResourceLeak(PSSSoftLeak)     | The memory usage of the background application exceeds twice the detection threshold, and the PSS memory accounts for the highest proportion.   |
| ResourceLeak(PSSLeak)         | The memory usage of the background application exceeds the specified threshold, and the PSS memory accounts for the highest proportion.     |
| ResourceLeak(VMALeak)         | VMA leak.                          |
| ResourceLeak(FDLeak)          | FD leak.                           |
| ResourceLeak(ThreadLeak)      | Thread leak.                          |
| ResourceLeak(KernelZoneLeak)  | Page table memory leak.                  |
| IllegalAudioRendererBySuspend | No proper background task is applied for the application, but a large amount of audio is played after the application is switched to the background.       |
| PowerSaveClean                | The device is switched to the power saving mode or emergency mode.                 |
| VrsKill                       | After a third-party application detects a malicious process, it calls the PC virus detection and disposal service interface to terminate the process.                |
| RssThresholdKiller            | The RSS (Resident Set Size) usage of the application exceeds the threshold.  |
| OomKiller                     | The system is low on memory, triggering kernel management and application termination based on specific policies.                  |
| CpaKiller                     | When the DRM (Digital Rights Management) service applies for memory but the memory is insufficient, the system terminates processes based on specific policies to reclaim memory.        |
| KillApplication               | The application exits on its own initiative.                         |
| OnRemoteDied                  | The remote service is dead.                          |
| Restart                       | The application restarts.                           |
| UserRequest                   | The application is swiped up or cleared in recent tasks.                      |
| Uninstall                     | The application exits due to uninstallation.                         |
| Upgrade                       | The application exits due to update.                         |
| Logout                        | The application sandbox is uninstalled when the user logs out.                   |
| PermissionUpdate              | The application permission is updated.                        |
| aaForceStop                   | The application is forcibly stopped by the aa command.                    |
| ThreadBlock6S                 | The application main thread is frozen (timeout).                       |
| AppInputBlock                 | User input response timeout.                        |
| LifecycleTimeout              | Application lifecycle timeout.                       |
| JsError                       | Crash at the js layer.                       |
| CppCrash                      | Crash at the native layer.                    |
| RSPixelMapFdOverLimit         | The PixelMap resources used by the application exceed the threshold, causing fd leaks in the render service.        |
| CPUHighloadNotify             | The CPU load of the background application is high, a dialog box is displayed, and the user chooses to stop the application.        |
| CPUHighloadUserRequest        | The CPU load of the background application is high, and the user chooses to stop the application in the settings screen.        |
| IllegalAudioCapturerBySuspend | No proper background task is applied for the application, but recording continues after the application is switched to the background.        |
| IOHighload                    | High I/O load.                          |
| AppFreeze                     | The application is frozen and not responding.                        |
| MaliciousContinuousTaskActive | Malicious continuous task is active.                        |
| RsDataOverflow                | RS data overflow.                        |
| HighTemperature               | The temperature exceeds the threshold.                           |
| TransientTaskTimeout          | The short-term task times out (6s) and is in the background.                 |
| TooManyReadyThreads           | Too many ready threads in a single process.                          |
| JsHeapSleepCleanKill          | In sleep state (charging at night), the js heap size is detected, and the application is terminated when the threshold is exceeded.              |
| HardwareDecodingResourcesLimit | Hardware decoding resource limit.                        |
| AppRecoveryNotifyAppOverLimit | The application recovery notification exceeds the application limit.                        |
| GpuError                      | GPU error.                           |
| NotAttachedToStatusBar        | Not attached to the status bar.                         |
| CPUHighload                   | The CPU load of the background application is high, and the system automatically terminates the application.              |
| AshmemKiller                  | The system is low on memory, and the ASHMEM memory of a single process exceeds the limit.                       |
| GpuKiller                     | The system is low on memory, and the GPU usage of a single process reaches the threshold.                      |
| DmaKiller                     | The system is low on memory, and the Dma usage of a single process reaches the threshold.                      |
| ThreadKiller                  | The thread count of a single process exceeds the limit.                      |
| UninstallStorage              | The memory card is uninstalled.                        |

**last_exit_detail_info Attribute:**

| Name    | Type   | Description                       |
| ------- | ------ | ------------------------- |
| exit_msg | String | App exit information. |
| kill_reason | String | Reason for the app exit. |
| pid | String | App process ID. |
| process_name | String | App process name. |
| process_state | String | App process state. |
| pss | String | Physical memory actually used by the process, in KB. |
| rss | String | Memory actually occupied by the process, in KB. |
| timestamp | String | Timestamp when the fault occurred. |
| uid | String | App user ID. |
