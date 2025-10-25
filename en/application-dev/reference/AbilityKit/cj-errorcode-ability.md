# Meta Capability Subsystem Error Codes

> **NOTE:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 16000001 The Specified Ability Does Not Exist

**Error Message**

The specified ability does not exist.

**Error Description**

This error code is returned when the specified ability name does not exist.

**Possible Causes**

The queried ability does not exist.

**Solution**

1. Verify that the bundleName, moduleName, and abilityName in the want are correct.
2. Check whether the application corresponding to the bundleName in the want is installed. Use the following command to query the list of installed applications. If the bundleName is not in the query result, the application is not installed successfully.

    ``` text
    hdc shell bm dump -a
    ```

3. For multi-HAP applications, confirm whether the HAP to which the ability belongs has been installed. Use the following command to query the package information of the application. If the corresponding HAP and ability are not found in the installed application, the HAP to which the ability belongs is not installed.

    ``` text
    hdc shell bm dump -n package_name
    ```

## 16000002 Incorrect Ability Type

**Error Message**

Incorrect ability type.

**Error Description**

This error code is returned when the ability type called by the interface is incorrect.

**Possible Causes**

The ability type where the interface is called does not support this interface call.

**Solution**

1. Verify that the bundleName, moduleName, and abilityName in the want are correct.
2. Call different interfaces based on the ability type.

## 16000003 The Specified ID Does Not Exist

**Error Message**

The specified ID does not exist.

**Error Description**

This error code is returned when the specified ID does not exist.

**Possible Causes**

The target ID of the operation does not exist.

**Solution**

Confirm whether the ID of the operation exists.

## 16000004 Visibility Verification Failed

**Error Message**

Failed to start the invisible ability.

**Error Description**

This error code is returned when visibility verification fails.

**Possible Causes**

Application visibility verification failed.

**Solution**

1. In the Stage model, if exception 16000004 is thrown when starting an application, it indicates that the called application failed to start. Check whether the exported configuration of the Ability field in the module.json5 of the called application is set to true. If this configuration field is true, the ability can be called by other applications; if it is false, the ability cannot be called by other applications.
2. If an application needs to start an ability with exported set to false, apply for the ohos.permission.START_INVISIBLE_ABILITY permission (this permission can only be applied for by system applications).

## 16000005 Permission Verification Failed for the Specified Process

**Error Message**

The specified process does not have the permission.

**Error Description**

This error code is returned when permission verification fails for the specified process.

**Possible Causes**

Permission verification failed for the specified process.

**Solution**

Confirm whether the permissions of the specified process are correct.

## 16000006 Cross-User Operations Are Not Allowed

**Error Message**

Cross-user operations are not allowed.

**Error Description**

This error code is returned when an application performs cross-user operations.

**Possible Causes**

The application performed cross-user operations.

**Solution**

Confirm whether cross-user operations were performed.

## 16000007 Service Busy

**Error Message**

Service busy. There are concurrent tasks. Try again later.

**Error Description**

This error code is returned when the service is busy.

**Possible Causes**

The service is busy.

**Solution**

The service is busy. Please try again later.

## 16000008 Crowdtesting Application Expired

**Error Message**

The crowdtesting application expires.

**Error Description**

This error code is returned when a crowdtesting application expires.

**Possible Causes**

The crowdtesting application has expired and cannot be opened.

**Solution**

Check whether the crowdtesting application has expired. Expired crowdtesting applications cannot be started.

## 16000009 Ability Cannot Be Started or Stopped in Wukong Mode

**Error Message**

An ability cannot be started or stopped in Wukong mode.

**Error Description**

This error code is returned when an ability is started or stopped in Wukong mode.

**Possible Causes**

Starting or stopping an ability is not allowed in Wukong mode.

**Solution**

Exit Wukong mode before attempting to start or stop the ability. Do not start or stop an ability in Wukong mode.

## 16000010 Call with Continuation Flag Is Forbidden

**Error Message**

The call with the continuation flag is forbidden.

**Error Description**

This error code is returned when a call carries the continuation flag.

**Possible Causes**

The current call does not allow the continuation flag.

**Solution**

Check whether the continuation flag is carried.

## 16000011 The Context Does Not Exist

**Error Message**

The context does not exist.

