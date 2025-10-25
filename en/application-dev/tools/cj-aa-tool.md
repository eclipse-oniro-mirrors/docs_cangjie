# aa Tool

Ability assistant (abbreviated as aa) is a tool for launching applications and test cases, providing developers with basic application debugging and testing capabilities, such as starting application components, forcibly terminating processes, printing component-related information, etc.

## Environment Requirements

Before using this tool, developers need to first obtain the <!--Del-->[<!--DelEnd-->hdc tool<!--Del-->](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-toolchain-hdc-guide.md)<!--DelEnd--> and execute `hdc shell`.

The command descriptions in this document are based on an interactive command environment. If directly executing `hdc shell [aa command]`, the aa command must be wrapped in `""` to ensure parameters are correctly recognized. Examples:

```bash
# Launch command
hdc shell "aa start -A ohos.want.action.viewData -U 'https://www.example.com'"

# Application debugging/tuning command
hdc shell "aa process -b com.example.myapplication -a EntryAbility -p perf-cmd"
```

## aa Tool Command List

| Command | Description |
|--------|--------|
| -h/help | Help command. Used to query supported aa command information. |
| start | Launch command. Used to start an application component, which can be a Stage model UIAbility or ServiceExtensionAbility component. The target component's exported tag in the configuration file must not be set to false. |
| force-stop | Force-stop process command. Forcibly terminates a process by bundleName. |
| test | Test framework launch command. Starts the test framework based on provided parameters. |
| attach | Debug mode entry command. Puts a specified application into debug mode by bundleName. |
| detach | Debug mode exit command. Takes a specified application out of debug mode by bundleName. |
| appdebug | Debug wait command. Used to set/unset an application's debug wait state, and retrieve package names and persistent information of applications in debug wait state. Debug wait state only applies to debug-type applications. The appdebug set command only affects a single application; repeated settings will overwrite previous package names and persistent states. |
| process | Application debugging/tuning command. Used for application debugging or tuning. IDEs use this command to integrate debugging and tuning tools. |

## Help Command (help)

```bash
# Display help information
aa help
```

## Start Command (start)

Launches an application component, which can be a Stage model UIAbility or ServiceExtensionAbility component. The target component's exported tag in the configuration file must not be set to false.

```bash
# Explicitly launch Ability
aa start [-d <deviceId>] [-a <abilityName> -b <bundleName>] [-m <moduleName>] [-D] [-R] [-S] [--pi <key> <integer-value>] [--pb <key> <bool-value: true/false/t/f case insensitive>] [--ps <key> <value>] [--psn <key>] [--wl <windowLeft>] [--wt <windowTop>] [--wh <windowHeight>] [--ww <windowWidth>] [-p <perf-cmd>]

# Implicitly launch Ability. If no parameters are provided, the launch will fail.
aa start [-d <deviceId>] [-U <URI>] [-t <type>] [-A <action>] [-e <entity>] [-D] [-R] [--pi <key> <integer-value>] [--pb <key> <bool-value: true/false/t/f case insensitive>] [--ps <key> <value>] [--psn <key>] [--wl <windowLeft>] [--wt <windowTop>] [--wh <windowHeight>] [--ww <windowWidth>] [-p <perf-cmd>]
```

**Start Command Parameter List**

