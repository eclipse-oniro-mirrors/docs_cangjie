# toybox

toybox is a lightweight collection of Linux command-line utilities that combines commonly used Linux commands into a single executable file.

## Prerequisites

### Usage Method 1

- Connect the device normally
- Use `hdc shell` to enter command-line execution mode

### Usage Method 2

- Run within the application sandbox

## Command-Line Instructions

toybox can be executed in two ways:

- `toybox [command] [arguments...]`
- Directly execute `[command] [arguments...]`

Where `[command]` can be replaced with any command supported by toybox (queryable by running toybox without parameters).  
`[arguments...]` represents the parameters required by `[command]`.

<!--RP1-->
<!--RP1End-->

### Help Command

Format: `toybox [--long | --help | --version | [command] [arguments...]]`

| Option | Parameters | Description |
| :- | :- | :- |
| `--help` | NA | Display command help. |
| `--long` | NA | Display paths of all supported commands. |
| `--version` | NA | Display version number. |
| NA | NA | Display all commands supported by `[command]`. |
| `[command]` | `[arguments]` | Execute a specific command. Most commands also support `--help` and `--version` parameters. |

Format: `help [-ah] [command]`

| Parameter | Description |
| :- | :- |
| `command` | Display help for `command`. `[command]` can be replaced with any command supported by toybox. |

| Option | Description |
| :- | :- |
| `-a` | Display help for all commands. |

### Mathematical and Basic Computer Functions

| Command | Description |
| :- | :- |
| `ascii`     | Display ASCII encoding table.<br/>Usage: `ascii` |
| `factor`     | Factorize numbers into primes.<br/>Usage: `factor NUMBER...` |
| `mcookie` | Generate a 128-bit strong random number.<br/>Usage: `mcookie [-vV]` |
| `mkpasswd` | Encrypt passwords.<br/>Usage: `mkpasswd [-P FD] [-m TYPE] [-S SALT] [PASSWORD] [SALT]` |
| `uuidgen`    | Create and print a new RFC4122 random UUID.<br/>Usage: `uuidgen` |

### Terminal Operations

| Command | Description |
| :- | :- |
| `chvt`   | Switch to virtual terminal N.<br/>Usage: `chvt N` |
| `chroot` | Run command with specified root directory.<br/>Usage: `chroot NEWROOT [COMMAND [ARG...]]` |
| `clear`  | Clear the terminal.<br/>Usage: `clear` |
| `nohup`  | Run a command immune to hangups.<br/>Usage: `nohup COMMAND [ARG...]` |
| `tty`    | Display the name of the terminal connected to standard input.<br/>Usage: `tty [-s]` |
| `reset`  | Reset the terminal.<br/>Usage: `reset` |
| `microcom` | Simple serial terminal.<br/>Usage: `microcom [-s SPEED] [-X] DEVICE` |

### sh Logic Commands

| Command | Description |
| :- | :- |
| `false` | Return non-zero exit status.<br/>Usage: `false` |
| `sh`    | Shell command interpreter. |
| `test`  | Evaluate conditional expressions. Returns false if no arguments.<br/>Usage: `test [-bcdefghLPrSsuwx PATH] [-nz STRING] [-t FD] [X ?? Y]` |
| `true`  | Return zero exit status.<br/>Usage: `true` |
| `yes`   | Repeatedly output a line until killed. Outputs "y" if no arguments.<br/>Usage: `yes [args...]` |

### System Operations