**Error Description**

This error code is returned when the context object does not exist.

**Possible Causes**

The current context object does not exist.

**Solution**

Check whether the context object is available.

## 16000012 The Application Is Controlled

**Error Message**

The application is controlled.

**Error Description**

This error code is returned when an application is controlled by the application market.

**Possible Causes**

The application is suspected of malicious behavior and is controlled by the application market, preventing it from being started.

**Solution**

It is recommended to uninstall the application.

## 16000013 The Application Is Controlled by EDM

**Error Message**

The application is controlled by EDM.

**Error Description**

This error code is returned when an application is controlled by Enterprise Device Manager (EDM).

**Possible Causes**

The application is controlled by Enterprise Device Manager.

**Solution**

Contact the relevant personnel of Enterprise Device Management.

## 16000015 Service Timeout

**Error Message**

Service timeout.

**Error Description**

This error code is returned when the service times out.

**Possible Causes**

The service timed out.

**Solution**

The service timed out. Please try again later.

## 16000017 Another Ability Is Being Started

**Error Message**

Another ability is being started. Wait until it finishes starting.

**Error Description**

Too many abilities need to be started. Due to limited system processing capability, requests are cached in a queue and processed in order.

**Possible Causes**

High system concurrency.

**Solution**

No action is required. Wait for the startup to complete.

## 16000018 Redirection to a Third-Party Application Is Not Allowed in API Version 11 or Later

**Error Message**

Redirection to a third-party application is not allowed in API version 11 or later.

**Error Description**

When the application API version is greater than 11, explicit redirection to other third-party applications is not allowed.

**Solution**

Use implicit startup or openLink to redirect to other applications.

## 16000019 No Matching Ability Is Found

**Error Message**

No matching ability is found.

**Error Description**

No matching ability is found during implicit startup.

**Solution**

Modify the matching items for implicit startup.

## 16000050 Internal Error

**Error Message**

Internal error.

**Error Description**

This error code is returned when internal processing errors occur, such as memory allocation or multi-threading exceptions.

**Possible Causes**

General kernel errors such as memory allocation or multi-threading issues. Possible causes include: internal objects being null, processing timeout, failure to obtain application information from package management, failure to obtain system services, or reaching the upper limit of started ability instances.

**Solution**

1. Check whether the system memory is sufficient and whether the system version used by the device is abnormal.
2. Check whether too many abilities have been started.
3. Try restarting the device.

## 16000051 Network Error

**Error Message**

Network error.

**Error Description**

This error code is returned when a network error occurs.

**Possible Causes**

The network is unavailable.

**Solution**

A network error occurred. Please try again later or reconnect to the network.

## 16000052 Installation-Free Is Not Supported

**Error Message**

Installation-free is not supported.

**Error Description**

This error code is returned when the current application does not support installation-free.

**Possible Causes**

The application package does not meet the installation-free requirements, such as exceeding the package size limit.

**Solution**

Check whether the application supports installation-free.

## 16000053 The Ability Is Not on the Top of the UI

**Error Message**

The ability is not on the top of the UI.

**Error Description**

This error code is returned when the current application is not displayed at the top of the UI.

**Possible Causes**

When performing an installation-free startup, the user needs to ensure that the application is in the foreground, but the application is not displayed at the top of the UI.

**Solution**

Check whether the current application is displayed at the top of the UI.

## 16000054 The Installation-Free Service Is Busy

**Error Message**

The installation-free service is busy. Try again later.

**Error Description**

This error code is returned when the installation-free service is busy.

**Possible Causes**

A download and installation task for the same atomic service is already in progress.

**Solution**

The installation-free service is busy. Please try again later.## 16000055 Installation-Free Timeout

**Error Message**

Installation-free timed out.

**Error Description**

This error code is returned when the installation-free operation times out.

**Possible Causes**

Installation-free operation timed out.

**Resolution Steps**

The installation-free operation timed out. Please try again later.

## 16000056 Installation-Free Not Allowed for Other Applications

**Error Message**

Installation-free is not allowed for other applications.

**Error Description**

This error code is returned when attempting to perform installation-free operations for other applications.

**Possible Causes**

Installation-free operations are not permitted for other applications.

**Resolution Steps**

Verify that the correct application is being targeted for installation-free operation.

