# devicedebug Tool

The devicedebug tool provides developers with the capability to send signals to debug applications. Currently, it only supports sending signal signals to the PID of debug-type application processes managed by AMS, enabling the termination of the corresponding PID process.

> **Note:**
>
> Before using this tool, developers need to first obtain the <!--Del-->[<!--DelEnd-->hdc tool<!--Del-->](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md)<!--DelEnd--> and execute `hdc shell`.

**Table 1** devicedebug Tool Command List

| Command | Description |
| -------- | -------- |
| help/-h | Help command, displays the command information supported by devicedebug. |
| kill | Process termination command, used to terminate the corresponding PID process. |

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

## Process Termination Command

```bash
devicedebug kill
```

Used to send a signal (1-64) to a debug-type application process. Upon receiving the signal, the application process terminates the corresponding PID process.

**Table 3** kill Command List

| Command | Description |
| -------- |-------|
| help/-h | Help information. |
| -\<signal> \<pid> |  Required fields: signal (1-64) is the termination signal, used to terminate the debug-type application process corresponding to the PID. |

**Return Value:**

When the process corresponding to the PID is not an application process, it returns `"devicedebug: kill: {pid}: No such app process"`. When the process corresponding to the PID is not a debug-type application process, it returns `"devicedebug: kill: process: {pid} is not debuggable app"`.

Example:

```bash
# Example of terminating process 12111 with signal 9.
devicedebug kill -9 12111
```