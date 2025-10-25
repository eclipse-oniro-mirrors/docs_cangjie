# bm Tool

Bundle Manager (abbreviated as bm) is a tool that implements functionalities such as application installation, uninstallation, updates, and queries. It provides developers with basic debugging capabilities for application installation packages.

> **Note:**
>
> Currently, Cangjie only supports the development of HAR and HAP packages and does not support HSP packages. Therefore, HSP-related functionalities in this tool are unavailable in the Cangjie program.

## Environment Requirements (hdc Tool)

Before using this tool, developers need to obtain the [hdc tool](./cj-hdc.md) and execute `hdc shell`.

## bm Tool Command List

| Command | Description |
| :-------- | :-------- |
| help | Help command, used to query the command information supported by bm. |
| install | Installation command, used to install applications. |
| uninstall | Uninstallation command, used to uninstall applications. |
| dump | Query command, used to query application-related information. |
| clean | Cleanup command, used to clear application cache and data. This command is available in root versions and in user versions with developer mode enabled. Otherwise, it is unavailable. |
| <!--DelRow-->enable | Enable command, used to enable applications. Once enabled, applications can continue to be used. This command is available in root versions but not in user versions. |
| <!--DelRow-->disable | Disable command, used to disable applications. Once disabled, applications cannot be used. This command is available in root versions but not in user versions. |
| get | Get UDID command, used to retrieve the device's UDID. |
| quickfix | Quick fix-related commands, used to perform patch-related operations such as patch installation and patch queries. |
| compile | Command to compile applications for AOT (Ahead-of-Time). |
| copy-ap | Copies the application's AP files to the `/data/local/pgo` directory for shell users to read the files. |
| dump-dependencies | Queries module dependency information for applications. |
| dump-shared | Queries HSP application information between applications. |
| dump-overlay | Prints the overlayModuleInfo of overlay applications. |
| dump-target-overlay | Prints the overlayModuleInfo of all associated overlay applications for the target application. |

## Help Command (help)

```bash
# Display help information
bm help
```

## Installation Command (install)

```bash
bm install [-h] [-p filePath] [-r] [-w waitingTime] [-s hspDirPath]
```

**Installation Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -p | Required parameter, specifies the path and allows simultaneous installation of multiple HAPs. |
| -r | Optional parameter, overwrites the installation of a HAP. The default is to overwrite. |
| -s | Required parameter when installing inter-application HSPs; otherwise optional. Installs inter-application shared libraries. Only one HSP with the same package name can exist in each directory path. |
| -w | Optional parameter, specifies the waiting time for the bm tool during HAP installation. The minimum wait time is 5s, and the maximum is 600s. The default is 5s. |

Examples:

```bash
# Install a HAP
bm install -p /data/app/ohos.app.hap
# Overwrite install a HAP
bm install -p /data/app/ohos.app.hap -r
# Install an inter-application shared library
bm install -s xxx.hsp
# Simultaneously install the consumer application and its dependent inter-application shared libraries
bm install -p aaa.hap -s xxx.hsp yyy.hsp
# Install a HAP with a 10s wait time
bm install -p /data/app/ohos.app.hap -w 10
```

## Uninstallation Command (uninstall)

```bash
bm uninstall [-h] [-n bundleName] [-m moduleName] [-k] [-s] [-v versionCode]
```

**Uninstallation Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -n | Required parameter, specifies the Bundle name to uninstall the application. |
| -m | Optional parameter, specifies a module of the application to uninstall. By default, all modules are uninstalled. |
| -k | Optional parameter, preserves application data during uninstallation. By default, application data is not preserved. |
| -s | Required parameter when uninstalling inter-application HSPs; otherwise optional. Uninstalls the specified shared library. |
| -v | Optional parameter, specifies the version number of the shared package. By default, all shared packages with the same name are uninstalled. |

Examples:

```bash
# Uninstall an application
bm uninstall -n com.ohos.app
# Uninstall a module of an application
bm uninstall -n com.ohos.app -m com.ohos.app.EntryAbility
# Uninstall a shared bundle
bm uninstall -n com.ohos.example -s
# Uninstall a specified version of a shared bundle
bm uninstall -n com.ohos.example -s -v 100001
# Uninstall an application and preserve user data
bm uninstall -n com.ohos.app -k
```

## Application Information Query Command (dump)

```bash
bm dump [-h] [-a] [-n bundleName] [-s shortcutInfo] [-d deviceId]
```

**Query Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -a | Optional parameter, queries all installed applications in the system. |
| -n | Optional parameter, queries detailed information for the specified Bundle name. |
| -s | Optional parameter, queries shortcut information for the specified Bundle name. |
| -d | Optional parameter, queries package information for the specified device. By default, the current device is queried. |

Examples:

```bash
# Display all installed Bundle names
bm dump -a
# Query detailed information for the application
bm dump -n com.ohos.app
# Query shortcut information for the application
bm dump -s -n com.ohos.app
# Query cross-device application information
bm dump -n com.ohos.app -d xxxxx
```

## Cleanup Command (clean)

```bash
bm clean [-h] [-c] [-n bundleName] [-d] [-i appIndex]
```

**Cleanup Command Parameter List:**

| Parameter | Description |
| :-------- | :--------- |
| -h | Help information. |
| -c&nbsp;-n | -n is required, -c is optional. Clears cache data for the specified Bundle name. |
| -d&nbsp;-n | -n is required, -d is optional. Clears the data directory for the specified Bundle name. |
| -i | Optional parameter, clears the data directory for a cloned application. Default is 0. |

Examples:

```bash
# Clear cache data for the application
bm clean -c -n com.ohos.app
# Clear user data for the application
bm clean -d -n com.ohos.app
// Execution result
clean bundle data files successfully.
```

<!--Del-->
## Enable Command (enable)

```bash
bm enable [-h] [-n bundleName] [-a abilityName]
```

**Enable Command Parameter List**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -n | Required parameter, enables the application with the specified Bundle name. |
| -a | Optional parameter, enables the meta-ability module under the specified Bundle name. |

Example:

```bash
# Enable the application
bm enable -n com.ohos.app -a com.ohos.app.EntryAbility
# Execution result
enable bundle successfully.
```

## Disable Command (disable)

```bash
bm disable [-h] [-n bundleName] [-a abilityName]
```

**Disable Command Parameter List**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -n | Required parameter, disables the application with the specified Bundle name. |
| -a | Optional parameter, disables the meta-ability module under the specified Bundle name. |

Example:

```bash
# Disable the application
bm disable -n com.ohos.app -a com.ohos.app.EntryAbility
# Execution result
disable bundle successfully.
```

<!--DelEnd-->

## Get UDID Command (get)

```bash
bm get [-h] [-u]
```

**Get UDID Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -u | Required parameter, retrieves the device's UDID. |

Example:

```bash
# Get the device's UDID
bm get -u
// Execution result
udid of current device is :
23CADE0C
```

## Quick Fix Command (quickfix)

```bash
bm quickfix [-h] [-a -f filePath [-t targetPath] [-d]] [-q -b bundleName] [-r -b bundleName]
```