| Command | Description |
| :- | :- |
| `acpi`   | Query power/temperature status.<br/>Usage: `acpi [-abctV]` |
| `arch` | Print system architecture.<br/>Usage: `arch` |
| `dmesg` | Display or control kernel ring buffer.<br/>Usage: `dmesg [-Cc] [-r \| -t \| -T] [-n LEVEL] [-s SIZE] [-w]` |
| `dnsdomainname` | Display system name (same as `hostname -d`).<br/>Usage: `dnsdomainname` |
| `getconf`   | Get system configuration values (some require PATH parameter).<br/>Usage: `getconf -a [PATH] \| -l \| NAME [PATH]` |
| `env`       | Set environment for command invocation or list environment variables.<br/>Usage: `env [-i] [-u NAME] [NAME=VALUE...] [COMMAND [ARG...]]` |
| `hostname`  | Get/set current hostname.<br/>Usage: `hostname [-bdsf] [-F FILENAME] [newname]` |
| `insmod`    | Load kernel module.<br/>Usage: `insmod MODULE [MODULE_OPTIONS]` |
| `logger`    | Log system messages.<br/>Usage: `logger [-s] [-t TAG] [-p [FACILITY.]PRIORITY] [message...]` |
| `lsmod`     | Display currently loaded modules, their sizes and dependencies.<br/>Usage: `lsmod` |
| `mix`       | Display OSS channels or set volume.<br/>Usage: `mix [-d DEV] [-c CHANNEL] [-l VOL] [-r RIGHT]` |
| `modinfo`   | Display kernel module information.<br/>Usage: `modinfo [-0] [-b basedir] [-k kernel] [-F field] [module \| file...]` |
| `nproc`     | Print number of processors.<br/>Usage: `nproc [--all]` |
| `oneit`     | Simple init program.<br/>Usage: `oneit [-p] [-c /dev/tty0] command [...]` |
| `partprobe` | Inform kernel of partition table changes.<br/>Usage: `partprobe DEVICE...` |
| `pivot_root` | Change root directory.<br/>Usage: `pivot_root OLD NEW` |
| `printenv`  | Print environment variables.<br/>Usage: `printenv [-0] [env_var...]` |
| `reboot/halt/poweroff` | Reboot/stop/shutdown.<br/>Usage: `reboot/halt/poweroff [-fn]` |
| `rfkill`    | Enable/disable wireless devices.<br/>Usage: `rfkill COMMAND [DEVICE]` |
| `rmmod`     | Unload kernel module.<br/>Usage: `rmmod [-wf] [MODULE]` |
| `sendevent` | Send Linux input event.<br/>Usage: `sendevent DEVICE TYPE CODE VALUE` |
| `swapoff`   | Disable swap space.<br/>Usage: `swapoff swapregion` |
| `swapon`    | Enable swapping on specified device/file.<br/>Usage: `swapon [-d] [-p priority] filename` |
| `switch_root` | Switch root directory and execute new INIT program.<br/>Usage: `switch_root [-c /dev/console] NEW_ROOT NEW_INIT...` |
| `uname`     | Print system information.<br/>Usage: `uname [-asnrvm]` |
| `vmstat`    | Print virtual memory statistics.<br/>Usage: `vmstat [-n] [DELAY [COUNT]]` |

### Time and Date

| Command | Description |
| :- | :- |
| `cal`     | Display calendar.<br/>Usage: `cal [[month] year]` |
| `date`    | Set/get current date/time.<br/>Usage: `date [-u] [-r FILE] [-d DATE] [+DISPLAY_FORMAT] [SET]` |
| `hwclock` | Get/set hardware clock.<br/>Usage: `hwclock [-rswtluf]` |
| `sleep`   | Wait for specified duration before exiting. Can be fractional. Optional suffixes: "m" (minutes), "h" (hours), "d" (days), or "s" (seconds, default).<br/>Usage: `sleep DURATION` |
| `time`    | Run command line and report real, user, and system time in seconds. (Real=clock time, user=CPU time used by command code, system=CPU time used by OS.)<br/>Usage: `time [-pv] COMMAND [ARGS...]` |
| `uptime`  | Display current time, system uptime, number of users, and system load averages for past 1, 5, and 15 minutes.<br/>Usage: `uptime [-ps]` |
| `usleep`  | Wait for specified microseconds before exiting.<br/>Usage: `usleep MICROSECONDS` |