| Parameter | Description |
| -------- |-------------------|
| -h/--help | Help information. |
| -d | Optional, deviceId. |
| -a | Optional, abilityName. |
| -b | Optional, bundleName. |
| -m | Optional, moduleName. |
| -U | Optional, URI. |
| -A | Optional, action. |
| -e | Optional, entity. |
| -t | Optional, type. |
| --pi | Optional, integer key-value pair. |
| --pb | Optional, boolean key-value pair. |
| --ps | Optional, string key-value pair. |
| --psn | Optional, empty string keyword. |
| --wl | Optional, windowLeft (left margin in px).<br>**Constraint:**<br>Only effective when the 2-in-1 device is in developer mode and the launched application uses debug signing.|
| --wt | Optional, windowTop (top margin in px).<br>**Constraint:**<br>Only effective when the 2-in-1 device is in developer mode and the launched application uses debug signing.|
| --wh | Optional, windowHeight (height in px).<br>**Constraint:**<br>Only effective when the 2-in-1 device is in developer mode and the launched application uses debug signing.|
| --ww | Optional, windowWidth (width in px).<br>**Constraint:**<br>Only effective when the 2-in-1 device is in developer mode and the launched application uses debug signing.|
| -R | Optional, enables multi-thread error detection during debugging. Presence indicates enabled; absence indicates disabled.|
| -S | Optional, enters application sandbox during debugging. Presence indicates enabled; absence indicates disabled. |
| -D | Optional, debug mode. |
| -p | Optional, tuning command. Customized by the caller. |

**Return Value:**

On successful launch: "start ability successfully." On failure: "error: failed to start ability." with corresponding error information.

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10103001 | Failed to verify the visibility of the target ability. |
| 10104001 | The specified ability does not exist. |
| 10105001 | Failed to connect to the ability service. |
| 10105002 | Failed to obtain ability information. |
| 10106002 | The target application does not support debug mode. |
| 10100101 | Failed to obtain application information. |
| 10100102 | The aa start command cannot be used to launch a UIExtensionAbility. |
| 10103101 | Failed to find a matching application for implicit launch. |
| 10103102 | The passed appCloneIndex is invalid. |
| 10106101 | The current ability will be placed in the queue to wait for the previous ability to finish launching. |
| 10106102 | The device screen is locked during the application launch. |
| 10106103 | The target application is an expired crowdtesting application. |
| 10106105 | The target application is under control. |
| 10106106 | The target application is managed by EDM. |
| 10106107 | The current device does not support using window options. |
| 10107102 | Permission verification failed for the specified process. |
| 10108101 | An internal error occurs while attempting to launch the ability. |

**Example:**

Example of implicitly launching an Ability.

> **Note:**
>
> This example only demonstrates partial field usage. For detailed Ability matching rules, refer to [Explicit Want vs. Implicit Want Matching Rules](../application-models/cj-explicit-implicit-want-mappings.md).

- **Target Application:**

    Modify module.json5 configuration to configure uris for the target Ability.

    ```json
    {
      "name": "TargetAbility",
      // ......
      "exported": true,
      "skills": [
        {
          "actions":[
            "ohos.want.action.viewData"
          ],
          "uris":[
            {
              "scheme": "myscheme",
              "host": "www.test.com",
              "port": "8080",
              "path": "path",
            }
          ]
        }
      ]
    }
    ```

- **Launcher Application:**

    Implicitly launch Ability.

    - To launch the application page, use the -U command:

        ```bash
        aa start -U myscheme://www.test.com:8080/path
        ```

    - To include parameters, use:

        ```bash
        aa start -U myscheme://www.test.com:8080/path --pi paramNumber 1 --pb paramBoolean true --ps paramString teststring  --psn paramNullString
        ```

        UIAbility parameter retrieval example:

        <!--compile-->
        ```cangjie
        import kit.AbilityKit.*
        import ohos.base.*
        import ohos.ability.*

        class TargetAbility <:  Ability {
          public override func onCreate(want:Want, launchParam: LaunchParam): Unit {
            hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
            let paramNumber = want.parameters.paramNumber
            let paramBoolean = want.parameters.paramBoolean
            let paramString = want.parameters.paramString
            let paramNullString = want.parameters.paramNullString
          }
        }
        ```

    - To launch a browser and navigate to a specified page, use -A -U commands:

        This example uses `https://www.example.com`; replace with actual URLs as needed.

        ```bash
        aa start -A ohos.want.action.viewData -U https://www.example.com
        ```

## Force-stop Process Command (force-stop)

Forcibly terminates a process by bundleName.