> **Note:**
>
> For HQF file creation methods, refer to [HQF Packing Instructions](./cj-packing-tool.md#hqf打包指令).

**Quick Fix Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -a&nbsp;-f | -a is optional; if specified, -f is required. Executes the quick fix patch installation command. `file-path` corresponds to the HQF file, supporting one or more HQF files or the directory containing HQF files. |
| -q&nbsp;-b | -q is optional; if specified, -b is required. Queries patch information based on the package name. |
| -r&nbsp;-b | -r is optional; if specified, -b is required. Uninstalls inactive patches based on the package name. |
| -t | Optional parameter, applies quick fixes to the specified target path. |
| -d | Optional parameter, enables quick fix debugging mode. |

**Example 1:**

```bash
# Query patch package information based on the package name
bm quickfix -q -b com.ohos.app
```

**Execution Result:**

```text
Information as follows:
ApplicationQuickFixInfo:
bundle name: com.ohos.app
bundle version code: xxx
bundle version name: xxx
patch version code: x
patch version name:
cpu abi:
native library path:
type:
```

**Example 2:**

```bash
# Install quick fix patches
bm quickfix -a -f /data/app/
```

**Execution Result:**

```text
apply quickfix succeed.
```

**Example 3:**

```bash
# Uninstall quick fix patches
bm quickfix -r -b com.ohos.app
```

**Execution Result:**

```text
delete quick fix successfully
```

## Shared Library Query Command (dump-shared)

```bash
bm dump-shared [-h] [-a] [-n bundleName] [-m moduleName]
```

**Shared Library Query Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -a | Optional parameter, queries all installed shared libraries in the system. |
| -n | Optional parameter, queries detailed information for the specified shared library package name. |
| -m | Optional parameter, queries detailed information for the specified shared library package name and module name. |

Examples:

```bash
# Display all installed shared library package names
bm dump-shared -a
# Display detailed information for the shared library
bm dump-shared -n com.ohos.lib
# Display shared library dependency information for the specified application and module
bm dump-dependencies -n com.ohos.app -m entry
```

## Shared Library Dependency Query Command (dump-dependencies)

Displays shared library dependency information for the specified application and module.

```bash
bm dump-dependencies [-h] [-n bundleName] [-m moduleName]
```

**Shared Library Dependency Query Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -n | Required parameter, queries detailed information for the specified shared library package name. |
| -m | Optional parameter, queries shared library dependency information for the specified application and module. |

Example:

```Bash
# Display shared library dependency information for the specified application and module
bm dump-dependencies -n com.ohos.app -m entry
```

## Application AOT Compilation Command (compile)

Command to compile applications for AOT (Ahead-of-Time).

```bash
bm compile [-h] [-m mode] [-r bundleName] [-a]
```

**Compile Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -a | Optional parameter, compiles all applications. |
| -m | Optional parameter, values can be `partial` or `full`. Compiles the application based on the package name. |
| -r | Optional parameter, removes the application's results. |

Example:

```bash
# Compile the application based on the package name
bm compile -m partial com.example.myapplication
```

## Copy AP Files Command (copy-ap)

Copies AP files to the `/data/local/pgo` directory for the specified application.

```bash
bm copy-ap [-h] [-a] [-n bundleName]
```

**Copy-ap Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -a | Optional parameter, copies all AP files related to the package by default. |
| -n | Optional parameter, defaults to the current application package name. Copies AP files related to the specified package name. |

Example:

```bash
# Move AP files related to the specified package name
bm copy-ap -n com.example.myapplication
```

## Overlay Application Information Query Command (dump-overlay)

Prints the overlayModuleInfo of overlay applications.

```bash
bm dump-overlay [-h] [-b bundleName] [-m moduleName] [-t targetModuleName]
```

**Dump-overlay Command Parameter List:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -b | Required parameter, retrieves all OverlayModuleInfo information for the specified application. |
| -m | Optional parameter, defaults to the current application's main module name. Queries OverlayModuleInfo information based on the specified package name and module name. |
| -t | Optional parameter, queries OverlayModuleInfo information based on the specified package name and target module name. |

Examples:

```bash
# Retrieve all OverlayModuleInfo information for the overlay application com.ohos.app based on the package name
bm dump-overlay -b com.ohos.app

# Retrieve all OverlayModuleInfo information for the overlay application com.ohos.app where the overlay module is entry, based on the package name and module
bm dump-overlay -b com.ohos.app -m entry

# Retrieve all OverlayModuleInfo information for the overlay application com.ohos.app where the target module is feature, based on the package name and module
bm dump-overlay -b com.ohos.app -m feature
```## Command for Querying Overlay Information of Applications (dump-target-overlay)

Query the overlayModuleInfo of all associated overlay applications for the target application.

```bash
bm dump-target-overlay [-h] [-b bundleName] [-m moduleName]
```

**Parameter List for dump-target-overlay Command:**

| Parameter | Description |
| :-------- | :-------- |
| -h | Help information. |
| -b | Required parameter. Retrieves all OverlayBundleInfo for the specified application. |
| -m | Optional parameter. Defaults to the current application's main module name. Queries OverlayBundleInfo based on the specified package name and module name. |

Examples:

```bash
# Retrieve all associated OverlayBundleInfo for the target application com.ohos.app based on the package name
bm dump-target-overlay -b com.ohos.app

# Retrieve all associated OverlayModuleInfo for the target module "entry" in the target application com.ohos.app based on the package name and module
bm dump-target-overlay -b com.ohos.app -m entry
```

## Error Codes for the bm Tool

### 301 System Account Does Not Exist

**Error Message:**

error: user not exist.

**Error Description:**

The system account does not exist.

**Possible Causes:**

The system account ID does not exist when installing the application.

**Resolution Steps:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating the above steps 3 to 5 times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
hdc file recv /data/log/hilog/
```

### 304 Current System Account Has No HAP Package Installed

**Error Message:**

error: user does not install the hap.

**Error Description:**

During uninstallation, the current system account has no HAP package installed.

**Possible Causes:**

No HAP package is installed under the current system account.

**Resolution Steps:**

Since no HAP package is installed under the current system account, do not perform the uninstallation operation.

### 9568319 Signature File Exception

**Error Message:**

error: cannot open signature file.

**Error Description:**

During application installation, an exception occurred while opening the signature file, causing the installation to fail.

**Possible Causes:**

The HAP package's signature file is abnormal.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568320 Signature File Does Not Exist

**Error Message:**

error: no signature file.

**Error Description:**

The user attempted to install an unsigned HAP package.

**Possible Causes:**

The HAP package is not signed.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568321 Signature File Parsing Failed

**Error Message:**

error: fail to parse signature file.

**Error Description:**

The signature file parsing failed during user installation.

**Possible Causes:**

The HAP package's signature file is abnormal.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568323 Signature Digest Verification Failed

**Error Message:**

error: signature verification failed due to not bad digest.

**Error Description:**

Signature verification failed during user installation.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568324 Signature Integrity Check Failed

**Error Message:**

error: signature verification failed due to out of integrity.

**Error Description:**

Signature verification failed during user installation.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568326 Signature Public Key Exception

**Error Message:**

error: signature verification failed due to bad public key.

**Error Description:**

Signature verification failed during user installation due to an abnormal signature public key.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568327 Signature Retrieval Exception

**Error Message:**

error: signature verification failed due to bad bundle signature.

**Error Description:**

Signature verification failed during user installation due to an abnormal signature retrieval.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568328 Profile Block Not Found

**Error Message:**

error: signature verification failed due to no profile block.

**Error Description:**

Signature verification failed during user installation because the profile block was not found.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568330 Signature Source Initialization Failed

**Error Message:**

error: signature verification failed due to init source failed.

**Error Description:**

Signature verification failed during user installation due to a failure in initializing the signature source.

**Possible Causes:**

The HAP package's signature is incorrect.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568257 Pkcs7 Signature File Verification Failed

**Error Message:**

error: fail to verify pkcs7 file.

**Error Description:**

Pkcs7 signature verification failed during user installation.

**Possible Causes:**

1. The certificate chain is incomplete or untrusted.
2. The signature algorithm does not match.
3. The data has been tampered with or the signature file is corrupted.
4. The signature format does not match.
5. The private key does not match.

**Resolution Steps:**

1. Use [automatic signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). After connecting the device, re-sign the application.
2. For manual signing, refer to [manual signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section297715173233).

### 9568344 Profile File Parsing Failed

**Error Message:**

error: install parse profile prop check error.

![Example Image](./figures/zh-cn_image_0000001585361412.png)

**Error Description:**

During application/service debugging or runtime, an error occurred while installing the HAP, displaying the message "error: install parse profile prop check error."

**Possible Causes:**

1. The bundleName in the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md) or the name in the [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) does not comply with naming rules. <!--Del-->

2. The type field in [extensionAbilities](../cj-start/basic-knowledge/module-configuration-file.md#extensionabilities标签) is configured as "service" or "dataShare."

<!--DelEnd-->

**Resolution Steps:**

1. Adjust the bundleName in the app.json5 configuration file and the name field in the module.json5 file according to naming rules. <!--Del-->

2. If the type field in extensionAbilities is configured as "service" or "dataShare," the application must configure the [allowAppUsePrivilegeExtension privilege](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-app-privilege-config-guide.md) as follows:

    1. Obtain a new signature fingerprint.

        a. In the project-level build-profile.json5 file (located in the project root directory), the value of the profile field under signingConfigs indicates the storage path of the signature file.

        b. Open the signature file (with a .p7b extension), search for "development-certificate," and copy the content between "-----BEGIN CERTIFICATE-----" and "-----END CERTIFICATE-----" into a new text file. Remove line breaks and save it as a new .cer file (e.g., xxx.cer).

        The format of the new .cer file is as follows (for illustration only; actual content may vary):

        ![Example Image](figures/zh-cn_image_0000001585521364.png)

        c. Use the keytool tool (located in the jbr/bin folder of the DevEco Studio installation directory) to execute the following command and obtain the SHA256 value of the certificate fingerprint from the .cer file.

        ```bash
        keytool -printcert -file xxx.cer
        ```

        d. Remove the colons from the SHA256 content of the certificate fingerprint to obtain the final signature fingerprint.

        Example (for illustration only; actual content may vary):

        ![Example Image](figures/zh-cn_image_0000001635921233.png)

        The signature fingerprint after removing colons is: 5753DDBC1A8EF88A62058A9FC4B6AFAFC1C5D8D1A1B86FB3532739B625F8F3DB.

    2. Obtain the device's privilege control whitelist file, install_list_capability.json.

        a. Connect to the device and enter the shell.

        ```bash
        hdc shell
        ```

        b. Execute the following command to locate the install_list_capability.json file on the device.

        ```bash
        // Query the location of the whitelist file on the device
        find /system -name install_list_capability.json
        ```

        c. Execute the following command to pull the install_list_capability.json file.

        ```bash
        hdc target mount
        hdc file recv /system/etc/app/install_list_capability.json
        ```

    3. Add the signature fingerprint obtained in step 1 to the app_signature field in the install_list_capability.json file, ensuring it is configured under the corresponding bundleName.

        ![Example Image](figures/zh-cn_image_0000001635641893.png)

    4. Push the modified install_list_capability.json file back to the device and restart the device.

        ```bash
        hdc target mount
        hdc file send install_list_capability.json /system/etc/app/install_list_capability.json
        hdc shell chmod 644 /system/etc/app/install_list_capability.json
        hdc shell reboot
        ```

    5. After the device restarts, reinstall the new application. <!--DelEnd-->

### 9568305 Dependent Module Does Not Exist

**Error Message:**

error: dependent module does not exist.

![Example Image](./figures/zh-cn_image_0000001560338986.png)

**Error Description:**

During application/service debugging or runtime, an error occurred while installing the HAP, displaying the message "error: dependent module does not exist."

**Possible Causes:**

The dynamic shared library (SharedLibrary) module required by the running/debugging application is not installed, causing the installation error.

**Resolution Steps:**

1. First, install the dependent dynamic shared library (SharedLibrary) module. Then, on the application runtime configuration page, check "Keep Application Data," click OK to save the configuration, and proceed with running/debugging.

    ![Example Image](./figures/zh-cn_image_0000001560201786.png)

2. On the runtime configuration page, select the "Deploy Multi Hap" tab, check "Deploy Multi Hap Packages," select the dependent module, click OK to save the configuration, and proceed with running/debugging.

    ![Example Image](./figures/zh-cn_image_0000001610761941.png)

3. Click Run > Edit Configurations, and under General, check "Auto Dependencies." Click OK to save the configuration and proceed with running/debugging.

    ![Example Image](./figures/zh-cn_image_9568305.png)

### 9568259 Required Field Missing in Profile File During Installation

**Error Message:**

error: install parse profile missing prop.

![Example Image](./figures/zh-cn_image_0000001559130596.png)

**Error Description:**

During application/service debugging or runtime, an error occurred while installing the HAP, displaying the message "error: install parse profile missing prop."

**Possible Causes:**

Required fields are missing in the app.json5 or module.json5 configuration files.

**Resolution Steps:**

- Method 1: Refer to the [app.json5 configuration file](../cj-start/basic-knowledge/app-configuration-file.md) and [module.json5 configuration file](../cj-start/basic-knowledge/module-configuration-file.md) to review and supplement the required fields.
- Method 2: Use hilog logs to identify the missing fields.

    Enable disk logging with the following command:

    ```bash
    hilog -w start
    ```

    Log location: /data/log/hilog.

    Open the logs and look for "profile prop %{public}s is mission." For example, "profile prop icon is mission" indicates that the "icon" field is missing.### 9568258 ReleaseType Mismatch Between Installed and New Application

**Error Message:**

error: install releaseType target not same.

![Example Image](./figures/zh-cn_image_0000001609976041.png)

**Error Description:**

When launching debugging or running an application/service, an error occurs during HAP installation with the message "error: install releaseType target not same."

**Possible Causes:**

- Scenario 1: The releaseType value in the SDK used by the old HAP installed on the device differs from that of the new HAP being installed.
- Scenario 2: When installing a multi-HAP application, the releaseType values in the SDK used by each HAP are inconsistent.

**Resolution Steps:**

- Scenario 1: Uninstall the old HAP from the device before installing the new HAP.
- Scenario 2: Repackage the HAPs using the same SDK version to ensure consistent releaseType values across all HAPs.

---

### 9568260 Internal Installation Error

**Error Message:**

error: install internal error.

**Error Description:**

Internal installation error.

**Possible Causes:**

An internal service exception occurred during installation.

**Resolution Steps:**

Restart the device and attempt the installation again.

---

### 9568267 Entry Module Already Exists

**Error Message:**

error: install entry already exist.

**Error Description:**

The entry module of the application to be installed already exists.

**Possible Causes:**

Multi-module applications require a unique entry module. The installation fails because the module name of the new package differs from the installed one, but both are of the entry type, violating the uniqueness requirement.

**Resolution Steps:**

1. Uninstall the existing HAP from the device before installing the new HAP.
2. Ensure the entry module name matches the installed one or change the new module's type to "feature" and retry.

---

### 9568268 Installation State Error

**Error Message:**

error: install state error.

**Error Description:**

Failed to update the application installation state.

**Possible Causes:**

A previous large installation package took too long, causing the state update to fail as the task was still ongoing.

**Resolution Steps:**

Wait for the previous installation to complete before retrying.

---

### 9568269 Invalid File Path

**Error Message:**

error: install file path invalid.

**Error Description:**

The installation package path provided is invalid.

**Possible Causes:**

1. The path does not exist (e.g., typo).
2. The path exceeds 256 bytes.

**Resolution Steps:**

1. Verify the path exists and has proper access permissions.
2. Ensure the path length does not exceed 256 bytes.

---

### 9568322 Signature Verification Failed Due to Untrusted Source

**Error Message:**

error: signature verification failed due to not trusted app source.

![Example Image](./figures/zh-cn_image_0000001585042216.png)

**Error Description:**

During debugging or runtime, HAP installation fails with the message "error: signature verification failed due to not trusted app source."

**Possible Causes:**

- Scenario 1: The signature does not include the UDID of the debugging device.
- Scenario 2: A [release certificate and profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-releaseharmony-0000001933963166) were used for signing. Release-signed apps cannot be debugged or run.

**Resolution Steps:**

- Scenario 1:
  1. Use [auto-signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section18815157237). Re-sign the app after connecting the device.
  2. For manual signing in OpenHarmony, refer to <!--RP2-->[OpenHarmony Manual Signing Guide](https://docs.openharmony.cn/pages/v4.1/en/application-dev/security/hapsigntool-guidelines.md)<!--RP2End--> and add the device's **UDID** to `UnsgnedDebugProfileTemplate.json`.

      a. Retrieve the device UDID:
      ```bash
      hdc shell bm get -u
      ```

      b. Locate `UnsgnedDebugProfileTemplate.json` in the IDE SDK directory:
      ```bash
      IDE_PATH\sdk\VERSION_OR_DEFAULT\openharmony\toolchains\lib\
      ```

      c. Add the UDID to the `device-ids` field in the JSON file.

- Scenario 2: Re-sign the app using [debug certificates and profiles](https://developer.huawei.com/consumer/cn/doc/app/agc-help-debug-app-0000001914423098).

---

### 9568286 Provision Type Mismatch

**Error Message:**

error: install provision type not same.

**Error Description:**

During installation, the provision type in the [signing profile](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796) differs from the installed app.

**Possible Causes:**

The provision type of the installed app does not match the new app.

**Resolution Steps:**

1. Ensure both apps use the same provision type for signing.
2. Uninstall the existing app before installing the new one.

---

### 9568288 Insufficient Disk Space

**Error Message:**

error: install failed due to insufficient disk memory.

**Error Description:**

Installation fails due to lack of storage space for creating files/directories.

**Possible Causes:**

Device storage is full.

**Resolution Steps:**

Free up space and retry. Check storage usage:
```bash
hdc shell df -h /system
hdc shell df -h /data
```

---

### 9568289 Permission Grant Failure

**Error Message:**

error: install failed due to grant request permissions failed.

![Example Image](./figures/zh-cn_image_0000001585201996.png)

**Error Description:**

Installation fails with permission grant errors.

**Possible Causes:**

Normal-grade apps cannot use `system_basic` or `system_core` permissions.

**Resolution Steps:**

Apply for restricted ACL permissions per the [ACL Signing Guide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section157591551175916).

---

### 9568290 HAP Token Update Failure

**Error Message:**

error: install failed due to update hap token failed.

**Error Description:**

Failed to update HAP token during installation.

**Possible Causes:**

Token authorization API call failed.

**Resolution Steps:**

1. Restart the device and retry.
2. If the issue persists after 3–5 attempts, submit logs via [Support Ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/):
```bash
hdc file recv /data/log/hilog/
```

---

### 9568297 Device SDK Version Too Low

**Error Message:**

error: install failed due to older sdk version in the device.

![Example Image](./figures/zh-cn_image_0000001635521909.png)

**Error Description:**

Installation fails due to SDK version mismatch.

**Possible Causes:**

The SDK version used for compilation is higher than the device's OS version.

**Resolution Steps:**

- Scenario 1: Upgrade the device OS. Check the API version:
  ```bash
  hdc shell param get const.ohos.apiversion
  ```
  If the issue persists despite matching versions, update to the latest OS.

- Scenario 2: For OpenHarmony apps, ensure `runtimeOS` is set to `OpenHarmony`.

---

### 9568300 Non-Unique Module Names

**Error Message:**

error: moduleName is not unique.

**Error Description:**

Installation fails due to duplicate module names in a multi-HAP app.

**Possible Causes:**

Conflicting module names in `module.json5`.

**Resolution Steps:**

Review all module names and ensure uniqueness before repackaging.

---

### 9568332 Signature Inconsistency

**Error Message:**

error: install sign info inconsistent.

![Example Image](./figures/zh-cn_image_0000001635761329.png)

**Error Description:**

Signature mismatch between installed and new apps or among HAPs/HSPs.

**Possible Causes:**

1. Re-signing with "Keep Application Data" enabled.
2. Retained data from an uninstalled app with a mismatched signature.

**Resolution Steps:**

1. Uninstall the app or disable "Keep Application Data."
2. For HSPs, use [Integrated HSPs](https://docs.openharmony.cn/pages/v5.1/zh-cn/application-dev/quick-start/integrated-hsp.md) or ensure consistent signatures.
3. Reinstall the old app and uninstall it without retaining data before installing the new one.

---

### 9568329 Signature Verification Failure

**Error Message:**

error: verify signature failed.

![Example Image](./figures/zh-cn_image_155401.png)

**Error Description:**

Package name in the signature does not match the app's `bundleName`.

**Possible Causes:**

- Scenario 1: Using a third-party HSP that is neither integrated nor shares the same package name.
- Scenario 2: Incorrect signing file (`.p7b`).

**Resolution Steps:**

- Scenario 1: Request an integrated HSP or same-package HSP from the provider.
- Scenario 2: Verify the signing process per [Debug Signing Guide](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing).

---

### 9568266 Installation Permission Denied

**Error Message:**

error: install permission denied.

![Example Image](./figures/zh-cn_image_9568266.png)

**Error Description:**

`hdc install` fails for release-signed enterprise apps.

**Possible Causes:**

`hdc install` only supports debug-signed enterprise apps.

**Resolution Steps:**

Use `hdc install` for debug-signed apps only.

---

### 9568337 Installation Parse Error

**Error Message:**

error: install parse unexpected.

**Error Description:**

Failed to open the HAP file during installation.

**Possible Causes:**

- Scenario 1: Full `/system` partition causing file corruption.
- Scenario 2: Corrupted HAP during transfer.

**Resolution Steps:**

- Scenario 1: Free up space in `/system`:
  ```bash
  hdc shell df -h /system
  ```

- Scenario 2: Compare MD5 hashes of local and transferred HAPs. Retransfer if mismatched.### 9568316 APL Permission Field in Proxy Data Indicates Insufficient Permissions  

**Error Message:**  

error: apl of required permission in proxy data is too low.  

**Error Description:**  

Validation failed for the `requiredReadPermission` and `requiredWritePermission` attributes in the `proxyData` tag.  

**Possible Causes:**  

In the user project's `module.json`, the validation for the `requiredReadPermission` and `requiredWritePermission` attributes in the `proxyData` tag failed. These attributes require permission levels of either `system_basic` or `system_core`.  

**Resolution Steps:**  

Verify that the `proxyData` content defined in the application meets the requirements. Refer to the [proxyData Tag](../cj-start/basic-knowledge/module-configuration-file.md#proxydata标签).  

---  

### 9568315 Incorrect URI in Proxy Data  

**Error Message:**  

error: uri in proxy data is wrong.  

**Error Description:**  

Validation failed for the `uri` attribute in the `proxyData` tag.  

**Possible Causes:**  

In the user project's `module.json`, the validation for the `uri` attribute in the `proxyData` tag failed because it does not comply with the URI format requirements.  

**Resolution Steps:**  

Verify that the `proxyData` content defined in the application meets the requirements. Refer to the [proxyData Tag](../cj-start/basic-knowledge/module-configuration-file.md#proxydata标签).  

---  

### 9568336 Debug Type Mismatch Between Application and Installed Version  

**Error Message:**  

error: install debug type not same.  

**Error Description:**  

The application's debug type (`debug` field in `app.json`) does not match the installed version.  

**Possible Causes:**  

The developer installed the application using the debug button in DevEco Studio and later installed a packaged version via `hdc install`.  

**Resolution Steps:**  

Uninstall the existing application and reinstall the new version.  

---  

### 9568296 Incorrect Bundle Type  

**Error Message:**  

error: install failed due to error bundle type.  

**Error Description:**  

Application installation failed due to an incorrect `bundleType`.  

**Possible Causes:**  

The `bundleType` of the newly installed application does not match that of an already installed application with the same `bundleName`.  

**Resolution Steps:**  

- **Method 1:** Uninstall the existing application and reinstall the new version.  
- **Method 2:** Modify the `bundleType` of the new application to match the installed version.  

---  

### 9568292 UserID 0 Can Only Install Singleton Applications  

**Error Message:**  

error: install failed due to zero user can only install singleton app.  

**Error Description:**  

UserID 0 is only allowed to install applications with `singleton` permissions, and `singleton` applications can only be installed by UserID 0.  

**Possible Causes:**  

A `singleton` permission application was installed without specifying UserID 0.  

**Resolution Steps:**  

For `singleton` permission applications, specify UserID 0 during installation:  

```bash  
// Command to install with userId  
hdc install -p hap_name.hap -u 0  
```  

---  

### 9568263 Downgrade Installation Not Allowed  

**Error Message:**  

error: install version downgrade.  

**Error Description:**  

The `VersionCode` of the application being installed is lower than that of the installed version, resulting in installation failure.  

**Possible Causes:**  

The `VersionCode` of the application being installed is lower than that of the installed version.  

**Resolution Steps:**  

Uninstall the existing application and reinstall the new version.  

---  

### 9568301 Module Type Mismatch  

**Error Message:**  

error: moduleName is inconsistent.  

**Error Description:**  

The module name being installed already exists in the system, but the module types are inconsistent, causing installation failure.  

**Possible Causes:**  

The module name of the application being installed already exists in the system, but the module types are inconsistent.  

**Resolution Steps:**  

Check whether the module names of the installed applications conflict with the new module. If the module names are the same but the types differ, modify the `type` attribute in the corresponding module's `module.json5`.  

---  

### 9568302 Inconsistent Singleton Configuration Across Application Modules  

**Error Message:**  

error: install failed due to singleton not same.  

**Error Description:**  

Inconsistent `singleton` configurations across multiple modules of the application caused installation failure.  

**Possible Causes:**  

During multi-module installation, the `singleton` configurations were inconsistent, failing the validation check.  

**Resolution Steps:**  

Adjust the `singleton` configurations of all modules to be consistent before reinstalling.  

---  

### 9568303 Installation Blocked by Enterprise Device Management  

**Error Message:**  

error: Failed to install the HAP because the installation is forbidden by enterprise device management.  

**Error Description:**  

Installation failed due to application control policies.  

**Possible Causes:**  

Application control policies are in place.  

**Resolution Steps:**  

Due to enterprise restrictions, no direct solution is available. Submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.  

---  

### 9568304 Application Does Not Support Current Device Type  

**Error Message:**  

error: device type is not supported.  

**Error Description:**  

The application being installed does not support the current device type, resulting in installation failure.  

**Possible Causes:**  

The application being installed does not support the current device type.  

**Resolution Steps:**  

To adapt to the current device, add the device type to the application's configuration. Supported `deviceTypes` include `phone`, `tablet`, `2in1`, `tv`, `wearable`, and `car`.  

---  

### 9568308 Inconsistent Bundle Types Across Application Packages  

**Error Message:**  

error: install bundleType not same.  

**Error Description:**  

Inconsistent `bundleType` across application packages caused installation failure.  

**Possible Causes:**  

During multi-HAP installation, the `bundleType` attributes of two modules were inconsistent.  

**Resolution Steps:**  

Ensure the `bundleType` attributes in `app.json5` are consistent across all modules in the multi-HAP application.  

---  

### 9568309 Installation of Inter-Application HSP Not Permitted  

**Error Message:**  

error: Failed to install the HSP due to the lack of required permission.  

**Error Description:**  

Installation of an inter-application HSP failed due to insufficient privileges.  

**Possible Causes:**  

The required privilege for installing an inter-application HSP is missing.  

**Resolution Steps:**  

Check whether the application has the `AllowAppShareLibrary` privilege in the device's `install_list_capability.json`. Refer to the [Application Privilege Configuration Guide](https://docs.openharmony.cn/pages/v5.1/en/device-dev/subsystems/subsys-app-privilege-config-guide.md).  

---  

### 9568311 Inter-Application HSP to Be Uninstalled Does Not Exist  

**Error Message:**  

error: shared bundle is not exist.  

**Error Description:**  

Uninstallation failed because the specified inter-application HSP does not exist.  

**Possible Causes:**  

The specified inter-application HSP does not exist.  

**Resolution Steps:**  

Verify the existence of the inter-application HSP to be uninstalled:  

```bash  
hdc shell bm dump-shared -n com.xxx.xxx.demo  
```  

---  

### 9568312 Inter-Application HSP to Be Uninstalled Is Being Used  

**Error Message:**  

error: The version of the shared bundle is dependent on other applications.  

**Error Description:**  

Uninstallation failed because the specified inter-application HSP is being used by other applications.  

**Possible Causes:**  

The specified inter-application HSP is being used by other applications.  

**Resolution Steps:**  

Check whether the inter-application HSP is being used by other applications. If dependencies exist, uninstall the dependent applications first.  

---  

### 9568317 Application's Multi-Process Configuration Mismatches System Settings  

**Error Message:**  

error: isolationMode does not match the system.  

**Error Description:**  

The `isolationMode` set during installation does not match the system's allowed configurations.  

**Possible Causes:**  

- **Scenario 1:** The device supports isolation mode (`persist.bms.supportIsolationMode` is `true`), but the HAP's `isolationMode` is set to `nonisolationOnly`.  
- **Scenario 2:** The device does not support isolation mode (`persist.bms.supportIsolationMode` is `false`), but the HAP's `isolationMode` is set to `isolationOnly`.  

**Resolution Steps:**  

Configure the HAP's `isolationMode` attribute according to the device's isolation mode settings:  

```bash  
// Check the device's persist.bms.supportIsolationMode value (errNum 106 indicates no configuration)  
hdc shell  
param get persist.bms.supportIsolationMode  
// Configure persist.bms.supportIsolationMode  
hdc shell  
param set persist.bms.supportIsolationMode [true|false]  
```  

---  

### 9568315 Incorrect URI Attribute in Proxy Data  

**Error Message:**  

error: uri in proxy data is wrong.  

**Error Description:**  

Validation failed for the `uri` attribute in the `proxyData` tag of the application's `module.json`.  

**Possible Causes:**  

The URI does not comply with format specifications.  

**Resolution Steps:**  

Ensure the URI meets the following format requirements:  

```text  
// URI Format Requirements  
URIs for different proxy data must be unique and follow the format: datashareproxy://current_application_package_name/xxx  
```  

---  

### 9568310 Compatibility Policy Mismatch  

**Error Message:**  

error: compatible policy not same.  

**Error Description:**  

The compatibility policy of the new package differs from that of the installed package.  

**Possible Causes:**  

1. An application is already installed, and an inter-application shared library with the same `bundleName` is being installed.  
2. An inter-application shared library is already installed, and an application with the same `bundleName` is being installed.  

**Resolution Steps:**  

Uninstall the existing application or inter-application shared library before installing the new package.  

---  

### 9568391 Bundle Manager Service Has Stopped  

**Error Message:**  

error: bundle manager service is died.  

**Error Description:**  

The bundle manager service has stopped.  

**Possible Causes:**  

An unknown system exception caused the bundle manager service to stop or crash.  

**Resolution Steps:**  

1. Restart the device and attempt installation again.  
2. If installation fails after 3–5 attempts, check for crash files containing `foundation` in `/data/log/faultlog/faultlogger/`:  

    ```bash  
    hdc shell  
    cd /data/log/faultlog/faultlogger/  
    ls -ls  
    ```  

3. Export the crash and log files and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance:  

    ```bash  
    hdc file recv /data/log/faultlog/faultlogger/  
    hdc file recv /data/log/hilog/  
    ```  

---  

### 9568393 Code Signature Verification Failed  

**Error Message:**  

error: verify code signature failed.  

**Error Description:**  

Code signature verification failed.  

**Possible Causes:**  

The package lacks code signature information.  

**Resolution Steps:**  

Install the latest version of DevEco Studio and resign the package.  

---  

### 9568399 File Copy Failed  

**Error Message:**  

error: copy file failed.  

**Error Description:**  

File copy failed during application installation.  

**Possible Causes:**  

1. The source or destination path is invalid.  
2. Failed to open the source file.  
3. Failed to retrieve the source file's status.  
4. The source file size is invalid.  
5. Failed to copy the source file.  
6. No access permissions for the source file.  
7. Failed to modify file permissions.  

**Resolution Steps:**  

1. Restart the device and attempt installation again.  
2. If installation fails after 3–5 attempts, export the log files and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance:  

    ```bash  
    hdc file recv /data/log/hilog/  
    ```### 9568401 Debug Bundle Only Supports Devices in Developer Mode

**Error Message:**

error: debug bundle can only be installed in developer mode.

**Error Description:**

The debug bundle can only run on devices in developer mode.

**Possible Causes:**

The terminal device has not enabled "Developer Mode."

**Resolution Steps:**

1. Check if "Developer Options" exists under "Settings > System" on the terminal device. If not, go to "Settings > About Device" and tap the "Build Number" seven times consecutively until the prompt "Developer Mode Enabled" appears. Click "Confirm Enable" and enter the PIN (if set). The device will restart automatically.
2. Connect the terminal to a PC via a USB cable. Under "Settings > System > Developer Options," toggle the "USB Debugging" switch. In the "Allow USB Debugging" pop-up, click "Allow."
3. Start debugging or run the application.

### 9568404 Failed to Deliver Signature Profile

**Error Message:**

error: delivery sign profile failed.

**Error Description:**

An exception occurred while delivering the code signature profile during installation, resulting in installation failure.

**Possible Causes:**

1. The file path does not exist.
2. Failed to create the file path.
3. Failed to change the file directory mode.
4. Failed to write configuration file data.
5. Failed to change the configuration file mode.
6. Failed to add configuration file data.

**Resolution Steps:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating steps 1-3 five times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
hdc file recv /data/log/hilog/
```

### 9568405 Failed to Remove Signature Profile

**Error Message:**

error: remove sign profile failed.

**Error Description:**

An exception occurred while deleting the signature profile during application uninstallation, resulting in uninstallation failure.

**Possible Causes:**

1. The file path does not exist.
2. Failed to load configuration file data.
3. The file does not have write permissions.

**Resolution Steps:**

1. Restart the phone and attempt to uninstall the application again.
2. If the uninstallation still fails after repeating steps 1-3 five times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

    ```bash
    hdc file recv /data/log/hilog/
    ```

### 9568386 Application to Uninstall Does Not Exist

**Error Message:**

error: uninstall missing installed bundle.

**Error Description:**

The application to uninstall does not exist.

**Possible Causes:**

The application to uninstall is not installed.

**Resolution Steps:**

Confirm whether the application to uninstall is already installed.

### 9568388 Enterprise Device Management Prohibits Uninstalling the Application

**Error Message:**

error: Failed to uninstall the HAP because the uninstall is forbidden by enterprise device management.

**Error Description:**

Enterprise device management does not allow uninstalling the application.

**Possible Causes:**

The application is configured to prohibit uninstallation.

**Resolution Steps:**

Have the administrator remove the uninstallation restriction for the application.

### 9568284 Installation Version Mismatch

**Error Message:**

error: install version not compatible.

**Error Description:**

The installation version does not match.

**Possible Causes:**

The version information of the currently installed HSP does not match that of the installed HAP. The following checks are performed during HSP installation:

1. The `bundleName` must match the HAP.
2. The `version` must match the HAP.
3. The signature must match the HAP.

**Resolution Steps:**

1. Uninstall the HAP with mismatched version information and then install the HSP.
2. Modify the HSP version information to match the HAP and then install the HSP.

### 9568287 Invalid Number of Entry Modules in Installation Package

**Error Message:**

error: install invalid number of entry hap.

**Error Description:**

The number of entry modules in the installation package is non-compliant.

**Possible Causes:**

The installation package contains multiple entry modules. An application can have only one entry module but multiple feature modules.

**Resolution Steps:**

Retain one entry module and modify the remaining entry modules to feature modules (by changing the `type` field in `module.json5`).

### 9568281 Vendor Mismatch in Installation Package

**Error Message:**

error: install vendor not same.

**Error Description:**

The vendor in the installation package does not match.

**Possible Causes:**

The `vendor` field in the `app.json5` file is inconsistent.

**Resolution Steps:**

1. If there is only one HAP, ensure the `vendor` field matches that of the installed application. Uninstall and reinstall if necessary.
2. If an integrated HSP is included, ensure the `vendor` field of the integrated HSP matches that of the dependent HAP.

### 9568272 Invalid Installation Package Size

**Error Message:**

error: install invalid hap size.

**Error Description:**

The installation package size exceeds the limit.

**Possible Causes:**

The installation package size exceeds 4GB.

**Resolution Steps:**

Split the package to ensure each installation package does not exceed 4GB.

### 9568273 Failed to Generate UID for Application, Resulting in Installation Failure

**Error Message:**

error: install generate uid error.

**Error Description:**

Failed to generate a UID for the application, resulting in installation failure.

**Possible Causes:**

The number of installed applications on the device has exceeded 65,535, causing UID allocation failure during installation.

**Resolution Steps:**

Uninstall unnecessary applications and retry.

### 9568274 Installation Service Error

**Error Message:**

error: install installd service error.

**Error Description:**

Installation service error.

**Possible Causes:**

The installation service is abnormal.

**Resolution Steps:**

Clear the cache and restart the device.

### 9568275 Package Management Service Error

**Error Message:**

error: install bundle mgr service error.

**Error Description:**

Package management service error.

**Possible Causes:**

The package management service is abnormal, such as encountering a null pointer exception.

**Resolution Steps:**

Restart the device or try again later.

### 9568277 Bundle Name Mismatch, Resulting in Installation Failure

**Error Message:**

error: install bundle name not same.

**Error Description:**

Bundle name mismatch, resulting in installation failure.

**Possible Causes:**

The bundle names of multiple installation packages in the target path are inconsistent.

**Resolution Steps:**

Check the bundle names of the installation packages in the target path and ensure the `bundleName` in the `app.json5` configuration file is consistent.

### 9568279 Version Mismatch, Resulting in Installation Failure

**Error Message:**

error: install version name not same.

**Error Description:**

Version (`versionName` field) mismatch, resulting in installation failure.

**Possible Causes:**

The `versionName` of multiple installation packages in the target path is inconsistent.

**Resolution Steps:**

Check the versions of the installation packages in the target path and ensure the `versionName` in the `app.json5` configuration file is consistent.

### 9568280 minCompatibleVersionCode Mismatch, Resulting in Installation Failure

**Error Message:**

error: install min compatible version code not same.

**Error Description:**

`minCompatibleVersionCode` field mismatch, resulting in installation failure.

**Possible Causes:**

The `minCompatibleVersionCode` of multiple installation packages in the target path is inconsistent.

**Resolution Steps:**

Check the installation packages in the target path and ensure the `minCompatibleVersionCode` in the `app.json5` configuration file is consistent.

### 9568282 targetAPIVersion Mismatch, Resulting in Installation Failure

**Error Message:**

error: install releaseType target not same.

**Error Description:**

`targetAPIVersion` field mismatch, resulting in installation failure.

**Possible Causes:**

The `targetAPIVersion` of multiple installation packages in the target path is inconsistent.

**Resolution Steps:**

Check the installation packages in the target path and ensure the `targetAPIVersion` in the `app.json5` configuration file is consistent.

### 9568314 Failed to Install Inter-Application Shared Library

**Error Message:**

error: Failed to install the HSP because installing a shared bundle specified by hapFilePaths is not allowed.

**Error Description:**

Failed to install the inter-application shared library.

**Possible Causes:**

The command `hdc app install ***` was used to install an inter-application shared HSP.

**Resolution Steps:**

Use the command `hdc install -s ***` to install inter-application HSPs.

### 9568349 Parameter Exception During File Operation

**Error Message:**

error: installd param error.

**Error Description:**

Parameter exception during file operation, resulting in installation failure.

**Possible Causes:**

Invalid parameters were passed during installation, or the directory path was empty.

**Resolution Steps:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating steps 1-3 five times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568351 Directory Creation Exception, Resulting in Installation Failure

**Error Message:**

error: installd create dir failed.

**Error Description:**

Directory creation exception, resulting in installation failure.

**Possible Causes:**

No write permissions when creating the directory.

**Resolution Steps:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating steps 1-3 five times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568354 Directory Deletion Exception, Resulting in Installation Failure

**Error Message:**

error: installd remove dir failed.

**Error Description:**

Directory deletion exception, resulting in installation failure.

**Possible Causes:**

The directory to delete does not exist, or the current directory lacks write permissions.

**Resolution Steps:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating steps 1-3 five times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```### 9568355 Failed to Extract Files from Installation Package

**Error Message:**

error: installd extract files failed.

**Error Description:**

Failed to extract files from the installation package, resulting in installation failure.

**Possible Causes:**

During installation, the directory for extracting SO files failed to be created, leading to the failure of extracting SO files from the HAP package.

**Steps to Resolve:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating the above steps 3 to 5 times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568356 Failed to Rename Directory During Installation

**Error Message:**

error: installd rename dir failed.

**Error Description:**

Failed to rename the directory, resulting in installation failure.

**Possible Causes:**

During installation, the directory name exceeds 260 characters, or the current directory lacks write permissions.

**Steps to Resolve:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating the above steps 3 to 5 times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568357 Failed to Clean Files

**Error Message:**

error: installd clean dir failed.

**Error Description:**

Failed to clean files, resulting in installation failure.

**Possible Causes:**

During installation, the files to be cleaned lack write permissions, causing the cleaning process to fail.

**Steps to Resolve:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating the above steps 3 to 5 times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568359 Failed to Set SELinux During Installation

**Error Message:**

error: installd set selinux label failed.

**Error Description:**

Failed to set SELinux during installation.

**Possible Causes:**

The APL field in the signing configuration file is incorrect. APL has three levels: "normal," "system_basic," and "system_core."

**Steps to Resolve:**

1. Verify if the APL field in the p7b signing file is incorrect.

    ![Example Image](./figures/zh-cn_image_9568359.png)

2. If the APL field is incorrect, modify the APL field in the `UnsgnedReleasedProfileTemplate.json` file and re-sign.

    ![Example Image](./figures/zh-cn_image_9568359_2.png)

### 9568403 Encryption Verification Failed During Installation

**Error Message:**

error: check encryption failed.

**Error Description:**

Encryption verification failed during installation.

**Possible Causes:**

The mirror version may be outdated, or non-SO files exist in the HAP package's `lib` directory.

**Steps to Resolve:**

1. Install a newer version of the mirror.
2. Remove non-SO files from the `lib` directory in the HAP project and re-sign the package.

### 9568413 Application Device Type Not Supported by Current Device

**Error Message:**

error: check syscap filed and device type is not supported.

**Error Description:**

The configured device type for the application is not supported for installation.

**Possible Causes:**

The configured device type for the application does not match the installation device.

**Steps to Resolve:**

Adjust to the correct device type.

### 9568417 Signature Verification Failed

**Error Message:**

error: bundle cannot be installed because the appId is not same with preinstalled bundle.

**Error Description:**

Signature verification failed.

**Possible Causes:**

The signature of the installed application does not match that of the preinstalled application with the same package name.

**Steps to Resolve:**

If the installed application is a preinstalled one, ensure its signature matches that of the preinstalled application.

### 9568278 Inconsistent Version Numbers in Installation Package

**Error Message:**

error: install version code not same.

**Possible Causes:**

1. The version code (`versionCode`) of the application installed on the device does not match that of the installation package causing the error.
2. Inconsistent version codes (`versionCode`) exist among multiple installation packages.

**Steps to Resolve:**

1. Adjust the version code of the installation package to match that of the application already installed on the device, or uninstall the existing application before installing the new one.
2. Ensure all installation packages have consistent version codes (`versionCode`).

### 9568380 Failed to Uninstall System Application

**Error Message:**

error: uninstall system app error.

**Error Description:**

Failed to uninstall a system application.

**Possible Causes:**

Some system applications are set as non-removable and cannot be uninstalled.

**Steps to Resolve:**

Do not attempt to uninstall non-removable applications.

### 9568387 Failed to Uninstall Non-Installed Module

**Error Message:**

error: uninstall missing installed module.

**Error Description:**

Attempted to uninstall a non-installed module.

**Possible Causes:**

Attempted to uninstall a module that is not installed.

**Steps to Resolve:**

Use the [bm dump -n](#query-application-information-command-dump) command to check the application configuration and confirm the module is installed.

### 9568432 Plugin and Application `pluginDistributionIDs` Verification Failed

**Error Message:**

error: Check pluginDistributionID between plugin and host application failed.

**Error Description:**

Verification failed between the `pluginDistributionIDs` of the application and the plugin.

**Possible Causes:**

The `pluginDistributionIDs` of the application and the plugin have no common values, causing verification failure.

**Steps to Resolve:**

Reconfigure the `pluginDistributionIDs` in the [signing certificate profile file](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-releaseprofile-0000001914714796) for the application or plugin.

### 9568433 Application Lacks `ohos.permission.SUPPORT_PLUGIN` Permission

**Error Message:**

error: Failed to install the plugin because host application check permission failed.

**Error Description:**

Permission verification failed when the application attempted to install a plugin.

**Possible Causes:**

The application lacks the `ohos.permission.SUPPORT_PLUGIN` permission.

**Steps to Resolve:**

1. Refer to the [Permission Application Guide](../security/AccessToken/cj-declare-permissions.md) to apply for the [`ohos.permission.kernel.SUPPORT_PLUGIN` permission](../security/AccessToken/cj-restricted-permissions.md#ohospermissionkernelsupport_plugin). <!--Del-->
2. This permission is classified as `system_basic`. If the [application's APL level](../security/AccessToken/cj-app-permission-mgmt-overview.md#basic-concepts-in-permission-mechanism) is lower than `system_basic`, [apply for restricted permissions](../security/AccessToken/cj-declare-permissions-in-acl.md).

<!--DelEnd-->

### 9568333 Module Name is Empty

**Error Message:**

error: Install failed due to hap moduleName is empty.

**Error Description:**

Module name is empty, causing installation failure.

**Possible Causes:**

Module name is empty.

**Steps to Resolve:**

Check if the `name` field in [`module.json5`](../cj-start/basic-knowledge/module-configuration-file.md) is empty.

### 9568331 Inconsistent Signature Information

**Error Message:**

error: Install incompatible signature info.

**Error Description:**

Inconsistent signature information, causing installation failure.

**Possible Causes:**

When installing a multi-HAP application, the signature information of the HAP packages is inconsistent.

**Steps to Resolve:**

Re-[sign](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing) to ensure consistent signature information across all HAP packages.

### 9568334 Duplicate Module Name

**Error Message:**

error: Install failed due to hap moduleName duplicate.

**Error Description:**

Duplicate module name, causing installation failure.

**Possible Causes:**

When installing multiple modules for the same application, module names are duplicated.

**Steps to Resolve:**

Ensure module names are unique across all modules of the same application.

### 9568340 Missing Configuration File

**Error Message:**

error: Install parse no profile.

**Error Description:**

HAP package lacks a configuration file, causing installation failure.

**Possible Causes:**

Configuration files such as [`module.json`, `pack.info`](../cj-start/basic-knowledge/application-package-structure-stage.md) are missing.

**Steps to Resolve:**

Rebuild, package, and install using DevEco Studio.

### 9568341 Failed to Parse Configuration File During Installation

**Error Message:**

error: Install parse bad profile.

**Error Description:**

Failed to parse the configuration file during installation.

**Possible Causes:**

Configuration files such as [`module.json`, `pack.info`](../cj-start/basic-knowledge/application-package-structure-stage.md) have abnormal formats.

**Steps to Resolve:**

Rebuild, package, and install using DevEco Studio.

### 9568342 Incorrect Data Type in Configuration File

**Error Message:**

error: Install parse profile prop type error.

**Error Description:**

Incorrect data type encountered while parsing the configuration file, causing installation failure.

**Possible Causes:**

Configuration files such as [`module.json`, `pack.info`](../cj-start/basic-knowledge/application-package-structure-stage.md) contain fields with incorrect data types.

**Steps to Resolve:**

Rebuild, package, and install using DevEco Studio.

### 9568345 String Length or Array Size in Configuration File Exceeds Limit

**Error Message:**

error: Too large size of string or array type element in the profile.

**Error Description:**

String length or array size in the configuration file exceeds the limit, causing installation failure.

**Possible Causes:**

Configuration files such as [`module.json`, `pack.info`](../cj-start/basic-knowledge/application-package-structure-stage.md) contain fields with excessively long strings or large arrays.

**Steps to Resolve:**

Rebuild, package, and install using DevEco Studio.

### 9568347 Failed to Parse Native SO File

**Error Message:**

error: install parse native so failed.

**Error Description:**

An error occurred while installing the HAP package during C++ application/service debugging or execution, displaying the message "error: install parse native so failed."

**Possible Causes:**

The device's supported ABI types do not match those configured in the C++ project.

> **Note:**
>
> If the project depends on HSP or HAR modules, ensure all modules containing C++ code include the device's supported ABI types.
> If the project depends on third-party libraries containing SO files, ensure the `oh_modules/third-party-libs/libs` directory includes the device's supported ABI directories, such as `libs/arm64-v8a` or `libs/x86_64`.
<!--RP1--><!--RP1End-->

**Steps to Resolve:**

1. Connect the device to DevEco Studio.
2. Execute the following command to query the device's supported ABI list. The result will include one or more ABI types: `default`, `armeabi-v7a`, `armeabi`, `arm64-v8a`, `x86`, or `x86_64`.

    ```bash
    hdc shell
    param get const.product.cpu.abilist
    ```

3. Based on the query result, check the `abiFilters` parameter in the [module-level `build-profile.json5`](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-hvigor-build-profile) file, following these rules:

    - If the result is `default`, execute the following command to check if the `lib64` folder exists.

        ```bash
        cd /system/
        ls
        ```

        ![Example Image](./figures/zh-cn_image_0000001609001262.png)

        If `lib64` exists: Include `arm64-v8a` in the `abiFilters` parameter. If `lib64` does not exist: Include at least one of `armeabi` or `armeabi-v7a` in the `abiFilters` parameter.

    - If the result includes one or more of `armeabi-v7a`, `armeabi`, `arm64-v8a`, `x86`, or `x86_64`, include at least one of these ABI types in the `abiFilters` parameter.

### 9568348 Failed to Parse Ark Native SO File

**Error Message:**

error: Install parse ark native file failed.

**Error Description:**

Failed to parse the Ark native SO file during installation.

**Possible Causes:**

During multi-HAP installation, ABI types are inconsistent and do not match the device's supported ABI types.

**Steps to Resolve:**

Check if the ABIs of multiple HAPs are consistent. Refer to the resolution steps for [Error Code 9568347](#9568347-failed-to-parse-native-so-file).

### 9568350 Failed to Obtain Proxy Object During Installation

**Error Message:**

error: Installd get proxy error.

**Error Description:**

Failed to obtain the proxy object during installation.

**Possible Causes:**

Package management or other services are abnormal, causing proxy acquisition to fail.

**Steps to Resolve:**

1. Restart the phone and attempt to install the application again.
2. If the installation still fails after repeating the above steps 3 to 5 times, export the log file and submit an [online ticket](https://developer.huawei.com/consumer/cn/support/feedback/#/) for assistance.

```bash
# Export log file
hdc file recv /data/log/hilog/
```

### 9568434 Device Does Not Support Plugin Capability

**Error Message:**

error: Failed to install the plugin because current device does not support plugin.

**Error Description:**

The current device does not support plugin capability, causing plugin installation to fail.

**Possible Causes:**

The device does not support plugin capability.

**Steps to Resolve:**

Use the [param tool](./cj-param-tool.md) to set `const.bms.support_plugin` to `true` by executing `hdc shell param set const.bms.support_plugin true`.

### 9568435 Application Package Name Does Not Exist

**Error Message:**

error: Host application is not found.

**Error Description:**

The provided application package name does not exist.

**Possible Causes:**

The application is not installed.

**Steps to Resolve:**

Verify if the provided application exists.

### 9568436 Inconsistent Information Among Multiple HSP Packages

**Error Message:**

error: Failed to install the plugin because they have different configuration information.

**Error Description:**

Inconsistent package information among multiple HSPs, causing installation failure.

**Possible Causes:**

When installing plugins as multiple HSPs, the package information of the HSP files is inconsistent.

**Steps to Resolve:**

Ensure consistency in package information among multiple HSPs, including the `bundleName`, `bundleType`, `versionCode`, and `apiReleaseType` fields in the [`app.json5` configuration file](../cj-start/basic-knowledge/app-configuration-file.md).

### 9568437 Failed to Parse Plugin's `pluginDistributionIDs`

**Error Message:**

error: Failed to install the plugin because the plugin id failed to be parsed.

**Error Description:**

Failed to parse the plugin's `pluginDistributionIDs`, causing installation failure.

**Possible Causes:**

The `pluginDistributionIDs` configuration in the plugin's signing information does not comply with specifications, causing parsing failure.

**Steps to Resolve:**

Reconfigure the `app-services-capabilities` field in the plugin's profile signing file as follows:

```json
"app-services-capabilities":{
    "ohos.permission.kernel.SUPPORT_PLUGIN":{
        "pluginDistributionIDs":"value-1|value-2|···"
    }
}
```

### 9568438 Plugin Package Name Does Not Exist

**Error Message:**

error: The plugin is not found.

**Error Description:**

The plugin does not exist.

**Possible Causes:**

The plugin is not installed for the current application.

**Steps to Resolve:**

Use the [bm dump -n command](#query-application-information-command-dump) to query the application's information and verify if the provided plugin is installed.

### 9568439 Plugin and Application Package Names Are Identical

**Error Message:**

error: The plugin name is same as host bundle name.

**Error Description:**

The plugin's package name matches the application's package name.

**Possible Causes:**

The plugin's package name is identical to the application's package name, causing plugin installation to fail.

**Steps to Resolve:**

Reconfigure the plugin's package name.

### 9568441 Application Cannot Change `U1Enabled`

**Error Message:**

error: install failed due to U1Enabled can not change.

**Error Description:**

Installation failed due to a change in the `U1Enabled` field in the signing information.

**Possible Causes:**

The `U1Enabled` configuration in the `allowed-acls` field of the application's [Profile signing file](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugprofile-0000001914423102) has changed, such as:

1. The installed application has `U1Enabled` configured in `allowed-acls`, but the installation package does not.
2. The installed application does not have `U1Enabled` configured in `allowed-acls`, but the installation package does.

**Steps to Resolve:**

**Option 1:** Re-sign the package. During signing, refer to the [Automatic Signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section9786111152213) guide for ACL permissions or the [Manual Signing](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/ide-signing#section157591551175916) guide for ACL configurations to ensure consistency between the installation package and the installed application.

**Option 2:** Uninstall the existing application on the device before installing the new one.

### 9568442 Inconsistent `U1Enabled` Configuration

**Error Message:**

error: Install failed due to the U1Enabled is not same in all haps.

**Error Description:**

Inconsistent `U1Enabled` configuration in the signing information, causing installation failure.

**Possible Causes:**

Different [Profile signing files](https://developer.huawei.com/consumer/cn/doc/app/agc-help-add-debugprofile-0000001914423102) were used for signing multiple HAP packages, resulting in inconsistent `U1Enabled` configurations in `allowed-acls`.

**Steps to Resolve:**

Re-sign the packages. During signing, refer to the [Automatic Signing](https://developer.huawei.com/## Frequently Asked Questions

### 1. Pre-installed System App Uninstalled: Errors Occur During Reinstallation in Specific Scenarios - Downgrade Installation or Signature Mismatch

**Issue Description**  

After uninstalling the app, errors such as "downgrade installation" or "signature mismatch" occur during reinstallation. However, the corresponding app icon appears on the desktop and can be launched normally.

**Possible Causes**  

Enhanced security controls have been implemented for uninstalled pre-installed system apps. When installing an app with the same bundleName, the system first restores the application from the pre-installed image version before proceeding with the installation of the incoming app.

**Resolution Steps**  

Address the issue based on the error message and error code.  
<!--DelEnd-->