### User Operations

| Command | Description |
| :- | :- |
| `groups`  | Print user's group memberships.<br/>Usage: `groups [user]` |
| `id`      | Print user and group IDs.<br/>Usage: `id [-nGgru] [USER...]` |
| `login`   | User login.<br/>Usage: `login [-p] [-h host] [-f USERNAME] [USERNAME]` |
| `logname/whoami` | Print current username.<br/>Usage: `logname/whoami` |
| `passwd`  | Update user's authentication tokens.<br/>Usage: `passwd [-a ALGO] [-dlu] [USER]` |
| `who`     | Print information about logged-in users.<br/>Usage: `who` |
| `w`       | Show who is logged on and what they're doing.<br/>Usage: `w` |

### Process Operations

| Command | Description |
| :- | :- |
| `chrt`      | Get/set process scheduling policy and priority.<br/>Usage: `chrt [-Rmofrbi] {-p PID [PRIORITY] \| [PRIORITY COMMAND...]}` |
| `iorenice`  | Display/modify process IO priority.<br/>Usage: `iorenice PID [CLASS] [PRIORITY]` |
| `iotop`     | Sort processes by I/O usage.<br/>Usage: `iotop [-AaKObq] [-n NUMBER] [-d SECONDS] [-p PID,] [-u USER,]` |
| `ionice`    | Display/modify process IO scheduling priority.<br/>Usage: `ionice [-t] [-c CLASS] [-n LEVEL] [COMMAND...\|-p PID]` |
| `kill`      | Send signal to process.<br/>Usage: `kill [-l [SIGNAL] \| -s SIGNAL \| -SIGNAL] pid...` |
| `killall`   | Send signal to all processes with given name (default: SIGTERM).<br/>Usage: `killall [-l] [-iqv] [-SIGNAL \| -s SIGNAL]  PROCESS_NAME...` |
| `killall5`  | Send signal to all processes outside current session.<br/>Usage: `killall5 [-l [SIGNAL]] [-SIGNAL \| -s SIGNAL] [-o PID]...` |
| `pidof`   | Print PIDs of all processes with given name.<br/>Usage: `pidof [-s] [-o omitpid[,omitpid...]] [NAME...]` |
| `pkill`   | Kill processes by name.<br/>Usage: `pkill [-fnovx] [-SIGNAL \| -l SIGNAL] [PATTERN] [-G GID,] [-g PGRP,] [-P PPID,] [-s SID,] [-t TERM,] [-U UID,] [-u EUID,]` |
| `pmap`    | Show process memory map.<br/>Usage: `pmap [-xq] [pids...]` |
| `ps`      | Display process information.<br/>Usage: `ps [-AadefLlnwZ] [-gG GROUP,] [-k FIELD,] [-o FIELD,] [-p PID,] [-t TTY,] [-uU USER,]` |
| `pwdx`    | Print process working directory.<br/>Usage: `pwdx PID...` |
| `renice`  | Alter priority of running process/group/user.<br/>Usage: `renice [-gpu] -n increment ID ...` |
| `setsid`  | Run program in new session.<br/>Usage: `setsid [-t] command [args...]` |
| `taskset` | Start task running only on specified processors, or modify existing process processor affinity.<br/>Usage: `taskset [-ap] [mask] [PID \| cmd [args...]]` |
| `timeout` | Create child process to execute command, send signal if child doesn't exit within DURATION. DURATION can be fractional. Optional suffixes: "m" (minutes), "h" (hours), "d" (days), or "s" (seconds, default).<br/>Usage: `timeout [-k DURATION] [-s SIGNAL] DURATION COMMAND...` |
| `top`     | Display real-time process information.<br/>Usage: `top [-Hhbq] [-k FIELD,] [-o FIELD,] [-s SORT] [-n NUMBER] [-m LINES] [-d SECONDS] [-p PID,] [-u USER,]` |
| `nice`    | Run command with specified priority.<br/>Usage: `nice [-n PRIORITY] COMMAND [ARG...]` |
| `nsenter` | Run command in specified namespaces.<br/>Usage: `nsenter [-t pid] [-F] [-i] [-m] [-n] [-p] [-u] [-U] COMMAND...` |
| `ulimit/prlimit` | Display/set process resource limits.<br/>Usage: `ulimit/prlimit [-P PID] [-SHRacdefilmnpqrstuv] [LIMIT]` |
| `unshare` | Create new namespaces for process, some attributes not shared with parent.<br/>Usage: `unshare [-imnpuUr] COMMAND...` |
| `watch`   | Run command every -n seconds, display output. Press q to quit.<br/>Usage: `watch [-teb] [-n SEC] PROG ARGS` |
| `xargs`   | Run command line one or more times, appending arguments from stdin.<br/>Usage: `xargs [-0prt] [-s NUM] [-n NUM] [-E STR] COMMAND...` |

