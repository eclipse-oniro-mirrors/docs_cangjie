# Snapshot Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **Note:**
>
> The following describes only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 160003 Unsupported Color Space or Dynamic Range Mode in Snapshot Options

**Error Message**

Unsupported color space or dynamic range mode in snapshot options.

**Error Description**

The color space or dynamic range mode set in the snapshot options is not supported. This error code is of the string type.

**Possible Causes**

The color space or dynamic range mode value set in the snapshot options is not within the supported range.

**Resolution Steps**

Change the color space or dynamic range mode value in the snapshot options to a supported value listed in the parameter description of the corresponding snapshot API.