## 16000057 Cross-Device Installation-Free Not Supported

**Error Message**

Cross-device installation-free is not supported.

**Error Description**

This error code is returned when cross-device installation-free operations are not supported.

**Possible Causes**

Cross-device installation-free operations are not supported.

**Resolution Steps**

Ensure the application is not attempting cross-device installation-free operations.

## 16000058 Invalid URI Flag Specified

**Error Message**

Invalid URI flag.

**Error Description**

The specified URI flag is invalid.

**Possible Causes**

Incorrect parameters were passed.

**Resolution Steps**

Verify that the passed parameters belong to the Uri flag.

## 16000059 Invalid URI Type Specified

**Error Message**

Invalid URI type.

**Error Description**

The specified URI type is invalid.

**Possible Causes**

Incorrect parameters were passed. Currently, URI authorization management only supports file-type URIs.

**Resolution Steps**

Verify that the passed parameters belong to the supported URI types.

## 16000060 Sandbox Application Cannot Grant URI Permission

**Error Message**

A sandbox application cannot grant URI permission.

**Error Description**

This error code is returned when a sandbox application attempts to grant URI permissions.

**Possible Causes**

Sandbox applications are not permitted to grant URI permissions.

**Resolution Steps**

Ensure the operation is performed by a non-sandbox application.

## 16000061 Operation Not Supported

**Error Message**

Operation not supported.

**Error Description**

This error code is returned when the operation is not supported on the current system.

**Possible Causes**

The operation is not supported on the current system.

**Resolution Steps**

Verify whether the operation is supported on the current system.

## 16000062 Child Process Limit Exceeded

**Error Message**

The number of child processes exceeds the upper limit.

**Error Description**

This error code is returned when attempting to create a child process while the maximum number of child processes (512) has already been reached.

**Possible Causes**

The maximum number of child processes has been reached.

**Resolution Steps**

Confirm whether the number of child processes has reached the upper limit (512).

## 16000063 Invalid Target Component for Application Restart

**Error Message**

The target to restart does not belong to the current application or is not a UIAbility.

**Error Description**

This error code is returned when the specified component name or type is invalid during application restart.

**Possible Causes**

The specified component name or type is invalid.

**Resolution Steps**

Ensure the specified component name belongs to the current application and is of type UIAbility.

## 16000064 Application Restart Too Frequent

**Error Message**

Restart too frequently. Try again at least 10s later.

**Error Description**

This error code is returned when attempting to restart an application within 10 seconds of the previous call.

**Possible Causes**

The interface was called too frequently.

**Resolution Steps**

Wait at least 10 seconds before retrying.

## 16000065 API Call Requires Foreground Ability

**Error Message**

The API can be called only when the ability is running in the foreground.

**Error Description**

This error code is returned when the Ability is not in the foreground.

**Possible Causes**

The interface was called while the Ability was not in the foreground.

**Resolution Steps**

Switch the Ability to the foreground before calling the interface.

## 16000066 Wukong Mode Restricts Ability Foreground/Background Switching

**Error Message**

An ability cannot switch to the foreground or background in Wukong mode.

**Error Description**

This error code is returned when attempting to move an Ability to the foreground/background in Wukong mode.

**Possible Causes**

Wukong mode prohibits foreground/background switching of Abilities.

**Resolution Steps**

Exit Wukong mode before attempting to move the Ability to the foreground/background. Do not perform this operation in Wukong mode.

## 16000067 Ability Startup Parameter Validation Failed

**Error Message**

The StartOptions check failed.

**Error Description**

This error code is returned when StartOptions-related parameter validation fails.

**Possible Causes**

1. When calling startAbility, if processMode is set to NEW_PROCESS_ATTACH_TO_STATUS_BAR_ITEM or ATTACH_TO_STATUS_BAR_ITEM but the application has no status bar icon, this error is returned.
2. When calling showAbility/hideAbility, if the caller was not started in NEW_PROCESS_ATTACH_TO_STATUS_BAR_ITEM or ATTACH_TO_STATUS_BAR_ITEM mode, this error is returned.

**Resolution Steps**

Verify StartOptions parameter configuration and ensure all constraints are met.

## 16000068 Ability Already Running

**Error Message**

The ability is already running.

**Error Description**

