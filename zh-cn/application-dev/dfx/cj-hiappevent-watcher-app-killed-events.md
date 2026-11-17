# 应用终止事件介绍

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

应用闪退指应用在使用过程中突然异常终止。当应用行为异常，比如消耗过多CPU、内存等系统资源时，系统为了保持整机健康状态，会按照规则挑选应用进行管控，通常通过服务进程向应用发送SIGKILL信号（信号值是9）来实施终止的。操作系统对SIGKILL的默认行为是不生成栈日志等维测信息的，导致应用闪退时faultlogger中无日志。

HiAppEvent提供接口用于订阅应用终止事件。

[订阅应用终止事件](./cj-hiappevent-watcher-app-killed-events-cangjie.md)

应用终止事件信息中params属性的详细描述如下：

**params属性：**

| 名称    | 类型   | 说明                       |
| ------- | ------ | ------------------------- |
| time     | Float64 | 事件触发时间，单位为毫秒。 |
| reason  | String | 终止原因，原因范围详见**reason属性**。 |
| foreground | Bool | 应用是否处于前台状态。true表示应用处于前台；false表示应用处于后台。|
| app_running_unique_id | String | 应用运行时唯一关联的id。从API version 24开始支持该参数。 |
| bundle_version | String | 应用版本信息。从API version 24开始支持该参数。 |
| last_exit_detail_info | String | 应用退出前的详细信息，详见**last_exit_detail_info属性**。从API version 26.0.0开始支持该参数。 |

**reason属性：**

| 类型                            | 说明                              |
| ----------------------------- | ------------------------------- |
| LowMemoryKill                 | 整机低内存触发，优先级由低到高终止应用。        |
| SwapFull                      | Swap交换空间接近占满。                    |
| ResourceLeak(IonLeak)         | 应用占用的Ion内存超标。                   |
| ResourceLeak(GpuRsLeak)       | 应用的ArkUI组件在Render Service进程占用的GPU内存超标。 |
| ResourceLeak(GpuLeak)         | 应用在本进程占用的GPU内存超标。                    |
| ResourceLeak(AshmemLeak)      | 应用占用的Ashmem内存超标。                 |
| ResourceLeak(CES)             | CES注册超限。                        |
| ResourceLeak(PSSSoftLeak)     | 后台应用内存占用超过检测阈值两倍，其中pss内存占比最高。   |
| ResourceLeak(PSSLeak)         | 后台应用内存占用超过特定阈值，其中pss内存占比最高。     |
| ResourceLeak(VMALeak)         | VMA泄漏。                          |
| ResourceLeak(FDLeak)          | FD泄漏。                           |
| ResourceLeak(ThreadLeak)      | 线程泄漏。                          |
| ResourceLeak(KernelZoneLeak)  | 页表内存泄漏。                  |
| IllegalAudioRendererBySuspend | 应用的音频播放未申请合理的后台任务，其退至后台后仍有大量音频播放。       |
| PowerSaveClean                | 整机切换到省电模式或应急模式。                 |
| VrsKill                       | 三方应用检测到恶意进程后，调用PC端病毒检测处置服务接口终止进程。                |
| RssThresholdKiller            | 应用的RSS（Resident Set Size）占用超标。  |
| OomKiller                     | 整机低内存，触发内核管控，按一定策略终止应用。                  |
| CpaKiller                     | DRM（Digital Rights Management）业务申请内存但是内存不足时，按一定策略终止进程以回收内存。        |
| KillApplication               | 应用主动退出。                         |
| OnRemoteDied                  | 远程服务死亡。                          |
| Restart                       | 应用重启。                           |
| UserRequest                   | 最近任务上划或清理。                      |
| Uninstall                     | 应用卸载退出。                         |
| Upgrade                       | 应用更新退出。                         |
| Logout                        | 用户注销时，卸载应用沙箱。                   |
| PermissionUpdate              | 应用权限更新。                        |
| aaForceStop                   | 通过aa命令强制停止应用。                    |
| ThreadBlock6S                 | 应用主线程卡死超时。                       |
| AppInputBlock                 | 用户输入响应超时。                        |
| LifecycleTimeout              | 应用生命周期超时。                       |
| JsError                       | js层程序崩溃。                       |
| CppCrash                      | native层程序崩溃。                    |
| RSPixelMapFdOverLimit         | 应用使用图片PixelMap资源超限导致渲染服务fd泄漏。        |
| CPUHighloadNotify             | 应用后台CPU高负载，出现弹框，用户选择停止该应用。        |
| CPUHighloadUserRequest        | 应用后台CPU高负载，设置界面用户选择停止该应用。        |
| IllegalAudioCapturerBySuspend | 应用录音未申请合理的后台任务，其退至后台后仍进行录音。        |
| IOHighload                    | IO高负载。                          |
| AppFreeze                     | 应用冻屏无响应。                        |
| MaliciousContinuousTaskActive | 恶意连续任务活跃。                        |
| RsDataOverflow                | RS数据溢出。                        |
| HighTemperature               | 温度超限。                           |
| TransientTaskTimeout          | 短时任务超时6s并且处于后台。                 |
| TooManyReadyThreads           | 就绪线程过多。                          |
| JsHeapSleepCleanKill          | sleep状态（夜间充电）进行js heapsize检测，超限后终止应用。              |
| HardwareDecodingResourcesLimit | 硬件解码资源限制。                        |
| AppRecoveryNotifyAppOverLimit | 应用恢复通知应用超限。                        |
| GpuError                      | GPU错误。                           |
| NotAttachedToStatusBar        | 未附加到状态栏。                         |
| CPUHighload                   | 应用后台CPU高负载，系统自动终止应用。              |
| AshmemKiller                  | 整机低内存，单进程ASHMEM内存超限。                       |
| GpuKiller                     | 整机低内存，单进程GPU占用达到阈值。                      |
| DmaKiller                     | 整机低内存，单进程Dma占用达到阈值。                      |
| ThreadKiller                  | 单进程线程超限。                      |
| UninstallStorage              | 卸载存储卡。                        |

**last_exit_detail_info属性：**

| 名称    | 类型   | 说明                       |
| ------- | ------ | ------------------------- |
| exit_msg | String | 应用退出信息。 |
| kill_reason | String | 应用退出理由。 |
| pid | String | 应用的进程ID。 |
| process_name | String | 应用的进程名称。 |
| process_state | String | 应用的进程状态。 |
| pss | String | 进程实际使用的物理内存大小，单位KB。 |
| rss | String | 进程实际占用内存大小，单位为KB。 |
| timestamp | String | 故障发生时间戳。 |
| uid | String | 应用的用户ID。 |