### Device Node Operations

| Command | Description |
| :- | :- |
| `blkid`       | Print filesystem type, label, UUID, etc.<br/>Usage: `blkid [-s TAG] [-UL] DEV...` |
| `blockdev`    | Call ioctl on block device for each command.<br/>Usage: `blockdev --OPTION... BLOCKDEV...` |
| `devmem`      | Read/write physical address via /dev/mem.<br/>Usage: `devmem ADDR [WIDTH [DATA]]` |
| `df`          | Show total/used/free disk space for each filesystem listed. Shows all mounted filesystems if no arguments.<br/>Usage: `df [-HPkhi] [-t type] [FILESYSTEM ...]` |
| `du`          | Show disk usage (space taken by files/directories).<br/>Usage: `du [-d N] [-askxHLlmc] [file...]` |
| `eject`       | Eject device (default: /dev/cdrom).<br/>Usage: `eject [-stT] [DEVICE]` |
| `free`        | Show total/used/free physical memory and swap space.<br/>Usage: `free [-bkmgt]` |
| `freeramdisk` | Free all memory of specified ramdisk.<br/>Usage: `freeramdisk [RAM device]` |
| `fsfreeze`    | Freeze/unfreeze filesystem.<br/>Usage: `fsfreeze {-f \| -u} MOUNTPOINT` |
| `fstype`      | Print filesystem type.<br/>Usage: `fstype DEV...` |
| `fsync`       | Sync file state with storage device.<br/>Usage: `fsync [-d] [FILE...]` |
| `i2cdetect`   | Detect i2c devices.<br/>Usage:<br/>&emsp;`i2cdetect [-ary] BUS [FIRST LAST]` <br/>&emsp;`i2cdetect -F BUS`<br/>&emsp;`i2cdetect -l`|
| `i2cdump`     | Print all i2c registers.<br/>Usage: `i2cdump [-fy] BUS CHIP` |
| `i2cget`      | Read i2c register.<br/>Usage: `i2cget [-fy] BUS CHIP ADDR` |
| `i2cset`      | Write i2c register.<br/>Usage: `i2cset [-fy] BUS CHIP ADDR VALUE... MODE` |
| `losetup`     | Set up loop devices.<br/>Usage: `losetup [-cdrs] [-o OFFSET] [-S SIZE] {-d DEVICE... \| -j FILE \| -af \| {DEVICE FILE}}` |
| `lspci`       | Show PCI device information.<br/>Usage: `lspci [-ekmn] [-i FILE ]` |
| `lsusb`       | Show USB device information.<br/>Usage: `lsusb` |
| `makedevs`    | Create special files (block/character devices, etc.).<br/>Usage: `makedevs [-d device_table] rootdir` |
| `mount`       | Mount new filesystem on directory. Shows existing mounts if no arguments.<br/>Usage: `mount [-afFrsvw] [-t TYPE] [-o OPTION,] [[DEVICE] DIR]` |
| `mountpoint`  | Check if