This error code is returned when the target Ability is already running.

**Possible Causes**

When calling startAbility with specified processMode and startupVisibility, if the target Ability's launchType is singleton or specified and the Ability is already running, this error is returned.

**Resolution Steps**

For Abilities with launchType singleton or specified, avoid repeated startAbility calls with processMode and startupVisibility parameters.

## 16000069 Strict Mode Prohibits Third-Party App Launch by Extension

**Error Message**

The extension cannot start the third party application.

**Error Description**

In strict mode, this Extension type cannot launch third-party applications.

**Possible Causes**

The current Extension is in strict mode, and its type prohibits third-party app launches under strict mode.

**Resolution Steps**

1. Review strict mode conditions for the Extension type.
2. Launch the Extension in non-strict mode.

## 16000070 Strict Mode Prohibits ServiceExtensionAbility Launch by Extension

**Error Message**

The extension cannot start the service.

**Error Description**

In strict mode, this Extension type cannot launch specified ServiceExtensionAbility.

**Possible Causes**

The current Extension is in strict mode, and its type prohibits ServiceExtensionAbility launches under strict mode.

**Resolution Steps**

1. Review strict mode conditions for the Extension type.
2. Launch the Extension in non-strict mode.

## 16000071 App Clone Mode Not Supported

**Error Message**

App clone is not supported.

**Error Description**

This error code is returned when the application does not support clone mode.

**Possible Causes**

Calling getCurrentAppCloneIndex in an application that does not support cloning returns this error.

**Resolution Steps**

Avoid calling getCurrentAppCloneIndex in applications that do not support cloning.

<!--Del-->
## 16000072 App Multi-Instance Not Supported

**Error Message**

App clone or multi-instance is not supported.

**Error Description**

This error code is returned when the application does not support multi-instance mode.

**Possible Causes**

Calling getRunningMultiAppInfo to query multi-instance information for an unsupported application returns this error.

**Resolution Steps**

Ensure the application supports multi-instance before calling getCurrentAppCloneIndex.
<!--DelEnd-->

## 16000073 Invalid appCloneIndex Value

**Error Message**

The app clone index is invalid.

**Error Description**

This error code is returned when an invalid appCloneIndex is passed.

**Possible Causes**

1. When calling startAbility, if the appCloneIndex carried by ohos.extra.param.key.appCloneIndex is invalid, this error is returned.
<!--Del-->
2. When calling isAppRunning, if the input appCloneIndex is invalid, this error is returned.
<!--DelEnd-->

**Resolution Steps**

Verify that appCloneIndex meets all constraints.

## 16000074 Caller Not Found for RequestCode

**Error Message**

The caller does not exist.

**Error Description**

When returning results via backTocallerAbilityResult, if the caller cannot be found using the provided requestCode, this error is returned.

**Possible Causes**

1. requestCode was not obtained from the CALLER_REQUEST_CODE field in the want.
2. The caller corresponding to requestCode has been destroyed or results have already been returned.

**Resolution Steps**

1. Verify requestCode was obtained from CALLER_REQUEST_CODE in the want.
2. Confirm whether the caller has been destroyed or results have been returned.

## 16000075 Back-to-Caller Result Not Supported

**Error Message**

Not support back to caller.

**Error Description**

This error code is returned when backToCallerAbilityWithResult is not supported.

**Possible Causes**

The current application lacks linkFeature configuration or has not passed system review.

**Resolution Steps**

1. Confirm linkFeature is configured in module.json5.
2. Ensure linkFeature values are correct, match actual functionality, and the application has passed system review.

## 16000076 Specified APP_INSTANCE_KEY Not Found

**Error Message**

The APP_INSTANCE_KEY is invalid.

**Error Description**

This error code is returned when the specified APP_INSTANCE_KEY does not exist.

**Possible Causes**

No application instance corresponds to the specified APP_INSTANCE_KEY.

**Resolution Steps**

Ensure the provided APP_INSTANCE_KEY is valid.## 16000077 Maximum Number of Application Instances Reached

**Error Message**

The number of app instances reaches the limit.

**Error Description**

This error code is returned when attempting to create additional application instances after reaching the configured maximum limit.

**Possible Causes**

Failure to check whether the current instance count has reached the application's predefined upper limit before creating new instances.

