# Analyzing AppKilled (Application Termination)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

An application flash exit refers to the unexpected exit of an application during use. When an application behaves abnormally, for example, consuming excessive system resources such as CPU and memory, the system manages the application based on rules to maintain its health status. Typically, the system kills the application by sending the SIGKILL signal (the signal value is 9) to the application through the service process. By default, the OS does not generate maintenance and debugging information such as stack logs for the SIGKILL behavior. As a result, no log is generated in the faultlogger when the application exits.

## Basic Concepts

An application exits in the following scenarios:

1. When an application is abnormal or throws an exception, for example, the crash exception triggered by SIGSEGV or SIGABRT, the system monitors the exception and records maintenance and debugging logs. For the analysis method, see [Analyzing Cangjie Crash (Process Crash)](./cj-cangjiecrash-guidelines.md).

2. When a user manually terminates an application, for example, by clicking the clear button in the task list to clear all applications or swiping up to clear an application, no stack or other maintenance and debugging logs are generated.

3. When the exit system call is invoked by the application developer, no stack or other maintenance and debugging logs are generated.

4. When the application main thread is blocked, the UI freezes and the appfreeze log is generally generated. For the analysis method, see [Analyzing AppFreeze (Application Not Responding)](./cj-appfreeze-guidelines.md).

5. When resources are overused, the system manages the application and provides detailed maintenance and debugging information. For example, when memory leaks occur in an application, resource leak maintenance and debugging logs are generally generated. You can subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain the corresponding events and logs.

6. When the system manages the application, it cannot provide detailed maintenance and debugging information in some scenarios, such as LowMemoryKiller, RSS of the application exceeding 4 GB, and fast leaks.

This topic describes the application termination caused by the SIGKILL signal in scenarios 5 and 6.

## Implementation Principles

1. Both the kernel and service processes monitor system resources.

2. When an exception is detected, the system selects and manages the application.

3. The system adds system event logging when triggering application termination.

4. The logging information includes the UID, bundle name, foreground and background information, termination reason, and maintenance and debugging information.

## Constraints

1. The application needs to subscribe to the termination event through HiAppEvent before receiving it.

2. Termination events are sent to the application asynchronously. The application receives the events upon the next startup.

3. The system management behavior is continuously added as versions evolve. Therefore, the current management mechanism may not be complete.

## Triggering Scenarios

The system terminates an application in the following scenarios:

1. The memory, CPU, and I/O load of the application exceeds the specified limit, and the number of file handles and threads exceeds the threshold.

2. When the device memory is low, the system terminates applications based on the memory usage and priority.

3. Power-consuming scenarios include frequent wake-ups caused by Binder calls, system freezes during audio playback or recording, and abnormal use of peripherals such as GPS or Bluetooth.

## Detection Methods

Applications can detect abnormal termination in either of the following ways:

