# Camera Management (Cangjie)

Before developing a camera application, you need to create an independent camera device by calling the camera interface.

## Development Steps

For detailed API documentation, refer to the [Camera API Reference](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md).

1. Import the camera interface, which provides camera-related properties and methods. The import method is as follows:

    <!-- compile -->

    ```cangjie
    import kit.CameraKit.*
    import kit.AbilityKit.*
    import ohos.hilog.Hilog
    import ohos.callback_invoke.Callback1Argument
    import ohos.business_exception.BusinessException
    ```

2. Obtain the cameraManager object through the [getCameraManager](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-getcameramanagerabilitycontext) method.

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
    > If the object acquisition fails, it may indicate that the camera is occupied or unavailable. If occupied, you must wait until the camera is released before attempting to acquire it again.

3. Use the [getSupportedCameras](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#func-getsupportedcameras) method in the [CameraManager](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#class-cameramanager) class to obtain the list of cameras supported by the current device. The list contains all camera IDs supported by the device. If the list is not empty, each ID in the list can independently create a camera object; otherwise, it indicates that no cameras are available on the current device, and subsequent operations cannot proceed.

    <!-- compile -->

    ```cangjie
    func getCameraDevices(cameraManager: CameraManager): Array<CameraDevice> {
        let cameraArray: Array<CameraDevice> = cameraManager.getSupportedCameras()
        if (cameraArray.size > 0) {
            for (index in 0..cameraArray.size) {
                Hilog.info(0,"","cameraId : ${cameraArray[index].cameraId}")  // Get camera ID.
                Hilog.info(0,"","cameraPosition : ${cameraArray[index].cameraPosition}")  // Get camera position.
                Hilog.info(0,"","cameraType : ${cameraArray[index].cameraType}")  // Get camera type.
                Hilog.info(0,"","connectionType : ${cameraArray[index].connectionType}")  // Get camera connection type.
            }
            return cameraArray
        } else {
            Hilog.error(0,"","cameraManager.getSupportedCameras error")
            return []
        }
    }
    ```

## Status Monitoring

During camera application development, you can monitor camera status at any time, including the appearance of new cameras, removal of cameras, and camera availability. In the callback function, monitoring is performed using two parameters: camera ID and camera status. For example, when a new camera appears, it can be added to the application's backup cameras.

Register the cameraStatus event to receive monitoring results via callback. The callback returns a CameraStatusInfo parameter. For specific details of the parameter, refer to the camera manager callback interface instance [CameraStatusInfo](../../../../en/application-dev/reference/CameraKit/cj-apis-multimedia-camera.md#class-camerastatusinfo).

<!-- compile -->

```cangjie
class CameraStatusCallBack <: Callback1Argument<CameraStatusInfo> {
    public open func invoke(error: ?BusinessException,cameraStatusInfo: CameraStatusInfo): Unit {
        // When a camera device is connected via USB, the callback function returns the new camera appearance status.
        if (cameraStatusInfo.status == CameraStatus.CameraStatusAppear) {
            Hilog.info(0,"","New Camera device appear.")
        }
        // When the USB connection of a camera device is disconnected, the callback function returns the camera removal status.
        if (cameraStatusInfo.status == CameraStatus.CameraStatusDisappear) {
            Hilog.info(0,"","Camera device has been removed.")
        }
        // When the camera is turned off, the callback function returns the camera available status.
        if (cameraStatusInfo.status == CameraStatus.CameraStatusAvailable) {
            Hilog.info(0,"","Current Camera is available.")
        }
        // When the camera is opened/occupied, the callback function returns the camera unavailable status.
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