**Resolution Steps**

Adjust the maximum instance limit setting or delete existing instances before creating new ones.

## 16000078 Multi-instance Not Supported

**Error Message**

The multi-instance is not supported.

**Error Description**

The application does not support multiple instances.

**Possible Causes**

1. The target application is not configured for multi-instance operation.
2. The current device type does not support multi-instance functionality.

**Resolution Steps**

1. Configure the target application for multi-instance operation.
2. Invoke this method on 2-in-1 devices.

## 16000079 Specifying APP_INSTANCE_KEY Not Supported

**Error Message**

The APP_INSTANCE_KEY cannot be specified.

**Error Description**

This error occurs when both APP_INSTANCE_KEY and CREATE_APP_INSTANCE_KEY parameters are specified simultaneously.

**Possible Causes**

Excessive parameter input.

**Resolution Steps**

Use either APP_INSTANCE_KEY or CREATE_APP_INSTANCE_KEY, but not both.

## 16000080 Instance Creation Not Supported

**Error Message**

Creating an instance is not supported.

**Error Description**

Applications can only use CREATE_APP_INSTANCE_KEY to create their own instances. Cross-application instance creation during launch is prohibited.

**Possible Causes**

Incorrect parameter usage scenario.

**Resolution Steps**

Remove the CREATE_APP_INSTANCE_KEY parameter.

## 16000082 UIAbility in Singleton Mode Not Fully Started

**Error Message**

The UIAbility is being started.

**Error Description**

For UIAbilities with "singleton" launch mode, startup interfaces cannot be called again until the initial launch completes.

**Possible Causes**

The UIAbility is in singleton mode and currently initializing.

**Resolution Steps**

Ensure the UIAbility completes startup before initiating new launch tasks.

## 16000100 AbilityMonitor Lifecycle Monitoring Failure

**Error Message**

- Calling AddAbilityMonitor failed.
- Calling AddAbilityMonitorSync failed.
- Calling RemoveAbilityMonitor failed.
- Calling RemoveAbilityMonitorSync failed.
- Calling WaitAbilityMonitor failed.
- Calling GetCurrentTopAbility failed.
- Calling DoAbilityForeground failed.
- Calling DoAbilityBackground failed.
- Calling FinishTest failed.
- Calling AddAbilityStageMonitor failed.
- Calling AddAbilityStageMonitorSync failed.
- Calling RemoveAbilityStageMonitor failed.
- Calling RemoveAbilityStageMonitorSync failed.
- Calling WaitAbilityStageMonitor failed.

**Error Description**

This error code indicates failure in monitoring Ability lifecycle changes via AbilityMonitor methods.

**Possible Causes**

Failure to create AbilityDelegatorRegistry instance.

**Resolution Steps**

Verify successful creation of AbilityDelegatorRegistry instance.

## 16000101 Shell Command Execution Failure

**Error Message**

Failed to run the shell command.

**Error Description**

Returned when the command is not a valid shell command.

**Possible Causes**

Invalid shell command syntax.

**Resolution Steps**

Validate the shell command format.

## 16000151 Invalid wantAgent Object

**Error Message**

Invalid wantAgent object.

**Error Description**

Returned when an invalid wantAgent object is passed to the interface.

**Possible Causes**

The provided wantAgent object is malformed or corrupted.

**Resolution Steps**

Inspect the wantAgent object passed to the interface.

## 16000152 wantAgent Object Not Found

**Error Message**

The wantAgent object does not exist.

**Error Description**

Returned when the specified wantAgent object cannot be located.

**Possible Causes**

Non-existent wantAgent object reference.

**Resolution Steps**

Verify the legitimacy of the wantAgent object.

## 16000153 wantAgent Object Canceled

**Error Message**

The wantAgent object has been canceled.

**Error Description**

Returned when attempting to use a canceled wantAgent object.

**Possible Causes**

The wantAgent trigger has been explicitly canceled.

**Resolution Steps**

Check the cancellation status of the wantAgent object.

## 16100001 URI-specified Ability Not Found

**Error Message**

The ability with the specified URI does not exist.

**Error Description**

Returned when no Ability matches the specified URI.

**Possible Causes**

The queried Ability is unavailable.

**Resolution Steps**