```bash
aa force-stop <bundleName>
```

**Return Value:**

On successful termination: "force stop process successfully." On failure: "error: failed to force stop process."

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10105001 | Failed to connect to the ability service. |
| 10104002 | Failed to retrieve specified package information. |
| 10106401 | Failed to terminate the process. |
| 10106402 | Persistent processes cannot be terminated. |

**Example:**

```bash
# Force-stop a process by bundleName
aa force-stop com.example.myapplication
```

## Test Framework Launch Command (test)

Starts the test framework based on provided parameters.

```bash
aa test -b <bundleName> [-m <module-name>] [-p <package-name>] [-s class <test-class>] [-s level <test-level>] [-s size <test-size>] [-s testType <test-testType>] [-s timeout <test-timeout>] [-s <any-key> <any-value>] [-w <wait-time>] -s unittest <testRunner>
```

**Test Framework Launch Command Parameter List**

| Parameter | Description |
| -------- | -------- |
| -h/--help | Help information. |
| -b | Required, bundleName. |
| -s unittest | Required, testRunner. |
| -m | Optional, testRunner's moduleName.<br>**Note:** This optional parameter is only available in Stage model. |
| -s class | Optional, specifies the test suite or test case to execute. |
| -s level | Optional, specifies the test case level to execute. |
| -s size | Optional, specifies the test case size to execute. |
| -s testType | Optional, specifies the test case type to execute. |
| -s timeout | Optional, test case execution timeout (in ms), default 5000. |
| -s \<any-key> | Optional, arbitrary key-value pair. |
| -w | Optional, specifies test run duration (in ms). |
| -D | Optional, debug mode. |

**Return Value:**

On successful launch: "user test started." On failure: "error: failed to start user test." with corresponding error information.

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10104002 | Failed to retrieve specified package information. |
| 10105001 | Failed to connect to the ability service. |
| 10106002 | The target application does not support debug mode. |
| 10108501 | An internal error occurs during the execution of the aa test command. |

**Examples:**

```bash
# Launch test framework
aa test -b com.example.myapplication -s unittest ActsAbilityTest
# Launch test framework with moduleName
aa test -b com.example.myapplication -m entry_test -s unittest ActsAbilityTest
# Launch test framework with timeout
aa test -b com.example.myapplication -m entry_test -s timeout 10000 -s unittest ActsAbilityTest
```

## Debug Mode Entry Command (attach)

Puts a specified application into debug mode by bundleName.

```bash
aa attach -b <bundleName>
```

**Debug Mode Entry Command Parameter List**

| Parameter | Description |
| -------- |-------------------|
| -h/--help | Help information. |
| -b | Required, bundleName. |

**Return Value:**

On success: "attach app debug successfully." On invalid parameters: "fail: unknown option." with help information.

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10105001 | Failed to connect to the ability service. |
| 10106001 | The current device is not in developer mode. |
| 10106002 | The target application does not support debug mode. |
| 10103601 | The specified bundleName does not exist. |
| 10108601 | An internal error occurs while attempting to enter/exit debug mode. |

**Example:**

```bash
# Put specified application into debug mode by bundleName
aa attach -b com.example.myapplication
```

## Debug Mode Exit Command (detach)

Takes a specified application out of debug mode by bundleName.

```bash
aa detach -b <bundleName>
```**Command Parameter List for Exiting Debug Mode**

| Parameter | Description              |
| -------- |-------------------|
| -h/--help | Help information.             |
| -b | Required parameter, bundleName.  |

**Return Value:**

When the application successfully exits debug mode, it returns "detach app debug successfully."; when the provided parameters are invalid, it returns "fail: unknown option." and prints the help information.

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10105001 | Failed to connect to the ability service.|
| 10106001 | The current device is not in developer mode. |
| 10106002 | The target application does not support debug mode. |
| 10103601 | The specified bundleName does not exist. |
| 10108601 | An internal error occurs while attempting to enter/exit debug mode. |

