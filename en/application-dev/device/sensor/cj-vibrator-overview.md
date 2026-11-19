# Vibrator Development Overview

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

By maximizing the capabilities of motor devices, the vibrator module service extends the motor service, integrating vibration with interactive design to create a unified and differentiated vibration experience, improving user interaction efficiency and ease of use.

## Working Mechanism

The Vibrator is a control-class device that includes the following four modules: Vibrator API, Vibrator Framework, Control-Class Device Service, and HDF layer.

- Vibrator API: Provides basic vibrator APIs, including vibration effect query, trigger/stop interfaces, simplifying application development.
- Vibrator Framework: Implements vibrator framework layer management and communication with the control-class device Service.
- Control-Class Device Service: Implements controller service management.
- HDF layer: Adapts to different devices.

## Constraints and Limitations

- The device must have the corresponding hardware to use the vibration function.
- To use the vibrator, configure the permission `ohos.permission.VIBRATE`. For details, see [Declaring Permissions](../../security/AccessToken/cj-declare-permissions.md).
