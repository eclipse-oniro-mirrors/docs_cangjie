# Window Error Codes

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

> **NOTE:**
>
> The following introduces only the error codes specific to this module. For general error codes, please refer to the [Universal Error Code Documentation](../cj-errorcode-universal.md).

## 1300001 Repeated Operation

**Error Message**

Repeated operation.

**Error Description**

This error code is reported when performing certain repeated operations.

**Possible Causes**

Attempting to create a window that already exists will trigger this error.

**Solution**

Before creating a window, check whether it already exists to ensure it is being created for the first time.

## 1300002 Abnormal Window State

**Error Message**

This window state is abnormal.

**Error Description**

This error code is reported when operating on a window with an abnormal state.

**Possible Causes**

The window was not created or has already been destroyed when attempting to operate on it.

**Solution**

Before performing operations on a window, check its existence to ensure it has been created and not destroyed.

## 1300003 Abnormal System Service Operation

**Error Message**

This window manager service works abnormally.

**Error Description**

This error code is reported when the system service is functioning abnormally.

**Possible Causes**

The internal window service failed to start properly.

**Solution**

If the system service is malfunctioning internally, retry after a while or restart the device.

## 1300004 Unauthorized Operation

**Error Message**

Unauthorized operation.

**Error Description**

This error code is reported when attempting to operate on an object without the required permissions.

**Possible Causes**

Attempting to operate on a window object belonging to another process.

**Solution**

Check whether the operation involves objects from another process illegally and remove such operations.

## 1300005 Abnormal WindowStage

**Error Message**

This window stage is abnormal.

**Error Description**

This error code is reported when operating on an abnormal WindowStage, such as one that has been destroyed.

**Possible Causes**

The WindowStage was already destroyed when attempting to operate on it.

**Solution**

Before operating on a WindowStage, check its existence. If it has been destroyed, release the windows under this WindowStage.

## 1300006 Abnormal Window Context

**Error Message**

This window context is abnormal.

**Error Description**

This error code is reported when operating on an abnormal window context, such as one that has been destroyed.

**Possible Causes**

The window context was already destroyed when attempting to operate on it.

**Solution**

Before operating on a window context, check its existence to ensure it has not been destroyed.

## 1300007 WindowExtension Failed to Start Application

**Error Message**

Start ability failed.

**Error Description**

WindowExtension failed to start the application.

**Possible Causes**

Abnormal parameters were passed when WindowExtension attempted to start the application.

**Solution**

Check whether the WindowExtension parameters have been modified abnormally and ensure they are valid before retrying.

## 1300008 Abnormal Display Device

**Error Message**

The operation is on invalid display.

**Error Description**

The display device is abnormal.

**Possible Causes**

1. The display device is not ready.
2. The display device has been removed.
3. The display device is damaged.

**Solution**

Ensure the display device is functioning normally before proceeding with development.

## 1300009 Invalid Parent Window

**Error Message**

The parent window is invalid.

**Error Description**

The parent window is invalid.

**Possible Causes**

1. The child window is not bound to a parent window.
2. The parent window bound to the child window is abnormal (e.g., already destroyed).

**Solution**

1. Ensure the child window is successfully bound to a parent window.
2. Check the state of the parent window to ensure it is normal.

## 1300010 Invalid Operation on Fullscreen Window

**Error Message**

This operation is not support in fullscreen.

**Error Description**

Invalid operation on a fullscreen window.

**Possible Causes**

1. Attempting to move a fullscreen window.
2. Attempting to resize a fullscreen window.

**Solution**

1. Do not move a fullscreen window.
2. Do not resize a fullscreen window.

## 1300011 Failed to Destroy Picture-in-Picture Window

**Error Message**

Destroy pip window failed.

**Error Description**

Failed to destroy the Picture-in-Picture (PiP) window.

**Possible Causes**

Null pointer for the PiP window.

**Solution**

No action required.

## 1300012 Abnormal PiP Window State

**Error Message**

Abnormal state of pip window.

**Error Description**

The PiP window is in an abnormal state.

**Possible Causes**

The PiP window is in an abnormal state.

**Solution**

No action required.

## 1300013 Failed to Create PiP Window

**Error Message**

Create pip window failed.

**Error Description**

Failed to create the PiP window.

**Possible Causes**

1. Invalid parameters were passed when starting PiP.
2. Attempting to start PiP in a non-fullscreen window.

**Solution**

1. Check the parameters for starting PiP.
2. Do not start PiP in a non-fullscreen window.

## 1300014 PiP Internal Error

**Error Message**

Pip internal error.

**Error Description**

Internal PiP error.

**Possible Causes**

Internal error.

**Solution**

No action required.

## 1300015 Repeated PiP Operation

**Error Message**

Repeat operation of pip.

**Error Description**

Repeated PiP operation.

**Possible Causes**

Repeatedly starting/stopping PiP.

**Solution**

Do not repeatedly start/stop PiP.

## 1300016 Parameter Error

**Error Message**

Parameter error. Possible cause: 1. Mandatory parameters are left unspecified;<br>2. Incorrect parameter types;<br>3. Parameter verification failed.

**Error Description**

This error code is reported when the input parameter is invalid.

**Possible Causes**

1. Mandatory parameters are left unspecified.
2. Incorrect parameter types.
3. Parameter verification failed.

**Solution**

Check the input parameters to ensure that mandatory parameters are specified, parameter types match the signature, and the parameter verification rules of the API are met.

## 1001 Window Null Pointer Exception<sup>(deprecated)</sup>

**Error Message**

This window nullptr occurs.

**Error Description**

This error code is reported when operating on a window with a null pointer.

**Possible Causes**

A null pointer occurred when operating on the window.

**Solution**

Before operating on a window, check for null pointers to ensure none exist.

## 1002 Invalid Window Type<sup>(deprecated)</sup>

**Error Message**

This window type is invalid.

**Error Description**

The window type is invalid.

**Possible Causes**

An invalid window type was used. Valid window types are listed in [WindowType](../arkui-cj/cj-apis-window.md#enum-windowtype).

**Solution**

Use a window type supported by WindowType before proceeding.

## 1003 Invalid Window Parameter<sup>(deprecated)</sup>

**Error Message**

This window parameter is invalid.

**Error Description**

This error code is reported when operating on a window with invalid parameters.

**Possible Causes**

The window parameters were invalid when operating on the window.

**Solution**

Before operating on a window, check whether its parameters are valid.

## 1004 Abnormal Ability Service<sup>(deprecated)</sup>

**Error Message**

This system ability service works abnormally.

**Error Description**

This error code is reported when the ability service is functioning abnormally.

**Possible Causes**

Failed to initialize the proxy when destroying the window.

**Solution**

Restart the device if the ability service is malfunctioning.

## 1005 IPC Communication Failure<sup>(deprecated)</sup>

**Error Message**

This window IPC failed.

**Error Description**

This error code is reported when IPC communication fails.

**Possible Causes**

Window parameters failed to transmit via IPC when operating on the window.

**Solution**

Before operating on a window, ensure both the client and server services are functioning properly.

## 1007 WindowExtension Failed to Start Application<sup>(deprecated)</sup>

**Error Message**

Start ability failed.

**Error Description**

WindowExtension failed to start the application.

**Possible Causes**

Abnormal parameters were passed when WindowExtension attempted to start the application.

**Solution**

Check whether the WindowExtension parameters have been modified abnormally and ensure they are valid before retrying.