**Example:**

```bash
# Exit debug mode for the specified application via bundleName
aa detach -b com.example.myapplication
```

## Wait for Debug Command (appdebug)

Used to set or unset the wait-for-debug state of an application, as well as to retrieve the package name and persistence information of applications in the wait-for-debug state. The wait-for-debug state only applies to debug-type applications. The appdebug set command only affects a single application. When repeatedly set, the application package name and persistence state will be replaced with the latest settings.

```bash
aa appdebug -b <bundleName> [-p]
```

**Wait for Debug Command Parameter List**

| Parameter | Sub-Parameter | Description |
| -------- | -------- | -------- |
| -h/--help | - | Help information. |
| -b/--bundlename | bundleName | Set the wait-for-debug state for the specified application. No validation is performed on the package name legality during setup. |
| -p/--persist | - | Optional parameter; persistence flag. Including this parameter means the application will remain in the wait-for-debug state persistently, effective even after device restarts or application reinstalls. Omitting this parameter means the wait-for-debug state will only take effect once before the device restarts. Must be used in combination with the -b parameter, e.g., `aa&nbsp;appdebug&nbsp;-b&nbsp;&lt;bundleName&gt;&nbsp;-p`. |
| -c/--cancel | - | Cancel the wait-for-debug state. |
| -g/--get | - | Retrieve the package name and persistence information of the application in the wait-for-debug state. |

**Return Value:**

When execution is successful, it returns "app debug successfully."; when execution fails, it returns "error: failed to app debug."; when the failure reason is non-developer mode, it returns "error: not developer mode."

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10105003 | Failed to connect to the app service. |
| 10106001 | The current device is not in developer mode. |
| 10106701 | The target application is not a debug application. |

**Examples:**

```bash
# Display help information
aa appdebug -h

# Set the wait-for-debug state for the specified application
aa appdebug -b com.example.myapplication [-p]

# Cancel the wait-for-debug state
aa appdebug -c

# Retrieve the package name and persistence information of the application in the wait-for-debug state
# Example output: bundle name : com.example.publishsystem, persist : false
aa appdebug -g
```

## Application Debugging/Profiling Command (process)

Used to debug or profile an application. IDEs use this command to integrate debugging and profiling tools.

```bash
# Debug an application
aa process -b <bundleName> -a <abilityName> [-m <moduleName>] [-D <debug-cmd>] [-S]

# Profile an application
aa process -b <bundleName> -a <abilityName> [-m <moduleName>] [-p <perf-cmd>] [-S]
```

**Application Debugging/Profiling Command Parameter List**

| Parameter | Description |
| -------- | -------- |
| -h/--help | Help information. |
| -b | Required parameter, bundleName. |
| -a | Required parameter, abilityName. |
| -m | Optional parameter, moduleName. |
| -p | Optional parameter, profiling command, mutually exclusive with -D. The command is user-defined. |
| -D | Optional parameter, debugging command, mutually exclusive with -p. The command is user-defined. |
| -S | Optional parameter, enter the application sandbox. |

**Return Value:**

When execution is successful, it returns "start native process successfully."; when execution fails, it returns "error: failed to start native process."; when the provided parameters are invalid, it returns "error: option requires a value." and prints the help information.

**Error Codes:**

| Error Code ID | Error Message |
| ------- | -------- |
| 10105002 | Failed to obtain ability information. |
| 10105003 | Failed to connect to the app service. |
| 10106002 | The target application does not support debug mode. |

**Examples:**

```bash
# Debug an application
aa process -b com.example.myapplication -a EntryAbility -D debug_cmd [-S]

# Profile an application
aa process -b com.example.myapplication -a EntryAbility -p perf-cmd [-S]
```

## AA Tool Error Codes

### 10103001 Target Ability Visibility Verification Failed

**Error Message**

Failed to verify the visibility of the target ability.

**Error Description**

The AA tool returns this error code when the visibility verification of the target ability fails.

