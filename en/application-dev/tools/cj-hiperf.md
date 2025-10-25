# hiperf

hiperf provides command-line tools for developers to capture performance data of specific programs or systems, similar to the kernel's perf tool. This tool supports running on operating systems such as Windows/Linux/Mac.

## Environment Requirements

- Complete the [environment preparation](./cj-hdc.md#environment-preparation) according to the hdc command-line tool guide.
- Ensure the device is properly connected and execute `hdc shell`.

## hiperf Command-Line Description

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| --debug | Output debug-level logs. |
| --hilog | Write logs to hilog. |
| --logpath | Log file path. |
| --logtag | Log level. |
| --mixlog | Mixed log output. |
| --much | Output as much log as possible. |
| --nodebug | No log output. |
| --verbose | Output verbose-level logs. |

## Help Command

Use `--help` to view help information.

```shell
hiperf --help
```

**Example Usage:**

```bash
$ hiperf --help
Usage: hiperf [options] command [args for command]
options:
        --debug                 show debug log, usage format: --debug [command] [args]
        --help                  show help
        --hilog                 use hilog not file to record log
        --logpath               log file name full path, usage format: --logpath [filepath] [command] [args]
        --logtag                enable log level for HILOG_TAG, usage format: --logtag <tag>[:level][,<tag>[:level]] [command] [args]
                                tag: Dump, Report, Record, Stat... level: D, V, M...
                                example: hiperf --verbose --logtag Record:D [command] [args]
        --mixlog                mix the log in output, usage format: --much [command] [args]
        --much                  show extremely much debug log, usage format: --much [command] [args]
        --nodebug               disable debug log, usage format: --nodebug [command] [args]
        --verbose               show debug log, usage format: --verbose [command] [args]
        -h                      show help
command:
        dump:   Dump content of a perf data file, like perf.data
        help:   Show more help information for hiperf
        list:   List the supported event types.
        record: Collect performance sample information
        report: report sampling information from perf.data format file
        stat:   Collect performance counter information

See 'hiperf help [command]' for more information on a specific command.
```

Use the following command to view help information for sub-commands.

```shell
hiperf [command] --help
```

## list Command

Lists all supported event names on the device. Event names are used for the `-e` and `-g` parameters in `stat` and `record` commands.

**list Command Parameters:**

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| hw | Hardware events. |
| sw | Software events. |
| tp | Tracepoint events. |
| cache | Hardware cache events. |
| raw | Raw PMU events. |

```shell
Usage: hiperf list [event type name]
```

Use the `help` command to query supported event types.

```shell
hiperf list --help
```

**Example Usage:**

```bash
$ hiperf list --help
Usage: hiperf list [event type name]
       List all supported event types on this devices.
   To list the events of a specific type, specify the type name
       hw          hardware events
       sw          software events
       tp          tracepoint events
       cache       hardware cache events
       raw         raw pmu events
```

The following lists the HW events supported by the device and indicates which events are not supported.

```shell
hiperf list hw
```

**Example Usage:**

```bash
$ hiperf list hw
event not support hw-ref-cpu-cycles

Supported events for hardware:
        hw-cpu-cycles
        hw-instructions
        hw-cache-references
        hw-cache-misses
        hw-branch-instructions
        hw-branch-misses
        hw-bus-cycles
        hw-stalled-cycles-frontend
        hw-stalled-cycles-backend
```

## record Command

Samples the specified target program and saves the sampling data to a specified file (default is `/data/local/tmp/perf.data`).

**record Command Parameters:**

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| -a  | Collect system-wide information to evaluate all processes and threads. |
| --exclude-hiperf | Exclude hiperf's own data from collection. |
| -c | Set the CPU IDs to collect data from. |
| --cpu-limit | Set the maximum CPU usage percentage during collection (range: 1 - 100, default: 25). |
| -d | Collection duration. |
| -f | Collection frequency (default: 4000 times per second). Cannot be used with `--period`. |
| --period | Set the event collection period (how many events to collect per sample). Cannot be used with `-f`. |
| -e | Events to collect, separated by commas. |
| -g | Event groups to collect, separated by commas. |
| --no-inherit | Do not collect data from child processes. |
| -p | Process IDs to collect, separated by commas. Cannot be used with `-a`. |
| -t | Thread IDs to collect, separated by commas. Cannot be used with `-a`. |
| --exclude-tid | Thread IDs to exclude from collection, separated by commas. Cannot be used with `-a`. |
| --exclude-thread | Thread names to exclude from collection, separated by commas. Cannot be used with `-a`. |
| --offcpu | Track when threads are off CPU scheduling. |
| -j | Branch stack sampling. Filters support: any, any_call, any_ret, ind_call, ind_jmp, cond, call. |
| -s/--callstack | Set the call stack mode. |
| --kernel-callchain | Collect kernel-mode call stacks. Must be used with `-s fp/dwarf`. |
| --callchain-useronly | Collect only user-mode call stacks. |
| --delay-unwind | When `-s dwarf` is set, stacks will be unwound after recording instead of during. |
| --disable-unwind | When `-s dwarf` is set, stacks will not be unwound by default during recording. |
| --disable-callstack-expand | When `-s dwarf` is set, disable the 64K stack limit. By default, call stacks are merged to build more complete call stacks (may sometimes be inaccurate). |
| --enable-debuginfo-symbolic | When `-s fp/dwarf` is set, symbols in the `.gnu_debugdata` section of ELF files will be parsed (not parsed by default). |
| --clockid | Set the clock type for collection (supports `monotonic` and `monotonic_raw`). |
| --symbol-dir | Path to symbol table files for online symbolization. |
| -m | Number of mmap pages (range: 2 - 1024, default: 1024). |
| --app | Application names to collect, separated by commas. Applications must be in debuggable mode. Waits 20s if the application is not running. |
| --chkms | Set the query interval (range: 1 - 200, default: 10). |
| --data-limit | Stop collection when output data reaches the specified size (no limit by default). |
| -o | Set the output file path. |
| -z | Output in compressed format. |
| --restart | Collect performance metrics during application startup. Exits if the process does not start within 30 seconds. |
| --verbose | Output more detailed reports. |
| --control [command]| Collection command control parameters. Commands include: prepare/start/pause/resume/stop. |
| --dedup_stack | Remove duplicate stacks from records. Cannot be used with `-a`. |
| --cmdline-size | Set the value of `/sys/kernel/tracing/saved_cmdlines_size` (range: 512 - 4096). |
| --report | Generate a stack report after collection. Cannot be used with `-a`. |
| --dumpoptions | Dump command options. |

```shell
Usage: hiperf record [options] [command [command-args]]
```

Sample process with PID 267 for 10 seconds using dwarf call stacks.

```shell
hiperf record -p 267 -d 10 -s dwarf
```

**Example Usage:**

```bash
$ hiperf record -p 1273 -d 10 -s dwarf
Profiling duration is 10.000 seconds.
Start Profiling...
Timeout exit (total 10000 ms)
Process and Saving data...
/proc/sys/kernel/kptr_restrict is NOT 0, will try set it to 0.
[ hiperf record: Captured 0.297 MB perf data. ]
[ Sample records: 97, Non sample records: 2426 ]
[ Sample lost: 0, Non sample lost: 0 ]
```

## stat Command

Monitors the specified target program and periodically prints performance counter values.

**stat Command Parameters:**

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| -a  | Collect system-wide information to evaluate all processes and threads. |
| -c | Set the CPU IDs to collect data from. |
| -d | Collection duration. |
| -i | Set the interval (in ms) for printing stat information. |
| -e | Events to collect, separated by commas. |
| -g | Event groups to collect, separated by commas. |
| --no-inherit | Do not collect data from child processes. |
| -p | Process IDs to collect, separated by commas. Cannot be used with `-a`. |
| -t | Thread IDs to collect, separated by commas. Cannot be used with `-a`. |
| --app | Application names to collect, separated by commas. Applications must be in debuggable mode. Waits 10s if the application is not running. |
| --chkms | Set the query interval (range: 1 - 200, default: 10). |
| --per-core | Print counts per CPU core. |
| --pre-thread | Print counts per thread. |
| --restart | Collect performance metrics during application startup. Exits if the process does not start within 30 seconds. |
| --verbose | Output more detailed reports. |
| --dumpoptions | Dump command options. |

```shell
Usage: hiperf stat [options] [command [command-args]]
```

The following example shows a `stat` command monitoring process 1273 on CPU 0 for 3 seconds.

```shell
hiperf stat -p 1273 -d 3 -c 0
```

**Example Usage:**

```bash
$ hiperf stat -p 1273 -d 3 -c 0
Profiling duration is 3.000 seconds.
Start Profiling...
Timeout exit (total 3000 ms)
                    count  name                           | comment                          | coverage
                      521  hw-branch-instructions         |                                  | (9%)
                      217  hw-branch-misses               |                                  | (9%)
                   32,491  hw-cpu-cycles                  |                                  | (9%)
                    4,472  hw-instructions                |                                  | (9%)
                        1  sw-context-switches            |                                  | (9%)
                        0  sw-page-faults                 |                                  | (9%)
                   39,083  sw-task-clock                  | 0.000143 cpus used               | (9%)
```

## dump Command

This command reads `perf.data` in raw format, allowing developers and testers to verify the correctness of the original sampling data.

**dump Command Parameters:**

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| --head | Output only the data header and attributes. |
| -d | Output only the data segment. |
| -f | Output only additional features. |
| --syspath | Symbol table file path. |
| -i | Input file path. |
| -o | Output file path (default: screen). |
| --elf | Output ELF file. |
| --proto | Output protobuf format data. |
| --export | Export user stack data to a split file (generates UT data). |

```shell
Usage: hiperf dump [option] <filename>
```

Use the `dump` command to read `/data/local/tmp/perf.data` and output to `/data/local/tmp/perf.dump`.

```shell
hiperf dump -i /data/local/tmp/perf.data -o /data/local/tmp/perf.dump
```

**Example Usage:**

```bash
$ hiperf dump -i /data/local/tmp/perf.data -o /data/local/tmp/perf.dump
dump result will save at '/data/local/tmp/perf.dump'
```

## report Command

This command primarily displays sampled data (read from `perf.data`) and converts it into the desired format (e.g., JSON or ProtoBuf).

**report Command Parameters:**

| Parameter | Description |
| -------- | -------- |
| -h/--help  | Help command. |
| --symbol-dir | Symbol table file path. |
| --limit-percent | Display only the top percentage of content. |
| -s | Display call stack mode. |
| --call-stack-limit-percent | Display only the top percentage of stack content. |
| -i | Input file path (default: `perf.data`). |
| -o | Output file path (default: screen). |
| --proto | Output protobuf format data. |
| --json | Output JSON format data. |
| --diff | Display differences between `-i` and `--diff` files. |
| --branch | Display branches from addresses instead of IP addresses. |
| --\<keys> \<keyname1>\[,keyname2]\[,...] | Optional keywords: comms, pids, tids, dsos, funcs, from_dsos, from_funcs. Example: `--comms hiperf`. |
| --sort [key1],[key2],[...] | Sort by keywords. |
| --hide_count | Hide counts in the report. |
| --dumpoptions | Dump command options. |

```shell
Usage: hiperf report [option] <filename>
```

Example command to output a standard report, limited to 1% of samples.

```shell
hiperf report --limit-percent 1
```

## Scripts

General users can use scripts to perform sampling operations and generate visual flame graphs. Tools can be obtained from the [developtools_hiperf repository](https://gitee.com/openharmony/developtools_hiperf/tree/master/script).

1. Sampling.

   Performed by `command_script.py`, a wrapper script for the `report` command.

   ```shell
   usage: command_script.py [-h]
                            (-app PACKAGE_NAME | -lp LOCAL_PROGRAM | -cmd CMD | -p [PID [PID ...]] | -t [TID [TID ...]] | -sw)
                            [-a ABILITY] [-r RECORD_OPTIONS] [-lib LOCAL_LIB_DIR]
                            [-o OUTPUT_PERF_DATA] [--not_hdc_root]
   ```

   Sample the specified package name (e.g., `com.ohos.launch`).

   ```shell
   python command_script.py -app com.ohos.launch
   ```

   Sample a specific process (e.g., `hdcd`).

   ```shell
   python command_script.py -lp hdcd
   ```

2. Collect Symbol Tables.

   Performed by `recv_binary_cache.py`, which searches for ELF files corresponding to the files and libraries recorded in `perf.data` (based on their build IDs) in user-specified paths for stack unwinding or function name printing.

   ```shell
   usage: recv_binary_cache.py [-h] [-i PERF_DATA] [-l LOCAL_LIB_DIR [LOCAL_LIB_DIR ...]]
   ```

   Specify two symbol table paths.

   ```shell
   python recv_binary_cache.py -l Z:\OHOS_MASTER\out\ohos-arm-release\lib.unstripped  Z:\OHOS_MASTER\out\ohos-arm-release\exe.unstripped
   ```

   Corresponding symbol table files will be copied to the `binary_cache` folder. The script first checks user-provided paths; if not found, it copies files from the device.

3. Generate Flame Graphs.

   Performed by `make_report.py`, which exports sampled data to an HTML display page.

   ```shell
   usage: make_report.py [-h] [-i PERF_DATA] [-r REPORT_HTML]
   ```

   Generate an HTML file (default filename: `hiperf_report.html`).

   ```shell
   python make_report.py -i perf.data
   ```