# hitrace  

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

HiTrace provides developers with debugging interfaces for tracking business process call chains. By utilizing the functionalities offered by these interfaces, developers can quickly obtain runtime logs of specified business process call chains, facilitating the identification of cross-device, cross-process, and cross-thread fault issues.  

## Environment Requirements  

- Complete the [environment setup](./cj-hdc.md#环境准备) as per the hdc command-line tool guide.  
- Ensure the device is properly connected.  

## Command Line Instructions  

| Command | Description |  
| -------- | -------- |  
| -h  | Help command. |  
| -l | View the list of tags. |  
| --trace_begin | Start capturing trace. |  
| --trace_finish | Stop capturing trace. |  
| --trace_dump | Export trace information. |  
| -b N | Set the buffer size (in KB) for storing and reading trace data. Default buffer size is 2048 KB. |  
| -t N | Set the duration for hitrace execution in seconds (default is 5 seconds), depending on the analysis time required. |  
| -o | Specify the output filename (default is stdout). |  
| -z | Compress the captured trace. |  
| --trace_clock | Set the clock type for timestamping trace data. Options: boot (default), global, mono, uptime, or perf. |  
| --trace_finish_nodump | Stop capturing trace without printing trace information. |  
| --start_bgsrv | Start the snapshot-mode trace collection service. |  
| --dump_bgsrv | Trigger snapshot-mode trace output to a file. |  
| --stop_bgsrv | Stop the snapshot-mode trace collection service. |  

> **Note:**  
>  
> Snapshot mode refers to a trace collection service with fixed trace tags. By default, traces are not saved to disk. Developers can use the `--dump_bgsrv` command to trigger trace dumping at the current moment. The trace is in binary format and is saved by default in the `/data/log/hitrace` directory. The filename follows the format `trace-YYMMDDHHmmSS@[BOOT_TIME].sys`. For visual trace analysis, use the [Smartperf_Host](https://gitcode.com/openharmony/developtools_smartperf_host) tool. Download link: [developtools_smartperf_host Release](https://gitcode.com/openharmony/developtools_smartperf_host/releases).  

## Common Commands  

Execute the following commands in hdc shell:  

1. View the tags included in hitrace.  

   ```shell  
   hitrace -l  
   ```  

   **Example:**  

   ```shell  
   $ hitrace -l  
   2024/11/14 11:43:00 hitrace enter, running_state is SHOW_LIST_CATEGORY  
         tagName:   description:  
            ability - Ability Manager  
      accesscontrol - Access Control Module  
            account - Account Manager  
               ace - ACE development framework  
         animation - Animation  
               app - APP Module  
               ark - ARK Module  
         bluetooth - Communication Bluetooth  
            cloud - Cloud subsystem tag  
         cloudfile - Cloud file system  
         commercial - Commercial version tag  
      commonlibrary - Commonlibrary subsystem  
            daudio - Distributed Audio  
            dcamera - Distributed Camera  
         deviceauth - Device Auth  
      devicemanager - Device Manager  
      deviceprofile - Device Profile  
            dhfwk - Distributed Hardware FWK  
            dinput - Distributed Input  
               disk - Disk I/O  
   istributeddatamgr - Distributed Data Manager  
            dlpcre - Dlp Credential Service  
               drm - Digital Rights Management  
            dsched - Distributed Schedule  
            dscreen - Distributed Screen  
               dslm - Device Security Level  
         dsoftbus - Distributed Softbus  
               ffrt - FFRT tasks  
   filemanagement - File Management  
               freq - CPU Frequency  
            graphic - Graphic Module  
         gresource - Global Resource Manager  
               hdcd - HDCD  
               hdf - HDF subsystem  
               huks - Universal KeyStore  
               i2c - I2C Events  
               idle - CPU Idle  
         interconn - Interconnection subsystem  
               ipa - Thermal Power Allocator  
               irq - IRQ Events  
            irqoff - IRQ-disabled code section tracing  
               load - CPU Load  
               mdfs - Mobile Distributed File System  
            membus - Memory Bus Utilization  
            memory - Memory  
         memreclaim - Kernel Memory Reclaim  
               misc - Misc Module  
               mmc - eMMC commands  
               msdp - Multimodal Sensor Data Platform  
   multimodalinput - HITRACE_TAG_MULTIMODALINPUT  
               net - Network  
      notification - Notification Module  
               nweb - NWEB Module  
               ohos - OpenHarmony  
         pagecache - Page Cache  
            power - Power Manager  
         preemptoff - Preempt-disabled code section tracing  
               push - Push subsystem  
         regulators - Voltage and Current Regulators  
               rpc - RPC and IPC  
            samgr - SAMGR  
            sched - CPU Scheduling  
         security - Security subsystem  
            sensors - Sensors Module  
               sync - Synchronization  
               ufs - UFS commands  
               usb - USB subsystem  
            useriam - User IAM  
            virse - Virtualization Service  
            window - Window Manager  
            workq - Kernel Workqueues  
            zaudio - OpenHarmony Audio Module  
            zcamera - OpenHarmony Camera Module  
            zimage - OpenHarmony Image Module  
            zmedia - OpenHarmony Media Module  
   ```  

2. Start capturing trace for specified tags.  

   ```shell  
   hitrace --trace_begin --record app  
   ```  

   **Example:**  

   ```shell  
   $ hitrace --trace_begin --record app  
   2024/11/14 11:48:45 hitrace enter, running_state is RECORDING_LONG_BEGIN_RECORD  
   2024/11/14 11:48:45 args: tags:app bufferSize:18432 overwrite:1  
   2024/11/14 11:48:45 OpenRecording done.  
   ```  

3. Stop capturing trace.  

   By default, trace information is printed in the command-line window.  

   ```shell  
   hitrace --trace_finish --record  
   ```  

   **Example 1:**  

   ```shell  
   $ hitrace --trace_finish --record  
   2024/11/14 11:50:33 hitrace enter, running_state is RECORDING_LONG_FINISH_RECORD  
   2024/11/14 11:50:33 capture done, output files:  
       /data/log/hitrace/record_trace_20241114115033@3010728-656499531.sys  
   ```  

   To specify an output path, trace information will be exported to the corresponding file.  

   ```shell  
   hitrace --trace_finish -o /data/local/tmp/test.ftrace  
   ```  

   **Example 2:**  

   ```shell  
   $ hitrace --trace_finish -o /data/local/tmp/test.ftrace  
   2024/11/14 11:50:33 start to read trace.  
   2024/11/14 11:50:33 trace read done, output: /data/local/tmp/test.ftrace  
   ```  

4. Set parameters for capturing trace.  

   ```shell  
   hitrace -b 10240 -t 10 -o /data/local/tmp/test2.ftrace app ability  
   ```  

   **Example:**  

   ```shell  
   $ hitrace -b 10240 -t 10 -o /data/local/tmp/test2.ftrace app ability  
   2024/11/14 11:52:13 start capture, please wait 10s ...  
   2024/11/14 11:52:23 capture done, start to read trace.  
   2024/11/14 11:52:23 trace read done, output: /data/local/tmp/test2.ftrace  
   ```  

   - Set buffer size to 10240 KB.  
   - Set trace capture duration to 10 seconds.  
   - Specify the output file as `/data/local/tmp/test1.htrace`.  
   - Capture trace for the `app` and `ability` tags.  

5. Export trace information.  

   By default, information is displayed in the command-line window.  

   ```shell  
   hitrace --trace_dump  
   ```  

   **Example 1:**  

   ```shell  
   $ hitrace --trace_dump  
   2024/11/14 11:54:23 start to read trace.  
   # tracer: nop  
   #  
   # entries-in-buffer/entries-written: 2/2   #P:4  
   #  
   #                                          _-----=> irqs-off  
   #                                         / _----=> need-resched  
   #                                        | / _---=> hardirq/softirq  
   #                                        || / _--=> preempt-depth  
   #                                        ||| /     delay  
   #           TASK-PID       TGID    CPU#  ||||   TIMESTAMP  FUNCTION  
   #              | |           |       |   ||||      |         |  
            <...>-21829   (  19280) [003] .... 3011033.731844: tracing_mark_write: trace_event_clock_sync: realtime_ts=1732002022239  
            <...>-21829   (  19280) [003] .... 3011033.731865: tracing_mark_write: trace_event_clock_sync: parent_ts=3011033.750000  
   #  
   ```  

   To specify an output path, trace information will be exported to the corresponding file.  

   ```shell  
   hitrace --trace_dump -o /data/local/tmp/test3.ftrace  
   ```  

   **Example 2:**  

   ```shell  
   $ hitrace --trace_dump -o /data/local/tmp/test3.ftrace  
   2024/11/14 11:54:23 start to read trace.  
   2024/11/14 11:54:23 trace read done, output: /data/local/tmp/test3.ftrace  
   ```  

   Alternatively, filter trace information by keywords using `hitrace --trace_dump | grep xxx`.  

6. Start snapshot-mode trace capture.  

   ```shell  
   hitrace --start_bgsrv  
   ```  

   **Example:**  

   ```shell  
   $ hitrace --start_bgsrv  
   2024/11/14 11:55:53 hitrace enter, running_state is SNAPSHOT_START  
   2024/11/14 11:55:54 OpenSnapshot done.  
   ```  

7. Export trace in snapshot mode.  

   By default, trace information is saved in `/data/log/hitrace/`. The filename follows the format `trace-YYMMDDHHmmSS@[BOOT_TIME].sys`. For visual trace analysis, use the [Smartperf_Host](https://gitcode.com/openharmony/developtools_smartperf_host) tool. Download link: [developtools_smartperf_host Release](https://gitcode.com/openharmony/developtools_smartperf_host/releases).  

   ```shell  
   hitrace --dump_bgsrv  
   ```  

   **Example:**  

   ```shell  
   $ hitrace --dump_bgsrv  
   2024/11/14 12:12:56 hitrace enter, running_state is SNAPSHOT_DUMP  
   2024/11/14 12:12:57 DumpSnapshot done, output:  
       /data/log/hitrace/record_trace_20241114121257@2566589-103807063.sys  
   ```  

8. Stop snapshot-mode trace capture.  

   ```shell  
   hitrace --stop_bgsrv  
   ```  

   **Example:**  

   ```shell  
   $ hitrace --stop_bgsrv  
   2024/11/14 11:59:43 hitrace enter, running_state is SNAPSHOT_STOP  
   2024/11/14 11:59:43 CloseSnapshot done.  
   ```  

9. Compress captured trace.  

   ```shell  
   hitrace -z -b 102400 -t 10 sched freq idle disk -o /data/local/tmp/test.ftrace  
   ```  

   **Example:**  

   ```shell  
   $ hitrace -z -b 102400 -t 10 sched freq idle disk -o /data/local/tmp/test.ftrace  
   2024/11/14 12:00:18 start capture, please wait 10s ...  
   2024/11/14 12:00:28 capture done, start to read trace.  
   2024/11/14 12:00:29 trace read done, output: /data/local/tmp/test.ftrace  
   ```  

10. Set trace output clock to boot (device system time).  

    ```shell  
    hitrace --trace_clock boot -b 102400 -t 10 sched freq idle disk -o /data/local/tmp/test.ftrace  
    ```  

    **Example:**  

    ```shell  
    $ hitrace --trace_clock boot -b 102400 -t 10 sched freq idle disk -o /data/local/tmp/test.ftrace  
    2024/11/14 12:01:42 start capture, please wait 10s ...  
    2024/11/14 12:01:52 capture done, start to read trace.  
    2024/11/14 12:01:52 trace read done, output: /data/local/tmp/test.ftrace  
    ```  

11. Stop capturing trace without printing trace information in the command-line window.  

   By default, trace information is saved in `/data/log/hitrace/`.  

   ```shell  
   hitrace --trace_finish_nodump  
   ```  

   **Example:**  

   ```shell  
   $ hitrace --trace_finish_nodump  
   2024/11/14 12:03:07 hitrace enter, running_state is RECORDING_LONG_FINISH_NODUMP  
   2024/11/14 12:03:07 end capture trace.  
   ```