**Possible Causes**

When the target application's `exported` field in the [abilities tag](../cj-start/basic-knowledge/module-configuration-file.md#abilities-tag) or [extensionAbilities tag](../cj-start/basic-knowledge/module-configuration-file.md#distributionfilter-tag) in the module.json5 configuration file is set to `false`, it means the corresponding UIAbility component/ExtensionAbility component cannot be invoked by other applications or launched via AA tool commands.

**Resolution Steps**

Check if the `exported` field for the corresponding Ability in the target application's module.json5 is set to `true`. If not, change it to `true` and retry.

### 10104001 Specified Ability Does Not Exist

**Error Message**

The specified ability does not exist.

**Error Description**

The AA tool returns this error code when the specified ability name does not exist.

**Possible Causes**

The specified ability is not installed.

**Resolution Steps**

1. Verify the `abilityName` parameter in the `-a` option and the `bundleName` parameter in the `-b` option of the AA command.
2. Check if the application corresponding to the specified `bundleName` is installed. Use the following command to query the list of installed applications. If the `bundleName` is not in the query results, the application is not installed successfully.

    ```bash
    hdc shell bm dump -a
    ```

3. For multi-HAP applications, confirm if the HAP containing the Ability is installed. Use the following command to query the package information of the application. If the HAP and Ability are not found in the installed application, the HAP containing the Ability is not installed.

    ```bash
    hdc shell bm dump -n package_name
    ```

### 10105001 Ability Service Connection Failed

**Error Message**

Failed to connect to the ability service.

**Error Description**

Failed to connect to the Ability service.

**Possible Causes**

The Ability service was disconnected during the interface call.

**Resolution Steps**

Try restarting the device and re-executing the command.

### 10105002 Failed to Obtain Ability Information

**Error Message**

Failed to obtain ability information.

**Error Description**

Failed to obtain Ability information.

**Possible Causes**

The AbilityInfo obtained via BMS during the generation of the Ability request was empty.

**Resolution Steps**

Check if the application corresponding to the specified `bundleName` is installed. Use the following command to query the list of installed applications. If the `bundleName` is not in the query results, the application is not installed successfully.

```bash
hdc shell bm dump -a
```

### 10105003 App Service Connection Failed

**Error Message**

Failed to connect to the app service.

**Error Description**

Failed to connect to the App service.

**Possible Causes**

The App service was disconnected during the interface call.

**Resolution Steps**

Try restarting the device.

### 10106001 Current Device Is Not in Developer Mode

**Error Message**

The current device is not in developer mode.

**Error Description**

The current device is not in developer mode.

**Possible Causes**

The current device is not in developer mode.

**Resolution Steps**

Enable developer mode in the settings.

### 10106002 Target Application Does Not Support Debug Mode

**Error Message**

The target application does not support debug mode.

**Error Description**

The target application does not support debug mode.

**Possible Causes**

The "type" parameter in the signing tool for the target application is not set to "debug".

**Resolution Steps**

Re-sign the application using a debug signing certificate, install the newly signed HAP, and then retry the command.

### 10100101 Failed to Obtain Application Information

**Error Message**

Failed to obtain application information.

**Error Description**

Abnormal App information queried from BMS.

**Possible Causes**

The application name or package name in the App information queried from BMS is abnormal.

**Resolution Steps**

1. Verify the `abilityName` parameter in the `-a` option and the `bundleName` parameter in the `-b` option of the AA command.
2. Check if the application corresponding to the specified `bundleName` is installed. Use the following command to query the list of installed applications. If the `bundleName` is not in the query results, the application is not installed successfully.

    ```bash
    hdc shell bm dump -a
    ```

3. For multi-HAP applications, confirm if the HAP containing the Ability is installed. Use the following command to query the package information of the application. If the HAP and Ability are not found in the installed application, the HAP containing the Ability is not installed.

    ```bash
    hdc shell bm dump -n package_name
    ```