Confirm the existence of the target Ability.

## 16100002 Incorrect Ability Type

**Error Message**

Incorrect ability type.

**Error Description**

Returned when the interface is called with an incompatible Ability type.

**Possible Causes**

The current Ability type doesn't support this interface call.

**Resolution Steps**

1. Verify the package name corresponds to the correct Ability.
2. Use appropriate interfaces based on Ability type.

## 16200001 Caller Released

**Error Message**

The caller has been released.

**Error Description**

Returned when the common component client (Caller) has been garbage collected.

**Possible Causes**

The Caller object was prematurely released.

**Resolution Steps**

1. Re-register valid common component client interfaces.
2. Verify the context's corresponding Ability is still running when calling startAbility.
3. For sequential startAbility/terminateSelf calls, ensure receiving startAbility callback before termination.

## 16200002 Invalid Callee

**Error Message**

The callee does not exist.

**Error Description**

Returned when the common component server (Callee) is invalid.

**Possible Causes**

The target Callee is unavailable.

**Resolution Steps**

Verify the existence of the common component server.

## 16200003 Release Failure

**Error Message**

Release error. The caller does not call any callee.

**Error Description**

Returned when release operation fails.

**Possible Causes**

The Caller never registered any Callee.

**Resolution Steps**

Confirm prior registration of common component server.

## 16200004 Method Already Registered

**Error Message**

The method has been registered.

**Error Description**

Returned for duplicate method registration attempts.

**Possible Causes**

The method exists in the Callee's registry.

**Resolution Steps**

Check for existing method registration.

## 16200005 Method Not Registered

**Error Message**

The method has not been registered.

**Error Description**

Returned when invoking an unregistered method.

**Possible Causes**

The method lacks Callee registration.

**Resolution Steps**

Verify method registration status.

## 16200006 Resident Process Permission Denied

**Error Message**

The caller application can only set the resident status of the configured process.

**Error Description**

Returned when lacking permissions to modify resident process status.

**Possible Causes**

Insufficient resident process configuration privileges.

**Resolution Steps**

Query caller's resident process enablement permissions from database.

## 16300001 Specified Mission Not Found

**Error Message**

Mission not found.

**Error Description**

Returned when the target mission doesn't exist.

**Possible Causes**

The operation targets a non-existent mission.

**Resolution Steps**

Confirm the mission's existence.

## 16300002 Mission Listener Not Found

**Error Message**

The specified mission listener does not exist.

**Error Description**

Returned when the target mission listener is unavailable.

**Possible Causes**

The operation references a non-existent listener.

**Resolution Steps**

Verify the listener's existence.

## 16300003 Target Application Mismatch

**Error Message**

The target application is not the current application.

**Error Description**

Returned when launching a non-self application.

**Possible Causes**

Discrepancy between calling and launched applications.

**Resolution Steps**

Ensure the launched application matches the caller.## 18500001 Specified Bundle Name Invalid

**Error Message**

The bundle does not exist or no patch has been applied.

**Error Description**

This error code is returned when the specified bundle name is invalid.

**Possible Causes**

The target bundle does not exist or is not installed.

**Resolution Steps**

Verify whether the queried application is installed.

## 18500002 Specified Patch Package Invalid

**Error Message**

Invalid patch package.

**Error Description**

This error code is returned when the specified patch package is invalid, non-existent, or inaccessible.

**Possible Causes**

The target patch package file does not exist or cannot be accessed.

**Resolution Steps**

1. Check if the provided patch package file path is valid.
2. Verify whether you have permission to access this patch package file.

## 18500003 Patch Package Deployment Failed

**Error Message**

Failed to deploy the patch.

**Error Description**

This error code is returned when patch package deployment fails.

**Possible Causes**

1. The `type` in `patch.json` must be either `patch` or `hotreload`; otherwise, deployment fails.
2. If the HAP package corresponding to `bundleName` is not installed, deployment fails.
3. `bundleName` and `versionCode` must match those of the installed HAP application. For `patch` type, `versionName` must also match; otherwise, deployment fails.
4. If a patch package has already been deployed, the `versionCode` of the new patch package must be greater than that of the previous one; otherwise, deployment fails.
5. For `patch`-type packages, signature verification is performed. The signing certificate must match that of the application; otherwise, deployment fails.
6. When deploying a `patch`-type package in debug mode, if an active patch package of `hotreload` type exists, deployment fails.
7. When deploying a `hotreload`-type package in debug mode, if an active patch package of `patch` type exists, deployment fails. In release mode, deployment fails directly.

