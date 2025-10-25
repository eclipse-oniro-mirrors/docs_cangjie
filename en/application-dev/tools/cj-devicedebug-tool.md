# devicedebug Tool

The devicedebug tool provides developers with the capability to send signals to debug applications. Currently, it only supports sending signal signals to the process IDs (pids) of debug-type application processes managed by AMS, enabling the termination of corresponding pid processes.

> **Note:**
>
> Before using this tool, developers need to first obtain the <!--Del-->[<!--DelEnd-->hdc tool<!--Del-->](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md)<!--DelEnd--> and execute `hdc shell`.

**Table 1** devicedebug Tool Command List

| Command | Description |
| -------- | -------- |
| help/-h | Help command, displays the command information supported by devicedebug. |
| kill | Terminate process command, used to terminate the corresponding pid process. |

## Help Command

```bash
devicedebug help
```

**Table 2** help Command List

| Command    | Description       |
| ------- | ---------- |
| devicedebug help | Displays the command information supported by devicedebug. |

Example:

```bash
# Display help information.
devicedebug help
```

## Terminate Process Command

```bash
devicedebug kill
```

Used to send a signal (1-64) to a debug-type application process. Upon receiving the signal, the application process terminates the corresponding pid process.

**Table 3** kill Command List

| Command | Description |
| -------- |-------|
| help/-h | Help information. |
| -\<signal> \<pid> |  Required field, where signal (1-64) is the termination signal, used to terminate the debug-type application process corresponding to the pid. |

**Return Value:**

When the process corresponding to the pid is not an application process, it returns "devicedebug: kill: {pid}: No such app process"; when the process corresponding to the pid is not a debug-type application process, it returns "devicedebug: kill: process: {pid} is not debuggable app".

Example:

```bash
# Example of terminating process 12111 with signal 9.
devicedebug kill -9 12111
```