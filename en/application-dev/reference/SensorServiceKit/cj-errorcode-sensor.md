# Sensor Error Codes

> **Note:**
>
> This document only introduces error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 14500101 Sensor Service Exception

**Error Message**

Service exception.

**Error Description**

This error code is reported when calling the `on`, `once`, or `off` interfaces of the sensor module if the HDI service is abnormal.

**Possible Causes**

Abnormal status when accessing the HDI service.

**Resolution Steps**

1. Retry the operation periodically, such as at 1-second intervals or with exponentially increasing intervals.
2. If the service remains unavailable after 3 consecutive retries, stop attempting. During this period, priority can be given to obtaining the device list to further determine device availability.

## 14500102 Sensor Not Supported by Device

**Error Message**

The sensor is not supported by the device.

**Error Description**

This error code is reported when calling the `GetSingleSensor` interface if the device does not support the specified sensor.

**Possible Causes**

The underlying hardware does not support the sensor, or the device lacks the necessary adaptation for the sensor.

**Resolution Steps**

1. If the `GetSingleSensor` interface returns error code 14500102, it indicates that the device does not support the specified sensor.