### 10100102 AA Start Command Cannot Launch UIExtensionAbility

**Error Message**

The aa start command cannot be used to launch a UIExtensionAbility.

**Error Description**The aa tool fails to launch UIExtensionAbility.

**Possible Causes**

The `aa start` command does not support launching UIExtensionAbility.

**Resolution Steps**

Verify whether the target Ability is a UIExtensionAbility. The `aa start` command cannot launch UIExtensionAbility.

### 10103101 No Matching Application Found for Implicit Launch

**Error Message**

Failed to find a matching application for implicit launch.

**Error Description**

No matching Ability is found during an implicit launch.

**Possible Causes**

- For implicit launches: Incorrect launch parameter configuration or the specified HAP package is not installed.
- For explicit launches: The command specifies `bundleName` but omits `abilityName`.

**Resolution Steps**

- For implicit launches: Ensure the launch parameters are correctly configured and the package is installed.
- For explicit launches: Verify that the `abilityName` parameter is correctly passed.

### 10103102 Invalid AppCloneIndex Value

**Error Message**

The passed appCloneIndex is invalid.

**Error Description**

This error code is returned when an invalid `AppCloneIndex` is provided.

**Possible Causes**

The `AppCloneIndex` parameter in the `aa start` command contains an invalid value.

**Resolution Steps**

Confirm whether the `AppCloneIndex` is valid.

### 10106101 Previous Ability Launch Incomplete; Current Ability Queued

**Error Message**

The current ability will be placed in the queue to wait for the previous ability to finish launching.

**Error Description**

Due to high system load, the requested Ability is queued and processed sequentially.

**Possible Causes**

High system concurrency.

**Resolution Steps**

No action required. Wait for the launch to complete.

### 10106102 Device Locked During Application Launch

**Error Message**

The device screen is locked during the application launch.

**Error Description**

The device is locked when attempting to launch the application.

**Possible Causes**

The screen cannot be unlocked during application launch.

**Resolution Steps**

Unlock the screen and retry.

### 10106103 Target Application Is an Expired Crowdtesting App

**Error Message**

The target application is an expired crowdtesting application.

**Error Description**

This error code is returned when the target application is a crowdtesting app that has reached its expiration date.

**Possible Causes**

The crowdtesting app has expired and cannot be opened.

**Resolution Steps**

Check whether the app's crowdtesting period has expired. Expired crowdtesting apps cannot be launched.

### 10106105 Target Application Is Restricted

**Error Message**

The target application is under control.

**Error Description**

This error code is returned when the target application is restricted by the app store.

**Possible Causes**

The target application is suspected of malicious behavior and is restricted from launching.

**Resolution Steps**

Uninstall the application.

### 10106106 Target Application Is Managed by EDM

**Error Message**

The target application is managed by EDM.

**Error Description**

This error code is returned when the target application is restricted by enterprise device management.

**Possible Causes**

The target application is prohibited from launching by enterprise management services.

**Resolution Steps**

This device is enterprise-managed, and the target application is blocked from launching. Developers cannot resolve this issue.

### 10106107 Current Device Does Not Support Window Options

**Error Message**

The current device does not support using window options.

**Error Description**

Window options are unsupported on the current device.

**Possible Causes**

The `aa start` command specifies `WindowOptions`, but the device does not support them.

**Resolution Steps**

Remove the `WindowOptions` parameters (`wl`, `wt`, `wh`, `ww`) from the `aa start` command and retry.

### 10107102 Specified Process Permission Verification Failed

**Error Message**

Permission verification failed for the specified process.

**Error Description**

This error code is returned when permission verification fails for the specified process.

**Possible Causes**

Permission verification failed for the specified process.

**Resolution Steps**

Verify whether the process permissions are correctly configured.

### 10108101 Internal Error During Ability Launch

**Error Message**

An internal error occurs while attempting to launch the ability.

**Error Description**

This error code is returned for internal processing errors such as memory allocation or multithreading exceptions.

