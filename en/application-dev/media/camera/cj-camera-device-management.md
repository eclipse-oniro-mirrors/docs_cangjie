# Camera Management (Cangjie)

<!--Del-->
> **Note:**
>
> Currently in the beta phase.
<!--DelEnd-->

Before developing a camera application, you need to create an independent camera device by calling camera APIs.

## Development Procedure

For detailed API specifications, refer to [Camera API Reference](../../reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the camera interface, which provides camera-related properties and methods. The import method is as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.AbilityKit.*
    import kit.PerformanceAnalysisKit.Hilog
    import kit.CangjieKit.Callback1Argument
    import kit.CangjieKit.BusinessException
    ```

2. Obtain the cameraManager object through the [getCameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-getcameramanagerabilitycontext) method.

    For Context acquisition methods, refer to: [Obtaining UIAbility Context Information](../../application-models/cj-uiability-usage.md#获取uiability的上下文信息).

    <!-- compile -->

    ```cangjie
    func createCameraManager(context: UIAbilityContext): CameraManager {
        let cameraManager: CameraManager = getCameraManager(context)
        return cameraManager
    }
    ```

    > **Note:**
    >
    > If object acquisition fails, it may indicate the camera is occupied or unavailable. If occupied, you must wait until the camera is released before reattempting acquisition.

3. Use the [getSupportedCameras](../../reference/CameraKit/cj-apis-multimedia-camera.md#func-getsupportedcameras) method in the [CameraManager](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to obtain the list of cameras supported by the current device. This list stores all camera IDs supported by the device. If the list is not empty, each ID can independently create a camera object; otherwise, it indicates no available cameras on the current device, and subsequent operations cannot proceed.

    <!-- compile -->

    ```cangjie
    func getCameraDevices(cameraManager: CameraManager): Array<CameraDevice> {
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size > 0) {
            for (index in 0..cameraArray.size) {
                Hilog.info(0,"","cameraId : ${cameraArray[index].cameraId}")  // Get camera ID
                Hilog.info(0,"","cameraPosition : ${cameraArray[index].cameraPosition}")  // Get camera position
                Hilog.info(0,"","cameraType : ${cameraArray[index].cameraType}")  // Get camera type
                Hilog.info(0,"","connectionType : ${cameraArray[index].connectionType}")  // Get camera connection type
            }
            return cameraArray
        } else {
            Hilog.error(0,"","cameraManager.getSupportedCameras error")
            return []
        }
    }
    ```

## Status Monitoring

During camera application development, you can monitor camera status at any time, including new camera appearances, camera removals, and camera availability. In the callback function, monitoring is performed through camera ID and camera status parameters. For example, when a new camera appears, it can be added to the application's backup cameras.

Register the cameraStatus event to return monitoring results via callback. The callback returns CameraStatusInfo parameters. For specific parameter content, refer to the camera manager callback interface instance [CameraStatusInfo](../../reference/CameraKit/cj-apis-multimedia-camera.md#class-camerastatusinfo).

<!-- compile -->

```cangjie
class CameraStatusCallBack <: Callback1Argument<CameraStatusInfo> {
    public open func invoke(error: ?BusinessException,cameraStatusInfo: CameraStatusInfo): Unit {
        // When connecting a camera device via USB, the callback returns new camera appearance status
        if (cameraStatusInfo.status == CameraStatus.CameraStatusAppear) {
            Hilog.info(0,"","New Camera device appear.")
        }
        // When disconnecting a camera device via USB, the callback returns camera removal status
        if (cameraStatusInfo.status == CameraStatus.CameraStatusDisappear) {
            Hilog.info(0,"","Camera device has been removed.")
        }
        // When the camera is turned off, the callback returns camera available status
        if (cameraStatusInfo.status == CameraStatus.CameraStatusAvailable) {
            Hilog.info(0,"","Current Camera is available.")
        }
        // When the camera is opened/occupied, the callback returns camera unavailable status
        if (cameraStatusInfo.status == CameraStatus.CameraStatusUnavailable) {
            Hilog.info(0,"","Current Camera has been occupied.")
        }
        Hilog.info(0,"","camera: ${cameraStatusInfo.camera.cameraId}")
        Hilog.info(0,"","status: ${cameraStatusInfo.status}")
    }
}

func onCameraStatusChange(cameraManager: CameraManager): Unit {
    cameraManager.on(CameraEvents.CameraStatus, CameraStatusCallBack())
}
```