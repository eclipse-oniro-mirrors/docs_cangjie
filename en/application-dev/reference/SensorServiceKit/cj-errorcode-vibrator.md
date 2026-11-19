# Vibrator Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> This document only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 14600101 Device Operation Failed

**Error Message**

Device operation failed.

**Error Description**

This error code is reported when calling the startVibration, stopVibration, or isHdHapticSupported interfaces of the vibrator module if the device operation fails.

**Possible Causes**

1. The device does not have vibrator hardware connected.
2. The vibrator hardware is faulty or unavailable.
3. The underlying HDI service is abnormal.

**Resolution Steps**

1. Check whether the device supports vibration functionality.
2. Verify that the vibrator hardware is working properly.
3. Retry the operation periodically, such as at 1-second intervals or with exponentially increasing intervals.
4. If the service remains unavailable after 3 consecutive retries, stop attempting.