**Possible Causes**

Generic kernel errors, including: null internal objects, timeouts, failure to retrieve app information from package management, failure to obtain system services, or exceeding the maximum number of Ability instances.

**Resolution Steps**

Internal errors occur during system operation and cannot be resolved by developers.

### 10103201 Target Ability Is Not a ServiceAbility

**Error Message**

The target ability is not of the ServiceAbility type.

**Error Description**

The target Ability is not a ServiceAbility.

**Possible Causes**

The `abilityName` parameter in the `aa stop` command does not correspond to a ServiceAbility.

**Resolution Steps**

Verify whether the `abilityName` parameter in the `aa stop` command refers to a ServiceAbility.

### 10104002 Failed to Retrieve Specified Package Information

**Error Message**

Failed to retrieve specified package information.

**Error Description**

Failed to retrieve information for the specified package.

**Possible Causes**

The application corresponding to the specified package name is not installed.

**Resolution Steps**

1. Verify whether the package name is correct.
2. Check whether the application corresponding to the `bundleName` is installed. Use the following command to list installed applications. If the `bundleName` is not in the results, the application is not installed.

    ```bash
    hdc shell bm dump -a
    ```

### 10106401 Failed to Terminate Process

**Error Message**

Failed to terminate the process.

**Error Description**

Failed to kill the process.

**Possible Causes**

1. The application specified in the `aa force-stop` command does not exist.
2. Failed to connect to AppManagerService.

**Resolution Steps**

1. Check whether the application corresponding to the `bundleName` is installed. Use the following command to list installed applications. If the `bundleName` is not in the results, the application is not installed.

    ```bash
    hdc shell bm dump -a
    ```

2. Try restarting the device.

### 10106402 Persistent Process Cannot Be Terminated

**Error Message**

Persistent processes cannot be terminated.

**Error Description**

Persistent processes cannot be killed.

**Possible Causes**

The `bundleName` specified in the `aa force-stop` command corresponds to a persistent process.

**Resolution Steps**

Check whether the target application is a persistent process. Persistent processes cannot be terminated via command.

### 10108501 Internal Error in `aa test` Command

**Error Message**

An internal error occurs during the execution of the `aa test` command.

**Error Description**

This error code is returned for internal processing errors such as memory allocation or multithreading exceptions.

**Possible Causes**

Generic kernel errors, including: null internal objects, timeouts, or failure to obtain system services.

**Resolution Steps**

Internal errors occur during system operation and cannot be resolved by developers.

### 10108601 Internal Error During Debug Mode Entry/Exit

**Error Message**

An internal error occurs while attempting to enter/exit debug mode.**Error Description**

This error code is returned when internal processing errors occur, such as memory allocation failures or multithreading exceptions.

**Possible Causes**

General kernel-level errors related to memory allocation or multithreading. Specific causes may include: null internal objects, processing timeouts, or failures to obtain system services.

**Resolution Steps**

Internal errors are system runtime errors that cannot be handled by developers.

### 10103601 Specified Bundle Name Does Not Exist

**Error Message**

The specified bundleName does not exist.

**Error Description**

This error code is returned when the user-specified bundle name cannot be found.

**Possible Causes**

The bundle name specified in the `aa attach/detach` command does not exist.

**Resolution Steps**

Verify whether the application corresponding to the specified bundleName is installed. Use the following command to query the list of installed applications. If the bundleName is not in the query results, the application was not successfully installed.

```bash
hdc shell bm dump -a
```

### 10106701 Target Application Is Not a Debug Application

**Error Message**

The target application is not a debug application.

**Error Description**

The target application is not configured as a debug application.

**Possible Causes**

The "type" parameter in the current signing tool is not set to "debug".

**Resolution Steps**

Re-sign the application using a debug signing certificate. After installing the newly signed HAP, retry the command.  
For guidance on signing tools and certificate generation, refer to: [Signing Tool Guide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing).