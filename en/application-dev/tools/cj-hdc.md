# hdc

hdc (OpenHarmony Device Connector) is a command-line tool provided for developers to debug and interact with devices across Windows/Linux/macOS systems.

hdc consists of three components:

**client:** A process running on the host computer, launched when developers execute hdc commands, which terminates after command completion.

**server:** A background service process running on the host computer, managing data interaction between client processes and device-side daemon processes, as well as device discovery.

**daemon:** A daemon process running on the device side, responding to requests from the host-side server.

The relationship is illustrated below:

![hdc architecture](./figures/hdc_image_005.PNG)

> **Note:**
>
> When hdc client starts, it automatically checks if the server is running. If not, it launches a new hdc program as a background server.
>
> By default, hdc server listens on port 8710 for 2-in-1 devices. Developers can customize the listening port by setting the system environment variable OHOS_HDC_SERVER_PORT.

## Environment Setup

Download and install [DevEco Studio](https://developer.huawei.com/consumer/cn/deveco-studio/). The hdc executable can be found in: DevEco Studio\sdk\default\openharmony\toolchains directory.

### (Optional) Direct hdc Execution via Command Line

Developers can navigate to the SDK's toolchains directory via command line and execute hdc commands for debugging.

To conveniently execute hdc directly from any command line location, developers can add the hdc executable path to the operating system's command search path environment variable.

For example, Windows users can add it to the system Path variable.

### (Optional) Server Listening Port Configuration

By default, hdc server listens on port 8710 for 2-in-1 devices, with hdc client using TCP protocol to connect through this port. If port 8710 is occupied or other ports are preferred, modify the server's listening port by adding the OHOS_HDC_SERVER_PORT environment variable.

Example: Add variable name: OHOS_HDC_SERVER_PORT, variable value: any available port (e.g., 18710).

> **Note:**
>
> After configuring environment variables, close and restart the command line or any software using OpenHarmony SDK.

## hdc Command List

### Global Parameters

Global parameters can follow hdc when executing certain commands, for example:

To execute commands on a specific device using -t parameter:

```shell
hdc -t connect-key shell echo "Hello world"
```

| Parameter | Description |
| -------- | -------- |
| -t | Connect to specified target device. Optional for single device, mandatory for multiple devices. |
| -l | Optional. Specify runtime log level (0-6), default 3 (LOG_INFO). |
| -s | Optional. Specify server process network listening parameters when client connects, format: ip:port. |
| -p | Optional. Bypass server process query step for faster client command execution. |
| -m | Optional. Start server process in foreground mode. |

### Command List

| Command | Description |
| -------- | -------- |
| list targets | Query all connected target devices. |
| wait | Wait for device connection. |
| tmode usb | Deprecated. No actual device channel operation. Configure via USB debugging switch in device settings. |
| tmode port | Enable device network connection channel. |
| tmode port close | Disable device network connection channel. |
| tconn | Connect specified device via "IP:port". |
| shell | Execute single command on device side. |
| install | Install specified application file. |
| uninstall | Uninstall specified application package. |
| file send | Send file from local to remote device. |
| file recv | Receive file from remote device to local. |
| fport ls | List all port forwarding tasks. |
| fport | Set up forward port forwarding: listen on "host port" and forward to "device port". |
| rport | Set up reverse port forwarding: listen on "device port" and forward to "host port". |
| fport rm | Remove specified port forwarding task. |
| start | Start hdc server process. |
| kill | Terminate hdc server process. |
| hilog | Print device-side log information. |
| jpid | Display PIDs of all applications with JDWP debugging protocol enabled. |
| track-jpid | Real-time display of application PIDs and names with JDWP debugging enabled. |
| target boot| Reboot target device. |
| <!--DelRow--> target mount | Mount system partition in read-write mode (not available for non-root devices). |
| <!--DelRow--> smode | Grant root privileges to device-side hdc daemon. Use -r parameter to revoke (not available for non-root devices). |
| keygen | Generate new key pair. |
| version | Print hdc version information (also available via hdc -v). |
| checkserver | Get client and server process version information. |

> **Note:**
>
> Global parameters must precede commands when used.

## Basic Usage

Before using hdc, enable USB debugging on the device and connect it to the 2-in-1 via USB cable.

### Query Connected Devices

```shell
hdc list targets
```

### Execute Shell Command

```shell
hdc shell echo "Hello world"
```

### Get Help

| Command | Description |
| -------- | -------- |
| -h [verbose] | Display hdc help information. Optional parameter: verbose for detailed help. |
| help | Display hdc help information. |

Display hdc help information:

```shell
hdc -h [verbose]
hdc help
```

**Return Value:**

| Return Value | Description |
| -------- | -------- |
| OpenHarmony device connector(HDC) ...<br/>------global commands:-------<br/>-h/help [verbose]&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- Print hdc help, 'verbose' for more other cmds<br/>..._(detailed help omitted)_ | hdc command help information |

**Usage:**

```shell
hdc -h
hdc help

// Display detailed help
hdc -h verbose
```

### Usage Notes

- If hdc encounters exceptions, try killing abnormal processes and restarting hdc service via `hdc kill -r`.

- If `hdc list targets` returns no device information, refer to [Device Not Recognized](#device-not-recognized) section.

## Device Connection Management

### Query Device List

Use `list targets` to query all connected target devices.

Add -v parameter for detailed device information.

Command format:

```shell
hdc list targets [-v]
```

**Return Value:**

| Return Value | Description |
| -------- | -------- |
| Device identifier list | List of connected device identifiers (connect-key for -t parameter). |
| [Empty] | No devices detected. |

**Usage:**

```shell
hdc list targets
hdc list targets -v
```

### Connect to Specified Target Device

For single device connections, device identifier is optional;
For multiple devices, use -t parameter to specify target device identifier:

```shell
hdc -t [connect-key] [command]
```

**Parameters:**

| Parameter | Description |
| -------- | -------- |
| connect-key| Unique device identifier (output from `hdc list targets`). |
| command | Supported hdc command. |

> **Note:**
>
> connect-key is unique per device. For USB connections, it's the serial number; for network connections, it's "IP:port".

**Return Value:**

| Return Value | Description |
| -------- | -------- |
| Command execution output | See corresponding command's return value. |
| [Fail]Not match target founded, check connect-key please | No device matches connect-key. |
| [Fail]Device not founded or connected | Device not found or disconnected. |
| [Fail]ExecuteCommand need connect-key? please confirm a device by help info | Device specification required for multiple connections. |
| Unknown operation command... | Unsupported command. |

> **Note:**
>
> Error messages may be optimized later. Do not use them for automated script/program result judgment.

**Usage Example:**

Used with specific operation commands. Example with shell command:

```shell
hdc list targets  // Query connect-key for all connected devices
hdc -t [connect-key] shell // Replace [connect-key] with actual device identifier
```

### Wait for Device Connection

Command format:

```shell
hdc wait // Wait for any device connection
hdc -t connect-key wait // Wait for specified device connection
```

**Return Value:**

| Return Value | Description |
| -------- | -------- |
| None | Command completes when recognized device connects normally. |

**Usage:**

```shell
hdc wait
hdc -t connect-key wait
```

### Common Connection Scenarios

#### USB Connection

- Environment Verification

| Check Item | Normal | Exception Handling |
| -------- | -------- | -------- |
| USB debugging | Enabled | If USB debugging cannot auto-enable, try rebooting device. |
| USB cable | Using data-capable USB cable connected to 2-in-1's USB port | Replace with official data cable if connection issues occur. |
| USB port | Direct motherboard USB port (rear panel for desktops, built-in for laptops) | Avoid using adapters/hubs/front panel ports which may cause instability. Use direct connection. |
| hdc environment | `hdc -h` returns help information | Refer to [Environment Setup](#environment-setup). |
| Driver | "HDC Device" or "HDC Interface" appears in device manager under USB devices | Refer to [Device Not Recognized](#device-not-recognized). |

- Connection Steps

1. Connect device to 2-in-1 via USB.
2. Check connected devices:
   ```shell
   hdc list targets
   ```
   Successful USB connection shows device identifier in output.
3. After device appears, execute commands. For USB-only connections (no TCP/IP in `list targets` output), omit device identifier:
   ```shell
   hdc shell
   ```

#### TCP Connection

> **Warning:**
>
> TCP debugging is not yet stable. Use cautiously in production.

- Environment Verification

| Check Item | Normal | Exception Handling |
| -------- | -------- | -------- |
| Network | 2-in-1 and device on same network. | Connect to same WiFi or use device hotspot. |
| Network status | `telnet IP:port` works, stable connection. | Choose stable network connection method. |
| hdc environment | `hdc -h` returns help information | Refer to [Environment Setup](#environment-setup). |

- Connection Steps

1. Enable wireless debugging in device settings.
2. Note the listening port number (PORT) displayed on device interface.
3. Connect via TCP (requires device IP and PORT):
   ```shell
   hdc tconn IP:PORT
   ```
   IP can be found in device settings, PORT is from step 2.4. To view connected devices, execute the following command:

   ```shell
   hdc list targets
   ```

   A return value in the format of IP:PORT indicates a successful connection.

5. To disable TCP connection mode, you can turn off the wireless debugging switch on the device.

#### Remote Connection Scenario

A remote connection scenario refers to a client connecting to a server over a network, where the client and server run on different 2-in-1 devices, and the server connects to the target device.
The remote connection is illustrated below:

![Remote Connection Structure](./figures/hdc_image_004.PNG)

The hdc client runs on 2-in-1 Device 1, while the hdc server runs on 2-in-1 Device 2, which connects to the target device.

1. Connection Commands

   | Command | Description |
   | -------- | -------- |
   | -s | Specifies the network listening parameters for the current server process. |

   The `-s` parameter is used for remote connections to specify the server's network parameters, including the IP address and port number. This setting is only valid during the execution of the current command. The command format is as follows:

   ```shell
   hdc -s [ip]:[port] [command]
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | ip | Specifies the listening IP address, supporting both IPv4 and IPv6. |
   | port | Specifies the listening port, range: 1–65535. |
   | command | Commands supported by hdc. |

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | Connect server failed | Failed to establish a connection with the server process. |
   | -s content port incorrect. | The port number exceeds the allowable range (1–65535). |

   **Usage Example:**

   ```shell
   # In an environment where a server process already exists with network listening parameters set to 127.0.0.1:8710, execute the device query command
   hdc -s 127.0.0.1:8710 list targets
   ```

   > **Note:**
   >
   > When the `-s` parameter is explicitly used in the command line to specify the server port, the system will ignore the port settings defined in the `OHOS_HDC_SERVER_PORT` environment variable.

2. Connection Steps

   i. Server Configuration

      After connecting the server to the corresponding HDC device via USB, execute the following commands:

      ```shell
      hdc kill          // Terminate the local hdc service
      hdc -s IP:8710 -m // Start the network-forwarded hdc service
                        // Here, IP is the server's own IP (queryable via `ipconfig` on Windows or `ifconfig` on Unix systems)
                        // 8710 is the default port number, which can be changed to another port (e.g., 18710)
                        // After startup, the server will print logs
      ```

   ii. Client Connection

      Ensure the client can reach the server's IP address. Once confirmed, execute the following command:

      ```shell
      hdc -s IP:8710 [command] // Here, IP is the server's IP, and 8710 is the port number set in the server startup step.
                              // If the port number was changed, update it here accordingly.
                              // `command` can be any valid hdc command, such as `list targets`.
      ```

### Switching Between USB Debugging and Wireless Debugging

The following commands are used for connection mode switching:

Currently, it is recommended to control the connection channel's activation and deactivation via the USB debugging and wireless debugging switches on the device.

| Command | Description |
| -------- | -------- |
| tmode usb | This command is deprecated and does not perform any actual device connection channel operations. Use the USB debugging switch in the device settings instead. |
| tmode port [port-number] | Opens the device's network connection channel: The device's daemon process will restart, and any existing USB connections will be interrupted, requiring reconnection. |
| tmode port close | Closes the device's network connection channel: The device's daemon process will restart, and any existing USB connections will be interrupted, requiring reconnection. |
| tconn [IP]:[port] [-remove] | Connects to the specified device using "IP:port". Use the `-remove` parameter to disconnect. |

1. To open the device's network connection channel, use the following command format:

   ```shell
   hdc tmode port [port-number]
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | port-number | The network port number for listening, range: 1–65535. |

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | Set device run mode successful. | Successfully opened. |
   | [Fail]ExecuteCommand need connect-key | Failed to open. No devices in the device list; unable to open the wireless debugging channel. |
   | [Fail]Incorrect port range | The port number exceeds the allowable range (1–65535). |

   **Usage Example:**

   ```shell
   hdc tmode port 1234
   ```

   > **Note:**
   >
   > Before switching, ensure the following conditions are met: The remote device and the local 2-in-1 device are on the same network, and the 2-in-1 device can ping the remote device's IP. If these conditions are not met, do not use this command for switching.
   > After execution, the remote daemon process will exit and restart, and USB connections will be interrupted, requiring reconnection.

2. To close the device's network connection channel, use the following command format:

   ```shell
   hdc tmode port close
   ```

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | [Fail]ExecuteCommand need connect-key | No devices in the device list; unable to execute the command. |

   **Usage Example:**

   ```shell
   hdc tmode port close
   ```

   > **Note:**
   >
   > After execution, the remote daemon process will exit and restart, and USB connections will be interrupted, requiring reconnection.

3. To connect to a specified device via TCP, use the following command format:

   ```shell
   hdc tconn [IP]:[port] [-remove]
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | [IP]:[port]  | The device's IP address and port number. |
   | -remove | Optional parameter to disconnect the specified device. |

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | Connect OK | Connection successful. |
   | [Info]Target is connected, repeat opration | The device is already connected. |
   | [Fail]Connect failed | Connection failed. |

   **Usage Example:**

   ```shell
   hdc tconn 192.168.0.1:8888
   hdc tconn 192.168.0.1:8888 -remove  // Disconnect the specified network device
   ```

## Executing Interactive Commands

The command format is as follows:

```shell
hdc shell [-b bundlename] [command]
```

**Parameters:**

| Parameter | Description |
| -------- | -------- |
| \[-b _bundlename_] | Specifies the debuggable application package name to execute commands in its data directory in non-interactive mode.<br>This parameter currently only supports non-interactive command execution and does not support entering an interactive shell session by omitting the `command` parameter. If this parameter is not specified, the default execution path is the system root directory. |
| \[command] | A single command to be executed on the device. The supported commands vary by system type or version. Use `hdc shell ls /system/bin` to view the list of supported commands. Many commands are provided by [toybox](./cj-toybox.md). Use `hdc shell toybox --help` for command help.<br>If this parameter is omitted, hdc will start an interactive shell session where developers can input commands such as `ls`, `cd`, and `pwd`. |

**Return Values:**

| Return Value | Description |
| -------- | -------- |
| Interactive command output | See other interactive command outputs for details. |
| /bin/sh: XXX : inaccessible or not found | Unsupported interactive command. |
| \[Fail]Specific failure message | Execution failed. Refer to the [hdc error codes section](#hdc-error-codes). |

**Usage Examples:**

```shell
# Enter interactive mode to execute commands
hdc shell

# Execute commands in non-interactive mode
hdc shell ps -ef

# Query all available commands
hdc shell help -a

# Execute commands in the specified application's data directory in non-interactive mode (supports `touch`, `rm`, `ls`, `stat`, `cat`, and `mkdir`).
hdc shell -b com.example.myapplication ls data/storage/el2/base/
```

> **Note:**
>
> When using the `[-b bundlename]` parameter to specify a package name, ensure the following: The installed application with the specified package name is "signed with a debug certificate." For details on applying for a debug certificate and signing, refer to: [Apply for Debug Certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178).

## Application Management

| Command | Description |
| -------- | -------- |
| install src | Installs the specified application file. |
| uninstall packageName | Uninstalls the specified application package. |

1. To install an APP package, use the following command format:

   ```shell
   hdc install [-r|-s] src
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | src| The filename of the application installation package. |
   | -r | Replaces an existing application (.hap). |
   | -s | Installs a shared package (.hsp). |

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | AppMod finish | On success, returns installation information and "AppMod finish." |
   | Specific installation failure reason | On failure, returns the specific installation failure message. |

   **Usage Example:**

   To install the `example.hap` package:

   ```shell
   hdc install E:\example.hap
   ```

2. To uninstall an application, use the following command format:

   ```shell
   hdc uninstall [-k|-s] packageName
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | packageName | The application installation package. |
   | -k | Retains the /data and /cache directories. |
   | -s | Uninstalls a shared package. |

   **Return Values:**

   | Return Value | Description |
   | -------- | -------- |
   | AppMod finish | On success, returns uninstallation information and "AppMod finish." |
   | Specific uninstallation failure reason | On failure, returns the specific uninstallation failure message. |

   **Usage Example:**

   To uninstall the `com.example.hello` package:

   ```shell
   hdc uninstall com.example.hello
   ```

## File Transfer

| Command | Description |
| -------- | -------- |
| file send localpath remotepath | Sends a file from the local machine to the remote device. |
| file recv remotepath localpath | Receives a file from the remote device to the local machine. |

1. To send a file from the local machine to the remote device, use the following command format:

   ```shell
   hdc file send [-a|-sync|-z|-m|-b bundlename] localpath remotepath
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | localpath | Local file path to be sent. |
   | remotepath | Remote file path to receive. |
   | -a | Preserve file timestamps. |
   | -sync | Only transfer files with updated mtime. |
   | -z | Compress transfer using LZ4 format (unavailable feature, do not use). |
   | -m | Synchronize file DAC permissions, uid, gid, and MAC permissions during transfer. |
   | -b | Transfer files from the specified debuggable application's data directory. |
   | bundlename | Package name of the debuggable application. |

   **Return Value:**

   Returns success information if file transfer succeeds; returns detailed failure information if transfer fails.

   **Usage:**

   ```shell
   hdc file send E:\example.txt /data/local/tmp/example.txt
   hdc file send -b com.example.myapplication a.txt data/storage/el2/base/b.txt
   ```

   > **Note:**
   >
   > In the usage example, `hdc file send -b com.example.myapplication a.txt data/storage/el2/base/b.txt` specifies the `-b` parameter to transfer file `a.txt` from the local current directory to the application data directory of the package `com.example.myapplication`, saving it under the relative path `data/storage/el2/base/` and renaming it to `b.txt`.
   >
   > When using the `[-b bundlename]` parameter to specify a package name, the following condition must be met: the installed application with the specified package name must be "signed with a debug certificate." For details on applying for a debug certificate and signing, refer to: [Apply for Debug Certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178).

2. Send files from a remote device to the local machine. Command format:

   ```shell
   hdc file recv [-a|-sync|-z|-m|-b bundlename] remotepath localpath
   ```

   **Parameters:**

   | Parameter | Description |
   | -------- | -------- |
   | localpath | Local file path to receive. |
   | remotepath | Remote file path to send. |
   | -a | Preserve file timestamps. |
   | -sync | Only transfer files with updated mtime. |
   | -z | Compress transfer using LZ4 format (unavailable feature, do not use). |
   | -m | Synchronize file DAC permissions, uid, gid, and MAC permissions during transfer. |
   | -b | Transfer files from the specified debuggable application's data directory. |
   | bundlename | Package name of the debuggable application. |

   **Return Value:**

   Returns success information if file transfer succeeds; returns detailed failure information if transfer fails.

   **Usage:**

   ```shell
   hdc file recv /data/local/tmp/a.txt ./a.txt
   hdc file recv -b com.example.myapplication data/storage/el2/base/b.txt a.txt
   ```

   > **Note:**
   >
   > In the usage example, `hdc file recv -b com.example.myapplication data/storage/el2/base/b.txt a.txt` specifies the `-b` parameter to transfer file `b.txt` from the relative path `data/storage/el2/base/` of the debuggable application `com.example.myapplication` to the local current directory, renaming it to `a.txt`.
   >
   > When using the `[-b bundlename]` parameter to specify a package name, the following condition must be met: the installed application with the specified package name must be "signed with a debug certificate." For details on applying for a debug certificate and signing, refer to: [Apply for Debug Certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178).

## Port Forwarding

| Command | Description |
| -------- | -------- |
| fport ls | List all port forwarding tasks. |
| fport localnode remotenode | Set up a forward port forwarding task: listen on "host port," forward requests to "device port." |
| rport remotenode localnode | Set up a reverse port forwarding task: listen on "device port," forward requests to "host port." |
| fport rm taskstr | Remove the specified port forwarding task. |

Port forwarding types supported by 2in1 port: tcp.

Port forwarding types supported by device: tcp, dev, localabstract, localfilesystem, jdwp, ark.

1. List all port forwarding tasks. Command format:

   ```shell
   hdc fport ls
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | tcp:1234 tcp:1080 [Forward] | Forward port forwarding task |
   | tcp:2080 tcp:2345 [Reverse] | Reverse port forwarding task |
   | [empty] | No port forwarding tasks |

   **Usage:**

   ```shell
   hdc fport ls
   ```

2. Set up a forward port forwarding task. Executing this command will set up a task to forward data from the specified "host port" to the "device port." Command format:

   ```shell
   hdc fport localnode remotenode
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Forwardport result:OK | Port forwarding task set up successfully. |
   | [Fail]Incorrect forward command | Port forwarding task setup failed due to incorrect parameters. |
   | [Fail]TCP Port listen failed at XXXX | Port forwarding task setup failed due to occupied local forwarding port. |

   **Usage:**

   ```shell
   hdc fport tcp:1234 tcp:1080
   ```

3. Set up a reverse port forwarding task. Executing this command will set up a task to forward data from the specified "device port" to the "host port." Command format:

   ```shell
   hdc rport remotenode localnode
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Forwardport result:OK | Port forwarding task set up successfully. |
   | [Fail]Incorrect forward command | Port forwarding task setup failed due to incorrect parameters. |
   | [Fail]TCP Port listen failed at XXXX | Port forwarding task setup failed due to occupied local forwarding port. |

   **Usage:**

   ```shell
   hdc rport tcp:1234 tcp:1080
   ```

4. Remove a port forwarding task. Executing this command will delete the specified forwarding task. Command format:

   ```shell
   hdc fport rm taskstr
   ```

   **Parameter:**

   | Parameter | Description |
   | -------- | -------- |
   | taskstr | Port forwarding task, formatted as tcp:XXXX tcp:XXXX. |

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Remove forward ruler success, ruler:tcp:XXXX tcp:XXXX | Port forwarding task removed successfully. |
   | [Fail]Remove forward ruler failed, ruler is not exist tcp:XXXX tcp:XXXX | Port forwarding task removal failed; specified task does not exist. |

   **Usage:**

   ```shell
   hdc fport rm tcp:1234 tcp:1080
   ```

## Service Process Management

| Command | Description |
| -------- | -------- |
| start [-r] | Start the hdc service process. Use `-r` to trigger a restart. |
| kill [-r] | Terminate the hdc service process. Use `-r` to trigger a restart. |
| -p | Bypass service process query for faster command execution. |
| -m | Start the service process in foreground mode. |

1. Start the hdc service process. Command format:

   ```shell
   hdc start [-r]
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | No return value | Service process started successfully |

   **Usage:**

   ```shell
   hdc start
   hdc start -r // Restart the service process if already running
   ```

   > **Note:**
   >
   > When starting the hdc service process, if the system does not detect a running service process, the log level priority is as follows: if both the `-l` parameter and the `OHOS_HDC_LOG_LEVEL` environment variable are specified, the environment variable takes precedence; if only `-l` is specified, it is used; if neither is specified, the service process starts with the default `LOG_INFO` level.

2. Terminate the hdc service process. Command format:

   ```shell
   hdc kill [-r]
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Kill server finish | Service process terminated successfully |
   | [Fail]Detailed failure information | Service process termination failed |

   **Usage:**

   ```shell
   hdc kill
   hdc kill -r  // Restart and terminate the service process
   ```

3. Bypass service process query for faster command execution. Command format:

   ```shell
   hdc -p [command]
   ```

   **Parameter:**

   | Parameter | Description |
   | -------- | -------- |
   | command | Command supported by hdc |

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Connect server failed | Failed to establish connection with the service process |

   **Usage:**

   ```shell
   # Start the background service process
   hdc start
   # Skip process query and execute command directly
   hdc -p list targets
   ```

   > **Note:**
   >
   > If the `-p` parameter is not specified when executing a command, the client first checks for a running service process locally. If none is detected, it automatically starts the service process and establishes a connection to relay the command; if a running service process is detected, the client directly connects to it and issues the command.

4. Start the service process in foreground mode. Command format:

   ```shell
   hdc -m
   ```

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Initial failed | Service process initialization failed. |
   | [I][1970-01-01 00:00:00.000][abcd][session.cpp:25] Program running. Ver: X.X.Xa Pid:12345 | Logs at the specified level, showing service process activity. |

   **Usage:**

   ```shell
   # Specify network listening parameters and start the service process
   hdc -s 127.0.0.1:8710 -m
   ```

   > **Note:**
   >
   > When starting in foreground mode, the `-s` parameter can be used to specify network listening parameters. If neither `-s` nor the `OHOS_HDC_SERVER_PORT` environment variable is configured, the default parameters `127.0.0.1:8710` are used.
   > In foreground mode, the default log level is `LOG_DEBUG`. Use the `-l` parameter to adjust the log level.
   > Only one service process instance is allowed in the runtime environment. If a background service process is already active, starting a new instance in foreground mode will fail.

## Device Operations

| Command | Description |
| -------- | -------- |
| hilog [-h] | Print device-side log information. Use `hdc hilog -h` to view supported parameters. |
| jpid | Display PIDs of all applications with JDWP debugging enabled on the device. |
| track-jpid [-a\|-p] | Real-time display of PIDs and application names with JDWP debugging enabled. Without parameters, only debug applications are shown; `-a` shows both debug and release applications; `-p` hides debug/release labels. |
| target boot [-bootloader\|-recovery] | Reboot the target device. Use `-bootloader` to enter fastboot mode or `-recovery` to enter recovery mode. |
| target boot [MODE] | Reboot the target device into the specified mode, where MODE is a parameter supported by `/bin/begetctl` reboot. |
| <!--DelRow--> target mount | Mount the system partition in read-write mode (requires rooted device). |
| <!--DelRow--> smode [-r] | Grant root permissions to the device-side hdc service process. Use `-r` to revoke (requires rooted device). |

1. Print device-side log information. Command format:

   ```shell
   hdc hilog [-h]
   ```

   **Parameter:**

   | Parameter | Description |
   | -------- | -------- |
   | [-h] | Parameters supported by hilog. Use `hdc hilog -h` to view the list. |

   **Return Value:**

   | Return Value | Description |
   | -------- | -------- |
   | Detailed information | Captured log information. |
```**Usage Instructions:**

```shell
hdc hilog
```

2. Display the PIDs of all processes on the device that have enabled the JDWP debugging protocol. The command format is as follows:

```shell
hdc jpid
```

**Return Values:**

| Return Value | Description |
| ------------ | ----------- |
| List of PIDs | PIDs of applications with the JDWP debugging protocol enabled. |
| [empty]      | No processes with the JDWP debugging protocol enabled. |

**Usage Instructions:**

```shell
hdc jpid
```

3. Display the PIDs and application names of processes with the JDWP debugging protocol enabled in real-time. The command format is as follows:

```shell
track-jpid [-a|-p]
```

**Parameters:**

| Parameter | Description |
| --------- | ----------- |
| No parameter | Displays only the process numbers and package/process names of debug applications. |
| -a        | Displays process numbers and package/process names of both debug and release applications. |
| -p        | Displays process numbers and package/process names of both debug and release applications but omits the debug/release labels. |

**Return Values:**

| Return Value | Description |
| ------------ | ----------- |
| List of process numbers and package/process names | - |
| [empty]      | When no parameter is used, indicates no debug applications with the JDWP debugging protocol enabled. When -a or -p is used, indicates no processes with the JDWP debugging protocol enabled. |

**Usage Instructions:**

```shell
hdc track-jpid
```

4. Reboot the target device. The command format is as follows:

```shell
target boot [-bootloader|-recovery]
target boot [MODE]
```

**Parameters:**

| Parameter | Description |
| --------- | ----------- |
| No parameter | Reboots the device. |
| -bootloader | Reboots into fastboot mode. |
| -recovery  | Reboots into recovery mode. |
| MODE       | Reboots into MODE mode, where MODE is a parameter supported by the `/bin/begetctl` command for reboot.<br>Use `hdc shell "/bin/begetctl -h \| grep reboot"` to view supported parameters. |

**Usage Instructions:**

```shell
hdc target boot -bootloader // Reboot into fastboot mode
hdc target boot -recovery  // Reboot into recovery mode
hdc target boot shutdown  // Shut down the device
```

<!--Del-->
5. Mount the system partition in read-write mode. The command format is as follows:

```shell
hdc target mount
```

**Return Values:**

| Return Value | Description |
| :---------- | :---------- |
| Mount finish | Mount successful. |
| [Fail]Mount failed | Mount failed. |

**Usage Instructions:**

```shell
hdc target mount
```

> **Note:**
>
> This command is supported only on rooted devices. Modifying the system partition carries risks; use with caution.

6. Grant root permissions to the hdc background service process on the device. The command format is as follows:

```shell
hdc smode [-r]
```

**Return Values:**

| Return Value | Description |
| :---------- | :---------- |
| No return value | Permission granted successfully. |
| [Fail]Detailed error message | Permission grant failed. |

**Usage Instructions:**

```shell
hdc smode
hdc smode -r  // Revoke root permissions
```

> **Note:**
>
> This command is supported only on rooted devices.
<!--DelEnd-->

## Security-Related Commands

| Command | Description |
| ------- | ----------- |
| keygen FILE | Generates a new key pair and saves the private and public keys to FILE and FILE.pub, respectively, where FILE is a customizable filename. |

1. Generate a new key pair. The command format is as follows:

```shell
hdc keygen FILE
```

**Parameters:**

| Parameter | Description |
| --------- | ----------- |
| FILE      | Custom filename. |

**Usage Instructions:**

```shell
hdc keygen key // Generates key and key.pub files in the current directory
```

## Query Version Number

| Command | Description |
| ------- | ----------- |
| -v/version | Prints hdc version information. |
| checkserver | Retrieves client and server process versions. |

1. Display hdc version information. The command format is as follows:

```shell
hdc -v/version
```

**Return Values:**

| Return Value | Description |
| ------------ | ----------- |
| Ver:X.X.Xa   | Version information of hdc (SDK). |

**Usage Instructions:**

```shell
hdc -v or hdc version
```

2. Retrieve client and server process versions. The command format is as follows:

```shell
hdc checkserver
```

**Return Values:**

| Return Value | Description |
| ------------ | ----------- |
| Client version: Ver:X.X.Xa, Server version: Ver:X.X.Xa | Version numbers of the client and server processes. |

**Usage Instructions:**

```shell
hdc checkserver
```

## hdc Debug Logs

### Server-Side Logs

#### Specify Runtime Log Level

The default runtime log level for hdc is LOG_INFO. The command format is as follows:

```shell
hdc -l [level] [command]
```

**Parameters:**

| Parameter | Description |
| --------- | ----------- |
| [level]   | Specifies the runtime log level:<br/>0: LOG_OFF<br/>1: LOG_FATAL<br/>2: LOG_WARN<br/>3: LOG_INFO<br/>4: LOG_DEBUG<br/>5: LOG_ALL<br/>6: LOG_LIBUSB. |
| command   | Any hdc-supported command. |

> **Note:**
>
> When the runtime log level is set to 6 (LOG_LIBUSB), incremental logs related to libusb will be activated. These logs are highly detailed and voluminous, aiding in precise diagnosis of USB-related anomalies in the server process. USB operations are primarily handled by the server process, so only the server process can print incremental logs. The client-side logs will contain almost no incremental log information.
> Specifying the runtime log level applies only to the current process (including the client and server processes) and cannot change the log level of existing processes.

**Return Values:**

| Return Value | Description |
| ------------ | ----------- |
| Command execution output | Refer to the return values of the corresponding command. |
| Log information | Logs printed at the specified runtime level. |

**Usage Instructions:**

To print LOG_DEBUG level logs on the client side while executing `shell ls`, use the following command:

```shell
hdc -l 5 shell ls
```

To start the server process in foreground mode with LOG_LIBUSB level logs, use the following command:

```shell
hdc kill && hdc -l 6 -m
```

> **Note:**
> The `-m` parameter starts the server process in foreground mode, allowing direct observation of log output. Press Ctrl+C to exit the process.

To start the server process in background mode with LOG_LIBUSB level logs, use the following command:

```shell
hdc kill && hdc -l 6 start
```

> **Note:**
> In background mode, logs can be observed in hdc.log. The log path is described in the **Log Retrieval** section.

#### Log Retrieval

Execute the following commands to enable log retrieval:

```shell
hdc kill
hdc -l5 start
```

The full log storage paths are as follows:

| Platform | Path | Remarks |
| -------- | ---- | ------- |
| Windows | %temp%\hdc.log | Actual path may vary; replace the username variable.<br/>Example: C:\Users\Username\AppData\Local\Temp\hdc.log. |
| Linux | /tmp/hdc.log | - |
| macOS | $TMPDIR/hdc.log | - |

Log-related environment variables:

| Environment Variable | Default Value | Description |
| -------------------- | ------------- | ----------- |
| OHOS_HDC_LOG_LEVEL | 5 | Configures the log level for the server process. For details, refer to the [Server-Side Logs](#server-side-logs) section on specifying runtime log levels. |

Environment variable configuration methods:

The following example demonstrates how to set the OHOS_HDC_LOG_LEVEL environment variable to 5.

| OS | Configuration Method |
| -- | -------------------- |
| Windows | Go to **This PC > Properties > Advanced system settings > Advanced > Environment Variables**, add OHOS_HDC_LOG_LEVEL with value 5, and click OK. Restart the command line or any OpenHarmony SDK software to apply the changes. |
| Linux | Append `export OHOS_HDC_LOG_LEVEL=5` to ~/.bash_profile, save, and run `source ~/.bash_profile` to apply. |
| macOS | Append `export OHOS_HDC_LOG_LEVEL=5` to ~/.zshrc, save, and run `source ~/.zshrc` to apply. Restart the command line or any OpenHarmony SDK software to apply the changes. |

### Device-Side Logs

Enable the hilog tool to retrieve logs using the following commands:

```shell
hdc shell hilog -w start                              // Enable hilog disk logging
hdc shell ls /data/log/hilog                          // View saved hilog logs
hdc file recv /data/log/hilog                         // Retrieve saved hilog logs (including kernel logs)
```

## Common Issues

### Device Not Recognized

**Symptom:**

Running `hdc list targets` returns `[empty]`.**Possible Causes & Solutions:**

You can troubleshoot using the following methods.

- **Scenario 1:** Check if the HDC device is displayed in Device Manager.

  **Windows Environment:**  
  In `Device Manager` > `Universal Serial Bus devices`, check if `HDC Device` (single-port device) or `HDC Interface` (composite-port device) is displayed.

  **Linux Environment:**  
  Execute `lsusb` in the command line and check the output for `HDC Device` (single-port device) or `HDC Interface` (composite-port device).

  **macOS Environment:**  
  Use `System Information` or `System Profiler` to view USB devices by following these steps:
    1. Hold the Option key and click the menu.
    2. Select `System Information` or `System Profiler`.
    3. In the window that appears, select `USB` on the left.
    4. Check the device tree for `HDC Device` (single-port device) or `HDC Interface` (composite-port device).

  **Possible Solutions:**  
  If the HDC device is not displayed in any of the above environments, it indicates the device is unrecognized. Try the following methods based on the actual scenario:
    - Use another physical USB port.
    - Replace the USB data cable.
    - Debug using another computer.
    - Enable USB debugging mode on the device.
    - Click "Allow debugging" if a pop-up appears on the device.
    - If TCP mode is available, execute `hdc tmode usb` to restore USB connection.
    - Reset the device to factory settings.

- **Scenario 2:** The USB device is present, but the driver is corrupted, showing an "HDC Device" ⚠ warning icon.

  **Description:** This issue is common in Windows environments. In `Device Manager` > `Universal Serial Bus devices`, `HDC Device` appears with a yellow warning icon, and the description states the device cannot function properly. Try reinstalling the driver. If reinstalling doesn’t resolve the issue, try replacing the USB data cable/dock/port.

  **Driver Reinstallation Method:**  
    1. Open `Device Manager`, right-click the `HDC Device` with the warning icon.
    2. Click `Update driver` in the menu.
    3. In the prompt window (Step 1/3), select `Browse my computer for drivers`.
    4. In the prompt window (Step 2/3), select `Let me pick from a list of available drivers on my computer`.
    5. In the prompt window (Step 3/3), uncheck `Show compatible hardware`, select Manufacturer: `WinUSB Device`, Model: `WinUSB Device`, then click `Next`.

- **Scenario 3:** `[Fail]Failed to communicate with daemon` appears when connecting the device.

  **Description:** Executing hdc-related commands in the command line fails with `[Fail]Failed to communicate with daemon`.

  **Possible Causes & Troubleshooting:**  
    - **hdc or SDK version mismatch with the device:** If the device is updated to the latest version, update hdc or SDK tools to the latest version.
    - **Port conflict:**  
      Commonly occurs when hdc and hdc_std use the same port (OHOS_HDC_SERVER_PORT). If not set, the default port 8710 is used, which may still conflict. Ensure only one is running. Other software occupying the hdc default port can also cause this issue.

- **Scenario 4:** `Connect server failed` appears when connecting the device.

  **Possible Causes:**  
    - **Port occupation:**  
      **Solutions:**  
        1. Check for processes with built-in hdc (e.g., DevEco Studio, DevEco Testing). Close these applications before executing hdc commands.
        2. Query HDC port status.  
           For example, if OHOS_HDC_SERVER_PORT is set to 8710, use the following commands:  
           **Unix:**  
           ```shell
           netstat -an |grep 8710
           ```  
           **Windows:**  
           ```shell
           netstat -an |findstr 8710
           ```  
           If port occupation is detected, close the conflicting process or change the OHOS_HDC_SERVER_PORT environment variable to another port.  
        3. Check for other versions of hdc server running.  
           **Windows:**  
           Use `Task Manager` > `Details` to locate the hdc.exe process. Right-click to open the file location and verify if it matches the hdc file path in the configured environment variables. If not, terminate the hdc.exe process (via `hdc kill` or Task Manager) and rerun the hdc command.  
           **Unix:**  
           Use `ps -ef |grep hdc` to locate the hdc server process. Verify if the process path matches the hdc file path in the configured environment variables. If not, terminate the hdc process (via `hdc kill` or `kill -9 [PID]`) and rerun the hdc command.  

    - **Registry anomaly:**  
      **Solution:** Clean the registry by following these steps:  
        1. Press `Win` + `R`, type `regedit`, and press Enter.  
        2. Enter the following path in the registry address bar and press Enter:  
           ```shell
           Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{88bae032-5a81-49f0-bc3d-a4ff138216d6}
           ```  
        3. Locate the `UpperFilters` key, right-click to modify, **back up** and clear its value data (restore if clearing doesn’t resolve the issue).  
        4. Refresh Device Manager/replug USB port/restart the computer.  

<!--Del-->
**Linux System: hdc Cannot Find Devices Without Root Permissions**  

For Linux environments, you can enable USB device operation permissions for non-root users as follows:  

- **(Temporary Permissions) Maximize USB Device Permissions:**  
  ```shell
  sudo chmod -R 777 /dev/bus/usb/
  ```  

- **(Permanent Permissions) Permanently Modify USB Device Permissions:**  
  1. Use `lsusb` to identify the USB device's vendorID and productID.  
  2. Create a new udev rule.  
     Edit the udev loading rule, replacing default values with the device's "idVendor" and "idProduct".  
     `MODE="0666"` sets USB device permissions; `GROUP` specifies the user group (ensure the current user is in this group):  
     ```shell
     sudo vim /etc/udev/rules.d/90-myusb.rules
     SUBSYSTEMS=="usb", ATTRS{idVendor}=="067b", ATTRS{idProduct}=="2303", GROUP="users", MODE="0666"
     ```  
  3. Restart the computer or reload udev rules:  
     ```shell
     sudo udevadm control --reload
     ```  

> **Note:**  
> **Enabling USB device permissions for non-root users** resolves hdc device detection issues in Linux environments. However, maximizing permissions **may pose security risks**. Developers should evaluate based on usage scenarios.  

<!--DelEnd-->

### hdc Fails to Run  

**Description:**  
Executing the hdc.exe/hdc binary file via the command line fails.  

**Possible Causes & Solutions:**  
- **Environment issues:**  
  - **Linux:** Recommended: Ubuntu 18.04 or later (64-bit). If `libc++.so` errors occur, use `ldd`/`readelf` to check library dependencies.  
  - **macOS:** Recommended: macOS 11 or later.  
  - **Windows:** Recommended: Windows 10/11 (64-bit). If older versions lack WinUSB libraries/drivers, use the Zadig tool to update. For composite devices, install the `libusb-win32` driver via Zadig. Details: [Zadig Link](https://github.com/pbatard/libwdi/releases).  

- **Incorrect execution method:** Use the command line to run hdc tools correctly, not by double-clicking the file.  

### General Troubleshooting Steps  
1. Execute `hdc list targets` to check the return value.  
2. Check `Device Manager` for `HDC Device`.  
3. Execute `hdc kill` to close the server, then execute `hdc -l5 start` to collect logs (hdc.log is located in the TEMP directory of the execution end; paths vary by platform. See [Server Logs](#server端日志)).  
4. Use hdc.log to identify issues.  

## hdc Error Codes  

### E003001 (Command Line) Invalid Bundle Name  

**Error Message:**  
`Invalid bundle name: _bundlename_`  

**Description:**  
The `bundlename` specified in `hdc shell [-b bundlename] [command]` is not an installed debuggable app bundle name, or the app directory does not exist.  

**Possible Causes:**  
- **Cause 1:** The specified app is not installed on the device.  
- **Cause 2:** The app is not built in debug mode.  
- **Cause 3:** The app is not running.  

**Steps:**  
- **Cause 1:** Confirm the app is installed.  
  a. Execute `hdc shell "bm dump -a | grep bundlename"`. Expected return: `bundlename`.  
  Example for `com.example.myapplication`:  
  ```shell
  hdc shell "bm dump -a | grep com.example.myapplication"
  ```  
  If installed, the output should be:  
  ```shell
  com.example.myapplication
  ```  
  b. If the app is debuggable but not installed, execute `hdc install [app_path]`.  
  c. If the app is a release build, specifying `bundlename` is unsupported.  

- **Cause 2:** Confirm the app is built in debug mode. Execute `hdc shell "bm dump -n bundlename | grep debug"`. Expected return:  
  ```shell
  "appProvisionType": "debug",
  ```  
  Example for `com.example.myapplication`:  
  ```shell
  hdc shell "bm dump -n com.example.myapplication | grep debug"
  ```  
  Debuggable apps require signing with a debug certificate. For details, see: [Apply for Debug Certificate](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugcert-0000001914263178).  

- **Cause 3:** Confirm the app is running.  
  a. Execute `hdc shell "mount |grep bundlename"` to check resource directory mounting.  
  Example for `com.example.myapplication`:  
  ```shell
  hdc shell "mount |grep com.example.myapplication"
  ```  
  If mounted, output will show the mount path (varies by device).  
  b. If unmounted, manually launch the app or use `aa` commands.  
  Example for `com.example.myapplication` (module: `EntryAbility`):  
  ```shell
  hdc shell aa start -b com.example.myapplication -a EntryAbility
  ```  
  For more details, see [aa Command Guide](./cj-aa-tool.md).  

### E003002 Unsupported Interactive Shell Command Option  

**Error Message:**  
`Unsupport interactive shell command option`  

**Description:**  
The `hdc shell [-b bundlename] [command]` command does not support interactive mode.  

**Possible Cause:**  
The `command` parameter is empty.  

**Solution:**  
Ensure the `command` parameter is not empty. For usage, see [Interactive Command Execution](#执行交互命令).  

### E003003 Unsupported Command Line Option  

**Error Message:**  
`Unsupported shell option: option`  

**Description:**  
The `hdc shell [-b bundlename] [command]` command includes an unsupported option (e.g., `-f`, `-B`; case-sensitive).  

**Solution:**  
Use supported options (e.g., `-b`).  

### E003004 Device Does Not Support This Command  

**Error Message:**  
`Device does not supported this shell command`  

**Description:**  
The device does not support the specified command.The command `hdc shell [-b bundlename] [command]` contains command-line parameters not supported by the device.

**Possible Causes:**

The device system version is too low and does not support the newly added command-line parameter functionality.

**Resolution Steps:**

Upgrade the device system to the latest version.

### E003005 (Command Line) Missing Parameter

**Error Message:**

The parameter is missing, correct your input by referring below: Usage

**Error Description:**

The `hdc shell [-b bundlename] [command]` command is missing required parameters when specifying options.

**Possible Causes:**

When the `-b` option is specified, the `bundlename` or `command` parameter is missing. For detailed parameter definitions, refer to [Interactive Command Execution Introduction](#执行交互命令).

**Resolution Steps:**

Ensure that both the `bundlename` and `command` parameters are not empty.

### E005101 (File Transfer) Invalid Bundle Name

**Error Message:**

Invalid bundle name: bundlename

**Error Description:**

The `bundlename` specified in the command `hdc file send/recv [-b bundlename] [localpath] [remotepath]` is not the name of an installed debuggable application, or the application directory does not exist.

**Possible Causes:**

Same as error code [E003001](#e003001-命令行指定的包名非法).

**Resolution Steps:**

Same as error code [E003001](#e003001-命令行指定的包名非法).

### E005102 Invalid Remote Path

**Error Message:**

Remote path: remotepath is invalid, it is out of the application directory.

**Error Description:**

For the command `hdc file send [-b bundlename] [localpath] [remotepath]`, the specified `remotepath` does not exist or exceeds the application data directory.

For the command `hdc file recv [-b bundlename] [remotepath] [localpath]`, the specified `remotepath` does not exist or exceeds the application data directory.

**Possible Causes:**

- Scenario 1: The path does not exist.
- Scenario 2: The `remotepath` parameter contains `..` navigation symbols, and the actual directory exceeds the root application data directory after navigation.

**Resolution Steps:**

Verify that the relative path specified by the `remotepath` parameter in the application data directory exists.

### E005003 (File Transfer) Missing Parameter

**Error Message:**

The parameter is missing, correct your input by referring below: Usage

**Error Description:**

The command `hdc file send [-b bundlename] [localpath] [remotepath]` is missing required parameters.

The command `hdc file recv [-b bundlename] [remotepath] [localpath]` is missing required parameters.

**Possible Causes:**

When the `-b` option is specified, the `bundlename`, `localpath`, or `remotepath` parameter is missing. For detailed parameter definitions, refer to [File Transfer Command Introduction](#文件传输).

**Resolution Steps:**

Ensure that the `bundlename`, `localpath`, and `remotepath` parameters are not empty.

### E005004 SDK or Device System Version Does Not Support the `-b` Option

**Error Message:**

SDK/Device ROM doesn't support -b option.

**Error Description:**

When using the `-b` option with the `hdc file send/recv` command, the hdc in the SDK or the device system version does not support this option.

**Possible Causes:**

- Scenario 1: When executing `hdc file send [-b bundlename] [localpath] [remotepath]`, the device system version does not support the `-b` option.
- Scenario 2: When executing `hdc file recv [-b bundlename] [remotepath] [localpath]`, the hdc in the SDK does not support the `-b` option.

**Resolution Steps:**

- Scenario 1: Upgrade to the latest system version.
- Scenario 2: Upgrade to the latest SDK version.