# Viewing HiTraceMeter Logs

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

## Viewing via DevEco Studio Visual Interface

Developers can use the CPU Insight feature in DevEco Studio Profiler to visually display HiTraceMeter log content, analyze the CPU usage and thread running status of applications/services, and examine the execution time consumption of programs on the CPU during specified time periods. For detailed usage instructions, refer to [CPU Activity Analysis: CPU Profiling](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-insight-session-cpu-V5).

## Viewing via Command Line Tools

1. Follow the hdc command-line tool guide to complete [Environment Preparation](../tools/cj-hdc.md#environment-preparation), ensuring the `hdc shell` command can properly connect to the device.

2. Execute the `hdc shell` command in DevEco Studio's Terminal window or the host command-line window to connect to the device. Then, run the [hitrace](../tools/cj-hitrace.md) command on the device to start the HiTraceMeter log capture service.

   ```shell
   PS D:\xxx\xxx> hdc shell
   # hitrace --trace_begin app
   ```

3. Run the program containing HiTraceMeter instrumentation points on the device.

4. Dump the HiTraceMeter text logs, which include the HiTraceMeter instrumentation information from step 3.

   - By default, logs are printed in the window.

   ```shell
   # hitrace --trace_dump
   ```

   - Alternatively, provide a filename to save the logs to a file. The file path must be `/data/local/tmp/`, as other paths lack permissions.

   ```shell
   # hitrace --trace_dump -o /data/local/tmp/trace.ftrace
   ```

5. Execute the hitrace command on the device to stop the HiTraceMeter log capture service.

   ```shell
   # hitrace --trace_finish
   ```

6. Exit the device, return to the host, and export the HiTraceMeter text logs from the device to the current directory.

   ```shell
   # exit
   PS D:\xxx\xxx> hdc file recv /data/local/tmp/trace.ftrace ./
   ```

7. Search for keywords such as instrumentation names in the HiTraceMeter text logs to verify successful instrumentation.

8. Visual analysis of HiTraceMeter text logs.

   - Import into DevEco Studio for analysis. Refer to the [CPU Activity Analysis: CPU Profiling](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-insight-session-cpu-V5) documentation. In DevEco Studio Profiler's session area, select "Open File" to import the HiTraceMeter text logs for analysis.
   - Use [Smartperf_Host](https://gitcode.com/openharmony/developtools_smartperf_host) for analysis. You can download the tool from [developtools_smartperf_host Release](https://gitcode.com/openharmony/developtools_smartperf_host/releases).