**Resolution Steps**

Ensure the patch package complies with the rules.

## 18500004 Patch Package Enablement Failed

**Error Message**

Failed to enable the patch package.

**Error Description**

This error code is returned when patch package enablement fails.

**Possible Causes**

The patch package is in an incorrect state during enablement.

**Resolution Steps**

Check the patch package status.

## 18500005 Patch Package Deletion Failed

**Error Message**

Failed to remove the patch package.

**Error Description**

This error code is returned when patch package deletion fails.

**Possible Causes**

The patch package is in an incorrect state during deletion.

**Resolution Steps**

Check the patch package status.

## 18500006 Patch Loading Failed

**Error Message**

Failed to load the patch.

**Error Description**

This error code is returned when patch loading fails.

**Possible Causes**

The Ark engine failed to load the patch.

**Resolution Steps**

Verify the patch package correctness.

## 18500007 Old Patch Unloading Failed

**Error Message**

Failed to unload the patch.

**Error Description**

This error code is returned when the Ark engine fails to unload the old patch.

**Possible Causes**

The Ark engine failed to unload the patch.

**Resolution Steps**

Verify the patch package correctness.

## 18500008 Quick Fix Internal Error

**Error Message**

Internal error.

**Error Description**

This error code is returned for internal processing errors such as memory allocation or multithreading exceptions.

**Possible Causes**

Generic kernel errors like memory allocation or multithreading issues.

**Resolution Steps**

Ensure sufficient system memory is available.

## 18500009 Ongoing Quick Fix Task for the Application

**Error Message**

The application has an ongoing quick fix task.

**Error Description**

This error code is returned when the application has an ongoing quick fix task.

**Possible Causes**

The specified application for quick fix rollback has an active quick fix task.

**Resolution Steps**

Wait for the quick fix task to complete.

## 16300004 Specified Observer Not Found

**Error Message**

observer not found.

**Error Description**

This error code is returned when the specified observer does not exist.

**Possible Causes**

The observer does not exist or has been unregistered.

**Resolution Steps**

Check for duplicate observer unregistration.

## 16300005 Specified Package Information Not Found

**Error Message**

The target bundle does not exist.

**Error Description**

This error code is returned when the preloaded application's package information does not exist.

**Possible Causes**

Incorrect `bundleName`, `userId`, or `appIndex` for preloading, resulting in missing package information.

**Resolution Steps**

Verify the correctness of `bundleName`, `userId`, and `appIndex` parameters.

## 29600001 Image Editing Internal Error

**Error Message**

Internal error.

**Error Description**

This error code is returned for internal errors during image saving, such as memory allocation or multithreading exceptions.

**Possible Causes**

Generic kernel errors like memory allocation or multithreading issues. Specific causes may include null internal objects or timeout errors.

**Resolution Steps**

1. Ensure sufficient system memory and check for abnormal system versions.
2. Try rebooting the device.

## 29600002 Image Input Error

**Error Message**

Image input error.

**Error Description**

This error code is returned when the image URI does not exist or the image cannot be parsed.

**Possible Causes**

The URI does not exist or points to a non-image file.

**Resolution Steps**

Verify the file existence and ensure it is an image file.

## 29600002 Image Size Exceeds Limit

**Error Message**

Image too big.

**Error Description**

The input image size exceeds the limit.

**Possible Causes**

This error code is returned when the input image size exceeds 50MB.

**Resolution Steps**

1. Try reducing the image size to under 50MB after editing.
2. Validate the image size.

## 16300007 Specified Atomic Service Download/Install Task Not Found

**Error Message**

The target free install task does not exist.

**Error Description**

This error code is returned when the specified atomic service download/install task does not exist while opening a window for the atomic service.

**Possible Causes**

Incorrect `bundleName`, `moduleName`, `abilityName`, or `startTime` parameters, resulting in missing atomic service download/install task information.

**Resolution Steps**

Verify the correctness of `bundleName`, `moduleName`, `abilityName`, or `startTime` parameters.