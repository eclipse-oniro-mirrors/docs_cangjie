# Flashlight Usage (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

The flashlight mode is activated by operating the terminal to enable the flashlight function, keeping the device's flashlight in a constant on state.

When using the camera application and operating the flashlight function, the following scenarios apply:

- When using the rear camera with the flash mode [FlashMode](../../reference/CameraKit/cj-apis-multimedia-camera.md#enum-flashmode) set to off, the flashlight function cannot be enabled.
- When using the front camera, the flashlight can be normally enabled and maintained in a constant on state.
- When switching from the front camera to the rear camera, if the flashlight was originally in the on state, it will be automatically turned off.

## Development Steps

For detailed API descriptions, refer to the [Camera API Reference](../../reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the camera interface, which provides camera-related properties and methods. The import method is as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.PerformanceAnalysisKit.Hilog
    import kit.CangjieKit.Callback1Argument
    import kit.CangjieKit.BusinessException
    ```

2. Use the [isTorchSupported](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-istorchsupported) method in the [CameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to check whether the current device supports the flashlight function.

    <!-- compile -->

    ```cangjie
    func isTorchSupported(cameraManager: CameraManager): Bool {
        let torchSupport: Bool = cameraManager.isTorchSupported()
        Hilog.info(0,"","Returned with the torch support status: ${torchSupport}")
        return torchSupport
    }
    ```

3. Use the [isTorchModeSupported](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-istorchmodesupportedtorchmode) method in the [CameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to check whether the specified flashlight mode [TorchMode](../../reference/CameraKit/cj-apis-multimedia-camera.md#enum-torchmode) is supported.

    <!-- compile -->

    ```cangjie
    func isTorchModeSupported(cameraManager: CameraManager, torchMode: TorchMode): Bool {
        return cameraManager.isTorchModeSupported(torchMode)
    }
    ```

4. Use the [setTorchMode](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-settorchmodetorchmode) method in the [CameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to set the flashlight mode for the current device. Additionally, use the [getTorchMode](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-gettorchmode) method in the [CameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to retrieve the current flashlight mode of the device.

    > **Note:**
    >
    > Before using the [getTorchMode](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-gettorchmode) method, you must first register a listener for flashlight state changes. Refer to [State Monitoring](#状态监听).

    <!-- compile -->

    ```cangjie
    func setTorchModeSupported(cameraManager: CameraManager, torchMode: TorchMode): Unit {
        cameraManager.setTorchMode(torchMode)
        let isTorchMode = cameraManager.getTorchMode()
        Hilog.info(0,"", "Returned with the torch mode supportd mode: ${isTorchMode}")
    }
    ```

## State Monitoring

During camera application development, you can monitor the flashlight state at any time, including flashlight on, flashlight off, flashlight unavailable, and flashlight restored to available. When the flashlight state changes, the flashlight mode change can be obtained through a callback function.

By registering the TorchStatusChange event, the monitoring result is returned via a callback. The callback returns a TorchStatusInfo parameter. For specific details of the parameter, refer to the camera manager callback interface instance [TorchStatusInfo](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-torchstatusinfo).

<!-- compile -->

```cangjie
class TorchStatusChangeCallBack <: Callback1Argument<TorchStatusInfo> {
    public open func invoke(error: ?BusinessException,torchStatusInfo: TorchStatusInfo): Unit {
        Hilog.info(0,"","onTorchStatusChange, isTorchAvailable: ${torchStatusInfo.isTorchAvailable}, isTorchActive: ${torchStatusInfo.isTorchActive}, level: ${torchStatusInfo.torchLevel}")
    }
}

func onTorchStatusChange(cameraManager: CameraManager): Unit {
    cameraManager.on(CameraEvents.TorchStatusChange, TorchStatusChangeCallBack())
}
```