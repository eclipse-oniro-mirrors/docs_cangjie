# Notification Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **NOTE:**
>
> The following describes only error codes specific to this module. For details about universal error codes, see [Universal Error Codes](../cj-errorcode-universal.md).

## 801 API Not Supported by This Device

**Error Message**

Capability not supported.

**Error Description**

This API is not supported by the device and therefore cannot be called properly.

**Possible Causes**

This error code is reported when the device supports the SysCap that the API belongs to but does not support the API itself.

**Solution**

Avoid using this API on the device, or use conditional checks in the code to mitigate the impact when the application runs on different devices in unexpected scenarios.

## 1600001 Internal Error

**Error Message**

Internal error.

**Error Description**

This error code is reported when an error occurs during internal processing, such as multi-thread processing or internal pointer checks.

**Possible Causes**

Common kernel errors such as multi-thread processing and internal processing errors occur.

**Solution**

Make sure the system resources are sufficient.

## 1600002 Marshalling or Unmarshalling Error

**Error Message**

Marshalling or unmarshalling error.

**Error Description**

This error code is reported when a marshalling or unmarshalling error occurs before data transmission.

**Possible Causes**

A parameter mismatch is detected between the application and the notification service.

**Solution**

Make sure the application SDK version matches the system version.

## 1600003 Failed to Connect to the Notification Service

**Error Message**

Failed to connect to the service.

**Error Description**

This error code is reported when the application fails to connect to the notification service.

**Possible Causes**

The notification service is busy or abnormal.

**Solution**

Wait for a while and try again, or check the running status of the notification service and restart it if necessary.

## 1600004 Notification Disabled

**Error Message**

Notification disabled.

**Error Description**

This error code is reported when the notification switch is off.

**Possible Causes**

The notification switch is off for the application, or the user has rejected the notification authorization request from the application.

**Solution**

Enable the application notification switch in the notification settings.

## 1600005 Notification Slot Disabled

**Error Message**

Notification slot disabled.

**Error Description**

This error code is reported when the notification slot is disabled.

**Possible Causes**

The notification slot is disabled or has not been added.

**Solution**

1. In the notification settings, check whether the application has a slot of this type. If not, add one.

2. In the notification settings, check the status of the notification slot of this type for the application and keep it enabled.

## 1600007 Notification Not Found

**Error Message**

The notification does not exist.

**Error Description**

This error code is reported when the notification service could not find the notification.

**Possible Causes**

The notification has been canceled or deleted.

**Solution**

None.

## 1600009 Notification Sending Frequency Limit Reached

**Error Message**

The notification sending frequency reaches the upper limit.

**Error Description**

This error code is reported when the notification sending frequency reaches the upper limit.

**Possible Causes**

More than 10 notifications are sent per second, or more than 20 notifications are updated per second.

**Solution**

1. Check whether there are scenarios where the sending frequency exceeds the limit, and adjust the notification sending frequency.

2. Multiple requests can be merged, and a single notification can be updated when necessary.

## 1600012 Insufficient Memory Space

**Error Message**

No memory space.

**Error Description**

This error code is returned if a memory allocation error occurs due to insufficient memory space.

**Possible Causes**

1. The memory space is insufficient.

2. A memory allocation error occurs.

**Solution**

Ensure sufficient system memory.

## 1600013 Notification Dialog Box Already Displayed

**Error Message**

A notification dialog box is already displayed.

**Error Description**

This error code is reported when the notification dialog box is already displayed.

**Possible Causes**

The notification dialog box has been displayed.

**Solution**

Check whether the notification dialog box is displayed.

## 1600014 No Related Permission

**Error Message**

1. No permission.

2. The right of liveView is not enabled.

**Error Description**

1. The application does not have the related permission, and the API returns this error code.

2. The application publishes a third-party live view notification without applying for the live view right, and the API returns this error code.

**Possible Causes**

1. The application does not have the related permission.

2. The application has not applied for the right of the corresponding scenario.

**Solution**

1. Check whether the application has the related permission.

2. Check whether the application has applied for the live view right.

## 1600015 Duplicate Configurations not Allowed for the Current Notification Status

**Error Message**

The current notification status does not support duplicate configurations.

**Error Description**

This error code is reported when the current notification status does not support duplicate configurations.

**Possible Causes**

The current notification status does not support duplicate configurations.

**Solution**

Check whether the notification status is duplicately configured.

## 1600016 Updated Notification Version Outdated

**Error Message**

The notification version for this update is too low.

**Error Description**

This error code is reported when the notification version for this update is too low.

**Possible Causes**

The notification version for this update is too low.

**Solution**

Check the notification version.

## 1600020 Applications in the Permission Control List Are Not Allowed to Publish Notifications

**Error Message**

The application is not allowed to send notifications due to permission settings.

**Error Description**

This error code is reported when an application in the permission control list publishes a notification.

**Possible Causes**

This scenario applies only to enterprise-customized devices.

**Solution**

The application is under permission control of enterprise device management, and it cannot exit the permission control list automatically.

## 1600029 Failed to Find the ExtensionAbility for the Custom Extension Area of the Live View Widget

**Error Message**

The system failed to find the ExtensionAbility instance for the custom Live View widget template.

**Error Description**

When the application publishes a third-party live view notification, the system fails to find the ExtensionAbility instance for the custom extension area, and the API returns this error code.

**Possible Causes**

The application does not configure or incorrectly configures the ExtensionAbility for the custom extension area of the live view widget.

**Solution**

Check whether the ExtensionAbility for the custom extension area of the live view widget is correctly configured, and make sure the corresponding ExtensionAbility implementation exists.

## 2300007 Network Unavailable

**Error Message**

Network unreachable.

**Error Description**

This error code is reported when the network is unavailable.

**Possible Causes**

The device has no network connection, or the network status is abnormal.

**Solution**

Check the network connection status of the device and try again after the network is restored.