1. Obtain the termination reason from the onCreate callback parameter of the ability. Specifically, set the lastExitReason field in LaunchParam. For details, see [LastExitReason](../reference/AbilityKit/cj-apis-app-ability-ability_constant.md#enum-lastexitreason).

2. Subscribe to the APP_KILLED event through HiAppEvent. For details, see [Introduction to AppKilled Events](./cj-hiappevent-watcher-app-killed-events.md).

> **Note:**
>
> The [LastExitReason](../reference/AbilityKit/cj-apis-app-ability-ability_constant.md#enum-lastexitreason) enum on the Cangjie side currently exposes only four values: `Unknown`, `Normal`, `CppCrash`, and `AppFreeze`, and the `lastExitMessage` field is not open in LaunchParam yet. When resource management control causes the application termination, `launchParam.lastExitReason` returns `Unknown`, and the specific control cause cannot be directly distinguished. Therefore, you are advised to use method 2 (subscribing to the APP_KILLED event through HiAppEvent) as the main method to detect and analyze application termination.

## Analysis Method and Procedure

1. Obtain the termination reason from the onCreate callback parameter of the ability.

    The values in the following table follow the system-side definitions (corresponding to the ArkTS enum naming): APP_FREEZE corresponds to `AppFreeze` on the Cangjie side; values such as RESOURCE_CONTROL are not open on the Cangjie side, and `lastExitReason` returns `Unknown`. Based on the preceding notes, subscribe to the APP_KILLED event using method 2 and distinguish the specific control cause based on the reason field in the event.

    | lastExitReason(enum) | lastExitMessage(string)  | Causes                                            | Handling Policy                                                    |
    | -------------------- | ------------------------ | ---------------------------------------------------- | ------------------------------------------------------------ |
    | APP_FREEZE           | APP_FREEZE               | The application exits because watchdog detects that the application is frozen.| Subscribe to the APP_FREEZE event through HiAppEvent and match its fault types. |
    | RESOURCE_CONTROL     | CPU Highload             | The CPU load is high.                                         | Reduce the CPU load of the application.                                 |
    | RESOURCE_CONTROL     | CPU_EXT Highload         | Fast CPU load detection.                                   | Reduce the CPU load of the application.                                 |
    | RESOURCE_CONTROL     | IO Manager Control       | I/O manager control.                                           | Reduce the I/O of the application.                                     |
    | RESOURCE_CONTROL     | App Memory Deterioration | The application memory usage exceeds the threshold.                                  | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more logs.      |
    | RESOURCE_CONTROL     | Temperature Control      | Temperature control.                                          | Reduce the CPU load of the application.                                 |
    | RESOURCE_CONTROL     | Memory Pressure          | The system is low on memory, triggering process termination in ascending order of priority.                | Reduce the memory usage of the application.|

2. Subscribe to the APP_KILLED event through HiAppEvent.

    Based on the APP_KILLED event, you can obtain key information such as the termination reason and application foreground and background status. Perform operations based on the following table:

    | reason(string)                | Causes                                                    | Handling Policy                                                    | Whether Control Is Triggered by Application Exceptions| Whether There Are Associated Events|
    | ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------ | -------------- |
    | LowMemoryKill                 | Same as the scenario where lastExitMessage is Memory Pressure, that is, the system is low on memory, triggering process termination in ascending order of priority.| Reduce the memory usage of the application. | No                      | No            |
    | SwapFull                      | The swap space is almost used up, which may be caused by memory leaks of some processes or too many background processes.| Reduce the memory usage of the application.| No                      | No            |
    | ResourceLeak(IonLeak)         | The ION memory used by the application exceeds the threshold.                                     | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more ION memory logs. After finding the leak point, reduce the ION memory usage of the application. Generally, the leak is caused by the Image component or Pixmap.| Yes                      | Yes            |
    | ResourceLeak(GpuRsLeak)       | The GPU memory used by the ArkUI component of the application in the render_service process exceeds the threshold.  | Reduce the GPU memory usage of the ArkUI component of the application.                        | Yes                      | No            |
    | ResourceLeak(GpuLeak)         | The GPU memory used by the application in the process (that is, the GPU memory generated by self-rendering) exceeds the threshold.  | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more GPU memory logs, find the leak point, and reduce the GPU memory usage of the application self-rendering (using the XComponent component).| Yes                      | Yes            |
    | ResourceLeak(AshmemLeak)      | The ashmem memory used by the application exceeds the threshold.                                  | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more ashmem memory logs. After finding the leak point, reduce the ashmem memory usage of the application. Generally, the leak is caused by the Image component or Pixmap.| Yes                      | Yes            |
    | ResourceLeak(CES)             | The CES registration exceeds the threshold.                              | Reduce the number of CES registrations of the application. | Yes                      | No            |
    | ResourceLeak(PSSSoftLeak)     | The memory usage of the background application exceeds twice the detection threshold, and the PSS memory accounts for the highest proportion.   | Reduce the memory usage of the application.  | Yes                      | Yes            |
    | ResourceLeak(PSSLeak)         | The memory usage of the background application exceeds the specified threshold, and the PSS memory accounts for the highest proportion.     | Reduce the memory usage of the application.  | Yes                      | Yes            |
    | ResourceLeak(VMALeak)         | VMA leak.                          | Reduce the VMA memory usage of the application, and release the corresponding virtual memory area after each call. | No                      | No            |
    | ResourceLeak(FDLeak)          | FD leak.                           | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more FD leak logs. After finding the leak point, close unnecessary file handles in a timely manner. | Yes                      | Yes            |
    | ResourceLeak(ThreadLeak)      | Thread leak.                          | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more thread leak logs. After finding the leak point, destroy unnecessary threads in a timely manner. | Yes                      | Yes            |
    | ResourceLeak(KernelZoneLeak)  | Page table memory leak.                  | No operation is required. | Yes                      | No            |
    | IllegalAudioRendererBySuspend | No proper background task is applied for the application, but a large amount of audio is played in the background.              | When the application is switched to the background, unnecessary background audio playback should be avoided, or the background task should be properly used. | Yes                      | No            |
    | PowerSaveClean                | The device is switched to the power saving mode or emergency mode.                              | No operation is required.                                                  | No                      | No            |
    | VrsKill                       | After a third-party application detects a malicious process, it calls the PC virus detection and disposal service interface to terminate the process.                             | No operation is required.                                                                                                  | No                      | No            |
    | RssThresholdKiller            | The RSS memory of the application exceeds a certain threshold.                                   | Subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more RSS memory logs. After finding the leak point, reduce the memory usage of the application to avoid the RSS memory exceeding the threshold. | Yes                      | Yes            |
    | OomKiller                     | The system is low on memory, triggering kernel management and application termination based on specific policies.                                     | Reduce the memory usage of the application. | No                      | No            |
    | CpaKiller                     | When the Digital Rights Management (DRM) service applies for memory but the memory is insufficient, the system terminates processes based on specific policies to reclaim memory. | Reduce the memory usage of the application. | No                      | No            |
    | KillApplication               | The application exits on its own initiative.                         | No operation is required.                                                  | No                      | No            |
    | OnRemoteDied                  | The remote service is dead.                          | Check whether the remote services the application depends on are normal. | No                      | No            |
    | Restart                       | The application restarts.                           | No operation is required.                                                  | No                      | No            |
    | UserRequest                   | The application is swiped up or cleared in recent tasks.                      | No operation is required.                                                  | No                      | No            |
    | Uninstall                     | The application exits due to uninstallation.                         | No operation is required.                                                  | No                      | No            |
    | Upgrade                       | The application exits due to update.                         | No operation is required.                                                  | No                      | No            |
    | Logout                        | The application sandbox is uninstalled when the user logs out.                   | No operation is required.                                                  | No                      | No            |
    | PermissionUpdate              | The application permission is updated.                        | Check whether the application permissions are used properly. | No                      | No            |
    | aaForceStop                   | The application is forcibly stopped by the aa command.                    | No operation is required.                                                  | No                      | No            |
    | ThreadBlock6S                 | The application main thread is frozen (timeout).                       | Check whether the application main thread has blocking operations, and optimize the code logic. | Yes                      | Yes. For details, see [THREAD_BLOCK_6S](./cj-appfreeze-guidelines.md#thread_block_6s-应用主线程执行停滞超时).        |
    | AppInputBlock                 | User input response timeout.                        | Check whether the application UI responds in a timely manner, and optimize the input processing logic. | Yes                      | Yes. For details, see [APP_INPUT_BLOCK](./cj-appfreeze-guidelines.md#app_input_block-用户输入响应超时).        |
    | LifecycleTimeout              | Application lifecycle timeout.                       | Check whether the application lifecycle callbacks contain time-consuming operations. | Yes                      | No            |
    | JsError                       | Crash at the js layer.                       | Check whether the js code has exceptions, and optimize error handling. | Yes                      | Yes.        |
    | CppCrash                      | Crash at the native layer.                    | Check whether the native code has exceptions, and optimize error handling. | Yes                      | Yes. For details, see [Analyzing Cangjie Crash (Process Crash)](./cj-cangjiecrash-guidelines.md).        |
    | RSPixelMapFdOverLimit         | The PixelMap resources used by the application exceed the threshold, causing fd leaks in the render service.        | Reduce the frequency of using PixelMap image resources. | Yes                      | No            |
    | CPUHighloadNotify             | The CPU load of the background application is high, a dialog box is displayed, and the user chooses to stop the application.        | Reduce the CPU load of the application. | No                      | No            |
    | CPUHighloadUserRequest        | The CPU load of the background application is high, and the user chooses to stop the application in the settings screen.        | Reduce the CPU load of the application. | No                      | No            |
    | IllegalAudioCapturerBySuspend  | No proper background task is applied for the application, but recording continues after the application is switched to the background. | When the application is switched to the background, unnecessary background recording should be avoided, or the background task should be properly used. | Yes                      | No            |
    | IOHighload                    | High I/O load.                          | Reduce the I/O operations of the application. | No                      | No            |
    | AppFreeze                     | The application is frozen and not responding.                        | Subscribe to the APP_FREEZE event through HiAppEvent and match its fault types. | Yes                      | Yes. For details, see [Analyzing AppFreeze (Application Not Responding)](./cj-appfreeze-guidelines.md).        |
    | MaliciousContinuousTaskActive | Malicious continuous task is active.                        | Check whether the application has malicious continuous tasks, and optimize task scheduling. | Yes                      | No            |
    | RsDataOverflow                | RS data overflow.                        | Reduce the RS data usage of the application. | No                      | No            |
    | HighTemperature               | The temperature exceeds the threshold.                           | Reduce the CPU load of the application to reduce heat generation. | No                      | No            |
    | TransientTaskTimeout          | The short-term task times out (6s) and is in the background.                 | Check whether short-term tasks have time-consuming operations, and optimize task execution efficiency. | Yes                      | No            |
    | TooManyReadyThreads           | Too many ready threads in a single process.                          | Reduce the number of threads created by the application, and optimize thread management. | Yes                      | No            |
    | JsHeapSleepCleanKill          | In sleep state (charging at night), the js heap size is detected, and the application is terminated when the threshold is exceeded.              | Classified as system background memory cleanup. Optimize the js heap usage. | No                      | No            |
    | HardwareDecodingResourcesLimit | Hardware decoding resource limit.                        | Reduce the usage of hardware decoding resources by the application. | No                      | No            |
    | AppRecoveryNotifyAppOverLimit | The application recovery notification exceeds the application limit.                        | Check whether the application recovery mechanism is abnormal, and optimize the recovery logic. | Yes                      | No            |
    | GpuError                      | GPU error.                           | Check whether the application uses the GPU properly, and optimize GPU resource management. | Yes                      | No            |
    | NotAttachedToStatusBar        | Not attached to the status bar.                         | Check whether the status bar attachment logic of the application is correct. | Yes                      | No            |
    | CPUHighload                   | The CPU load of the background application is high, and the system automatically terminates the application.              | Reduce the CPU load of the application. | No                      | No            |
    | AshmemKiller                  | The system is low on memory, and the ASHMEM memory of a single process exceeds the limit.                       | Reduce the ashmem memory usage of the application, and subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more ashmem memory overlimit logs. | Yes                      | Yes            |
    | GpuKiller                     | The system is low on memory, and the GPU usage of a single process reaches the threshold.                      | Reduce the GPU memory usage of the application, and subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more logs about the GPU usage of a single process reaching the threshold. | Yes                      | Yes            |
    | DmaKiller                     | The system is low on memory, and the Dma usage of a single process reaches the threshold.                      | Reduce the Dma memory usage of the application, and subscribe to RESOURCE_OVERLIMIT through HiAppEvent to obtain more logs about the Dma usage of a single process reaching the threshold. | Yes                      | Yes            |
    | ThreadKiller                  | The thread count of a single process exceeds the limit.                      | Reduce the number of threads created by the application, and optimize thread management. | Yes                      | Yes            |
    | UninstallStorage              | The memory card is uninstalled.                        | No operation is required. | No                      | No            |
