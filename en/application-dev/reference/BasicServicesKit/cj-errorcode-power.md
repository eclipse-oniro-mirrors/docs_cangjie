# System Power Management Error Codes

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 4900101 Failed to Connect to Service

**Error Message**

Failed to connect to the service.

**Error Description**

The operation failed due to an exception while connecting to the system service.

**Possible Causes**

1. The system service has stopped running.

2. An internal communication exception occurred in the system service.

**Resolution Steps**

Check whether the system service is running normally.

1. Enter the following command in the console to view the current list of system services.

    ```bash
    > hdc shell hidumper -ls
    ```

2. Check whether the PowerManagerService system service is included in the system service list.