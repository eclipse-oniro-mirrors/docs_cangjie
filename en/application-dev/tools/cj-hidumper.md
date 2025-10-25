# hidumper

HiDumper provides a unified system information retrieval tool for developers and testers, assisting users in analyzing and troubleshooting issues.

## Environment Requirements

- Complete [environment preparation](./cj-hdc.md#environment-preparation) according to the hdc command-line tool guide.
- Ensure normal device connection.

## Command Line Instructions

| Option | Description |
| -------- | -------- |
| -h  | Help command. |
| -lc | List system information clusters. |
| -ls | List system capabilities. |
| -c | Retrieve detailed information of system information clusters. |
| -c [base system] | Retrieve detailed information of "base" or "system" information clusters. |
| -s | Retrieve detailed information of all system capabilities. |
| -s [SA0 SA1] | Retrieve detailed information of one or multiple system capabilities. |
| -s [SA] -a ["option"] | Execute specific options for a single system capability. SA represents the system capability name, and option denotes the supported options for that capability. Use -s [SA] -a ["-h"] to view all supported options for a single system capability. |
| -e | Retrieve fault logs of crash history. |
| --net [pid] | Retrieve network information. If a process pid is specified, only the network traffic usage of that process will be displayed. |
| --storage [pid] | Retrieve storage information. If a process pid is specified, only the I/O information of that process will be displayed. |
| -p [pid] | Retrieve process information, including lists and details of processes and threads. |
| --cpuusage [pid] | Retrieve CPU usage categorized by process and type; if a pid is specified, retrieve CPU usage information for that specific pid. |
| --cpufreq | Retrieve the actual frequency of each CPU core. |
| --mem [pid] | Retrieve total memory usage; if a pid is specified, retrieve memory usage for that specific pid. |
| --zip | Save command output to a compressed file in /data/log/hidumper. |
| --ipc pid/-a --start-stat/stop-stat/stat | Collect IPC information of processes over a period. Use -a to collect IPC data for all processes, --start-stat to begin collection, --stat to retrieve collected data, and --stop-stat to end collection. |
| --mem-smaps pid [-v] | Retrieve memory statistics for a pid, sourced from /proc/pid/smaps. Use -v for more detailed information. (Only available in debug versions) |
| --mem-jsheap pid [-T tid] [--gc] [--leakobj] | pid is a required parameter. The command triggers GC and snapshot export for all threads. If a thread tid is specified, only that thread's GC and snapshot export are triggered; if --gc is specified, only GC is triggered without snapshot export; if --leakobj is specified, a list of leaked objects is retrieved. |

## Common Commands

1. View help command.

    ```shell
    hidumper -h
    ```

    **Example Usage:**

    ```shell
    $ hidumper -h
    usage:
    -h                          |help text for the tool
    -lc                         |a list of system information clusters
    -ls                         |a list of system abilities
    -c                          |all system information clusters
    -c [base system]            |system information clusters labeled "base" and "system"
    -s                          |all system abilities
    -s [SA0 SA1]                |system abilities labeled "SA0" and "SA1"
    -s [SA] -a ['-h']           |system ability labeled "SA" with arguments "-h" specified
    -e                          |faultlogs of crash history
    --net [pid]                 |dump network information; if pid is specified, dump traffic usage of specified pid
    --storage [pid]             |dump storage information; if pid is specified, dump /proc/pid/io
    -p                          |processes information, include list and infromation of processes and threads
    -p [pid]                    |dump threads under pid, includes smap, block channel, execute time, mountinfo
    --cpufreq                   |dump real CPU frequency of each core
    --mem [pid]                 |dump memory usage of total; dump memory usage of specified pid if pid was specified
    --zip                       |compress output to /data/log/hidumper
    --mem-smaps pid [-v]        |display statistic in /proc/pid/smaps, use -v specify more details
    --mem-jsheap pid [-T tid] [--gc] [--leakobj]  |triggerGC, dumpHeapSnapshot and dumpLeakList under pid and tid
    --ipc pid ARG               |ipc load statistic; pid must be specified or set to -a dump all processes. ARG must be one of --start-stat | --stop-stat | --stat
    --cpuusage [pid]            |dump cpu usage by processes and category; if PID is specified, dump category usage of specified pid
    ```

2. List system information clusters.

    ```shell
    hidumper -lc
    ```

    **Example Usage:**

    ```shell
    $ hidumper -lc
    System cluster list:
    base                             system
    ```

3. List system capabilities.

    ```shell
    hidumper -ls
    ```

    **Example Usage:**

    ```shell
    $ hidumper -ls
    System ability list:
    SystemAbilityManager             RenderService                    AbilityManagerService
    DataObserverMgr                  AccountMgr                       AIEngine
    BundleMgr                        FormMgr                          ApplicationManagerService
    AccessibilityManagerService      UserIdmService                   UserAuthService
    AuthExecutorMgrService           PinAuthService                   FaceAuthService
    FingerprintAuthService           WifiDevice                       WifiHotspot
    WifiP2p                          WifiScan                         1125
    1126                             BluetoothHost                    NetConnManager
    NetPolicyManager                 NetStatsManager                  NetTetheringManager
    ...
    ```

4. Retrieve detailed information of system information clusters.

    ```shell
    hidumper -c
    ```

    **Example Usage:**

    ```shell
    $ hidumper -c

    -------------------------------[base]-------------------------------

    BuildId: OpenHarmony 5.0.0.37
    RleaseType: Canary1
    ...
    ```

5. Retrieve detailed information of "base" or "system" information clusters.

    ```shell
    hidumper -c base
    hidumper -c system
    ```

    **Example Usage:**

    ```shell
    $ hidumper -c base

    -------------------------------[base]-------------------------------

    BuildId: OpenHarmony 5.0.0.37
    RleaseType: Canary1
    ...

    $ hidumper -c system

    -------------------------------[system]-------------------------------


    cmd is: printenv

    _=/system/bin/printenv
    LANG=en_US.UTF-8
    HOME=/root
    PULSE_STATE_PATH=/data/data/.pulse_dir/state
    ...
    ```

6. Retrieve detailed information of all system capabilities. Command format:

    ```shell
    hidumper -s
    ```

    **Example Usage:**

    ```shell
    $ hidumper -s

    -------------------------------[ability]-------------------------------


    ----------------------------------SystemAbilityManager----------------------------------
    The arguments are illegal and you can enter '-h' for help.

    -------------------------------[ability]-------------------------------


    ----------------------------------RenderService----------------------------------
    ------Graphic2D--RenderSerice ------
    Usage:
    h                             |help text for the tool
    ...
    ```

7. Retrieve detailed information of one or multiple system capabilities. Command format:

    ```shell
    hidumper -s [SA0]
    hidumper -s [SA0] [SA1]
    ```

    **Example Usage:**

    ```shell
    $ hidumper -s 4606

    -------------------------------[ability]-------------------------------


    ----------------------------------WindowManagerService----------------------------------
    Usage:
    -h                             |help text for the tool
    -a                             |dump all window information in the system
    -w {window id} [ArkUI Option]  |dump specified window information
    ------------------------------------[ArkUI Option]------------------------------------

    $ hidumper -s 4606 10

    -------------------------------[ability]-------------------------------


    ----------------------------------WindowManagerService----------------------------------
    Usage:
    -h                             |help text for the tool
    -a                             |dump all window information in the system
    -w {window id} [ArkUI Option]  |dump specified window information
    ------------------------------------[ArkUI Option]------------------------------------


    -------------------------------[ability]-------------------------------


    ----------------------------------RenderService----------------------------------
    ------Graphic2D--RenderSerice ------
    Usage:
    h                             |help text for the tool
    screen                         |dump all screen infomation in the system
    surface                        |dump all surface information
    composer fps                   |dump the fps info of composer
    ...
    ```

8. Execute specific options for a single system capability.

    To get usage help for RenderService, use the following command:

    ```shell
    hidumper -s RenderService -a "h"
    ```

    **Example Usage:**

    ```shell
    $ hidumper -s RenderService -a "h"

    -------------------------------[ability]-------------------------------


    ----------------------------------RenderService----------------------------------
    ------Graphic2D--RenderSerice ------
    Usage:
    h                             |help text for the tool
    screen                         |dump all screen infomation in the system
    surface                        |dump all surface information
    composer fps                   |dump the fps info of composer
    [surface name] fps             |dump the fps info of surface
    composer fpsClear              |clear the fps info of composer
    [windowname] fps               |dump the fps info of window
    [windowname] hitchs            |dump the hitchs info of window
    [surface name] fpsClear        |clear the fps info of surface
    nodeNotOnTree                  |dump nodeNotOnTree info
    allSurfacesMem                 |dump surface mem info
    RSTree                         |dump RSTree info
    EventParamList                 |dump EventParamList info
    allInfo                        |dump all info
    client                         |dump client ui node trees
    client-server                  |dump client and server info
    dumpMem                        |dump Cache
    trimMem cpu/gpu/shader         |release Cache
    surfacenode [id]               |dump node info
    fpsCount                       |dump the refresh rate counts info
    clearFpsCount                  |clear the refresh rate counts info
    vktextureLimit                 |dump vk texture limit info
    flushJankStatsRs|flush rs jank stats hisysevent
    ```

    To retrieve the refresh frame rate of a specific surface, use the following command, which returns timestamps corresponding to the surface's refresh frames.

    ```shell
    hidumper -s RenderService -a "surface_name fps"
    ```

    **Example Usage:**

    ```shell
    $ hidumper -s RenderService -a "surface_name fps"

    -------------------------------[ability]-------------------------------


    ----------------------------------RenderService----------------------------------

    -- The recently fps records info of screens:
    ```

    Provides developers with the capability to prevent the device from automatically sleeping. The -t parameter prevents automatic sleep, while the -f parameter restores automatic sleep functionality or requires a device reboot to restore it.

    ```shell
    hidumper -s 3301 -a -t
    hidumper -s 3301 -a -f
    ```

    **Usage Examples:**

    ```shell
    $ hidumper -s 3301 -a -t

    -------------------------------[ability]-------------------------------


    ----------------------------------PowerManagerService----------------------------------
    $ hidumper -s 3301 -a -f

    -------------------------------[ability]-------------------------------


    ----------------------------------PowerManagerService----------------------------------
    ```

9. Retrieve crash history information generated by the Faultlog module.

    ```shell
    hidumper -e
    ```

    **Usage Example:**

    ```shell
    $ hidumper -e

    -------------------------------[faultlog]-------------------------------


    /data/log/faultlog/faultlogger/syswarning-com.ohos.sceneboard-20020022-20241106104006

    Generated by HiviewDFX@OpenHarmony
    ...
    ```

10. Obtain network information; if a process PID is specified, only the network traffic usage information for that process will be retrieved.

    ```shell
    hidumper --net pid
    hidumper --net
    ```

    **Usage Example:**

    ```shell
    $ hidumper --net 1

    -------------------------------[net traffic]-------------------------------

    Received Bytes:0
    Sent Bytes:51885

    $ hidumper --net

    -------------------------------[net traffic]-------------------------------

    Received Bytes:0
    Sent Bytes:51885

    -------------------------------[net]-------------------------------

    cmd is: netstat -nW
    ...

    ```

11. Retrieve storage information. If a process PID is specified, only the I/O information for that process will be output.

    ```shell
    hidumper --storage pid
    hidumper --storage
    ```

    **Usage Example:**

    ```shell
    $ hidumper --storage 1

    -------------------------------[storage io]-------------------------------


    /proc/1/io

    rchar: 28848175
    wchar: 4364169
    syscr: 16886
    syscw: 15866
    read_bytes: 30617600
    write_bytes: 10907648
    cancelled_write_bytes: 7340032
    $ hidumper --storage

    -------------------------------[storage]-------------------------------


    cmd is: storaged -u -p
    ...
    ```

12. Obtain process information, including lists of processes and threads.

    ```shell
    hidumper -p pid
    hidumper -p
    ```

    **Note:**

    > **Note:**
    >
    > In release versions, this command only supports exporting process information for debug applications.
    >
    > How to distinguish between debug/release versions:
    >
    > Command 1: Execute `hdc shell "param get|grep const.debuggable"` and check if the output is 0 or 1.
    >
    > Command 2: Execute `hdc shell "param get|grep const.product.software.version"` and check if the current version contains the string "log".
    >
    > Release version: Command 1 output is 0 and Command 2 does not contain the string "log".
    >
    > Debug version: Any version that is not a release version is a debug version.

    **Usage Example:**

    ```shell
    $ hidumper -p 64949

    -------------------------------[processes]-------------------------------


    cmd is: ps -efT -p 64949

    UID            PID   TID  PPID TCNT STIME TTY          TIME CMD
    20020169     64949 64949   629   17 11:40:14 ?     00:00:00 com.example.jsleakwatcher
    20020169     64949   733   629   17 11:40:28 ?     00:00:00 com.example.jsleakwatcher
    ...
    $ hidumper -p

    -------------------------------[processes]-------------------------------


    cmd is: ps -efT

    UID            PID   TID  PPID TCNT STIME TTY          TIME CMD
    root             1     1     0    1 10:46:59 ?     00:00:08 init --second-stage 2389791
    root             2     2     0  127 10:46:59 ?     00:00:24 [sysmgr-main]
    root             2     4     0  127 10:46:59 ?     00:00:00 [call_ebr]
    ...
    ```

13. Obtain CPU usage, categorized by process and type.

    ```shell
    hidumper --cpuusage pid
    hidumper --cpuusage
    ```

    **Usage Example:**

    ```shell
    $ hidumper --cpuusage 1

    -------------------------------[cpuusage]-------------------------------

    Load average: 12.1 / 12.2 / 12.1; the cpu load average in 1 min, 5 min and 15 min
    CPU usage from 2024-11-06 11:59:33 to 2024-11-06 11:59:35
    Total: 3.80%; User Space: 1.45%; Kernel Space: 2.35%; iowait: 0.00%; irq: 0.14%; idle: 96.06%
    Details of Processes:
        PID   Total Usage      User Space    Kernel Space    Page Fault Minor    Page Fault Major    Name
        1          0.00%           0.00%          0.00%           38368                1394            init
    $ hidumper --cpuusage

    -------------------------------[cpuusage]-------------------------------

    Load average: 12.1 / 12.2 / 12.1; the cpu load average in 1 min, 5 min and 15 min
    CPU usage from 2024-11-06 11:59:33 to 2024-11-06 11:59:38
    Total: 6.38%; User Space: 2.57%; Kernel Space: 3.81%; iowait: 0.02%; irq: 0.14%; idle: 93.46%
    Details of Processes:
        PID   Total Usage      User Space    Kernel Space    Page Fault Minor    Page Fault Major    Name
        105      109.01%           0.00%        109.01%             164                   0            tppmgr.elf
        2          0.89%           0.00%          0.89%               0                   0            sysmgr-main
    ...
    ```

14. Obtain the actual frequency of each CPU core.

    ```shell
    hidumper --cpufreq
    ```

    **Usage Example:**

    ```shell
    $ hidumper --cpufreq

    -------------------------------[cpufreq]-------------------------------


    cmd is: cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq

    1018000

    cmd is: cat /sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_max_freq

    1530000
    ...
    ```

15. Obtain memory information for all PIDs in the device.

    ```shell
    hidumper --mem
    ```

    **Usage Example:**

    ```shell
    $ hidumper --mem
    -------------------------------[memory]-------------------------------
    Total Memory Usage by PID:
    PID       Total Pss(xxx in SwapPss)   Total Vss   Total Rss   Total Uss          GL       Graph         Dma     PurgSum     PurgPin    Name
    1          4309(2216 in SwapPss) kB  2158196 kB     4180 kB     1760 kB        0 kB        0 kB        0 kB        0 kB        0 kB    init
    2            45613(0 in SwapPss) kB 17452952 kB    48352 kB    44088 kB        0 kB        0 kB        0 kB        0 kB        0 kB    sysmgr-main
    ...
    ```

    Obtain memory information for a specified PID.

    ```shell
    hidumper --mem pid
    ```

    **Usage Example:**

    ```shell
    $ hidumper --mem 1

    -------------------------------[memory]-------------------------------

                            Pss        Shared        Shared       Private       Private          Swap       SwapPss          Heap          Heap          Heap
                        Total         Clean         Dirty         Clean         Dirty         Total         Total          Size         Alloc          Free
                        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )        ( kB )
                --------------------------------------------------------------------------------------------------------------------------------------------
                GL             0             0             0             0             0             0             0             0             0             0
            Graph             0             0             0             0             0             0             0             0             0             0
    native heap           924             0             0           924             0          1948          1948             0             0             0
    AnonPage other            84            16             0            84             0            52            52             0             0             0
            stack            28             0             0            28             0             0             0             0             0             0
            .so           413          1548             0           248            56           216           216             0             0             0
            dev           190             0           856             0             0             0             0             0             0             0
    FilePage other           420             0             0           404            16             0             0             0             0             0
    ----------------------------------------------------------------------------------------------------------------------------------------------------------
            Total          4275          1564           856          1688            72          2216          2216             0             0             0

    native heap:
    jemalloc meta:           120             0             0           120             0            52            52             0             0             0
    jemalloc heap:           776             0             0           776             0          1888          1888             0             0             0
        brk heap:            20             0             0            20             0             8             8             0             0             0
        musl heap:             8             0             0             8             0             0             0             0             0             0

    Purgeable:
            PurgSum:0 kB
            PurgPin:0 kB

    DMA:
                Dma:0 kB
    ```

    **The Graph field is calculated as: the memory size used by the process under the `/proc/process_dmabuf_info` node.**

16. Save command output to a compressed file in `/data/log/hidumper`.

    ```shell
    hidumper --zip
    ```

    **Usage Example:**

    ```shell
    $ hidumper --zip
    100%,[-],The result is:/data/log/hidumper/20241106-120444-166.zip
    ```

17. Collect IPC information for a process over a period of time. Use `-a` to collect IPC data for all processes, or specify a PID to collect IPC data for that process. `--start-stat` begins collection, `--stat` retrieves collected data, and `--stop-stat` ends collection.

    ```shell
    hidumper --ipc pid --start-stat
    hidumper --ipc pid --stat
    hidumper --ipc pid --stop-stat
    ```

    **Usage Example:**

    ```shell
    $ hidumper --ipc 1473 --start-stat
    StartIpcStatistics pid:1473 success
    $ hidumper --ipc 1473 --stat
    ********************************GlobalStatisticsInfo********************************
    CurrentPid:1473
    TotalCount:2
    TotalTimeCost:2214
    --------------------------------ProcessStatisticsInfo-------------------------------
    CallingPid:625
    CallingPidTotalCount:2
    CallingPidTotalTimeCost:2214
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~InterfaceStatisticsInfo~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    DescriptorCode:OHOS.ILocalAbilityManager_6
    DescriptorCodeCount:2
    DescriptorCodeTimeCost:
    Total:2214 | Max:1444 | Min:770 | Avg:1107
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    ------------------------------------------------------------------------------------
    ************************************************************************************
    $ hidumper --ipc 1473 --stop-stat
    StopIpcStatistics pid:1473 success
    ```

    ```shell
    hidumper --ipc -a --start-stat
    hidumper --ipc -a --stat
    hidumper --ipc -a --stop-stat
    ```

    **Usage Example:**

    ```shell
    $ hidumper --ipc -a --start-stat
    StartIpcStatistics pid:1473 success
    StartIpcStatistics pid:775 success
    StartIpcStatistics pid:1472 success
    ...
    $ hidumper --ipc -a --stat
    ********************************GlobalStatisticsInfo********************************
    CurrentPid:1473
    TotalCount:3
    TotalTimeCost:3783
    --------------------------------ProcessStatisticsInfo-------------------------------
    CallingPid:625
    CallingPidTotalCount:3
    ...
    $ hidumper --ipc -a --stop-stat
    StopIpcStatistics pid:1473 success
    StopIpcStatistics pid:775 success
    StopIpcStatistics pid:1472 success
    ...
    ```

18. Export detailed memory usage information for specified processes.

    ```shell
    hidumper --mem-smaps pid [-v]
    ```

    > **Note:**
    >
    > This command is only available in debug builds, not in release builds.
    >
    > How to distinguish debug/release builds: Refer to the instructions in `hidumper -p`.

    **Usage Example:**

    ```shell
    $ hidumper --mem-smaps 1
    usage:
    -h                          |help text for the tool
    -lc                         |a list of system information clusters
    -ls                         |a list of system abilities
    -c                          |all system information clusters
    -c [base system]            |system information clusters labeled "base" and "system"
    -s                          |all system abilities
    -s [SA0 SA1]                |system abilities labeled "SA0" and "SA1"
    -s [SA] -a ['-h']           |system ability labeled "SA" with arguments "-h" specified
    -e                          |faultlogs of crash history
    --net [pid]                 |dump network information; if pid is specified, dump traffic usage of specified pid
    --storage [pid]             |dump storage information; if pid is specified, dump /proc/pid/io
    -p                          |processes information, include list and infromation of processes and threads
    -p [pid]                    |dump threads under pid, includes smap, block channel, execute time, mountinfo
    --cpufreq                   |dump real CPU frequency of each core
    --mem [pid]                 |dump memory usage of total; dump memory usage of specified pid if pid was specified
    --zip                       |compress output to /data/log/hidumper
    --mem-smaps pid [-v]        |display statistic in /proc/pid/smaps, use -v specify more details
    --mem-jsheap pid [-T tid] [--gc] [--leakobj]  |triggerGC, dumpHeapSnapshot and dumpLeakList under pid and tid
    --ipc pid ARG               |ipc load statistic; pid must be specified or set to -a dump all processes. ARG must be one of --start-stat | --stop-stat | --stat
    --cpuusage [pid]            |dump cpu usage by processes and category; if PID is specified, dump category usage of specified pid

    $ hidumper --mem-smaps 1 -v
    usage:
    -h                          |help text for the tool
    -lc                         |a list of system information clusters
    -ls                         |a list of system abilities
    -c                          |all system information clusters
    -c [base system]            |system information clusters labeled "base" and "system"
    -s                          |all system abilities
    -s [SA0 SA1]                |system abilities labeled "SA0" and "SA1"
    -s [SA] -a ['-h']           |system ability labeled "SA" with arguments "-h" specified
    -e                          |faultlogs of crash history
    --net [pid]                 |dump network information; if pid is specified, dump traffic usage of specified pid
    --storage [pid]             |dump storage information; if pid is specified, dump /proc/pid/io
    -p                          |processes information, include list and infromation of processes and threads
    -p [pid]                    |dump threads under pid, includes smap, block channel, execute time, mountinfo
    --cpufreq                   |dump real CPU frequency of each core
    --mem [pid]                 |dump memory usage of total; dump memory usage of specified pid if pid was specified
    --zip                       |compress output to /data/log/hidumper
    --mem-smaps pid [-v]        |display statistic in /proc/pid/smaps, use -v specify more details
    --mem-jsheap pid [-T tid] [--gc] [--leakobj]  |triggerGC, dumpHeapSnapshot and dumpLeakList under pid and tid
    --ipc pid ARG               |ipc load statistic; pid must be specified or set to -a dump all processes. ARG must be one of --start-stat | --stop-stat | --stat
    --cpuusage [pid]            |dump cpu usage by processes and category; if PID is specified, dump category usage of specified pid
    ```

19. Execute **hidumper --mem-jsheap pid [-T tid] [--gc] [--leakobj]** where pid is a mandatory parameter. This command triggers GC and snapshot exports for all threads. If a thread's tid is specified, only triggers GC and snapshot export for that thread; if --gc is specified, only triggers GC without snapshot export; if --leakobj is specified, retrieves the list of leaked objects. (Only available in debug builds)

    ```shell
    hidumper --mem-jsheap pid [-T tid] [--gc] [--leakobj]
    ```

    > **Note:**
    >
    > In release builds, this command only supports exporting snapshot information for debug applications.
    >
    > How to distinguish debug and release builds: Refer to the instructions in `hidumper -p`.
    >
    > The exported jsheap files are typically located in /data/log/faultlog/temp or /data/log/reliability/resource_leak/memory_leak.

    **Usage Example:**

    ```shell
    $ hidumper --mem-jsheap 64949
    $ ls |grep hidumper
    hidumper-jsheap-64949-64949-1730872962493
    $ hidumper --mem-jsheap 64949 -T 64949
    $ ls |grep hidumper
    hidumper-jsheap-64949-64949-1730872962493
    $ hidumper --mem-jsheap 64949 --gc
    $ hidumper --mem-jsheap 64949 --leakobj
    $ ls |grep hidumper
    hidumper-jsheap-64949-64949-1730873174145
    hidumper-leaklist-64949-1730873210483
    ```
